# Run-On-Arch Github Action


[![](https://github.com/uraimo/run-on-arch-action/workflows/Test/badge.svg)](https://github.com/uraimo/run-on-arch/actions)

A Github Action that executes commands on an alternative architecture (amd64, i386, arm64, armv7, s390x, ppc64le).

## Usage

This action requires three input parameters:

* `architecture`: The cpu architecture of the container that will run your commands;
* `distribution`: The Linux distribution the will be launched by the container (right now, Debian stretch and buster);
* `run`: A series of commands that will be executed.

The action does not define any default output variable, feel free to create as many as you want and set them in the `run` block. 

### Basic example

This basic example executes `uname -a` and then does it again to save the value in a variable:

```
on: [push]

jobs:
  armv7_job:
    runs-on: ubuntu-18.04
    name: Build on ARMv7 
    steps:
      - uses: actions/checkout@v1.0.0
      - uses: baetyl/run-on-arch-action@master
        id: runcmd
        with:
          architecture: armv7
          distribution: buster
          run: |
            uname -a
            echo ::set-output name=uname::$(uname -a)
      - name: Get the output
        run: |
            echo "The uname output was ${{ steps.runcmd.outputs.uname }}"
```

## Supported Platforms

This table contains a list of possible Architecture/Distribution combinations:

| Architecture | Distributions |
| -------- | ------------- |
| amd64    | stretch, buster |
| i386    | stretch, buster |
| arm64    | stretch, buster|
| armv7  | stretch, buster |
| s390x  | stretch, buster |
| ppc64le  | stretch, buster |

Using an invalid combination will result in a crash but new configuration can be easily added if a working docker image is available.

## License

This project is licensed under the [BSD 3-Clause License](https://github.com/baetyl/run-on-arch-action/blob/master/LICENSE).
