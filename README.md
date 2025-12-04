# SEP25

COMP SCI 3006 - Software Engineering Project

The MASS project involved the development of a project which outlines the ability to develop software which can accurately predict and reconstruct a state-space based on limited stochastic data. 

Project Description video: https://youtu.be/rnyycKZLooc

Project Process Description: https://youtu.be/17c6qT_2zLE

## Building the Project

This project uses CMake as its build system. The project structure includes:

- `/src` - Source code files
- `/test` - Unit tests using Google Test
- `/performanceTester` - Source files for integration testing models

### Prerequisites

- C++20 compatible compiler
- CMake 3.16 or higher
- MinGW (see installation instructions below)

### MinGW Installation

1. Install MinGW:
```bash
sudo apt update
sudo apt install mingw-w64
```

2. Validate installation:
```bash
which x86_64-w64-mingw32-gcc 
which x86_64-w64-mingw32-g++
```

### Changing Models

To change the model used by the build, update the `ALGORITHM` value in the `CMakeLists.txt` file to the desired model definition and add the algorithm in main. Refer to the DumbModel implementation as an example.

### Local Build Instructions

1. Create the build directory and navigate to it:
```bash
mkdir -p build && cd build
```

2. Generate the build files:
```bash
cmake ..
```

3. Build the project:
```bash
cmake --build .
```

### Windows Cross-Compilation Instructions

1. From the project root directory, use the following command to build the project and compile the executable:
```bash
rm -rf build-windows && cmake -B build-windows -S . -DCMAKE_TOOLCHAIN_FILE=windows-toolchain.cmake -DCMAKE_BUILD_TYPE=Release && cmake --build build-windows
```

2. The .exe file is located at `./build-windows/sep25_main_#######.exe`. Note that this cannot be run locally on a Linux machine but can be copied to a Windows machine for testing.

### Running the Application

After building, run the main executable:
```bash
./build/sep25_main
```

### Running Tests

To run the unit tests:
```bash
./build/sep25_tests
```

Or use CTest for more detailed output:
```bash
cd build
ctest
```

### Running the Performance Tests

To test the performance of the model, navigate to `main.cpp` in `/performanceTester`, edit the parameters, and run:
```bash
cmake --build build && ./build/sep25_performance {dimensions} {dimensionSize} [--output outputToFile (default false)] [--rand stochastic? (default false)]
```

### Development Workflow

For development, you can use the following commands:

1. Clean build:
```bash
rm -rf build
cmake -S . -B build
cmake --build build
```

2. Run tests after building:
```bash
cmake --build build && ./build/sep25_tests
```

### Documentation Instructions

To create local documentation, use the following commands once you have a working local build:
```bash
sudo apt install doxygen
cd build
cmake --build . --target docs
```

To view the documentation, navigate to the index.html file and open it in your browser.

### Visualiser

Once you have run the performance tests and selected `true` for outputToFile, you can run the visualiser on your model. Complete the following steps:

Note: The following steps assume you are in the home directory `/SEP25`.

1. Create a virtual environment and activate it:
```bash
python3 -m venv .venv
source .venv/bin/activate
```

2. Install requirements:
```bash
pip install -r requirements.txt
```

3. Navigate to the visualiser folder:
```bash
cd ./performanceTester/visualisation/
```

4. Run the script:
```bash
python3 -m main [filename (e.g. PerformanceData2:50)]
```

5. Optional: To overlay ground truth onto your prediction, run the script with:
```bash
python3 -m main [filename (e.g. PerformanceData2:50)] true
```

This will save a visualisation of the ground truth along with your predictions in `./visualisationImages`. Note that the current implementation requires the file to contain the dimension size prior to the `:` symbol.

## Contributors

*Archie Rowe, Bowen Sun, Cuinn Kemp, David Maslov, Jarrod Hackett, Michelle Nguyen, Mischa Sarac, Mitchell Parrington, Omar Badr*