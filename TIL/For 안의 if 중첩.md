# For 안의 if 중첩

For문 안에 if 문이 동위치 블럭 단위로 되어 있으면 여러 조건을 만족하더라도 가장 처음 만난 if문만 실행된다.

```
    for i in range(len(move_types)):
        if plan == move_types[i]:
            nx = x + dx[i]
            ny = y + dy[i]

        if nx < 1 or nx > n or ny < 1 or ny > n:
            continue
```

위의 경우 

1. if plan == move_types[i]:

2. if nx < 1 or nx > n or ny < 1 or ny

두 가지 중 1, 2번 두가지를 만족하는 상황이더라도 1번 조건만 실행 된다는 뜻


