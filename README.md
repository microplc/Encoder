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


http://www.pjrc.com/teensy/td_libs_Encoder.html

http://www.youtube.com/watch?v=2puhIong-cs

![Encoder Knobs Demo](http://www.pjrc.com/teensy/td_libs_Encoder_1.jpg)
