Table Assembly Tutorial
============
A very simple subassembly task using the FreeCAD Assembly 4 Workbench
----------

Our table has just three component types:

1. table top
1. leg
1. foot

We will make a sub-assembly from the leg and the foot, then add four of these to the table top.

Set up the files:
==================
Create the following five files, saving them in the same directory for convenience:

![](TableSubassyScreenshots/Files.png)

Switch to the TableTop tab at the bottom of your window: ![](TableSubassyScreenshots/TabTableTop.png)

Choose the Assembly 4 workbench ![](TableSubassyScreenshots/Assy4Workbench.png)  and insert a new Assembly4 Model: ![](TableSubassyScreenshots/Assy4Model.png)

Create a new Body ![](TableSubassyScreenshots/NewBody.png) leaving the default name "Body".

Expanding our model tree, it now looks like this:

![](TableSubassyScreenshots/TreeTable.png)

Drag the parts folder into the Model in the tree.  This simplifies later steps when choosing what to include in our assembly.


![](TableSubassyScreenshots/TreeTablePartsMoved.png)

Add a Model ![](TableSubassyScreenshots/Assy4Model.png) and Body ![](TableSubassyScreenshots/NewBody.png) in the same way for the *Leg* and *Foot* files.

For the LegFootAssembly and the TableAssembly files, add a model ![](TableSubassyScreenshots/Assy4Model.png) only.  We don't need a Body for these (though it won't do any harm).


---------------------
Create the table top:
=======================

Switch to the *TabelTop* file, select the Assembly 4 workbench ![](TableSubassyScreenshots/Assy4Workbench.png).

Right-click on the Body in the tree:
![](TableSubassyScreenshots/ActiveBody.png)
and select "Toggle active body".
This will change you out of the **Assembly 4** workbench to the **Part Design** workbench.

Click on the New Sketch button: ![](TableSubassyScreenshots/NewSketch.png).  Select XY_Plane001 (Base Plane) from the dialog and hit OK.

Create the following sketch of approximately 600mm x 400mm small table top:
![](TableSubassyScreenshots/SketchTableTop.png)

Constrain the corners to the centre with a symmetry constraint.  (Select the two corners, then the origin, and hit the 's' key).

Hit ESC or OK and pad the selected sketch ![](TableSubassyScreenshots/PadSketch.png) by 20mm:

![](TableSubassyScreenshots/TableTopComplete.png)

Save the *TableTop* file.

--------------------------
Create the leg
=================

Follow the same procedure as above to create the table leg, with sketch dimensions of 40x40mm and pad height of 300mm.
![](TableSubassyScreenshots/SketchLeg.png)

As per the table, constrain the corners to the centre with a symmetry constraint.  (Select the two corners, then the origin, and hit the 's' key). This will allow us to use the default Local Co-ordinate System to attach the foot to the centre of the leg later.

![](TableSubassyScreenshots/LegComplete.png)

Our leg model tree should now look like this:

![](TableSubassyScreenshots/TreeLeg.png)

Save the *Leg* file.

----------------------

Create the foot:
===================

Repeat the procedure again, this time creating a circular sketch with a 60mm diameter:

![](TableSubassyScreenshots/SketchFoot.png)

Constrain the sketch centrepoint to the origin (select both points and hit 'c' for coincident)

This time, when you create the pad feature, reverse the direction so that the solid is below the origin:

![](TableSubassyScreenshots/FootPadReversed.png)

![](TableSubassyScreenshots/FootComplete.png)

When we attach the top of the foot to the bottom of the leg, we can use the origin without needing to add another Local Co-ordinate System.

Save the *Foot* file.

------------------------

Create the leg and foot assembly:
=====================

To enable file model names to appear in the assembly windows, close all the files and re-open them.

Select the *LegFootAssembly* tab (at the bottom of the window)

![](TableSubassyScreenshots/LegFootAssemblyTab.png)

to activate the file.

From the Assembly 4 workbench toolbar, select "*Insert part into the assembly*".  ![](TableSubassyScreenshots/InsertPartAssembly.png)

Choose **Leg#Model** and click OK.

Repeat for the foot, choosing **Foot#Model**.

Because we chose the pad direction for the leg to be **up** from the origin, and the pad direction for the foot to be **down**, the parts automatically align correctly, each with its origin at the assembly origin:

![](TableSubassyScreenshots/FootLegAssy.png)

Save the *LegFootAssembly* file.

-------------------------

Create the table assembly:
============================

Activate the *TableAssembly* file: ![](TableSubassyScreenshots/TableAssyTab.png)

Insert the *TableTop* part into the assembly
-------------

From the Assembly 4 workbench toolbar, select *Insert part into the assembly*.  ![](TableSubassyScreenshots/InsertPartAssembly.png)

Select **TableTop#Model** and hit OK.
This will insert the *TableTop* part at the origin.

![](TableSubassyScreenshots/AssemblyTop.png)

Insert the *LegFootAssembly*
-------------

