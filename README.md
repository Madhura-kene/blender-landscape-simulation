#  Scene 2 - Blender Landscape & Physics Simulation

A detailed natural landscape scene created in **Blender 5.1.x** featuring terrain geometry, water simulation (dynamic paint ripples + ocean waves), high-poly tree models, and a particle system distribution.

---

##  Scene Statistics & Settings

### Render Configurations
* **Render Engine:** `CYCLES` (Path Tracing)
* **Resolution:** `1920 x 1080` (Full HD, 16:9 ratio) at `100%` render scale
* **Frame Range:** `1` to `250` (250 frames total — *10.4 seconds of animation at 24fps*)
* **Frame Rate:** `24 FPS` (Standard Cinematic)

### Polycount & Object Breakdown
* **Total Objects:** 32
* **Total Static Polygons:** ~2.45 Million polygons *(prior to Ocean modifier & Particle displacement)*
* **Objects by Type:**
  * **Mesh Objects (`MESH`):** 30
  * **Camera Objects (`CAMERA`):** 1 (focal length: 30mm)
  * **Light Objects (`LIGHT`):** 1 (Sun light, Strength: 1.0)

---

##  Scene Hierarchy & Collections

```
Scene Collection
└── Collection
    ├── Camera (Focal Length: 30mm, Perspective)
    ├── Sun (Directional Light, Energy: 1.0, White)
    ├── Plane (Ground / Particle Emitter)
    ├── Plano (Water Surface / Dynamic Paint & Ocean)
    ├── Landscape.001 (Terrain mesh)
    ├── Landscape.002 (Terrain mesh)
    ├── Landscape.005 (Background mountain mesh)
    ├── tree.001 - tree.025 (25 High-detail oak trees)
    └── rumput (Sub-Collection / Grass - currently empty)
```

---

##  Modifiers & Physics Simulations

This scene makes heavy use of physics caching to simulate natural elements. The physics cache is stored in the `blendcache_scene2` folder.

### 1. `Plano` (Water Surface)
* **Modifiers:** 
  1. **Oceano (Ocean):** Generates realistic ocean waves.
  2. **Subsurf (Subdivision Surface):** High-density tessellation for wave detail.
  3. **Pintura dinâmica (Dynamic Paint):** Configured as a Canvas to receive ripple brushes/physics.
* **Physics Cache:** Pre-calculated simulation frames are saved as `.bphys` files inside `blendcache_scene2`. The cache filename prefix `506C616E6F` is the hexadecimal representation of the object's name: **`Plano`**.

### 2. `Plane` (Ground / Particle Emitter)
* **Geometry:** Very high-density ground grid containing `743,044` vertices and `741,321` polygons.
* **Modifiers:**
  1. **ParticleSystem:** Set up as a hair/instancing system (likely distributing grass assets from the `rumput` collection or temporary directories).

---

##  Materials & Texture Audit

The scene references 5 node-based materials. Several external textures are linked, some of which use **absolute paths** that may need updating on your system:

| Material Name | Assigned To | Linked Textures / References | Status |
| :--- | :--- | :--- | :--- |
| **`Materiais.001`** | `Plano` (Water) | *Procedural shader nodes* | `OK` (Self-contained) |
| **`Material.001`** | Landscapes | `rocky_terrain_03_diff_4k.jpg`<br>`rocky_terrain_03_rough_4k.exr`<br>`rocky_terrain_03_nor_gl_4k.exr` | `OK` (Relative to `//rocky_terrain_03_4k.blend`) |
| **`Material.010`** | Oak Trees | `jolcham_oak_bark_01_diff_4k.jpg`<br>`jolcham_oak_bark_01_disp_4k.png`<br>`jolcham_oak_bark_01_nor_gl_4k.exr` | `OK` (Relative to `//jolcham_oak_bark_01_4k.blend`) |
| **`Material.011`** | `Plane` (Ground) | *Procedural shader nodes* | `OK` (Self-contained) |
| **`World Environment`** | World background | `cloud_layers_4k.exr` | `OK` (Relative `//cloud_layers_4k.exr`) |

###  Attention Required: Potentially Broken File Paths
Blender's file structure database indicates that the following image assets are mapped to local directories that may not exist on your computer:
1. **Tree Bark Texture (`BarkDecidious0194_7_S.jpg`):**
   * *Path:* `D:\Models\1f9jtr180dxk-Tree1ByTyroSmith\Tree1\BarkDecidious0194_7_S.jpg`
   * *Resolution:* Extract the file `1f9jtr180dxk-Tree1ByTyroSmith.zip` in your downloads and remap the path.
2. **Grass Textures (`Grass1.jpg`, `Grass2.jpg`):**
   * *Path:* `C:\Users\Madhura\AppData\Local\Temp\0e3ae81c-87be-45c0-96dd-4acd8d87fb41_24-grass.rar.b41\Texture\...`
   * *Resolution:* These point to a Windows temporary directory. Extract the `24-grass.rar` file to your working directory and remap them.

---

##  How to Open & Configure the Scene

### 1. Requirements
* **Blender Version:** Blender **5.1.x** is recommended. The file uses compression and structural features that may fail to read in Blender versions prior to 5.0 (which will return a *"not a blend file"* error).

### 2. Remapping Missing Textures
If the landscapes or trees render pink (indicating missing textures):
1. Open the file in Blender.
2. Go to **File** ➔ **External Data** ➔ **Find Missing Files**.
3. Choose your downloads directory (where your texture folders like `jolcham_oak_bark_01_4k.blend` and `rocky_terrain_03_4k.blend` are extracted).
4. Blender will recursively scan and re-anchor the paths.
5. Go to **File** ➔ **External Data** ➔ **Make Paths Relative** to ensure the scene remains portable.

### 3. Caching Physics & Dynamic Paint
To run or render the water ripple animation:
* Ensure the `blendcache_scene2` folder is in the **same directory** as `scene2.blend`.
* If the ripples do not animate, select the `Plano` object, navigate to the **Physics Properties** tab, find the **Dynamic Paint** section under *Canvas*, and click **Reload Cache** or **Bake**.

---
*Document generated automatically using background inspection analysis tools on June 26, 2026.*
