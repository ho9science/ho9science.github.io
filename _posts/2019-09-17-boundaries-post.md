---
title: "8장: 경계"
date: 2019-09-17 01:01:11
categories: cleancode
tag: 클린코드 개발
---

## 외부 코드 사용하기
java.util.Map을 살펴보자. Map은 굉장히 다양한 인터페이스로 수많은 기능을 제공하지만 위험도 크다.
제네릭스를 사용하여 코드 가독성을 높인다.
```
Map<String, Water> waters = new HashMap<String>();
Water w = waters.get(waterId);
```
다음은 좀 더 깔끔한 코드이다.
```
public class Waters{
	private Map waters = new HashMap();

	public Water getById(String id){
		return (Water)waters.get(id);
	}
}
```
경계 인터페이스인 Map을 Waters 안으로 숨겨 Map 인터페이스가 변하더라도 나머지 프로그램에 영향을 미치지 않는다. Map 인스턴스를 공개 API의 인수로 넘기거나 반환값으로 사용하지 않는다.

## 경계 살피고 익히기
간단한 테스트 케이스를 작성해 외부 코드를 익히는 것을 학습테스트라 부른다. 새 버전이 우리 코드와 호환되지 않으면 학습 테스트가 이 사실을 바로 밝혀낸다. 

## 깨끗한 경계
통제하지 못하는 코드를 사용할 때는 너무 많은 투자를 하거나 향후 변경 비용이 지나치게 커지지 않도록 주의한다. 외부 패키지를 호출하는 코드를 가능한 줄여 경계를 관리하자. 새로운 클래스로 경계를 감싸거나 ADAPTER 패턴을 사용한다.
