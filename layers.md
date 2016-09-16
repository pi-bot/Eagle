# Eagle Layers

Layers are seperate overlays that together make up a complete design.  **Layer 1** in Eagle represents the top copper layer of the pcb whilst **layer 16** represents the bottom. When routing traces in eagle on a two layer board you'll be effecting these two layers. 

A PCB is much more than just the copper though. Examine any PCB and you'll see there' more going on.  Other standard layers include:

[LIST OF STANDARD LAYERS AND WHAT THEY DO]

- 44 Drills 
- 45 Holes 
- 46 Milling 


Any library part place into your design is likely to effect multiple layers. 




### Documenting your designs.
Just as with effective coding it is usefull to add comments and notes to your designs.  There are appropriate layers for this:
- 47 **Measures** Dimension Labels 
- 48 **Document** Documentation for the board - printed. 
- 49 **Reference** Alignment reference marks for component placements etc.
- 51/52 **tDocument/bDocument** Documentation for the board - not printed. 
