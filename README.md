Below is the same text with only the formulas modified into proper GitHub Markdown formatting. All text has been preserved.

──────────────────────────────

**Introduction to Computer Graphics**

Concept:  
Computer Graphics is broadly defined as any use of computers to create images. At its core, this field involves modeling objects mathematically, transforming them through various operations, and ultimately producing images by mapping these models onto a discrete grid of pixels.

Mathematical Formulation:  
You can view an image as a function:  
  $$ I(x, y) = \text{color} $$  
where (x, y) are discrete pixel coordinates and color represents the pixel’s value. In a framebuffer (see below), the entire image is stored as a 2D array of these color values.

──────────────────────────────  
**2. Graphics Areas**

These slides divide computer graphics into several areas. Although the slides describe them conceptually, here are some of the core mathematical ideas behind each:

a. **Modeling**  
Concept:  
Modeling involves the mathematical representation of shapes and objects. This typically means describing curves, surfaces, and volumes using equations.

Formulas & Examples:

- *Points and Vectors:*  
  A point in 3D is given by:  
  $$ P = (x, y, z) $$

- *Lines (Parametric Form):*  
  Given two points, \(P_0\) and \(P_1\), a line can be defined as:  
  $$ L(t) = P_0 + t \cdot (P_1 - P_0) \quad \text{for } t \in [0, 1] $$

- *Curves (Bézier Curves):*  
  A quadratic Bézier curve defined by control points \(P_0\), \(P_1\), and \(P_2\) is given by:  
  $$ B(t) = (1 - t)^2 P_0 + 2t(1 - t) P_1 + t^2 P_2 \quad \text{for } t \in [0, 1] $$

- *Surfaces (Parametric Surfaces):*  
  A parametric surface might be defined as:  
  $$ S(u, v) = \bigl(x(u,v),\; y(u,v),\; z(u,v)\bigr) $$  
where \(u\) and \(v\) are parameters in a given range.

b. **Rendering**  
Concept:  
Rendering transforms a mathematical model into a visual image by computing shading, lighting, and color. Much of rendering is based on how light interacts with surfaces.

Common Shading Models and Their Formulas:

- *Lambertian (Diffuse) Reflection:*  
  For diffuse surfaces, the brightness (I) is proportional to the cosine of the angle between the surface normal (N) and the light direction (L):  
  $$ I_{\text{diffuse}} = I_0 \cdot (N \cdot L) $$  
where \(I_0\) is the light intensity and \((N \cdot L)\) represents the dot product (cosine of the angle).

- *Phong Reflection Model:*  
  A more comprehensive model that includes ambient, diffuse, and specular reflection:  
  $$ I = I_a K_a + I_d K_d (N \cdot L) + I_s K_s (R \cdot V)^n $$  
Here,  
  • \(I_a\), \(I_d\), \(I_s\) are the ambient, diffuse, and specular light intensities,  
  • \(K_a\), \(K_d\), \(K_s\) are the material’s reflection coefficients,  
  • \(N\) is the normalized surface normal,  
  • \(L\) is the normalized light direction,  
  • \(R\) is the reflection vector computed as  
    $$ R = 2 (N \cdot L) N - L $$  
  • \(V\) is the normalized view vector, and  
  • \(n\) is the shininess exponent controlling the size of the specular highlight.

c. **Animation**  
Concept:  
Animation is about generating a sequence of images that show change over time.

Key Mathematical Concept – Interpolation:  
For smooth transitions between keyframes, linear interpolation (lerp) is often used:  
  $$ P(t) = (1 - t) P_0 + t P_1 \quad \text{for } t \in [0, 1] $$  
For more sophisticated motion, spline interpolation (such as Bézier or B-splines) is employed. For instance, as given earlier for curves, Bézier formulas are used to interpolate between control points.

d. **Visualization**  
Concept:  
Visualization translates data into images in order to reveal structure or meaning. Although this slide primarily provides an overview, the concept relies on mapping numerical data to visual attributes (like position, color, and size) using well-defined functions.

──────────────────────────────  
**3. Graphics APIs and WebGL**

Concept:  
APIs, like OpenGL, Direct3D, and WebGL, provide libraries and routines to perform graphics rendering. WebGL in particular allows developers to write 3D graphics code using JavaScript and render in a web browser.

Mathematical Impact:  
While these APIs are software tools rather than mathematical theories, they implement many mathematical operations (e.g., transformation matrices, perspective projection) behind the scenes to transform models from world coordinates to screen coordinates. For example, a typical 4×4 transformation matrix is used in homogeneous coordinates:  
  $$ P' = M \cdot P $$  
where \(P\) is a 4D vector \((x, y, z, 1)\) and \(M\) encodes translation, rotation, and scaling.

──────────────────────────────  
**4. Raster Graphics, Framebuffer, and Rasterization**

a. **Raster Graphics and Framebuffer**  
Concept:  
Raster graphics represent images as arrays (grids) of pixels stored in a framebuffer. The resolution (detail) is determined by the number of pixels, and the color depth (precision) is determined by the number of bits per pixel.

Formulas:

- **Resolution:**  
  If the screen has width \(W\) and height \(H\), then the total number of pixels \(N\) is:  
    $$ N = W \times H $$

