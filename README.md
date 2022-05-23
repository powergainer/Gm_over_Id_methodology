# Gm over Id methodology
An overview of Gm over Id methodology.

## Why gm controls the speed
From the simple small signal model of a MOSFET (just gm and ro) we calculate Av as vout/vin and we get Av = gm * ro.

Then we calculate the BW, to do that we just put in a load cap CL (we don't even consider device caps), so that gives a simple RC circuit, simple Low Pass filter with one pole given by 1/ro * CL, in this basic single pole system the bandwidth is equal to the pole.

Then we multiply Av * BW to get the Gain-Bandwidth product (this is the same we do in amplifiers where we obtain the unity gain frequency omega_u = Ao * |p1|).

At that point we see that ro cancels out so the only thing that defines GBW is gm.

GBW is what defines speed (responsiveness) of the circuit when we apply negative feedback.

So that's why at the end of the day gm is what defines speed.

![image](https://user-images.githubusercontent.com/95447782/169857997-3428e288-4a72-4d3d-8e8d-21f6f9242d05.png)


## gm also controls the noise
MOSFET thermal noise (input referred noise of the device) ends up being proportional to the INVERSE of gm.

So, more gm less noise.

![image](https://user-images.githubusercontent.com/95447782/169858135-e84d9715-69b5-4bc3-a7c7-8cbc2140d25d.png)

## Motivation for a gm/Id methodology

First, let's define the concept of Transistor Efficiency, TE, as the ratio between gm and the bias current that we need to burn in order to get that gm.

![image](https://user-images.githubusercontent.com/95447782/169858303-a97b762e-cda7-4eb5-bb05-5dca062a0964.png)


### Why a gm/Ic methodology didn't make sense for BJTs

In the BJT the TE (transistor efficiency = gm/Iq) is CONSTANT, regardless of what Ic you give it. Low or high, it doesn't matter. **Your gm/Ic is CONSTANT in the BJT.**

![image](https://user-images.githubusercontent.com/95447782/169858435-94b3e368-41c0-40cf-900a-f0cca1eac66b.png)

For the BJT there is no gm/Id methodology because the TE is CONSTANT. So in the BJT days no one talked about gm/Id methodology.

For the BJT, since the Ic is an exponential of VBE, the LOG (LN) of the Ic is proportional to VBE.

Now, if you differentate the LOG of the Ic with respect to VBE, you get 1/Vt which is the same as gm/Ic we got before.

![image](https://user-images.githubusercontent.com/95447782/169858477-7812e4ee-71e5-452a-81f0-4fec588c1267.png)

We simply OBSERVE THE FACT that the SLOPE OF THE LOGARITHMIC VERSION OF THE CURRENT HAPPENS TO BOIL DOWN TO THE SAME VALUE AS THE GM/ID.

And therefore we say **TRANSISTOR EFFICIENCY TE IS (PROPORTIONAL TO) THE SLOPE OF THE LOGARITHMIC VERSION OF THE CURRENT**.

Later on we will use this PROPERTY as a TOOL, simply because it's HANDY to know that we can PLOT THE CURRENT IN LOGARITHMIC SCALE (i.e. plot the LOG of the Id) VERSUS VGS, LOOK AT THE SLOPE OF THAT, AND THE SLOPE OF THAT GRAPH IS THE GM/ID.

Overall, 
* **the SLOPE OF THE CURRENT (VERSUS VGS) IS GM**
* **the SLOPE OF THE LOGARITHM OF THE CURRENT (VERSUS VGS ALSO) IS "PROPORTIONAL" TO GM/ID** (so it's not the exact gm/Id value but it's an indication of BIG gm/Id or SMALL gm/Id, which is that same as BIG TE or SMALL TE).

At the end of the day what matters here is: **in the BJT the TE is CONSTANT so no point in a gm/Ic methodology for BJTs.**


## The MOSFET

This is the OLD-SCHOOL MOSFET MODEL, LONG CHANNEL MOSFET model:
* NMOS channel is the **INVERSION LAYER**. Substrate is p-type (if it's an NMOS) but it "becomes" n-type due to the attracted electrons which form the channel.
* **The INVERSION LAYER starts to form when VGS > VTH (channel formation, conduction starts, OFF to ON).**
* Where VTH is any thing from 0.3V to 1V.
* When VGS is larger than VTH (conduction) we say **VGS is equal to VTH + some overdrive (Vov)**.
* If you keep increasing VGS for a constant VD OR if you increase VDS too much, you reach the point where you PINCH-OFF the channel.
* The **PINCH-OFF happens IF VGD VTH** (like not enough "VGD" to form a channel at the Drain edge). And that's the **start of the SATURATION REGION**. If you do a tiny bit of math you see that **the condition for Saturation VGD VTH is the same as saying that VDS >= Vov**.
* Finally, once we are in SATURATION the drain current is given by the SQUARE LAW:


<img src="https://render.githubusercontent.com/render/math?math=$I_D =\frac{\mu_n C_{\mathrm{ox}} }{2}\frac{W}{L}{\left(V_{\mathrm{GS}} -V_{\mathrm{TH}} \right)}^2 =\frac{\mu_n C_{\mathrm{ox}} }{2}\frac{W}{L}V_{\mathrm{ov}}^2$">


![image](https://user-images.githubusercontent.com/95447782/169861605-d82edce8-8922-468b-81a2-ac677d864df0.png)


But the problem with this model is that it's not very good for SHORT CHANNEL MOSFETs.

See that the SQUARE LAW fits quite well the actual characteristic for the LONG CHANNEL device (blue curve).

But the SQUARE LAW does NOT fit well the actual characteristic of the SHORT CHANNEL device (red curve).

![image](https://user-images.githubusercontent.com/95447782/169862807-c7a3cd2f-28c3-4d06-b89f-075cccb704c5.png)

If we look at the gm, again we see the gm predicted by the SQUARE LAW fits (relatively) well the LONG CHANNEL device but it does NOT fit well the actual gm of a SHORT CHANNEL device.

Notice how gm is supposed to grow linearly with VGS-VTH which is the Vov. In the LONG CHANNEL device that's a good approximation, more overdrive gives more gm, approximately linearly. **But not in the SHORT CHANNEL one, there as you increase the overdrive the gm flattens off, it stops growing linearly so you can't get more gm by just overdriving it more.**

Notice that **the "PROBLEM" is at high Overdrive (STRONG INVERSION).** At the beginning (low Overdrive, WEAK INVERSION) the Square Law works more or less, **it's at STRONG INVERSION where it starts to fail for the SHORT CHANNEL one.**


![image](https://user-images.githubusercontent.com/95447782/169866635-2a16c1d3-9a80-45ba-981a-ee66136a897b.png)

The causes for this are:

* Short channel effects (velocity saturation, mobility degradation, etc)
* In strong inversion, short channel, Id is no longer quadratic with V overdrive, but it's more like linear (gm saturates at large Vov)

Overall, we have that:
* **SQUARE LAW FAILS TO DESCRIBE THE SHORT CHANNEL DEVICE IN STRONG INVERSION **


So:

* In the **SHORT CHANNEL MOSFET**, due to short channel effects, the **SQUARE LAW stops working at STRONG INVERSION**.
* For the SHORT CHANNEL, in STRONG INVERSION, the CURRENT is NO LONGER SQUARE, IT BECOMES MORE LIKE LINEAR GROWTH WITH Vov.
* Since gm is just the slope:
* For the **SHORT CHANNEL MOSFET in STRONG INVERSION, the GM is NO LONGER GROWING LINEARLY, IT BECOMES FLAT, CONSTANT OR SATURATED AT LARGE Vov**.

Now, what happens with gm/Id ratio for the SHORT CHANNEL device?

And by what happens we mean, does the SQUARE LAW PREDICT a dependency of gm/Id versus VGS that really matches the actual characteristic of the device in real life?

Starting from the SQUARE LAW expression of Id, we are "supposed" to get a gm/Id dependency of VGS that is INVERSE function of gm/Id versus VGS.

![image](https://user-images.githubusercontent.com/95447782/169869264-9a1e5eec-d40a-46ff-a32f-90d7d3f8eb36.png)


Now let's look at model versus reality:

![image](https://user-images.githubusercontent.com/95447782/169870245-ac68170d-7a52-4878-b9cc-0a9159174a05.png)


Notice how the gm/Id expression that results from the SQUARE LAW

<img src="https://render.githubusercontent.com/render/math?math=$\frac{g_m }{I_D }=\frac{2}{V_{\textrm{ov}} }$">

**predicts that at very low overdrive (weak inversion) we should get HUGE gm/Id values** (HUGE TRANSISTOR EFFICIENCY, nearly infinite) but that's **not the case in reality**.

So, **the SQUARE LAW fails to describe weak-inversion COMPLETELY**, for both LONG and SHORT channel devices.

Remember that for the BJT we got that TE (transistor efficiency, gm/Ic) was CONSTANT no matter what VBE?

For the MOSFET, the TE (transistor efficiency, gm/Id) is NOT constant, it actually DEPENDS ON THE BIAS POINT:

![image](https://user-images.githubusercontent.com/95447782/169871545-55a71119-a7aa-4511-927c-41253a4604b0.png)


Boundary between WI, MI and SI:

* There is no real boundary but just rough values:
* If you have:
* **gm/Id > 20 ==> You are in WI**
* **gm/Id ~ 10 to 20 ==> You are in MI**
* **gm/Id < 10 ==> You are in SI**

![image](https://user-images.githubusercontent.com/95447782/169871770-6489081a-ca58-421d-948d-7f1ff13bcfa3.png)


Actually the value of the **gm/Id TELLS YOU what kind of inversion you have** and what region you are in.

