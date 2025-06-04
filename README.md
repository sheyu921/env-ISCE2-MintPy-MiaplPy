# env-ISCE2-MintPy-MiaplPy

## First, install the miniforge3

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
mamba env create --file conda-env-rev.yml
```

### 1.3 Install MiaplPy via pip
```
conda activate miaplpy-env
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
mamba install git cmake pytest pybind11 opencv



