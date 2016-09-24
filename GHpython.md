# Set up your points for looping
This is the script:

import rhinoscriptsyntax as rs

if not x: x = rs.AddPoint (0,0,0)
if not y: y = rs.AddPoint (0,5,5)

a = rs.AddLine(x,y)
```


