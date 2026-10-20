# Finite Element Analysis of Stress Concentration in a Perforated Plate Under Tensile Loading

## Summary

Holes raise local stress above the nominal value, and fatigue cracks usually start there. Finite element analysis (FEA) predicts this stress concentration, but its accuracy depends on the mesh. A rectangular plate with a central circular hole was modelled in Ansys SpaceClaim and analysed in Ansys Mechanical as a linear-elastic static problem in Structural Steel. The left edge was fixed, and a uniform tensile pressure of 100 kPa was applied to the right edge. Default, 10 mm and 2.5 mm quadrilateral meshes and two triangular meshes were compared, and the pressure was doubled. The default mesh under-predicted the peak stress at the hole by about 38%, whereas the refined meshes agreed within 4%, giving a stress concentration factor of about 3.3. The model was two-dimensional, the load units were inconsistent, and no validation was performed. Future work should correct the units, refine the mesh, and validate analytically.

## Computational Design

| View  |                     Image                      |
| :---: | :--------------------------------------------: |
| Front | ![Front View](images/computational_design.png) |
| Back  | ![Back View](images/computational_design.png)  |

## Finite Element Analysis

### Analysis Settings

<!-- Default Mesh -->

| Setting |                          Image                           |
| :-----: | :------------------------------------------------------: |
|  Mesh   |  ![Mesh](images/default_100kpa_mesh.png)  |
|  Model  | ![Model](images/default_100kpa_model.png) |

|          Result          |                                     Image                                     |
| :----------------------: | :---------------------------------------------------------------------------: |
|    Total Deformation     | ![Total Deformation](images/default_100kpa_total_deformation.png) |
|    Equivalent Stress     |       ![Equivalent Stress](images/default_100kpa_equivalent_stress.png)       |
| Maximum Principal Stress |   ![Maximum Principal Stress](images/default_100kpa_max_principal_stress.png)    |
| Minimum Principal Stress |   ![Minimum Principal Stress](images/default_100kpa_min_principal_stress.png)    |
|   Maximum Shear Stress   |     ![Maximum Shear Stress](images/default_100kpa_max_shear_stress.png)      |
|      Strain Energy       |         ![Strain Energy](images/default_100kpa_strain_energy.png)         |

## Optimization

<!-- Mesh: 10 mm -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/quad_10mm_100kpa_mesh.png)  |
|  Model  | ![Model](images/quad_10mm_100kpa_model.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/quad_10mm_100kpa_total_deformation.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/quad_10mm_100kpa_equivalent_stress.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/quad_10mm_100kpa_max_principal_stress.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/quad_10mm_100kpa_min_principal_stress.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/quad_10mm_100kpa_max_shear_stress.png)   |
|      Strain Energy       |      ![Strain Energy](images/quad_10mm_100kpa_strain_energy.png)       |

<!-- Mesh: 2.5 mm -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/quad_2p5mm_100kpa_mesh.png)  |
|  Model  | ![Model](images/quad_2p5mm_100kpa_model.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/quad_2p5mm_100kpa_total_deformation.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/quad_2p5mm_100kpa_equivalent_stress.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/quad_2p5mm_100kpa_max_principal_stress.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/quad_2p5mm_100kpa_min_principal_stress.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/quad_2p5mm_100kpa_max_shear_stress.png)   |
|      Strain Energy       |      ![Strain Energy](images/quad_2p5mm_100kpa_strain_energy.png)       |

<!-- Mesh: Triangular 10 mm -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/tri_10mm_100kpa_mesh.png)  |
|  Model  | ![Model](images/quad_2p5mm_100kpa_model.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/tri_10mm_100kpa_total_deformation.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/tri_10mm_100kpa_equivalent_stress.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/tri_10mm_100kpa_max_principal_stress.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/tri_10mm_100kpa_min_principal_stress.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/tri_10mm_100kpa_max_shear_stress.png)   |
|      Strain Energy       |      ![Strain Energy](images/tri_10mm_100kpa_strain_energy.png)       |

