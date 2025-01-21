## Imports

```python
import torch
```

<br>

---

<br>

## CUDA Status Check

```python
print(torch.cuda.is_available())
```

or

```python
if torch.cuda.is_available():
    print("CUDA is available")
else:
    print("CUDA is not available")
```

<br>

---

<br>

## List All Available GPU Device Info

```python
# Get the number of GPUs
gpu_count = torch.cuda.device_count()

print(f"Available Devices: ({gpu_count})")
print("======================")
for i in range(0, cuda_count):
    print(f"Device: {i}: {torch.cuda.get_device_name(i)}")
```

<br>

---

<br>

## Get and Change GPU Device

<br>

#### Get Current GPU Device

```python
print(torch.cuda.current_device())
```

#### Change Current GPU Device

```python
torch.cuda.set_device(0) # For device 0
```