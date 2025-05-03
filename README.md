# Analog_t12_controller
Simple analog controller for T12 soldering iron with N-channel high side switching transistor 

The original circuit diagram was taken from [here](https://ludens.cl/Electron/T12tempcont/T12tempcont.html), but it uses P-channel MOSFET as a high side switch(like all similar schematics that i found on the internet). This is not really all that surprising, because it is the simplest way to implament high side switch, but that comes with 3 main drawbacks:
- P-channel FETs are not as common as N-channel ones(in fact i could not find any in my junk box, and that was the reason why i decided to mod this circuit);
- P-channel MOSFETs have much higher R(DS)on, and subsequently more loses in form of heat;
- Most P-channel FETs have maximum Gate-source voltage of about ~20V which is too low if you want to use 24V as the input voltage.

However driving N-channel FET in high side configuration is not easy, becouse gate voltage should be at least 10V above the supply voltage(for non-logiclevel MOSFETs), as voltage on gate in referenceto source will subtract from voltage on source in reference to ground. So if we need 10V gate-source voltage in this configuration and supply voltage is 24V we need 34V on gate in reference to ground. And if we ignore this and just apply 24V to gate the transistor will balance itself at a point where G-S voltage is just enough to slightly open it, which results in high R(DS)on and a ton of heat.

The easiest way to achieve this is charge pump:

![cnarge pump OFF](https://github.com/user-attachments/assets/ace0910d-11d8-470d-bf0a-93aa2fbe874d)![PNG](https://github.com/user-attachments/assets/b3e2d268-e4ff-42d3-ad1b-284318987799)

![4](https://github.com/user-attachments/assets/82d32f47-cdfc-4b45-b55d-927af93ad4d2)![5](https://github.com/user-attachments/assets/8319afb1-d2b5-4e2d-b310-a17dccff9ec7)

Ground - gate voltage on the right, gate - source voltage on the left(NO zener diode).

The working principal is fairly simple, when small BJT is ON the gate is pulled low, the electrolytic cap charges via the diode to nearly 24V. When base of the BJT is pulled low the electrolytic cap apples 15V(becouse of 15V zener diode) to the gate, and FET turns on fully. Because gate takes almost no current MOSFET can stay on for long period of time.

As far as the rest of the circuit goes i didn`t change anything else, just added another small decoupling cap near comparator IC, and trim pot to shift temp. range.

Here is the entire circuit diagram([PDF](https://github.com/hopper775/Analog_t12_controller/blob/main/Circuit%20diagram.pdf)):
![вивід](https://github.com/user-attachments/assets/0f3ba72c-7e8d-4554-9f37-8f509f3c6761)

if you want to know how the rest of the circuit works i highly recommend reading [this](https://ludens.cl/Electron/T12tempcont/T12tempcont.html).

From my testing this works perfectly, temprature range in my case is 200 - 470C. As far as constraction goes I put everything together using prototyping board and then stuffed it in enclosure from laptop charger:

![IMG_20250503_214025](https://github.com/user-attachments/assets/905e9b17-89cf-4224-b12b-09f2e522b7e0)
