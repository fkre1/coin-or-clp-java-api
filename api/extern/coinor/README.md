# building on mac:
some dependencies are needed:

* bash (coinbrew)
* wget (coinbrew)
* gcc (includes gfortran)

these can be obtained with `homebrew`:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

```bash
brew install bash wget gcc
```

# download, build and install CLP

to download and build CLP, first download `coinbrew`:

```bash
wget https://raw.githubusercontent.com/coin-or/coinbrew/master/coinbrew
chmod +x coinbrew
```

Then build and install CLP and CBC

```bash
export ADD_FFLAGS=-fallow-argument-mismatch # if using gfortran10 (from gcc10)
./coinbrew build install Cbc@2.10.5 Clp@1.17.5 --parallel-jobs $(nproc) --tests none --prefix $os$arch/dist
```
