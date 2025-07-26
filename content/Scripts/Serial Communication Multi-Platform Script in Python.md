
Code for using serial write to any USB UART device.
requires the s_searcher.py to find what OS is being used, either windows or Linux/android
afterwards the serialcomm.py is a simple GUI with the option to send data in UART.

# s_searcher.py
```python
import os
import time
if os.name == "nt":  # Windows
    import serial
    import serial.tools.list_ports
elif os.name == "posix":  # Linux/Android
    from usb4a import usb
    from usbserial4a import serial4a


def send_data_windows(data):
    """Send data using pyserial on Windows."""
    ports = serial.tools.list_ports.comports()
    if not ports:
        print("No serial ports found.")
        return

    selected_port = ports[0].device
    print(f"Using port: {selected_port}")

    baudrate = 115200
    bytesize = serial.EIGHTBITS
    parity = serial.PARITY_NONE
    stopbits = serial.STOPBITS_ONE
    timeout = 3

    try:
        with serial.Serial(selected_port, baudrate, bytesize, parity, stopbits, timeout=timeout) as ser:
            ser.write(data.encode())  # Send data
            print(f"Sent: {data}")
    except Exception as e:
        print(f"Error: {e}")


def send_data_linux_android(data):
    """Send data using usb4a and usbserial4a on Linux/Android."""
    usb_device_list = usb.get_usb_device_list()
    if not usb_device_list:
        print("No USB devices found.")
        return

    device_name = usb_device_list[0].getDeviceName()
    print(f"Using USB device: {device_name}")

    try:
        serial_port = serial4a.get_serial_port(device_name, 115200, 8, "N", 1)
        if serial_port and serial_port.is_open:
            serial_port.write(data.encode())  # Send data
            print(f"Sent: {data}")
            serial_port.close()
    except Exception as e:
        print(f"Error: {e}")


def send_data(data):
    """Send data based on the detected OS."""
    if os.name == "nt":  # Windows
        send_data_windows(data)
        time.sleep(0.1)
    elif os.name == "posix":  # Linux/Android
        send_data_linux_android(data)
        time.sleep(0.1)
    else:
        print("Unsupported platform!")
```

# serialcomm.py
```python
import tkinter as tk
import s_searcher

# Function to send "11111111"
def send_ones():
    s_searcher.send_data("11111111")

# Function to send "00000000"
def send_zeros():
    s_searcher.send_data("00000000")

# Create the Tkinter GUI
root = tk.Tk()
root.title("Serial Sender")

# Create buttons
button_ones = tk.Button(root, text='Send "11111111"', command=send_ones, width=20, height=2)
button_ones.pack(pady=10)

button_zeros = tk.Button(root, text='Send "00000000"', command=send_zeros, width=20, height=2)
button_zeros.pack(pady=10)

# Run the GUI
root.mainloop()
```

for testing, I used a RP2040 with a built-in USB to send data, if I got the data "11111111" the RP2040 would turn on it built-in LED

# UART_MICRO.py
```python
import machine
import sys
import select

#pins = [machine.Pin(i,machine.Pin.OUT) for i in range(2,10)]
uart =machine.UART(0, baudrate=115200)
uart.init(115200,bits=8, parity=None, stop=1, timeout=3000)

led = machine.Pin(25, machine.Pin.OUT)

def check_input():
    while True:
        if sys.stdin in select.select([sys.stdin], [], [], 0)[0]:
            user_input = sys.stdin.read(8)
            if user_input.strip() == "11111111":
                led.value(1)
            else:
                led.value(0)

check_input()
```