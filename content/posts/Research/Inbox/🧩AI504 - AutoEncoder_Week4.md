---
title: <Fill me w/ a compact title>
draft: true
tags:
---
### 🎯 Goal 
The rest of your content lives here. You can use **Markdown** here :)
- Autoencoder를 PyTorch로 실습하기

# Contents
## Model 식 세울 때
``` PyTorch
class Autoencoder(nn.Module):

	def __init__(self):
		super(Autoencoder,self).__init__()
		self.encoder = nn.Sequential(
			nn.Linear(784, 100),
			nn.ReLU(), # activation function
			nn.Linear(100, 30),
			nn.ReLU() # activation function
		)

		self.decoder = nn.Sequential(
			nn.Linear(30, 100),
			nn.ReLU(), # activation function
			nn.Linear(100, 784),
			nn.Sigmoid() # activation function
		)

	def forward(self, x): # x: (batch_size, 1, 28, 28)
		batch_size = x.size(0)
		x = x.view(-1, 28*28) # reshape to 784(28*28)-dimensional vector #linearize
		encoded = self.encoder(x) # hidden vector
		out = self.decoder(encoded).view(batch_size, 28,28) # final output. resize to input's size
return out, encoded
```

input은 batch_size x 28 x 28로 들어오는데,
모델 안 function에서는 각 이미지 샘플에 대해서만 생각한다.
그런데 `forward` 함수에서는 실제 batch_size까지 고려해서 input output dimension을 고려해야한다.