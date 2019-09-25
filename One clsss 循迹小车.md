   
**

## 记录：

**
  1、`**pinMode();**`**：将指定引脚配置为输入或输出**
 
***参数：*
pin：Arduino引脚号设置模式。
mode：INPUT，OUTPUT，或INPUT_PULLUP**
2、`**analogRead();**`**：从指定的模拟引脚读取值**
***参数*：
pinMode(pin, mode)
analogRead(pin)
pin：要从中读取的模拟输入引脚的名称（大多数板上的A0至A5，MKR板上的A0至A6，Mini和Nano上的A0至A7，Mega上的A0至A15）**
3、`**analogWrite();**`**：将模拟值（PWM wave）写入引脚。可用于以不同的亮度点亮LED或以不同的速度驱动电动机。在调用之后analogWrite()，引脚将产生指定占空比的稳定矩形波，直到下一次调用analogWrite()（或调用digitalRead()或digitalWrite()）在同一引脚上**
***参数*：
analogWrite(pin, value)
pin：要写入的Arduino引脚。允许的数据类型：int。
value：占空比：介于0（始终关闭）和255（始终打开）之间。允许的数据类型：int**
4、  `#include <Servo.h>`**：伺服库，该库可以控制大量的伺服器**

5、`Serial.begin(9600);`**：打开串行端口，将数据速率设置为9600 bps**
6、`**Serial.print();**`**：将数据作为人类可读的ASCII文本打印到串行端口**

   

```
#include <Servo.h>//伺服库
int leftMotor1 = 3;
int leftMotor2 = 4;
int rightMotor1 = 5;
int rightMotor2 = 6;
int sum=0;
void setup() {
Serial.begin(9600);//打开串行端口，将数据速率设置为9600 bps
pinMode(leftMotor1, OUTPUT);
pinMode(leftMotor2, OUTPUT);
pinMode(rightMotor1, OUTPUT);
pinMode(rightMotor2, OUTPUT);
pinMode(A0, INPUT);
pinMode(A1, INPUT);
pinMode(A2, INPUT);
}

void loop()
{
int data[4];
data[0]=analogRead(A0);
data[1]=analogRead(A1);
data[2]=analogRead(A2);

if(data[0]<210&&data[1]>500&&data[2]<210)//向前走
{
analogWrite(3,128);
analogWrite(5,128);
analogWrite(6,128);
analogWrite(4,128);
}
if(data[0]>500 &&data[1]<210 && data[2]<210) // 小车偏左
{
analogWrite(3,128);
analogWrite(5,0);
analogWrite(6,0);
analogWrite(4,0);
}
if(data[0]>500&&data[1]>500&&data[2]<210) //小车偏大左
{
analogWrite(3,0);
analogWrite(5,128);
analogWrite(6,128);
analogWrite(4,0);
}
if(data[0]<210&&(data[1]-30)<210&&data[2]>500) //小车偏右
{
analogWrite(3,0);
analogWrite(5,128);
analogWrite(6,0);
analogWrite(4,0);
}
if(data[0]<210&&data[1]>500&&data[2]>500) //小车偏大右
{
analogWrite(3,0);
analogWrite(5,128);
analogWrite(6,128);
analogWrite(4,0);
}
if(data[0]>500&&data[1]>500&&data[2]>500) //左右都检测到黑线是停止
{
analogWrite(3,0);
analogWrite(5,0);
analogWrite(6,0);
analogWrite(4,0);
}

Serial.print(data[0]);//将数据作为人类可读的ASCII文本打印到串行端口
Serial.print("---");
Serial.print(data[1]-30);
Serial.print("---");
Serial.print(data[2]);
Serial.print("---");
Serial.println(data[3]);//最后一个标签后的回车
}
```

