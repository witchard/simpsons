# Install torch with OpenCL support

```bash
git clone --recursive https://github.com/hughperkins/distro -b distro-cl ~/torch-cl
cd ~/torch-cl
brew update
brew upgrade
brew install git readline cmake wget qt libjpeg imagemagick zeromq graphicsmagick openssl
brew cask install xquartz
brew install gnuplot --with-wxmac --with-cairo --with-pdflib-lite --with-x11 --without-lua
./install.sh
source ~/torch-cl/install/bin/torch-activate
luajit -l cutorch -e 'cutorch.test()'
```

# Install deps

```bash
source ~/torch-cl/install/bin/torch-activate
luarocks install lua-cjson
brew install homebrew/science/hdf5
cd ~/torch-cl/pkg
git clone https://github.com/deepmind/torch-hdf5
cd torch-hdf5
luarocks make hdf5-0-0.rockspec
```

Note, needed to hack the following to get torch-hdf5 working:

* Edit `~/torch-cl/install/share/lua/5.1/hdf5/config.lua` to set the include path as `/usr/local/include`
* Edit `vim ~/torch-cl/install/share/lua/5.1/hdf5/ffi.lua` to read `local headerPath = path.join(includePath, "hdf5hack.h")`
* Make `/usr/local/include/hdf5hack.h` say the following:

```c
#define _close 
#define _read 
#define _seek 
#define _write 
#include "hdf5.h"
```

# Install torch-rnn

```bash
cd WHEREVER
git clone https://github.com/jcjohnson/torch-rnn.git
cd torch-rnn
virtualenv .env
source .env/bin/activate
pip install -r requirements.txt
```

# Run

```bash
python scripts/preprocess.py --input_txt simpson_data.txt --output_h5 simpson_data.h5 --output_json simpson_data.json
source ~/torch-cl/install/bin/torch-activate
th train.lua -input_h5 simpson_data.h5 -input_json simpson_data.json
```
