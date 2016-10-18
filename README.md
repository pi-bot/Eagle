# Eagle
Eagle Resources for the PiBot

## Component List Conventions

- U = chip or integrated circuit
- S = Switch
- R = Resistor
- C = Capacitor
- D = Diode
- F = Fuse
- H = Header connector
- J = connector
- L = inductor or LED
- X = crystal

### Other conventions not used:
- B = battery
- K = relay
- Q = transistor
- T = transformer
- V = varistor / MOV
-BR = Bridge Rectifier
- M = MOSFET
- J = jack (connector)
- P = plug


##More Tips

Heres a good guide here: http://dangerousprototypes.com/docs/Cadsoft_Eagle_tips_and_tricks

Also here: 
http://www.lucidarme.me/?p=2363


When making a new symbol, to place a bar over a signal name use the "!" character and a bar will be placed over the following characters. (ie. !EN) To terminate a bar in the middle of a signal name use another "!". (ie. !WR!/RD)


Always do the schematic and symbols in Imperial units because most libraries are in Imperial units. Do the board and packages in either Imperial or Metric depending on whats most appropropriate for the footprint.


## pin direction
Use **SUPPLY**  only for symbols meant to indicate a supply net in aschematic, like for a ground symbol.  Use **POWER** for power and ground pins of a IC. 
https://www.element14.com/community/thread/15253/l/pin-direction?displayFullThread=true


##Filling and unfilling board pours
Clicking hte **ratsnest** butten will fillouot all pours on the pcbs ground or other planes. Its sometimes usefull to remove this to see better what is going on with the board.  This can be done with this command:
```
RIPUP @;
```
Another problem I faced was closing the sheets menu and getting it back. Here's a good guide to the userinterface.
http://www.computeraideddesignguide.com/schematic-options-menus-eagle-pcb-tutorial/

I found controls under **options>GUI options>Sheet tabs**

## Working with and saving Libraries 
The installation of Eagle comes with a large number of default libraries. Its not clear what each library is for and in my view its better to learn and work with a much simpler clearly labelled set.  To do this I've put all the default libraries in a lbr-default folder and then the libraries I need for my projects in the root library directory.

A common workflow when starting out is to first work on a project and then find or create parts to complete a project design. When I did this I found some parts on libraries online, a few from the default libraries and some parts I needed to make myself.  Once complete it then makes sense to consolodate the parts for a project in one library and there are useful **ULPs** for this.  

####Half a solution available
In **File>Export>Librairies** You can see a shortcut to a **ULP** that resaves all the devices for the open project into a single library. The problem is that all the devices in the project will still be linked to their original libraries. The **replace** tool can be used to replace a part with its new version in the new library however doing this manually for each device may be a big job.  Thankfully there is another **ULP** that can be used to automate the replacing of parts to the newly created library. In fact its best to use the altermative **ULP** from the outset and let it both generate the library and reassociate the devices. 

The ULP is from Bob Starr and can be found [here](https://github.com/robertstarr/ulp_user/blob/master/exp-lbrs-replace.ulp)

I recommend you download and use this over the default Eagle one!
