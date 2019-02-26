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
model.load_state_dict(torch.load(PATH))
model.eval()
```
