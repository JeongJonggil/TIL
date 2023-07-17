```
T = int(input())

result2 = 0
result3 = 0

for test_case in range(1, T + 1):
    N,M = map(int,input().split())
    numbers1 = list(map(int,input().split()))
    numbers2 = list(map(int,input().split()))

    if N < M:
        for j in range(M - N + 1):  #작은 리스트의 이동가능 횟수
            result1 = 0

            for i in range(N):
                result1 += numbers1[i] * numbers2[i+j]
                result2 = result1

        if result2 >= result1:
            result3 = result2

        elif result1 >= result2:
            result3 = result1

    elif N > M:
        for j in range(N - M + 1):  #작은 리스트의 이동가능 횟수
            result1 = 0

            for i in range(M):
                result1 += numbers2[i] * numbers1[i+j]
                result2 = result1

        if result2 >= result1:
            result3 = result2

        elif result1 >= result2:
            result3 = result1

    print(f'#{test_case} {result3}')
```


