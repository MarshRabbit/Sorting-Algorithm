# Sorting-Algorithm

## 버블정렬이란
버블 정렬은 두 인접한 데이터를 비교해서 앞에 있는 데이터가 뒤에 있는 데이터보다 크면 자리를 바꾸는 정렬 알고리즘이다.

1번째부터 마지막 n번째 까지 정렬하면 마지막 수가 가장 큰 수 이고 다시 처음으로 돌아가 n-1번째 까지 돌면서 최종적으로 n(n-2)/2번 정렬된다

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

## 
