# ResNet 학습
1. ResNetBlock을 만들고나서
2. 전체 ResNet에 위 block을 얼마나 넣을지 결정해서 모델을 구현.

## 주의할 점.
1. identity mapping을 할 때, channel  수와 image dimension을 맞춰주고 더하자.  
	→ ```
```PyTorch
def down_sampling(self, x) : 
    out = F.pad(x, (0,0,0,0,0,self.out_channels - self.in_channels))
    out = nn.MaxPool2d(2, stride=self.stride)(out)
    return out
```

2. nn.Modulelist
```PyTorch
def get_layers(self, block, in_channels, out_channels, stride):
	if stride == 2:
		down_sample = True
	else:
		down_sample = False
		
	layer_list = nn.ModuleList([block(in_channels, out_channels, stride, down_sample)])
	

for _ in range(self.num_layers -1) :
	layer_list.append(block(out_channels, out_channels, stride=1, down_sample=False))

return nn.Sequential(*layer_list)
```
여기서 맨 처음 `layer)list = nn.ModuleList([block(~~~)])`하는데 이 때 []를 넣어주어야함.
return은 nn.Sequential