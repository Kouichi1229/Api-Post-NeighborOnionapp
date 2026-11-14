# 隔壁老洋｜管理端資料輸入工具

本 Repository 是「隔壁老洋」系統的管理端原型，使用 Streamlit 建立表單，讓管理者輸入洋蔥栽植期提醒與預警報，再透過 HTTP POST 將 JSON 資料送至 FastAPI 後端。

此 Repository 屬於主系統的管理端子模組，不應與後端 API 或整體應用重複計算為獨立產品。

## 主要功能

- 栽植期提醒表單：輸入溫度與雨量注意事項。
- 預警報表單：輸入預警報文字。
- 使用 Requests 將表單資料以 POST 請求傳送至後端。
- 使用 Streamlit 建立簡易操作介面。

## 技術

- Python
- Streamlit
- Requests
- JSON / HTTP POST

## 資料流程

```text
管理者
  -> Streamlit 表單
  -> Requests POST（JSON）
  -> FastAPI 後端
  -> Pydantic / SQLAlchemy
  -> SQLite
```

後端 Repository：[API-client-NeighborOnionapp](https://github.com/Kouichi1229/API-client-NeighborOnionapp)

整體系統：[NeighborOnionapp](https://github.com/Kouichi1229/NeighborOnionapp)

## 程式現況與限制

- 表單雖然提供更新日期欄位，但目前 POST payload 未包含該日期。
- 後端 URL 寫定為歷史 Heroku 網址，不代表服務目前仍可使用。
- HTTP 錯誤處理較簡單，尚未完整處理 timeout、連線例外及非 JSON 回應。
- 目前程式涵蓋栽植期與預警報輸入，沒有管理端預約功能。
- 本文件依程式碼靜態整理，未重新部署或進行端到端測試。

本專案適合作為 Python Web UI 與 REST API 串接的實作紀錄。
