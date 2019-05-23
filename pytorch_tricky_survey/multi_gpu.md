# Multi-GPU

## Data parallel

```Python
device = torch.device("cuda:0") # This is the main device, it MUST be zero, and the sum data pool will be in this device.
model = nn.DataParallel(model)
model.to(device) 
mytensor = my_tensor.to(device) # 这三行指令顺序不是问题，主要是dataparallel要包住model
```


## Distributed
