---
title: <Fill me w/ a compact title>
draft: true
tags:
---
## Generator
### model 만들기
noise를 통해서 이미지를 만드는 거니까 noise 차원에서부터 시작하기.
→ `torch.randn(128,100)`

```PyTorch
for epoch in range(n_epoch):
	for i, (data, _) in enumerate(dataloader):

		####################################################
		
		# (1) Update D network: maximize log(D(x)) + log(1 - D(G(z))) #
		
		###################################################
		
		# train with real
		
		netD.zero_grad()
		data = data.cuda()
		batch_size = data.size(0)
		label = torch.ones((batch_size,)).cuda()# real label = 1
		output = netD(data)
		errD_real = criterion(output, label)
		
		# train with fake
		
		noise = torch.randn(batch_size, 100).cuda()
		fake = netG(noise)
		label = torch.zeros((batch_size, )).cuda() # fake label #zeros
		output = netD(fake.detach())
		errD_fake = criterion(output, label)
		D_G_z1 = output.mean().item()
		
		# Loss backward
		
		errD = errD_real + errD_fake
		errD.backward()
		optimizerD.step()
		
		########################################
		
		# (2) Update G network: maximize log(D(G(z))) #
		
		########################################
		
		netG.zero_grad()
		label = torch.ones((batch_size, )).cuda() # fake labels are real for generator cost
		output = netD(fake)
		errG = criterion(output, label)
		D_G_z2 = output.mean().item()
		
		errG.backward()
		
		optimizerG.step()
```

코드에서 보면, (1)에서 label에 `ones`로 초기화하는 것과 `zeros`로 초기화하는 것을 볼 수 있다.
D(x)의 경우, `ones`로 초기화해주고, D(G(z))의 경우는 `zeros`로 초기화해준다. 
log(1-D(G(z)))는 0에 가까워져야하니까 정답을 0으로 주니까 그런 것 같다.