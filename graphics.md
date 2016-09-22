#Beautiful graphics in Eagle 

In my quest to make a stunning PCB look I've be researching ways of importing vector graphics into Eagle.  I was not able to find a solution that worked for me hence forming a custom solution.  What I did learn is that Eagle is limited to polygons (color filled and made up of straight lines) and wires (Single line rendered in a given thickness.) By using either the silkscreen, exposed copper (e.g. in tStop layer) and etching (bRestrict layer)you can make some great graphics.  The way to go is create graphics and icons as 'packages'in a library.  From there they can then be imported to any board layout. 
 Packages in Eagle are written in XML with a packages containing a single polygon looking like: 
```
<package name="X-22">
<!-- 1 -->
<polygon width="0" layer="29">
<vertex x="-0.437" y="-0.382"/>
<vertex x="-0.437" y="0.411"/>
<vertex x="-0.53" y="0.411"/>
<vertex x="-0.617" y="0.44"/>
<vertex x="-0.639" y="0.519"/>
<vertex x="-0.61" y="0.598"/>
<vertex x="-0.53" y="0.634"/>
<vertex x="-0.307" y="0.634"/>
<vertex x="-0.228" y="0.605"/>
<vertex x="-0.199" y="0.519"/>
<vertex x="-0.199" y="-0.382"/>
<vertex x="-0.235" y="-0.475"/>
<vertex x="-0.314" y="-0.504"/>
<vertex x="-0.401" y="-0.475"/>
<vertex x="-0.437" y="-0.382"/>
</polygon>
</package>
```
You can see that the vertexes contain the **x** and **y** coordinates of all the controll points.  This also tells me that it would be pretty easy to convert graphics in SVG format to Eagle packages.   See here for a **polyline** in  **SVG**.

```
<svg width="150" height="200">
 <desc>Second orange polyline demonstrating yellow fill on open path.</desc>
 <polyline points="0,40 40,40 40,80 80,80 80,120 120,120 120,160" fill="#F9F38C" stroke="#D07735" stroke-width="6" />
</svg>
```

##Cunning Plan
My plan then is to create both an SVG library and Eagle Packages library from the same graphics. My software of choice to create vector graphics is Rhino and luckily there is a great automation and parametric plugin for Rhino called Grasshopper.  With grasshopper I can create algorythms that can take the raw geometry, text, and artwork and convert it to outputs I can use to make the libraries. 

###




##Cat
cat file1 file2 > file3



