---
layout: single
title: "내일배움캠프 팀프로젝트1 Find TeamMate"
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
