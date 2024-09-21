# InterruptAtomicCompareExchange

This project demonstrates how to safely handle interrupts in an embedded system using atomic operations to avoid race conditions. Specifically, it showcases the usage of `atomic_compare_exchange_strong` to handle flag ownership between the main loop and an interrupt handler. The project is built using Keil uVision and is targeted for the STM32F401RE microcontroller.

## Features:
- **Platform**: STM32F401RE
- **Tools**: Keil uVision IDE (I suspect STMCubeIDE works too, I just checked in the sources, no projects).
- **Dependency**: This project depends on the Valvano Texas Instruments COM port reader, which can be obtained by downloading ValvanoWaveTMC123v6.zip from the [Valvano website](https://users.ece.utexas.edu/~valvano/arm/#FSM).

### Project Overview:
The main goal of this project is to demonstrate how to use atomic operations to manage a shared flag between an interrupt service routine (ISR) and the main program. The flag ensures mutual exclusion so that both the ISR and the main loop can safely print over UART without clashing.

### Key Components:
- **UART Initialization**: UART is initialized using UART0 for communication, which outputs to a serial terminal.
- **Atomic Flag Handling**: The main program and the ISR both check the `flag` using `atomic_compare_exchange_strong`. Only one can print at a time, ensuring synchronization between the two contexts.
- **TIM2 Interrupt**: TIM2 is configured to trigger an interrupt periodically. The interrupt handler checks and sets the atomic flag, and if successful, it prints a message over UART.

### Setup:
1. **Board**: STM32F401RE
2. **Valvano COM Port Reader**: The project assumes you have the Valvano COM port reader for observing UART output.
3. **Keil uVision**: This project is set up to run in the Keil uVision IDE, create new project and add these files.  STMCubeIDE should work too, configure the Terminal to serial and COM5 if you are using ST-Link drivers for usb.

### Usage:
1. **Clone the repository**:
   ```bash
   git clone https://github.com/stevemac321/InterruptAtomicCompareExchange.git
