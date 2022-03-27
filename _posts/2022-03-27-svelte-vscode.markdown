---
layout: post
title:  "Svelte + vscode : launch.json 설정하기"
date:   2022-03-27 00:00:00
---

이번 회사 프로젝트에서 Svelte를 쓰고 있다. 한번 익혀보겠다고 실험적으로 써본거였는데 밑도끝도없이 일이 커져 이제는 되돌릴 방법이 없어졌다.

회사에서 Django/Python 작업을 할 땐 PyCharm 을 사용하고, Svelte/Typescript 작업을 할 땐 Visual Studio Code 를 사용한다. 언어/프레임워크별로 IDE 도구를 바꾸고 테마까지 다르게 설정하면 컨텍스트 스위칭의 피로도가 줄어들고 집중도가 높아지는 편이다. 

PyCharm 은 익숙하지만 vscode는 여전히 모르는게 많은데 Run 돌리는게 여간 불편한게 아니었다. 알아서 `yarn run dev` 돌린 뒤 개발하라는 메뉴얼밖에 없었는데, JetBrain 계열 IDE와 Django/Python 쪽 문서에 익숙해져서인지 이런 가이드는 불친절하다는 느낌이 들었다. 터미널 여는거야 쉽지...터미널을 열었다간 vscode 돌려놓고 vim을 돌리기 일쑤였다. 그러니 vscode 에서 뭐든 다 할 수 있는 환경을 갖출 필요가 생겼다.

Visual Studio Code 는 각종 설정을 `.vscode` 폴더에 담는다. Run 쪽 설정은 `.vscode/launch.json` 에서 고칠 수 있다.
나는 Svelte 프로젝트에서 아래와 같이 설정해둔다.

```json
{
    "version": "0.1.0",
    "configurations": [
        {
            "type": "pwa-node",
            "request": "launch",
            "name": "yarn run dev",
            "cwd": "${workspaceRoot}",
            "runtimeExecutable": "yarn",
            "runtimeArgs": ["run", "dev"],
            "trace": true
        },
        {
            "type": "chrome",
            "request": "launch",
            "name": "Launch Chrome",
            "url": "http://localhost:3000",
            "webRoot": "${workspaceFolder}"
        }
    ]
}
```
Run 에서 `yarn run dev` 를 누르면 서버가 켜지고 `Launch Chrome` 을 누르면 Chrome 브라우저가 열린다. 서버 debug console을 볼 필요가 없다면 `"trace": true` 를 제거하면 된다.


