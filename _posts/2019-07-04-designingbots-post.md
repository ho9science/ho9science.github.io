---
title: "책리뷰:봇 설계는 이렇게 한다"
date: 2019-07-04 00:00:01
categories: review
tag: 봇설계 챗봇 시나리오 봇기획
---

# 봇 설계는 이렇게 한다 - 다양한 봇으로 알아보는 대화형 서비스 만들기 (Designing bots - Creating conversational experiences)

모두들 챗봇 만들고 있습니다. 형태소 분석기 라이브러리 가져다 붙이고 단순히 DB에 질의하는 간단한 것부터 오픈소스 검색 엔진 붙이고 그래프 DB에 질의하거나 word2vec을 사용하거나 azure, watson 등 클라우드를 사용하는 등 봇을 만들기 위해 고군분투하고 있습니다. 이 책은 봇을 막 만드려는 사람 또는 막 만들기 시작한 사람을 위한 책입니다. 새로운 인터페이스인 봇을 제대로 기획할 수 있는 길을 제시해줍니다. 인터페이스의 한 형태인 봇을 기획하는 것이기 때문에 대화관리, 문맥 등 자연어 처리와 관련된 문제들은 분량이 적지만 브랜딩 등 봇의 인터페이스를 정의하고 사용자들에게 더 나은 경험을 주기 위해서 읽어봐야 할 내용들입니다. 

## 봇이란 무엇인가?
봇은 새로운 사용자 인터페이스입니다.
대화형 인터페이스를 통해 서비스를 제공하는 새로운 방법입니다. 챗봇, 대화형 에이전트, 대화형 인터페이스, 채팅 에이전트 모두 봇입니다.

## 봇 사용 사례
* 대화형 상거래 : 아마존 구매, 여행봇, 우버, 쇼핑 등
* 비즈니스 : 인사, 법률, 마케팅, 엔지니어링, 제품 등 기업 내 업무 흐름에 봇을 사용하는 사례
* 생산성 및 코칭 : 알림과 할 일 목록, 작업관리, 다이어트, 육아, 스포츠 등 개인용 코치 봇
* 경고/알림 봇 : 뉴스 봇, 가격 감시 봇, 분석 보고서 봇 등
* 사람 사이를 연결하는 봇 : 
* 고객 서비스 및 FAQ 봇 : 가장 일반적인 사용 사례. 질문에 대한 대답을 할 수 있다.
* 게임 및 엔터테인먼트 봇 : 사용자를 즐겁고 기쁘게 하는 목적이 있는 봇
* 브랜드 봇 : 신제품 알림이나 할인 알림 같은 봇

## 봇 만들기 

### 브랜딩, 성격 및 사람의 개입
#### 성격
성격은 대화하고자 하는 대상의 유형, 완료해야 하는 일의 유형, 봇을 연관시키고자 하는 브랜드에 적합해야 합니다.
#### 로고와 아이콘
로고와 아이콘을 사용하면 사용자가 봇을 식별할 수 있고 인간과 유사한 속성을 의미하여 브랜드 인지도에 도움이 됩니다.
#### 이름
봇의 이름은 브랜드와 연결되기 때문에 강한 감정적 연결고리를 갖거나 다양한 의미를 가질 수 있습니다.
#### 사람의 개입
초기에 봇의 대답을 검토하고 오류를 처리할 필요가 있습니다.

### 인공지능
인공지능은 대화의 최적화 및 봇 인터랙션의 다양한 측명을 가능하게 함으로 서비스 성공의 열쇠가 될 수 있습니다.
#### 자연어 이해
의도를 이해하고 주요 변수를 추출하는 기능
#### 대화관리
복잡하고 다양한 의도가 담긴 대화를 관리하는 기능 
#### 이미지인식
사진 인식할 수 있는 기능
#### 예측
질문에 대한 올바른 답 또는 대화 중 특정 시간에 취할 행동을 예측하는 기능
#### 심리분석
대화의 감정을 이해하는 기능

### 대화
#### 온보딩
온보딩은 사용자가 봇에서 처음 마주하는 인터랙션입니다. 온보딩은 사용자에게 보여 줄 봇의 첫인상을 설정하고 처음 대화를 수행할 때의 작업을 처리합니다. 
* 봇의 목적 선언하기
* 사용자에게 봇 사용법 가르치기
* 봇의 말투와 성격 결정하기

