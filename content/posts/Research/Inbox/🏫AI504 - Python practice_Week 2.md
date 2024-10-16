Plot과 기본 ML 방식에 대해 학습함
## Import
```Python
import numpy as np
from matplotlib import pyplot as plt
import sklearn
```
### Plot vs scatter
```Python
plt.plot([1,2,3], [3,2,1])

plt.scatter([1,2,3], [3,2,1])

plt.show()
```

### Drawing a function
```Python
foo = lambda x: -(2/7*x**3-9/2*x**2+15*x-10.) # 함수 작성할 때 x**3 이런 거 복습.
x_line = np.linspace(0, 10, 100)


# Quiz: Draw the function foo using x_line

y_line = foo(x_line)
plt.plot(x_line, y_line)
plt.show()
```
#### Random 값 주기 : 차원 맞춰서 사이즈 기입하는 거 잊지 않기.
```Python
#np.random.rand 할 때 seed 설치하고 np.random.rand
np.random.seed(10)
y_sample = foo(x_sample) + np.random.rand(sample_size)

# Gaussian noise.
#y_sample = foo(x_sample) + np.random.normal(loc=0, scale=0.1, size=sample_size)
```

# Iris dataset
150장 데이터셋, 3개의 종류로 구별해야하고, 4개의 feature가 있음.
X : [150,4], y:[150, ]
y의 index 값에는 0, 1, 2가 있을 거고, X는 150장 하나하나에 대해 각 feature의 값들이 들어있음.

### Subplot
```Python
y_logistic = logistic.predict(X_test[:, :2])
y_svc = svc.predict(X_test[:, :2])
y_tree = tree.predict(X_test[:, :2])

plt.figure(figsize=(20,5))

plt.subplot(141)
plt.title('Logistic Regression')
plt.scatter(X_test[:, 0], X_test[:, 1], c=y_logistic)

plt.subplot(142)
plt.title('SVM')
plt.scatter(X_test[:, 0], X_test[:, 1], c=y_svc)

plt.subplot(143)
plt.title('Decision Tree')
plt.scatter(X_test[:, 0], X_test[:, 1], c=y_tree)

plt.subplot(144)
plt.title('Ground Truth')
plt.scatter(X_test[:, 0], X_test[:, 1], c=y_test)

plt.show()
```
plt에서 그릴 때, c= y_logistic 이렇게 쓰면 색깔은 알아서 지정이 됨.