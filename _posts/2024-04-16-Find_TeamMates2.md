---
layout: single
title: "내일배움캠프 팀프로젝트1 Find TeamMate 2일차"
permalink: /2024/04/16/Find_TeamMates2/
tags: [Unity, 내일배움캠프, 스파르타내일배움캠프, 카드게임]
---

# 오늘 진행한 내용:
## 베이스+추가 기능 5가지 구현 추가:

### 2-1 매칭 성공 시, 팀원의 이름 표시 / 실패 시 실패 표시 (종료 시 끝! 나타나는 것처럼)
  1. Board class에 ownerNames에 이름들 배열로 추가(인스팩터창에서 수정), Start에 카드들 생성할 때 각 카드에 이름 넣어줌
  2. Card class에서 string ownerName 을 두고 여기에 받은 이름을 저장
  3. GameManager class에 public Text matchTxt; 를 넣어서 실패, 성공시 이름 뜨는 text칸 구현.
  4. 그 다음 GameManager.Matched() 함수에서 matchTxt.text = firstCard.ownerName;를 넣어서 성공시 이름 출력, matchTxt.text = "실패!"; 를 넣어서 실패로 변경

### 2-2 클릭할 때(카드 뒤집을 때), 시작할 때, 진행 중일 때 성공, 실패 소리 넣어보기
  1. 클릭시는 Card class에서 OpenCard에 audio 재생
  2. 시작할 때는 기존대로 게임 시작시 AudioManager에서 시작
  3. 진행중 매칭 성공시 GameManager.Matched()에서 audioSource로 clip 1회 재생
  4. 실패시도 동일

### 2-3 타이머 시간이 촉박 할 때 게이머에게 경고하는 기능 작성해보기(시간이 붉게 변하거나 긴박한 배경음악으로 변경)
  1. GameManager class에서 Update()에서 time >= 20 이고 bgmNotChanged == True이면 실행
  2. camera background 색을 Color.red로 바꾸고
  3. audioManager의 audioSource를 bgmSource로 받아서 긴박한 음악으로 clip을 바꿔주고 Play 시킴

### 2-4 한 번씩 뒤집은 카드는 색을 다르게 표시하기 (옅은 회색 등)
  1. Card class에서 OpenCard()를 실행시 해당 Card prefab의 Back 이미지의 color를 Color.gray로 변경

### 2-5 결과에 매칭 시도 횟수 표시
  1. GameManager class에 matchCount 변수를 두고
  2. Matched() 함수가 불릴 때 마다 그 안에서 matchCount++; 로 증가
  3. EndGame() 함수가 불리면 endtext.text = "끝\n시도횟수: " + matchCount.ToString(); 로 시도횟수 출력. 끝 텍스트 사이즈를 조금 줄임

# 일지
팀원들 각자 맡은 부분을 만들고 시간이 남으면 다른 부분도 만들기로 하였는데, 각자 모든 부분을 구현하고나니 깃으로 모을수가 없었다. 충돌 위험이 당연히 있고 다들 깃 사용법에도 익숙하시지 않아서 결국 한명이 만든 내용을 뽑아서 그걸 베이스로 main에 올리고 다시 그걸 기본으로 다들 끌어와서 작업하기로 했다.
그리고 앞으로는 각자 맡은 부분만 수정하고 rebase나 branch 생성 등 내일 들을 깃 특강을 듣고나서 모두 이해가 되면 merge 진행을 하기로 했다.
추가로 각자 기능을 구현하고나니 배운 것이 모두 생각하는 구현방법이나 구현 결과가 달랐다. 방식이 다른것이야 그래도 코드방식이 다른것이니 어쩔수 없지만 구현 결과가 다른 것은 와이어프레임을 짜라고 되어있던 계획서가 있는 이유를 이해할 수 있었다.
와이어프레임으로 게임 구현 완료시 어떻게 생겼는지를 정확하게 생각 해놓아야지 다음에 구현을 각자 완료했을 때 서로 생각한 구현 결과가 달라서 혹시모를 충돌이나 의견 충돌이 생길 것을 방지할 수 있을 것이다.
그래서 이제부터 구현할 때는 최소한 어떻게 구현할지 함께 모여서 생각을 하기로 했다.
