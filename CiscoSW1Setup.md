# How to Console into a Cisco Switch Using Linux Mint 

## Requirements
- Cisco switch
- Console cable (RJ-45 to DB-9 or USB to RJ-45)
- Terminal emulator (e.g., `minicom` or `screen`)

## Steps

1. **Connect the Console Cable**
    - Connect the RJ-45 end of the console cable to the console port on the Cisco switch.
    - Connect the other end of the console cable to your computer's serial port or USB-to-serial adapter.

2. **Identify the Serial Port**
    - Open a terminal on your Linux Mint machine.    
    - Run the following command to locate the dev directory and change into that directory :
      ```
      ls
      cd dev
      
      ```
    - Look for the output that corresponds to your serial device (e.g., `/dev/ttyUSB0`).
![cisco switch](https://github.com/user-attachments/assets/3d5d2946-ef8b-4747-b428-af626b472700)

3. **Install a Terminal Emulator**
    - If you don't have a terminal emulator installed, you can install `putty` or `screen`:
      ```bash
      sudo apt-get install putty
      ```
      or
      ```bash
      sudo apt-get install screen
      ```

4. **Configure and Start the Terminal Emulator**
    - Using `putty`:
   Type putty into your terminal and it will open up the third party app in another screen
      ```bash
      putty
      ```
      - Navigate to "Serial port setup" and configure the following settings:
         - Select Serial Device: `/dev/ttyUSB0` (or your identified serial port)
         - Paste the output from the previous step (ttyUSB0) next to /dev/
         - Click on open
    ![image](https://github.com/user-attachments/assets/1c325dfb-205d-406c-85f3-8f8d99b10469)


5. **Access the Cisco Switch**
    - You should now see the console output from the Cisco switch.
    - Press `Enter` to get the switch prompt.
      
    ![image](https://github.com/user-attachments/assets/2368ecc3-8ab8-4af7-a85d-c115b78377f1)

 Make sure you press enter or it won't start up the terminal! :) 

6. **Exit the Terminal Emulator**
    - To exit `minicom`, press `Ctrl+A` followed by `X`.
    - To exit `screen`, press `Ctrl+A` followed by `\`.

## Troubleshooting
- Ensure the console cable is securely connected.
- Verify the correct serial port is being used.
- Check the terminal emulator settings for correct baud rate and flow control.
