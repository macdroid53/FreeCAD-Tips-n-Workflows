# A collection of tips, workflows, and miscellaneous information about using FreeCAD



## Import STL files
STL files are best used to trace over. They are typically more trouble than they are worth.

They can be imported and converted to a solid. But, there is no parametric info in a STL file.
The result of the import, if successful, is a solid, devoid of any parametric information.

The steps to import an STL file:
<ul>
  <li>Use File>Import to import the STL file</li>
  Or, use Mesh workbench Import Mesh
  <li>use tools in Mesh workbench to verify it is a manifold file</li>
  Mesh workbench Analyze, Fill hole, etc. as needed.
  <li>Use Mesh workbench Decimate</li>
  Reduce as far below 100k triangles as possible.
  <li>use Part workbench Convert to shape</li>
  <li>use Part WB Check geometry to make sure it produced a valid shape</li>
  <li>use Part WB Convert to solid</li>
  <li>use Part WB Check geometry to make sure it produced a valid solid</li>
  <li>if all that was successful, the solid can be used directly with Part workbench</li>
  <li>to use it with Part Design workbench, create a Part Design Body</li>
  <li>drag-n-drop the solid into the Body</li>
  This will create a Basefeature. It is a solid that you can add to or cut away from with Part Design tools.
</ul>


## Get the radius of a selected arc
<ul>
  <li>Select the edge in the 3D view.</li>
  <li>Press Ctrl+Shift+P.</li>
  <li>In the python console (view menu -> panels -> python console) enter:</li>
  elt.Curve.Radius
</ul>

## Get the length of selected edge
<ul>
  <li>Select the edge in the 3D view.</li>
  <li>Press Ctrl+Shift+P.</li>
  <li>In the python console (view menu -> panels -> python console) enter:</li>
  elt.Length
</ul>

## Expression syntax to refer to the Body object Placement object
<ul>
  <li>For example, to use the z value of the Body placement</li>
  <li>Body.Placement.Base.z</li>
</ul>

## Find open and gap vertexes in a sketch
<ul>
  <li>In the python console, enter:</li>
  App.ActiveDocument.Sketch.detectMissingPointOnPointConstraints(100)
  <li>This launch the detection process, returns the number of missing constraints.</li>
  <li>In the python console, enter:</li>
  App.ActiveDocument.Sketch.MissingPointOnPointConstraints
  <li>This returns a Python List of tuples that are the missing coincidences found at the previous step</li>
  <li>In the python console, enter:</li>
  App.ActiveDocument.Sketch.OpenVertices
  <li>This return a Python list of tuples that are the open vertexes.</li>
</ul>

## Using shapestrings effectively
Most discussions make this far more complicated than it is.

There are a few things to keep in mind:
<ul>
  <li>The chosen font must be viable for use.</li>
  <li>It must have closed profiles and no crossing or intersecting lines.</li>
</ul>
Fonts are art, so basically don't necessarily care about such things.

If working in Part Design, you can't pocket through your solid because letters like R, O, D, etc. are going to break the single solid rule. A Pocket into the surface, but not through, or a Pad is fine.

Many videos show various machinations that are out of date, since you can just drag the Shapestring into the Body, position it (grossly with Transform, then fine tune with the properties of the Shapestring), then Pad or Pocket.

## Expression syntax for unnamed constraint

Given Sketch has a constraint 'Constraint9' that has been named 'abc' the following can be used in an expression.

*Sketch.Constraints.abc*

But what is the syntax for an unnamed constraint?

*Sketch.Constraints.Constraint9*

Fails to parse.

***Answer:*** 

*Sketch.Constraints[8]*

**Note:** Look at the Properties view and see that the Constraints property is a Python list

## Mass, COG, Area, etc.
In the Python console enter:

*m = FreeCADGui.Selection.getSelection()[0].Shape.MatrixOfInertia*
*m*

***Result:***

*Matrix ((61.7946,4.9086,-11.5488,0),(4.9086,66.5861,-18.4738,0),(-11.5488,-18.4738,102.199,0),(0,0,0,1))*

In the Python console enter:

*mass = FreeCADGui.Selection.getSelection()[0].Shape.CenterOfMass*
*mass*

***Result:***

*Vector (21.63548536771986, 35.499731244404686, 36.656887161270994)*

In the Python console enter:

*a = FreeCADGui.Selection.getSelection()[0].Shape.Area*
*a*

Result:
*106.4468*

## Expression syntax for spreadsheet cell to access area property

Assuming there is a feature in the Tree view with the label *Face001*

*=Face001.Shape.Area*

## Select an object by name

Assume the document is named: *Unnamed*
Assume the objects label in the Treeview is: *Face001*

In the Python console enter:

*Gui.Selection.addSelection('Unnamed','Face001')*

***Result:***

The first selection object is Face001.

*m = FreeCADGui.Selection.getSelection()[0].Shape*

## Set a spreadsheet cell from the Python console

Assume the document is named: *Unnamed*
Assume the objects label in the Treeview is: *Face001*

In the Python console enter:

*Gui.Selection.addSelection('Unnamed','Face001')*

*m = FreeCADGui.Selection.getSelection()[0].Shape*

*ar=m.Area*

*App.ActiveDocument.Spreadsheet.set("A2", str(ar))*

***Result:***

After recompute, cell A2 of the spreadsheet is the area of Face001.

## Dealing with lost in space import geometry

<ul>
  <li>If the solid is in a container, drag it out into the tree</li>
  <li>Use one of the following to move the solid to the origin</li>
  <ul>
    <li>MoveToOrigin macro</li>
    <li>Manipulator workbench</li>
  </ul>
  <li>Use KicadSteup workbench Reset origin</li>
</ul>

Now, the solid can be dragged into a Body and not revert to it's original location in space.

