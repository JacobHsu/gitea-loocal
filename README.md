# gitea-loocal

在本機用 Docker 架設 [Gitea](https://about.gitea.com/) 作為版本控制，供學習與練習使用。

## 參考資料

- [Gitea 官方文件（繁體中文）](https://docs.gitea.com/zh-tw/)
- [Docker 安裝說明](https://docs.gitea.com/zh-tw/installation/install-with-docker)
- [設定檔速查（app.ini）](https://docs.gitea.com/zh-tw/administration/config-cheat-sheet)
- [Gitea 原始碼與 Releases](https://github.com/go-gitea/gitea)

## 環境需求

- Docker Desktop（需先啟動）

## 快速開始

```powershell
docker compose up -d      # 啟動
docker compose down       # 停止
docker logs gitea         # 查看日誌
```

| 服務 | 位址 |
| --- | --- |
| Web 介面 | http://localhost:3000 |
| SSH | `ssh://git@localhost:2222/<使用者>/<repo>.git` |


## 建立管理員帳號

`docker-compose.yml` 已設定 `INSTALL_LOCK=true`，會略過網頁安裝畫面，因此需用指令建立管理員：

```powershell
docker exec -u git gitea gitea admin user create --admin `
  --username admin --password "<自訂密碼>" --email admin@localhost.local
```

登入後請到「設定 → 帳號」修改密碼。

## 資料與備份

- 所有資料（SQLite 資料庫、repo、設定）存放於專案內的 `data/` 資料夾。
- 備份時先 `docker compose down`，再複製 `data/`。
- `data/` 含密鑰與資料庫，不要提交到 git（已列於 `.gitignore`）。

## 學習路線

1. 建立儲存庫（repository）。
2. `git clone http://localhost:3000/admin/<repo>.git`，commit 後 push。
3. 練習 Issues、Branch、Pull Request、Wiki。
4. 在「個人設定 → SSH/GPG 金鑰」加入公鑰，改用 SSH 免密碼 push。
