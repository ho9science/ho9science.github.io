---
title: "13장: 동시성"
date: 2019-09-23 23:59:11
categories: cleancode
tag: 클린코드 개발
---

## 동시성이 필요한 이유

동시성은 결합(coupling)을 없애는 전략이다. 무엇(what)과 언제(when)을 분리하는 전략이다. 스레드가 하나인 프로그램은 무엇과 언제가 서로 밀접하다. 무엇과 언제를 분리하면 애플리케이션 구조와 효율이 극적으로 나아진다. 

### 서블릿(Servlet) 모델

서블릿은 웹 혹은 EJB컨테이너라는 우산 아래서 돌아가는데 이들 컨테이너는 동시성을 부분적으로 관리한다. 웹 요청이 들어올 때마다 웹 서버는 비동기식으로 서블릿을 실행한다. 원칙적으로 각 서블릿 스레드는 다른 서블릿 스레드와 무관하게 자신만의 세상에서 돌아간다.

### 미신과 오해

* 동시성은 항상 성능을 높여준다. X

동시성은 때로 성능을 높여준다. 대기 시간이 아주 길어 여러 스레드가 프로세서를 공유할 수 있거나, 여러 프로세서가 동시에 처리할 독립적인 계산이 많은 경우에만 성능이 높아진다.

* 동시성을 구현해도 설계는 변하지 않는다. X

단일 스레드 시스템과 다중 스레드 시스템은 설계가 판이하게 다르다.

* 웹 또는 EJB 컨테이너를 사용하면 동시성을 이해할 필요가 없다. X

실제로 컨테이너가 어떻게 동작하는지, 어떻게 동시 수정, 데드락 등의 문제를 피할 수 있는지를 알아야 한다.

* 동시성은 다소 부하를 유발한다.

* 동시성은 복잡하다.

* 일반적으로 동시성 버그는 재현하기 어렵다.

* 동시성을 구현하려면 흔히 근본적인 설계 전략을 재고해야 한다.

## 난관

두 스레드가 같은 변수를 동시에 참조하면 놀라운 결과가 발생한다. 두 스레드가 자바 한 줄을 거쳐가는 경로는 수없이 많은데 일부 경로가 잘못된 결과를 내높기 때문이다.

## 동시성 방어 원칙

### 단일 책임 원칙(Single Responsibility Principle, SRP)

SRP는 주어진 메서드/클래스/컴포넌트를 변경할 이유가 하나여야 한다는 원칙. 동시성은 복잡성 하나만으로도 따로 분리할 이유가 충분하다. 즉, 동시성 관련 코드는 다른 코드와 분리해야 한다.

** 동시성 코드는 다른 코드와 분리하라. **

### 자료 범위를 제한하라 

객체 하나를 공유한 후 동일 필드를 수정하던 두 스레드가 서로 간섭하므로 예상치 못한 결과를 내놓는다. 이 문제는 공유 객체를 사용하는 코드 내 임계 영역(critical section)을 synchronized 키워드로 보호한다. 이런 임계 영역의 수를 줄이는 기술이 중요하다.

** 자료를 캡슐화(encapsulation)하라. 공유 자료를 최대한 줄여라. ** 

### 자료 사본을 이용하라

공유 자료를 줄이려면 처음부터 공유하지 않는 방법이 제일 좋다. 어떤 경우에는 객체를 복사해 읽기 전용으로 사용하는 방법이 가능하다.

### 스레드는 가능한 독립적으로 구현하라

다른 스레드와 자료를 공유하지 않는다. 각 스레드는 클라이언트 요청 하나를 처리한다. 모든 정보는 비공유 출처에서 가저오며 로컬 변수에 저장한다. 예를 들어 HttpServlet 클래스에서 파생한 클래스는 모든 정보를 doGet과 doPost 매개변수로 받는다. 그래서 각 서블릿은 마치 자신이 독자적인 시스템에서 동작하는 양 요청을 처리한다. 서블릿이 로컬 변수만 사용한다면 서블릿이 동기화 문제를 일으킬 가능성은 전무하다. 데이터베이스 연결과 같은 자원을 고유하는 상황은 예외.

** 독자적인 스레드로, 가능하면 다른 프로세서에서, 돌려도 괜찮도록 자료를 독립적인 단위로 분할하라. **

## 라이브러리를 이해하라

* 스레드 환경에 안정한 콜렉션을 사용한다.
* 서로 무관한 작업을 수행할 때는 executor 프레임워크를 사용한다.
* 가능하다면 스레드가 차단(blocking)되지 않는 방법을 사용한다.
* 일부 클래스 라이브러리는 스레드에 안전하지 못하다.

#### java.util.concurrent

* ReentrantLock : 한 메서드에서 잠그고 다른 메서드에서 푸는 락(lock)이다.
* Semaphore : 전형적인 세마포어다. 개수(count)가 있는 락이다.
* CountDownLatch : 지정한 수만큼 이벤트가 발생하고 나서야 대기 중인 스레드를 모두 해제 하는 락이다. 모든 스레드에게 동시에 공평하게 시작할 기회를 준다.

** 언어가 제공하는 클래스를 검토하라. 자바에서는 java.util.concurrent, java.util.concurrent.atomic, java.util.concurrent.locks를 익혀라. **

## 실행 모델을 이해하라

