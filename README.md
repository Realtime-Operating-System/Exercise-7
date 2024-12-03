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
  #### SYS
  <img width="578" alt="sys" src="https://github.com/user-attachments/assets/566d21cc-be8c-4369-aa2d-467de1df3624">
  
  #### Pin Configuration
  <img width="395" alt="pin" src="https://github.com/user-attachments/assets/1beb6c9d-9fa8-4004-827a-bf3ef38c87f4">
  
  #### FreeRTOS
  <img width="928" alt="freertos" src="https://github.com/user-attachments/assets/c44efd36-a3ea-4e1c-897c-7d2aa88d6ee7">

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

## How It Works?
### redLEDTask
1. Turns on the red LED (HAL_GPIO_WritePin(GPIOA, GPIO_PIN_11, GPIO_PIN_SET)).
2. Enters a critical section (taskENTER_CRITICAL()).
3. Calls the AccessSharedData() function:
   - Checks and modifies the StartFlag variable.
   - Simulates a read/write operation for 1 second using SimulateReadWriteOperation().
   - Turns off the blue LED if it was lit during contention.
4. Exits the critical section (taskEXIT_CRITICAL()).
5. Turns off the red LED.
6. Waits for 550 milliseconds (osDelay(550)) before repeating.
### greenLEDTask
1. Turns on the green LED (HAL_GPIO_WritePin(GPIOA, GPIO_PIN_9, GPIO_PIN_SET)).
2. Enters a critical section (taskENTER_CRITICAL()).
3. Calls the AccessSharedData() function (same behavior as in redLEDTask).
4. Exits the critical section (taskEXIT_CRITICAL()).
5. Turns off the green LED.
6. Waits for 200 milliseconds (osDelay(200)) before repeating.
### orangeLEDTask
1. Toggles the orange LED (HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_8)).
2. Waits for 50 milliseconds (osDelay(50)) before toggling again.

## Demo Video
[Exercise 7](https://github.com/user-attachments/assets/6e049b82-bb28-4653-aa1f-f0b7459ce102)

