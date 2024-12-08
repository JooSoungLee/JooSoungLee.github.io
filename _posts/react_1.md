---
title:  "[React] 리액트 개발환경 만들기"
excerpt: "리액트 개발환경을 만들어보자"

categories:
  - Blog
tags:
  - [Blog, React, Github, Git, md]

toc: true
toc_sticky: true
 
date: 2024-12-08
last_modified_at: 2024-12-08
---
# 리액트의 개발환경 세팅하기
프론트앤드의 최고 대세 리액트 개발환경을 세팅해 보자

## 1. node.js 설치
1. https://nodejs.org/ -> Download -> Prebuilt Installer -> Download Node.js 클릭하여 설치. 별도의 옵션변경 필요 없이 다음다음 눌러서 진행하면 된다.
![K-001](https://github.com/user-attachments/assets/bef8c9c0-f30b-4a9a-bc5b-931aff21e5bd)
2. 명령 프롬프트(cmd) -> node -v 명령어로 정상 설치되었는지 확인. 버전정보가 조회되면 정상 설치된 것이다.
![K-003](https://github.com/user-attachments/assets/42977051-ae8f-419c-aba4-34d6a52ed927)

## 2. Visual Studio Code 설치
1. https://code.visualstudio.com/ -> Download for Windows 클릭하여 설치. 별도의 옵션변경 필요 없이 다음다음 눌러서 진행하면 된다.
![K-002](https://github.com/user-attachments/assets/2b31206a-4a1c-49fd-8c30-d337b84ecada)


## 3. 리액트 프로젝트 생성
```npm
cd [프로젝트 경로]
npx create-react-app [프로젝트명]
```
1. 명령어 실행
![K-006](https://github.com/user-attachments/assets/bf2e9298-7877-4e9a-b44a-0d5399ad2235)

2. 명령어 결과
![K-007](https://github.com/user-attachments/assets/849c0651-bae5-4929-9667-2442c4450767)

3. 명령어를 실행한 폴더에서 프로젝트가 생성된 것을 볼 수 있다.
![K-008](https://github.com/user-attachments/assets/d6de5422-7db8-4cca-aa28-d4fcfb15b7ef)

## 3. 프로젝트 실행
1. Visual Studio Code 실행 -> File -> Open Folder... -> 프로젝트 폴더 선택
![K-009](https://github.com/user-attachments/assets/b9991bfd-2fd2-4165-9b25-ead56bc94666)

2. Terminal -> New Terminal
![K-010](https://github.com/user-attachments/assets/ee0c64e4-6f18-4e6e-ac70-03275048f587)

3. 터미널에서 npm start
![K-011](https://github.com/user-attachments/assets/484cb150-c669-4df0-8fd0-ea7bc98bd697)
![K-012](https://github.com/user-attachments/assets/2742e83e-8070-4971-ae3f-2bcf9bfd3fea)

4. http://localhost:3000 웹 사이트 확인
![K-013](https://github.com/user-attachments/assets/0b9fd08a-d8b8-4cfc-98b3-364166ea9345)


리액트 웹 프로젝트 생성 성공~!
