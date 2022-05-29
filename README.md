# A collection of tips, workflows, and miscellaneous information about using FreeCAD



## Import STL files
STL files are best used to trace over. They are typically more trouble than they are worth.

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
  <li>If all that was successful, then create a Part Design Body</li>
  This will create a Basefeature. It is a solid that you can add to or cut away from.
</ul>


