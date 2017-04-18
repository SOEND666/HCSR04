# HCSR04
about how to ues python to control HC-SR04 on pi


import RPi.GPIO as io
import time
import client   #引入之前编的clientsocket
def Init():
    io.setmode(io.BCM)
    io.setup(2,io.OUT)
    io.setup(3,io.IN)
    time.sleep(2)
    io.setwarnings(False)
def readvalue():
    io.output(2,io.HIGH)
    time.sleep(0.000015)
    io.output(2,io.LOW)
    while not io.input(3):   #当没输出高电平
        pass
    timestart = time.time()   #记下没输出高电平的时刻
    while io.input(3): #wait  #当输出高电平
        pass

    return (time.time()-timestart) * 340 /2   #算出距离

#main
Init()   #初始化
while True:
    long1 = readvalue()
    client.sen(long1)
    print("distance value :%0.4f M" % long1)
    time.sleep(0.5)
