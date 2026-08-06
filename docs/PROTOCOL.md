# SQL Monitor 通信仕様

**Version:** v0.1 Draft  
**Project:** SQL Monitor  
**Organization:** Sapporo Quake Lab

---

# 1. 概要

本ドキュメントは、SQL Monitorにおける観測機・クライアント・サーバー間の通信仕様を定義します。

---

# 2. システム構成

```text
観測機
(EQIS-1 / 自作震度計)
        │
USB / Serial / LAN
        │
        ▼
SQL Monitor
        │
WebSocket (予定)
        │
        ▼
SQL Server
        │
        ▼
他の観測者
```

---

# 3. 通信方式

## 観測機 ⇔ SQL Monitor

対応予定

- USB Serial
- TCP/IP
- UDP（将来対応）

---

## SQL Monitor ⇔ SQL Server

通信方式

- WebSocket（予定）
- HTTPS（設定・認証など）

---

# 4. データ送信タイミング

通常時

- 1秒ごと（予定）

地震検知時

- 100ms～250msごと（予定）

※最終的な送信間隔は調整予定

---

# 5. データ形式

JSONを使用予定

例

```json
{
  "station_id": "JP001",
  "timestamp": "2026-08-06T12:34:56Z",
  "intensity": 1.2,
  "pga": 8.5,
  "status": "online"
}
```

---

# 6. ステータス

online

通信正常

offline

未接続

warning

通信遅延

error

通信エラー

---

# 7. エラー処理

サーバー切断時

- 自動再接続

観測機切断時

- 接続待機
- ログへ記録

通信エラー

- ログへ保存
- ユーザーへ通知

---

# 8. 将来追加予定

- データ圧縮
- 暗号化通信（TLS）
- API認証
- プラグイン通信
- MQTT対応検討

---

# 9. バージョン管理

現在

Protocol v0.1 Draft

今後、互換性を維持しながら更新予定。