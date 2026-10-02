## 111210529陳宏傑
## 專案連結
* **目標母專案**：[sese-TEST-examples/git-exmples](https://github.com/sese-TEST-examples/git-exmples)
* **我 Fork 的專案**：[jerry92916/git-exmples](https://github.com/jerry92916/git-exmples)

## 操作步驟

### 1. Fork 專案
在母專案頁面右上角點擊 **Fork**，把專案複製到我的帳號下。

### 2. Clone 到本地端
將剛 Fork 過來的專案下載到電腦裡，並進入資料夾：

```bash
git clone https://github.com/jerry92916/git-exmples.git
cd git-exmples
```

### 3. 建立並切換分支
開一個新分支來修改檔案，避免直接動到 main：

```bash
git checkout -b feature/update-doc
```

### 4. 提交變更 (Commit)
修改或新增檔案後，將變更 commit 起來：

```bash
git add .
git commit -m "docs: 更新 README 練習紀錄"
```

### 5. 推送回 GitHub (Push)
把本地的分支推送到我自己的 GitHub 上：

```bash
git push origin feature/update-doc
```

### 6. 發出 Pull Request (PR)
回到 GitHub 網頁端：
1. 進入我的專案頁面，點擊 **Compare & pull request**。
2. 確認合併方向：由我的 `feature/update-doc` 分支 `->` 母專案的 `main` 分支。
3. 填寫說明後送出 **Create pull request**，等待原作者審核與合併 (Merge)。
