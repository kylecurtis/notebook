# Tensors in PyTorch

> https://pytorch.org/docs/stable/tensors.html

<br>

---

<br>

## What is a Tensor?

> A [`torch.Tensor`](https://pytorch.org/docs/stable/tensors.html#torch.Tensor "torch.Tensor") is a multi-dimensional matrix containing elements of a single data type.

Tensors are the fundamental data structure in PyTorch, akin to multidimensional arrays or matrices in other libraries like NumPy. However, tensors are optimized for deep learning tasks and can leverage GPU acceleration.

<br>

### Key Characteristics:

#### Parameters

```python
tensor(data, *, dtype=None, device=None, requires_grad=False, pin_memory=False) -> Tensor
```

<br>

#### Dimensionality: 

> Tensors in PyTorch can have various dimensions, and their interpretation depends on the number of axes (or dimensions).
> Below are examples:

<br>

**0-D Tensor (Scalar):** A single number, no axes

```python
scalar = torch.tensor(3.14) # Shape: ()
print(scalar.shape)         # Output: torch.Size([])
```

<br>

**1-D Tensor (Vector):** A single axis, like a list or array.

```python
vector = torch.tensor([1, 2, 3])  # Shape: (3,)
print(vector.shape)               # Output: torch.Size([3])
```

<br>

**2-D Tensor (Matrix):** Two axes, like a table or spreadsheet.

```python
matrix = torch.tensor([[1, 2], [3, 4]])  # Shape: (2, 2)
print(matrix.shape)                      # Output: torch.Size([2, 2])
```

<br>

**3-D Tensor:** Typically used to represent a stack of matrices, like RGB images.

```python
tensor_3d = torch.rand(3, 4, 5)  # Shape: (3, 4, 5)
print(tensor_3d.shape)           # Output: torch.Size([3, 4, 5])
```

<br>

**n-D Tensor (Higher-order arrays):** Generalized tensors with n dimensions.

```python
tensor_nd = torch.rand(2, 3, 4, 5)  # Shape: (2, 3, 4, 5)
print(tensor_nd.shape)              # Output: torch.Size([2, 3, 4, 5])
```

<br>

#### Data Types:

> Tensors support a variety of data types:

| Data Type | Torch Type | Note |
| :--- | :--- | :--- |
|32-bit floating point|`torch.float32` or `torch.float`| |
|64-bit floating point|`torch.float64` or `torch.double`| |
|16-bit floating point |`torch.float16` or `torch.half`| Sometimes referred to as binary16: uses 1 sign, 5 exponent, and 10 significand bits. Useful when precision is important at the expense of range.|
|16-bit floating point |`torch.bfloat16`| Sometimes referred to as Brain Floating Point: uses 1 sign, 8 exponent, and 7 significand bits. Useful when range is important, since it has the same number of exponent bits as `float32` |
|32-bit complex|`torch.complex32` or `torch.chalf`| |
|64-bit complex|`torch.complex64` or `torch.cfloat`| |
|128-bit complex|`torch.complex128` or `torch.cdouble`| |
|8-bit integer (unsigned)|`torch.uint8`| |
|16-bit integer (unsigned)|`torch.uint16` (limited support) | Unsigned types asides from `uint8` are currently planned to only have limited support in eager mode (they primarily exist to assist usage with torch.compile); if you need eager support and the extra range is not needed, we recommend using their signed variants instead. See [https://github.com/pytorch/pytorch/issues/58734](https://github.com/pytorch/pytorch/issues/58734) for more details. |
|32-bit integer (unsigned)|`torch.uint32` (limited support) | Unsigned types asides from `uint8` are currently planned to only have limited support in eager mode (they primarily exist to assist usage with torch.compile); if you need eager support and the extra range is not needed, we recommend using their signed variants instead. See [https://github.com/pytorch/pytorch/issues/58734](https://github.com/pytorch/pytorch/issues/58734) for more details. |
|64-bit integer (unsigned)|`torch.uint64` (limited support) | Unsigned types asides from `uint8` are currently planned to only have limited support in eager mode (they primarily exist to assist usage with torch.compile); if you need eager support and the extra range is not needed, we recommend using their signed variants instead. See [https://github.com/pytorch/pytorch/issues/58734](https://github.com/pytorch/pytorch/issues/58734) for more details. |
|8-bit integer (signed)|`torch.int8`| | 
|16-bit integer (signed)|`torch.int16` or `torch.short`| |
|32-bit integer (signed)|`torch.int32` or `torch.int`| |
|64-bit integer (signed)|`torch.int64` or `torch.long`| |
|Boolean|`torch.bool`| |
|quantized 8-bit integer (unsigned)|`torch.quint8`| |
|quantized 8-bit integer (signed)|`torch.qint8`| |
|quantized 32-bit integer (signed)|`torch.qint32`| |
|quantized 4-bit integer (unsigned) |`torch.quint4x2`| quantized 4-bit integer is stored as a 8-bit signed integer. Currently it’s only supported in EmbeddingBag operator. |
|8-bit floating point, e4m3 |`torch.float8_e4m3fn` (limited support)| `torch.float8_e4m3fn` and `torch.float8_e5m2` implement the spec for 8-bit floating point types from [https://arxiv.org/abs/2209.05433](https://arxiv.org/abs/2209.05433). The op support is very limited. |
|8-bit floating point, e5m2 |`torch.float8_e5m2` (limited support)| `torch.float8_e4m3fn` and `torch.float8_e5m2` implement the spec for 8-bit floating point types from [https://arxiv.org/abs/2209.05433](https://arxiv.org/abs/2209.05433). The op support is very limited. |

<br>

#### Device Support:

> Tensors can exist on CPU or GPU.

<br>

---

<br>

## Import and Verify Torch

```python
import torch
print(torch.__version__)
```

<br>

## Creating Tensors in PyTorch

PyTorch provides multiple ways to create tensors. Below are key methods:

<br>

### torch.tensor()

Creates a tensor from data.

```python
x = torch.tensor([[1, 2], [3, 4]], dtype=torch.float32)
```

<br>

### Tensor Initialization

**Empty Tensor:** Uninitialized tensor.

```python
torch.empty(size=(2, 3))
```

**Zeros Tensor:** Filled with zeros.

```python
torch.zeros(size=(2, 3))
```

**Ones Tensor:** Filled with ones.

```python
torch.ones(size=(2, 3))
```
 
**Random Tensor:** Randomly initialized.
 
```python
torch.rand(size=(2, 3))
```

**Range Tensor:** Sequence of numbers.

```python
torch.arange(start=0, end=10, step=2)
```
 
<br>

### Special Tensors

**Identity Matrix:**
 
```python
torch.eye(3)
```

**Linspace/Logspace:**

```python
torch.linspace(0, 1, steps=5) # Linear space
torch.logspace(0, 2, steps=5) # Logarithmic space
```

<br>

---

<br>

## Tensor Attributes

Understanding tensor attributes is crucial:

```python
x = torch.tensor([[1, 2, 3], [4, 5, 6]], dtype=torch.float32)

# Attributes
x.dtype        # Data type (e.g., torch.float32)
x.shape        # Shape of the tensor (rows, columns)
x.size()       # Size (similar to shape)
x.ndimension() # Number of dimensions
x.device       # Device (e.g., CPU or GPU)
x.is_cuda      # True if tensor is on GPU
```

<br>

---

<br>

## Tensor Operations

PyTorch tensors support a rich set of operations, including:

### Element-wise Operations

```python
x + y  # Addition
x - y  # Subtraction
x * y  # Multiplication
x / y  # Division
```

### Reduction Operations

```python
x.sum()    # Sum of all elements
x.mean()   # Mean value
x.min()    # Minimum value
x.max()    # Maximum value
x.prod()   # Product of elements
```

### Matrix Operations

```python
torch.matmul(a, b)  # Matrix multiplication
torch.mm(a, b)      # Same as matmul
torch.einsum("ij,jk->ik", a, b)  # Einstein summation
```

### Broadcasting

PyTorch automatically broadcasts tensors with compatible shapes:

```python
a = torch.tensor([1, 2, 3])
b = torch.tensor([[1], [2], [3]])
a + b  # Broadcasting
```

### Indexing and Slicing

```python
x = torch.tensor([[1, 2, 3], [4, 5, 6]])
x[0, :]   # First row
x[:, 1]   # Second column
x[1, 1]   # Single element
```

<br>

---

<br>

## Tensor Manipulation

### Reshaping

```python
x = torch.arange(12)
x_reshaped = x.view(3, 4)  # Reshape into 3x4
```

### Stacking and Concatenation

```python
torch.cat((a, b), dim=0)   # Concatenate along dimension 0
torch.stack((a, b), dim=1) # Stack along new dimension
```

### Transpose and Permute

```python
x.t()               # Transpose for 2-D tensor
x.permute(1, 0, 2)  # Generalized permute
```

### Splitting

```python
torch.chunk(x, chunks=2, dim=0) # Split into chunks
torch.split(x, split_size_or_sections=2, dim=0) # Split by size
```

<br>

---

<br>

## Tensor Utilities

### Type Conversion

```python
x = x.float()       # Convert to float
x = x.int()         # Convert to int
```

### Moving Tensors Between Devices

```python
x = x.to('cuda')    # Move to GPU
x = x.to('cpu')     # Move to CPU
```

### Detaching Tensors

Detaching from the computation graph:

```python
x = x.detach()
```

<br>

---

<br>

## Autograd and Tensors

PyTorch integrates automatic differentiation with tensors:

```python
x = torch.tensor([1.0, 2.0, 3.0], requires_grad=True)
y = x ** 2
y.backward(torch.tensor([1.0, 1.0, 1.0]))  # Compute gradients
x.grad  # Access gradients
```

<br>

---

<br>