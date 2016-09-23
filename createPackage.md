#Automatically creating packages

This will be used to collect code and think through solution initially. I'll then tiddy it up and make it clearer whats its all about.  

The question is how to create a script/system that takes a list characters and returns a package library of the characters in eagle scaled correctly and in a font of your choice.  This involves the character list.

##Character List 
The character list for the PiBot board represent the input and out put pins for the board.
```
1
2
3
4
5
```

We put our list is a **CHARS-[libName].txt** file.  This list is then a source variable to drive the whole system. **CHARS-** is given as a convention for the generated Eagle package Library.  The completed Eagle Library will therefore be named: **CHARS-[libName].lbr **.  For our example project we'll call our character list **CHARS-PIBOT.txt** that will be used to create an Eagle **CHARS-PIBOT.lbr** package library. 

##System Overview
The system is made up of two key elements:
- **Grasshopper Polygon Engine**.  Grasshopper is a programming and parametric modelling interface for the *Rhino* CAD software. Rhino is great for generating vector graphics and Grasshopper is a truly awesome plugin that allows you to visually automate anything without needing to know or write programming code.  We'll create visual (blockly) system to automatically take our character list and generate the polygon geometry required for all our icons.  
- **Ruby** A scripting launguage used to take the control point data from the CAD program and build the package library in Eagle.  Most scripting launguages could have been used for this.  I chose Ruby as it is lightweight and elegant and I am learning it at the moment!


##Building the package library in Ruby 

The assets that we have now are:
- **characters.txt** : List of characters to be converted to graphic icons in Eagle.   
- **Points Lists for each character**: E.G. the character **16** generates 3 polygons who's control points exist in 16-1.pts, 16-2.pts, and 16-3.pts list files respectively. Our Grasshopper algorythm generates points lists for all characters in the characters.txt list.
- **config.txt** a config file containing the font, render size and anchor point for each character. It is not possible to complete Typesetting automatially.  The size and positioning of poloygons depends on specific characters.  The algorythym is set up for a user to do this in an interface and to tweak parameters untill the desired result is obtained. Once each character is **Typeset** the specific scale, font and anchor point is recorded and saved in this config file.  
- **Lib-template.xml** This is a template used to generate the Eagle Library. Library Eagle files are pretty easy to follow **XML** files with the package data contained in the middle. This is a standard template that will be converted by our Ruby script to build the complete CHAR-PIBOT.lbr file.

###Typical List

```
1.31423434, -2.34545345435, 0
0.53424344, -2.93434234234, 0
3.23232322, 0.343443435343, 0
etc...
```


Questions: How to build the file in Ruby.  