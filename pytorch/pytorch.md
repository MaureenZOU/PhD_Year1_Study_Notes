# Pytorch misc

## (N,C,H,W) tensor to np image

```Python
import numpy as np
import cv2
mean=[0.485, 0.456, 0.406]
std=[0.229, 0.224, 0.225]
image = (((images[0][0].cpu().numpy() * np.array(std).reshape(3,1,1)) + np.array(mean).reshape(3,1,1))*255).transpose(1,2,0)[:,:,::-1]


```

## Inheritance in Python
```Python
class Animal(object):
    def __init__(self, age):
        self.age = age
        return self

    def forward(age):
        self.age += age
    
class Cat(Animal):
    def __init__(self, *argv):
        self.obj1 = super(Cat, self).__init__(argv)
        self.obj2 = super(Cat, self).__init__(argv)
        print(self.obj1)

cat = Cat(3)
print(cat.obj1.age)
print(cat.obj2.age)
```

## torch.nn.Module.training and torch.nn.Module.train(mode)
These are build in function of pytorch. For change the mode of training. eval() will call model.train() to set the training mode.

```Python
def eval(self):
        r"""Sets the module in evaluation mode.

        This has any effect only on certain modules. See documentations of
        particular modules for details of their behaviors in training/evaluation
        mode, if they are affected, e.g. :class:`Dropout`, :class:`BatchNorm`,
        etc.
        """
        return self.train(False)
```


```Python
def train(self, mode=True):
        r"""Sets the module in training mode.

        This has any effect only on certain modules. See documentations of
        particular modules for details of their behaviors in training/evaluation
        mode, if they are affected, e.g. :class:`Dropout`, :class:`BatchNorm`,
        etc.

        Returns:
            Module: self
        """
        self.training = mode
        for module in self.children():
            module.train(mode)
        return self
```

## torch.nn.Module.named_parameters()

```Python
# Returns an iterator over module parameters(could be some class inherit nn.Module), yielding both the name of the parameter as well as the parameter itself.

for name, param in self.named_parameters(): 
    if "bias" in name:
        nn.init.constant_(param, 0)
    elif "weight" in name:
        nn.init.kaiming_normal_(param, mode="fan_out", nonlinearity="relu")
                
```

## torch.max
for more than three dimension input, it will first return the max value and then return the coordinates. 

## Version Control
For each project if you work on a specific pytorch version, then stick on that. Otherwise it will create some problem.

## MSE Loss and BCE Loss
BCE loss could only require gradient for the input, but MSE could require both.

At the same time, MSE loss automatically average the loss across different dimensions unless you unflag it, please please bare in mind!!!!

## Autogradient [\[link\]](https://pytorch.org/tutorials/beginner/blitz/autograd_tutorial.html)
![#f03c15](https://placehold.it/15/f03c15/000000?text=+) This bad thing fool me for two month until I recognize it is the bug of autogradient.

* key question before reading this section. (1) Network Autogradient (2) Input tensor Autogradient (3) How does autogradient link with optimizer.



## Saving and loading Models [\[link\]](https://pytorch.org/tutorials/beginner/saving_loading_models.html)
### Main related function

```python
torch.save
torch.load
torch.nn.Module.load_state_dict
```

#### state_dict
All the model is inherited from ```torch.nn.Module```, and the model weights could be accessed through ```model.parameters()```. A state_dict is simply a Python dictionary object that maps each layer to its parameter tensor. Optimizer objects ```torch.optim``` also have a state_dict, which contains information about the optimizer’s state, as well as the hyperparameters used.

![#f03c15](https://placehold.it/15/f03c15/000000?text=+) `Why no bias sometimes.`

#### Saving and Loading Model for Inference
```python
#save
torch.save(model.state_dict(), PATH)

#load
model = TheModelClass(*args, **kwargs)

device = torch.device("cuda")
model.load_state_dict(torch.load(PATH))
model.to(device)
model.eval() #Remember that you must call model.eval() to set dropout and batch normalization layers to evaluation mode before running inference. Failing to do this will yield inconsistent inference results.
```
#### Saving torch.nn.DataParallel Models

```python
#save
torch.save(model.module.state_dict(), PATH)

#Load to whatever device you want
```
