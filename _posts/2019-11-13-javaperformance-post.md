---
title: "자바 성능"
date: 2019-11-14 01:59:11
categories: java
tag:
	- java
	- 자바
    - 책리뷰
---

자바 성능을 결정짓는 코딩 습관과 튜닝 이야기

책이 나온지 십년이 넘었지만 자바 개발자로서 피가 되고 살이 되는 알찬 내용이 가득 담겨 있었다. 일반적으로 중소 개발자들은 체험하지 못할 프로세스와 상황들을 나초보라는 가상의 인물을 통해 간접 경험을 할 수 있어서 좋았다. 프로젝트 튜닝 경험도 설명해주어서 경험이 부족한 개발자들에게 굉장히 만족스러운 책이다.

# GC
Garbage Collection, 객체는 메모리를 점유하고, 필요하지 않으면 메모리에서 해제되어야 한다. 더 이상 필요가 없는 객체를 효과적으로 처리하는 작업을 GC라고 한다.
가비지 콜렉터의 역할
* 메모리 할당
* 사용 중인 메모리 인식
* 사용하지 않는 메모리 인식

메모리 크기를 전부 사용한 다음 GC를 해도 더 이상 사용 가능한 메모리 영역이 없는데 계속 메모리를 할당하려고 하면 OutOfMemoryError가 발생하여 was가 다운될 수 있다.
JVM의 메모리는 크게 클래스영역, 자바 스택, 힙, 네이티브 메소드 스택의 4가지 영역으로 나뉜다.
Young 영역의 Eden, Survivor1, Survivor2 Old 영역의 메모리 영역으로 나뉜다고 볼 수 있다. 
GC는 각 영역의 할당된 크기의 메모리가 허용치를 넘을 때 수행한다는 것, 개발자가 컨트롤할 영역은 아니라는 것, 따라서
```
System.gc()
Runtime.getRuntime.get()
```
메소드를 쓰면 안된다.

# String
String()
JDK5.0이상을 사용한다면 컴파일러에서 자동으로 StringBuilder로 변환하여 준다.
StringBuffer()
스레드와 관련
StringBuilder()
스레드 안전 여부와 상관이 없을 경우

# Collection
* Collection : 가장 상위 인터페이스
* Set : 중복을 허용하지 않는 집합을 처리하기 위한 인터페이스
* List : 순서가 있는 집합을 처리하기 위한 인터페이스, 인덱스가 있어 위츨 지정하여 값을 찾을 수 있음, 중복허용
* Queue : 여러 개의 객체를 처리하기 전에 담아서 처리할 때 사용하기 위한 인터페이스. 기본적으로 FIFO
* Map : 키와 값의 쌍으로 구성된 객체의 집합을 처리하기 위한 인터페이스, 중복 키를 허용하지 않음

### Set
* HashSet : 데이터를 해쉬 테이블에 담는 클래스로 순서 없이 저장
* TreeSet : red-black이라는 트리에 데이터를 담는다. 값에 따라서 순서가 정해짐, HashSet보다 느리지만 데이터를 담으면서 정렬할 때 유용
* LinkedHashSet : 해쉬 테이블에 데이터를 담는데, 저장된 순서에 따라 순서가 저장된다.

### List
* Vector : 객체 생성시에 크기를 지정할 필요가 없는 배열 클래스
* ArrayList : Vector와 비슷하지만 동기화 처리가 되어 있지 않음
* LinkedList : ArrayList와 동일하지만 Queue인터페이스를 구현하였기 때문에 FIFO 큐 작업을 수행

### Map
* Hashtable : 데이터를 해쉬 테이블에 담는 클래스, 내부에서 관리하는 해쉬 테이블 객체가 동기화 되어 있음
* HashMap : 데이터를 해쉬 테이블에 담는 클래스, Hashtable과 다른 점은 null값을 허용한다는 것과 동기화되어 있지 않다는 것
* TreeMap : red-black 트리에 데이터를 담는다. TreeSet과 다른 점은 키에 의해서 순서가 정해짐
* LinkedHashMap : HashMap과 거의 동일하며 이중 연결 리스트라는 방식을 사용하여 데이터를 담는다.

