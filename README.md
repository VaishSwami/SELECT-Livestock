# SELECT-Livestock
Python for implementing SELECT on ArcGIS 
import arcpy
from arcpy.sa import *
arcpy.CheckOutExtension("Spatial")
#Getting input, output and scratch folder paths 
InputWorkspace= arcpy.GetParameterAsText(0)
UserWorkspace= arcpy.GetParameterAsText(1)
ScratchSpace= arcpy.GetParameterAsText(2)

arcpy.env.workspace= UserWorkspace
arcpy.env.scratchWorkspace= ScratchSpace

#Livestock options (checkbox parameters) 
Opt1= arcpy.GetParameterAsText(3)
Opt2= arcpy.GetParameterAsText(4)
Opt3= arcpy.GetParameterAsText(5)


try:
    if str(Opt1)== "true":
        op1= Reclassify(InputWorkspace+ "\\lamplanduse", "VALUE", RemapValue([[24, 1],[41, 1], [43, 1], [52, 1]]), "NODATA")
        op1.save("op1_Test")
    if str(Opt2)== "true":
        op2= Reclassify(InputWorkspace+ "\\lamplanduse", "VALUE", RemapValue([[21, 1],[82, 1], [90, 1], [31, 1]]), "NODATA")
        op2.save("op2_Test")
    if str(Opt3)== "true":
        op3= Reclassify(InputWorkspace+ "\\lamplanduse", "VALUE", RemapValue([[22, 1]]), "NODATA")
        op3.save("op3_Test")



except:
    e= sys.exc_info()[1]
    print(e.agrs[0])
    arcpy.AddError(e.args[0])
