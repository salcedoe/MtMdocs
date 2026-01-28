# Volume and Surface Rendering using the Medical Volume Viewer

When dealing with image volumes, it is often useful to see "inside" the volume — that is, to construct 3D representations of internal structures inside that volume. 3D Rendering is the computer graphics process of converting 3D models into 2D images for display on a 2D computer screen. The process considers the positioning of the objects in a 3D scene and renders a 2D image based on this perspective. Any change in the view, such as rotating the scene, generates a new render to reflect the new perspective of the 3D scene, as shown below.

![viewing frustrum](images/viewing-frustrum.GIF){ width="250"}

>In 3D graphics, the **Viewing frustrum** is the computed view from a virtual camera, represented here as a truncated pyramid lying on its side. Notice the smaller end of the pyramid is closest to the camera, while the large end is further way, representing foreshortening. Everything between the near and far clip planes is the viewing area, and will be rendered. Here, the "near clip plane" represents what is rendered in the 3D Scene. If you move the position of the camera, you change the position of the viewing frustrum and render a different image. For example, if you rotate the camera to the right, the red cylinder would appear in front of the yellow sphere.

There are two main types of rendering that we deal with in this course:

- **Volume Rendering:** visualizes 3D structures by  adjusting the transparencies of the voxels of a 3D volume. Usually, the outer edge and background voxels are made completely transparent — to allow viewing inside the volume. Voxels contained within structures of interest are set to varying levels of opacity to reveal (or render) these structures.  In effect, each voxel in volume has a opacity setting based on its intensity value. These opacities are set using a lookup table called an alphamap, which maps opacity to intensity.

- **Surface rendering:** visualizes a surface model of an internal structure. For surface rendering, you first need to create a surface model, made up of vertices and triangular faces. In this method, only the surface is rendered, the rest of the volume is ignored. This technique is commonly used in medical imaging to visualize segmented structures like bones or organs.