<!-- Mesh: Triangular 2.5 mm -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/tri_2p5mm_100kpa_mesh.png)  |
|  Model  | ![Model](images/quad_2p5mm_100kpa_model.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/tri_2p5mm_100kpa_total_deformation.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/tri_2p5mm_100kpa_equivalent_stress.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/tri_2p5mm_100kpa_max_principal_stress.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/tri_2p5mm_100kpa_min_principal_stress.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/tri_2p5mm_100kpa_max_shear_stress.png)   |
|      Strain Energy       |      ![Strain Energy](images/tri_2p5mm_100kpa_strain_energy.png)       |

<!-- End: Pressure: 100 kPa -->

<!-- Default Mesh, Pressure: 200 kPa -->

| Setting |                         Image                         |
| :-----: | :---------------------------------------------------: |
|  Mesh   | ![Mesh](images/default_200kpa_mesh.png)  |
|  Model  | ![Model](images/default_200kpa_model.png) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/default_200kpa_total_deformation.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/default_200kpa_equivalent_stress.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/default_200kpa_max_principal_stress.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/default_200kpa_min_principal_stress.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/default_200kpa_max_shear_stress.png)   |
|      Strain Energy       |      ![Strain Energy](images/default_200kpa_strain_energy.png)       |

<!-- Mesh: 10 mm -->

| Setting |                        Image                         |
| :-----: | :--------------------------------------------------: |
|  Mesh   | ![Mesh](images/quad_10mm_200kpa_mesh.png) |
|  Model  |                  ![Model](images/)                   |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/quad_10mm_200kpa_total_deformation.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/quad_10mm_200kpa_equivalent_stress.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/quad_10mm_200kpa_max_principal_stress.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/quad_10mm_200kpa_min_principal_stress.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/quad_10mm_200kpa_max_shear_stress.png)   |
|      Strain Energy       |      ![Strain Energy](images/quad_10mm_200kpa_strain_energy.png)       |

<!-- Mesh: 2.5 mm -->

| Setting |       Image       |
| :-----: | :---------------: |
|  Mesh   | ![Mesh](images/)  |
|  Model  | ![Model](images/) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/quad_2p5mm_200kpa_total_deformation.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/quad_2p5mm_200kpa_equivalent_stress.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/quad_2p5mm_200kpa_max_principal_stress.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/quad_2p5mm_200kpa_min_principal_stress.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/quad_2p5mm_200kpa_max_shear_stress.png)   |
|      Strain Energy       |      ![Strain Energy](images/quad_2p5mm_200kpa_strain_energy.png)       |

<!-- Mesh: Triangular 10 mm -->

| Setting |       Image       |
| :-----: | :---------------: |
|  Mesh   | ![Mesh](images/)  |
|  Model  | ![Model](images/) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/tri_10mm_200kpa_total_deformation.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/tri_10mm_200kpa_equivalent_stress.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/tri_10mm_200kpa_max_principal_stress.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/tri_10mm_200kpa_min_principal_stress.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/tri_10mm_200kpa_max_shear_stress.png)   |
|      Strain Energy       |      ![Strain Energy](images/tri_10mm_200kpa_strain_energy.png)       |

<!-- Mesh: Triangular 2.5 mm -->

| Setting |       Image       |
| :-----: | :---------------: |
|  Mesh   | ![Mesh](images/)  |
|  Model  | ![Model](images/) |

|          Result          |                                  Image                                   |
| :----------------------: | :----------------------------------------------------------------------: |
|    Total Deformation     |    ![Total Deformation](images/tri_2p5mm_200kpa_total_deformation.png)     |
|    Equivalent Stress     |    ![Equivalent Stress](images/tri_2p5mm_200kpa_equivalent_stress.png)     |
| Maximum Principal Stress | ![Maximum Principal Stress](images/tri_2p5mm_200kpa_max_principal_stress.png) |
| Minimum Principal Stress | ![Minimum Principal Stress](images/tri_2p5mm_200kpa_min_principal_stress.png) |
|   Maximum Shear Stress   |   ![Maximum Shear Stress](images/tri_2p5mm_200kpa_max_shear_stress.png)   |
|      Strain Energy       |      ![Strain Energy](images/tri_2p5mm_200kpa_strain_energy.png)       |

