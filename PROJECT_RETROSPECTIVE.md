# 技術回顧｜隔壁老洋管理端資料輸入工具

## 專案定位

這是「隔壁老洋」農業資訊應用中的管理端原型。使用者透過 Streamlit 表單輸入栽植期提醒及預警報文字，程式再以 HTTP POST 將資料送至獨立的 FastAPI 後端。

它是整體系統的一個子模組，而非完整獨立產品。相關後端與系統文件應合併閱讀。

## 可由程式確認的實作

### 1. Streamlit 表單介面

- 使用側邊欄選擇「栽植期」或「預警報」頁面。
- 使用 `st.form`、`st.date_input`、`st.text_area` 建立輸入表單。
- 以 `max_chars` 限制文字輸入長度。
- 使用表單送出事件觸發資料傳送。

### 2. HTTP API 串接

- 使用 Requests 發送 POST 請求。
- 將輸入欄位組成 Python dictionary，再序列化為 JSON。
- 栽植期資料包含 `temp`、`rain`。
- 預警報資料包含 `aler`。
- 依 HTTP status code 顯示送出結果，並輸出後端 JSON 回應。

### 3. 系統整合概念

管理端與 API 後端分離：前端負責輸入與送出，後端負責資料驗證、資料存取及 API 回應。這可佐證使用者曾實作 Python UI 與 REST API 之間的基本整合流程。

## 技術能力紀錄

- Python
- Streamlit
- Requests
- JSON serialization
- HTTP POST / REST API integration
- 表單輸入與基本回應呈現

## 靜態檢視發現

以下是從目前程式碼可確認的限制，不代表曾經發生的實際故障：

1. 日期欄位 `update_time` 有建立，但沒有加入送出的 payload。
2. API 網址寫定為歷史 Heroku endpoint，無法據此確認目前服務狀態。
3. Requests 使用 `data=json.dumps(data)` 傳送字串，沒有明確設定 `Content-Type: application/json`；FastAPI JSON body parsing 可能因此無法依預期解析。
4. Requests 呼叫沒有 timeout 參數，也沒有完整的例外處理。
5. 程式在回應狀態為 200 時顯示成功訊息，之後直接呼叫 `res.json()`；未處理非 JSON 回應。
6. 目前管理端只串接栽植期與預警報，沒有串接後端預約 API。

## 與其他 Repository 的關係

- `API-client-NeighborOnionapp`：提供 FastAPI 後端及資料庫存取。
- `NeighborOnionapp`：整體應用及系統架構紀錄。
- `projecttest010522`：較早期的資料擷取／原型實驗，應與後續系統區分。

## 驗證範圍

本回顧以 Repository 內的原始碼與 README 為依據，未重新啟動舊服務、未連接歷史 Heroku endpoint，也未執行端到端測試。因此不宣稱目前部署可用或完整流程已通過測試。
