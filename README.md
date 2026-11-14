# Api-Post-NeighborOnionapp

**隔壁老洋｜Streamlit 管理端資料輸入工具**

本 Repository 提供管理者輸入洋蔥栽植期提醒及預警報的簡易介面，並透過 HTTP POST 將資料送至 [API-client-NeighborOnionapp](https://github.com/Kouichi1229/API-client-NeighborOnionapp)。

## 技術

- Python
- Streamlit
- Requests
- JSON

## 功能

### 栽植期表單

- 輸入溫度注意事項（最多 150 字）。
- 輸入雨量注意事項（最多 150 字）。
- 送出時呼叫 `POST /plant`，傳送 `temp` 與 `rain` 欄位。

### 預警報表單

- 輸入預警報文字（最多 400 字）。
- 送出時呼叫 `POST /aler`，傳送 `aler` 欄位。

## 資料流程

```text
管理者
  -> Streamlit 表單
  -> Requests POST（JSON）
  -> FastAPI API
  -> Pydantic schema
  -> SQLAlchemy ORM
  -> SQLite
```

## 程式碼注意事項

- 表單包含日期輸入欄位，但目前 `update_time` 沒有加入 POST payload，因此程式目前沒有把該日期送往後端。
- API URL 寫定為歷史 Heroku 網址 `https://apipost-no-v1.herokuapp.com`；這只代表程式當時設定的服務位置，不保證該服務目前仍在線。
- 目前主要檢查 HTTP 200，錯誤處理尚未涵蓋 timeout、連線失敗及非 JSON 回應。
- 未見預約功能的管理表單。

完整系統架構及技術回顧請參閱主專案：[NeighborOnionapp](https://github.com/Kouichi1229/NeighborOnionapp)。
