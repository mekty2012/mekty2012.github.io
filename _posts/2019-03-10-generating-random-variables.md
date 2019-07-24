---
title: "Construction of Random Variables"
date: 2019-03-10 01:48 -0400
categories: Statistics
---

일반적으로 우리가 '랜덤'을 뜻할때, 실제로는 pseudo-random에 가깝다. 즉 완전 무작위적이지 않고 해당 수열에는 일정한 규칙이 존재한다. 예를 들어 java의 java.util.Random은
```java
public int nextInt() {

  int result = (int)(seed >> (48 - bits))

  seed = (seed * 0x5DEECE66DL + 0xBL) & ((1L << 48) - 1)

}
```
에 의해 생성된다. 실제로 보면 굉장히 무작위적으로 보이지만, 이 랜덤에서 생성된 값들이 충분히 있을때 다음 값을 예측하는 것이 가능하다.

다만 이 글에서는 우리가 [0, 1]에서 균일한 확률 변수 U를 가지고 있다고 가정한다.

## uniform(a, b)
굉장히 간단하다. $$(b - a) \times U + a$$를 반환하면 a, b 상에서 균일한 확률 변수를 만들 수 있다.

## equally distributed n classes
역시 굉장히 간단하다. Floor Function(floor(x)는 x보다 작거나 같은 정수 중 가장 큰 수)을 이용하여 $$\text{floor}(k \times U)$$를 반환하면 $$P(X=i) = \dfrac{1}{n}$$ 인 이산 확률 변수를 만들 수 있다.

## Permuatation of n numbers
먼저 위의 이산 확률 변수를 이용하여 $$\text{floor}(k \times U) + 1$$을 생각하자. 이 확률 변수는 $$1 \ldots n$$의 값을 가진다.

먼저, $$r[1], r[2], \ldots, r[n]$$이 $$1, 2, \ldots, n$$들이 섞여있는 상태라고 보자. 이제 다음과 같은 알고리즘을 통해 이 수열을 섞을 수 있다.

```
k = n
I = floor(k * U) + 1
swap(r[I], r[k])
k = k - 1
if k > 1, goto 1
return r[1], r[2], ... r[n]
```
비슷하게, 위 알고리즘의 루프를 k번 반복하여 마지막 k개의 원소를 반환함으로서 크기가 k인 무작위 부분집합을 만드는 알고리즘을 생각해볼 수 있다.

## Discrete Random Variables
다음과 같은 확률 변수 X를 만들고 싶다고 하자.

$$P(X = x[i]) = p[i], p[1] + p[2] + \ldots + p[n] = 1$$

이를 위해서 다음과 같이 정의한다.

$$X = x[i]\text{ if }p[1] + p[2] + \ldots + p[i-1] < U \le p[1] + p[2] + \ldots + p[i]$$

다르게 쓰면,

$$X = x[1]\text{ if }U \in (0, p[1]]$$

$$X = x[2]\text{ if }U \in (p[1], p[1] + p[2]]$$

\vdots

X = x[i]\text{ if }U \in (p[1] + \ldots + p[i-1], p[1] + \ldots + p[i]]

\vdots

X = x[n]\text{ if }U \in (p[1] + \ldots + p[n-1], 1]

U가 (0, 1)에서 균일하기 때문에, $$P(U \in (a, b]) = b-a$$ 이며, $$P(U \in (p[1] + \ldots p[i-1], p[1] + \ldots + p[i])) = p[i]$$이다.

이 방법을 discrete inverse transform method라고 한다.

## Continuous Random Variables
우리가 생성하고 싶은 연속 확률 변수 X의 누적 분포 함수(Cumulative Distribution Function)을 F라고 하자.

누적 분포 함수는 단조 증가 함수이므로 (0, 1)을 정의역으로 하는 F의 역함수를 생각할 수 있다. 이를 F'이라 하자.

이때 $$X = F'(U)$$는 우리가 원하는 연속 확률 변수가 된다.

### 증명

F가 감소하지 않으므로(단조 증가 함수이므로) $$a\leb$$ 가 $$F(a) \le F(b)$$와 동치이다. 따라서

$$P(F'(U)\lex) = P(F(F'(U))\leF(x)) = P(U \le F(x)) = F(x)$$

X가 누적 분포 함수로 F를 가지기 때문에, X는 우리가 원하는 연속 확률 변수이다.

## Normal Variables
정규 분포의 역함수를 구하는 것이 쉽지 않기 때문에 Box-Muller method라고 불리는 특별한 방법을 사용한다.

먼저, X와 Y가 표준 정규 분포를 따른다고 가정하자. 이때 결합 확률 밀도 함수(Joint Density Distribution Function) f는

$$f(x, y) = \dfrac{1}{\sqrt{2\pi}} exp(-\dfrac{x^2}{2}) \dfrac{1}{\sqrt{2\pi}} exp(- \dfrac{y^2}{2}) = \dfrac{1}{2\pi} exp(-\dfrac{x^2+y^2}{2})$$

이다. 이제, $$(X, Y)$$를 극좌표 $$(R, θ)$$로 나타내보자.

$$R^2 \tilde \Xi^2(2)$$ (자유도 2의 카이제곱 분포)

따라서 $$R^2$$의 분포는  $$f(r) = \dfrac{1}{2} exp(-\dfrac{r}{2})$$ 이다.

이제 $$R^2 = r$$이라고 고정하였을 때

f(x, y) = \dfrac{1}{2\pi} exp(-\dfrac{r}{2})

이며, $$(X, Y)$$는 θ 에 대하여 $$(0, 2π)$$ 에서 균일하게 분포되어있다. 그리고, R은 카이제곱 분포의 특성에 의해 평균이 2인 지수 확률 변수의 제곱근이 된다.

따라서, 다음과 같이 확률 변수를 정의하면

$$R^2 = -2 \log(U[1])$$

$$\Theta = 2\pi U[2]$$

일때, $$X = R cos(θ), Y = R sin(θ)$$으로 결론적으로

$$X = √(-2 log(U[1])) cos(2πU[2]), Y = √(-2 log(U[1])) sin(2πU[2])$$

모두 표준 정규 분포를 따른다.
