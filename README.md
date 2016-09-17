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
