# Notes about Building on Windows

Please follow the instructions from [here](https://gitlab.com/tspiteri/gmp-mpfr-sys#building-on-windows) first.

After setting up MSYS2 MinGW64 envorinment, open the MinGW64 terminal and run the following commands

```bash
# Clang is necessary for building the project. Gcc does not work.
pacman -S mingw-w64-x86_64-clang

# Need to build with GNU toolchain. Default MSVC will fail.
rustup install stable-x86_64-pc-windows-gnu
rustup default stable-x86_64-pc-windows-gnu

# Build with Clang
# This may take a while. On my machine, it took 32 minutes.
CC=clang cargo build -r
```

To build python bindings, install [maturin](https://www.maturin.rs/installation.html) and activate conda environment.

```bash
# Activate conda env with any version of python pre-installed.
conda activate py12

# Build and install with maturin
CC=clang maturin develop --features py

# This should now work
python -c "import calc_pi; print(calc_pi.chudnovsky(1000))"
```