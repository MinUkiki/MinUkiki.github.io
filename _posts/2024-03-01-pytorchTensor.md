---
title : "Pytorch Tensor vs tensor"
excerpt: "Pytorch Tensor vs tensor"
categories:
  - AI
tag:
  - AI
toc: true
toc_sticky: true
use_math: true
---

# Tensor vs tensor

Pytorch에서 텐서를 생성할 때 쓸수 있는 두가지 함수가 있다.

바로 Tensor(), tensor()이다.

이 글은 두 함수의 차이점에 대해서 알아보려고 작성한다.

가장 간단하게 비교를 해보자

```python

print(f"tensor : {torch.tensor([1,2])}")
print(f"Tensor : {torch.Tensor([1,2])}")

print(f"tensor : {torch.tensor([1,2]).dtype}")
print(f"Tensor : {torch.Tensor([1,2]).dtype}")

''' output

tensor : tensor([1, 2])
Tensor : tensor([1., 2.])

tensor : torch.int64
Tensor : torch.float32

'''
```

여기서 확인할 수 있는 점은 Tensor()는 type를 Float 고정이며, tensor()는 입력 데이터에 따라 type이 변하게 된다.

또한 Pytorch 공식 문서에서 다음과 같이 명시되어있다.

- torch.tensor() : function
- torch.Tensor() : class

torch.tensor()를 사용하기 위해선 항상 data 파라미터가 있어야한다. torch.tensor(data)는 항상 data를 복사하여 텐서를 생성한다. 간략히 설명하면 다음과 같다.

`torch.tensor(data)` -> `텐서`로 `data`를 입력받아 텐서 객체를 생성한다.

반대로 torch.Tensor()는 비어있는 텐서를 생성할 수 있다.

다음은 `data`로 스칼라 값이 들어온 경우 각각 다른 output을 보여준다.

```python

print(f"tensor : {torch.tensor(10)}")
print(f"Tensor : {torch.Tensor(10)}")

''' output

tensor : 10
Tensor : tensor([-2.1488e-25,  1.7110e-42,  0.0000e+00,  0.0000e+00,  0.0000e+00,0.0000e+00,  0.0000e+00,  0.0000e+00,  0.0000e+00,  0.0000e+00])
'''
```

torch.tensor는 그대로 출력하는 반면에 torch.Tensor는 n개의 리스트를 생성하는 모습이다.

다음은 Pytorch에서 자동 미분을 이용하기 위한 requires_grad 파라미터의 유무이다.

```python
torch.tensor([2.,3.], requires_grad=True)
# torch.Tensor([2.,3.], requires_grad=True) # error

''' output

tensor([2., 3.], requires_grad=True)

'''
```

`torch.tensor()`은 정상적으로 실행이 되는 것을 볼수있다. 반면에 같은 값을 입력으로 받은 `torch.Tensor()`은 오류를 나타낸다.

`torch.Tensor()`에는 requires_grad 파라미터가 존재하지 않지만 다음과 같이 사용할 수 있다.

`torch.Tensor([2.,3.]).requires_grad=True`

`torch.tensor()`는 `data`가 무조건 있기 때문에 기울기를 추적할 수있어 파라미터가 존재하고 `torch.Tensor()`는 빈 텐선를 생성할 수 있기 때문에 파라미터가 존재하지 않는 것으로 생각된다. 

마지막으로 call by value, call by reference에 관한 차이점이다. 

`torch.tensor()`의 경우 `call by vlaue`

```python
# torch.torch의 경우 값을 복사해 Tensor 생성

a = torch.tensor([1])
new_a = torch.tensor(a)

print(f"a : {a},\nnew_a : {new_a}")
print("-"*20)

a[0] = 5
print(f"a : {a},\nnew_a : {new_a}")

''' output

a : tensor([1]),
new_a : tensor([1])
--------------------
a : tensor([5]),
new_a : tensor([1])

'''
```

`torch.Tensor()`의 경우 `call by refrence`, `call by value` 두가지가 존재한다.

- call by refrence

```python

# orch.Tensor은 Tensor 객체를 받으면 메모리 주소값을 복사해 온다.

a = torch.Tensor([1])
new_a = torch.Tensor(a)

print(f"a : {a},\nnew_a : {new_a}")
print("-"*20)

a[0] = 5
print(f"a : {a},\nnew_a : {new_a}")

''' output

a : tensor([1.]),
new_a : tensor([1.])
--------------------
a : tensor([5.]),
new_a : tensor([5.])

'''
```

- call by value

```python
# torch.Tensor은 list나 numpy를 받으면 값을 복사해온다

a = [1]
new_a = torch.Tensor(a)

print(f"a : {a},\nnew_a : {new_a}")
print("-"*20)

a[0] = 5
print(f"a : {a},\nnew_a : {new_a}")

''' output

a : [1],
new_a : tensor([1.])
--------------------
a : [5],
new_a : tensor([1.])

'''
```

# 요약

1. `torch.tensor()`는 입력 데이터에 따라 type이 정해짐, `torch.Tensor()`는 type를 Float 고정

2. `torch.tensor()` : `function` 항상 data 파라미터가 있어야함,  
`torch.Tensor()` : `class` 비어있는 텐서를 생성할 수 있다.

3. `data`로 스칼라 값이 들어온 경우
    - `torch.tensor()`는 `data` 그대로 출력
    - `torch.Tensor()`는 n개의 리스트를 생성

4. requires_grad 파라미터의 유무
    - `torch.tensor()`는 `data`를 받아야하기 때문에 존재
    - `torch.Tensor()`는 빈 텐서를 생성할 수 있기 때문에 없음 ( 하지만 함수로 실행 가능 )

5. `torch.tensor()`는 `call by value`,  
`torch.Tensor()`는 입력이 텐서이면 `call by refrence`, 입력이 리스트이면 `call by value`