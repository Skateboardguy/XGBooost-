🔹 步驟 7) 在 Test 上做最後一次評估
y_pred = final_model.predict(X_test)
y_prob = final_model.predict_proba(X_test)[:, 1]
👉 到這裡才動用 Test 集：
•	y_pred → 最終的分類結果 (0/1)。
•	y_prob → 對應的機率。
最後會計算 AUC / Accuracy / Recall 等指標，當作最終報告。