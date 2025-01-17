## Setup

### Third party dependencies

Install Python's build dependencies using `pip3`:

```
$ pip3 install -r requirements.txt
```

It is recommended to do so in a separate `venv` environment. One time
initialization:

```
$ python3 -m venv venv
```

Then activate the environment by sourcing its `bin/activate` file:

```
$ source venv/bin/activate
```

--------------------------------------------------------------------------------

Download plugin's third party repositories:

```
$ git submodule update --init
```

### Build

Build the plugin using `cmake`:

```
$ mkdir build
$ cd build
$ cmake ..
$ make -j
```

The build process accepts the following variables, set using `cmake -D` command
line argument:

*   **BN_INSTALL_DIR**: Binary Ninja installation directory. This parameter is
    required in order to find BN's core library. If not specified, cmakes tries
    to find BN at its default install location.

*   **HEXAGON_SDK_TOOLS_DIR**: points to Qualcomm's
    [Hexagon SDK](https://developer.qualcomm.com/software/hexagon-dsp-sdk/tools).
    The SDK is optional, and only used to build the test binaries.

To build using `clang` override CC environment variable and include
`clang_overrides.cmake` as follows:

```
$ CC="$(which clang)" CXX="$(which clang++)" cmake .. \
  -DCMAKE_USER_MAKE_RULES_OVERRIDE="${PWD}/../cmake/clang_overrides.cmake"
```

--------------------------------------------------------------------------------

`make check` runs all unit tests. Note, a BN professional license is required in
order to run the headless e2e tests.

### Binary Ninja plugin

Add a symlink to the plugin binary:

```
$ ln -s ${PWD}/build/plugin/libarch_hexagon.so ${HOME}/.binaryninja/plugins/libarch_hexagon.so
```
