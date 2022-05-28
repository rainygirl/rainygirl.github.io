---
layout: post
title:  "django GenericRelation 유닛테스트 수난기"
date: 2022-05-28 00:00:00
---

django 프로젝트에 큰 DB Migration을 적용한 직후부터 django Unit Test가 와장창 깨지기 시작했다. Migration에 Side Effect가 있나?하고 서버 응답을 확인해 보니 서버는 멀쩡히 돌아가고 있었다. 과거에도 Migration은 자주 했었는데 이번에만 느닷없이 유닛테스트가 실패하고 있었다. 자세히 보니 유독 GenericRelation을 사용하는 테스트 단위만 깨지고 있었다.


# 배경

이 django 프로젝트의 DB model은 간단히 요약해서 아래와 같이 구성되어 있었다.

```python
# models.py

from django.db import models

from django.contrib.contenttypes.fields import GenericForeignKey
from django.contrib.contenttypes.models import ContentType


class Person(models.Model):
    name = models.CharField(max_length=64)

class Track(models.Model):
    title = models.CharField(max_length=64)

class Video(models.Model):
    title = models.CharField(max_length=64)


class PersonRel(models.Model):
    person = models.ForeignKey('Person', on_delete=models.CASCADE, related_name='person_test')

    target_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
    target_id = models.IntegerField(null=True)
  
    target = GenericForeignKey('target_type', 'target_id')

    def __str__(self):
        return f'{self.person}, {self.target_type_id}, {self.target_type}, {self.target}'
```

실서비스가 돌아가는 서버에서는 이 모델에 아무런 문제가 없었다. shell 환경에서도 전혀 문제가 없었다. 유독, 유닛테스트 환경에서만 광범위한 오작동이 벌어졌다. 모델에 변경사항이 생긴것도 아니었다. 어째서 잘 돌아가던 유닛테스트가 한꺼번에 깨지는가? 아래와 같이 새 테스트를 추가해 실험해보았다.

```python
# test1.py
from rest_framework.test import APITestCase
from app.models import Track, PersonRel

class GenericTests(APITestCase):
    def setUp(self):
        self.http_host = 'localhost:8000'

    def test(self):
        target_item = Track.objects.get(id=1)
        print('target_item:', target_item)

        pr = PersonRel(person_id=1, target=target_item)
        pr.save()

        print('pr from instance:', pr)

        print('pr from queryset:', PersonRel.objects.last())
```

응답값은 아래와 같았다.

```
Found 1 test(s).
Creating test database for alias 'default'...
System check identified no issues (0 silenced).

target_item: <Track: 1>
pr from instance: <PersonRel: <Person: 1>, 11, app | video, <Track: 1>>
pr from queryset: <PersonRel: <Person: 1>, 11, app | video, <Video: 1>>
```

그러니까, DB Migration 이후, 모종의 이유로 유닛테스트에서 GenericRelation이 들어간 Track object가 Video object로 바뀌기 시작한 것이다. object instance는 Track으로 인식되는데 target_type은 video로 인식되고 있었다. DB에 들어갔다 나오면 Video로 바뀌어버렸다. 


# GenericRelation이란?

django 프로젝트에서 영화, 드라마, 도서 등을 담는 다양한 모델이 있다고 가정하자. 이 모든 모델에 일제히 댓글을 다는 기능을 구현할 때 DB Model을 설계 방법은 두 가지가 있다.

1. 모든 모델에 ManyToManyField 로 댓글 모델을 붙인다.
2. 댓글 모델에 GenericRelation 을 구성해 모든 모델과 연결한다.

ManyToManyField 를 사용하게 되면, 두 모델간의 관계를 정의하는 새로운 테이블이 DB에 생겨난다. GenericRelation을 사용하게 되면, 한 모델에 다른 모델타입을 담는 칼럼 하나만 추가하면 된다.

