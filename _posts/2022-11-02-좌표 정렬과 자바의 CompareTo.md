---
layout: single
title: "[알고리즘] 좌표 정렬과 자바의 compareTo 구현"
categories: Algorithm
---

## 좌표 정렬과 자바의 compareTo 구현

```
N개의 평면상 좌표(x,y)를 오름차순으로 정렬하여 출력하세요.
정렬 기준 : x값에 의해 우선 정렬하고, x값이 같을 경우 y값에 의해 정렬한다.
```

#### 예시 입력

```
5
2 7
1 3
1 2
2 5
3 6
```

#### 예시 출력

```
1 2
1 3
2 5
2 7
3 6
```

- 우선 각각의 좌표값을 저장할 클래스를 만든다
- 값을 입력 받아 객체를 생성하여 입력값을 저장한다
- `Collections.sort()`를 이용하여 객체를 정렬한다

```java
class Point {
    public int x,y;
    Point(int x, int y){
        this.x = x;
        this.y = y;
    }
}

class Main {
    public static void main(Stirng[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt(); // N개의 좌표값
        ArrayList<Point> list = new ArrayList<>();
        for(int i = 0; i<n; i++) {
            int x = sc.nextInt();
            int y = sc.nextInt();
            list.add(new Point(x,y));
        }

        Collections.sort(list);
    }
}
```

그러면 마지막 줄 `Collections.sort(list)`에서 오류가 날 것이다!

```java
// 공식 API 문서의 Collection.sort() 메서드
public static <T extends Comparable<? super T>> void sort(List<T> list)
```

```
All elements in the list must implement the Comparable interface.
```

`Collections.sort()`의 매개변수 타입 T는 Comaprable 인터페이스를 구현한 타입이어야 한다.

```java
class Point {
    public int x,y;
    Point(int x, int y){
        this.x = x;
        this.y = y;
    }
}
```

만들어진 Point 클래스를 살펴보면 x와 y 값이 있는데, 만약 두 Point 객체가 있을 경우 어떤 것을 기준으로 이들을 비교해야 할지 모르기 때문이다.

이 기준을 잡아주는 것이 `Comparable` 인터페이스이고 이를 구현한 클래스는 정렬이 가능해진다.

![image](https://user-images.githubusercontent.com/80742079/199395846-f738cebc-e9ee-40a6-808b-693a8f847424.png)

Point 클래스에서 Comparable 인터페이스의 `compareTo()` 메서드를 구현하자.

```java
class Point implements Comparable<Point> {
    public int x,y;
    Point(int x, int y){
        this.x = x;
        this.y = y;
    }

    @Override
    public int compareTo(Point p) {
        if(this.x == p.x) {
            return this.y - p.y;
        } else {
            return this.x - p.x;
        }
    }
}
```
