# tflite_convert without fused activation function

## Build

+ Follow https://www.tensorflow.org/install/source to build it

```bash
$ virtualenv --python python3.6 env_tf2
$ source env_tf2/bin/activate
$ pip install numpy==1.18.5 wheel
$ pip install h5py==2.10.0
$ pip install keras_preprocessing --no-deps

$ git clone https://github.com/aben20807/tensorflow.git
$ cd tensorflow
$ git checkout aben20807-v2.3.4-no-fused-activation

$ ./configure
$ bazel clean
$ bazel build -c opt tensorflow/lite/python:tflite_convert
```

## Usage

```bash
$ bazel-bin/tensorflow/lite/python/tflite_convert --keras_model_file=<input h5> --output_file=<output tflite> --inference_type=QUANTIZED_UINT8 --inference_input_type=QUANTIZED_UINT8 --std_dev_values=1 --mean_values=0 --default_ranges_min=0 --default_ranges_max=255 --experimental_new_converter
```

## Results

+ Before

![Screenshot from 2021-11-08 10-24-41](https://user-images.githubusercontent.com/14831545/140674960-aed527e0-cb39-497f-9920-b76f68f0fe05.png)

+ After

![Screenshot from 2021-11-08 10-24-53](https://user-images.githubusercontent.com/14831545/140674965-822b7ec3-3846-40b7-9ce8-57376ea83226.png)
