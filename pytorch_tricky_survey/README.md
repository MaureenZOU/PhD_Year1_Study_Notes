# Pytorch Tricky Survey

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
