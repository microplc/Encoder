# Encoder Library

对脉冲进行计数从正交编码器信号，一般来自于旋转旋钮，电机或轴传感器和其他位置传感器。
编码器提供 4X 计数模式，针对Arduino板高度优化代码。

编码器有 2 个信号引脚，有三种接法：
最佳性能: 两个信号都连接到中断引脚
一般性能: 第一个引脚接入中断脚，第二个接入非中断脚
较低性能: 两个信号都接入非中断脚

低成本的编码器Low cost encoders only connect their pins to ground. Encoder will activate the on-chip pullup resistors. If you connect lengthy wires, adding 1K pullup resistors may provide a better signal.

http://www.pjrc.com/teensy/td_libs_Encoder.html

http://www.youtube.com/watch?v=2puhIong-cs

![Encoder Knobs Demo](http://www.pjrc.com/teensy/td_libs_Encoder_1.jpg)
