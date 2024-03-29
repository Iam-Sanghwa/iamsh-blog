---
emoji: 💻👨🏻‍💻
title: package.json에 대하여
date: '2024-02-29 16:55:00'
author: 상화
tags: FE study
categories: FE
---

# ✔ intro
첫 개발 프로젝트를 할 때, 아무것도 모르는 상태였지만 일단 부딪혀본다는 마음으로 남정네 일곱명이서 여기 저기 블로그를 뒤져보며 삽질만 했다. 블로그를 따라하며 개발 환경을 구축했다. '파일을 깃에 안올려도 된다고..?'라는 신기함을 선사해준,, 바로 그 package.json에 대하여 알아보자~~ :)

# ✔ Package.json이란 무엇인가!

>You can add a package.json file to your package to make it easy for others to manage and install. Packages published to the registry must contain a package.json file.
>- lists the packages your project depends on
>- specifies versions of a package that your project can use using semantic versioning rules
>- makes your build reproducible, and therefore easier to share with other developers

npm docs의 설명을 요약하자면

1. 다른 사람이 쉽게 관리하고 설치하기 쉽게하는 문서이다.
1. package를 publish하기 위해 반드시 있어야하는 문서이다.
1. 프로젝트가 의존하는 package의 리스트이다.
1. 자신의 프로젝트가 의존하는 package의 버전을 sementic versioning으로 명시해놓은 것이다.
1. 다른 개발자가 쉽게 사용할 수 있게 해주는 것이다.

# ✔ package.json의 구성요소
```
$ npm init -y
```
terminal에 'npm init -y' 명령을 입력하면 아래와 같은 package.json파일이 생성된다.
```json
{
  "name": "PROJECT_DIRECTORY",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```
여기에 나오는 요소들에 대해 알아보고, 마지막으로는 (아마도)가장 중요한 dependencies와 devdependencies에 대해 알아보자!
### ✔ "name"
"name" 필드는 패키지 설치를 위해 필수로 있어야하는 필드이다.
"name" 필드는 이름 그대로 패키지의 이름을 작성하는 것이고, 명명규칙은 아래와 같다.
- 소문자로 작성
- 한 단어로 작성
- _ 혹은 - 포함 가능

### ✔ "version"
"version" 필드 역시 "name" field와 마찬가지로 필수로 있어야하는 필드이다.
"version" 필드는 해당 패키지의 버전을 명시하는 것이고, sementic versioning guidelines를 따라 [Major, Minor, Patch]의 형식으로 작성한다.(ex. v9.2.6)

### ✔ "description"
"description" 필드는 본 패키지가 어떤 패키지인지를 설명하는 필드이다. npm에서 검색하였을 때 표시되는 부분이다.

### ✔ "main"
"main" 필드는 패키지의 진입점(entry point)을 지정하는 것이라고 되어있는데 내가 쉽게 이해한 바로는 마치 index.html과 같이 패키지를 import하면 바로 나오는 것이라고.. 이해했다.

### ✔ "scripts"
"scripts" 필드는 cli에서 자주 사용할 기능을 단축어로 지정하여 모아두는 필드이다.

scripts 필드에 dev라는 단축어를 지정하면, terminal에 npm run dev 명령을 입력하여 해당 기능을 바로 수행하게 할 수 있다!

### ✔ "keywords"
"keywords" 필드는 앞서 이야기한 "description" 필드와 유사한 역할을 한다. npm에서 검색하였을 때 리스트에 노출되어 쉽게 사용자가 필요한 패키지를 찾게 해주는 필드이다.

### ✔ "author"
"author" 필드는 배포자를 명시하는 부분이다.

한 사람이 배포를 한 경우에는 author 필드를 사용하지만, 여러 사람이 배포하였을 때는 "contributors" 필드로 작성해야 한다.

### ✔ "license"
"license" 필드는 패키지를 사용하는 사람에게 해당 패키지를 사용할 때 어떤 제한사항이 있는지 명시하는 필드이다.

### ✔ "dependencies" 와 "devdependencies"
"dependencies"필드와 "devdependencies" 필드는 모두 본 패키지가 의존하고있는 다른 패키지들과 그 패키지들의 버전을 명시하는 필드이다.

프로젝트에서 다른 패키지를 다운받으면 dependencies필드에 자동으로 해당 패키지의 이름과 버전이 기록된다.

```cli
$ npm install @mui/icons-material
$ npm install @mui/material
$ npm install -D gh-pages
$ npm install --save-dev prettier
```
위의 명령을 차례로 기입하면 네가지 패키지를 설치함과 동시에 @mui/material과 @mui/icons-material은 dependencies필드에, gh-pages와 prettier는 devdependencie필드에 이름과 버전이 기록된다.

```json
"dependencies": {
    "@mui/icons-material": "^5.1.0",
    "@mui/material": "^5.1.0"
}
"devDependencies": {
    "gh-pages": "^3.2.3",
    "prettier": "2.2.1"
  }
```
