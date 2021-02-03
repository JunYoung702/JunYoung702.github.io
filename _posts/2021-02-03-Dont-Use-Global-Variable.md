---
layout: post
title: "DP에서 주의할 점"
date: 2021-02-03 23:55:55 +0900
author: JunYoung
categories: CS 알고리즘
tags: Coding_standards DP Algorithm Global_variable
math: true
---

알고리즘책 연습문제 잠깐 해보는데 귀찮다고 배열을 전역변수로 썼다가 디버깅하는데 몇시간 날려먹었다...

# 전역변수 쓰지말자

```java
    public static double binomial(int N, int k, double p)
    {
        if (N < 0 || k < 0) return 0.0;
        if (arr[N][k] != 0.0)
        {
            return arr[N][k];
        }
        if (N == k)
        {
            arr[N][k] = Math.pow(p, N);
            return arr[N][k];
        } else if (k == 0)
        {
            arr[N][k] = Math.pow(1.0 - p, N);
            return arr[N][k];
        } else
        {
            arr[N][k] = p * binomial(N - 1, k - 1, p) + (1.0 - p) * binomial(N - 1, k, p);
            return arr[N][k];
        }
    }

    public static double binomial2(int N, int k, double p)
    {
        double[][] b = new double[N + 1][k + 1];

        for (int i = 0; i <= N; i++)
            b[i][0] = Math.pow(1.0 - p, i);
        b[0][0] = 1.0;

        for (int i = 1; i <= N; i++)
        {
            for (int j = 1; j <= k; j++)
            {
                b[i][j] = p * b[i - 1][j - 1] + (1.0 - p) * b[i - 1][j];
            }
        }
        return b[N][k];
    }
```

문제 자체는 매우 단순한데 자꾸 binomial과 binomial2의 리턴값이 달라서 이리저리 디버깅했는데
binomial에 인풋을 서로 다른걸 주고 두번 불렀더니 arr에 첫번째 리턴값이 저장된걸 두번째에서도 리턴하는데
두번째랑 첫번째 p값이 달라서 결괏값이 달라졌다.

전역변수쓰면 디버깅이 힘들어지고 오류난다는걸 말로만 들었었는데 직접 몇시간 날려가며 뼈저리게 깨달았다

다음부턴 이러지 말아야지...

# DP구현시 base case처리를 잘 생각하자

```java
    public static double binomialRec(int N, int k, double p)
    {
        if (N == 0 && k == 0) return 1.0;
        if (N < 0 || k < 0)
            return 0.0;
        return p * binomialRec(N - 1, k - 1, p) + (1 - p) * binomialRec(N - 1, k, p);
    }
```

recursive버전의 원본은 이건데

저걸 그대로 DP로 옮기기만 해서

```java
    public static double binomial(int N, int k, double p)
    {
        if (N < 0 || k < 0) return 0.0;
        if (arr[N][k] != 0.0)
        {
            return arr[N][k];
        }
        if (N == 0 || k == 0)
        {
            arr[N][k] = 1.0;
            return arr[N][k];
        } else
        {
            arr[N][k] = p * binomial(N - 1, k - 1, p) + (1.0 - p) * binomial(N - 1, k, p);
            return arr[N][k];
        }
    }
```

이렇게 하거나

```java
    public static double binomial(int N, int k, double p)
    {
        if (N < 0 || k < 0) return 0.0;
        if (arr[N][k] != 0.0)
        {
            return arr[N][k];
        }
        if (k == 0)
        {
            arr[N][k] = Math.pow(1.0 - p, N);
            return arr[N][k];
        } else
        {
            arr[N][k] = p * binomial(N - 1, k - 1, p) + (1.0 - p) * binomial(N - 1, k, p);
            return arr[N][k];
        }
    }
```

bottom-up 솔루션처럼 이렇게 하면 매우 느리다.

반면, `k == 0`을 처리하는 부분은 제거해도 별로 영향을 안 미쳤다.

bottom-up 솔루션의 경우에는 어차피 자명하게 $$O(nk)$$인데,
`n == k` 와 `k == 0`은 좀 차이가 있다.

DP를 배울때 흔히 하듯이 함수 호출을 트리 형태로 그려보면,
한번 호출한 케이스는 기억하므로(즉 한 번 들어간 노드는 다시 들어갈 필요가 없으므로)
시간복잡도는 노드의 개수에 비례할 것을 알 수 있다.
`k == 0`을 따로 처리를 안 해도,

```
binomial(m, 0) -> binomial(m - 1, 0) -> ... -> binomial(0, 0)
```

으로, linear한 횟수의 연산이 추가될 뿐이다. `binomial(n, k)`
로 시작하면 `binomial(n - k, 0)` 부터 `binomial(n, 0)`
까지의 경우의 수가 존재한다. 즉
노드가 $$ n - k + 1$$ 개 추가된다. 따라서 연산 비용에 큰 증가가 없을 것임을 알 수 있다.

반면, `n == k`를 처리하지 않으면,

```
binomial(k, k) -> binomial(k - 1, k - 1) ...
               -> binomial(k - 1, k) ...
```

로 쭉 증가하여 `n == 0`이 될 때까지 노드의 개수가 증가할 것이다.
트리의 깊이가 최대 $$n - k$$만큼 증가하므로
트리의 노드의 개수가 이에 비례하여 지수적으로 증가하게 되고, 연산 횟수도 지수적으로 증가하게 된다.

물론 DP를 아예 안 쓸 때보다는 한참 작지만(적어도 같은 노드에 두번 들어가는 일은 없으니)
그래도 `n == k`를 처리하지 않을 때와는 비교도 안 되게 크다.
(실제로 `n = 100, k = 50`정도만 넣어서 계산해 봐도 차이가 엄청 큼을 알 수 있다.)

원래 이항계수 구현할 때는 항상 `n == k`를 당연히 처리했었는데,
이번에 연습문제 풀면서 그냥 책에 나와있는 재귀함수를 그대로 옮기다 보니 처음 알았다.
