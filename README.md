# env-ISCE2-MintPy-MiaplPy

## First, install the miniforge3 （https://github.com/conda-forge/miniforge）

## 1. MintPy & MiaplPy （Modified from https://github.com/insarlab/MiaplPy/blob/main/docs/installation.md）

### 1.1 Download the MiaplPy
```
cd ~/tools
git clone https://github.com/insarlab/MiaplPy.git
cd ~/tools/MiaplPy
```

### 1.2 Install dependencies
copy conda-env-rev.yml to MiaplPy
```
mamba env create --file mamba-env-rev.yml
```

### 1.3 Install MiaplPy via pip
```
mamba activate miaplpy-env
python -m pip install .
```

### 1.4. Install [SNAPHU](https://web.stanford.edu/group/radar/softwareandlinks/sw/snaphu/)
```
export TOOLS_DIR=~/tools
cd ~/tools;
wget --no-check-certificate  https://web.stanford.edu/group/radar/softwareandlinks/sw/snaphu/snaphu-v2.0.5.tar.gz
tar -xvf snaphu-v2.0.5.tar.gz
mv snaphu-v2.0.5 snaphu;
rm snaphu-v2.0.5.tar.gz;
sed -i 's/\/usr\/local/$(TOOLS_DIR)\/snaphu/g' snaphu/src/Makefile
cd snaphu/src; make
export PATH=${TOOLS_DIR}/snaphu/bin:${PATH}
```

## 2. ISCE2 (Modified from https://github.com/lijun99/isce2-install?tab=readme-ov-file#macosx-with-anaconda3-and-homebrew-apple-silicon)

### 2.1 Install brew (https://github.com/Homebrew/brew/releases/)
```
brew install gfortran@14
/opt/homebrew/bin/gfortran --version # check
```
gfortran@15 will report error in compilering the isce2

### 2.2 Install dependencies
```
mamba install git cmake pytest pybind11 opencv
```

### 2.3 Compile ISCE2
Make a link to make the installation path easier (-DPYTHON_MODULE_DIR not longer need)
```
ln -sf `python3 -c 'import site; print(site.getsitepackages()[0])'` $CONDA_PREFIX/packages
```
Download ISCE2 from github
```
git clone https://github.com/isce-framework/isce2.git
```
Compile ISCE2 with cmake
```
cd isce2
mkdir build && cd build
cmake .. -DCMAKE_INSTALL_PREFIX=$CONDA_PREFIX \
         -DCMAKE_PREFIX_PATH=${CONDA_PREFIX} \
         -DCMAKE_C_COMPILER="/opt/homebrew/bin/gcc-14" \
         -DCMAKE_CXX_COMPILER="/opt/homebrew/bin/g++-14" \
         -DCMAKE_Fortran_COMPILER="/opt/homebrew/bin/gfortran-14"
make -j # to use multiple threads
make install       
```
Config and run isce2
```
export ISCE_HOME="$CONDA_PREFIX/packages/isce"
export PATH="$ISCE_HOME/applications:$PATH"
```
check the install
```
python3 -c "import isce"
```

## 3. Accelerating the computing at the setp 2 of MiaplPy called phasing linking.
```
mamba install "libblas=*=*accelerate" "liblapack=*=*accelerate"
```
Notice: If do not install the accelerated edition above the phasing linking will be very very slow, and it will be slower about 10 times than the accelerated edtion. 


