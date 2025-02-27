# UpdateDefinition
Updates underlying service definition of a layer in ArcGIS Online

Service Definitions are defined at the time of publishing a feature service. In cases of symbology, this can be edited in the portal but does not change the definition of the feature itself and the original symbology will be visible when brought into external applications. Users can typically utilize ArcPro to make the edits and overwrite the feature with the changes, however, republishing the layer from ArcPro may not be an option in some situations depending on the source and layer type. ArcPro does not recognize data shared from the ETL server as a valid layer type for publishing. 

To combat this, the feature service API Update Definition operation can be used to update the definition directly by replacing elements of the JSON. Like in overwriting with ArcPro, users will need to have ownership of the layer to complete this task. In most cases, a URL can navigate the user to a backend which allows the edited JSON element to be posted from within the browser. This URL looks something like: 
https://services.myserver.com/OrgID/ArcGIS/rest/admin/services/example/FeatureServer/0/updateDefinition

This may also be done via the update_definition() function in ArcPy. 

The script authenticates to ArcGIS Online Portal and retrieves the feature by the layer ID and item number using the GIS class. Update_params acts as our dictionary which will be passed to the update_definition() class with the new values we would like to see. Here, we update symbology using ESRI’s Picture Marker Symbol properties (esriPMS) to change the symbology to the company logo. The “imageData” value is the base64 encoded data for the image and was retrieved by publishing the desired symbology in a test layer from ArcPro. The value for “url” is derived from the example in the esriPMS documentation. Labels can also be set here and the values used also come from the test layer with the desired output. Finally, response = fs_layer.manager.update_definition(update_params) updates our definition. 

It was found that this will successfully apply to the original layer. Attempting this on a view layer gave inconsistent results. 
