## [Sobel filtering](https://github.com/microsoft/EVA/blob/a5fbcce9d7d2ff2549ebe4ad4faec23fa3d4873c/examples/image_processing.py)

``` python
from EVA import *

# sqrt evaluates a 3rd degree polynomial approximation of square root.
def sqrt(x):
  return x*constant(scale, 2.214) +
    (x**2)*constant(scale, -1.098) +
    (x**3)*constant(scale, 0.173)

program = Program(vec_size=64*64)
scale = 30
with program:
  image = inputEncrypted(scale)
  F = [[-1, 0, 1],
		[-2, 0, 2],
        [-1, 0, 1]]
  for i in range(3):
    for j in range(3):
      rot = image << (i*64+j)
      h = rot * constant(scale, F[i][j])
      v = rot * constant(scale, F[j][i])
      first = i == 0 and j == 0
      Ix = h if first else Ix + h
      Iy = v if first else Iy + v

  d = sqrt(Ix**2 + Iy**2)
  output(d, scale)
```

## [Harris filtering](https://github.com/microsoft/EVA/blob/a5fbcce9d7d2ff2549ebe4ad4faec23fa3d4873c/examples/image_processing.py)

``` python
from EVA import *

def convolutionXY(image, width, filter):
  for i in range(len(filter)):
    for j in range(len(filter[0])):
      rotated = image << (i * width + j)
      horizontal = rotated * filter[i][j]
      vertical = rotated * filter[j][i]
      if i == 0 and j == 0:
        Ix = horizontal
        Iy = vertical
      else:
        Ix += horizontal
        Iy += vertical
  return Ix, Iy

harris = EvaProgram('harris', vec_size=h*w)

with harris:
image = Input('image')

sobel_filter = [
  [-1, 0, 1],
  [-2, 0, 2],
  [-1, 0, 1]]

pool = [
[1, 1, 1],
[1, 1, 1],
[1, 1, 1]]

c = 0.04

Ix, Iy = convolutionXY(image, w, sobel_filter)
Ixx = Ix**2
Iyy = Iy**2
Ixy = Ix * Iy

#FIX: masking may be needed here (to handle boundaries)

Sxx = convolution(Ixx, w, pool)
Syy = convolution(Iyy, w, pool)
Sxy = convolution(Ixy, w, pool)

SxxSyy = Sxx * Syy
SxySxy = Sxy * Sxy
det = SxxSyy - SxySxy
trace = Sxx + Syy

Output('image', det - trace**2 * c)
```