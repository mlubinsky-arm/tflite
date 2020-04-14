## TFLite + MbedOs

<https://www.tensorflow.org/lite/microcontrollers>

Models are kept in read-only program memory and provided in the form of a simple C file. 
Standard tools can be used to convert the FlatBuffer into a C array:

<https://www.tensorflow.org/lite/microcontrollers/build_convert#convert_to_a_c_array>

```
xxd -i converted_model.tflite > model_data.cc
```
Once you have generated the file, you can include it in your program. It is important to change the array declaration to const for better memory efficiency on embedded platforms.

Example:
<https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/examples/hello_world/sine_model_data.cc>

<https://github.com/tensorflow/tensorflow/blob/master/tensorflow/lite/micro/examples/hello_world/main_functions.cc>

```
git clone --depth 1 https://github.com/tensorflow/tensorflow.git
cd tensorflow
```
use Make version >= 4.2.1
```
make -f tensorflow/lite/experimental/micro/tools/make/Makefile TARGET=mbed TAGS="CMSIS disco_f746ng" generate_hello_world_mbed_project
```
You should see the expected mbed folder here:
```
tensorflow/lite/experimental/micro/tools/make/gen/mbed_cortex-m4/prj/hello_world/mbed/
```