Insert ![](TableSubassyScreenshots/InsertPartAssembly.png) the leg and foot assembly in the same way by choosing **LegFootAssembly#Model**.

This also inserts the assembly by default at the origin:

![](TableSubassyScreenshots/AssemblyLegFootInitial.png)



We need to attach it to the corner of the table.  For this, we need to create **Local Co-ordinate Systems** (LCS), four on the *TableTop* and a matching one on the *LegFootAssembly*.

**Create the *TableTop* LCSs:**

Open the *TableTop* file and click Create new co-ordinate system in part. ![](TableSubassyScreenshots/CreateCoordinateSystem.png)

Rename it to "LCS\_Leg1"

![](TableSubassyScreenshots/LCS_Leg1.png)

This will place our new LCS at the origin:

![](TableSubassyScreenshots/LCS_Leg1Origin.png)

Move it to the corner where we want to attach the leg as follows:

Right-click on the LCS in the model tree:

![](TableSubassyScreenshots/LCS_Leg1ModelTree.png)

Select "Edit Datum" to bring up the Co-ordinate system parameters dialog.

![](TableSubassyScreenshots/LCSCoordinateSystmemParameters.png)

In the order shown by 1,2 and 3 below, select the bottom corners of the table top:

![](TableSubassyScreenshots/LCSCoordinateSystemMove1.png)

Next, select the Attachment mode "**Align O-X-Y**" to indicate that the three points we just selected should be the Origin, X-axis direction and Y-axis direction of our new LCS.

![](TableSubassyScreenshots/LCSAlignO-X-Y.png)

This will align the new LCS as shown:

![](TableSubassyScreenshots/LCSAligned.png)

Add LCS\_Leg2, LCS\_Leg3 and LCS\_Leg4 in the same way, rotating the table top each time.

**\*Note:** Ensure you select three **vertices** each time for your Origin, X-direction and Y-direction, and not one of the other LCSs you just created.

Our part should now look like this:

![](TableSubassyScreenshots/LCSAlignedComplete.png)

Also check that your LCSs are created at the root of the model tree as shown:

![](TableSubassyScreenshots/TreeLCSRoot.png)

If you want to import this LCS into another assembly later, it must be at the root level.

**Create the LegFootAssembly LCS:**

It is not possible to position an LCS in an assembly, so we instead create an LCS in the *Leg* part and **import** it into the *LegFootAssembly*.

Activate the *Leg* part: ![](TableSubassyScreenshots/TabLeg.png)

Click Create new co-ordinate system in part. ![](TableSubassyScreenshots/CreateCoordinateSystem.png)

Rename it to "LCS\_TopCorner".
This will place it at the origin as shown:

![](TableSubassyScreenshots/LCSTopCornerDefault.png)

Right click on the new LCS in the model tree:

![](TableSubassyScreenshots/LCS_TopCornerRightClick.png)

and select "Edit datum".

As before with the table top, select the three corners and choose attachment mode **O-X-Y**.

![](TableSubassyScreenshots/LCS_LegOXY.png)

![](TableSubassyScreenshots/LCSLegChooseOXY.png)

Hit OK and save the *Leg* file.

Activate the *LegFootAssembly* file, where you will now see the new LCS.

Select the new LCS in the model tree of the *LegFootAssembly*:
![](TableSubassyScreenshots/LCS_LegFootSelected.png)


Click "Import datum object" ![](TableSubassyScreenshots/ImportDatumObject.png) and keep the default settings:

![](TableSubassyScreenshots/ImportDatumObjectDefaults.png)

We can now see a copy of the datum object in the *LegFootAssembly* tree:

![](TableSubassyScreenshots/TreeLegFootAssyImportedDatum.png)


Activate the *TabelAssembly* file: ![](TableSubassyScreenshots/TableAssyTab.png)

Select the LegFootAssembly in the model tree:

![](TableSubassyScreenshots/TreeSelectLegFootAssembly.png)

Click "Move/Attach a part in the assembly" ![](TableSubassyScreenshots/MoveAttachPart.png)

In the following dialog, select Attach to: TableTop.
Under "Select LCS in Part:" choose LCS\_TopCorner.
Under "Select LSC in Parent:" choose LCS\_Leg1

![](TableSubassyScreenshots/AssemblyTablePlaceLinkedPart.png)

This aligns the two parts by aligning the co-ordinate systems we created.

![](TableSubassyScreenshots/AssemblyTableLeg1.png)

Hit OK, and then repeat for the other three legs, renaming them as you go to LegFootAssembly_2, etc.

The finished product won't win us any Furniture Industry Association awards, but at least we can now make assemblies and sub-assembles with Zolko's Assembly 4 workbench.

![](TableSubassyScreenshots/AssemblyTableComplete.png)

Summary
===============
We need a total of nine parts to assemble the table: four legs, four feet and a table top.  We could add each of these nine individually, but it is much faster - and easier to update - if we include the leg and foot together as a sub-assembly.

To do this, we need to add a Local Co-ordinate System to the leg, and import it into the leg/foot subassembly for use in the finished product.