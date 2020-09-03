---
title: ImageFolder Function
date: 2020-08-18 10:15:55
categories: Pytorch function
tags: Pytorch
---

## ImageFolder

### 数据集结构：

> root
>
> > dog
> >
> > > 001.png
> > >
> > > 002.png
> > >
> > > ...
> > >
>
> > cat
> > > 001.png
> > > 
> > > 002.png
> > > 
> > > ...

### 函数调用

```python
import torchvision.datasets as dset
# ImageFolder用于数据的加载，其调用方式为:
dset.ImageFolder(root, transform=None, target_transform=None, loader=<function default_loader>, is_valid_file=None)
'''
Parameters:
	+root(srting)-图片的根目录
	+transform(callable, optional)-将输入的PIL图像进行转换
	+target_transform(callable, optional)-将target(label)进行转换
	+loader(callable, optional)-对于给定的root路径，决定如何读取image。没有设定则为defaule loader，根据设置的_image_backend(默认'PIL')判断
	+is_valid_file-用于检查文件
'''
```

### transform示例

```python
# transform callable variable example
transform = transforms.Compose([
            transforms.RandomHorizontalFlip(), # 随机对图片继续水平翻转
            transforms.Resize((self.img_size + 30, self.img_size + 30)),
            transforms.RandomCrop(self.img_size), # 根据给定的size对Image进行随机裁剪
            transforms.ToTensor(),
            transforms.Normalize(mean=(0.5, 0.5, 0.5), std=(0.5, 0.5, 0.5))
        ])
```

更多[torchvision.transform](https://pytorch.org/docs/stable/torchvision/transforms.html?highlight=transform)操作。

### Default loader

```python
# torchvision/datasets/folder.py
def pil_loader(path):
    # open path as file to avoid ResourceWarning (https://github.com/python-pillow/Pillow/issues/835)
    with open(path, 'rb') as f:
        img = Image.open(f)
        return img.convert('RGB')

def accimage_loader(path):
    import accimage
    try:
        return accimage.Image(path)
    except IOError:
        # Potentially a decoding problem, fall back to PIL.Image
        return pil_loader(path)
    
def default_loader(path):
    from torchvision import get_image_backend
    if get_image_backend() == 'accimage':
        return accimage_loader(path)
    else:
        return pil_loader(path)
```

`get_image_backend`函数

```python
# torchvision/__init__.py
# 通过torchvision.set_image_backend设置image backend，默认设置为'PIL'
from torchvision import models
from torchvision import datasets
from torchvision import ops
from torchvision import transforms
from torchvision import utils
from torchvision import io

try:
    from .version import __version__  # noqa: F401
except ImportError:
    pass

_image_backend = 'PIL'

def set_image_backend(backend):
    """
    Specifies the package used to load images.

    Args:
        backend (string): Name of the image backend. one of {'PIL', 'accimage'}.
            The :mod:`accimage` package uses the Intel IPP library. It is
            generally faster than PIL, but does not support as many operations.
    """
    global _image_backend
    if backend not in ['PIL', 'accimage']:
        raise ValueError("Invalid backend '{}'. Options are 'PIL' and 'accimage'"
                         .format(backend))
    _image_backend = backend

def get_image_backend():
    """
    Gets the name of the package used to load images
    """
    return _image_backend
```

