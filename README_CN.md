# 用于 Zephyr 系统的 Memfault 示例应用 

在 https://github.com/zephyrproject-rtos/example-application 和 https://github.com/memfault/zephyr-memfault-example.git 基础上进行更改, 为Memfault的集成提供的最基础的参考

该项目应该可以运行在任何受到支持的板子上*

*对于 NXP RT10xx EVKs 系列，需要使用下面的分支 (在 RT1021 和 RT1060)上进行了测试:

- https://github.com/memfault/zephyr-memfault-example/tree/rt102x-noinit-workaround

## 使用方法

在设置好 zephyr 开发环境后[zephyr_getting_start](https://docs.zephyrproject.org/latest/getting_started/index.html), 运行以下指令进行测试

```shell
# 初始化这个项目
❯ west init -m https://github.com/dingiso/zephyr-memfault-example.git zephyr-memfault-example
❯ cd zephyr-memfault-example
❯ west update

# build- example here is Nordic nRF52480 dk
❯ west build -b nrf9160dk_nrf9160_ns -s zephyr-memfault-example/app

# connect the USB cable to the board

# open a console in one terminal
❯ pyserial-miniterm /dev/serial/by-id/usb-SEGGER_J-Link_000683232543-if00 115200 --raw

# now flash from another terminal
❯ west flash

# the console should start working
uart:~$ mflt get_device_info
<inf> <mflt>: S/N: DEMOSERIAL
<inf> <mflt>: SW type: zephyr-app
<inf> <mflt>: SW version: 1.0.0-dev
<inf> <mflt>: HW version: nrf52840dk_nrf52840
```

For testing without real hardware, a `qemu` target can be used, for example:

```bash
❯ west build -b qemu_cortex_m3 --pristine=always zephyr-memfault-example/app
❯ west build -t run

[00:00:00.000,000] <inf> main: Memfault Demo App! Board qemu_cortex_m3

<inf> mflt: S/N: DEMOSERIAL
<inf> mflt: SW type: zephyr-app
<inf> mflt: SW version: 1.0.0-dev
<inf> mflt: HW version: qemu_cortex_m3
```