### Queue
* PriorityQueue : 큐에 추가된 순서와 상관없이 먼저 생성한 객체가 먼저 나오도록 되어 있는 큐
* LinkedBlockingQueue : 선택적으로 저장할 데이터의 크기를 정할 수도 있는 FIFO 기반의 링크 노드를 사용하는 블로킹 큐
* ArrayBlockingQueue : 저장되는 데이터의 크기가 정해져 있는 FIFO 기반의 블로킹 큐
* PriorityBlockingQueue : 저장되는 데이터의 크기가 정해져 있지 않고, 객체의 생성 순서에 따라서 순서가 저장되는 블로킹 큐
* DelayQueue : 큐가 대기하는 시간을 지정하여 처리하도록 되어 있는 큐
* SynchronousQueue : put() 메소드를 호출하면 다른 스레드에서 take()메소드가 호출될 때까지 대기하도록 되어 있는 큐

Set : HashSet
List : ArrayList
Map : HashMap
Queue : LinkedList

# static
클래스의 변수를 static으로 선언하면 그 변수는 객체의 변수가 되는 것이 아니라 클래스의 변수가 된다.
static의 특징은 다른 JVM에서는 static이라고 선언해도 다른 주소나 다른 값을 참조하지만, 같은 JVM에서는 같은 주소와 같은 값을 참조하고 GC의 대상이 되지 않는다. 
#### 자주 사용하고 절대 변하지 않는 변수는 final static으로 선언하자
#### 설정 파일 정보도 static으로 관리하자 
#### 코드성 데이터는 DB에서 한 번만 읽자

# synchronized
### 프로세스와 스레드
하나의 프로세스에는 여러 개의 스레드가 생성된다.
### 스레드의 구현
```
public class ThreadExtends extends Thread{
    public void run() {

    }
}
```
Thread 클래스를 상속받는 방법
```
public class RunnableImple implements Runnable{
    public void run() {

    }
}
```
Runnable 인터페이스를 구현하는 방법
```
public class RunThreads{
    public static void main(String[] args){
        RunnableImple ri = new RunnableImple();
        ThreadExtends te = new ThreadExtends();
        new Thread(ri).start();
        te.start();
    }
}
```
### synchronized 식별자 사용
* 하나의 객체를 여러 스레드에서 동시에 사용할 경우
* static으로 선언한 객체를 여러 스레드에서 동시에 사용할 경우

### java.util concurrent
* Lock : 실행중인 스레드를 간단한 방법으로 정지시켰다가 실행시키도록 한다. 상호 참조로 인해 발생하는 데드락 피할 수 있음
* Executors : 스레드를 더 효율적으로 관리할 수 있는 클래스들을 제공, 스레드 풀동 제공
* Concurrent : 동기화된 클래스 제공
* Atomic : 동기화 되어 있는 변수, synchronized 식별자를 메소드에 지정할 필요 없이 사용 가능

# I/O
자바에서 입력과 출력은 Stream을 통해서 이루어진다. 일반적으로 파일 IO만을 생각할 수 있는데 넽워크를 통해서 서버로 데이터를 전송하거나 다른 서버로부터 데이터를 전송받는 것도 I/O에 포함된다. 

### 자바의 I/O 프로세스
1. 파일을 읽으라는 메소드를 자바에 전달
2. 파일명을 전달 받은 메소드가 운영체제의 커널에게 파일을 읽어달라고 부탁
3. 커널이 하드 디스크로부터 파일을 읽어서 자신의 커널에 있는 버퍼에 복사하는 작업 수행. DMA
4. 자바에서는 마음대로 커널의 버퍼를 사용하지 못하므로, JVM으로 그 데이터를 전달
5. JVM에서 메소드에 있는 스트림 관리 클래스를 사용하여 데이터를 처리

# 튜닝 대상
가장 많이 수행하는 상위 20%의 화면을 분석 및 튜닝 대상으로 선정
