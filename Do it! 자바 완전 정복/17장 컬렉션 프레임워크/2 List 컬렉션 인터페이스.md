# 2. List<E> 컬렉션 인터페이스

List<E>는 5개의 대표적인 컬렉션 중 배열과 가장 비슷한 구조를 지닌 자료구조다.
먼저, 배열과 리스트의 차이점을 알아보자.

## 1. 배열과 리스트의 차이점

배열과 리스트의 가장 큰 차이점은 저장 공간의 크기가 고정적인지, 동적으로 변화할 수 있는지이다. 배열은 저장 공간이 최초에 생성 당시 지정한 크기로 고정되고, 이후 변경할 수 없으나, 배열과 달리 리스트는 내부 요소의 개수에 따라 저장 공간의 크기가 동적으로 조정된다.

배열은 저장된 요소를 삭제하려면, 해당 요소의 위치에 null을 할당하여, 최초 지정한 저장 공간의 크기가 변화하지 않지만, 리스트는 특정 요소를 삭제할 때마다 저장 공간의 크기가 줄어든다.

데이터의 저장 공간 크기 <sup>size</sup>는 실제 저장되어 있는 데이터의 수를 의미하며, 저장 용량 <sup>capacity</sup>와는 다르다.

## 2. List<E> 객체 생성

List<E> 는 인터페이스이기 때문에 객체를 스스로 생성할 수 없다. 하지만 컬렉션 프레임워크를 이용할 때에는 직접 인터페이스를 구현하지 않아도 된다. 이미 클래스가 구현되어 있기 때문이다. List<E> 인터페이스를 구현한 대표적인 클래스로는 크게 ArrayList<E>, Vector<E>, LinkedList<E>를 들 수 있다.

<table>
    <tr>
        <th style="border: 1px solid black; border-radius: 5px; text-align: center;">List&lt;E&gt;</th>
    </tr>
    <tr>
        <td>ArrayList&lt;E&gt;</td>
    </tr>
    <tr>
        <td>LinkedList&lt;E&gt;</td>
    </tr>
    <tr>
        <td>Vector</td>
    </tr>
</table>

### List<E> 인터페이스 구현 클래스 생성자로 동적 컬렉션 객체 생성

List<E> 인터페이스는 제네릭 인터페이스이므로 이를 상속한 자식 클래스들도 제네릭 클래스다. 즉, 객체를 생성할 때 제네릭의 실제 타입을 지정해야 한다. 객체를 생성할 때는 일반적으로 기본 생성자를 사용하지만, 초기 저장 용량을 매개변수로 포함하고 있는 생성자를 사용할 수도 있다. 단, LinkedList<E>는 기본 생성자만 존재한다.

저장 용량은 데이터의 개수를 나타내는 저장 공간의 크기 <sup>size</sup>와는 다른 개념으로, 데이터를 저장하기 위해 미리 할당해 놓은 메모리의 크기라고 생각하면 된다.

예를 들어 List<E> 기본 생성자를 사용해 객체를 생성하면 기본으로 10만큼의 저장 용량을 내부에 확보해 놓는다. 이후 데이터가 추가돼 저장 용량이 더 필요하면 자바 가상 머신이 저장 용량을 자동으로 늘리므로 개발자가 따로 신경쓸 필요가 없다. 

#### List<E> 인터페이스의 구현 클래스 생성자로 동적 컬렉션 생성

    List<제네릭 타입 지정> 참조변수 = new ArrayList<제네릭 타입 지정>;
    List<제네릭 타입 지정> 참조변수 = new Vector<제네릭 타입 지정>;
    List<제네릭 타입 지정> 참조변수 = new LinkedList<제네릭 타입 지정>;

#### 예시

    List<Integer> intList1 = new ArrayList<Integer>();  // capacity = 10
    List<Integer> intList2 = new ArrayList<Integer>(30);  // capacity = 30
    List<Integer> intList2 = new LinkedList<Integer>(30);  // 오류

### Arrays.asList() 메서드를 이용해 정적 컬렉션 객체 생성

List<E> 객체를 생성하는 또다른 방법은 Arrays 클래스의 asList() 정적 메서드를 사용하는 것이다. 내부적으로 배열을 먼저 생성하고, 이를 List<E>로 Wrapping, 즉 포장만 해 놓은 것이다. 따라서 내부 구조는 배열과 동일하므로 컬렉션 객체인데도 저장 공간의 크기를 변경할 수 없다.

## 3. List<E> 주요 메서드



