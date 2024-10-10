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
```Python
x = np.array([1,2,3])
x_repeat = x.repeat(2) #[1 1 2 2 3 3]
```