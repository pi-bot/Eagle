#Automatically Creating Icon Libraries for use in Eagle

Exposed Printed Circuit Board products are becoming ever more jazzy in their visual design and layout. Icons etched from the gold of the copper, multi-coloured silkscreen and brigntly colored PCB's are becoming more and more popular. I personally love graphics and with the PiBot board expposed I really wanted it to look just a good as it functions.  Being used to graphic design when I started designing PCB's I naturally wanted to control them graphically. Unsurprisingly this is not the focus of PCB design software and there innate graphica and layourt capabilities are mostly limited. There is only one font for example and no, in built way of importing graphics into silkscreens.

I did find various blogs and pointers on the subject however I could not get them working well enough for my set up of needs.  I rolled up my sleaves and I've come up with a solution I'm happy with.

###Graphic Limits
Its good to have limits in any creative medium and as a starting point lets consider. 

####Wires or Polygons 
Firstly Eagle has two graphical objects **wire** and **polygon**.  Wires are made up of straight lines with a thickness applied. Typically you see these marking the outlines of device packages on the white silskcreen layer of the PCB.  A typical wire is coded like this in Eagle:
```
<wire x1="-8.89" y1="-2.54" x2="-11.43" y2="5.08" width="0" layer="1"/>
```
As well as its width and layer the required data for a wire is its start and end point. A polygon is a filled area that is made up of a closed polyline. In eagle this is coded as:
```
<polygon width="0" layer="1">
<vertex x="16.51" y="-6.35"/>
<vertex x="13.97" y="2.54"/>
<vertex x="6.35" y="-3.81"/>
<vertex x="5.08" y="-10.16"/>
<vertex x="10.16" y="-8.89"/>
<vertex x="12.7" y="-7.62"/>
</polygon>
```
You  can see that the basic units of Eagle polygons are verteces that represent the polygons connection points.  

#### Representing Curves 
With enough verteces and lines in Eagle you can imagine that it it will be possible to creat pretty much any kind of vector graphic.  This circle for example is actually a polygon of 36 sides and at this level of resolution you can see that we can achieve **good enough** results to represent anything.  The one caveat that needs a workaround though is to have the ability to have holes in polygons. This limitation is more serious though there are work arounds. 

###Making Holes
Take the number 8.  It is possible to make this shape in Eagle however you need to split the polygons that do not contain any other polygon.  With the 8 we do this by making two polygons that touch.

This guide assumes a working knowledge of Eagle, PCB design as well as  a basic understanding of vector graphics.

Graphics are 
To make graphics portable it makes sense to create them as library parts that is the established best practice. As graphics perform no electrical function they are packages that need no symbol counterpart. Pretty quickly you see that the device interface with the polygon and wire tool are appropriate for really making simple praphics. For complex shapes it makes sense to import the graphics from external sources.

The two I've explored are DXF inport and . There are two ULPs for this.  For one reason or another I found all these methods did not work for my set up. (Eagle instances on Windows and Mac) . 


Specifically what I wanted to create is a way of importing characters and icons from existing font sets and icon libraries.  I also wnated to find a way for automating this.  



##Creating the app

  
My goal is to create an application that genates an icon library for use in Eagle.  By 'icons' I mean character symbols that will be used for markers and decorations in my PCB design.  The app is made up of two elements:
- **Aotomated Icon Geometry Engine**.  This will essentially take a list of the characters I want rendered in Eagle and will generate all the geometry for these icons. 
- **Eagle Library Builder** This is a script that converts all the data output from the Icon Geometry Engine to build a valid Eagle Library - one for each icon set.

### App Overview
I'll place my app in Eagle's cam folder in a directory called **icons**  (Eagle/cam/icons).  CAM - Computer Aided Manufacture).
The App consists of: 
- **buildEagleIconsLib.rb**. This is is the ruby script that will be used to build the Eagle library. One of many scripting languages could have been used though I chose ruby as its a language I'm learning and I wnated to improve in.
- **Lib-template.xml** This is a template used to generate the Eagle Libraries. Eagle Library files are pretty easy to follow **XML** files with a libraries package data contained in the middle. This is a standard template that will be converted by our Ruby script to build the completed icon libraries.

For each icon set there will then be two key files: 

- **[iconName]-config.json** e.g. for the pibot icons this will be **pibot-config.json**. This will contain all the information required for the geometry engine to build the geometry of our icons. 
- **[iconName]-data.json** e.g. for the pibot icons this will be **pibot-data.json**. This will be all the geometry and other information required to build the eagle library from.  

