# ccc: git branch 怎麼用

`git branch` 是 Git 中用來**管理分支**（創建、查看、重新命名與刪除）的核心指令。

在 Git 中，分支就像是專案的「平行宇宙」，讓你能在不影響主線程式碼（通常是 `main` 或 `master`）的情況下開發新功能或修復 Bug。

---

## 常用情境與指令總覽

### 1. 查看分支 (List)

* **查看本地所有分支**（前面有 `*` 標號的代表當前所在分支）：
```bash
git branch

```


* **查看遠端（Remote）分支**：
```bash
git branch -r

```


* **查看本地與遠端的「所有」分支**：
```bash
git branch -a

```


* **查看各分支最後一次 commit 的訊息**：
```bash
git branch -v

```



---

### 2. 建立分支 (Create)

* **建立新分支**（但停留在當前分支）：
```bash
git branch <new-branch-name>

```


> **驗證步驟**：輸入 `git branch`，確認列表中出現了 `<new-branch-name>`。


* **【最常用】建立新分支並「直接切換」過去**：
```bash
git switch -c <new-branch-name>
# 或傳統指令：git checkout -b <new-branch-name>

```


> **驗證步驟**：輸入 `git branch`，會看到 `* <new-branch-name>` 變為綠色並帶有星號，代表已成功切換。



---

### 3. 切換分支 (Switch)

* **切換到已存在的分支**：
```bash
git switch <branch-name>
# 或傳統指令：git checkout <branch-name>

```


> **驗證步驟**：終端機提示字元會顯示目前的分支名稱，也可執行 `git status` 確認當前分支。



---

### 4. 刪除分支 (Delete)

* **安全刪除分支**（若該分支還有程式碼尚未合併，Git 會阻止刪除以防資料遺失）：
```bash
git branch -d <branch-name>

```


* **強制刪除分支**（不管有沒有合併，直接丟棄）：
```bash
git branch -D <branch-name>

```


> **驗證步驟**：輸入 `git branch`，確認該分支已不在清單中。


* **刪除遠端伺服器上的分支**：
```bash
git push origin --delete <branch-name>

```



---

### 5. 重命名分支 (Rename)

* **修改「當前所在」的分支名稱**：
```bash
git branch -m <new-branch-name>

```


* **修改「指定」的分支名稱**：
```bash
git branch -m <old-branch-name> <new-branch-name>

```



---

## 標準開發工作流程範例 (Workflow)

假設你要開發一個「登入功能」：

1. **切換到主分支並拉取最新程式碼:** 預備動作.
```bash
git switch main
git pull

```

> **驗證**：確保當前環境是基於最新主線。


2. **開立並切換到新功能分支:** 建立開發環境.
```bash
git switch -c feature/login

```

> **驗證**：執行 `git branch`，確認目前位於 `feature/login`。


3. **進行開發、提交變更:** 撰寫程式碼.
```bash
git add .
git commit -m "Add login page UI"

```


4. **合併回主分支:** 完成開發.
切換回主分支，並將新功能合併進來：

```bash
git switch main
git merge feature/login

```

> **驗證**：執行 `git log`，確認主分支已包含 `feature/login` 的 commit 紀錄。


5. **清理已合併的分支:** 保持專案整潔.
```bash
git branch -d feature/login

```

> **驗證**：執行 `git branch`，確認舊分支已刪除。

`git checkout -b <branch-name>` 實際上就是將 **`git branch`（建立分支）** 與 **`git checkout`（切換分支）** 這兩個獨立指令合併在一起的「快捷縮寫」。

---

## 語法與等價關係

執行一行：

```bash
git checkout -b feature/login

```

這完全等同於**依序執行以下兩行**：

```bash
git branch feature/login   # 1. 先用 branch 建立分支
git checkout feature/login # 2. 再用 checkout 切換過去

```

---

## 指令職責拆解

| 指令 | 主要功能 | 執行後的狀態 |
| --- | --- | --- |
| **`git branch <name>`** | 單純**建立**新分支。 | 你依然停留在**原本的分支**上（`HEAD` 指針沒變）。 |
| **`git checkout <name>`** | 單純**切換**到已存在的分支。 | 你的工作目錄會切換到該分支最新的 Commit 狀態。 |
| **`git checkout -b <name>`** | **建立**新分支並**立即切換**過去。 | 新分支建立完成，且你已經身處在**新分支**上。 |

---

## 現代 Git 的替代語法 (`git switch`)

由於 `git checkout` 的功能過於龐雜（除了切換分支，還能還原檔案），Git 在 2.23 版本後推出了專門用來處理分支切換的指令 `git switch`：

* **傳統方式**：
```bash
git checkout -b feature/login

```


* **現代方式（語意更直覺）**：
```bash
git switch -c feature/login

```


* `-c` 代表 `--create`，效果與 `checkout -b` 完全一致。
