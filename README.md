# 金融詐欺 AI 偵測系統

## 專案簡介

此專案旨在開發一個金融詐欺偵測系統，使用機器學習模型來識別可疑的金融交易。我們利用交易行為特徵、帳戶資訊和客戶資料，建立了一個可以即時辨識詐欺風險的預測模型，並提供視覺化的風險解釋。

## 技術架構

- **資料儲存**: AWS S3
- **資料處理**: SageMaker Data Wrangler
- **模型訓練**: SageMaker XGBoost & LightGBM
- **超參數調整**: SageMaker Automatic Model Tuning
- **模型解釋**: SageMaker Clarify
- **視覺化儀表板**: Amazon QuickSight
- **部署**: SageMaker Inference Pipeline & Streamlit

## 資料處理

我們使用了四種主要資料來源:
- 客戶基本資料 (`ID_Data`)
- 帳戶資訊 (`ACCTS_Data`)
- 交易明細 (`SAV_TXN_Data`)
- 詐欺標記 (`ECCUS_Data`)

資料處理步驟:
1. 以 `CUST_ID` 和 `ACCT_NBR` 為鍵進行資料連接
2. 處理缺失值並執行特徵轉換 (日期、類別編碼等)
3. 建立時間序列特徵 (交易頻率、金額變化等)
4. 計算群組統計量 (近期交易行為、異常模式等)
5. 標準化數值特徵並處理類別變數

## 模型選擇

我們優先使用 XGBoost 模型:

- **XGBoost** (baseline)
   - 優點: 訓練速度快，對 Tabular 資料表現優異
   - 使用 AUPRC 和 F1 作為評估指標

透過 XGBoost 模型獲得最佳預測表現。

## 使用方法

1. 將資料上傳至 S3 儲存桶
2. 使用 SageMaker Studio 執行資料處理和模型訓練筆記本
3. 部署模型並使用提供的 API 進行預測

## 結果展示

模型能夠識別出多種詐欺模式，主要風險因子包括:
- 凌晨高額跨國轉出
- 新裝置異常登入
- 非常規地理位置的交易

系統提供即時風險評分和解釋，幫助風控人員快速做出判斷。