| |구분|Return Type|Method|Function|
|:-:|:-:|-|:-|-|
|1<td rowspan=4> 데이터 추가</td>|boolean|add(E element)| 매개변수로 입력된 원소를 리스트 마지막에 추가|
|2|void|add(int index, E element)| index 위치에 입력된 원소 추가|
|3|boolean|addAll(Collection<? Extends E> c)| 매개변수로 입력된 컬렉션 전체를 리스트 마지막에 추가|
|4|boolean|addAll(int index, Collection<? Extends E> c)| index 위치에 매개변수로 입력된 컬렉션 전체를 리스트 마지막에 추가|
|5|데이터 변경|E|set(int index, E element)|index 위치의 원솟값을 입력된 원소로 변경
|6<td rowspan=3> 데이터 삭제</td>|E|remove(int index)|원소 중 매개변수 입력과 동일한 객체 삭제
|7|boolean|remove(Object o)|원소 중 매개변수 입력과 동일한 객체 삭제|
|8|void|clear()|전체 원소 삭제|
|9<td rowspan=3> 리스트 데이터 정보 추출</td>|E|get(int index)|index 위치의 원솟값을 꺼내 리턴
|10|int|size()|리스트 객체 내에 포함된 원소의 개수
|11|boolean|isEmpty()|리스트의 원소가 하나도 없는지 여부를 리턴|
|12<td rowspan=2> 리스트 배열 변환</td>|Object[]|toArray()|리스트를 Object 배열로 변환
|13|T[]|toArray(T[] t)|입력매개변수로 전달한 타입의 배열로 변환|

## 4. ArrayList<E> 구현 클래스

ArrayList<E> 는 List<E> 인터페이스를 구현한 배열처럼 수집한 원소를 인덱스로 관리하며 저장 용량을 동적으로 관리하는 클래스이다.

## 5. Vector<E> 구현 클래스

Vector<E>는 ArrayList<E>와 마찬가지로 동일한 타입의 객체를 수집할 수 있고, 메모리를 동적 할당할 수 있으며, 데이터의 추가, 변경, 삭제 등이 가능하다. 

Vector<E>의 주요 메서드는 ArrayList<E>와 달리 동기화 메서드로 구현되어 있으므로 멀티 쓰레드에 적합하도록 설계돼있다. 

동기화 메서드는 하나의 공유 객체를 2개의 쓰레드가 동시에 사용할 수 없도록 만든 메서드다. 메서드를 동기화하지 않으면 List<E> 객체가 있을 때 하나의 쓰레드는 데이터를 읽고, 또 하나의 쓰레드는 데이터를 삭제하는 작업을 동시에 수행해 작업이 충돌할 수 있다. 

**쓰레드와 동기화는 15장을 참고**


## 6. LinkedList<E> 구현 클래스

LinkedList<E> 또한 ArrayList<E>와 마찬가지로 동일한 타입의 객체를 수집할 수 있고, 메모리를 동적 할당할 수 있으며, 데이터의 추가, 변경, 삭제 등이 가능하다. 

ArrayList<E>와 다른 점은 2가지이다.
첫째, LinkedList<E>는 저장 용량을 매개변수로 갖는 생성자가 없기 때문에 객체를 생성할 때 저장 용량을 지정할 수 없다.

둘째, 내부적으로 데이터를 저장하는 방식이 ArrayList<E>와 다르다.
ArrayList<E>는 모든 데이터를 위치 정보인 인덱스와 값으로 저장하는 반면, LinkedList<E>는 앞뒤 객체 정보를 저장한다. 모든 데이터가 서로 연결된 형태로 관리되는 것이다.


## 7. ArrayList<E> 와 LinkedList<E> 성능 비교

ArrayList<E>의 경우, 데이터를 추가 또는 삭제할 때, 데이터의 위치 정보인 인덱스를 수정해야 하지만, LinkedList<E>는 각 원소의 앞뒤 객체 정보만을 저장하고 있으므로 값이 추가, 삭제 될 시 앞뒤 데이터 정보만 수정하면 된다. 따라서 중간에 데이터를 추가할 때 속도 차이가 발생할 수 있다.

LinkedList<E>는 각 원소가 자신의 인덱스 정보를 따로 갖고 있지 않기 때문에 특정 인덱스의 값을 가져오기 위해서는 앞에서부터 차례대로 번호를 세어가면서 인덱스의 위치를 찾아야 한다.

정리하면 데이터 추가 삭제 시 LinkedList<E>가, 특정 데이터를 검색할 시 ArrayList<E>의 속도가 빠르다.