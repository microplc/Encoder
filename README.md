# Encoder Library

对脉冲进行计数从正交编码器信号，一般来自于旋转旋钮，电机或轴传感器和其他位置传感器。
编码器提供 4X 计数模式，针对Arduino板高度优化代码。

编码器有 2 个信号引脚，有三种接法：
最佳性能: 两个信号都连接到中断引脚
一般性能: 第一个引脚接入中断脚，第二个接入非中断脚
较低性能: 两个信号都接入非中断脚

低成本的编码器仅仅是把他们的引脚接地，工作时需要激活片内上拉电阻，如果你连接线较长，添加一个1K上拉电阻会提供较高质量的信号。

基本用法：
Encoder myEnc(pin1, pin2);
使用两个引脚创建编码器对象，可以创建多个编码器对象，每个有自己的2个引脚。

myEnc.read();
返回积累的位置，正或负。

myEnc.write(newPosition);
设置积累的位置为新的数值。

理解编码器信号：
![Encoder Knobs Demo](https://www.pjrc.com/teensy/td_libs_Encoder_pos1.png)
编码器库监控2个引脚并根据相关的变化更新位置数值，库更新计数在每一个变化，被称为4X计数是因为每个物理或硬件上面的标记或孔会有4次计数。

中断延迟需求：
编码器需要低延时的信号变化响应，一个引脚或两个引脚都是中断脚工作起来都很好，但是如果中断被长时间禁止，无论谁写的代码谁的库函数都会丢失信号变化。结果都是不准确的计数，下面的1，2或3个信号变化都会计数错误。

优化中断选项：
当用于 Arduino，编码器使用优化的汇编语句。一般情况下，编码器使用 attachInterrupt()允许动态触发每一个中断处理，动态函数调用会增加少量开销。为了消除这种额外开销，可以使用如下选项使编码器使用更优化的代码：
// 必须在 Encoder.h 被包含之前定义
#define ENCODER_OPTIMIZE_INTERRUPTS
#include <Encoder.h>
这样编码器被直接定义为最小开销，缺点是与你其他代码或库调用 attachInterrupt() 产生冲突。最高速度和CPU开销测试的结果如下：同一个板子，一般最高100KHz，使用ENCODER_OPTIMIZE_INTERRUPTS选项优化后可以达到127KHz。
           
低性能的轮询模式：
没有中断脚编码器也可以工作，信号只是在每次使用 read() 函数时进行检查。调用 read() 的频率越快，越容易获得准确的结果。此种轮询模式用于低速低精度的码盘或旋钮，或由人手拧动情况下是可以使用的。连接电机轴的高分辨率编码器一般必须使用中断。

注意：使用 Arduino Uno, Duemilanove or Mega 板，其 Serial.print() 可能会引发一些问题。 Arduino 1.0 由于提供了数据传送机制，工作会优于 Arduino 0023 甚至更早的版本。无论哪个版本，高波特率和减少发送数据量都很有帮助。

http://www.pjrc.com/teensy/td_libs_Encoder.html          这个网站有很多可借鉴的内容。

http://www.youtube.com/watch?v=2puhIong-cs

![Encoder Knobs Demo](http://www.pjrc.com/teensy/td_libs_Encoder_1.jpg)
