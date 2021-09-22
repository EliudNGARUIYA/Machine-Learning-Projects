# Passenger Tracking

The Open Model Zoo demo applications are console applications that demonstrate how you can use the Inference Engine in your applications to solve specific use-cases.


- [Pedestrian Tracker C++ ]- Application for pedestrian tracking scenario.

## Media Files Available for Demos

To run the demo applications, you can use images and videos from the media files collection available at https://github.com/intel-iot-devkit/sample-videos.

## Demos that Support Pre-Trained Models

> **NOTE:** Inference Engine HDDL and FPGA plugins are available in [proprietary](https://software.intel.com/en-us/openvino-toolkit) distribution only.

You can download the [pre-trained models](../models/intel/index.md) using the OpenVINO [Model Downloader](../tools/downloader/README.md) or from [https://download.01.org/opencv/](https://download.01.org/opencv/).
The table below shows the correlation between models, demos, and supported plugins. The plugins names are exactly as they are passed to the demos with `-d` option. The correlation between the plugins and supported devices see in the [Supported Devices](https://docs.openvinotoolkit.org/latest/_docs_IE_DG_supported_plugins_Supported_Devices.html) section.

> **NOTE:** **MYRIAD** below stands for Intel® Movidius™ Neural Compute Stick, Intel® Neural Compute Stick 2, and Intel® Vision Accelerator Design with Intel® Movidius™ Vision Processing Units.

| Model                                            | Demos supported on the model                                                                                 | CPU       | GPU       | MYRIAD/HDDL | HETERO:FPGA,CPU |
|--------------------------------------------------|----------------------------------------------------------------------------------------------------------------|-----------|-----------|-------------|-----------------|
      Supported     |                 |
| gaze-estimation-adas-0002                        | [Gaze Estimation Demo](./gaze_estimation_demo/README.md)                              | Supported | Supported | Supported | Supported |
| head-pose-estimation-adas-0001                   | [Gaze Estimation Demo](./gaze_estimation_demo/README.md)                              | Supported | Supported | Supported | Supported |
| facial-landmarks-35-adas-0002                    | [Gaze Estimation Demo](./gaze_estimation_demo/README.md)                              | Supported | Supported | Supported | Supported |
| pedestrian-and-vehicle-detector-adas-0001        | any demo that supports SSD\*-based models, above                                                               | Supported | Supported | Supported   | Supported       |
| pedestrian-detection-adas-0002                   | any demo that supports SSD\*-based models, above                                                               | Supported | Supported | Supported   | Supported       |
| pedestrian-detection-adas-binary-0001            | any demo that supports SSD\*-based models, above                                                               | Supported | Supported |             |                 |
| person-detection-retail-0002                     | any demo that supports SSD\*-based models, above                                                               | Supported | Supported | Supported   | Supported       |
| person-detection-retail-0013                     | any demo that supports SSD\*-based models, above                                                               | Supported | Supported | Supported   | Supported       |
| road-segmentation-adas-0001                      | any demo that supports SSD\*-based models, above                                                               | Supported | Supported | Supported   | Supported       |
| vehicle-detection-adas-binary-0001               | any demo that supports SSD\*-based models, above                                                               | Supported | Supported |             |                 |
| vehicle-detection-adas-0002                      | any demo that supports SSD\*-based models, above                                                               | Supported | Supported | Supported   | Supported       |
| yolo-v2-tiny-vehicle-detection-0001              | [Object Detection for YOLO V3 Python\* Demo](./python_demos/object_detection_demo_yolov3_async/README.md) | Supported |           |             |                 |


Notice that the FPGA support comes through a [heterogeneous execution](https://docs.openvinotoolkit.org/latest/_docs_IE_DG_supported_plugins_HETERO.html), for example, when the post-processing is happening on the CPU.

## Build the Demo Applications

To be able to build demos you need to source _InferenceEngine_ and _OpenCV_ environment from a binary package which is available as [proprietary](https://software.intel.com/en-us/openvino-toolkit) distribution.
Please run the following command before the demos build (assuming that the binary package was installed to `<INSTALL_DIR>`):
```sh
source <INSTALL_DIR>/deployment_tools/bin/setupvars.sh
```
You can also build demos manually using Inference Engine built from the [openvino](https://github.com/openvinotoolkit/openvino) repo. In this case please set `InferenceEngine_DIR` environment variable to a folder containing `InferenceEngineConfig.cmake` and `ngraph_DIR` to a folder containing `ngraphConfig.cmake` in a build folder. Please also set the `OpenCV_DIR` to point to the OpenCV package to use. The same OpenCV version should be used both for Inference Engine and demos build. Alternatively these values can be provided via command line while running `cmake`. See [CMake's search procedure](https://cmake.org/cmake/help/latest/command/find_package.html#search-procedure).
Please refer to the Inference Engine <a href="https://github.com/openvinotoolkit/openvino/blob/master/build-instruction.md">build instructions</a>
for details. Please also add path to built Inference Engine libraries to `LD_LIBRARY_PATH` (Linux*) or `PATH` (Windows*) variable before building the demos.

### <a name="build_demos_linux"></a>Build the Demo Applications on Linux*

The officially supported Linux* build environment is the following:

* Ubuntu* 16.04 LTS 64-bit or CentOS* 7.4 64-bit
* GCC* 5.4.0 (for Ubuntu* 16.04) or GCC* 4.8.5 (for CentOS* 7.4)
* CMake* version 2.8 or higher.

To build the demo applications for Linux, go to the directory with the `build_demos.sh` script and
run it:
```sh
build_demos.sh
```

You can also build the demo applications manually:

1. Navigate to a directory that you have write access to and create a demos build directory. This example uses a directory named `build`:
```sh
mkdir build
```
2. Go to the created directory:
```sh
cd build
```

3. Run CMake to generate the Make files for release or debug configuration:
  - For release configuration:
  ```sh
  cmake -DCMAKE_BUILD_TYPE=Release <open_model_zoo>/demos
  ```
  - For debug configuration:
  ```sh
  cmake -DCMAKE_BUILD_TYPE=Debug <open_model_zoo>/demos
  ```
4. Run `make` to build the demos:
```sh
make
```

For the release configuration, the demo application binaries are in `<path_to_build_directory>/intel64/Release/`;
for the debug configuration — in `<path_to_build_directory>/intel64/Debug/`.

### <a name="build_demos_windows"></a>Build the Demos Applications on Microsoft Windows* OS

The recommended Windows* build environment is the following:
* Microsoft Windows* 10
* Microsoft Visual Studio* 2015, 2017, or 2019
* CMake* version 2.8 or higher

> **NOTE**: If you want to use Microsoft Visual Studio 2019, you are required to install CMake 3.14.

To build the demo applications for Windows, go to the directory with the `build_demos_msvc.bat`
batch file and run it:
```bat
build_demos_msvc.bat
```

By default, the script automatically detects the highest Microsoft Visual Studio version installed on the machine and uses it to create and build
a solution for a demo code. Optionally, you can also specify the preffered Microsoft Visual Studio version to be used by the script. Supported
versions are: `VS2015`, `VS2017`, `VS2019`. For example, to build the demos using the Microsoft Visual Studio 2017, use the following command:
```bat
build_demos_msvc.bat VS2017
```

The demo applications binaries are in the `C:\Users\<username>\Documents\Intel\OpenVINO\omz_demos_build_build\intel64\Release` directory.

You can also build a generated solution by yourself, for example, if you want to
build binaries in Debug configuration. Run the appropriate version of the
Microsoft Visual Studio and open the generated solution file from the `C:\Users\<username>\Documents\Intel\OpenVINO\omz_demos_build\Demos.sln`
directory.

### <a name="build_python_extensions"></a>Build the Native Python* Extension Modules

Some of the Python demo applications require native Python extension modules to be built before they can be run.
This requires you to have Python development files (headers and import libraries) installed.
To build these modules, follow the instructions for building the demo applications above,
but add `-DENABLE_PYTHON=ON` to either the `cmake` or the `build_demos*` command, depending on which you use.
For example:

```sh
cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_PYTHON=ON <open_model_zoo>/demos
```

## Get Ready for Running the Demo Applications

### Get Ready for Running the Demo Applications on Linux*

Before running compiled binary files, make sure your application can find the Inference Engine and OpenCV libraries.
If you use a [proprietary](https://software.intel.com/en-us/openvino-toolkit) distribution to build demos,
run the `setupvars` script to set all necessary environment variables:
```sh
source <INSTALL_DIR>/bin/setupvars.sh
```
If you use your own Inference Engine and OpenCV binaries to build the demos please make sure you have added them
to the `LD_LIBRARY_PATH` environment variable.

**(Optional)**: The OpenVINO environment variables are removed when you close the
shell. As an option, you can permanently set the environment variables as follows:

1. Open the `.bashrc` file in `<user_home_directory>`:
```sh
vi <user_home_directory>/.bashrc
```

2. Add this line to the end of the file:
```sh
source <INSTALL_DIR>/bin/setupvars.sh
```

3. Save and close the file: press the **Esc** key, type `:wq` and press the **Enter** key.
4. To test your change, open a new terminal. You will see `[setupvars.sh] OpenVINO environment initialized`.

To run Python demo applications that require native Python extension modules, you must additionally
set up the `PYTHONPATH` environment variable as follows, where `<bin_dir>` is the directory with
the built demo applications:

```sh
export PYTHONPATH="$PYTHONPATH:<bin_dir>/lib"
```

You are ready to run the demo applications. To learn about how to run a particular
demo, read the demo documentation by clicking the demo name in the demo
list above.

### Get Ready for Running the Demo Applications on Windows*

Before running compiled binary files, make sure your application can find the Inference Engine and OpenCV libraries.
Optionally download OpenCV community FFmpeg plugin. There is a downloader script in the OpenVINO package: `<INSTALL_DIR>\opencv\ffmpeg-download.ps1`.
If you use a [proprietary](https://software.intel.com/en-us/openvino-toolkit) distribution to build demos,
run the `setupvars` script to set all necessary environment variables:
```bat
<INSTALL_DIR>\bin\setupvars.bat
```
If you use your own Inference Engine and OpenCV binaries to build the demos please make sure you have added
to the `PATH` environment variable.

To run Python demo applications that require native Python extension modules, you must additionally
set up the `PYTHONPATH` environment variable as follows, where `<bin_dir>` is the directory with
the built demo applications:

```bat
set PYTHONPATH=%PYTHONPATH%;<bin_dir>
```

To debug or run the demos on Windows in Microsoft Visual Studio, make sure you
have properly configured **Debugging** environment settings for the **Debug**
and **Release** configurations. Set correct paths to the OpenCV libraries, and
debug and release versions of the Inference Engine libraries.
For example, for the **Debug** configuration, go to the project's
**Configuration Properties** to the **Debugging** category and set the `PATH`
variable in the **Environment** field to the following:

```
PATH=<INSTALL_DIR>\deployment_tools\inference_engine\bin\intel64\Debug;<INSTALL_DIR>\opencv\bin;%PATH%
```
where `<INSTALL_DIR>` is the directory in which the OpenVINO toolkit is installed.

You are ready to run the demo applications. To learn about how to run a particular
demo, read the demo documentation by clicking the demo name in the demos
list above.

## See Also
* [Introduction to Intel's Deep Learning Inference Engine](https://docs.openvinotoolkit.org/latest/_docs_IE_DG_Introduction.html)
