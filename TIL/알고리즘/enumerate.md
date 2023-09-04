# enumerate

## : list에서 index, 요소를 튜플형 리스트로 출력하는 함수

     enumerate(list)    →     [(index, 값), (index, 값) ]과 같이 튜플형 리스트로 출력됨

```
fruits = ['apple','bannan','cherry']

for index, fruit in enumerate(fruits):
    print(f'{index} : {fruit}')

0 : apple
1 : banana
2 : cherry
```




