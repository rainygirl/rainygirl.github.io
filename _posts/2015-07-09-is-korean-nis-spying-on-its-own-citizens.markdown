---
layout: post
title:  "해킹팀 스캔들 - 5163부대는 당신이 무엇을 하고 있는지 알고 있다"
date:   2015-07-09 00:00:00
---

지난 7월 6일, 이탈리아의 스파이웨어 개발업체 &#8216;Hacking Team(HT)&#8217; 이 해킹되어 400 기가 가량의 내부 자료가 몽땅 토렌트로 유출되었다. 이 회사에서 유출된 자료에는 소프트웨어 소스코드는 물론, 직원의 개인정보나 퇴직 직원들의 사직서 내용에다 연봉수준이나 보너스순위 같은 민감한 인사정보까지 담겨져 있었다. 

그러나 해외 언론들이 주목한 이유는 따로 있었다. 유출된 자료에는 **이 스파이웨어 회사로부터 감청장비를 구매한 각국 기관들, 특히 정부기관들에 대한 모든 정보가 담겨져 있었던 것이다.**

* [[Wall Street Journal] Hacking Team, the Surveillance Tech Firm, Gets Hacked](http://www.wsj.com/articles/hacking-software-maker-gets-hacked-1436223757)
* [[the guardian] Hacking Team hacked: firm sold spying tools to repressive&#8230;](http://www.theguardian.com/technology/2015/jul/06/hacking-team-hacked-firm-sold-spying-tools-to-repressive-regimes-documents-claim)
* [[ZDNet] Hacking Team hit by breach; leak suggests it sold spyware to oppressive regimes](http://www.zdnet.com/article/hacking-team-hit-by-breach-files-suggest-it-sold-spyware-to-oppressive-regimes/)
* [[WIRED] Hacking Team Breach Shows a Global Spying Firm Run Amok](http://www.wired.com/2015/07/hacking-team-breach-shows-global-spying-firm-run-amok/)
* [[VERGE] Hacking Team spyware company hacked, embarrassing emails revealed](http://www.theverge.com/2015/7/6/8899861/hacking-team-hacked-security-leak)

그리고 WIRED UK등의 매체를 통해, 이 업체의 소프트웨어를 구매한 고객 중 &#8220;한국도 포함되어 있다&#8221;는 보도가 나오기 시작한다.

> (공개된) 파일을 통해 “해킹팀”의 고객 중에 **한국**, 카자흐스탄, 아제르바이잔, 사우디 아라비아, 레바논, 이집트, 나이지리아, 수단이 포함된 걸로 밝혀졌다.
>
> Files reveal that Hacking Team customers include **South Korea**, Kazakhstan, Azerbaijan, Saudi Arabia, Lebanon, Egypt, Nigeria and Sudan.
>
> &#8211; [[WIRED UK] Hacking Team's oppressive regimes customer list revealed in hack
](http://www.wired.co.uk/news/archive/2015-07/06/hacking-team-spyware-company-hacked)


> 일요일 저녁 유출된 내부 문서에 따르면 해킹팀은 현재 다음의 고객을 보유하고 있다. 이집트, 에티오피아, 모로코, 나이지리아, 수단, 칠레, 콜롬비아, 에콰도르, 온두라스, 멕시코, 파나마, 미국, 아제르바이잔, 카자흐스탄, 말레이시아, 몽골, 싱가포르, **한국**, 태국
> Hacking Team currently has, based on internal documents leaked by the attackers on Sunday evening, customers in the following locations: Egypt, Ethiopia, Morocco, Nigeria, Sudan, Chile, Colombia, Ecuador, Honduras, Mexico, Panama, United States, Azerbaijan, Kazakhstan, Malaysia, Mongolia, Singapore, **South Korea**, Thailand&#8230;
>
> &#8211; [[CSO Online] Hacking Team hacked, attackers claim 400GB in dumped data](http://www.csoonline.com/article/2943968/data-breach/hacking-team-hacked-attackers-claim-400gb-in-dumped-data.html)


그리고 7월 9일 새벽 3시, 이 시각까지도, **한국의 어느 메이저 언론들도 이 사건을 보도하지 않고 있다.** 지금까지 이 사건을 언급한 국내 매체는 작은 보안전문 인터넷뉴스 [보안뉴스](http://www.boannews.com/media/view.asp?idx=46922)라는 곳과 [전자신문](http://www.etnews.com/20150707000291)이 유일하다. 게다가 전자신문은 첫 보도부터 익명의 전문가를 빌어 &#8216;인권침해로 해석하는건 무리가 있다&#8217;며 물타기를 시도했다. **과연 그럴까? 그동안 한국 정부와 이 업체 사이에서 무슨 일이 벌어졌던 것일까?**

그래서 HT로부터 유출된 자료를 직접 모두 확보해보았다.

# Hacking Team 의 고객, 한국 5163부대

다음 장표는 유출된 자료 중 아래 문서에 기록된 내용이다.

> [Client Overview_list_20150603.xlsx](http://ht.transparencytoolkit.org/Amministrazione/01%20-%20CLIENTI/5%20-%20Analisi%20Fatturato/2015/02%20-%20Client%20Overview%202015/Client%20Overview_list_20150603.xlsx)

> ![-](/images/2015-07-09-ht-doc-1.png)

이탈리아 스파이웨어 업체 HT 과 거래한 미국 기관으로는 당장 FBI 라는 이름이 보인다.
한편 **South Korea**, 한국의 기관명도 눈에 띄는데, &#8216;**The 5163 Army Division**&#8216;, 즉 &#8216;**5163부대**&#8216;로 기재되어있다.

**HT는 한국 &#8216;5163부대&#8217;로부터 2012년부터 총 686,400 유로를 받았다고 문서에 기록되어 있다.**

> ![-](/images/2015-07-09-ht-doc-2.png)

> ![-](/images/2015-07-09-ht-doc-3.png)

* 2012년 라이센스 구입 등 소프트웨어 도입비용으로 448,000 유로
* 2013년 유지보수비용으로 58,850 유로
* 2014년 업그레이드 및 유지보수 비용으로 145,700 유로
* 2015년 유지보수 비용으로 33,850 유로

7월 9일 공시환율 1유로 = 1,253원을 적용하면 **한국 &#8216;5163부대&#8217;는 약 8억 6천만원 가량의 국가예산을 이탈리아 스파이웨어 업체에 지급했다**는 것이 문서의 내용이다. 그러면 8억 가량의 국가예산으로 이 한국 부대는 무엇을 구매했다는 것일까? 이는 &#8216;청구서&#8217;에 기재된 내용을 통해 쉽게 확인할 수 있다. 유출된 자료들 중 Invoice &#8211; 003_2015 &#8211; Army Division Korea.pdf 등등의 자료에 의하면 다음과 같다.

> ![-](/images/2015-07-09-ht-doc-4.png)

&#8216;**Remote Control System**&#8216; 이라고 기재되어있다. 언뜻 보면 네이트온 PC원격제어처럼 보이는 이 소프트웨어의 실체는 사실 &#8216;**감청 프로그램**&#8216;이다. 이에 대한 내용은 난데없이 위키리크스(Wikileaks)에서 발견된다.

> ![-](/images/2015-07-09-wikileaks-leaked-docu-rcs.png)
>
> [Wikileaks, 31_200810-ISS-PRG-HACKINGTEAM.pdf](https://wikileaks.org/spyfiles/files/0/31_200810-ISS-PRG-HACKINGTEAM.pdf)


스텔스-스파이웨어 기반으로, 컴퓨터와 스마트폰을 공격, 감염, 감시할 수 있는 시스템으로, 표적 사용자의 암호화된 통신 (스카이프 등 메신저나 보이스톡, PGP 암호 커뮤니케이션, 암호화된 웹메일 등) 까지 모두 감시할 수 있는 시스템이라는 것이 이 회사의 소개이다. 심지어 이 회사는 동영상 광고까지 제작하여 업체 홈페이지에 올려두었다.

<iframe src="https://www.youtube.com/embed/-hNqTobYylI" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>
> *한글 번역은 필자가 붙인 것이다*

대략 이런 걸 만드는 스파이웨어 개발회사 HT 와 한국 &#8216;5163부대&#8217;가 거래를 한 것이다.

유출된 자료 중 **RCS 8 Technical.pptx** 에 따르면 이 회사가 감시 가능하다고 밝힌 서비스는
스카이프, 지메일, 페이스북, 트위터 등이다.

> [RCS 8 Technical.pptx](https://ht.transparencytoolkit.org/rcs-dev%5cshare/Documentation/Presentations/RCS%208%20Technical.pptx)

> ![-](/images/2015-07-09-ht-doc-5.png)

보이스톡, 이메일, SNS가 모두 감청 가능하다는 이야기이다. 물론 한국 국가정보원이 구글 지메일을 감청하더라는 의혹은 한겨레 2011년 9월 보도를 통해 한차례 제기된 바 있다.

> ![-](http://i0.wp.com/www.mediaus.co.kr/news/photo/201109/19663_37805_181.jpg?resize=300%2C519)
>
> [한겨레] 구글 지메일도 국정원이 감청, 2011. 9. 6.

당시 기술적 어려움 때문에 이것이 어찌 가능하겠냐는 것이 당시 한겨레 보도의 주된 내용이었다. 하지만 네트워크단계에서 인증서 바꿔치기, PC에 감시소프트웨어 설치하기 등과 같은 방법이 이미 있기 때문에 불가능한 일은 아니었다. 그리고 그 다음해 이 업체와의 거래가 시작되면서, 관련 시스템 구축 작업이 본격 시작된 것으로 보인다.

# 무엇을 감청하겠다는건가?

한국 &#8216;5163부대&#8217;가 구매한 HT의 RCS 에서 구현 가능하다는 감청 항목은 다음과 같다. 다음은 유출된 자료중 **RCS_9.1_Features_Compatibility_v1.2.pdf** 파일에 기재된 내용이다.

> [RCS_9.5_Features_Compatibility_v1.0.pdf](http://ht.transparencytoolkit.org/rcs-dev%5cshare/Documentation/Compatibility%20List/RCS_9.5_Features_Compatibility_v1.0.pdf)

데스크탑의 경우 **캠 카메라를 통한 도촬, 마이크를 통한 도청, 채팅, 파일 확보, 키보드 입력, 패스워드, 접속 사이트, 스크린샷 **등&#8230; 획득이 가능하다.

> ![-](/images/2015-07-09-ht-doc-6.png)
 

모바일의 경우 **폰 카메라를 통한 도촬, 마이크를 통한 도청, 위치 정보, 스크린샷** 등&#8230; 획득이 가능하다.

> ![-](/images/2015-07-09-ht-doc-7.png)


또한, 같은 자료에서 밝히기를 운영체제의 종류와 버전에 따라 각기 지원하는 기능이 조금씩 다르기는 하지만, 데스크톱과 모바일 모두 특정 프로그램 원격 실행, 기록, 설치 삭제 및 정보 무단 삭제가 가능하다는 것이 “해킹팀”의 설명이다.

> ![-](/images/2015-07-09-ht-doc-8.png)

> [Compatibillity List (not for customers).9.6.xlsx](http://ht.transparencytoolkit.org/rcs-dev%5cshare/Documentation/Compatibility%20List/Compatibility%20List%20%28not%20for%20customers%29.9.6.xlsx)

“해킹팀”의 “리모트 컨트롤 시스템”이 감염시킬 수 있는 데스크톱·스마트폰 환경에는 어떤 것들이 있을까. 위의 기능 소개 문서에도 나와 있지만 편집할 수 있는 표로 잘 기재한 문서도 있다.



* Android 는 2.2 (Froyo) 부터 5.0 (Lolipop) 까지 감청이 가능하다고 한다.
* iOS 는 3.x부터 8.x 까지 감청이 가능하다고 한다.
* Blackberry 는 4.5부터 7.1까지 감청이 가능하다고 한다.
* Mac OS는 10.6 (Snow Leopard) 부터 10.10 (Yosemite)까지 감청이 가능하다고 한다.
* Windows는 XP부터 10 까지 감청이 가능하다고 한다.
* Linux 또한 Ubuntu, Debian, Linux Mint, Fedora 등이 모두 감청이 가능하다고 한다.

> ![-](/images/2015-07-09-ht-doc-9.png)
> 
> *x가 감시 가능하다는 표시이다*

# 무슨 수로 감청이 가능하다는 이야기인가?

HT 가 전세계 국가정보기관과 금융권 등에 판매한 이 RCS 는 앞서 소개한바와 같이 본질적으로 &#8216;스파이웨어&#8217;이다. 즉 감청할 표적에게 이 스파이웨어를 심어야 작동하는 구조이다. HT 역시 네트워크 패킷감청만으로는 부족하다며 RCS 도입을 호소한다. 다음은 위키리크스에 이미 공개된 바 있는 HT측 프레젠테이션 자료중 일부이다.

> [31_200810-ISS-PRG-HACKINGTEAM.pdf](https://wikileaks.org/spyfiles/files/0/31_200810-ISS-PRG-HACKINGTEAM.pdf)

> ![-](/images/2015-07-09-ht-doc-10.png)

이런저런 수단을 써서 스파이웨어를 심으라는 이야기이다. 그렇다면 어떻게 이 스파이웨어를 배포해야할까? 이에 대한 HT 의 가이드는 RCS.pdf, RCS 9 Attack Vectors.pptx 등의 문서에서 확인된다.


> [RCS 9 Attack Vectors.pptx](http://ht.transparencytoolkit.org/rcs-dev%5cshare/Documentation/Presentations/RCS%209%20Attack%20Vectors.pptx)

* **USB와 CD-ROM를 몰래 꽂아 부팅시켜라**
* **메모리카드를 꽂아라**
* **WIFI망 라우터를 조작하라**

USB와 CD-ROM을 몰래 넣어 부팅시키는 방식은 요원을 침투시키거나 장비 압수수색후 반환시점에 작동시키는 등의 방식으로 실행이 가능할 것이다. 실제로 모로코가 이 시스템을 담은 USB를 UN 사무국 컴퓨터에 꼽아 UN 평화유지군을 해킹한 사실도 발각되었다.

* [[allafrica] Morocco Seems to Have Hacked UN Computers With Hacking Team Technologies](http://allafrica.com/stories/201507080731.html)

WIFI망 라우터를 조작하라는 가이드는 한국의 여러 인터넷 공유기 펌웨어가 조작되어 피싱사이트로 연결되었던 과거 사례를 떠올리면 원리를 쉽게 이해할 수 있다.

여기에다 HT가 제시하는 또다른 침투방법이 몇가지 더 있다.

> ![-](/images/2015-07-09-ht-doc-12.png)

* **인터넷 서비스 제공자(ISP)를 통제하라**
* **모바일 서비스 제공자(3G/LTE)를 통제하라**
* **인터넷을 통해 EXE나 APK를 실행시켜라**

인터넷 서비스 제공자는 우리가 흔히 알고있는 SK브로드밴드, KT, LG U+와 같은 인터넷 케이블 사업자를 말한다. 모바일 서비스 제공자 역시 SKT, KT, LGU+와 삼성전자와 같은 단말기사업자를 의미한다. 이들을 통제하여 특정 유저의 PC나 스마트폰에 가짜 자동업데이트를 보내어 스파이웨어를 자동 설치토록 하는 것이다. HT 는 이 방법을 동종업계인** gammagroup.com** 의 가이드 문서와 동영상까지 가져와다가 상세히 가이드하고 있다. 유출된 자료 중 **309_GAMMA-201110-FinFly_ISP.mp4** 라는 동영상은 더 적나라하다.

> 309_GAMMA-201110-FinFly_ISP.mp4
<iframe width="560" height="315" src="https://www.youtube.com/embed/4zSo3dZnTDk" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

동영상을 보면 ISP의 서버실에 요원을 침투시켜 핀플라이 ISP(FinFly ISP)를 심어둔다. (동영상의 요원은 경찰이라 쓰인 옷을 입고 있다) 그런 후 네트워크 접속을 가로챈 후 감시 표적에게 가짜 아이튠스 업데이트를 보내라는 것이다.

> ![-](/images/2015-07-09-finfly-isp.jpg)

원격 자동업데이트와 자동실행을 통해 스파이웨어를 심고, 이를 통해 원격제어로 PC를 망가트린 사례는 이미 2013년 3월 20일 사이버테러 사건 때 한국의 KBS, MBC, YTN, 신한은행, 농협 등이 겪은 바 있는 그 공격방식이다.

> ![-](/images/2015-07-09-nonghyup.jpg)
>
> *역시 북한 소행으로만 덮어졌을 이 사건의 전모는 결국 중앙보안관제시스템 해킹이 원인인 것으로 밝혀졌다*

한국은 알약과 같은 백신, 알집과 같은 압축프로그램, 곰플레이어 같은 각종 동영상 플레이어에 온갖 인터넷뱅킹 보안소프트웨어(ActiveX부터 EXE까지)가 계속 자동업데이트되고 있는 국가이기 때문에, 네트워크를 통한 원격 침투에 가장 최적화된 환경을 갖추고 있는 국가다. **게다가 이미 관련 기술적 조치를 법제화하기 위한 &#8216;[통신비밀보호법개정안](http://likms.assembly.go.kr/bill/jsp/BillDetail.jsp?bill_id=PRC_D1D5O0L6U0L1D1R9P4Z0L1M1M2D4B6)&#8216;이 국회에 제출되어있기도 하다.** 이 개정안의 핵심은 통신사 또는 SNS 운영업체로 하여금 감청설비 설치를 의무화하고, 이를 거부할 경우 처벌토록 하는 것이다.

> 통신비밀보호법 일부개정법률안 (박민식의원 대표발의)
>
> 의안번호 15387
>
> 발의연원일 : 2015. 6. 1.
>
> 발의자 : 박민식 이한성 김태환 김성찬 황진하 김광림 홍일표 권성동 안효대 여상규 경대수 이채익 의원(12인)
>
>
> 제15조의2제1항 중 "전기통신사업자는"을 "**전화, 인터넷, SNS등** 대통령령으로 정한 통신 서비스 역무를 담당하는 전기통신사업자(이하 "전기통신사업자"라 한다)는" 으로 하고, 같은 조 2항을 다음과 같이 하며, 같은 조에 제3항부터 제6항까지를 각각 다음과 같이 신설한다.
>
> ..중략..
>
> ② 제1항의 규정에 따른 *전기통신사업자는 통신제한조치의 집행을 위하여 감청협조설비를 갖추고 운용해야 한다.*
>
> ③ 제2항에 따른 **감청협조설비는 대통령령으로 정하는 기준․방법 및 절차에 적합하여야** 한다.
>
> ④ 제3항에 따른 **통신사업자의 감청협조설비 비용은 대통령령으로 정하는 바에 따라 국가가 부담한다.**
>
> ..중략..
>
> 제15조의3 및 제15조의4를 각각 다음과 같이 신설한다.
>
> 제15조의3(이행강제금) ① 미래창조과학부장관은 제15조의2제2항을 위반하여 **감청협조설비를 갖추지 아니한 전기통신사업자에 대하여 1년 이내의 기간을 정하여 감청협조설비 구축 의무를 이행할 것을 명할 수 있다.**
>
> ② 미래창조과학부장관은 제1항에 따른 이행명령을 받은 전기통신사업자가 시정기간 내에 당해 **시정명령을 이행하지 아니한 경우에는 대통령령으로 정하는 매출액의 100분의 3 이하에 해당하는 금액을 이행강제금으로 부과할 수 있다**

유출된 자료 중 RCS 7.3 &#8211; Administration Manual.pdf 등 RCS의 메뉴얼에 따르면, 여러 방식으로 공격을 통해 스파이웨어 에이전트가 설치된 뒤, 네트워크를 통해 지속적으로 감청 정보가 전송되며, 네트워크에 접속되어 있지 않더라도 (스마트폰 데이터네트워크를 끄더라도) 지속적으로 데이터를 수집한 뒤, 네트워크에 연결되는 시점에 다시 모아 전송토록 하고 있다.

> [RCS 7.3 – Administration Manual.pdf](http://ht.transparencytoolkit.org/rcs-dev%5cshare/DELIVERY/Countries%20Operations/TURKEY/TNP/Documentation/RCS%207.3%20-%20Administration%20Manual.pdf)

전송되는 경로 또한 익명화시켜 어디로 전송되는지 알 수 없도록 구현되어있다는 것이 HT 의 설명이다. 에이전트가 설치된 PC에 문제의 감시에이전트는 평소 PC이용자가 자주 사용하는 프로그램과 아주 비슷하게 생긴 프로세스를 보거나 프로세스를 확인조차 할 수 없다는 설명도 곁들여져있다.** &#8216;악성코드&#8217;가 하는 바로 그 짓이다.**

> ![-](/images/2015-07-09-ht-doc-13.png)

시스템 구축을 통해 국가기관은 전국민을 대상으로 다음과 같은 감시화면을 운영할 수 있게 된다.


# 실제 RCS 의 구동 스크린샷

> ![-](/images/2015-07-09-ht-doc-14.png)

감시 표적의 현재 위치가 지도에 표시되고, 감시 표적이 현재 스마트폰이나 PC로 하고 있는 일, **누구와 어떤 전화통화를 하는지, 보이스톡으로 무슨 대화를 나누었는지, 폰카메라에 잡힌 풍경은 어떠한지, 마이크에 잡힌 대화내용은 무엇인지, 페이스북에서 누구와 대화하고 있는지**까지 모두 한 곳에서 확인이 가능하다. 영화에서나 보던 그 장면이 이제 현실이 된 것이다. 노동조합 파업 회의를 왜 사측이 미리 알아챘을까? 카카오톡 대화내용을 왜 정보과 형사가 알고있을까? 우리는 상상속에서만 떠올리던 답을 이제 눈 앞에서 실제로 마주하고 있는 것이다.


# 한국 &#8216;5163부대&#8217;는 어디인가?

서울 서초구에 위치한 &#8216;5163부대&#8217;는 (강남서초송파예비군훈련장이 아니라) 이미 그 실체가 시사in 2013년 11월 기사를 통해 밝혀진 바 있다.

> ‘7452부대’와 함께 **국정원이 사용하는 위장 명칭은 또 있다. ‘5163 부대’이다.** 5163부대와 7452부대는 국정원 직원들이 은행 대출을 받거나 외부 기관에 재직증명서를 낼 때도 사용된 이름이다. 한 시중은행 관계자는 “5163부대라고 재직증명서에 적혀 있어서 군무원인 줄 알았는데, 주소지가 국정원과 같은 내곡동이었다”라고 말했다.
>
> &#8211; [[시사인] 국정원의 대외용 이름 ‘5163부대’](http://www.sisainlive.com/news/articleView.html?idxno=18454)

그렇다. 바로 서초구 내곡동에 있는 **국가정보원**이다.
인보이스 사업자번호 **229-83-00055** 역시 **국가정보원의 위장 사업체 ['세기문화사'](http://www.hani.co.kr/arti/society/society_general/598823.html)**의 사업자번호이다.

> ![-](/images/2015-07-09-nis.jpg)
>
> *로고가 뭔가 좀 이상하지만 기분 탓이다.*

어찌하여 지구 반대편 이탈리아 스파이웨어 개발업체 HT는 이런 시스템을 정말 간절히 원할법한 한국 정보기관이 평소 쓰던 위장명칭 &#8216;5163부대&#8217; 이름을 정확하게 알고있었을까? 심지어 납품업체 이름까지?


# 사건 3일째, 왜 아무런 취재도 없는 것일까?

유출된 400 기가 가량의 자료는 이미 토렌트를 통해 전세계로 널리 배포되고 있다. 토렌트로 퍼지는 이상 이 데이터는 절대 삭제되지 않고 영원히 인터넷을 떠돌게 될 것이다. 아예 유출 내용을 인터넷에서 바로 확인할 수 있는 미러 사이트도 등장했다. 심지어 프로그램 소스 코드까지 계속해서 올라오고 있다.


* [reddit – Torrent magnet for the dump (마그넷)](https://www.reddit.com/r/HackedTeam/comments/3caimp/torrent_magnet_for_the_dump/)
* [ht.transparencytoolkit.org (미러 사이트)](http://ht.transparencytoolkit.org/)
* [GitHub “HackingTeam” Repository (소스 코드)](https://github.com/hackedteam?tab=repositories)

모든 자료가 이렇게 버젓이 드러난 상황에서도 왜 한국 언론에는 아무런 보도도 나오고 있지 않을까? **간단하다. 그토록 쫓는 외신이 이토록 시끄러운데도, 이 사안의 본질에 대해 모르거나, 아니면 보도할 수 없거나. 둘 중 하나일 것이다.**

이 글이 공개된 이후부터 한국 언론들이 이 사안을 어떻게 보도할지, 진실을 어디까지 더 캐낼 수 있을지 지켜볼 때이다. 그리고 과연, 한국 국가정보원 원장이, 혹은 국가정보원의 최종 보고를 받을 한국 정부의 최고 수장이 이 사건을 어떻게 해명할지 지켜볼 때이다.


# 누구를, 누구를 위해 감시하려 했을까?

당장 우리의 궁금증은 여기로 모아져야한다. 국가정보원이 이 시스템을 활용하여 누구를 감시하려 했을까? 인터넷이 연결되어있지 않은 북한의 누군가일까? 아니면 국내의 누군가일까? 국내의 누군가라면 어떤 이유에서일까?


지출 내역을 다시 보자.

* **2012년 라이센스 구입 등 소프트웨어 도입비용으로 448,000 유로**
* 2013년 유지보수비용으로 58,850 유로
* **2014년 업그레이드 및 유지보수 비용으로 145,700 유로**
* 2015년 유지보수 비용으로 33,850 유로

- - -

## 2012년

한국 &#8216;5163부대&#8217; 가 이 소프트웨어를 구매했다는 2012년 당시 국정원장은 원세훈이었다.

2012년, HT가 한국 &#8216;5163부대&#8217;, 즉 국가정보원으로부터 소프트웨어 도입 비용으로 448,000 유로를 받았다는 그 해에는 이런 일이 있었다.

> ![국정원 댓글부대, 2012년 대선 개입](https://s2.dmcdn.net/v/Lg0aX1RJWUeP_58bB/x1080)

2012년 당시 국정원장은 이 SNS 계정들과 관련하여 재판에까지 넘겨졌었다.

* [뉴스타파 – “국정원 사유화 바로잡아야”…원세훈에 징역 4년 구형](http://newstapa.org/13458)
* [뉴스타파 – 원세훈 대선개입 구속..’지록위마’ 판결 뒤집어](http://newstapa.org/23300)

그해 &#8216;5163부대&#8217;, 즉 국가정보원에게 HT가 착수금 273,000 유로 등 총 448,000 유로를 청구했다. 한화로 약 5억 6천만원 가량의 국가예산이다.

> ![-](/images/2015-07-09-s1.png)
>
> *273.000,00 EUR*

그리고 이런 일도 있었다.

* [[경향신문]축하전화 받는 박근혜 당선인](http://news.khan.co.kr/kh_news/khan_art_view.html?artid=201212202335331&code=910110)


- - -

## 2014년

한국 &#8216;5163부대&#8217; 가 업그레이드 및 유지보수 비용으로 145,700 유로를 지불했다는 2014년 그 해에는 이런 사건이 있었다.

> ![-](/images/2015-07-09-2848415_90.jpg)
> 
> *세월호 참사*

당시 여객선 세월호 침몰사고 검경 합동수사본부는 [SNS 괴담 유포를 엄단하겠다](https://www.yna.co.kr/view/AKR20140418077000054)고 했고, 국정원은 다음카카오에 감청영장 집행을 시도했으며, '카톡 감청'을 피한다며 '사이버망명'이라는 이야기가 나돌기 시작했다.

그해 HT는 한국 &#8216;5163부대&#8217;, 즉 국가정보원에게 업그레이드 명목으로 78,000 유로 등 총 145,700 유로를 청구했다. 한화로 약 2억 가량의 국가예산이다.

> ![-](/images/2015-07-09-s2.png)
>
> *78.000,00 EUR*

이 모든 것들이 그저 우연으로 맞아떨어졌던 것일까?

이것은 합법일까? 아니면 불법일까?

**이 사이버무기를 전세계 각국 정부기관들은 어떻게 활용해왔을까? 그리고. 한국 &#8216;5163부대&#8217;는 과연 어떻게 활용해왔을까?
그리고, ISP 감청설비 설치 의무화 법안 = 통신비밀보호법 개정안이 통과된 이후 우리의 인터넷은 어떻게 될까?
과연 내 PC 와 스마트폰에도 감시 에이전트가 스며들까?**

- - -


# p.s.

1. 유출된 소스코드를 전세계 언론들이 분석한 결과, HT 는 그동안 OS의 버그든, Adobe Flash 의 버그든 여러 종류의 제로데이공격 취약성 버그를 이용해 시스템 관리권한을 탈취하고 기기를 원격 제어하도록 시스템을 구현한 것으로 확인되었다.
  ( [[the Register] KILLER! Adobe Flash, Windows zero-day vulns leak from Hacking Team raid](http://www.theregister.co.uk/2015/07/07/hacking_team_zero_days_flash_windows_kernel/) )
  관련 취약성이 마구 밝혀질 예정이기 때문에 앞으로 수많은 서버 혹은 PC/스마트폰들이 공격에 노출될 지도 모른다. 당분간 관련 소식을 주의깊게 살펴보는 것이 좋겠다.
2. 이와 함께, 전세계 언론들이 유출된 자료에 포함된 이메일 데이터를 분석한 결과, HT는 감시 표적의 데이터를 파트너와 고객(=국가정보기관)과 함께 공유하며 지속적으로 공격 및 침투기법을 발전시켜온 것으로 보인다. 이메일 데이터에 대한 더 많은 분석이 필요하다. 각국 정세에 대한 분석 메일까지 유출된 만큼, HT와 한국 기관이 서로 주고받은 이메일도 곧 밝혀지리라 생각한다. 누군가 본래 사명에 따라 조금만 더 노력한다면.
  > ![-](/images/2015-07-09-b01.png)
  >
  > *HT가 고객과 주고받은 이메일, high value target 은 누구일까?*


