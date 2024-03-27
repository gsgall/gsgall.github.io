# Boiler Plate Project


## Project Structure

For the work that we do even simple projects may contain a large amount of code. This can quickly become unruly if you include all of your code in a single file and makes maintance more difficult for future programmers. An example of a code that is very difficult to read/maintian is [eduPIC](https://github.com/donkozoltan/eduPIC). While eduPIC it is a great educational tool it contains all of its functionality in one file. This is good for a basic educational tool but a production quality code should be split into multiple files. Try to avoid really large files if you can but some files do just need to be big and that's okay too.

## Body-Header Split

To improve the readability of your code you should have a header file and a body file for each file. The header contains information about what functions/classes exist in your project and provides a simple preview of what is contained in the body file without the uneeded information of the actual implementation. This is useful if you're working on a project and you just need to know where a specific function or class exists and the variables/functions that exist in the file.

```
├── README.md
├── Makefile
├── main
├── src
│ ├── file1.C
│ ├── file2.C
│ └── file3.C
├── include
│ └── project-name
│   ├── project-name.h
│   ├── file1.h
│   ├── file2.h
│   └── file3.h
├── test
│ ├── Makefile
│ ├── run_tests
│ └── tests
│   ├── test1.C
│   └── test2.C
├── doc
│ ├── doc1.md
│ ├── doc2.md
└── tutorial
  ├── tutorial.md
  └── example-files
    ├── ex1.C
    └── ex2.C
```

## Using the project

In the directory `code-standards/boiler-plate-project` is a C++ project that has all of the basic requirements for a project. All of the directories, and Makefile are setup, tested and ready to use for your next production quality project. To get started with this project you should first make a new conda environment for the project see [using_conda.md] for instructions on how to do this. Once you have conda installed you should also install [GoogleTest](https://google.github.io/googletest/) for creating an automated testing suite.

```bash
conda install -c conda-forge gtest
```

Now that that is in place you can get started by copying this boiler plate project to your new project location.

```bash
  cp -r ~/projects/code-standards/boiler-plate-project ~/projects/your-project-name
```

## Building and running as an executeable

```bash
  make
  ./main
```

You should see the following on the terminal

```
  Success!
```

When you need to recompile the project you may also need to remove the executeable and the build directory. To do so you can simply run

```bash
  make clean
```


## Building and running tests

All projects that are going to be made public and distributed to the broaded plasam physics community should have some level of automated testing. The first that you need to do this is that you should have some level of testing to ensure your code functions as it should. The second is that when someone else installs your project have an automated test suite for them to run helps ensure that they have installed the project correctly and it functions as expected. To run the test for this project please use the following

```bash
  cd ~/projects/your-project/test
  make
  ./run_tests
```

You should see the following as output if the tests were successful

```
[==========] Running 1 test from 1 test suite.
[----------] Global test environment set-up.
[----------] 1 test from Test1
[ RUN      ] Test1.Equal
[       OK ] Test1.Equal (0 ms)
[----------] 1 test from Test1 (0 ms total)

[----------] Global test environment tear-down
[==========] 1 test from 1 test suite ran. (0 ms total)
[  PASSED  ] 1 test.
```

## Building as a Dynamically Linkable Library

While you may just want to build your project in your local directories and as a single executable there are other options for building a project as well. You may for example want to build your poject as a dynamically linkable library. If you are interested in doing so you can do the following

```bash
  mv Makefile Makefile-local
  mv Makefile-as-dll Makefile
  make
```

This will compile your project as a dynamically linkable libary.

!alert note title=Dynamically Linkable Library Usage
The way you compile as a dynamically linkable library does depend on the platform you are using. Currently the Makefile is setup for use on a macOS platform. To change this you will need to modify this line of the Makefile `LIBRARY_NAME = lib$(PROJECT_NAME).dylib`. The part you need to change is the extension. See the table below for guidance.


| Platform | Extension |
| - | - |
| macOS | .dylib |
| Linux | .so |
| Windows | .dll |


This will build the dynamically linkable library object in your local directory. If you would like to build this and then install it in your conda environment simply use

```bash
  make install
```

This will copy your header files and move the dynamically linkable library object to the proper place to be used as a conda package.

## Building with a Dynamically Linkable Library

If you would like to now use your installed project as a dynamically linkable library in another project you can use the following


```bash
  mv Makefile Makefile-as-dll
  mv Makefile-with-dll Makfile
  make
```


!alert warning title=Configuring your conda environment
Your computer will likely not automatically be configured to search in your conda environment for dynamically linkable libraries. In order to enable this you will need to do to the following.

## macOS

```bash
  cd $CONDA_PREFIX
  mkdir -p ./etc/conda/activate.d
  mkdir -p ./etc/conda/deactivate.d
  touch ./etc/conda/activate.d/env_vars.sh
  echo 'export DYLD_LIBRARY_PATH="$CONDA_PREFIX/lib:$DYLD_LIBRARY_PATH"' > ./etc/conda/activate.d/env_vars.sh
  touch ./etc/conda/deactivate.d/env_vars.sh
  echo 'unset DYLD_LIBRARY_PATH' > ./etc/conda/deactivate.d/env_vars.sh
```

## Linux

```bash
  cd $CONDA_PREFIX
  mkdir -p ./etc/conda/activate.d
  mkdir -p ./etc/conda/deactivate.d
  touch ./etc/conda/activate.d/env_vars.sh
  echo 'export LD_LIBRARY_PATH="$CONDA_PREFIX/lib:$LD_LIBRARY_PATH"' > ./etc/conda/activate.d/env_vars.sh
  touch ./etc/conda/deactivate.d/env_vars.sh
  echo 'unset LD_LIBRARY_PATH' > ./etc/conda/deactivate.d/env_vars.sh
```

## Windows

A similar procedure may be needed for windows users. However, at tht time of writing I have not used a windows system for many years and so a little external research may be required.

## Building Test Options

A Makefile to build the test suite with your project as an installed conda package also exists. Assuming you got the main executable to run while building your project as a dynamically linkable library you can simply do the following.

```bash
  cd ~/projects/your-project/test
  mv Makefile Makefile-local
  mv Makefile Makefile-with-dll
  make
  ./run_tests
```

If successful you should again see the following output


```
[==========] Running 1 test from 1 test suite.
[----------] Global test environment set-up.
[----------] 1 test from Test1
[ RUN      ] Test1.Equal
[       OK ] Test1.Equal (0 ms)
[----------] 1 test from Test1 (0 ms total)

[----------] Global test environment tear-down
[==========] 1 test from 1 test suite ran. (0 ms total)
[  PASSED  ] 1 test.
```

## Code coverage

In the the Makefile which builds the test suite directly as an executable you will also find that it has been set up for use of [lcov](https://anaconda.org/conda-forge/lcov). lcov is a code coverage testing tool. This allows us to see how much of our code has actually been executed when we run our test suites. In the perfect world this should be 100% but that is often un reasonable and uneeded for most use cases. However, before any code is released there should be at least a minimum of 90% code coverage. Luckily we have taken care of the complex part of writing the Makefile to enable this feature. So lets go over the expected behaviour. When you run the `./run_tests` executable you should still see the normal output.

```
[==========] Running 1 test from 1 test suite.
[----------] Global test environment set-up.
[----------] 1 test from Test1
[ RUN      ] Test1.Equal
[       OK ] Test1.Equal (0 ms)
[----------] 1 test from Test1 (0 ms total)

[----------] Global test environment tear-down
[==========] 1 test from 1 test suite ran. (0 ms total)
[  PASSED  ] 1 test.
```

However, now we can take a closer look at the project if we run the command

```bash
  make coverage
```

Then you should the following html page appear in your browser.

!media media/coverage_example.png style=width:100%;display:block;margin-top:3em;margin-left:auto;margin-right:auto;

There are only two functions in this project 1 is tested and the other is not. If you click on the `src` link you will be able to see which function in which file is untested.
