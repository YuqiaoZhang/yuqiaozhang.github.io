## SVO  

[GigaVoxels](http://gigavoxels.inrialpes.fr/index.html)  


## Cone Tracing

[GigaVoxels](http://gigavoxels.inrialpes.fr/index.html) "Data/Shaders/rayCastFrag.glsl"

## Tips

### Geometry Shader
By \[Harris 2019\], the geometry shader is hostile to the performance for mobile GPU.  
Besides, for Mali GPU, the geometry shader is not supported by the hardware and is emulated by the compute shader. And since the number of the vertices produced by a single geometry shader may vary, a parallel scan pass is required to perform the prefix sum.  
The normals may be calculated when the vertices are loaded. It must be ensured that the normals of the vertices of the same triangle are the same. For example, if a vertex is shared by multiple triangles, new vertices with different normals may be created for different triangles.  

### Conservative Rasterization
\[Hasselgren 2005\] may be replaced by "VK_EXT_conservative_rasterization"  

### Atomic Read-Modify-Write Operation
The atomic read-modify-write operation may be replaced by "VK_EXT_fragment_shader_interlock" or "GL_EXT_shader_framebuffer_fetch"  

## Reference  
\[Crassin 2011\] [Cyril Crassin. "GigaVoxels: A Voxel-Based Rendering Pipeline For Efficient Exploration Of Large And Detailed Scenes." PhD Thesis 2011](http://gigavoxels.inrialpes.fr/index.html)  
\[Lin 2013] [heng-Tso Lin. "Implementing Sparse Voxel Octree." JCGT 2013](https://github.com/otaku690/SparseVoxelOctree)  
\[Crassin 2009\] [Cyril Crassin, Fabrice Neyret, Sylvain Lefebvre, Elmar Eisemann. "GigaVoxels: Ray-Guided Streaming for Efficient and Detailed Voxel Rendering." SIGGRAPH 2009.](https://maverick.inria.fr/Publications/2009/CNLE09/CNLE09.pdf)  
\[Crassin 2010\] Cyril Crassin, Fabrice Neyret, Miguel Sainz, Elmar Eisemann. "Part X. 3. Efficient Rendering of Highly Detailed Volumetric Scenes with GigaVoxels." GPU Pro 2010.  
\[Crassin 2012\] [Cyril Crassin, Simon Green. "Chapter 22. Octree-Based Sparse Voxelization Using The GPU Hardware Rasterizer." OpenGL Insights 2012.](https://research.nvidia.com/publication/octree-based-sparse-voxelization-using-gpu-hardware-rasterizer)  
\[Crassin 2011\] [Cyril Crassin, Fabrice Neyret, Miguel Sainz, Simon Green, Elmar Eisemann. "Interactive Indirect Illumination Using Voxel Cone Tracing." SIGGRAPH 2011.](https://research.nvidia.com/publication/interactive-indirect-illumination-using-voxel-cone-tracing)  
\[Hoetzlein 2016\] Rama Hoetzlein. "GVDB: Raytracing Sparse Voxel Database Structures on the GPU." HPG 2016.  
\[Hasselgren 2005\] [Jon Hasselgren, Tomas Akenine-Moller, Lennart Ohlsson. "Chapter 42. Conservative Rasterization." GPU Gems 2.](https://developer.nvidia.com/gpugems/gpugems2/part-v-image-oriented-computing/chapter-42-conservative-rasterization)  
\[Harris 2019\] [Pete Harris. "Arm Mali GPUs Best Practices Developer Guide." ARM Developer 2019.](https://developer.arm.com/solutions/graphics/developer-guides/mali-gpu-best-practices)  