# Analog_t12_controller
Simple analog controller for T12 soldering iron with N-channel high side switching transistor 

The original circuit diagram was taken from [here](https://ludens.cl/Electron/T12tempcont/T12tempcont.html), but it uses P-channel MOSFET as a high side switch(like all similar schematics that i found on the internet). This is not really all that surprising, because it is the simplest way to implament high side switch, but that comes with 3 main drawbacks:
- P-channel FETs are not as common as N-channel ones(in fact i could not find any in my junk box, and that was the reason why i decided to mod this circuit);
- P-channel MOSFETs have much higher R(DS)on, and subsequently more loses in form of heat;
- Most P-channel FETs have maximum Gate-source voltage of about ~20V which is too low if you want to use 24V as the input voltage.

However driving N-channel FET in high side configuration is not easy, becouse gate voltage should be at least 10V above the supply voltage(for non-logiclevel MOSFETs). The easiest way to achieve this is charge pump:

![image](https://github.com/user-attachments/assets/df96acc4-cdfe-47f4-bc5b-18e2c244fb46)
