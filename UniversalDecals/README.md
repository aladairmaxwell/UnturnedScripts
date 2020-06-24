QUICK NOTE: The README Text wrapping drives me insane! If you want an easier to read guide but with no photos click here https://gist.github.com/olie304/4c1dca2c1b9d6ae6a1956391601142e2

This allows you to apply decals to modded objects without the need of two seperate objects or the need of the editor.
You can even have more than one decal on a single object.
This is useful when your object is not part of the landscape and is something like a placeable object or a vehicle.

First setup an object like so:
Add the texture you want to use for the Decal to the workspace and name it "Decal".
Create an empty Game Object on the asset you want to include decals with, I am going to call it "DecalSystem" for this guide.
DecalSystem should have a BoxCollider on it. Anything that intersects the BoxCollider will have the Decal texture projected onto it.
Add two child Game Objects to DecalSystem named "Mesh" and "Decal".
Add a MeshRenderer and a MeshFilter with a plane to Mesh.
Mesh is what will get loaded if the user's graphics settings are on Forward.
Create a material named "Decal_Forward" with a standard shader and the texture named Decal and apply it to Mesh's MeshRenderer.
The Game Object Decal should have the script "Decal.cs" as a component.
Create a material named "Decal_Deferred" with a standard shader and the texture named Decal and add it to the Decal script's material slot.
Export your finished Game Object setup to an asset bundle like you would normally.
If you get stuck look at the included DecalSystemExample.unitypackage inside this folder.

Open Unity Asset Bundle Extractor (UABE) and open the file resources.assets in the Unturned/Unturned_Data directory.
Click the Info button if nothing has happened yet.
Navigate to View>Search By Name and inside of the prompt type Material_Decal.
Open up the Data Inspector by clicking 'View Data'.
Expand the tree Material Base>m_Shader>[view asset]>Shader Base>m_ParsedForm and look at the m_Name property. If your Decal uses an alpha channel then make sure this says Decal/Diffuse-Alpha.
![1](images/1.png)

Otherwise if you are not using an alpha channel look for the other object named Material_Decal right next to the other one.
![2](images/2.png)

Once you have found the correct Material_Decal, copy down the Shader's m_PathID because you will need it again in a moment.
![3](images/3.png)

You can now exit out of the data inspection menu and while ensuring that the right Material_Decal is selected click 'Export Dump'. This will create a text file named something like "Material_Decal-resources.assets-39-Material.txt" in the directory of resources.assets.
Navigate to View>Go To Asset and then in the File ID box ensure resources.asset is selected and the Path ID is the one for the shader that you copied down earlier; Click 'Ok'.
Then click 'Export Dump' again.
Lastly go to File>Close.

Next open the asset bundle you exported from Unity in the beginning in UABE, it will prompt you to decompress the file and you should say yes, save it to a file with the same name but a different extension to make things easier.
Go to View>Search by Name and search for your material named "Decal_Deferred".
Open the data inspector.
Find the shader m_PathID the same way you did the other one and copy that down, you do not need to export it.
Now expand the tree m_SavedProperties>m_TexEnvs>Array>0>...>m_Texture and copy down that m_PathID as well.
![4](images/4.png)

You are almost done (Yay!).
Now open up your dump file that has a similar name to "Material_Decal-resources.assets-39-Material.txt" and replace the Shader and _MainTex Path IDs with the ones you copied from your own asset bundle.
![5](images/5.png)

Now go back to UABE.
Find that shader with the Path ID inside of your asset bundle using View>Go to Asset again.
Click  'Import Dump' and open the dump generated by the Export Dump we did on the shader from resources.assets, the name should be similar to "unnamed asset-resources.assets-5923-Shader.txt".
Find your "Decal_Deferred" material again and then click 'Import Dump' and then import the Material_Decal dump you edited earlier.

Lastly you just need to save the new Asset Bundle which is a little bit jankey so I recommend doing all of the following:
On the current window click File>Save then File>Close and then on the next window do File>Save then File>Close again.
You can now use the uncompressed asset bundle you saved with a different extension as you would normally and any decals will render correctly!

Now you can have decals in places never once thought possible! Unlimited Power!
![6](images/6.png)