# Chaotic-Pendulum-Encrytion
This is the project page for our Chatoic Pendulum Encrytion system. A driven double pendulum is by nature a chaotic system, meaning it is highly dependent on, and sensitive to initial conditions. The idea behind this project is to utilize this chaos to produce highly variable keys and encrypt data via symmetric stream cypher. We design a pendulum using aluminum, and to detect its motion, we use neodymium magnets and hall effect sensors. To encrypt a message, we collect a series of bytes from the pendulum and use this as our key. 
Since we can collect data very quickly, an encryption of this sort is theoretically very secure where we can make the key the same length as the message. 


<img width="448" alt="Screen Shot 2023-06-01 at 3 34 16 PM" src="https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/81fcaa43-f65b-420c-b719-8bccc97bdfee">


## Table of contents
- [Budget](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#budget)
- [Circuits](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#circuits)
    - [Motor](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#motor-circuit)
    - [Sensor](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#sensor-circuit)
    - [Op-amp](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#op-amp-circuit)
- [Labjack Control and Code](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#labjack-and-code)
- [Pendulum Control](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#control-of-pendulum)
    - [Tests](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#testing-and-changes)
    - [Randomness](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#randomness)
- [Sensor Data](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#sensor-data)
- [Results](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#results)
    - [Examples](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#examples)
- [Conclusion](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/blob/main/README.md#conclusion)


## Budget

| Part  | Quantity | Cost |
| ------------- | ------------- | ------------- |
| DC Gear Motor  | 3  | $44.97 |
| Aluminium Rods  | 6  | Third Header |
| Flanged Ball Bearings  | 5  | $36.91 |
| Bolts  | 20  | $11.50 |
| Screws  | 25  | $11. |
| Hall Effect Sensors  | 20  | $8.04 |
| Neodymium Magnets  | 18  | $7.82 |
| H-Bridge  | 5  | $11.5 |
| Solenoids  | 3  | $29.97 |




## Circuits 
For the setup we used three circuits, one to run the motor, another for the op-amp, and a third to connect three to four the sensors. 

### Motor circuit 

Using a DRV8833 motor driver we connect a 12V, 100RPM DC motor, this is then connected to a standard DC power supply.

Circuit Diagram             |  Physical
:-------------------------:|:-------------------------:
<img width="974" alt="Screen Shot 2023-05-15 at 5 27 41 PM" src="https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/761e181d-c835-4561-83f3-1964c36d5877">  |  <img width="380" alt="Screen Shot 2023-06-07 at 1 44 44 PM" src="https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/dfcd8c5d-4844-43e7-b7f6-bded4390f2a8">




### Sensor Circuit

Circuit Diagram             |  Physical
:-------------------------:|:-------------------------:
![circuit](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/f747b40a-b0e2-493b-96f8-a94cdae36696)  |  <img width="408" alt="Screen Shot 2023-06-07 at 1 44 36 PM" src="https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/2656bd21-4531-4f47-8fe4-42e9d1a0d6fb">



### Op-Amp Circuit

Linear Hall Effect Sensors are connect in a circuit with an op-amp


Circuit Diagram             |  Physical
:-------------------------:|:-------------------------:
!<img width="654" alt="Screen Shot 2023-06-07 at 1 05 00 PM" src="https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/d66b2220-7c99-4e32-b2e1-29581b4d6da8">  |  !<img width="596" alt="Screen Shot 2023-06-07 at 1 41 58 PM" src="https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/82695fac-90fd-4860-bd45-9a6716b4b97d">




# Control of Pendulum
We use a LabJack U3-HV and a DC Power Supply to control the motor and collect data. The process begins when a message is given to the program to be encrypted and initial conditions specified. Once the program is run, the pendulum begins oscillating until enough data is collected. 

### Pendulum design

<img width="179" alt="Screen Shot 2023-06-07 at 1 24 21 PM" src="https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/aeddee32-f7ab-49ac-a1ff-a2b2e1b109af">


### Motion

![Untitled design-7](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/7b1fa93a-b0d1-4735-992e-43c29964d53f)

We set up the pendulum on a 3D printed base. For the chaotic regimn, the ideal frequency is 2 Hz, this motion is shown above. The motor oscillates at 6 V, and 0.2 Amp.


![Untitled design-8](https://github.com/vbodenstein/Chaotic-Pendulum-Encrytion/assets/133536500/84e38877-7525-4d6a-bdcd-338ed04f42e3)


Here the pendulum is set to 2.5 Hz, 6 V, 0.2 A. The motion is periodic, as there is not enough energy supplied by the motor to cause divergence. To find these two regimns we tested the pendulum at various frequencies and voltages. These numbers are specific to the our setup.



### Testing and Changes 





### Randomness

There are a few places to look for randomness when looking at the data collected by the sensors.

GRAPHS and analysis of them

Using our knowledge of aproximately where the data is systematic and where it is random, we set a cut





# Encryption Results


### Examples of encryption and decryption: 


### Ex. 1

The data generated by the device:

00010101011010101011010101101010111001010110011110101001110101101110101001000010011001110110100000000100111001100111110011000111010110101001010100100100100110100110011010101001011010101010010010100111111110101010001010001010101001110011001010100100101010011010101010011011000101011010101010011110010110101011101010101011011110010110010110111011010110011000110110100111011011101110101000101011010101000111001010100001110111001010101010101110010101110000010000100110011011101000110101100110001100011011000111100011001000101011010010101011001100000000100010001010011001010101010110100101011110101010001010010100100010001010


This is converted into a key:

\x01V\xabV\xaeVz\x9dn\xa4&v\x80Ng\xccu\xa9RI\xa6j\x96\xaaJ\x7f\xaa(\xaas*J\x9a\xa9\xb1Z\xa9\xe5\xab\xaa\xb7\x96[\xb5\x98\xdav\xee\xa2\xb5G*\x1d\xca\xaa\xe5pBf\xe8\xd6c\x1b\x1e2+J\xb3\x00\x88\xa6UZW\xaa)H\x8a'


Message we gave the system to encrypt:

Against stupidity the Gods themselves contend in vain.


The encrypted data is: b"!\x17\xcc7\xc78\t\xe9N\xd7R\x03\xf0'\x03\xa5\x01\xd0r=\xce\x0f\xb6\xed%\x1b\xd9\x08\xde\x1bO'\xe9\xcc\xdd,\xcc\x96\x8b\xc9\xd8\xf8/\xd0\xf6\xbeV\x87\xcc\x951Kt\xa4\x84" 

The decrypted data is:  Against stupidity the Gods themselves contend in vain.


### Ex. 2

We can compare the normalizad data for the ordered motion vs. the chaotic motion. 

Ordered:
1111110011011100100011100001100111001101110011001101111011001001110011101111111011011110110011001110011011001100111011000100100011001110011011011100110110011

Chaotic:
11000100001010101001010100000000011000101000101010101000001001100010010100100010001101000000110100000000001001000100100000001000100010100000001

Encryption with the chaotic:
The input is: b' hello world' 

The key is: b'b\x15J\x801ET\x13\x12\x91\x1a\x06\x80\x12$\x04E\x01' 

The encrypted data is: b'B}/\xec]*#3e\xfehj\xe4' 

The decrypted data is:  hello world


### Ex. 3 -- plts are labeled with no.4

Ordered:
 
1101110010011100110111001100110011011100100110011000110111001100110011001100110011001100110011010000110010001100110111001100110011001100110011001100110011001
 
Chaotic:

110110010001000001001110101001001001001100001010010011100011000100100010100110101010010001001001010100101010110000101010101001000000010100


Chaotic: 

The input is: b' Abracadabra' 

The key is: b'\x03dA:\x92L)8\xc4\x8aj\x91%J\xb0\xaa\x90\x14' 

The encrypted data is: b'#%#H\xf3/H\\\xa5\xe8\x18\xf0' 

The decrypted data is:  Abracadabra


Ordered:

What do you want to encrypt?Abracadabra
The input is: b'Abracadabra' 

The key is: b'\x1b\x93\x9b\x99\x9b\x931\xb9\x99\x99\x99\x99\xa1\x91\x9b\x99\x99\x99\x99\x99' 

The encrypted data is: b'Z\xf1\xe9\xf8\xf8\xf2U\xd8\xfb\xeb\xf8' 

The decrypted data is: Abracadabra



Notice the repetition in the ordered sequence as apposed to the chaotic sequence for the encrypted data. 

# Conclusion

In this project w
The use of hall effect sensors is not recommended for such a set up, they break very easily and something more reliable would serve much better. 

There is a endless amount of data analysis one can do to find the most randomized keys.

The great thing is that with the chatoic system the key will obvioulsy not be guessed. Hypothetically if we use the sinusoidal wave for encryption we get a string of zeros and ones, which will encrypt the message without problems. Obviously this is not safe since it is very easy to deduce they key. 
