## 🎯Goal
- basic concepts of PyTorch Framework
-  simple logistic regression and multinomial logistic regression (softmax) with PyTorch
- simple linear model and multi-layer perceptron (MLP)
---
# Contents
## Numpy vs PyTorch tensor
### 1. Same operations w/ identical grammar
#### shape vs size()
numpy는 `np_array_1.shape` 처럼 shape 함수를 써야하는데, PyTorch는 `torch_tensor_1.shape` `torch_tensor_1.size()` 둘 다 같은 결과를 내보낸다.

### 2. Same operations with different grammar
#### np.concatenate vs torch.cat
[[🧩AI504 - Python practice_Week1#Stack, concatenation]]

- axis(numpy) and dim(torch)는 identical하다.
```PyTorch
torch_concate=torch.cat([torch_tensor_1, torch_tensor_2], dim=0)
```

#### reshape (np) vs view (PyTorch)

```PyTorch
torch_reshaped = torch_concate.view(4,2)
```

### 3. Different operations with same grammar
#### repeat
repeat을 그냥 expansion이라 생각하자. 
python : 원소별로 expansion
PyTorch : 하나의 배열을 기본 단위로 expansion
```Python
x = np.array([1,2,3])
x_repeat = x.repeat(2) #[1 1 2 2 3 3]

x = torch.tensor([1,2,3])
x_repeat = x.repeat(2) # [1 2 3 1 2 3]

######
x_repeat = x.view(3,1) # [1],[2],[3]
x_repeat = x_repeat.repeat(2,3) ## expansion이라 생각하면 됨.
x_repeat = x_repeat.view(-1) # [1,1,1,2,2,2,3,3,3,1,1,1,2,2,2,3,3,3]
```

#### stack 
torch.cat() : 주어진 차원을 기준으로 텐서들을 붙이기
torch.stack() : 새로운 차원으로 텐서를 붙이기.

```PyTorch
x = torch.tensor([1,2,3])
x_repeat = x.repeat(4) # [1,2,3,1,2,3,1,2,3,1,2,3]
x_stack = torch.stack([x, x, x, x]) #[[1,2,3],[1,2,3],[1,2,3],[1,2,3]]

```


## Tensor operations under GPU utilization

```
a = torch.ones(3)
b = torch.randn(100,50,3) # 100(row)*50(column)*3(layer)로 만듦 # rgb 이미지로 생각을 하면 되나봐, 100개의 sample, 50개의 특성(생상, 밝기), 3개의 layer(rgb)
b = torch.randn(4,2,3) # 4개의 layer, 2(row)*3(column)
```