步驟 4) 建立基礎模型 (baseline XGBClassifier)
base_params = dict(
    objective="binary:logistic",   # 二元分類，輸出機率
    eval_metric="logloss",         # 評估指標：交叉熵 (也可用 auc)
    learning_rate=0.1,             # 每棵樹的步伐 (控制更新幅度)
    max_depth=4,                   # 每棵樹的最大深度 (避免過度擬合)
    subsample=0.9,                 # 每次建樹時，隨機取 90% 資料
    colsample_bytree=0.9,          # 每棵樹隨機取 90% 特徵
    reg_lambda=1.0,                # L2 正規化，避免過擬合
    n_estimators=500,              # 預設很多樹，搭配 early_stopping 自動挑選最佳
    random_state=42,               # 固定隨機性，結果可重現
    n_jobs=-1                      # 使用所有 CPU 核心加速
)
👉 這裡先定義一組 合理的預設值，等於基礎配置（baseline hyperparameters）。
之後我們會只調整少數幾個超參數（如 learning_rate、max_depth），其他保持不動。
