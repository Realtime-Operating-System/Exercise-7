# Excerise 7

The exercise demonstrates how sharing resources in a multitasking design can lead to system performance deterioration. It uses the STM32F1 board and FreeRTOS to simulate resource contention and address critical section challenges. The project implements multiple threads controlling LEDs, where critical sections of the code are managed using FreeRTOS APIs to simulate contention and critical resource management.

## Prequisites
### Hardware: 
STM32F103C8T6 board. Ensure the board is operational and has the required drivers installed.
### Software:
1. STM32CubeIDE for code generation and peripheral configuration.
2. STM32Cube HAL (Hardware Abstraction Layer).
3. FreeRTOS, integrated with STM32CubeMX.
### Programming Environment: 
Familiarity with C programming, embedded systems, and FreeRTOS APIs.

## Program Description
The program simulates resource contention in a multitasking environment:
### Tasks:
1. redLEDTask: Toggles the red LED and simulates access to a shared resource.
2. greenLEDTask: Toggles the green LED with a different delay, accessing the same shared resource.
3. orangeLEDTask: Continuously toggles the orange LED without accessing shared resources.
### Shared Resource Management:
The AccessSharedData() function demonstrates a shared resource that both redLEDTask and greenLEDTask attempt to use. Critical sections are protected using FreeRTOS APIs (taskENTER_CRITICAL() and taskEXIT_CRITICAL()).
### Delay Mechanism:
The SimulateReadWriteOperation() function emulates resource usage time with a precise loop-based delay.

## How to Run
### Hardware Setup:
- Connect every LED to the STM32F1 board. You can use the available pins on stm32f1. Here I use pin PA11 for RED LED, PA10 for BLUE LED, PA9 for GREEN LED, and PA8 for ORANGE LED, where the pins are connected to the positive side of the LED. While the negative side of the LED is connected to Ground (GND). And then connect the STM32F1 board to your computer via USB.
### Code Generation:
- Open STM32CubeIDE and load the provided .ioc file.
- Ensure the GPIO pins for LEDs and middleware (FreeRTOS) are configured as follows:
  1. SYS
     <img width="578" alt="sys" src="https://github.com/user-attachments/assets/566d21cc-be8c-4369-aa2d-467de1df3624">
  2. Pin Configuration   
  
- Generate the project files for your IDE.
### Build and Deploy:
- Import the generated project into your IDE.
- Add the application code (main program provided above).
- Compile the project and flash it to the STM32 board.
### Observe Behavior:
- LEDs will toggle according to their tasks.

## Project Files
- main.c: Contains the primary application code, task definitions, and shared resource functions.
- STM32CubeIDE.ioc: Configuration file for STM32CubeIDE.
- FreeRTOSConfig.h: Configuration for FreeRTOS parameters.
