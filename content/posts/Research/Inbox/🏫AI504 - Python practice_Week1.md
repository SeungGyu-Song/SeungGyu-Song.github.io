# Week 1
d = np.array([[[1., 2., 3.], [4., 5., 6.]], [[7., 8., 9.], [10., 11., 12.]]])`
a.ndim = 3, a.shape=(2,2,3)

`a = np.arange(10)`
a[8:5:-1], slicing에서 두 번째 거는 excluding으로 생각하면 됨.

``` Python
a = np.arange(3*2).reshape((3,2))
print(a>2) -## a의 인덱스별로 True/ False 나옴.

print(a[a>2]) ## 배열 안의 값에 대해 체크하고, return값은 index에 대한 true / false구나.
```
### Tuple indexing vs ndarray indexing
```Python
#Tuple indexing vs ndarray indexing
a = np.arange(24).reshape((6,4))
idx = ((0,0,1,5),(1,2,0,3))

print_obj(a[idx], "tuple indexing") #진짜 몇 컴마 몇 에 해당하는 값 1*4로 출력

idx = np.array([[0,0,1,5],[1,2,0,3]]) # index가 행렬이므로 아래 줄의 결과는 2*4*4

print_obj(a[idx], "ndarray indexing")
```
### Ellipsis (:,:,:,…: 을 그냥 …로)
```Python
# 둘의 결과는 같음.
print_obj(a[1,:,:,:,:,2], "Plain indexing")

print_obj(a[1,...,2], "Ellipsis")
```

### Unary Operations
```Python
a = np.arange(6).reshape((3,2))

print_obj(a.sum(), "a.sum()")
print_obj(a.sum(axis=0), "a.sum(axis=0)") # row별 더하기.(column wise)# 1,2
print_obj(a.sum(axis=1), "a.sum(axis=1)") # column별 더하기.(row wise)# 1,3

# Quiz: Given a = np.arange(24).reshape((2,3,4)), what is the mean of the sum w.r.t to the last dimension?

a = np.arange(24).reshape((2,3,4))

b = a.mean(axis=-1) #column별 더하기, (2,3)차원.
```

### Dot product
1차벡터끼리는 inner product인데 2차원 행렬 넘어가서부터는 그냥 행렬곱임
```Python
a = np.arange(24).reshape((4, 3, 2))
b = np.ones((4, 2, 3))
print_obj(a, "a")
print_obj(b, "b")

print_obj(np.dot(a,b).shape, "a dot b")
print_obj((a@b).shape, "a @ b") # @을 사용해야 high dimension에서 정확한 결과를 얻을 수 있따.
```
### Extra dimention
```Python
# Adding an extra dimension !!

a = np.arange(3)
print_obj(a, "a")

print_obj(a[:, None], "a[:, None]")

# Quiz: How to make a = np.ones((3,4)) into shape (3, 1, 1, 4) using reshape and None?

a=np.ones((3,4))
print(a[:,None,None,:])
```

### Stack, concatenation
`np.vstack([a,b])  === np.concatenate([a,b], axis=0) ` row방향 (row 옆에다)
`np.hstack([a,b])   === np.concatenate([a,b], axis=1)` column 방향 (column 옆에다)

`np.hstack([a,b,a])`

### Transpose
```Python
a = np.arange(24).reshape((4, 3, 2))

b = np.transpose(a, [0, 2, 1])
print_obj(b, "Swap axis 1 and 2")
print_obj(b.shape, "b's shape")
```

### Broadcasting
행렬의 연산에서 둘의 차원이 안 맞으면 높여줄 수 있는 애한테 같은 값을 복사해서 차원을 맞춰줌