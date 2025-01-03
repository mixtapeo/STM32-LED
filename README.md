# Introduction  
The aim of this project is to understand the general workflow of working with the STMCubeIDE and configuring board, debug, and miscellaneous settings crucial to any project.  
Inspiration for the project is credited to [Digikey](https://www.digikey.com/en/maker/projects/discovering-the-stm32-cube-ide-a-simple-led-blink-and-gpio-project/58573ed093f4415084de88e03f03ef6d). However, the code they provide is outdated, and the steps are slightly different due to the use of different boards.  
FreeRTOS will be used for task scheduling.  

# Steps

1. **Connect your STM32-L152RE board**, install STMCubeIDE, and set up the environment.  
2. Open the auto-configurator, and select the following:  
   - <b>a.</b> "GPIO\_OUTPUT" on two pins (these will power the LEDs).  
   - <b>b.</b> Search for "EXTI" in the search bar and enable this on the available port.  
     - <b>i.</b> Navigate through the GPIO menu and enable the interrupt.  
     - <b>ii.</b> This allows the blue button's external interrupt on the board to toggle the LED on press.  
3. Navigate to "Middleware" and enable FreeRTOS:  
   - <b>a.</b> Add up to two tasks:  
     - <b>i.</b> One task should have normal priority.  
     - <b>ii.</b> The other task should have below-normal priority to avoid clashing with system tasks.  
   - <b>b. </b>Add a semaphore for the button press:  
     - <b>i.</b> FreeRTOS will arrange for the button press to be communicated to the code at an appropriate time if other tasks (e.g., system tasks) are using the resource.  
     - **Note**: This step can be skipped by using a toggle variable in the code, but using a semaphore is cleaner and more efficient.  
4. Modify the system clock to ensure accuracy:  
   - Navigate to `SYS` and scroll down to change the system clock to "TIM6".  
5. Adjust the NVIC settings as required.  
6. Implement the code:  
   - The code is straightforward and includes the LED toggle functionality.  

```c
// update code
```

# Challenges

1. The system timer being stuck on the base clock after an interrupt caused the STM program to freeze.  
2. For the longest time, I mistakenly pressed the reset (black) button, thinking it was the interrupt button.  
3. Initially, I assigned both tasks very low priority, which worked but wasn't optimal. Task scheduling priority considerations were discovered later.  


This should ensure readability and proper structure in your Markdown document. Let me know if you'd like to further refine any section!
