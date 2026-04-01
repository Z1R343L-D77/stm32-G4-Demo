# STM32 G4 Demo

该仓库包含 STM32 G4 系列微控制器的基础项目设置，使用 CLion 作为开发环境，并通过 CMake 和 STM32CubeMX 配置进行构建。项目包含多个子项目，展示了不同功能的实现，如LED控制、按键处理、LCD显示、ADC采集和日历功能等。

## 项目概述

本项目旨在为 STM32 G4 系列微控制器提供一个基础的开发框架，包含以下特点：
- 使用 CLion + CMake + STM32CubeMX 的开发环境
- 模块化的代码结构，分离核心代码、驱动代码和应用代码
- 自定义驱动和应用模块，如 GPIO 操作、按钮处理、调度器等
- 多个子项目，展示不同功能的实现

## 子项目说明

项目包含以下子项目：

| 子项目名称 | 功能描述 |
|-----------|---------|
| 001_Led_Key | 基础的 LED 控制和按键处理 |
| 002_Lcd | LCD 显示功能 |
| 003_List_Lcd单向链表 | 单向链表实现和 LCD 显示 |
| 003_List_Lcd双向链表 | 双向链表实现和 LCD 显示 |
| 004_Adc | ADC 采集功能 |
| 005_Calendar | 日历功能 |

## 项目结构

项目结构如下：

```
stm32-G4-Demo/
├── 001_Led_Key/                # LED 控制和按键处理项目
│   ├── .idea/                       # CLion IDE 配置文件
│   ├── cmake-build-debug/           # 构建目录
│   ├── Core/                        # 核心功能代码
│   │   ├── Inc/                     # 头文件
│   │   └── Src/                     # 源文件
│   ├── Drivers/                     # 外设驱动代码
│   │   ├── CMSIS/                   # CMSIS 核心文件
│   │   └── STM32G4xx_HAL_Driver/    # STM32 G4 HAL 驱动
│   ├── myApp/                       # 应用程序代码
│   │   ├── bsp_key.h                # 按键处理头文件
│   │   ├── bsp_system.h             # 系统相关头文件
│   │   ├── loop.c                   # 主循环实现
│   │   └── scheduler.h              # 调度器头文件
│   ├── myDrivers/                   # 自定义驱动代码
│   │   ├── myGpio.h                 # GPIO 操作头文件
│   │   └── myButton.h               # 按钮处理头文件
│   ├── .gitignore                   # Git 忽略文件
│   ├── LICENSE                      # 开源许可证文件
│   ├── CMakeLists.txt               # CMake 构建配置文件
│   └── 001_Led_Key.ioc              # STM32CubeMX 配置文件
├── 002_Lcd/                        # LCD 显示项目
├── 003_List_Lcd单向链表/            # 单向链表和 LCD 显示项目
├── 003_List_Lcd双向链表/            # 双向链表和 LCD 显示项目
├── 004_Adc/                        # ADC 采集项目
├── 005_Calendar/                    # 日历功能项目
├── .gitignore                       # Git 忽略文件
└── LICENSE                          # 开源许可证文件
```

## 前提条件

- **IDE**: CLion 2021.3 或更高版本
- **工具链**: ARM GCC 工具链（如 GNU Arm Embedded Toolchain）
- **CMake**: 3.16 或更高版本
- **STM32CubeMX**: 6.0 或更高版本
- **OpenOCD**: 用于烧录和调试

## 设置与构建

### 1. 安装必要的工具

1. **安装 CLion**：从 [JetBrains 官网](https://www.jetbrains.com/clion/) 下载并安装 CLion。
2. **安装 ARM GCC 工具链**：从 [ARM 官网](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads) 下载并安装 GNU Arm Embedded Toolchain。
3. **安装 STM32CubeMX**：从 [ST 官网](https://www.st.com/en/development-tools/stm32cubemx.html) 下载并安装 STM32CubeMX。
4. **安装 OpenOCD**：从 [OpenOCD 官网](https://openocd.org/) 下载并安装 OpenOCD。

### 2. 克隆仓库

```bash
git clone https://github.com/D77go77/stm32-G4-Demo.git
cd stm32-G4-Demo
```

### 3. 配置 CLion

1. **打开项目**：打开 CLion，选择 "Open" 打开 `stm32-G4-Demo` 目录。
2. **配置工具链**：
   - 进入 File > Settings > Build, Execution, Deployment > Toolchains
   - 点击 "+" 添加新的工具链，选择 "Cross-Compiler"
   - 配置以下路径：
     - C Compiler: 指向 ARM GCC 工具链中的 `arm-none-eabi-gcc.exe`
     - C++ Compiler: 指向 ARM GCC 工具链中的 `arm-none-eabi-g++.exe`
     - Debugger: 指向 OpenOCD 中的 `openocd.exe`
3. **配置 CMake**：
   - 进入 File > Settings > Build, Execution, Deployment > CMake
   - 选择刚才配置的工具链
   - 在 "CMake options" 中添加适当的参数，如 `-DCMAKE_TOOLCHAIN_FILE=cmake/arm-none-eabi.cmake`
4. **配置 OpenOCD**：
   - 进入 Run > Edit Configurations
   - 点击 "+" 添加 "OpenOCD Download & Run"
   - 配置 "Board config file" 为适用的配置文件，如 `cmsis-dap.cfg`

### 4. 构建项目

1. **选择子项目**：在 CLion 中打开相应子项目的目录，如 `001_Led_Key`。
2. **构建项目**：点击 "Build" 按钮或使用快捷键 `Ctrl+F9` 进行项目编译。

### 5. 烧录固件

1. **连接开发板**：使用 USB 线缆将 STM32 G4 开发板连接到电脑。
2. **烧录固件**：点击 "Run" 按钮或使用快捷键 `Shift+F10` 将固件烧录到开发板上。

## 代码说明

### 主要模块

1. **GPIO 操作**：通过 `myGpio.h` 提供 GPIO 的初始化和操作功能。
2. **按钮处理**：通过 `myButton.h` 提供按钮的初始化和状态检测功能。
3. **调度器**：通过 `scheduler.h` 提供任务调度功能，实现多任务的并发执行。
4. **主循环**：在 `loop.c` 中实现，初始化系统组件并进入无限循环运行调度器。

### 核心流程

1. **系统初始化**：在 `main.c` 中，系统首先进行 HAL 初始化，然后配置系统时钟，最后初始化所有外设。
2. **应用初始化**：调用 `loop()` 函数，初始化 GPIO、按钮和调度器。
3. **主循环**：进入无限循环，运行调度器处理任务。

## 注意事项

1. **工具链配置**：确保 ARM GCC 工具链和 OpenOCD 已正确安装并配置。
2. **CubeMX 配置**：如果需要修改外设配置，可以通过 STM32CubeMX 打开相应的 `.ioc` 文件进行修改，然后重新生成代码。
3. **调试**：可以使用 CLion 的调试功能，通过 OpenOCD 对代码进行调试。
4. **硬件连接**：确保开发板的硬件连接正确，特别是 LED 和按键的连接。

## 常见问题

1. **构建失败**：检查 CMake 配置和工具链路径是否正确。
2. **烧录失败**：检查开发板是否正确连接，OpenOCD 配置文件是否适用。
3. **功能异常**：检查硬件连接和代码逻辑是否正确。

## 许可证

本项目采用 GPL-3.0 许可证 - 详情请参见 [LICENSE](LICENSE) 文件。
