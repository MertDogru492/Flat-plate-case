# Flat Plate Laminar Validation Case

This case was prepared to validate the laminar boundary layer solution over a flat plate using OpenFOAM 2312.

## Purpose

This case is used to check Cp, Cf, boundary layer profiles, and, if available, eN/Xtr outputs over a flat plate.

## Case Location

/home/flatplate/flatplate_laminar_en_L30

## Basic Run Procedure

source /usr/lib/openfoam/openfoam2312/etc/bashrc
cd /home/flatplate/flatplate_laminar_en_L30
blockMesh
checkMesh
simpleFoam

If an Allrun script is available:

./Allrun

## Plot Outputs

The plots are expected in the following directory:

FINAL_FLATPLATE_VALIDATION/plots

Expected files:

- Cf_flatplate.png
- Cp_flatplate.png
- Cp_Cf_flatplate.png
- cp_cf_flatplate.csv

Check with:

ls -lh FINAL_FLATPLATE_VALIDATION/plots

## Cf Validation

For a laminar flat plate, the theoretical local skin-friction coefficient is:

Cf_x = 0.664 / sqrt(Re_x)

where:

Re_x = U_inf * x / nu

The Cf curve should generally decrease along the x direction.

If Cf is zero or looks incorrect, check the following:

- Is the wall patch really defined as a wall?
- Was the wallShearStress output generated?
- Is the correct patch name used in the Cf calculation?
- Is U_inf correct?
- Is nu correct?
- Is the plotting script reading the correct file?
- Is the correct component of the wall shear stress vector being used?

## Cp Validation

For a flat plate at zero angle of attack, the pressure field should behave close to a zero-pressure-gradient flow. If the Cp plot shows large oscillations, check the mesh, boundary conditions, pressure reference, and solver convergence.

## Xtr / eN Check

If Xtr output exists, it should be checked in these files:

postProcessing/eN1/xtr.txt
postProcessing/eN1/sigma_of_x.csv

Check with:

cat postProcessing/eN1/xtr.txt
head postProcessing/eN1/sigma_of_x.csv

If the message "N did not reach Ncr" appears, the code has run, but transition was not found under the selected conditions.

## Note

Airfoil transition/Xtr results should not be trusted before the flat plate case gives correct Cf, Cp, and boundary layer behavior.
