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
                    array[j] = temp;
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
            array[i] = temp;
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

기본적인 동작 과정은 우선 간격을 설정하고 각 간격끼리 분류된 서브 리스트에서 삽입 정렬을 실행한다. 그 다음 간격을 줄인 다음에 다시한번 삽입 정렬을 실행한다. 이 과정을 간격이 1이 될때 까지 반복하여 전체적인 삽입정렬을 실행한다.

쉘 정렬은 간격의 설정에 따라서 알고리즘의 성능이 달라진다. 고로 갭의 크기를 정하는 것이 중요한데 여기서는 성능이 가장 좋다고 알려진 Marcin Ciura's gap sequence를 이용한다.

Marcin Ciura's gap sequence는 1, 4, 10, 23, 57, 132, 301, 701 까지 알려져 있지만 여기에 2.25를 곱해 더 큰 간격을 설정할 수 있다.

*구현*
```java
class Shell {
    int[] array;
    int temp, index;
    int[] gaps =
            { 1, 4, 10, 23, 57, 132, 301, 701, 1750, 3937, 8858, 19930, 44842, 100894,
            227011, 510774, 1149241, 2585792, 5818032, 13090572};

    Shell(int[] num) {
        array = num;
    }

    public void start() {
        System.out.println("쉘정렬 시작");
        for (index = 0; gaps[index] > array.length; index++) {}
        long start = System.currentTimeMillis();
        while (index >= 0) {
            int step = gaps[index--];
            for (int i = step; i < array.length; i++)
                for (int j = i; j >= step && array[j] < array[j-step]; j -= step) {
                    temp = array[j];
                    array[j] = array[j-step];
                    array[j-step] = temp;
                }
        }
        long end = System.currentTimeMillis();
        System.out.println("쉘정렬 종료, 소요시간: " + (end - start) +" ms");
    }
```

## 전체 코드
``` java
package Lab01;
import java.util.Scanner;

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
                    array[j] = temp;
                }
        long end = System.currentTimeMillis();
        System.out.println("버블정렬 종료, 소요시간: " + (end - start) +" ms");
    }
}

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
            array[i] = temp;
        }
        long end = System.currentTimeMillis();
        System.out.println("선택정렬 종료, 소요시간: " + (end - start) +" ms");
    }
}

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

class Shell {
    int[] array;
    int temp, index;
    int[] gaps =
            { 1, 4, 10, 23, 57, 132, 301, 701, 1750, 3937, 8858, 19930, 44842, 100894,
            227011, 510774, 1149241, 2585792, 5818032, 13090572};

    Shell(int[] num) {
        array = num;
    }

    public void start() {
        System.out.println("쉘정렬 시작");
        for (index = 0; gaps[index] > array.length; index++) {}
        long start = System.currentTimeMillis();
        while (index >= 0) {
            int step = gaps[index--];
            for (int i = step; i < array.length; i++)
                for (int j = i; j >= step && array[j] < array[j-step]; j -= step) {
                    temp = array[j];
                    array[j] = array[j-step];
                    array[j-step] = temp;
                }
        }
        long end = System.currentTimeMillis();
        System.out.println("쉘정렬 종료, 소요시간: " + (end - start) +" ms");
    }
}

public class Sorting {
    public static void main(String[] args) {
        System.out.print("배열크기를 입력하세요: ");
        Scanner sc = new Scanner(System.in);
        int size = sc.nextInt();

        int[] num = new int[size];

        for (int i = 0; i < size; i++) {
            num[i] = (int) (Math.random() * 100);
            //System.out.print(num[i] + " ");
        }
        System.out.println("난수배열 생성");
        System.out.println();

        Bubble bubble = new Bubble(num);
        Selection selection = new Selection(num);
        Insertion insertion = new Insertion(num);
        Shell shell = new Shell(num);

        bubble.start();
        selection.start();
        insertion.start();
        shell.start();
    }
}
```

## 시간복잡도 