* 한정된 자원(Bound Resource) : 다중 스레드 환경에서 사용하는 자원으로 크기나 숫자가 제한적이다. 데이터 베이스 연결, 길이가 일정한 읽기/쓰기 버퍼 등이 예이다.
* 상호 배제(Mutual Exclusion) : 한 번에 한 스레드만 공유 자료나 공유 자원을 사용할 수 있는 경우
* 기아(Starvation) : 한 스레드나 여러 스레드가 굉장히 오랫동안 혹은 영원히 자원을 기다린다. 예를 들어, 항상 짧은 스레드에게 우선순위를 준다면, 긴 스레드가 기아 상태에 빠진다.
* 데드락(Deadlock) : 여러 스레드가 서로가 끝나기를 기다린다. 모든 스레드가 각기 필요한 자원을 다른 스레드가 점유하는 바람에 어느 쪽도 더 이상 진행하지 못한다.
* 라이브락(Livelock) : 락을 건느 단계에서 각 스레드가 서로를 방해한다. 스레드는 계속해서 진행하려 하지만, 공명(resonance)으로 인해, 굉장히 오랫동안 혹은 영원히 진행하지 못한다.

### 생산자-소비자(Producer-Consumer)

하나 이상 생산자 스레드가 정보를 생성해 버퍼(buffer)나 대기열(queue)에 넣는다. 하나 이상 소비자 스레드가 대기열에서 정보를 가져와 사용한다. 생산자 스레드와 소비자 스레드가 사용하는 대기열은 한정된 자원이다. 생산자 스레드는 대기열에 빈 공간이 있어야 정보를 채운다. 즉, 빈 공간이 생길 때까지 기다린다. 소비자 스레드는 대기열에 정보가 있어야 가져온다. 즉, 정보가 채워질 때까지 기다린다.

### 읽기-쓰기(Readers-Writers)

읽기 쓰레드를 위한 주된 정보원으로 공유 자원을 사용하지만 쓰기 스레드가 이 공유 자원을 이따금 갱신한다고 하자. 이런 경우 처리율(throughput)이 문제에 핵심이다. 처리율을 강조하면 기아 현상이 생기거나 오래된 정보가 쌓인다. 갱신을 허용하면 처리율에 영향을 미친다. 쓰기 스레드가 버퍼를 갱신하는 동안 읽기 스레드가 버퍼를 읽지 않으려면, 마찬가지로 읽기 스레드가 버퍼를 읽는 동안 쓰기 스레드가 버퍼를 갱신하지 않으려는 균형이 필요하다. 간단한 전략은 읽기 스레드가 없을 때까지 갱신을 원하는 쓰기 쓰레드가 버퍼를 기다리는 방법이다. 

### 식사하는 철학자들(Dining Philosophers)

** 위에서 설명한 기본 알고리즘과 각 해법을 이해하라 **

## 동기화 하는 메서드 사이에 존재하는 의존성을 이해하라

동기화하는 메서드 사이에 의존성이 존재하면 동시성 코드에 찾아내기 어려운 버그가 생긴다.공유 클래스 하나에 동기화된 메서드가 여럿이라면 구현이 올바른지 다시 한 번 확인한다.

** 공유 객체 하나에는 메서드 하나만 사용하라 ** 

### 공유 객체 하나에 여러 메서드가 필요한 상황

* 클라이언트 잠금 : 클라이언트에서 첫 번재 메서드를 호출하기 전에 서버를 잠근다. 마지막 메서드를 호출할 때까지 잠금을 유지한다.
* 서버 잠금 : 서버를 잠그고 모든 메서드를 호출한 후 잠금을 해제하는 메서드를 구현한다. 클라이언트는 이 메서드를 호출한다.
* 연결(Adapted) 서버 : 잠금을 수행하는 중간 단게를 생성한다. 

## 동기화하는 부분을 작게 만들어라

자바에서 synchronized 키워드를 사용하면 락을 설정한다. 같은 락으로 감싼 모든 코드 영역은 한 번에 한 스레드만 실행이 가능하다. 락은 스레드를 지연시키고 부하를 가중시킨다. synchronized 문을 남발하는 코드는 바람직하지 않다. 반면 임계영역은 반드시 보호해야 한다. 임계영역 크기를 키우지 않고 수를 최대한 줄여야 한다.

** 동기화 하는 부분을 작게 만들어라 **

## 올바른 종료 코드는 구현하기 어렵다.

스레드가 절대 오지 않을 시그널을 기다릴 때 가장 흔히 발생하는 문제가 데드락이다. 

## 스레드 코드 테스트하기

문제를 노출하는 테스트 케이스를 작성하라. 프로그램 설정과 시스템 설정과 부하를 바꿔가며 자주 돌려라. 테스트가 실패하면 원인을 추적한다. 다시 돌려서 통과하더라도 절대로 그냥 넘어가면 안된다.

* 말이 안되는 실패는 잠정적인 스레드 문제로 취급하라.
* 다중 스레드를 고려하지 않은 순차 코드부터 제대로 돌게 만들자.
* 다중 스레드를 쓰는 코드 부분을 다양한 환경에 쉽게 끼워 넣을 수 있게 스레드 코드를 구현하라.
* 다중 스레드를 쓰는 코드 부분을 상황에 맞게 조율할 수 있게 작성하라.
* 프로세서 수보다 많은 스레드를 돌려보라.
* 다른 플랫폼에서 돌려보라.
* 코드에 보조코드(instrument)를 넣어 돌려라. 강제로 실패를 일으키게 해보라.

## 결론

SRP를 준순한다. POJO를 사용해 스레드를 아는 코드와 모르는 코드를 분리한다. 스레드 코드를 테스트 할 때는 전적으로 스레드만 테스트한다. 동시성 오류를 일으키는 잠정적인 원인을 철저히 이해한다. 예를 들어 스레드가 공유 자료를 조작하거나 자원 풀을 공유할 때 동시성 오류가 발생한다. 