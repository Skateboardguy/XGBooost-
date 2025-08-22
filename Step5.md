步驟 5) 在 Validation 上調參，並用 early_stopping 找最佳迭代數
(a) 定義搜尋空間
search_space = [
    (0.05, 3), (0.05, 4), (0.05, 5),
    (0.10, 3), (0.10, 4), (0.10, 5),
    (0.20, 3), (0.20, 4), (0.20, 5),
]
👉 我們要測試不同 learning_rate 與 max_depth 的組合（共 9 種）。
 
(b) 迴圈嘗試每一組組合
for lr, depth in search_space:
    model = xgb.XGBClassifier(**{**base_params, "learning_rate": lr, "max_depth": depth})
👉 建立模型，把 基礎參數 + 搜尋組合 合併。
例如：learning_rate=0.05, max_depth=3。
 
(c) 訓練並監控 Validation
    model.fit(
        X_train, y_train,
        eval_set=[(X_valid, y_valid)],
        verbose=False,
        early_stopping_rounds=50
    )
•	eval_set → 指定監控的驗證集 (Validation)。
•	early_stopping_rounds=50 → 如果連續 50 次迭代沒有進步，就自動停止。
•	model.best_iteration → 紀錄最佳樹的數量。
 
(d) 計算驗證集 AUC
    valid_prob = model.predict_proba(X_valid)[:, 1]
    valid_auc = roc_auc_score(y_valid, valid_prob)
👉 用 AUC 當模型好壞的評估標準。
 
(e) 保留最佳組合
    if valid_auc > best_valid_auc:
        best_valid_auc = valid_auc
        best_cfg = {"learning_rate": lr, "max_depth": depth}
        best_boosting_rounds = model.best_iteration + 1
👉 更新最佳參數組合，並記錄下「最佳迭代數」。
