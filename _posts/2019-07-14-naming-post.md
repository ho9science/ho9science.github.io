---
title: "2장: 의미있는 이름 "
date: 2019-07-11 00:00:11
categories: cleancode
tag: 클린코드 개발
---
# 2장: 의미있는 이름 

## 의도를 분명히 밝혀라 

변수나 함수 클래스 이름은 존재 이유, 수행 기능, 사용 방법과 같은 의도가 코드에 분명히 드러나야한다. 
```
int t; //보다는 

int elapsedTime; //과 같이  사용 
```

## 그릇된 정보를 피하라

컨테이너가 실제 List가 아니라면 List라는 이름을 사용하지 않는다.
서로 흡사한 이름을 사용하지 않도록 한다.
유사한 개념은 유사한 표기법을 사용하여 일관성을 유지한다. 

## 의미있게 구분하라
연속적인 숫자를 덧붙이거나 불용어를 추가하여 이름을 만들지 않는다. a, an, the, info, data는 의미가 불분명한 불용어이다.

## 검색하기 쉬운 이름을 사용하라
문자 하나를 사용하는 이름과 상수는 쉽게 눈에 띄지 않는다. 이름 길이는 범위 크기에 비례해야한다. 변수나 상수를 코드 여러 곳에서 사용한다면 검색하기 쉬운 이름이 바람직하다.

## 인코딩을 피하라
인터페이스 클래스와 구현 클래스의 경우 구현 클래스의 이름을 인코딩하는 것이 좋다. ex) interface ShapeFactory , 구현체는 ShapeFactoryImple or  CShapeFactory

## 자신의 기억력을 자랑하지 마라
문자 하나만 사용하는 변수 이름은 문제가 있다. 루프에서 반복 횟수를 세는 변수 i,j,k는 괜찮다.
* 클래스 이름 : 클래스 이름과 객체 이름은 명사나 명사구가 적합하다. Manger, Processor, Data, Info 같은 단어는 피하고 동사는 사용하지 않는다.
* 메서드 이름 : 동사나 동사구가 적합하다. 접근자(Accessor), 변경자(Mutator), 조건자(Predicate)는 javabean 표준에 따라 get, set, is를 붙인다.
생성자를 중복정의 할 때는 정적 팩토리 메서드를 사용한다. 메서드는 인수를 설명하는 이름을 사용한다. 
```
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
위 코드가 아래 코드보다 낫다
Complex fulcrumPoint = new Complex(23.0);
```

## 한 개념에 한 단어를 사용하라
추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다. 
똑같은 메서드를 클래스마다 fetch, retrieve, get 으로 제각각 부르면 혼란스럽다. 마찬가지로 controller, manager, driver를 섞어 쓰면 혼란스럽다.

## 말장난을 하지 마라
한 단어를 두가지 목적으로 사용하지 마라. 다른 개념에 같은 단어를 사용하지 않는다. 

## 해법 영역에서 가져온 이름을 사용하라 
전산 용어, 알고리즘 이름, 패턴 이름, 수학 용어 등을 사용할 수 있다.

## 의미 있는 맥락을 추가하라
클래스, 함수, 네임스페이스를 넣어 맥락을 부여한다. 마지막 수단으로 접두어를 붙인다. 변수가 어떤 구조에 속하는지 분명해지면 좋다.

## 불필요한 맥락을 없애라
일반적으로 의미가 분명한 경우에 한해서 짧은 이름이 긴 이름보다 좋다. 