#### 기능 스크립팅
업무 중심과 주제 중심의 두가지 방식의 대화를 기획합니다.
- 업무 중심 대화
시작부터 완료까지 흐름을 만들고 추가적인 흐름을 붙여서 이상적인 경로 흐름을 만들 수 있습니다.
* 흐름 분기와 코스 교정 : 예상치 못한 반응이 나올 경우, 코스를 교정하는 경우 또는 사람이 개입하는 방법이 있습니다.
* 개체 추출 : 대화에서 추출해야 하는 개체의 집합을 정의하고 나열해야합니다. 개체들의 우선순위와 허용 가능한 데이터 유형도 지정해야합니다.
* 의도 매핑과 대화형 컨트롤 : 사용자는 선택 가능한 항목돌을 살펴보고 원하는 것을 선택할 수 있도록 해야합니다. 
* 작업 전환 : 작업을 새로 시작하거나 홈으로 돌아갈 수 있는 기능
* 약칭 : 컨트롤의 복잡성을 줄일 수 있다. 사용자가 원하는 것을 단순히 서술하여 모든 개체를 추출하고 탐색하는 과정을 거칠 필요가 없습니다.
* 스토리 : 시나리오 기반으로 각각의 스토리를 캡술화하거나 분리하여 어떤 스토리를 효과적으로 사용했는지 학습하거나 대화를 관리하기 쉽습니다.
* 대화 퍼넬 : 웹사이트에서 전환 퍼넬을 통과하는 방법과 유사한 방식

**좋은 업무 주도형 대화는 대화 흐름을 통해 사용자를 파악하고 전환율을 최적화하는데 도움을 줍니다.**

-주제 중심 대화 
일련의 주제를 정의한 다음 이 주제를 둘러싼 대화를 촉진시키는 것이 중요합니다.

### 데코레이션 
대화에 깊이를 더하고 기계와 대화하고 있는 느낌을 최소화 하는 문장에 추가하는 단어들로 대화의 성격에 영향을 줍니다.
* 랜덤화 : 확인이나 동의 같은 대화에서 반복적인 내용을 랜덤화하여 사용자를 흥미롭게 합니다.
* 올바른 정보 유도하기 : 프리이밍, 대화를 최적화하고 사용자가 형식에 맞게 올바르게 말하도록 유도하는 방법
* 승인 및 확인 : 사용자의 입력과 입력의 정확성을 확인합니다.
* 반응성: 봇은 절대 사용자를 무시하면 안됩니다.
* 일관성: 대화는 정상적인 흐름과 오류 흐름 모웨서 일관되고 친절해야 합니다.
* 상호호혜성 : 입력을 툐청하기전에 가치를 전달하기
* 질문 및 제안으로 참여 유도하기 
* 적극성
* 예의 

#### 피드백과 에러처리
대화를 기억하는 것은 봇의 실수로부터 학습하는 과정입니다.
사용자를 기획된 대화 흐름으로 끌어들이거나 봇의 오류를 해결하기 위해 사람과 연결시키거나 다른 봇으로 연결하는 방법

#### 도움말 및 지원
사용법을 가르치거나 도움말 흐름을 통해 사용자의 올바른 선택을 유도합니다.

### 리치 인터랙션
리치 인터랙션은 대화를 간단하고 직접적으로 더욱 풍부하게 만들 수 있습니다.
봇은 파일, 오디오 및 비디오, 이미지, 지도, 링크, 이모티콘, 슬래시명령, 웹뷰 등을 지원해야 합니다.
#### 버튼 
버튼은 키보드를 대체하여 사용자의 선택을 제한하여 올바른 응답으로 이끕니다. 응답을 유도하지 않아도 대화의 방향을 잡을 수 있습니다.
#### 템플릿
템플릿은 여러 다른 UI 요소들을 미리 형식화되고 표준화된 방법으로 보여주는 방법을 말합니다. 공통 요소들의 표준화를 돕고 사용자 경험을 예측할 수 있게 합니다.
#### 타이핑 표시
봇이 입력하고 있는 것처럼 꾸밀 수 있어 봇의 존재감을 나타낼 수 있습니다.

### 문맥(context)과 기억(memory)
대화의 문맥을 추론하고 대화의 상태를 유지하고 이전 대화의 중요한 사항들을 기억할 필요가 있습니다.
봇은 가능하다면 문맥을 제거해서는 안됩니다. 문맥을 유지하여 사용자가 대화를 시작하면 잠시 후에 다시 시도할 수 있어야 합니다.
* 의도트리 탐색 : 의도에는 고유한 문맥이 있지만 일부 의도는 중첩될수 있습니다.
* 대명사에서 문맥 추론하기 : 자연어 이해(NLU)영역으로 복잡하고 다양한 의도가 있는 문맥을 이해하고 추론하는 기능
* 리치컨트롤 사용 : 리치컨트롤을 사용하면 의도를 보다 명확하게 파악할 수 있습니다.
