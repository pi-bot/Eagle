# Set up your points for looping
This is the script:
````
import rhinoscriptsyntax as rs

if not x: x = rs.AddPoint (0,0,0)
if not y: y = rs.AddPoint (0,5,5)

a = rs.AddLine(x,y)
```


This is how to get data
```
polygons = rs.GetObjects (Select Polygons for conversion to an Icon, 1)

for pt in points:
ptCoord = rs.PointCoordinates(pt)
x = ptCoord[0]
y = ptCoord[1]
# we'll ingnore the z

print "x: %.3f,y: %.3f"  %[x,y]  # using python string formattters

# or to add to variables: 

line =  "%.3f,%.3f"  %[x,y]  # using python string formattters

```


