
1. **Control Flow and Conditional Logic**
  **Brief Program Workflow**
  Prompt User for Input:
  
  Displays "Enter a number:" to the user using the sys_write syscall.
  Read Input:
  
  Reads up to 16 bytes of user input into a buffer using the sys_read syscall.
  Classify Input:
  
  Empty Input: If the input is a newline, print "INVALID INPUT."
  Zero ('0'): If the first character is '0', print "ZERO."
  Negative Number: If the first character is '-' and the next character is a digit, print "NEGATIVE."
  Positive Number: If the first character is between '1' and '9', print "POSITIVE."
  Invalid Input: If none of these cases match, print "INVALID INPUT."
  Output Result:
  
  Displays the classification result using sys_write.
  Terminate Program:
  
  Exits the program gracefully with sys_exit.

  **Challenges**
  Multi-Digit Input Handling:

    The program doesn't fully process multi-digit numbers. For example:
    Input 123 will classify as POSITIVE because it only checks the first character ('1').
    A more comprehensive parsing logic would be needed for multi-digit input.

**How to Run**
# Assemble the program
nasm -f elf64 control_flow.asm -o control_flow.o

# Link the object file to create the executable
ld -o control_flow control_flow.o

# Run the program
./control_flow
  
  
2.  **Array Manipulation with Looping and Reversal**

**Program Overview**
Prompt User for Input:

Displays a message prompting the user to enter five single digits separated by spaces.
Read Input:

Accepts up to 16 characters from the user into a buffer (input).
Parse Input:

Iterates through the input buffer to extract valid digits ('0' to '9').
Valid digits are stored sequentially in the array. Non-digit characters are ignored.
If fewer than 5 digits are extracted, the program restarts with an "Invalid input" message.
Reverse Array:

Swaps elements in the array from the two ends toward the middle using a loop, reversing the order in place without additional memory.
Print Array:

Iterates through the reversed array and prints each character, followed by a newline.
Handle Errors:

Invalid input (fewer than 5 digits) triggers an error message and restarts the input loop.
Exit:

Once the reversed array is printed, the program exits gracefully.

**Challenges**
Direct manipulation of memory (e.g., swapping elements during reversal) requires careful index management to avoid buffer overflows or invalid memory access.

**How to run**
# Assemble the program
nasm -f elf64 array_reverse.asm -o array_reverse.o

# Link the object file to create the executable
ld -o array_reverse array_reverse.o

# Run the program
./array_reverse

3. **Modular Program with Subroutines for Factorial Calculation**

**Program Overview**

Display Prompt:

The program first displays a prompt to the user asking them to input a number between 0 and 12 using sys_write.
Read User Input:

The program reads the user's input from stdin using sys_read, storing it in input_buffer.
Convert Input to Integer:

The program converts the ASCII input (e.g., "5") to an integer using the atoi subroutine. The result is stored in the rax register.
Input Validation:

The input is validated to ensure it's between 0 and 12. If it's not, an error message is displayed, and the program exits.
Factorial Calculation:

The program then calculates the factorial of the number by calling the factorial subroutine. The result is returned in rax.
Convert Result to String:

The itoa subroutine is used to convert the integer result of the factorial calculation back into a string.
Display Result:

The program displays the result message ("Factorial is: ") followed by the calculated factorial using sys_write.
Exit Program:

The program exits with sys_exit.

**Challenges**
Factorials grow very quickly. For instance, 13! is a large number (6,227,020,800). The program restricts input to 0-12, but if this restriction were lifted, handling very large numbers (larger than what can fit in a 64-bit register) would require additional logic.

**How to Run**
# Assemble the program
nasm -f elf64 factorial.asm -o factorial.o

# Link the object file to create the executable
ld -o factorial factorial.o

# Run the program
./factorial

4. **Data Monitoring and Control Using Port-Based Simulation**

**Program Overview**
Prompt and Read Input: The program prompts the user to input a sensor value and reads it into a buffer.
Convert Input: The input (a string) is converted to an integer using the atoi subroutine.
Sensor Evaluation: The program compares the sensor value to predefined thresholds:
If the value is above 80 (HIGH_LEVEL), both the motor and alarm are ON.
If between 50 and 80 (MODERATE_LEVEL), both are OFF.
If below 50, the motor is ON and the alarm is OFF.
Display Status: It displays the motor and alarm status (ON or OFF) based on the evaluation.
Exit: The program exits after displaying the statuses.

**Challenges**
The atoi subroutine assumes well-formed input (digits and optional newline). Any unexpected characters (such as letters or special symbols) can cause incorrect results or undefined behavior.

**How to run**
# Assemble the program
nasm -f elf64 port_control.asm -o port_control.o

# Link the object file to create the executable
ld -o port_control port_control.o

# Run the program
./port_control
