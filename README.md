# NTUT-UTL Gerber to CTB
### 北科大 UTL 實驗室 PCB UV 曝光檔轉換工具

Browser-based Gerber-to-CTB converter for PCB UV exposure on the
Phrozen Sonic Mighty 8K.

This tool is designed for Gerber ZIP files exported from
**EasyEDA Standard Edition**. It converts PCB copper and drill data
into a CTB exposure file that can be used with the Phrozen Sonic Mighty 8K.

專為 **EasyEDA Standard Edition** 輸出的 Gerber ZIP 檔設計，
可將 PCB 銅箔層、板框與鑽孔資料轉換成 Phrozen Sonic Mighty 8K
可使用的 CTB UV 曝光檔。

Originally developed for the UTL Lab at
National Taipei University of Technology (NTUT).

最初開發用途為國立臺北科技大學 UTL 實驗室之 PCB 製作與 UV 曝光實驗。

GitHub Pages:
https://long-jun.github.io/Gerber2CTB_Mighty8K/

---

## 🚀 How to Use 使用方式

### 1. Export Gerber ZIP from EasyEDA Standard
### 從 EasyEDA Standard 匯出 Gerber ZIP

Open your PCB project in **EasyEDA Standard Edition**.

在 **EasyEDA Standard Edition** 中開啟 PCB 專案。

Export the fabrication Gerber files as a ZIP package.

將 PCB 製造檔案匯出為 Gerber ZIP。

The ZIP file should normally contain files such as:

* `Gerber_TopLayer.GTL`
* `Gerber_BottomLayer.GBL`
* `Gerber_BoardOutlineLayer.GKO`
* `Drill_PTH_Through.DRL`
* `Drill_NPTH_Through.DRL`
* `Drill_PTH_Through_Via.DRL`

The exact filenames may vary slightly depending on the EasyEDA project.

實際檔名可能因 EasyEDA 專案而略有不同，但至少需要包含銅箔層與板框資料。

---

### 2. Open the Gerber-to-CTB web tool
### 開啟 Gerber-to-CTB 網頁工具

Open:

https://long-jun.github.io/Gerber2CTB_Mighty8K/

No software installation is required.

不需要安裝額外軟體，直接使用 Chrome、Edge 或其他現代瀏覽器即可。

---

### 3. Upload the Gerber ZIP
### 上傳 Gerber ZIP

Drag the Gerber ZIP file into the upload area, or click the upload area
to select the ZIP file manually.

將 EasyEDA 匯出的 Gerber ZIP 拖曳到網頁中，
或直接點擊上傳區域選擇檔案。

The tool automatically reads:

* Top Copper
* Bottom Copper
* Board Outline (GKO)
* PTH drill data
* NPTH drill data
* Via drill data

工具會自動辨識銅箔層、GKO 板框與鑽孔資料。

---

### 4. Select the PCB layer
### 選擇要曝光的 PCB 層

Choose:

* **Top Copper**
* **Bottom Copper**

選擇要產生曝光檔的銅箔層：

* Top Copper
* Bottom Copper

---

### 5. Set the exposure time
### 設定曝光時間

Enter the desired **total UV exposure time**.

輸入希望 PCB 實際接受的總 UV 曝光時間。

Example:

`10.0 s`

The generated CTB internally uses a 10-layer compatibility structure.
The program automatically compensates the auxiliary layers so that the
total exposure remains equal to the value entered by the user.

例如輸入：

`10.0 s`

程式會自動補償 CTB 相容層的時間，使實際總曝光時間維持約 10.0 秒。

---

### 6. Set GKO expansion
### 設定板框外擴距離

`GKO expansion (mm)` controls how far the UV exposure area extends
outside the PCB board outline.

`GKO expansion (mm)` 用來設定 UV 曝光區域在 PCB 板框外額外延伸的距離。

Default:

`0 mm`

For example:

`2 mm`

means the exposure region extends approximately 2 mm outside the
closed GKO board outline.

---

### 7. Select drill exposure
### 選擇鑽孔曝光

The following drill files can be enabled independently:

* `PTH_Through.DRL`
* `NPTH_Through.DRL`
* `PTH_Through_Via.DRL`

Enabled drill holes are forced to **UV ON** according to their actual
drill diameter.

三種鑽孔資料可以分別勾選。

勾選後，對應孔位會依實際孔徑加入 UV 曝光區。

Default setting:

* PTH Through: enabled
* NPTH Through: disabled
* PTH Through Via: disabled

---

### 8. Check the preview
### 檢查預覽

The tool provides two preview windows.

#### PCB ZOOM

Automatically enlarges the PCB area based on the GKO board outline.

依據 GKO 板框自動放大 PCB 區域，方便檢查：

* Copper pattern
* Drill holes
* Negative mask
* Board boundary

#### LCD FULL FRAME

Shows the actual PCB position on the full
**7680 × 4320 Phrozen Sonic Mighty 8K LCD**.

顯示 PCB 在 Mighty 8K LCD 上的實際位置，可用來確認是否置中。

---

### 9. Download the CTB file
### 下載 CTB

Click:

**Download CTB**

The browser will generate and download the CTB file.

按下 **Download CTB** 後，瀏覽器會直接產生 CTB 曝光檔。

The file can then be copied to the storage device used by the
Phrozen Sonic Mighty 8K.

產生的 CTB 檔即可再傳送至 Phrozen Sonic Mighty 8K 使用。
