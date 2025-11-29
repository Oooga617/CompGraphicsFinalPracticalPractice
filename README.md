# CompGraphicsFinPracticalPractice

# Bump mapping and tiling:
The first shader used that was shown off in the earlier half of the semester in this class is bump mapping. Though it has been modified to account for tiling, which means that the textures can be scaled on the x and y axis. Firstly though, bump mapping is when a texture is given more depth by using a normal texture (a texture that uses the rgb values to modify the object normals) along with lighting calculations to add more depth and roughness to the texture itself. How it works is that the base texture along with the normal map is sampled first, and then the normal map on the x and y axis is multiplied with a slider property that controls the blend amount of the bump map effect. Then those values and the alpha value gets plugged into a 3D vector that is connected to a transform node that converts the tangents and normals to world space for lighting calculations to show the bump mapping and depth of the object, and so that gets plugged into a dot product node with the main light direction being normalized, and being saturated and multplied with negative -1 gets multiplied with the sampled base texture and the blend amount is controled with the lerp node. Though a Tiling and Offset node with the tiling 2D vector connected in the tiling port is used to control the tiling of both the base and normal textures. 

<img width="1462" height="663" alt="image" src="https://github.com/user-attachments/assets/c71d8603-5771-421f-b91f-55fe0c42c72e" />

This shader was utilized in this way in the project because I want to enhance the detail and realism of the stone textures as seen in Contra, as in that game the use of lighting and shadows convey a sense of depth and roughness of the stones. So, to try and mimic that but enhance it in a 3D space, bump mapping was used to create some insect in the lines between the stones to get some bit of depth without modifying the mesh itself. As for the modification of tiling, this was used so that the textures don't get stretched out across the surfaces, as the result will look very ugly. Like in Contra the stones are seen repeating itself in a smooth, transitional way so the stone texture and normal map applied is designed for that, and tiling was used to give context to the stone texture surface in a clean manner:

<img width="937" height="491" alt="image" src="https://github.com/user-attachments/assets/b9b6b944-5c0d-415d-ad6f-8fc6a7f0a4e8" />

<img width="397" height="171" alt="image" src="https://github.com/user-attachments/assets/6f6bda25-3629-46af-adea-6e457611ec6b" />

This is also seen in the grass texture to, it has both a base texture and a normal map to make the grass textures repeat itself and be scaled appropriately to not be stretched, but also have the bump mapping applied to give more roughness to try and convey that this is grass in the environment for more realism with how grass is viewed in it's coarse pattern and feel.

<img width="1081" height="388" alt="image" src="https://github.com/user-attachments/assets/f39950d1-84c0-4a04-9609-f5b06cbd5fce" />

# Transparency:
The second shader used is this transparency shader, which takes a transparent sprite and renders it without the background using the alpha channel. How it works simply is that the transparent sprite is sampled, and the RGBA values is linked to the final color output, and the alpha value is hooked to the alpha node of the fragment shader (this is only shown if you allow material override in the shader settings and that the sprite is set to be a transparent image). 

<img width="748" height="362" alt="image" src="https://github.com/user-attachments/assets/6fe9c012-8ca5-4a74-86d6-b5c5c3174859" />

This is used in the trees in the scene because in the reference in Contra in setting is seemingly set on an island (that is emphasized more later), where on the island minus the enemies and turrets are tones of follage and trees to show that there are forests in the environment. To give context and communicate that, having transparent tree sprites set up quickly conveys that in a quick, and also efficient manner in not having to model in and render tones of trees in the scene. 

<img width="1108" height="407" alt="image" src="https://github.com/user-attachments/assets/ee06fc1a-e0e6-4bd5-9b3f-9e184503e1b8" />

<img width="436" height="122" alt="image" src="https://github.com/user-attachments/assets/672d581c-b277-48e7-acbf-1b93558a3335" />

# Metallic:
The third shader used in this, but also coming from the latter half of the course is this mettalic shine effect, where it samples both the metallic texture for acting as the base texture being rendered but also layering on top of it a specular effect that adds smoothness and shine to the surfaces. It was calculated by computing the specular effect, which involves adding the normalized view direction and normals (multiplied by -1 to correct the specular) together. Then, that gets plugged into the dot product with the normalized main light direction to get the specular dot, and then its controlled by a property in the linked power node, and then it gets multiplied with the same sampled base texture for the metallic effect and added to the final output.

<img width="1077" height="601" alt="image" src="https://github.com/user-attachments/assets/004db02a-43dc-4bdd-ba8b-269d1ac0cfb0" />

This was used in the scene because there are mettalic pieces of a bridge that get destroyed, but to convey more realism into the scene I want to emphasize how metallic works in reflecting light with adding shine. The shine along with the metal textures further conveys that this piece of the bridge is meant to be metal as it is brighter than the other elements of the scene from how light works. 

<img width="943" height="467" alt="image" src="https://github.com/user-attachments/assets/2ccdb144-b516-4fa7-97e9-c550dc2ddc61" />

<img width="250" height="193" alt="image" src="https://github.com/user-attachments/assets/9ca9ba50-e823-41ac-ac1b-46a1be54cd07" />

# Water and Reflection:
Finally, there is the water shader. There are two components, the UV scrolling effect and the cube map reflection. For the scrolling that was done by sampling the base water texture and the foam, and using the Tiling and Offset node to animate the scrolling. A 2D vector property is used and being multiplied by the product of the time and speed float to control where the UVs shall scroll along with the direction it should travel in (the foam texture is set to scroll slower as it's speed is cut in half). The tiling is also added with a 2D vector property to not have the water stretch over and look ugly and unrealistic. As for the reflection, being added to the final output a cube map was sampled and being reflected with the Sample Reflected Cubemap node that takes the cube map, along with the normalized view direction and normal vectors (multiplied with -1 to flip the cubemap projection), and then it gets blended with a LERP node that controls how visible the sky reflection is in the water:

<img width="1191" height="492" alt="image" src="https://github.com/user-attachments/assets/6ac6030c-b83f-496c-8e97-d72d5eb49249" />

<img width="1120" height="497" alt="image" src="https://github.com/user-attachments/assets/3366a1f3-37d1-4eb4-abc8-6724f207494c" />

This was used in the scene because in Contra there is water visible at the bottom of the screen, which conveys that the environment is set on an island to traverse through. The water though looks flat and uninteresting, it is simply a blue color with splash effects at the edges. To make the water look way more dynamic and realistic, the scrolling textures are used to convey that the water is slowly flowing by, and the reflection is used to add realism as the water given that it is clear and how light works reflects the sky (which in real life gives it its color). The skybox chosen is meant to be more serious and darker in tone, trying to match the night sky as seen in Contra.  So, the water is meant to be flowing and also reflect the sky to enhance the scene:

<img width="1420" height="767" alt="image" src="https://github.com/user-attachments/assets/2e5ab61a-0e0c-4a87-99c9-453b687c252a" />

<img width="760" height="517" alt="image" src="https://github.com/user-attachments/assets/c919c004-82fd-46dc-839d-8fe8b568a5bf" />

ALMOST ALL OF THE TEXTURES USED IN THIS PROJECT ARE MADE BY ME IN SUBSTANCE PAINTER 3D, AS FOR THE TREE SPRITES IT COMES FROM THIS WEBSITE FOR REFERENCE: 
https://opengameart.org/content/tree-collection-v26-bleeds-game-art
THE SKYBOX USED IN THE SCENE COMES FROM THIS FREE UNITY ASSET PACK: https://assetstore.unity.com/packages/2d/textures-materials/sky/skybox-series-free-103633
