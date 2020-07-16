building on mac:
some dependencies are needed:
- bash (coinbrew)
- wget (coinbrew)
- gcc (includes gfortran)

these can be obtained with `homebrew`:
````bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

````bash
brew install bash wget gcc
```

to download and build CLP, first download `coinbrew`:
````bash
wget https://raw.githubusercontent.com/coin-or/coinbrew/master/coinbrew
chmod +x coinbrew
```

download Clp:
````bash
./coinbrew fetch Clp:releases/1.17.5
```

optionally edit the sources to remove print statements:
```bash
emacs Clp/Clp/src/OsiClp/OsiClpSolverInterface.cpp
# remove "std::cout" lines
```

Then build and install
````bash
export ADD_FFLAGS=-fallow-argument-mismatch # if using gfortran10 (from gcc10)
./coinbrew build install Clp:releases/1.17.5
```

to build for multiple platforms (required for building the CLPModelWrapper with cmake), create subfolders corresponding to the OS and architecture (win32/win64/macos/linux32/linux64),
copy/link the coinbrew script to there and execute as described above