## Software Used

|                 Purpose                  |              Name               |
| :--------------------------------------: | :-----------------------------: |
| Design and Finite Element Analysis (FEA) | Ansys (Student Version 2026 R1) [7] |

## Limitations

- **Dimensionality and material:** The model is a 2D surface with linear-elastic Structural Steel, so it cannot capture yielding, plasticity or through-thickness effects.
- **Load units:** The applied pressure appears as 10,000 MPa in Ansys instead of the intended 100 kPa (and 20,000 MPa instead of 200 kPa). The absolute stresses therefore exceed the yield strength of steel and are not physically meaningful. Only the relative trends, the stress patterns and the stress concentration factor are reliable.
- **Mesh convergence:** Only the default mesh, 10 mm and 2.5 mm face sizes were compared. The peak stress still differs between meshes and element types (31,854 to 32,999 MPa), so a converged value was not established.
- **Peak stress location:** The maximum stress sits at a single node at the hole edge, so it is the quantity most sensitive to the mesh. The averaged contour display smooths the peak.
- **No validation:** The results were not compared quantitatively against a handbook stress concentration factor [1], the classical analytical solutions [2], [3], [6] or experimental data.
- **Geometry documentation:** The plate and hole dimensions were not recorded in the sketch screenshots and were estimated from the scale bar. The back-view image also duplicates the front view.
- **Single configuration:** Only one hole size, one hole shape and one boundary-condition set were studied.
- **Missing screenshots:** Some mesh and model images for the 200 kPa cases were not captured. They are identical to the 100 kPa meshes and are left blank.

## Future Improvements

- Correct the load units so that the pressure is 100 kPa and 200 kPa as intended, and recheck that the stresses are physically meaningful.
- Record the exact plate and hole dimensions in the sketch, and compare the computed K<sub>t</sub> with the handbook value [1], [2].
- Refine the mesh near the hole edge, for example to 1 mm and 0.5 mm, and use a mesh convergence study [4], [5] to confirm a converged peak.
- Vary the hole diameter and shape, such as ellipses or multiple holes, to see how K<sub>t</sub> changes.
- Add a plastic material model and a 3D model with thickness.
- Check the result against a hand calculation or a physical tensile test.

## Acknowledgements

I am really grateful to our faculty member, Sefat Mahmud Siddique, Junior Lecturer, MPE, for his valuable instruction in ME 4638: Computational Mechanics Lab.

## References

1. W. D. Pilkey, D. F. Pilkey and Z. Bi, *Peterson's Stress Concentration Factors*, 4th ed. Hoboken, NJ, USA: Wiley, 2020.
2. S. P. Timoshenko and J. N. Goodier, *Theory of Elasticity*, 3rd ed. New York, NY, USA: McGraw-Hill, 1970.
3. G. Kirsch, "Die Theorie der Elastizität und die Bedürfnisse der Festigkeitslehre," *Zeitschrift des Vereines Deutscher Ingenieure*, vol. 42, pp. 797-807, 1898.
4. R. D. Cook, D. S. Malkus, M. E. Plesha and R. J. Witt, *Concepts and Applications of Finite Element Analysis*, 4th ed. New York, NY, USA: Wiley, 2002.
5. O. C. Zienkiewicz, R. L. Taylor and J. Z. Zhu, *The Finite Element Method: Its Basis and Fundamentals*, 7th ed. Oxford, UK: Butterworth-Heinemann, 2013.
6. R. C. Howland, "On the stresses in the neighbourhood of a circular hole in a strip under tension," *Philosophical Transactions of the Royal Society of London, Series A*, vol. 229, pp. 49-86, 1930.
7. Ansys, Inc., *Ansys Mechanical User's Guide*, Release 2026 R1. Canonsburg, PA, USA: Ansys, Inc., 2026.
