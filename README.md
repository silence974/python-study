# Optimo & Pulchrum
# My Study for Scikit-build with pybind11 and standard Python Project

# how to build for dev

pip install . --no-build-isolation

## requirement

- cmake>=4.0.0
- pybind11>=3.0.0

# how to build with tmp

pip install ./

# how to build for publish

python -m cibuildwheel --platform linux

## requirement

- cibuildwheel>=3.3.0