After the **geometry engine** and the **buildEagleIconsLib** script have done their work the generated eagle Library will be placed in the Eagle/lbr folder ready for use with eagle. Now I'll go into greater details with each element of app as well as it's data files. 

##JSON files for data tranfer
JSON (Javascript Object Notation) has been chosen as the ideal transfer file for the app as it is lightweight, clearly structured, readable and easily used by each app element. The Jason syntax looks like: 
```
 [ { line object 1 } , { line object 2 } ] 
 ```
 Each line object comprises of { key : value } pairs, where **key** is the variable and **value** is the data assigned to the variable for the object.  To illustrate here is an example JSON file:
 
 ```
 {
    "firstName": "John",
    "lastName": "Smith",
    "age": 25,
    "address": {
        "streetAddress": "21 2nd Street",
        "city": "New York",
        "state": "NY",
        "postalCode": 10021
    },
    "phoneNumbers": [
        {
            "type": "home",
            "number": "212 555-1234"
        },
        {
            "type": "fax",
            "number": "646 555-4567"
        }
    ]
}
```
 
 




### [iconName]-config.json in detail

A complete config file for creating the required geometric data for the icon library. Each file contains:

- **chars** the character set that the icons represent. e.g. for the pibot.pcb this is : 1, 2, ~3, 4, ~5, ~6, 7, 8, ~9 ,~10 ,~11 ,12 ,13 ,22 ,23 ,24 ,25 ,26 ,27 ,28 ,32 ,14 ,15 ,16 ,17 ,19.
- **font** the font used render the chars (e.g. VAG rounded)
- **size** the default size in mm that the font is rendered in.
- **bold** true/false value whether the chars are to be rendered as **bold** or not.
- **italic** true/false value whether the chars are to be rendered as *italics* or not.
- **anchor** the default anchor point for each charset
- **resolution** the number of decimal places to store geometry data for the char set. Default is 3. 


### [iconName]-data.json in detail

A complete export file containing everything required to build an Icon package library for each icon set. It is two levels deep 
At the top (library) level data given is
Each file contains:

- **char** the character that the icons represent. e.g.
- **scale** the scale factor used to center/normalise the character icon. Used with the charsets **size** parameter
- **offset** an offset vector(difference in x and y) used to normalise/center the icon character. (used in combination with **scale**
- **num_polygons** number of seperate polygons used to represent the icon. (there will be a data set for each)
- **brocken** true/false value whether the geometry for the icon was broken up to remove holes.
- **pointSets** the control points (verteces in eagle) used to create each polygon.  
 
An example file for two characters would then be:
```
 {
    "char": "1",
    "scale": "0.95",
    "age": 25,
    "offset": {
        "x": -0.12,
        "y": -.15
    },
    "num_polygons": 3,
    "brocken": true,
    "pointSets": {
      [
        [-0.302921,-0.515019]
        [-0.503542,-0.444211]
        [-0.615654,-0.261292]
        [-0.651058,-0.037069]
      ],
      [
        [-0.615654,0.193056]
        [-0.503542,0.375975]
        [-0.302921,0.446782]
      ],  
      [
        [-0.143604,0.405478]
        [-0.037393,0.293366]
        [0.021613,0.134049]
        [0.039315,-0.037069]
        [0.021613,-0.202286] 
      ]
      }
}
```




##Icon Geometry Engine
- **Grasshopper Polygon Engine**.  Grasshopper is a programming and parametric modelling interface for the *Rhino* CAD software. Rhino is great for generating vector graphics and Grasshopper is a truly awesome plugin that allows you to visually automate anything without needing to know or write programming code.  We'll create visual (blockly) system to automatically take our character list and generate the polygon geometry required for all our icons.  
- **Ruby** A scripting launguage used to take the control point data from the CAD program and build the package library in Eagle.  Most scripting launguages could have been used for this.  I chose Ruby as it is lightweight and elegant and I am learning it at the moment!





takes a list characters and returns a package library of the characters in eagle scaled correctly and in a font of your choice.  This involves the character list.

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
libName = ARGV.first #corresponds with directory in root
charList = open("#{libName}/chars.txt")
puts "Here's an output of the #{libName} char list:"
print charList.read
puts "Confirm the file contains the geometry wanted to build your package library?"


File.readlines('test.txt').map do |line|
  line.split.map(&:to_i)
end
```
