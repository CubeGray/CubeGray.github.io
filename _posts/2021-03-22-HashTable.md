---
title: "HashTable?"
date: 2021-03-22 00:00:28 -0400
draft: false
description: "[JAVA]HashTable"
categories: [JAVA]
toc : true
toc_sticky : true
toc_label : 목차
---


## **1. 해시테이블(HashTable)이란?**


### HashTable(해시테이블)이란? 

해시 테이블은  (Key, Value)로 데이터를 저장하는 자료구조  중 하나로 빠르게 데이터를 검색할 수 있는 자료구조이다. 해시 테이블이 빠른 검색속도를 제공하는 이유는 내부적으로 배열(버킷)을 사용하여 데이터를 저장하기 때문이다. 해시 테이블은 각각의 Key값에 해시함수를 적용해 배열의 고유한 index를 생성하고, 이 index를 활용해 값을 저장하거나 검색하게 된다. 여기서 실제 값이 저장되는 장소를 버킷 또는 슬롯이라고 한다.


Key값으로 데이터를 찾을 때 해시 함수를 1번만 수행하여(충돌이 안날 경우) value를 찾을 수 있으므로 매우 빠르게 데이터를 저장/삭제/조회할 수 있다.  해시테이블의 평균 시간복잡도는 O(1)이다.

### Hash 함수(해시 함수) 

해시 함수의 조건은 충돌이 거의 없어야 하며, 해시 함수의 계산에 시간이 적게 들어야한다.
해시 함수에서 중요한 것은 고유한 인덱스 값을 설정하도록 하는 것이다.
ex)sha
    

## **2.  해시(Hash)값이 충돌하는 경우**


### 해시(Hash)값이 충돌하는 경우

그런데 만약 "John Smith"를 해시 함수를 돌려 나온 값과 "Mang Kyu"를 해시 함수를 돌려 나온 값이 동일하다면 어떻게 해야 할까?

해시 테이블에서는 충돌에 의한 문제를  분리 연결법(Separate Chaining)과 개방 주소법(Open Addressing)  크게 2가지로 해결하고 있다.

###  분리 연결법(Separate Chaining)

![](https://blog.kakaocdn.net/dn/bTF67c/btqL7xx3OGw/DM8KEKU5x7dx6Nks4JR7K1/img.png)

Separate Chaining이란 동일한 버킷의 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장하는 것이다.  위의 그림과 같이 동일한 버킷으로 접근을 한다면 데이터들을 연결을 해서 관리해주고 있다. 

이러한 Chaining 방식은 해시 테이블의 확장이 필요없고 간단하게 구현이 가능하며, 손쉽게 삭제할 수 있다는 장점이 있다. 하지만 데이터의 수가 많아지면 동일한 버킷에 chaining되는 데이터가 많아지며 그에 따라 캐시의 효율성이 감소한다는 단점이 있다.

### 개방 주소법(Open Addressing) 

Open Addressing이란 추가적인 메모리를 사용하는 Chaining 방식과 다르게 비어있는 해시 테이블의 공간을 활용하는 방법이다. Open Addressing을 구현하기 위한 대표적인 방법으로는 3가지 방식이 존재한다.

1.  Linear Probing: 현재의 버킷 index로부터 고정폭 만큼씩 이동하여 차례대로 검색해 비어 있는 버킷에 데이터를 저장한다.
2.  Quadratic Probing: 해시의 저장순서 폭을 제곱으로 저장하는 방식이다. 예를 들어 처음 충돌이 발생한 경우에는 1만큼 이동하고 그 다음 계속 충돌이 발생하면 2^2, 3^2 칸씩 옮기는 방식이다.
3.  Double Hashing Probing: 해시된 값을 한번 더 해싱하여 해시의 규칙성을 없애버리는 방식이다. 해시된 값을 한번 더 해싱하여 새로운 주소를 할당하기 때문에 다른 방법들보다 많은 연산을 하게 된다.

![](https://blog.kakaocdn.net/dn/WR1fv/btqL5APCcSa/BZN6wvxUXzJBEiOfOMLfR0/img.png)

Open Addressing에서 데이터를 삭제하면 삭제된 공간은 Dummy Space로 활용되는데, 그렇기 때문에  Hash Table을 재정리 해주는 작업이 필요하다고 한다.

## **3. 해시테이블(HashTable) 시간복잡도**

### 해시테이블(HashTable) 시간복잡도 

각각의 Key값은 해시함수에 의해 고유한 index를 가지게 되어 바로 접근할 수 있으므로  평균 O(1)의 시간복잡도로 데이터를 조회할 수 있다. 하지만  데이터의 충돌이 발생한 경우 Chaining에 연결된 리스트들까지 검색을 해야 하므로 O(N)까지 시간복잡도가 증가할 수 있다.

충돌을 방지하는 방법들은 데이터의 규칙성(클러스터링)을 방지하기 위한 방식이지만 공간을 많이 사용한다는 치명적인 단점이 있다.

만약 테이블이 꽉 차있는 경우라면 테이블을 확장해주어야 하는데, 이는 매우 심각한 성능의 저하를 불러오기 때문에 가급적이면 확장을 하지 않도록 테이블을 설계해주어야 한다.
(통계적으로 해시 테이블의 공간 사용률이 70% ~ 80%정도가 되면 해시의 충돌이 빈번하게 발생하여 성능이 저하되기 시작한다고 한다.)

또한 해시 테이블에서 자주 사용하게 되는 데이터를 Cache에 적용하면 효율을 높일 수 있다. 자주 hit하게 되는 데이터를 캐시에서 바로 찾음으로써 해시 테이블의 성능을 향상시킬 수 있다.

## **4. Java의 HashMap(해시맵)과 HashTable(해시테이블) 차이**

----------

### ********[ Java의 HashMap(해시맵) vs HashTable(해시테이블) ]********

Java 개발자라면 (Key,Value)로 저장하는 익숙한 자료구조인 HashMap이 있다. 그렇다면 Java에서 HashTable과 HashMap의 차이가 당연히 있을 텐데, 그 차이는  동기화 지원 여부에 있다.

```java
// 해시테이블의 put
public synchronized V put(K key, V value) {
    // Make sure the value is not null
    if (value == null) {
        throw new NullPointerException();
    }
    // Makes sure the key is not already in the hashtable.
    Entry<?,?> tab[] = table;
    int hash = key.hashCode();
    int index = (hash & 0x7FFFFFFF) % tab.length;
    @SuppressWarnings("unchecked")
    Entry<K,V> entry = (Entry<K,V>)tab[index];
    for(; entry != null ; entry = entry.next) {
        if ((entry.hash == hash) && entry.key.equals(key)) {
            V old = entry.value;
            entry.value = value;
            return old;
        }
    }
    addEntry(hash, key, value, index);
    return null;
}

// 해시맵의 put
public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}
```

위의 코드에서 첫번째 put은 해시테이블의 put이며, 두번째 put은 해시맵의 put이다. 첫번째 해시테이블의 put에는 synchronized 키워드가 붙어있는 것을 확인할 수 있는데, 이것은 병렬 프로그래밍을 할 때 동기화를 지원해준다는 것을 의미한다. 이것은 해당 함수를 처리하는 시간이 조금 지연됨을 의미힌다.

그렇기 때문에 우리는  병렬 처리를 하면서 자원의 동기화를 고려해야 하는 상황이라면 해시테이블(HashTable)을 사용해야 하며,  병렬 처리를 하지 않거나 자원의 동기화를 고려하지 않는 상황이라면 해시맵(HashMap)을 사용하면 된다.

**출처**
https://mangkyu.tistory.com/102