# torch-hub-models
https://pytorch.org/docs/stable/hub.html

One layer CNN
# Hello World!
torch.hub.set_dir('/kaggle/working/mytorchcache')
entrypoints = torch.hub.list('andreipit/torch-hub-models:master', force_reload=True) # (:v1/master)
torch.hub.help('andreipit/torch-hub-models', 'one_layer_cnn', force_reload=True)

input_size_train = iter(trainloader).next()['image'].shape[1:]

### way 1
### net = torch.hub.load('andreipit/torch-hub-models:master', 'one_layer_cnn', input_size=input_size_train, pretrained=True, force_reload=True, testkwarg=78)

### # way 2
### net = torch.hub.load('andreipit/torch-hub-models:master', 'one_layer_cnn', input_size=input_size_train, pretrained=False, force_reload=True, testkwarg=78)
### state_dict = torch.hub.load_state_dict_from_url('https://github.com/andreipit/torch-hub-models/releases/download/v2/one_layer_cnn_weights.pth')
### net.load_state_dict(state_dict)

### way 3
net = torch.hub.load('andreipit/torch-hub-models:master', 'one_layer_cnn', input_size=input_size_train, pretrained=False, force_reload=True, testkwarg=78)
torch.hub.download_url_to_file('https://github.com/andreipit/torch-hub-models/releases/download/v2/one_layer_cnn_weights.pth', 'temporary_file', hash_prefix=None, progress=True)
state_dict = torch.load('/kaggle/working/temporary_file')
net.load_state_dict(state_dict)

dir(net) # => forward
help(net.forward)


# 1) get info
entrypoints = torch.hub.list('andreipit/torch-hub-models:master', force_reload=True) # refresh downloaded (:v1/master)
torch.hub.help('andreipit/torch-hub-models', 'one_layer_cnn', force_reload=True)

# 2) load test function
model = torch.hub.load('andreipit/torch-hub-models:master', 'shown_in_hub_list', pretrained=True, force_reload=True, testkwarg=78)
    pretrained = True
    testkwarg = 78
    v1
model
    dict_items([('pretrained', True), ('testkwarg', 78)])    
list(model)[1][1] #78    

# 3) just download file
torch.hub.download_url_to_file('https://github.com/andreipit/torch-hub-models/releases/download/v1/one_layer_cnn_weights.pth', 'temporary_file', hash_prefix=None, progress=True) # creates output/kaggle/working/temporary_file

# 4) load model with weights and init with input_size
model = torch.hub.load('andreipit/torch-hub-models:master', 'one_layer_cnn', input_size=iter(trainloader).next()['image'].shape[1:], pretrained=True, force_reload=True, testkwarg=78)
dir(model) # => forward
help(model.forward)

# 5) load weights from url
state_dict = torch.hub.load_state_dict_from_url('https://github.com/andreipit/torch-hub-models/releases/download/v1/one_layer_cnn_weights.pth')

# 6) change default download folder
default cache folder:
x = os.listdir('/root/.cache/torch/hub/andreipit_torch-hub-models_master')
x.sort()
x # ['LICENSE', 'README.md', '__pycache__', 'hubconf.py', 'one_layer_cnn_weights.pth']
new cache folder:
torch.hub.set_dir('/kaggle/working/mytorchcache')
entrypoints = torch.hub.list('andreipit/torch-hub-models:master', force_reload=True) # refresh downloaded (:v1/master)

# 7) caching
by default - no files downloaded, if already exist
use hub.load(..., force_reload=True) to stay up-to-date

# 8) limitations:
user CANNOT load two different branches of the same repo in the same python process
