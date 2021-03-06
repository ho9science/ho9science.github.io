---
title: "책리뷰:알고리즘라이프 - 일상 속 스마트한 선택을 위한"
date: 2019-02-23 00:00:01 
categories: review
tag: 책리뷰 알고리즘 생활알고리즘
---

# 알고리즘라이프 - 일상 속 스마트한 선택을 위한

생활 속에서 알고리즘을 적용하는 여러 사례를 소개하면서 알고리즘의 기본 개념을 강의하는 책입니다. 알고리즘 입문자 및 초급자에게 굉장히 좋은 책이라는 생각이 듭니다. 일상의 다양한 사례들을 통해 컴퓨팅적 사고를 어떻게 적용해 볼 수 있을지 생각해볼 기회가 될 것 같습니다. 책을 읽고 각 장의 중요 키워드를 정리해 보았습니다. 각 키워드의 내용을 잘 알지 못하거나 생활 속에서 어떻게 적용하여 문제를 풀어나가는지 궁금하신 분들께 추천해 드립니다. 

## 01 산더미처럼 쌓인 양말 짝을 맞춰라
> 짝없는 양말을 미리 한쪽에 늘어놓았기 때문에 빨래 더미에서 어떤 양말인지 아닌지 알 수 있는 방법은 검색표(lookup table) 즉 캐시(cache) 덕분이다.
식별자들 각각이 데이터 연관항목을 가리키고 우리는 그 항목에서 키의 값을 검색하는 방법을 키값 짝짓기(key-value pair)라고 한다.

* 배열(array)의 경우 찾고 있는 것이 배열의 제일 끝일 경우 전체를 찾아야 한다.
* 배열 검색의 대안으로 연관배열(associative array) 혹은 사전(dictionary), 해시표(hash table)라고 불림
	* 해시표는 집합에 데이터를 보관한다는 점에서 배열과 정확히 똑같지만 순서를 따르지 않고 거의 즉각적인 검색을 함, 상수기간(constant-time)검색
	* 상수기나 검색은 작업을 수행하면서 전체 항목을 다시 반복(iterate)할 필요 없어질 때 가능
	* 해시함수(hash function)
		
## 02 폭탄세일 셔츠를 담아라
* 많은 물건 중 하나의 물건을 찾고 있는데 찾는 물건을 발견할 때까지 모든 물건을 다 살펴봐야 하는 상황 : 선형시간(linear time)
* 선형함수(linear function)에서 100개 중의 한 개를 찾는 데 1분이 걸린다면 200개 중에서는 2분이 걸림을 예상 가능하다
* 로그시간(logarithmic time): 물건이 정렬된 경우, log는 지수의 역
* 이진검색(binary search): 정렬된 물건 중 무엇을 로그적으로 찾는 방법, 선형검색(linear search)보다 월등히 낫다

## 03 장보기 횟수를 최소한으로 줄여라
* 데이터구조(data structure), 추상데이터타입(abstract data type)의 작동방식은 특성을 극대화하여 사용가능
* 스택(stack), 상위에 있는 항목을 보는 것에 관심(peaking), 스택에서 항목을 꺼내는 것(popping), 추가(push)
	* 웹사이트에서 뒤로 가기를 누르게 된다면 스택에서 하나씩 꺼내는 것
	
## 04 빠르게 미로를 탈출하라
* 무작위로 이동하는 쥐(random mouse): 무작위로 이곳저곳 가는 방식
* 벽따라가기, 오른손법: 벽을 따라가는 방법
* 역추적(backtracking): 막다른 곳에서 온 길로 되돌아가는 방법
* 네트워크(network), 그래프(graph): 제한된 환경에서 한 지점에서 다른 지점으로 이동한다는 개념
	* Edge(선)는 미로의길, vertex(정점)는 교차로
	
## 05 쏟아진 우편물을 주소에 따라 저장하라
* 이차시간(quadratic-time)알고리즘: 정렬하는데 걸리는 시간이 n^2시간이 걸림-> 삽입(insertion), 선택(selection), 거품(bubble)
* 이차미만시간 정렬(subquadratic), 분할정복법(divide and conquer), 선형로그시간(linearithmic), 이차시간보다 빠르고 선형시간보다 느리다. 항목들의 집합을 더 작은 집합으로 쪼갠후에 그 집합들을 정렬하는 방식
* 선형로그 알고리즘 : 병합정렬(merge sort), 빠른정렬(quick sort)

## 06 위대한 음악가들을 정복하라
* 링크분석(link analysis): 어떤 자질을 공통으로 가지고 있는 것들의 집합이 있다면 그들의 관계를 분석하는 것, 인용수
* 연결정도(degree), 유사성(similar)
* 행렬복합(matrix multiplication): 
* 자카드지표(Jaccard index)

## 07 SNS에서 관심받을 만한 상태 메시지를 업로드하라
* 수행시간 복잡도(run-time complexity): 상대적 속도
* 공간 복잡도(space complexity): 메모리나 디스크 공간
* tree diagram
* 허프만 부호화
	
## 08 연말 송년회 전에 모든 잔업을 끝마쳐라
* 문맥전환(context switching)
* -파이프라이닝(pipelining): 한 명령이 끝나기 전에 다른 명령 실행하는 것
* interrupt handler: 진행 중인 프로세스를 일시적으로 중단시키고 필요한 데이터를 넘기거나 우선순위를 낮추는 방법
* 탐욕적 방법(greedy approach): 이미 성취한 작업의 수를 최대한으로 늘리고자 하는 방법
* 데이크스트라 알고리즘: 최단 거리
* 패턴 맞추기(pattern matching): 하나의 패턴에 맞는 것이 본문 텍스트에 있는지 찾는 방법
* 우선순위 대기열(priority queue)
	
## 09 수제 이니셜 목걸이를 고쳐라
* 링크(link)
* 연결리스트(linked list): 삽입과 삭제를 효율적으로 처리,작업과작업사이 넣을 때
* 이중연결리스트(doubly linked list) 

## 10 분리수거장에서 택배용 빈 상자를 찾아라
* 빅세타표기법(big-theta notation): 상한계와 하한계를 가진 함수
* 빅오메가: 하한계가 있는 함수
* 빅오: 상한계가 있는 함수


## 11 저자의 이름순으로 책장을 정리하라
* 도서관정렬(library sort), 간격 삽입정렬(grapped-insertion sort)

## 12 마트에서 최대한 빠르게 필요한 물건만 쓸어 담기
* 어떤 배열에 문자열literal 대신 다른 배열을 저장하면 행렬이 된다
* 2차원배열, 다차원배열(multidimensional array)
* 해시함수 충돌(collision)
* 부하율(load factor), 해시표의 점유율
* 연쇄화(chaining)
* 우선순위 대기열
* 이진검색트리(binary search tree): 모든 마디의 순위가 정해져 있는 구조
