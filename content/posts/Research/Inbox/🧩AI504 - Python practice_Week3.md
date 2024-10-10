## 🎯Goal
- basic concepts of PyTorch Framework
-  simple logistic regression and multinomial logistic regression (softmax) with PyTorch
- simple linear model and multi-layer perceptron (MLP)
- reference : [Jinsol Kim](https://gaussian37.github.io/dl-pytorch-snippets/)
	- GPU에 있을 때에는 CPU로 변경 후 np로 변경해야한다.
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
b = torch.randn(4,2,3) # normal distribution으로 4개의 layer, 2(row)*3(column)
```

![[Pasted image 20241010110802.png]]

## Autograd
`x = torch.ones(2,2, requires_grad=True)` : requires_grad 켜줘야 해당 변수에 대한 연산을 tracking함.
마지막 loss function이든 행렬에서 .backward()를 해주면 gradient를 자동적으로 계산함.
`out.backward()` 이후 , `print(z.grad)`

근데 메모리 효율성을 위해 연산 history tracking을 금지하고 싶으면, `torch.no_grad()`를 사용하면 됨. → Testset 돌릴 때!

```PyTorch
with torch.no_grad(): 
	x = torch.ones(2,2, requires_grad=True)
	y = x + 2
	z = y * y * 3
	out = z.mean()
```


## nn.Module

```PyTorch
class Model(nn.Module):

def __init__(self, input_dim, output_dim, hidden_dim):
	super(Model, self).__init__()
	self.linear_1 = nn.Linear(input_dim, hidden_dim)
	self.linear_2 = nn.Linear(hidden_dim, output_dim)
	self.relu = nn.ReLU()

def forward(self, x):
	x = self.linear_1(x)
	x = self.relu(x) # Activation function
	x = self.linear_2(x)

return x
```

##### Train
```PyTorch
model = Multinomial_logistic_regression(784, 10) # init(784, 10)
model = model.to('cuda')
optimizer = torch.optim.SGD(model.parameters(), lr=0.05, momentum=0.9)

# Loss function define (we use cross-entropy)

loss_fn = nn.CrossEntropyLoss()

  
#Train the model
total_step = len(train_loader)

for epoch in range(10):
	for i, (images, labels) in enumerate(train_loader): # mini batch for loop
		# upload to gpu
		images = images.reshape(-1, 28*28).to('cuda') # -1이 batch_size
		labels = labels.to('cuda')
		
		# Forward
		outputs = model(images) # forwardI(images): get prediction, model(images)하면 자동적으로 forward함수가 호출이 된대.
		
		loss = loss_fn(outputs, labels) # calculate the loss (cross entropy loss) with ground truth & prediction value
		
		# Backward and optimize
		optimizer.zero_grad()
		loss.backward() # automatic gradient calculation (autograd)
		optimizer.step() # update model parameter with requires_grad=True
		
		if (i+1) % 100 == 0:
		print ('Epoch [{}/{}], Step [{}/{}], Loss: {:.4f}'
		.format(epoch+1, 10, i+1, total_step, loss.item()))
```

##### Test
```PyTorch
# Test the model
# In test phase, we don't need to compute gradients (for memory efficiency)

with torch.no_grad():
	correct = 0
	total = 0
	for images, labels in test_loader:
	
		images = images.reshape(-1, 28*28).to('cuda')
		labels = labels.to('cuda')
		outputs = model(images)
		_, predicted = torch.max(outputs.data, 1) # classification -> get the label prediction of top 1
		total += labels.size(0)
		correct += (predicted == labels).sum().item()
	
	print('Accuracy of the network on the 10000 test images: {} %'.format(100 * correct / total))
```