두 설계방식은 저마다의 장단점이 있다. 특히 대표적인 문제로, 만약 서로 다른 구조의 모델을 GenericRelation 에 담았다면 특정 모델에만 존재하는 필드를 prefetch로 몽땅 불러올 때 필연적으로 오류를 만나게 된다. 
여러 ORM Framework들이 [prefetch 등을 활용해 JOIN 쿼리 성능을 끌어올리는 Eager Loading을 권장하는데,](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#prefetch-related) GenericRelation에서는 이를 100% 활용하기 어렵다. 따라서 서비스를 고도화하다보면 성능 한계에 봉착해 raw SQL을 짜거나 캐시 데이터를 따로 저장하는 구조로 나아가게 된다. GenericRelation은 Django의 안티 패턴으로 여기는 의견도 있다.

> Why it's bad
> - Database design
> - Referential integrity
> - Performance
> - Django code
> - Deleting
> - Admin interface ...
>
> [Avoid Django's GenericForeignKey](https://lukeplant.me.uk/blog/posts/avoid-django-genericforeignkey/) by [Luke Plant](https://lukeplant.me.uk/blog/posts/avoid-django-genericforeignkey/)


하지만 제품 전략이 수시로 바뀌고 성능 최적화를 훗날로 미루기가 종종 권장되는 개발조직이라면, 초기단계 개발시 GenericRelation이 선호될 수도 있다. 버려진 모델과의 연결관계를 정의하는 테이블이 덕지덕지 널려있다면 그것 역시 raw SQL 을 관리하는 관점에서는 성가신 일이다. 그런 이유에서 Django와 비슷한 시기에 등장한 [Rails 역시 Polymorphic assiciations 개념을 광범위하게 활용한다.](https://guides.rubyonrails.org/association_basics.html#polymorphic-associations)
태그나 댓글 처럼 모든 모델에 걸쳐 매우 범용적으로 적용될 수 있고, 모든 레코드의 생성/수정/삭제를 잘 통제할 수 있는 경우에는 GenericRelation을 택하는 것도 아주 나쁜 선택은 아니다. 이 django 프로젝트 역시 Rails 레거시 시스템의 Polymorphic 구조와의 호환을 고려하여 GenericRelation을 광범위하게 활용하고 있었다.


# GenericRelation 작동 원리

[django는 GenericRelation을 contenttypes framework 을 통해 구현한다.](https://docs.djangoproject.com/en/4.0/ref/contrib/contenttypes/)
ContentType 은 아래와 같이 작동한다.

```python
>>> user = User.objects.get(username='Guido')
>>> t = PersonRel(target=user, person=p)
>>> t.save()
>>> t.target
<User: Guido>
>>> movie = Video.objects.get(title='Shoplifters')
>>> t = PersonRel(target=movie, person=p)
>>> t.save()
>>> t.target
<Video: Shoplifters>
```

ContentType은 django_content_type DB 테이블에 app_label과 model을 넣어두고, GenericRelation을 사용하는 모델에서 item의 id값과 item type의 id값을 동시에 넣어 모든 모델을 ForeignKey처럼 당겨올 수 있게 한다. DB를 열어보면 django_content_type 테이블은 아래와 같이 생겼다.

```sql
mysql> select * from django_content_type;
+----+-----------+----------+
| id | app_label | model    |
+----+-----------+----------+
|  1 | admin     | logentry |
|  4 | auth      | user     |
| 11 | app       | person   |
| 12 | app       | track    |
| 13 | app       | video    |
...
```
위 조건에서 PersonRel은 아래와 같이 들어갔을 것이다.
```sql
mysql> select * from app_personrel;
+----+----------------+-----------+-----------+
| id | target_type_id | target_id | person_id |
+----+----------------+-----------+-----------+
|  1 | 4              | 1         | 1         |
|  2 | 13             | 1         | 1         |
+----+----------------+-----------+-----------+
```

즉 두 칼럼값을 참조하여 object의 model type을 결정하는 것이다. target_type_id 가 바뀌거나 django_content_type가 바뀌면 object의 model type이 바뀔 것이다. 위 유닛테스트에서는 target_type_id 가 바뀌지 않았다.


# 오작동의 원인을 찾아서

깨진 유닛테스트에서는 DB에 넣은 Track object가 Video object로 바뀌어 응답되고 있었다. type_id 값이 바뀌는 것은 아니었다. object를 DB에 넣기 전과 DB에서 다시 꺼낼 때 인식되는 model type이 서로 달랐다.
원인을 찾기 위해 새로 빈 유닛테스트를 아래와 같이 구성했다.

```python

from django.contrib.contenttypes.models import ContentType
from app.models import Track

from rest_framework.test import APITestCase

class TestTests(APITestCase):
    def setUp(self):
        print(
            'ContentType.get_for_model Track Instance : ',
            ContentType.objects.get_for_model(Track),
            ContentType.objects.get_for_model(Track).id,
        )
        ctid = ContentType.objects.get_for_model(Track).id
        print(
            f'ContentType.get           id={ctid} Instance : ',
            ContentType.objects.get(id=ctid),
            ContentType.objects.get(id=ctid).id,
        )
        print(
            'ContentType.get from get_for_model(Track): ',
            ContentType.objects.get(id=ContentType.objects.get_for_model(Track).id),
            ContentType.objects.get(id=ContentType.objects.get_for_model(Track).id).id,
        )
    def test(self):
        pass
```

이 코드의 수행 결과는 아래와 같이 찍혔다.

```
Creating test database for alias 'default'...

ContentType.get_for_model Track Instance :  music | track 11
ContentType.get           id=11 Instance :  music | video 11
ContentType.get from get_for_model(Track):  music | video 11
```

그러니까, `ContentType.objects.get_for_model()` 에서 테스트 DB와는 다른 값을 내놓은 것이다. get_for_model()은 캐시를 활용한다. 테스트 코드 상단에 하나의 코드를 더 추가해보았다.

```python
        ContentType.objects.clear_cache()
```
결과는 아래와 같이 찍혔다.

```
Creating test database for alias 'default'...

ContentType.get_for_model Track Instance :  music | track 11
ContentType.get           id=11 Instance :  music | track 11
ContentType.get from get_for_model(Track):  music | track 11
```

더는 object의 model type이 바뀌는 현상이 발생되지 않았다.


# ContentType 의 캐싱

`manage.py test` 로 테스트를 돌리게 되면 django는 test 데이터베이스를 따로 만들게 된다. `test_` prefix가 붙은 데이터베이스를 새로 만들고, migrations를 참조해 새로운 테이블을 DB에 잠시 만든다. django_content_type 테이블도 최신 migrations를 참조하여 최신 버전으로 생성된다.

개발환경의 django_content_type 테이블 데이터는 이전의 레거시가 겹겹이 쌓여 생겨났다. 사라진 모델의 content type 레코드는 id를 차지했다가 버려진 상태이다. 테스트 환경의 django_content_type 테이블은 가장 최신의 환경을 기준으로 새로 깔끔한 id가 매겨져있다. 사라진 모델의 content type 레코드는 만들지 않는다. 즉 개발환경의 django_content_type 테이블의 id값과 테스트 환경의 django_content_type 테이블의 id값이 다를 수 있다.

ContentType은 GenericRelation으로 object 를 넣고 꺼낼 때마다 django_content_type 테이블에 담긴 각 모델의 type_id값을 알아야 한다. 특히 다량의 SELECT 쿼리로 가져온 object 들의 model type을 알기 위해 매번 DB query를 보내는 것은 좋은 방법이 아닐 것이다. 그래서 [object의 타입을 결정하는 `ContentType.objects.get_for_model` 은 관련 데이터를 ContentTypeManager 클래스의 캐시에 담아 응답한다.](https://github.com/django/django/blob/main/django/contrib/contenttypes/models.py)

ContentType의 캐싱은 `ContentTypeManager._add_to_cache` 에서 담당한다. 이 코드는 `django.contrib.contenttypes.models` 안에 있다. 테스트 데이터베이스로 전환되기 전 캐시가 생성되는 것은 아닌지 확인하기 위해, django 코드를 잠시 열고 다음과 같이 `ContentTypeManger._add_to_cache` 가 호출될 때마다 어느 데이터를 읽는지 print를 찍어보았다.

```python
def _add_to_cache(self, using, ct):
    key = (ct.app_label, ct.model)
    print(key)    # new line

    self._cache.setdefault(using, {})[key] = ct
    self._cache.setdefault(using, {})[ct.id] = ct
```

manage.py test를 돌려보니 결과는 다음과 같이 찍혔다.

```
('app', 'track')
('app', 'person')
('app', 'video')

Found 103 test(s).
Creating test database for alias 'default'...
('admin', 'logentry')
('auth', 'permission')
('auth', 'group')
('auth', 'user')
..중략..
('app', 'track')
('app', 'person')
('app', 'video')
```

그러니까, 테스트 데이터베이스로 전환되기 전 기존 DB 데이터를 기준으로 어디에선가 ContentType 캐시가 생겨난 것이다. 


# 해결

대충 메꿔버리자 하고 models.Manager를 바꿔보기도 하고, model의 save() 를 뜯어보기도 했다. 잠시 차를 마시고, 바람을 쐰 뒤, 머리를 식히며 천천히 생각해보다 django의 ContentType 구동원리를 떠올렸다. 역시 [소프트웨어 엔지니어는 규칙적으로 휴식을 취해야 한다.](https://rainygirl.github.io/2021/11/pomodoro-room-light-timer)

서버 가동과정에서 ContentType 캐시를 일부러 만드는 코드가 있었다. 전혀 엉뚱한 곳에 있던 django management command 의 환경설정 코드였다. 서버 가동 단계에서부터 ContentType을 조회하게끔 구현했었다. django의 test runner는 지정된 모든 app 의 코드를 돌며 기본적으로 체크할 테스트 코드를 찾아내는데, 이 과정에서 여러 코드를 로드하게 되고, 그 과정에서 ContentType 캐시가 먼저 만들어졌고, 그 다음에 테스트 데이터베이스로 전환된 것이었다. 유닛테스트 과정에서는 테스트 데이터베이스와는 전혀 다른 ContentType이 응답되고 있으니 강아지가 고양이로 변할 수 밖에 없었을 것이다. 그전까지는 개발환경의 django_content_type 테이블 id가 테스트 환경의 새 테이블 id와 다르지 않아 문제가 되지 않았는데, 최근의 DB Migration 이후 django_content_type 테이블의 id가 재배열되면서 이 문제가 수면 위로 드러났다.

test runner의 코드 조회 때 ContentType을 호출하지 않도록 해당 코드를 서버 가동 단계에서 command handle 실행 단계로 옮겼다.
코드를 옮긴 이후에는 모든 유닛 테스트가 이전처럼 잘 작동하였다.

