步驟 6) 用最佳參數重新訓練（Train+Valid）
final_model = xgb.XGBClassifier(
    **base_params,
    learning_rate = best_cfg["learning_rate"],
    max_depth=best_cfg["max_depth"],
    n_estimators=best_boosting_rounds
)

final_model.fit(
    np.vstack([X_train, X_valid]),   # 合併 Train + Valid
    np.hstack([y_train, y_valid])
)
👉 這裡的邏輯是：
•	Validation 不再需要（因為調參已經完成）。
•	所以把 Train + Valid 合併，重新訓練 最終模型。
•	n_estimators 設成最佳迭代數，不再靠 early_stopping。
