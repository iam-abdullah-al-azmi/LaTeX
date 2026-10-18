# Finite Element Analysis of Stress Concentration in a Perforated Plate Under Tensile Loading

## Summary

Whenever a structural member contains a hole, notch or fillet, the load path can no longer run straight through it. The force lines bunch up and bend around the discontinuity, and the local stress rises well above the nominal stress, which is the load divided by the cross-sectional area. The ratio of the peak stress to the nominal stress is called the stress concentration factor, K<sub>t</sub>. It matters because fatigue cracks and fractures usually start at these points, not in the bulk of the part. For a small circular hole in a very wide plate under uniaxial tension, the classical Kirsch solution gives K<sub>t</sub> = 3, with the peak at the hole edge perpendicular to the load. In a plate of finite width the value changes with the ratio of hole diameter to plate width. Handbook curves, such as Peterson's, cover this simple case, but real components with irregular shapes and loads rarely have a closed-form answer.

This is why finite element analysis (FEA) is widely used. It divides the part into many small elements, solves the equilibrium equations over them, and returns the stress field. The answer depends on the mesh, though. Elements that are too coarse smear out the steep stress gradient at the hole and under-predict the peak. Elements of different shapes, such as quadrilaterals and triangles, also behave differently. A good FEA study therefore checks the mesh as well as the physics. This project, done for ME 4638: Computational Mechanics Lab, uses a plate with a central hole as a simple test case. The behaviour is well understood, so I could judge the mesh sensitivity of the model and the stress pattern it produced.

In this project I built a rectangular plate with a central circular hole in Ansys SpaceClaim and analysed it in Ansys Mechanical as a linear-elastic static problem in Structural Steel. The left edge was fixed and a uniform tensile pressure was applied to the right edge. I first ran the default mesh, which has a 30.115 mm element size and the Prime Quad Dominant method, and extracted six results: total deformation, equivalent (von Mises) stress, maximum and minimum principal stress, maximum shear stress and strain energy. I then refined the mesh with face sizing of 10 mm and 2.5 mm, and repeated both sizes with a triangular mesh method to compare element shapes. Finally, I doubled the applied pressure and repeated the whole mesh set. In every case the stress concentrates at the top and bottom of the hole, perpendicular to the load, and is lowest on the left and right sides of the hole. The default mesh gave a peak equivalent stress of 20,320 MPa, while the refined meshes gave about 32,700 to 33,000 MPa: 32,999 MPa for the 10 mm quadrilateral mesh, 32,945 MPa for 2.5 mm quadrilateral, 31,854 MPa for 10 mm triangular and 32,749 MPa for 2.5 mm triangular. The default mesh therefore under-predicts the peak by about 38%, and the refined meshes agree with each other within about 4%. With the default mesh, doubling the pressure doubled the peak stress to 40,639 MPa, as a linear model should. Dividing the refined peak by the applied pressure of 10,000 MPa gives K<sub>t</sub> of about 3.3. This is close to the roughly 3.2 I estimated from Peterson's finite-width formula, using the hole-to-width ratio of about 0.25 read from the screenshots.

The study has limits. The model is 2D and linear-elastic, so it ignores plasticity and thickness effects. The pressure appears as 10,000 MPa in Ansys instead of the 1 kPa and 2 kPa I intended. This is a unit mismatch, so the absolute stresses exceed the yield strength of steel and only the trends and the K<sub>t</sub> ratio are meaningful. The plate and hole dimensions were estimated from the screenshots, the mesh study covered only three element sizes, and I did not compare against experiment. Future work could fix the load units, record the exact dimensions, refine the mesh further near the hole, and compare the result with the analytical K<sub>t</sub> more carefully. It could also vary the hole size, add a plastic material model, and try a 3D model with thickness.

## Computational Design

The model is a flat rectangular plate with a circular hole at its centre. It was sketched in Ansys SpaceClaim as a 2D surface and analysed in Ansys Mechanical as a linear-elastic static problem. From the scale bar in the screenshots, the plate measures roughly 300 mm x 200 mm and the hole is roughly 50 mm in diameter. The material is the default Structural Steel. The left edge is a fixed support, and a uniform tensile pressure acts on the right edge.

| View  |                           Image                            |
| :---: | :--------------------------------------------------------: |
| Front | ![Front View](images/Screenshot%202026-10-16%20104924.png) |
| Back  | ![Back View](images/Screenshot%202026-10-16%20104924.png)  |

## Finite Element Analysis

### Analysis Settings

The baseline study uses the default mesh. Ansys sets the element size to 30.115 mm and meshes the surface with the Prime Quad Dominant method, so the elements are mostly quadrilaterals. The material is Structural Steel. The left edge is a fixed support and a pressure acts on the right edge. The model is solved as a static structural analysis, and the six results are total deformation, equivalent stress, maximum and minimum principal stress, maximum shear stress and strain energy. The peak equivalent stress here is 20,320 MPa. The pressure is shown as 10,000 MPa, a unit mismatch discussed under Limitations.

<!-- Default Mesh -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/Screenshot%202026-10-16%20105909.png)  |
|  Model  | ![Model](images/Screenshot%202026-10-16%20105919.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20105935.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20110014.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20110022.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20110029.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20110037.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20110043.png)       |

## Optimization

