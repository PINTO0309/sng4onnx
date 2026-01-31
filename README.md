# sng4onnx
A simple tool that automatically generates and assigns an OP name to each OP in an old format ONNX file.
**S**imple op **N**ame **G**enerator for **ONNX**.

https://github.com/PINTO0309/simple-onnx-processing-tools

[![Downloads](https://static.pepy.tech/personalized-badge/sng4onnx?period=total&units=none&left_color=grey&right_color=brightgreen&left_text=Downloads)](https://pepy.tech/project/sng4onnx) ![GitHub](https://img.shields.io/github/license/PINTO0309/sng4onnx?color=2BAF2B) [![PyPI](https://img.shields.io/pypi/v/sng4onnx?color=2BAF2B)](https://pypi.org/project/sng4onnx/) [![CodeQL](https://github.com/PINTO0309/sng4onnx/workflows/CodeQL/badge.svg)](https://github.com/PINTO0309/sng4onnx/actions?query=workflow%3ACodeQL)

<p align="center">
  <img src="https://user-images.githubusercontent.com/33194443/195636410-a797d847-365a-469e-8bdd-7a3abb8aa3fd.png" />
</p>

# Key concept

- [x] Automatically generates and assigns an OP name to each OP in an old format ONNX file.

## 1. Setup
### 1-1. HostPC
```bash
### option
$ echo export PATH="~/.local/bin:$PATH" >> ~/.bashrc \
&& source ~/.bashrc

### run
$ pip install -U onnx \
&& python3 -m pip install -U onnx_graphsurgeon --index-url https://pypi.ngc.nvidia.com \
&& pip install -U sng4onnx
```
### 1-2. Docker
https://github.com/PINTO0309/simple-onnx-processing-tools#docker

## 2. CLI Usage
```
$ sng4onnx -h

usage:
  sng4onnx [-h]
  -if INPUT_ONNX_FILE_PATH
  -of OUTPUT_ONNX_FILE_PATH
  [-n]

optional arguments:
  -h, --help
      show this help message and exit.

  -if INPUT_ONNX_FILE_PATH, --input_onnx_file_path INPUT_ONNX_FILE_PATH
      Input onnx file path.

  -of OUTPUT_ONNX_FILE_PATH, --output_onnx_file_path OUTPUT_ONNX_FILE_PATH
      Output onnx file path.

  -n, --non_verbose
      Do not show all information logs. Only error logs are displayed.
```

## 3. In-script Usage
```python
>>> from sng4onnx import generate
>>> help(generate)

Help on function generate in module sng4onnx.onnx_opname_generator:

generate(
    input_onnx_file_path: Union[str, NoneType] = '',
    onnx_graph: Union[onnx.onnx_ml_pb2.ModelProto, NoneType] = None,
    output_onnx_file_path: Union[str, NoneType] = '',
    has_external_data: Optional[bool] = False,
    non_verbose: Union[bool, NoneType] = False
) -> onnx.onnx_ml_pb2.ModelProto

    Parameters
    ----------
    input_onnx_file_path: Optional[str]
        Input onnx file path.
        Either input_onnx_file_path or onnx_graph must be specified.
        Default: ''

    onnx_graph: Optional[onnx.ModelProto]
        onnx.ModelProto.
        Either input_onnx_file_path or onnx_graph must be specified.
        onnx_graph If specified, ignore input_onnx_file_path and process onnx_graph.

    output_onnx_file_path: Optional[str]
        Output onnx file path. If not specified, no ONNX file is output.
        Default: ''

    has_external_data: Optional[bool]
        Default: False

    non_verbose: Optional[bool]
        Do not show all information logs. Only error logs are displayed.
        Default: False

    Returns
    -------
    renamed_graph: onnx.ModelProto
        Renamed onnx ModelProto.
```

## 4. CLI Execution
```bash
$ sng4onnx \
--input_onnx_file_path emotion-ferplus-8.onnx \
--output_onnx_file_path emotion-ferplus-8_renamed.onnx
```

## 5. In-script Execution
```python
from sng4onnx import generate

onnx_graph = generate(
  input_onnx_file_path="fusionnet_180x320.onnx",
  output_onnx_file_path="fusionnet_180x320_renamed.onnx",
)
```

## 6. Sample
https://github.com/onnx/models/blob/main/vision/classification/resnet/model/resnet18-v1-7.onnx
### Before
![image](https://user-images.githubusercontent.com/33194443/195632927-75c76b9a-a14b-411c-8932-f114dc2b9f29.png)

### After
![image](https://user-images.githubusercontent.com/33194443/195633029-86b0ebec-3df5-4dc4-b0ec-079f4f063e46.png)

## 7. Reference
1. https://github.com/onnx/onnx/blob/main/docs/Operators.md
2. https://docs.nvidia.com/deeplearning/tensorrt/onnx-graphsurgeon/docs/index.html
3. https://github.com/NVIDIA/TensorRT/tree/main/tools/onnx-graphsurgeon
4. https://github.com/PINTO0309/simple-onnx-processing-tools
5. https://github.com/PINTO0309/PINTO_model_zoo

## 8. Issues
https://github.com/PINTO0309/simple-onnx-processing-tools/issues
