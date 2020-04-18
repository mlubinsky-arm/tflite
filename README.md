## TFLite + MbedOs

<https://www.tensorflow.org/lite/microcontrollers>

Models are kept in read-only program memory and provided in the form of a simple C file. 
Standard tools can be used to convert the FlatBuffer into a C array:

<https://www.tensorflow.org/lite/microcontrollers/build_convert#convert_to_a_c_array>

```
xxd -i converted_model.tflite > model_data.cc
```
Once you have generated the file, you can include it in your program. It is important to change the array declaration to const for better memory efficiency on embedded platforms.


### C++ 11

By default, Mbed will build the project using C++98. However, TensorFlow Lite requires C++11. Run the following Python snippet to modify the Mbed configuration files so that it uses C++11:
```
python -c 'import fileinput, glob;
for filename in glob.glob("mbed-os/tools/profiles/*.json"):
  for line in fileinput.input(filename, inplace=True):
    print line.replace("\"-std=gnu++98\"","\"-std=c++11\", \"-fpermissive\"")'
```

```
/Users/miclub01/GIT/tensorflow/tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4/prj
(mbed) (base) [prj](master)$ ls ./hello_world/mbed/tensorflow/lite/micro/examples/hello_world/
constants.h        main.cc            main_functions.h   sine_model_data.cc
disco_f746ng       main_functions.cc  output_handler.h   sine_model_data.h
```
### Example:
<https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/micro/examples/hello_world>

<https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/examples/hello_world/sine_model_data.cc>

<https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/examples/hello_world/main_functions.cc>

<https://stackoverflow.com/questions/60764852/deploying-tflite-on-microcontrollers>

```
git clone --depth 1 https://github.com/tensorflow/tensorflow.git
cd tensorflow
```
use Make version >= 4.2.1
```
gmake -f tensorflow/lite/micro/tools/make/Makefile  TARGET=mbed TAGS="CMSIS disco_f746ng" generate_hello_world_mbed_project
gmake -f tensorflow/lite/micro/tools/make/Makefile  TARGET=mbed  generate_hello_world_mbed_project

cd tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4/prj/hello_world/mbed
find tensorflow/ | grep main
tensorflow//lite/micro/examples/hello_world/main.cc
tensorflow//lite/micro/examples/hello_world/main_functions.h
tensorflow//lite/micro/examples/hello_world/main_functions.cc

ls
BSP_DISCO_F746NG     LCD_DISCO_F746NG     README_MBED.md       mbed-os.lib          run.sh
BSP_DISCO_F746NG.lib LCD_DISCO_F746NG.lib __pycache__          mbed_app.json        tensorflow
BUILD                LICENSE              mbed-os              mbed_settings.py     third_party


mbed compile -m DISCO_F746NG -t GCC_ARM 
```

## CMSIS
<https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/micro/kernels/cmsis-nn>
<https://arm-software.github.io/CMSIS_5/General/html/index.html>
<https://github.com/ARM-software/CMSIS_5>