The optimization here is a mesh study. Using the same geometry, material and boundary conditions, I changed only the element size and shape. Face sizing of 10 mm and 2.5 mm was applied, first with the default quadrilateral-dominant mesh and then with the Triangles Method, to see how the peak stress responds. The refined meshes give a peak equivalent stress of about 32,700 to 33,000 MPa, against 20,320 MPa on the default mesh. The 10 mm and 2.5 mm meshes agree with each other, so the 10 mm mesh already captures the peak. After that, the same set of meshes was repeated at double the pressure, and the stresses scaled proportionally.

<!-- Mesh: 10 mm -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/Screenshot%202026-10-16%20110222.png)  |
|  Model  | ![Model](images/Screenshot%202026-10-16%20110231.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20110237.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20110242.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20110247.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20110255.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20110307.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20110312.png)       |

<!-- Mesh: 2.5 mm -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/Screenshot%202026-10-16%20110100.png)  |
|  Model  | ![Model](images/Screenshot%202026-10-16%20110115.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20110123.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20110128.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20110136.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20110142.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20110148.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20110154.png)       |

<!-- Mesh: Triangular 10 mm -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/Screenshot%202026-10-16%20111000.png)  |
|  Model  | ![Model](images/Screenshot%202026-10-16%20110115.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20111018.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20111024.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20111031.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20111037.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20111042.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20111049.png)       |

<!-- Mesh: Triangular 2.5 mm -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/Screenshot%202026-10-16%20110849.png)  |
|  Model  | ![Model](images/Screenshot%202026-10-16%20110115.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20110902.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20110910.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20110917.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20110922.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20110929.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20110935.png)       |

<!-- End: Pressure: 1 KPa -->

<!-- Default Mesh, Pressure: 2 KPa -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/Screenshot%202026-10-16%20111252.png)  |
|  Model  | ![Model](images/Screenshot%202026-10-16%20111302.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20111309.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20111314.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20111320.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20111327.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20111332.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20111339.png)       |

<!-- Mesh: 10 mm -->

| Setting |                        Image                         |
| :-----: | :--------------------------------------------------: |
|  Mesh   | ![Mesh](images/Screenshot%202026-10-16%20111521.png) |
|  Model  |                  ![Model](images/)                   |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20111538.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20111545.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20111559.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20111606.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20111612.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20111617.png)       |

<!-- Mesh: 2.5 mm -->

| Setting |       Image       |
| :-----: | :---------------: |
|  Mesh   | ![Mesh](images/)  |
|  Model  | ![Model](images/) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20111418.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20111425.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20111433.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20111443.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20111450.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20111456.png)       |

<!-- Mesh: Triangular 10 mm -->

| Setting |       Image       |
| :-----: | :---------------: |
|  Mesh   | ![Mesh](images/)  |
|  Model  | ![Model](images/) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20111822.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20111829.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20111836.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20111843.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20111849.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20111853.png)       |

<!-- Mesh: Triangular 2.5 mm -->

| Setting |       Image       |
| :-----: | :---------------: |
|  Mesh   | ![Mesh](images/)  |
|  Model  | ![Model](images/) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/Screenshot%202026-10-16%20111706.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/Screenshot%202026-10-16%20111713.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/Screenshot%202026-10-16%20111720.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/Screenshot%202026-10-16%20111727.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/Screenshot%202026-10-16%20111735.png)   |
|      Strain Energy       |      ![Strain Energy](images/Screenshot%202026-10-16%20111743.png)       |

## Software Used

|                 Purpose                  |              Name               |
| :--------------------------------------: | :-----------------------------: |
| Design and Finite Element Analysis (FEA) | Ansys (Student Version 2026 R1) |

## Limitations

- **Dimensionality and material:** The model is a 2D surface with linear-elastic Structural Steel, so it cannot capture yielding, plasticity or through-thickness effects.
- **Load units:** The applied pressure appears as 10,000 MPa in Ansys instead of the intended 1 kPa and 2 kPa. The absolute stresses exceed the yield strength of steel and are not physically meaningful. Only the relative trends and stress patterns are reliable.
- **Mesh convergence:** I compared only the default mesh, 10 mm and 2.5 mm. The peak stress still differs between meshes and element types, so a converged value was not established.
- **Peak stress locations:** The maximum stress sits at a single node at the hole edge, so it is the quantity most sensitive to the mesh. The stress contours are averaged, which smooths the peak.
- **No validation:** The results were not compared against an analytical stress concentration factor or experimental data.
- **Geometry documentation:** The plate and hole dimensions were not recorded in the sketch screenshots, and the back-view image duplicates the front view.
- **Single configuration:** Only one hole size and one boundary-condition set were studied.

## Future Improvements

- Correct the load units so that the pressure is 1 kPa and 2 kPa as intended, and recheck that the stresses are physically meaningful.
- Record the exact plate and hole dimensions in the sketch, and calculate K<sub>t</sub> against the handbook value.
- Add finer refinement near the hole edge, for example 1 mm and 0.5 mm, to confirm a converged peak.
- Vary the hole diameter and shape, such as ellipses or multiple holes, to see how K<sub>t</sub> changes.
- Add a plastic material model and a 3D model with thickness.
- Check the result against a hand calculation or an experiment.

## Acknowledgements

I am really grateful to our faculty member, Sefat Mahmud Siddique, Junior Lecturer, MPE, for his valuable instruction in ME 4638: Computational Mechanics Lab.

## References
