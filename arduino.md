setup 只运行一次

loop 循环运行

GND接地接口，要连接

RESET复位键

A0~A5 模拟输入输出

0-13  数字输入/输出引脚

PWM功能

13连接到LED灯

PWM信号高到低(500Hz)，用于直流电机的速度控制，led光控等

**设置引脚**

pinMode(引脚吗，output/input)

**数字输入/输出**

digitalwrite(引脚吗，high/low)    输出

变量=digitalRead(引脚名)              输入

**模拟输入/输出**

analogWrite(引脚吗，0~255)      输出      0~255  -----     

变量=analogRead(引脚名)J          输入



L298N

OUTPUT1  A+ 电机正极

OUTPUT2 A-  电机负极

....

+12V  GND   +5V

电机电源   GND  芯片电源

*双轴电机   驱动

*单轴           风扇

要拆掉减速块

+12v--电池

+5V  UNO板供电

输入引脚、使能引脚

IN                   EN

向右转——左侧启用电机

向左转——右侧启用

继电器                              接风扇

VCC:弱电电路正极 5V

GND   弱电电路负极

IN      弱电电路信号引脚

COM     强电电路的公共极

NC         不通电时NC与COM接通,通电时断开

NO        通电时NO与COM接通,不通电时断开

可以调用delay()函数用于延迟

delay(毫秒)

1s-1000ms

蓝牙模块介绍

VCC-----正极5V

GND---模块供电负极

RXD:接收端，接arduino的TX

TXD:发送端，接arduino的RX

蓝牙接受手机信号——发给arduino板——驱动电机

serial.begin()   打开串口，设置波特率为9600

loop函数中要检查串口是否打开

打开时，serial.available()=1

否则=0

串口读取

serial.read()    (输入字符型变量，char c=serial.read())

串口监视器上打印

serial.println(变量名)

蓝牙监视器注意事项

携带数据信号的信号单元称为码元

每秒钟通过信道传输的码元数成为波特率，若串口波特率与信号波特率不一致，则无法工作

写入arduino时要断开与蓝牙相连的RX，因为arduino与电脑和蓝牙模块通讯都是用RX/TX串口

蓝牙的默认密码是0000或1234

红外传感模块

V+   供电正极

G:供电负极 

S:信号端









规则

时间限制  3分钟

W