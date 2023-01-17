##  [BoxBlur](https://github.com/MarbleHE/HECO/blob/main/test/bench/BoxBlur.cpp)

## [DotProduct](https://github.com/MarbleHE/HECO/blob/main/test/bench/DotProduct.cpp)

```
// input
x, y: int vector of length n 

// pseudocode
sum = 0
for i = 0; i < n; ++i 
	sum += x[i] * y[i]
```

## [GxKernel](https://github.com/MarbleHE/HECO/blob/main/test/bench/GxKernel.cpp)

```
// input
img: int vector of length imgSize^2 where a pixel (x,y) in image is at x*imgSize + y in img 

// pseudocode
new img2;
for y = 0; y < img_size; ++y 
	img2[0*img_size+y] = 
		img[(-1*img_size+y)%img_size] - img[(1*img_size+y)%img_size]

```

## [GyKernel](https://github.com/MarbleHE/HECO/blob/main/test/bench/GyKernel.cpp)

## [HammingDistance](https://github.com/MarbleHE/HECO/blob/main/test/bench/HammingDistance.cpp)

```
// input
x, y: bool vector of length n 

// pseudocode
sum = 0
for i = 0; i < n; ++i 
	sum += (x[i] - y[i])^2
```

## [L2Distance](https://github.com/MarbleHE/HECO/blob/main/test/bench/L2Distance.cpp)

```
// input
x, y: int vector of length n 

// pseudocode
sum = 0
for i = 0; i < n; ++i 
	sum += (x[i] - y[i])^2
```

## [LaplaceSharpening](https://github.com/MarbleHE/HECO/blob/main/test/bench/LaplaceSharpening.cpp)

```
// input
img: vector of length n 

// pseudocode
result;
weight_matrix = {1, 1, 1, 1, -8, 1, 1, 1, 1};
for (int x = 0; x < img_size; ++x) {
	for (int y = 0; y < img_size; ++y) {
		value = 0;
		for (int j = -1; j < 2; ++j) {
			for (int i = -1; i < 2; ++i) {
				pixel = img[((x + i)*img_size + (y + j))%img_size];

			if (weight_matrix[i]!=1) {
				evaluator.multiply_plain_inplace(pixel, w_ptxts[(i + 1)*3 + (j + 1)]);
			}
			value += pixel;
			}
		}

		two_times = img[img_size*x + y] + img[img_size*x + y];

		two_times -= value;
		result[img_size*x + y] = two_times;
	}
}
```

## [LinearPolynomial](https://github.com/MarbleHE/HECO/blob/main/test/bench/LinearPolynomial.cpp)

```
// input
a, b, x, y: int vector of length n 

// pseudocode
result;
for i = 0; i < n; ++i 
	result[i] = y[i] - a[i] * x[i] - b[i]
```

## [MultiTimer](https://github.com/MarbleHE/HECO/blob/main/test/bench/MultiTimer.cpp)

## [QuadraticPolynomial](https://github.com/MarbleHE/HECO/blob/main/test/bench/QuadraticPolynomial.cpp)

```
// input
a, b, c, x, y: int vector of length n 

// pseudocode
result;
for i = 0; i < n; ++i 
	result[i] = y[i] - a[i] * x[i] - b[i]
```

## [RobertsCross](https://github.com/MarbleHE/HECO/blob/main/test/bench/RobertsCross.cpp)