DIY GPS Module for Nikon DSLRs
==============================

Using a GPS Module, most modern Nikon DSLRs are able to automatically geotag
pictures right when taking them. Unfortunately, the official Nikon GP-1 is very
expensive (~200€). In this project I'll try to build an equivalent module using
low-cost components. If everything works out as planned, no microcontroller is
required. Instead, we can attach the GPS module directly to the camera.

**Project Status:**

```
[i] planning, searching for parts
[ ] schematics design
[ ] functional prototype
[ ] PCB design
[ ] housing design

i = in progress, x = done
```


Nikon GPS Port Specs
--------------------

![Connector](connector.jpg)

* Proprietary 8-pin connector,
  [pinout](http://pinoutsguide.com/DigitalCameras/nikon_d90_pinout.shtml)
* Operating voltage: 5V
* GPS pin expects NMEA data via UART
* UART specs: 4800 baud, no parity, 1 stop bit


Required Parts
--------------

* A cable which fits to the prop. connector. Cheapest source: third party cable
  remote triggers (< 10€) which can be cut off at an appropriate length.
* A GPS module, see GPS for more details.
* Housing for the parts, ideally fitting on camera's the hot shoe mount.
* Supporting electronics for voltage regulation etc.


### GPS

I'm still searching for the perfect module. The best one I have found so far
is the Maestro A2235H ([farnell](http://goo.gl/wVIlpc)). At a price of 19€
it's reasonably cheap while featuring an internal antenna as well as perfectly
matching default transmission settings (4800baud UART). That means no
configuration is necessary and we can assemble the unit right away.

One downside of the A2235H is that it needs an explicit low-high signal to
power up the module after power has been supplied. We can either do this
manually (using a push-button) or possibly also automatically ~1s after
plugging the device in.


### Housing

Finding a good housing is always quite difficult if the end product should
look good. It will mostly depend on the PCB which is yet to be determined. 3D
printing might be a good option in order to get a fitting mount for DSLR hot
shoes. For those who don't own a 3D printer (including me), this can be done
e.g. in your local [FabLab](http://en.wikipedia.org/wiki/Fablab) either very
cheaply or usually even for free.


### Supporting Electrocincs

If we use the A2235H, we will have to use a voltage regulator since the module's
operating voltage is at 3.3V. From previous projects, the LP2985-33 low dropout
regulator is cheap, small and easy to use. It can drive up to 150mA which is
more than enough for the GPS module. For the on-off mechanics of the A2235H we
need either a push-button or a simple timer-based circuit that sends an impulse
to the module about a second after the circuit has been powered on.

Additionally, the outgoing data has to be converted from 3.3V module voltage
back to the 5V operating voltage of the camera, since the GPS DATA input port
apparently does not work reliably with 3.3V levels. A simple transistor circuit
might be sufficient here, this will be evaluated in future experiments.

Apart from that we might want to throw in small capcaitors here and there to
dampen noise on the circuit, but that should be pretty much it.


Sources
-------

1. [Peter Miller Photography](http://www.petermillerphoto.com/nikongps/nikongps2.html)
2. [Homepage of Bálint Kis](http://www.k-i-s.org/index.php?item=13)
3. [Pinouts Guide](http://pinoutsguide.com/DigitalCameras/nikon_d90_pinout.shtml)
