# GAPartNet_env
GAPartNet conda environment

## An worked environment:

build env for RL-Pose

### Step 1: CUDA and basic conda environment

python == 3.8

cuda, nvcc >= 11.3

My device is 4090, so cuda11.7 does not work for me. I use cuda11.8.
torch >= 1.11: 
e.g. pip install torch==2.0.1+cu118 torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu117

### Step 2: cmake and open3d
cmake >= 3.20: following the instruction (here)[https://cmake.org/install/]

open3d with pytorch extension (need to build from source)
install repo
```
git clone https://github.com/isl-org/Open3D
```
install dependences
```
util/install_deps_ubuntu.sh
```
prepare required files and build:
```
mkdir open3d_install
mkdir build
cd build
git clone https://github.com/isl-org/Open3D-ML.git
```

cmake command:
```
cmake \
-DPython3_ROOT="/home/yandan/anaconda3/envs/gapartnet/bin/" \
-DWITH_OPENMP=ON \
-DWITH_SIMD=ON \
-DBUILD_PYTORCH_OPS=ON \
-DBUILD_CUDA_MODULE=ON \
-DBUILD_COMMON_CUDA_ARCHS=ON \
-DGLIBCXX_USE_CXX11_ABI=OFF \
-DBUILD_JUPYTER_EXTENSION=ON \
-DCMAKE_CUDA_COMPILER=$(which nvcc) \
-DCMAKE_INSTALL_PREFIX="/home/yandan/workspace/Open3D/open3d_install" \
-DBUNDLE_OPEN3D_ML=ON \
-DOPEN3D_ML_ROOT=Open3D-ML \
..                       
```

```
make -j$(nproc)
```

```
make install
```

```
# Activate the virtualenv first
# Install pip package in the current python environment
make install-pip-package
```

If you get ModuleNotFoundError like: No module named ‘yapf’
```
pip install yapf
```

Test Open3D installation
```
python -c "import open3d"
```

#### pointnet_ops

https://github.com/erikwijmans/Pointnet2_PyTorch/tree/master/pointnet2_ops_lib

clone repo
```
git clone git@github.com:erikwijmans/Pointnet2_PyTorch.git
```

install this repo
```
cd pointnet2_ops_lib
python setup.py install
```
#### epic_ops

https://github.com/geng-haoran/epic_ops

clone repo
```
git clone git@github.com:geng-haoran/epic_ops.git
```

install this repo
```
cd epic_ops
python setup.py develop
```

#### spconv
```
spconv: pip install spconv-cuxxx (https://github.com/traveller59/spconv)
```

#### pip
```
pip install wandb tensorboard ipdb gym tqdm rich opencv_python pytorch3d pyparsing pytorch_lightning addict yapf h5py sorcery  pynvml torchdata==0.5.1 einops
```
