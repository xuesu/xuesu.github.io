#Chapter 3 Operating Systems Security
##Password Salt
- Associate a random number with each userid.
- Rather than comparing the hash of an entered password with a stored hash of a password, the system compares the hash of an entered password and the salt for the associated userid with a stored hash of the password and salt. 
##Buffer Overflow Attacks
[http://www.cse.scu.edu/~tschwarz/coen152_05/Lectures/BufferOverflow.html](http://www.cse.scu.edu/~tschwarz/coen152_05/Lectures/BufferOverflow.html)
In a buffer overflow attack, an attacker provides input that the program  blindly copies to a buffer that is smaller than the input. This commonly occurs, with the use of unchecked  C library functions , such as strcpy（）and gets(), which copy user input without checking its length.
A buffer overflow involving a local variable can cause a program to overwrite memory beyond the buffer’s  allocated space in the stack, which can have dangerous consequences. An example of a program that has a stack buffer overflow vulnerability is shown in the code fragment of the picture. 

