# 資料前處理流程

## 1. 區分變數型態
- **連續變數** → 可直接使用  
- **類別變數** → 轉換成 Dummy / Label Encoding  

## 2. 切分資料集
- **訓練集 (Train)**  
- **驗證集 (Validation)** → 用於調參 / early_stopping  
- **測試集 (Test)** → 最終評估  

## 3. 模型建立 (XGBoostRegressor)
- `max_depth`、`learning_rate`、`n_estimators`  
- `subsample`、`colsample_bytree`  
- `reg_alpha (L1)`、`reg_lambda (L2)`  

## 4. 模型訓練
- 使用 **early_stopping_rounds** 防止過擬合  

## 5. 模型評估
- RMSE  
- R²  
- MAE  

## 6. 特徵重要性輸出
- Gain  
- Weight  
- Cover


