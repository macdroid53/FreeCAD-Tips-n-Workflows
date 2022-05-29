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


