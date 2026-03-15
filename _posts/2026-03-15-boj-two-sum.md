---
title: "[BOJ 1002] 두 원 - 수학"
excerpt: "두 원의 교점 개수를 구하는 문제"
categories:
  - BOJ
tags:
  - Math
  - Geometry
  - Silver
date: 2026-03-15
toc: true
toc_sticky: true
---

## 문제 정보

| 항목 | 내용 |
|------|------|
| 문제 번호 | BOJ 1002 |
| 제목 | 두 원 |
| 난이도 | Silver 5 |
| 분류 | 수학, 기하학 |
| 링크 | [BOJ 1002](https://www.acmicpc.net/problem/1002) |

## 문제 설명

조건에 따라 두 원이 서로 만나는 점의 수를 구하는 문제입니다.

두 원의 중심 좌표 (x1, y1), (x2, y2)와 각각의 반지름 r1, r2가 주어질 때, 교점의 수를 구합니다.

## 풀이 접근

두 원의 관계를 **중심 간 거리 d**를 기준으로 판단합니다:

1. **완전히 분리** (d > r1 + r2): 교점 0개
2. **외접** (d == r1 + r2): 교점 1개
3. **두 점 교차** (|r1 - r2| < d < r1 + r2): 교점 2개
4. **내접** (d == |r1 - r2|, d != 0): 교점 1개
5. **내부에 포함** (d < |r1 - r2|): 교점 0개
6. **완전 일치** (d == 0, r1 == r2): 교점 무한개 (-1 출력)

> ⚠️ **주의:** 부동소수점 오류를 피하기 위해 거리 계산 시 제곱 상태로 비교합니다.

## 코드

```python
import sys
input = sys.stdin.readline

T = int(input())
for _ in range(T):
    x1, y1, r1, x2, y2, r2 = map(int, input().split())
    
    # 두 원의 중심 거리의 제곱
    d2 = (x2 - x1)**2 + (y2 - y1)**2
    
    # 두 원이 완전히 같은 경우
    if d2 == 0 and r1 == r2:
        print(-1)
        continue
    
    # 비교를 위해 제곱 값 사용 (부동소수점 오류 방지)
    sum_r = (r1 + r2)**2
    diff_r = (r1 - r2)**2
    
    if d2 == sum_r or d2 == diff_r:
        print(1)
    elif diff_r < d2 < sum_r:
        print(2)
    else:
        print(0)
```

## 복잡도 분석

- **시간 복잡도:** O(T)
- **공간 복잡도:** O(1)

## 핵심 포인트

- 두 원의 위치 관계를 **중심 간 거리**로 판단
- `math.sqrt()` 대신 **제곱 비교**를 사용하여 부동소수점 오류 방지
- 두 원이 완전히 일치하는 엣지 케이스(d=0, r1=r2) 처리 필수

## 유사 문제

- [BOJ 1001 - A-B](https://www.acmicpc.net/problem/1001)
- [BOJ 3009 - 네 번째 점](https://www.acmicpc.net/problem/3009)
