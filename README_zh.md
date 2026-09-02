# UTL Gerber2CTB

[English](./README.md) | **繁體中文**


使用**Phrozen Sonic Mighty 8K**進行PCB UV曝光的Gerber轉CTB網頁工具。

## 📚 簡介

UTL Gerber2CTB可將**EasyEDA Standard Edition**輸出的Gerber ZIP轉換為**Phrozen Sonic Mighty 8K**使用的PCB UV曝光CTB檔。整個轉換流程直接在瀏覽器中完成，包含銅箔層選擇、GKO遮罩、鑽孔曝光控制、預覽與CTB輸出。

本工具針對**EasyEDA Standard Edition**輸出的Gerber ZIP設計，可讀取PCB銅箔層、GKO板框與指定鑽孔資料，產生曝光預覽並輸出Mighty 8K可使用的CTB檔案。

**線上工具：**  
https://long-jun.github.io/UTL_Gerber2CTB/

最初開發用途為國立臺北科技大學UTL實驗室之PCB製作與UV曝光實驗。

---

## 🔄 操作流程

```text
EasyEDA Standard
      ↓
匯出Gerber ZIP
      ↓
上傳至UTL Gerber2CTB
      ↓
選擇Top / Bottom Copper
      ↓
設定總曝光時間
      ↓
設定GKO外擴與鑽孔曝光
      ↓
檢查PCB ZOOM與LCD FULL FRAME
      ↓
下載CTB
      ↓
Phrozen Sonic Mighty 8K
```

---

## ✨ 功能特色

- 針對**EasyEDA Standard Edition**輸出的Gerber ZIP設計
- 可選擇Top Copper / Bottom Copper
- 自動讀取GKO封閉板框
- GKO曝光區外擴距離可調
- 支援PCB負片曝光
- 三種鑽孔資料可獨立勾選：
  - `PTH_Through.DRL`
  - `NPTH_Through.DRL`
  - `PTH_Through_Via.DRL`
- 依Excellon工具表讀取實際鑽孔直徑
- PCB ZOOM局部放大預覽
- LCD FULL FRAME完整LCD定位預覽
- 自動將PCB置中於7680 × 4320的Mighty 8K LCD
- CTB於瀏覽器端直接產生
- Gerber資料不需要送至後端伺服器處理

---

## 🚀 使用方式

### 1. 從EasyEDA Standard匯出Gerber ZIP

在**EasyEDA Standard Edition**中開啟PCB專案，將製造檔案匯出為Gerber ZIP。

典型EasyEDA ZIP可能包含：

```text
Gerber_TopLayer.GTL
Gerber_BottomLayer.GBL
Gerber_BoardOutlineLayer.GKO
Drill_PTH_Through.DRL
Drill_NPTH_Through.DRL
Drill_PTH_Through_Via.DRL
```

一般使用流程至少需要銅箔層與GKO板框。鑽孔檔案則可依需求選擇是否加入曝光。

### 2. 開啟UTL Gerber2CTB

直接開啟：

https://long-jun.github.io/UTL_Gerber2CTB/

不需要安裝額外軟體。

### 3. 上傳Gerber ZIP

可直接將ZIP拖曳至上傳區，或點擊上傳區選擇檔案。

Gerber與Excellon資料會直接在瀏覽器中解析。

### 4. 選擇銅箔層

可選擇：

- **Top Copper**
- **Bottom Copper**

### 5. 設定總曝光時間

`Total exposure time (s)`代表希望PCB接受的**累積UV曝光時間**。

產生的CTB使用10層相容結構。第2–10層固定為0.1秒，第1層會自動扣除這0.9秒。

例如：

```text
設定總曝光時間 = 10.0 s

Layer 1  = 9.1 s
Layer 2  = 0.1 s
...
Layer 10 = 0.1 s

Total = 10.0 s
```

因此使用者只需要輸入希望的總曝光時間，不需要自行換算。

### 6. 設定GKO Expansion

`GKO expansion (mm)`用於控制有效曝光區在PCB封閉板框之外額外延伸的距離。

預設：

```text
0 mm
```

外擴範圍會依據實際GKO封閉輪廓處理，而不是只使用矩形外接框。

### 7. 選擇鑽孔曝光

以下三種鑽孔資料可獨立勾選：

- `PTH_Through.DRL`
- `NPTH_Through.DRL`
- `PTH_Through_Via.DRL`

啟用後，對應鑽孔位置會依Excellon工具表中的實際孔徑強制設成**UV ON**。

預設設定：

- PTH Through：啟用
- NPTH Through：停用
- PTH Through Via：停用

### 8. 檢查預覽

工具提供兩個預覽畫面。

#### PCB ZOOM · GKO FRAME

依據PCB板框自動放大，方便檢查：

- 銅箔圖形
- 負片方向
- 鑽孔曝光
- PCB板框

#### LCD FULL FRAME

顯示PCB在完整**7680 × 4320 Mighty 8K LCD**上的實際位置。

可用來確認PCB是否置中，以及曝光圖在LCD上的位置是否合理。

### 9. 下載CTB

按下**Download CTB**。

CTB會直接在瀏覽器中產生並下載。

---

## 🖨️ 目標印表機規格

目前CTB輸出針對：

| 項目 | 規格 |
|---|---:|
| 印表機 | Phrozen Sonic Mighty 8K |
| LCD解析度 | 7680 × 4320 |
| 成型面積 | 218.88 × 123.12 mm |
| Pixel size | 28.5 µm |
| CTB格式 | CTB v4 |

---

## 🗂️ 專案結構

```text
UTL_Gerber2CTB/
├── index.html
├── README.md
├── README.zh-TW.md
└── LICENSE
```

本工具為靜態網頁，可直接透過GitHub Pages部署。

---

## 📝 使用注意事項

- 目前工作流程主要針對**EasyEDA Standard Edition**輸出的Gerber ZIP進行開發與驗證。
- 曝光前請先檢查工具中的預覽結果。
- 使用樹脂3D印表機進行PCB曝光前，請確認Z軸、平台與LCD周圍的機構配置，避免碰撞。
- 不同韌體版本對CTB的處理方式可能存在差異。

---

## 🌐 GitHub Pages

在repository的**Settings → Pages**中設定：

- Source：Deploy from a branch
- Branch：`main`
- Folder：`/ (root)`

線上工具網址：

https://long-jun.github.io/UTL_Gerber2CTB/

---

## 📜 授權

本專案採用**Apache License 2.0**。

詳細內容請參考[LICENSE](./LICENSE)。

---

## 🙌 致謝

本工具最初因應**國立臺北科技大學UTL實驗室**之PCB製作與UV曝光實驗需求開發。

若發現問題或有改進建議，歡迎透過GitHub Issues回饋。
