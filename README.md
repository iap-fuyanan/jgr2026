# CM1 Simulation Configuration and Input Data

This repository contains the essential input configuration files, initial atmospheric soundings, and terrain datasets required to replicate the high-resolution numerical simulations conducted in our study. All simulations were performed using Cloud Model 1 (CM1; version 21.1).

---

## 1. Terrain Datasets

The simulation domain covers an $800\text{ km} \times 800\text{ km}$ region. Two types of topography configurations are provided:

* **`TerrainElevation_500m_800km_800km_112.0E_31.0N.npy`** * **Description:** This file contains the **realistic terrain data** derived from the SRTM dataset and processed via a Gaussian filter. It is formatted as a Python NumPy saved object. 
    * **Data Structure:** Loading this `.npy` file yields a **Python tuple containing three 2D arrays**: `(longitude_grid, latitude_grid, terrain_elevation)`. 
    * **Domain Specification:** The grid has a uniform horizontal resolution of **$500\text{ m}$** and is **centered at $112.0^\circ\text{E}, 31.0^\circ\text{N}$**.
    * **Usage:** Specifically employed to initialize the **REAL experiment** (Validation run).

* **`perts.dat`** * **Description:** This file contains the **idealized, quasi-two-dimensional terrain profile** mathematically defined by a piecewise half-cosine function.
    * **Usage:** Applied across all idealized sensitivity simulations, including the **CTRL, EXP_S, EXP_SW, and EXP_VWS experiments**.

---

## 2. Initial Sounding Files

The thermodynamic and kinematic profiles are formatted in the standard CM1 input sounding structure (`input_sounding`). 

* **`input_sounding_original`** * **Description:** The **raw, unaltered early-morning sounding** observed at the Wuhan Meteorological Station (ID: 57494) at 0000 UTC on 4 July 2018.

* **`input_sounding_ctrl`** * **Description:** The **thermodynamically adjusted sounding profile**. The early-morning surface inversion layer was modified based on 0600 UTC surface observations to produce a well-defined dry-adiabatic mixed layer, approximating the afternoon pre-convective state.
    * **Usage:** Used as the base-state environment for both the **REAL and CTRL experiments**.

* **`input_sounding_exp_s`** * **Description:** Modified from `input_sounding_ctrl`. The boundary-layer southeasterlies within the lowest $1000\text{ m}$ above the surface are **modified into pure southerlies** by setting the negative zonal wind component to zero.
    * **Usage:** Explicitly used for the **EXP_S experiment**.

* **`input_sounding_exp_sw`** * **Description:** Modified from `input_sounding_ctrl`. The boundary-layer winds within the lowest $1000\text{ m}$ above the surface are **modified into southwesterlies ($225^\circ$)** while maintaining the original wind speed.
    * **Usage:** Explicitly used for the **EXP_SW experiment**.

* **`input_sounding_exp_vws`** * **Description:** Modified from `input_sounding_ctrl`. A **uniform zonal wind of $3\text{ m s}^{-1}$ is added throughout the entire vertical layer** to completely eliminate the boundary-layer zonal easterlies while preserving the identical vertical wind shear as in the CTRL run.
    * **Usage:** Explicitly used for the **EXP_VWS experiment**.

---

## 3. Simulation Namelist

* **`namelist.input`** * **Description:** Contains the core model configurations, including the third-order Runge–Kutta time integration scheme, fifth-order advection, WENO scalar advection option, the 1.5-order subgrid-scale TKE closure, and the Morrison double-moment microphysics scheme. (Note: Please rename the specific configurations or replace the sounding file names in this namelist according to the respective experiment you wish to replicate).

---

## How to Cite
If you use these datasets or configuration files in your research, please cite our peer-reviewed paper:
*[Insert your paper citation here once published]*
