# Week 13 Homework — ARIA v9.0: The Cloud Engine

**課程：** 台灣大學 遙測與空間資訊分析  
**研究區：** 秀林 / 太魯閣山區（花蓮縣）  
**分析目標：** 使用 Google Earth Engine（GEE）進行 2020–2026 年雲端時序植被與地表變化分析，聚焦 2024/04/03 花蓮地震的衝擊與後續恢復

---

## 檔案說明

| 檔案 | 說明 |
|------|------|
| `ARIA_v9_merged.ipynb` | 主程式：完整四個 Task + Bonus 1 & 2 |
| `task1_ndvi_time_series.png` | Task 1：2020–2026 月均 NDVI 時序圖 |
| `task2_taroko_ndvi_change_map.html` | Task 2：震前/震後/堰塞湖後 ΔNDVI 互動地圖 |
| `task2_delta_ndvi_loss_area.csv` | Task 2：三期 ΔNDVI < -0.15 損失面積（公頃） |
| `task3_sar_vv_time_series.png` | Task 3：Sentinel-1 VV 後向散射時序圖 |
| `task3_taroko_sar_change_map.html` | Task 3：ΔVV 與高可信度變化區互動地圖 |
| `taroko_ndvi_timelapse.gif` | Bonus 2：2020–2026 NDVI 時序動畫 GIF |

> **GeoTIFF 匯出檔案**（`taroko_ndvi_post_eq_2024.tif` 等）存放於 Google Drive `GEE_Exports` 資料夾，截圖附於 notebook 內。

---

## 主要結果

### Task 1 — NDVI 時序
- 處理 **291 張** Sentinel-2 L2A 影像，涵蓋 72 個有效月份（3 個缺值月份）
- NDVI 年內振幅約 **0.125**，5 月最高、10 月最低，反映山區植被物候
- 震前均值 **0.481**，震後六個月均值 **0.469**（差異 -0.013）

### Task 2 — ΔNDVI 合成比較
| 比較時期 | ΔNDVI < -0.15 損失面積 |
|---------|----------------------|
| 震後 vs 震前（地震損害） | **7,370.9 ha** |
| 堰塞湖後 vs 震後（後續影響） | **3,612.3 ha** |
| 堰塞湖後 vs 震前（總累積） | **6,166.6 ha** |

> 總累積（6,166.6 ha）小於地震期（7,370.9 ha），代表部分受擾動區域已有植被恢復跡象。

### Task 3 — SAR VV 時序
- 處理 **147 張** Sentinel-1 DESCENDING VV 影像（2022–2026）
- 震前均值 **-9.45 dB**，震後均值 **-9.49 dB**（AOI 均值差異微小，因大面積穩定森林稀釋）
- 高可信度 mask（ΔNDVI < -0.15 且 |ΔVV| > 2 dB）：**487.4 ha**

### Task 4 — GeoTIFF 匯出
匯出 4 個產品至 Google Drive `GEE_Exports`：
- `taroko_ndvi_post_eq_2024.tif`
- `taroko_delta_ndvi_eq_2024.tif`
- `taroko_delta_ndvi_total_2023_2026.tif`
- `taroko_delta_vv_2024_2026.tif`

---

## 執行環境

```
Python 3.10+
earthengine-api
geemap
pandas
matplotlib
Pillow
imageio
requests
```

執行前請在 `ARIA_v9_merged.ipynb` 的 Setup cell 填入自己的 GEE Project ID：
```python
PROJECT_ID = 'your-project-id'
```

---

## Bonus

- **Bonus 1**：InSAR 干涉圖判讀（水保署電子報第 141 期，ALOS-2 熊本地震，每環 11.8 cm，估計最大 LOS 位移 ~189 cm）
- **Bonus 2**：2020–2026 NDVI 半年度時序動畫 GIF（13 幀，含地震與堰塞湖事件標記）
