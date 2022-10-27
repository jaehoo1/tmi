## Map vs Dictionary
공통점
1. Key, Value를 가지고 있으며, Key로 찾아서 Value를 참조하는 자료구조
2. 중복 Key 값이 존재할 때 값을 넣지 않는다. (중복키 불허, Key의 Unique한 성질을 보장해야함)(예외 : multimap)

차이점  
Map
1. Key 값을 기준으로 요소들이 추가, 삽입, 삭제될 때 재정렬 수행
2. 내부가 트리로 구성
3. 트리로 구성되어 있어 탐색 - O(logN)

Dictionary
1. 내부가 해시테이블로 구성

<br/>

## C++ map
- 순서 있는 연관 컨테이너(map, set)는 내부가 트리로 구현됨
- 노드 기반으로 이루어져있고 균형 이진 트리 구조
- map은 key와 value로 이루어져있으며 이는 pair 객체 형태로 저장
- key 중복 불가(unique key)

<br/>

## C++ unordered_map
순서가 지정되지 않은(unordered) 연관 컨테이너는 기존의 순서가 지정된 연관 컨테이너와 같은 동작을 한다.  
기존의 연관 컨테이너는 트리(tree) 구조를 기반으로 동작하지만, C++11부터 추가된 이 컨테이너는 해시 테이블(hash table)을 기반으로 동작한다.

따라서 요소의 추가, 삭제 속도가 빨라졌으며, 다양한 검색 알고리즘을 사용할 수 있게 됨  
순서가 지정된 연관 컨테이너는 양방향 반복자를 지원하지만, 이 컨테이너는 순방향 반복자만을 지원

<br/>

## C++ multimap
- multimap은 map과 거의 동일하지만 딱 한부분만 다름
- key값이 중복 가능

<br/>

## Python Dictionary
- key 값에 `list`, `set`이 올 수 없음
  - 키 값은 immutable(불변) 객체 타입이 와야함
- 키 값은 중복될 수 없음
  - 동일한 키를 추가하면 덮어쓰기됨

Python 3.7 이전에는 기본 Dictionary를 사용하면 순서를 보장받을 수 없었지만, 3.7부터는 기본 Dictionary도 순서를 가지게 됨  
(3.6은 아마 과도기인듯)
```python3
# [Python3.5] 입력된 순서가 보장되지 않음.
>>> dict_3_5 = {}
>>> dict_3_5['a'] = 1
>>> dict_3_5['b'] = 2
>>> dict_3_5['c'] = 3

>>> dict_3_5
{'b': 2, 'a': 1, 'c': 3}

# [Python3.6] 입력된 순서가 보장됨.
>>> dict_3_6 = {}
>>> dict_3_6['a'] = 1
>>> dict_3_6['b'] = 2
>>> dict_3_6['c'] = 3
>>> dict_3_6
{'a': 1, 'b': 2, 'c': 3}
```

이후부터는 기존 Dictionary도 순서를 가지게 되어 OrderedDict와 크게 차이점이 없다고 생각을 할 수 있다. 하지만 동등성을 확인할 때 OrderedDict는 순서까지도 동등한지를 확인해 더 엄격하게 동등성을 검증한다.
```python3
# 기본 딕셔너리
>>> dict_a
{'a': 'apple', 'b': 'banana', 'p': 'pineapple'}
>>> dict_b
{'b': 'banana', 'a': 'apple', 'p': 'pineapple'}

>>> dict_a == dict_b
True

# OrderedDict
>>> ordered_a
OrderedDict([('a', 'apple'), ('b', 'banana'), ('p', 'pineapple')])
>>> ordered_b
OrderedDict([('b', 'banana'), ('a', 'apple'), ('p', 'pineapple')])

>>> ordered_a == ordered_b
False
```

<br/>

## Javascript Map vs Dictionary
[모질라 제단의 Map 문서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)에는 [Map과 Object의 비교와 선택 가이드](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#objects_vs._maps)가 적혀있다. 내용 중 Map 사용이 더 적합한 경우는 아래와 같다.
- 통상적으로 키(Key)는 런타임까지 알 수 없으며, 유동적으로 그것들을 찾아야 하는가?
- 모든 값(Value)은 동일한 타입을 가지고 있으며, 상호 변환이 가능하도록 사용되는가?
- 문자열이 아닌 키(Key)가 필요한가?
- 키-값 짝이 때때로 추가되거나 삭제되는가?
- 자주, 쉽게 변하는 임의의 양의 키-값 짝이 있는가?
- 데이터가 Iterated 되어야 하는가?

<br/>

## Java HashMap vs Hashtable
`HashMap`과 `Hashtable`을 정의한다면, '키에 대한 해시 값을 사용하여 값을 저장하고 조회하며, 키-값 쌍의 개수에 따라 동적으로 크기가 증가하는 associate array'라고 할 수 있다. 이 associate array를 지칭하는 다른 용어가 있는데, 대표적으로 Map, Dictionary, Symbol Table 등이다.

`Hashtable`이란 JDK 1.0부터 있던 Java의 API이고, `HashMap`은 Java 2에서 처음 선보인 Java Collections Framework에 속한 API다. `Hashtable` 또한 `Map` 인터페이스를 구현하고 있기 때문에 `HashMap`과 `Hashtable`이 제공하는 기능은 같다. 다만 `HashMap`은 보조 해시 함수(Additional Hash Function)를 사용하기 때문에 보조 해시 함수를 사용하지 않는 `Hashtable`에 비하여 해시 충돌(hash collision)이 덜 발생할 수 있어 상대적으로 성능상 이점이 있다. 보조 해시 함수가 아니더라도, `Hashtable` 구현에는 거의 변화가 없는 반면, `HashMap`은 지속적으로 개선되고 있다. `Hashtable`의 현재 가치는 JRE 1.0, JRE 1.1 환경을 대상으로 구현한 Java 애플리케이션이 잘 동작할 수 있도록 하위 호환성을 제공하는 것에 있기 때문에, 이 둘 사이에 성능과 기능을 비교하는 것은 큰 의미가 없다고 할 수 있다.

- Thread-safe 여부
  - `Hashtable`은 Thread-safe하고, `HashMap`은 Thread-safe하지 않다는 특징을 가지고 있다. 그렇기에 멀티스레드 환경이 아니라면 `Hashtable`은 `HashMap` 보다 성능이 떨어진다는 단점을 가지고 있다.
- `null` 값 허용 여부
  - `Hashtable`은 key에 `null`을 허용하지 않지만, `HashMap`은 key에 `null`을 허용
- `Enumeration` 여부
  - `Hashtable`은 not fail-fast `Enumeration`을 제공하지만, `HashMap`은 `Enumeration`을 제공하지 않음
- `HashMap`은 보조해시를 사용하기 때문에 보조 해시 함수를 사용하지 않는 `Hashtable`에 비하여 해시 충돌(hash collision)이 덜 발생할 수 있어 상대적으로 성능상 이점이 있음
- 최근까지 `Hashtable`은 구현에 거의 변화가 없지만, `HashMap`은 현재까지도 지속적으로 개선되고 있다.

<br/>

## Reference
- https://woong-programing.tistory.com/171
- https://blockdmask.tistory.com/87
- http://www.tcpschool.com/cpp/cpp_container_associate
- https://blockdmask.tistory.com/450
- http://blog.hwahae.co.kr/all/tech/tech-tech/6662/
- https://partnerjun.tistory.com/64
- https://d2.naver.com/helloworld/831311
- https://devlog-wjdrbs96.tistory.com/253