- **Color Depth:**  
  For a system with \(b\) bits per pixel, the total number of colors is:  
    $$ N_{\text{colors}} = 2^b $$  
Examples from the slides:  
  • 1-bit: \(2^1 = 2\) colors  
  • 8-bit: \(2^8 = 256\) colors  
  • Full-color (24-bit, typically 8-bit per RGB channel): \(2^{24} \approx 16.7\) million colors  
  • HDR (12-bit per channel is often cited): \(2^{12} = 4096\) colors per channel  
These formulas illustrate how increasing bit depth exponentially increases the number of colors that can be represented.

b. **Rasterization**  
Concept:  
Rasterization (or scan conversion) is the process of converting geometric primitives (like lines, circles, and triangles) defined in mathematical (vector) form into pixels that best approximate those primitives on the screen.

Key Examples and Formulas:

- **Line Drawing:**  
  A line between two points \((x_0, y_0)\) and \((x_1, y_1)\) is given by the line equation:  
  $$ y - y_0 = m (x - x_0) \quad \text{where } m = \frac{y_1 - y_0}{x_1 - x_0} $$  
Algorithms such as the Digital Differential Analyzer (DDA) or Bresenham’s algorithm use this idea to decide which pixels to light up.

- **Triangle Filling with Barycentric Coordinates:**  
  To decide if a pixel \((x, y)\) lies inside a triangle defined by vertices \(A\), \(B\), and \(C\), barycentric coordinates \((\alpha, \beta, \gamma)\) are calculated so that:  
  $$ P = \alpha A + \beta B + \gamma C \quad \text{with } \alpha + \beta + \gamma = 1 $$  
A point is inside the triangle if all \(\alpha\), \(\beta\), and \(\gamma\) are non-negative. One common formulation for these coordinates is:  
  $$ \alpha = \frac{\text{Area}(P, B, C)}{\text{Area}(A, B, C)} $$  
  $$ \beta = \frac{\text{Area}(P, C, A)}{\text{Area}(A, B, C)} $$  
  $$ \gamma = \frac{\text{Area}(P, A, B)}{\text{Area}(A, B, C)} $$

──────────────────────────────  
**5. CPU, GPU, and Output**

a. **CPU vs. GPU**  
Concept:  
Early graphics systems used a single processor (the CPU) for both general computations and graphics. Today, dedicated Graphics Processing Units (GPUs) perform parallelized calculations for tasks such as transforming vertices, shading, and rasterizing primitives.

Mathematical Note:  
While there is no “formula” for comparing a CPU to a GPU, the key idea is parallelism. For example, if a GPU has \(N\) cores, an operation that takes \(O(n)\) time on a CPU might be reduced to \(O\left(\frac{n}{N}\right)\) on a GPU when parallelized.

b. **Output and Display**  
Concept:  
Once the image is stored in the framebuffer, the output system displays the image on a monitor or screen.

Interlaced vs. Non-Interlaced Displays:

- **Non-Interlaced:**  
  The display is refreshed by scanning every row sequentially (row by row), so that the entire frame is updated at the refresh rate.

- **Interlaced:**  
  In an interlaced system, the display updates alternate lines (e.g., odd rows then even rows). This means that if the full refresh rate is \(R\), the effective complete redraw rate is:  
  $$ \text{Effective Refresh Rate} = \frac{R}{2} $$

c. **3D Displays**  
Concept:  
3D display techniques create the illusion of depth by showing two slightly different images—one for each eye. In stereo systems, these images are alternated rapidly or projected with different polarizations.

Stereo Vision (Conceptual Formula):  
One of the mathematical ideas behind stereo vision (used in 3D movie projection) involves calculating the disparity between the left-eye and right-eye images. An often-used relation (from stereo geometry) is:  
  $$ d = \frac{f \cdot B}{Z} $$  
where  
  • \(d\) is the disparity (difference in horizontal position of the same point in two images),  
  • \(f\) is the camera’s focal length,  
  • \(B\) is the baseline distance between the two viewpoints, and  
  • \(Z\) is the depth (distance from the camera).  
This formula underlies depth estimation algorithms, although it is only mentioned conceptually in the slides.

──────────────────────────────  
**6. Course Administration and Historical Context**

Some slides focus on course logistics (instructor information, grading, regulations, schedule) and a brief history of computer graphics development from the 1980s to the present. Although there are no mathematical formulas here, understanding the evolution of techniques (from wireframe models to photorealistic rendering) sets the stage for the deeper mathematical and algorithmic concepts that will follow later in the course.

──────────────────────────────  
**Summary**

The slides introduce several core topics in computer graphics:

• **Modeling** — using points, vectors, and parametric equations to represent objects.  
• **Rendering** — applying lighting models (like Lambertian and Phong reflection) to produce realistic images.  
• **Animation** — employing interpolation methods (linear and spline-based) to create motion.  
• **Raster Graphics & Framebuffers** — representing images as arrays of pixels, with formulas showing how resolution and bit depth determine image quality.  
• **Rasterization** — converting geometric primitives into pixel data using line equations, barycentric coordinates, etc.  
• **Hardware (CPU/GPU) and Display Systems** — leveraging parallel processing for graphics and understanding various refresh and 3D display techniques.

──────────────────────────────  

Feel free to use this Markdown text as needed.
