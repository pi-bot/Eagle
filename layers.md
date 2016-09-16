# Eagle Layers

Layers are seperate overlays that together make up a complete design.  **Layer 1** in Eagle represents the top copper layer of the pcb whilst **layer 16** represents the bottom. When routing traces in Eagle on a two layer board you'll be effecting these two layers. 
Fundamental layers used in eagle are:
- 21 **tPlace**
- 44 **Drills** 
- 45 **Holes** 
- 46 **Milling** 

[LIST OF STANDARD LAYERS AND WHAT THEY DO]


As with routing many tools work on specific layers in particular. For example the **line tool** will effect **tPlace(21)** that will be rendered as the silk screen on your PCBs (the printed text/lines/shapes we see). Lines are also used for **tDocu(51)** for drawing the mechanical dimensions of your part for example. 

When assigning **Names** (e.g. C1, R5, X2 etc) and **Values** (e.g. 10K, 0.1µF, AT86RF212) to packages in the Schematics editor text is output to the **tNames(21)** and **tValues(27)** layers respectively. 

Any library part place into your design is likely to effect multiple layers. 


### Documenting your designs.
Just as with effective coding it is usefull to add comments and notes to your designs.  There are appropriate layers for this:
- 47 **Measures** Dimension Labels 
- 48 **Document** Documentation for the board - printed. 
- 49 **Reference** Alignment reference marks for component placements etc.
- 51/52 **tDocument/bDocument** Documentation for the board - not printed. 
- 

See:https://learn.adafruit.com/ktowns-ultimate-creating-parts-in-eagle-tutorial


## Layer use in Schematic view and Layout View
Whats the difference?
I wnat to place headers and notes in the Schematics editor.  What layer should that be on?


