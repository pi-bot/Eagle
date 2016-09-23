#Automatically creating packages

This will be used to collect code and think through solution initially. I'll then tiddy it up and make it clearer whats its all about.  

The question is how to create a script/system that takes a list characters and returns a package library of the characters in eagle scaled correctly and in a font of your choice.  This involves the character list.

##Character List 
The character list for the PiBot board represent the input and out put pins for the board.
```
1
2
~3
4
~5
~6
7
8
~9
~10
~11
12
13
22
23
24
25
26
27
28
32
14
15
16
17
19
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

###Typical Poygon Point List

```
{-0.302921,-0.515019,0.0}
{-0.503542,-0.444211,0.0}
{-0.615654,-0.261292,0.0}
{-0.651058,-0.037069,0.0}
{-0.615654,0.193056,0.0}
{-0.503542,0.375975,0.0}
{-0.302921,0.446782,0.0}
{-0.143604,0.405478,0.0}
{-0.037393,0.293366,0.0}
{0.021613,0.134049,0.0}
{0.039315,-0.037069,0.0}
{0.021613,-0.202286,0.0}
```

###File Locations
All files need to be located in a created **icons** directory nested in the Eagle cam folder. For me this **pwd** (present working directory) is:
```
/Users/Agilimac/Dropbox/Eagle/cam/icons
```
In the root of this folder we'll place all the source directories (one per Eagle library) as well as the Ruby **buildEagleIconsLib.rb** script. 

##Building the Ruby app

We'll design the app so it takes just one argument: the name of the character icon library. The script will then use this to locate all the required make files, make the Eagle library and place the library in the **Eagle/lib** folder ready for use.   It takes just one parameter the URL of the directory to build the library from.


```
libName = ARGV.first
charList = open(libName)
puts "Here's an output of the #{Libname} char list:"
print charList.read
puts "Confirm the file contains the geometry wanted to build your package library?"


makeFolder = 


File.readlines('test.txt').map do |line|
  line.split.map(&:to_i)
end
```
