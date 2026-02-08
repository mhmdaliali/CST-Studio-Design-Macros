# U-Shaped Meander Line Generator

A VBA macro for CST Studio Suite that automatically constructs meander transmission lines with U-shaped alternating half cells.

## Overview

This macro generates meander lines that extend along the x-direction. The meander structure consists of repeating U-shaped cells with configurable dimensions, providing a compact way to implement long transmission lines in constrained spaces.

> **Note:** The current version only supports x-direction extension. For other orientations, rotate the generated structure after creation.

## Parameters

### Required Inputs

| Parameter | Description | Unit |
|-----------|-------------|------|
| `mLine_xloc` | X-coordinate of line start point (trace center) | mm |
| `mLine_yloc` | Y-coordinate of line start point (trace center) | mm |
| `mLine_zloc` | Z-coordinate of line start point (trace center) | mm |
| `mLine_Lu` | Length of each U-arm | mm |
| `mLine_Ws` | Gap between meander steps | mm |
| `mLine_Wt` | Trace width | mm |
| `mLine_Pu` | Ucell Period | mm |
| `mLine_L` | Required total line extension | mm |
| `mt` | Metal thickness | mm |

### Computed Parameters

These parameters are automatically calculated based on the expressions in `Parameters.json`:

| Parameter | Expression | Description |
|-----------|------------|-------------|
| `mLine_Pu` | `mLine_Wt + mLine_Ws` | Period of one U-cell |
| `mLine_Nu` | `int((mLine_L - mLine_Wt) / mLine_Pu)` | Number of U-cells |
| `mLine_La` | `mLine_Nu * mLine_Pu + mLine_Wt` | Actual line extension achieved |
| `mLine_Lc` | `mLine_L - mLine_La` | Complementary flat length needed |

## Installation & Usage

### Step 1: Import the Macro

1. Open your CST project
2. Go to **Modeling** → **VBA Macros**
3. Import the `.mcs` macro file

### Step 2: Configure Parameters

1. Navigate to your project directory: `CST/yourProject/Model/`
2. Open or create `Parameters.json`
3. Add the meander line parameters from the provided `Parameters.json` template
4. Set parameter values according to your design requirements

### Step 3: Run the Macro

1. In CST, go to **Modeling** → **VBA Macros**
2. Select the meander line macro
3. Click **Run**

## Design Considerations

- **Start Point:** The coordinates (`mLine_xloc`, `mLine_yloc`, `mLine_zloc`) define the center of the trace at the starting point
- **Metal Thickness:** The structure extends from `mLine_zloc` to `mLine_zloc + mt`
- **Line Extension:** The actual extension `mLine_La` may differ slightly from the required `mLine_L` due to integer number of cells. Use `mLine_Lc` to add a straight section if exact length is critical
- **Orientation:** To create meander lines in other directions, generate the x-direction line first, then apply rotation transformations

## File Structure
```
yourProject/
├── Model/
│   ├── Parameters.json    # Parameter definitions
│   └── ...
└── meander_line.mcs       # VBA macro file
```

## Requirements

- CST Studio Suite

## License

MIT License

---

**Questions or Issues?** Please open an issue in the repository.
