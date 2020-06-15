# torch-hub-models
https://pytorch.org/docs/stable/hub.html

One layer CNN

entrypoints = torch.hub.list('andreipit/torch-hub-models:master', force_reload=True) # refresh downloaded (:v1/master)
torch.hub.help('andreipit/torch-hub-models', 'one_layer_cnn', force_reload=True)

model = torch.hub.load('andreipit/torch-hub-models:master', 'shown_in_hub_list', pretrained=True, force_reload=True, testkwarg=78)
    pretrained = True
    testkwarg = 78
    v1
model
    dict_items([('pretrained', True), ('testkwarg', 78)])    
list(model)[1][1] #78    

torch.hub.download_url_to_file('https://github.com/andreipit/torch-hub-models/releases/download/v1/one_layer_cnn_weights.pth', 'temporary_file', hash_prefix=None, progress=True) # creates output/kaggle/working/temporary_file

model = torch.hub.load('andreipit/torch-hub-models:master', 'one_layer_cnn', pretrained=True, force_reload=True, testkwarg=78)
dir(model) # => forward


