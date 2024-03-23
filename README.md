# NestConfig

NestConfig is a flexible configuration management system designed to simplify 
the handling of configurations in Python applications. 
It leverages Python's type hints and dataclasses to offer type-safe 
configuration updates, including support for nested configurations and 
direct application of command-line options.

This class is similar to 
[fvcore.common.config.CfgNode](https://github.com/facebookresearch/fvcore/blob/main/fvcore/common/config.py), 
but it offers the added benefit of **AutoCompletion**.

## Features

- Type-safe configuration management using dataclasses.
- Support for nested configurations.
- Easy integration of command-line options into the configuration.
- Simple and intuitive usage.

## Installation

To install NestConfig, simply use pip:

```bash
pip install nestconfig
```

It can also be built from source with ```pip install .``` from this repository.

## How to use
### Minimal Example
```python
from dataclasses import dataclass
from nestconfig import NestConfig

@dataclass
class ModelConfig:
    ENC_NUM_HEADS: int = 8

@dataclass
class Config(NestConfig):
    MODEL: ModelConfig = ModelConfig()
    SOME_OTHER_CONFIG: int = 10

# Instantiate your configuration
config = Config()

# Update the configuration with new values.
# You can also use a yaml file: updates = yaml.safe_load(yaml_file)
updates = {'MODEL': {'ENC_NUM_HEADS': 12}, 'SOME_OTHER_CONFIG': 15}
config.merge_updates(updates)
print(config.MODEL.ENC_NUM_HEADS)  # Outputs: 12
print(config.SOME_OTHER_CONFIG)  # Outputs: 15

# Apply command-line options directly.
# You can use argparse here and set opts to args.opts
opts = ['MODEL.ENC_NUM_HEADS', '16', 'SOME_OTHER_CONFIG', '20']
config.merge_opts(opts)
print(config.MODEL.ENC_NUM_HEADS)  # Outputs: 16
print(config.SOME_OTHER_CONFIG)  # Outputs: 20
```

### More examples
More examples can be found in [test](test) folder.

### Blog post
A blog post can be found [here](https://zeyun-zhong.github.io/blog/2024/NestConfig/).

If you find this code useful, please consider giving it a star (☆) :).
