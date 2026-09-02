# UTL Gerber2CTB

**English** | [繁體中文](./README_zh.md)


Browser-based Gerber-to-CTB converter for PCB UV exposure using the **Phrozen Sonic Mighty 8K**.

## 📚 Overview

UTL Gerber2CTB converts Gerber ZIP files exported from **EasyEDA Standard Edition** into CTB exposure files for PCB UV exposure on the **Phrozen Sonic Mighty 8K**. The complete conversion runs locally in the browser and includes copper-layer selection, GKO-based masking, drill exposure control, preview, and CTB export.

Designed for Gerber ZIP files exported from **EasyEDA Standard Edition**. The tool reads PCB copper, board-outline, and selected drill data, generates exposure previews, and exports a CTB file for the Mighty 8K.

**Online tool:**  
https://long-jun.github.io/UTL_Gerber2CTB/

Originally developed for PCB fabrication and UV-exposure experiments in the UTL Lab at National Taipei University of Technology (NTUT).

---

## 🔄 Workflow

```text
EasyEDA Standard
      ↓
Export Gerber ZIP
      ↓
Upload to UTL Gerber2CTB
      ↓
Select Top / Bottom Copper
      ↓
Set total exposure time
      ↓
Configure GKO expansion and drill exposure
      ↓
Check PCB ZOOM and LCD FULL FRAME
      ↓
Download CTB
      ↓
Phrozen Sonic Mighty 8K
```

---

## ✨ Features

- Designed for **EasyEDA Standard Edition** Gerber ZIP exports
- Top Copper / Bottom Copper selection
- Automatic closed-board-outline detection from GKO
- Adjustable GKO exposure expansion
- Negative-polarity PCB exposure mask
- Independent drill exposure options for:
  - `PTH_Through.DRL`
  - `NPTH_Through.DRL`
  - `PTH_Through_Via.DRL`
- Drill diameters are read from Excellon tool definitions
- PCB ZOOM preview for detailed inspection
- LCD FULL FRAME preview for placement inspection
- Automatic centering on the 7680 × 4320 Mighty 8K LCD
- Browser-side CTB generation
- No server-side Gerber processing

---

## 🚀 How to Use

### 1. Export Gerber ZIP from EasyEDA Standard

Open the PCB project in **EasyEDA Standard Edition** and export the fabrication Gerber files as a ZIP package.

A typical EasyEDA ZIP may contain:

```text
Gerber_TopLayer.GTL
Gerber_BottomLayer.GBL
Gerber_BoardOutlineLayer.GKO
Drill_PTH_Through.DRL
Drill_NPTH_Through.DRL
Drill_PTH_Through_Via.DRL
```

Copper and board-outline files are required for the normal workflow. Drill files are optional and can be enabled independently.

### 2. Open UTL Gerber2CTB

Open:

https://long-jun.github.io/UTL_Gerber2CTB/

No software installation is required.

### 3. Upload the Gerber ZIP

Drag the ZIP onto the upload area or click the upload area to select the file.

The tool parses the Gerber and Excellon data locally in the browser.

### 4. Select the Copper Layer

Choose:

- **Top Copper**
- **Bottom Copper**

### 5. Set Total Exposure Time

`Total exposure time (s)` represents the requested accumulated UV exposure time.

The generated CTB uses a 10-layer compatibility structure. Layers 2–10 use 0.1 s each, and the first layer is automatically compensated.

For example:

```text
Requested total exposure = 10.0 s

Layer 1  = 9.1 s
Layer 2  = 0.1 s
...
Layer 10 = 0.1 s

Total = 10.0 s
```

### 6. Set GKO Expansion

`GKO expansion (mm)` controls how far the active exposure region extends beyond the closed PCB board outline.

Default:

```text
0 mm
```

The expansion follows the actual closed GKO outline rather than only using a rectangular bounding box.

### 7. Select Drill Exposure

The following drill datasets can be enabled independently:

- `PTH_Through.DRL`
- `NPTH_Through.DRL`
- `PTH_Through_Via.DRL`

Enabled drill locations are forced to **UV ON** using the actual drill diameter from the Excellon tool definition.

Default configuration:

- PTH Through: enabled
- NPTH Through: disabled
- PTH Through Via: disabled

### 8. Check the Preview

Two previews are provided.

#### PCB ZOOM · GKO FRAME

Automatically enlarges the PCB region for inspecting:

- Copper geometry
- Negative polarity
- Drill exposure
- Board boundary

#### LCD FULL FRAME

Shows the PCB location on the complete **7680 × 4320** Mighty 8K LCD.

This view is useful for checking placement and centering before generating the CTB.

### 9. Download CTB

Click **Download CTB**.

The CTB file is generated in the browser and downloaded directly.

---

## 🖨️ Target Printer Profile

Current CTB output is designed for:

| Parameter | Value |
|---|---:|
| Printer | Phrozen Sonic Mighty 8K |
| LCD resolution | 7680 × 4320 |
| Build area | 218.88 × 123.12 mm |
| Pixel size | 28.5 µm |
| CTB format | CTB v4 |

---

## 🗂️ Project Structure

```text
UTL_Gerber2CTB/
├── index.html
├── README.md
├── README.zh-TW.md
└── LICENSE
```

The application is implemented as a static browser application and can be hosted directly with GitHub Pages.

---

## 📝 Notes

- The current workflow was developed and validated around Gerber ZIP files exported from **EasyEDA Standard Edition**.
- Always inspect the generated preview before exposure.
- Verify the printer setup and Z-axis configuration before using a resin printer as a PCB UV exposure system.
- CTB compatibility behavior may vary between printer firmware versions.

---

## 🌐 GitHub Pages

Deploy from the `main` branch and `/ (root)` directory under **Settings → Pages**.

The published tool is available at:

https://long-jun.github.io/UTL_Gerber2CTB/

---

## 📜 License

This project is licensed under the **Apache License 2.0**.

See [LICENSE](./LICENSE) for details.

---

## 🙌 Acknowledgements

Originally developed for PCB fabrication and UV-exposure experiments in the **UTL Lab, National Taipei University of Technology (NTUT)**.

Feedback, bug reports, and improvements are welcome through GitHub Issues.
