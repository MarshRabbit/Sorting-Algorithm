# Sorting-Algorithm

## 버블정렬이란
버블 정렬은 두 인접한 데이터를 비교해서 앞에 있는 데이터가 뒤에 있는 데이터보다 크면 자리를 바꾸는 정렬 알고리즘이다.

1번째부터 마지막 n번째 까지 정렬하면 마지막 수가 가장 큰 값이고 다시 처음으로 돌아가 n-1번째 까지 돌면서 최종적으로 n(n-2)/2번 정렬된다

*구현*
``` java
class Bubble {
    int[] array;
    int temp;

    Bubble(int[] num) {
        array = num;
    }

    public void start() {
        System.out.println("버블정렬 시작");
        long start = System.currentTimeMillis();
        for (int i = 0; i < array.length - 1; i++)
            for (int j = 1; j < array.length - i; j++)
                if (array[j] < array[j - 1]) {
                    temp = array[j - 1];
                    array[j - 1] = array[j];
                    array[j] = array[j - 1];
                }
        long end = System.currentTimeMillis();
        System.out.println("버블정렬 종료, 소요시간: " + (end - start) +" ms");
    }
}
```

## 선택정렬이란
선택 정렬은 주어진 데이터 속에서 가장 작은 값을 찾아내 맨 앞자리 수와 교환한다. 그 다음 두 번째 수 부터 시작하여 가장 작은 값을 찾아 두번째 수와 교환한다.

이 과정을 n-1번 반복하여 총 n(n-2)/2번 정렬된다.

*구현*
```java
class Selection {
    int[] array;
    int temp;

    Selection(int[] num) {
        array = num;
    }

    public void start() {
        System.out.println("선택정렬 시작");
        long start = System.currentTimeMillis();
        for (int i = 0; i < array.length - 1; i++) {
            int index = i;
            for (int j = i + 1; j < array.length; j++)
                if (array[index] > array[j])
                    index = j;
            temp = array[index];
            array[index] = array[i];
            array[i] = array[index];
        }
        long end = System.currentTimeMillis();
        System.out.println("선택정렬 종료, 소요시간: " + (end - start) +" ms");
    }
}
```

## 삽입정렬이란
삽입정렬은 배열의 앞부분을 정렬된 부분으로, 배열의 뒷부분을 정렬이 안 된 부분으로 나누고 정렬이 안 된 부분의 가장 왼쪽 값을 정렬된 부분에서 선택한 값보다 작은수가 나올때 까지 오른쪽으로 밀고 그 자리에 삽입하는 방식이다.

*구현*
``` java
class Insertion {
    int[] array;
    int temp, j;

    Insertion(int[] num) {
        array = num;
    }

    public void start() {
        System.out.println("삽입정렬 시작");
        long start = System.currentTimeMillis();
        for (int i = 1; i < array.length; i++) {
            temp = array[i];
            for (j = i - 1; j >= 0 && temp < array[j]; j--)
                array[j+1] = array[j];
            array[j +1] = temp;
        }
        long end = System.currentTimeMillis();
        System.out.println("삽입정렬 종료, 소요시간: " + (end - start) +" ms");
    }
}
```

## 쉘정렬이란
쉘 정렬은 삽입 정렬이 거의 정렬된 배열에서 최적의 성능을 내는 것에서 착안하여 삽입 정렬의 장점을 살리면서 단점을 최소화 하기 위해 고안한 정렬 방법이다. 
