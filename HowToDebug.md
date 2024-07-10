Qtcreator is a great IDE for C and C++ development and we will use it for setting up a debugger for AMBF. You can use the debugger both for AMBF or any of its plugins.

# Qt Creator first time setup

<details>
<summary>Click to expand</summary>
<br>
When installing Qt creator for the first time you will need to disable the plugins `ClangCodeModel` and the `ClangTools` to avoid getting linting errors when seeing AMBF source code.

<br>

![f177c03386d74e7d5064955a4cd77a06.png](_resources/f177c03386d74e7d5064955a4cd77a06.png)

Plugin configuration can be found in the `Help` -> `about plugins`

![048e2d189d6eef119a914028ecd2ce59.png](_resources/048e2d189d6eef119a914028ecd2ce59.png)

</details>

# Debugging AMBF source code

Before starting make sure you are not auto sourcing any AMBF build into your terminal session.

### Step 0

Qt Creator stores configurations for each `CMake` project in a `xml` file called `CMakeLists.txt.user`. Please make sure to erase this file before continuing the steps below. This file would be usually found in the root folder of `ambf`.

### Step 1

Compile AMBF in debug mode. Make sure you are not sourcing any previously compiled versions of ROS into your terminal session.

```
cd <ambf path>
mkdir build-debug
cd build-debug
cmake .. -DCMAKE_BUILD_TYPE=Debug
make 
```

Note that you can also have another build folder with 'Release' mode build for AMBF. Excutables for the debug and release builds are kept separated. 

### Step 2

Open Qt creator in a new terminal session and source ROS and the ambf-debug build from step one.

```
source  <ambf path>/build-debug/devel/setup.bash
qtcreator
```

Now, import AMBF into Qt Creator the using the `CMakeLists.txt` file in the root folder of AMBF. Make sure you get the configure project window. If you don't see the configure project window please see [troubleshooting section](#troubleshooting).

![8d28e139e45676a621b9152bbbf61b0f.png](_resources/8d28e139e45676a621b9152bbbf61b0f.png)

From the configure window select only the kit that contains the debug information.

![68537db0ae3f4c376376c1baba0c407c.png](_resources/68537db0ae3f4c376376c1baba0c407c.png)

### Step 3

Select a break point and start the debugger.

![02f7e89d176fa77c35732b3558b8808b.png](_resources/02f7e89d176fa77c35732b3558b8808b.png)

Then, finally select the correct executable and run the debugger

![af9284f2248d71d7762ed145311c243d.png](_resources/af9284f2248d71d7762ed145311c243d.png)

# Debugging AMBF plugin

Before debugging an AMBF plugin, make sure that you are able to run the [debugger in ambf](#debugging-ambf-source-code).

### Step 1 - Build your plugin in debug mode

Compile your plugin in debug mode. Remember to source the correct AMBF build. Before compiling also make sure that the CMAKE option `AMBF_DIR` points to the build-debug. After you changing the "AMBF_DIR" option in `ccmake`, you can configure with "c" and generate by pressing "g".

```
cd <plugin path>
cd build
ccmake . # Change the "AMBF_DIR" to "<ambf path>/build-debug"
cmake .. -DCMAKE_BUILD_TYPE=Debug
make
```

### Step 2 - Add project in Qt Creator

Add plugin code to Qt Creator and re select AMBF project as the active project. You can do this by right clicking on the ambf project.

![ba85de45991a2dbb8f30e38e84d9f9dc.png](_resources/ba85de45991a2dbb8f30e38e84d9f9dc.png)

### Step 3 - Config CMD arguments and run debugger

Config command line arguments. Remember to use absolute paths.

![1454c7c5a25248d6dc64d652798c0ddf.png](_resources/1454c7c5a25248d6dc64d652798c0ddf.png)

Then, select a break point in your plugin and run the debugger.

### Troubleshooting

In case of any problem, the best option is to erase the `CMakeLists.txt.user` that stores the QtCreator configuration for a project and the `CMakeCache.txt` (stored in your build folder) and start the debuging steps again.

