# lkpatcher

![License](https://img.shields.io/github/license/R0rt1z2/lkpatcher)
![GitHub Issues](https://img.shields.io/github/issues-raw/R0rt1z2/lkpatcher?color=red)

`lkpatcher` serves as both a streamlined Python tool and module designed for the alteration and patching of LK (_Little Kernel_) images. The utility offers flexibility along with an intuitive API for ease of use. To use the library, **Python 3.11** or higher is required. An alternative method of access is available via the [new web version](https://lkpatcher.r0rt1z2.com/) of the tool, which is not open-source but offers the same functionality and has a GUI.

## Installation

```bash
sudo apt install python3-pip # If you don't have pip installed.
pip3 install --upgrade pip   # If pip hasn't been updated yet.
pip3 install --upgrade git+https://github.com/R0rt1z2/lkpatcher
```
> <small>[!NOTE]
> _Windows users should omit the first two command(s) and install python manually from [here](https://www.python.org/downloads/)._</small>

## Instructions
```bash
python3 -m lkpatcher [-h] [-o OUTPUT] [-j JSON] [-d DUMP_PARTITION] bootloader_image
```
> <small>[!NOTE]
> _Arguments between `<>` are required, while arguments between `[]` are optional.</small>_

You can also use the module in your own projects:
```python
# Import the patcher class from the module. This should be enough to
# get you started, as it provides an API to apply patches to images.
from lkpatcher.patcher import LkPatcher

# Create the patcher object. When initializing the object, you MUST
# specify the path to the image you want to patch, and, optionally,
# the path to the JSON file containing the patches. If you don't
# specify a JSON file, the default one will be used.
patcher = LkPatcher(image='lk.img', patches='patches.json')

# Use the patcher object to apply patches to the image. The output
# parameter is optional, and, if not specified, the patched image
# will be saved as 'lk-patched.img'.
image = patcher.patch(output='lk-patched.bin')
```

## Important notes
- To successfully boot patched images, it's a prerequisite to unlock **seccfg**, which can be accomplished using [mtkclient](https://github.com/bkerler/mtkclient).
- Prior to the patching process, it's recommended to create backups of your existing images. The responsibility for any damage inflicted upon your device is solely your own. 
- If your device doesn't boot (even) after unlocking it with mtkclient, it most likely uses SBC, and, therefore, is not supported by this tool.
- If you're running into issues and need to debug, dump the `expdb` partition using mtkclient and open a new issue here with the dump attached.
- To request device-specific patches, please open a new issue and attach both your LK image and the `image.txt` file generated by the tool.
- If you're interested in understanding how these patches function and want to give creating your own a try, take a look at the [guide](https://blog.r0rt1z2.com/patch-mediatek-bootloader-images-lk.html) [(alternatively, check this old PDF)](https://github.com/R0rt1z2/lkpatcher/blob/ab9f8bb5b17aebf35bcfdf83db084a15cc50a9cf/guide.pdf).
- The `patches.json` file has sample patches applicable to various devices. These samples serve as reference material for the creation of your own device-specific patches.

## License
This project is licensed under the GPL-3.0 License - see the [LICENSE](https://github.com/R0rt1z2/lkpatcher/tree/master/LICENSE) file for details.
