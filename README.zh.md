# Seafile v12 安裝教學

本指南將引導您使用 Docker 設置 **Seafile v12**。建議使用 **Portainer** 來管理容器。

## 前置條件
- 已在伺服器上安裝 Docker
- Portainer（選用，推薦使用）
- 基本的終端指令操作知識

## Seafile v12 安裝步驟

### 1. 啟動 Docker 容器
使用以下指令啟動 Seafile 容器：

```bash
docker-compose up -d
```

### 2. 初始設定
容器啟動後，需要進行一些初始設定。

#### 設定管理員帳號
由於 Seafile v12 存在一個 Bug，必須手動設定管理員帳號。執行以下指令：

```bash
docker exec seafile-container bash
seafile-server-latest/reset-admin.sh
```

此腳本將提示您設定管理員的使用者名稱和密碼。請妥善保管這些憑證。

### 3. 啟用 WebDAV（可選）
如果需要啟用 WebDAV，請編輯 `seafdav.conf` 文件：

```bash
nano ./conf/seafdav.conf
```

添加或修改以下內容：

```ini
enabled = true
```

保存並退出文件。

### 4. 配置 HTTPS（可選）
如果您透過域名主機部署 Seafile，請確保服務 URL 使用 HTTPS。編輯 `seahub_settings.py` 文件：

```bash
nano ./conf/seahub_settings.py
```

更新以下設定：

```python
SERVICE_URL = 'https://your-domain.com'
FILE_SERVER_ROOT = 'https://your-domain.com/seafhttp'
```

保存並退出文件。

## 注意事項
- 如果在安裝過程中遇到問題，請參考 [Seafile 官方文檔](https://manual.seafile.com/) 獲取更多幫助。
- 修改配置文件後，請重新啟動容器：

  ```bash
  docker-compose restart
  ```

## 推薦工具
- [Portainer](https://www.portainer.io/)：用於管理 Docker 容器
- [Nano](https://www.nano-editor.org/)：用於編輯配置文件

## 貢獻
歡迎通過提交 Pull Request 或 Issue 為本教程做出貢獻。

## 授權
本項目採用 MIT 授權條款。詳情請參閱 [LICENSE](LICENSE) 文件。

---
**Seafile v12** 是一款強大的文件同步和共享解決方案。通過本教程，您可以快速設置並配置自己的 Seafile 實例。祝您使用愉快！
