# Python Port Scanner

This is a simple python script that scans port of a specific machine. This is used for educational purposes only. Please don't execute a port scanner against any website or IP address without explicit, written permission from the owner of the server or computer that you are targeting.

## Prerequisites

In order to run the python script, your system must have the following programs/packages installed
* Python 3.8: Download it from https://www.python.org/downloads

## Approach
* First need to clone this respiratory
* Run python script script.py using py script.py in the terminal
* The script will ask you to enter the ip address.
* The script will execute and show you the open ports.

## Code
```
import socket
import time
import threading
from queue import Queue

#Author @inforkgodara

socket.setdefaulttimeout(0.25)
lock = threading.Lock()

ip_address = input('IP Address: ')
host = socket.gethostbyname(ip_address)
print ('Scanning on IP Address: ', host)

def scan(port):
   sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
   try:
      con = sock.connect((host, port))
      with lock:
         print(port, 'is open')
      con.close()
   except:
      pass

def execute():
   while True:
      worker = queue.get()
      scan(worker)
      queue.task_done()
      
queue = Queue()
start_time = time.time()
   
for x in range(100):
   thread = threading.Thread(target = execute)
   thread.daemon = True
   thread.start()
   
for worker in range(1, 500):
   queue.put(worker)
   
queue.join()

print('Time taken:', time.time() - start_time)
```
