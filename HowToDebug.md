# How to Debug AMBF and AMBF Plugin


## Compile AMBF in debug mode
Go in to your ambf repo and create new folder "build-debug".

Do NOT use Qtcreator debug mode before doing the following steps.

```
cd <ambf path>
mkdir build-debug
cd build-debug
cmake .. -DCMAKE_BUILD_TYPE=Debug #Change build type in Debug mode
make 
```
## Compile plugin in Debug mode
After compiling AMBF in the debug mode, specify the "AMBF_DIR" to point to the "build-debug" folder that you created in the previous step.
After you change "AMBF_DIR", you can configure by "c" and generate by  pressing "g".

```
cd <plugin path>
cd build
ccmake . # Change the "AMBF_DIR" to "<ambf path>/build-debug"
cmake .. -DCMAKE_BUILD_TYPE=Debug
make
```

## QtCreator
Please make sure that you have finished the previous steps before going to this step.

Open the projects, AMBF and your plugin, and build them in "DEBUG" mode.
Select AMBF project as "active project" and specify your run configuratioin in "Project" tab on your left.

![Qtcreator_documentation](./howtodebug_image.png)

## Trouble shooting
In the case when you have a trouble compiling, you can try following steps and redo the steps.

```
rm CMakeLists.txt.user #If using QtCreator
rm CMakeCache.txt
```
