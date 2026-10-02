# Azure AI Search Hotel Index 範例

這個專案示範如何使用 Azure AI Search Python SDK 建立 hotel 索引、定義欄位、設定語意搜尋與評分設定檔，並將範例資料上傳到 Azure AI Search 服務中。

## 專案簡介

本範例主要包含兩個 Python 腳本：

- `azure_ai_search_hotel_index.py`
  - 建立索引
  - 定義索引欄位與結構
  - 設定語意搜尋
  - 設定評分配置
  - 上傳 hotel 文件
  - 刪除索引

- `azure_ai_search_index_maintenance.py`
  - 取得索引資訊
  - 查詢索引文件數量
  - 清除索引中的所有文件
  - 記錄執行結果

## 專案檔案

- `azure_ai_search_hotel_index.py`：索引建立與資料上傳腳本
- `azure_ai_search_index_maintenance.py`：索引維護腳本
- `hotels-small.json`：Hotel 範例資料
- `text-sample.json`：測試文字資料
- `README.md`：專案說明文件
- `app.log`：執行日誌（若程式有執行）

## 功能特色

- 建立 `hotel` 索引
- 定義 `hotelId`、`hotelName`、`description`、`category`、`tags`、`location`、`address`、`rooms` 等欄位
- 支援 `ComplexField` 與 `collection` 欄位
- 啟用語意搜尋（Semantic Search）
- 配置評分設定檔（Scoring Profile）
- 支援 CORS 設定
- 可批次上傳檔案資料
- 可清除索引中的全部文件

## 需求

- Python 3.9+
- Azure AI Search 服務
- Azure AI Search API Key
- Azure AI Search Endpoint

## 安裝依賴

在專案根目錄執行：

```bash
pip install azure-search-documents python-dotenv rich
```

如果你使用虛擬環境，請先啟用它後再安裝套件。

## 環境變數設定

在專案根目錄新增 `.env` 檔案，內容如下：

```env
AZURE_AI_SEARCH_API_ENDPOINT=https://<your-search-service>.search.windows.net
AZURE_AI_SEARCH_API_KEY=<your-api-key>
AZURE_AI_SEARCH_HOTEL_INDEX_NAME=hotels
```

> 請將 `<your-search-service>`、`<your-api-key>` 替換成實際 Azure AI Search 服務資訊。

## 執行方式

### 1. 建立索引與上傳資料

```bash
python azure_ai_search_hotel_index.py
```

這個腳本會：

- 建立 hotel 索引
- 定義索引欄位
- 設定語意搜尋
- 上傳 `hotels-small.json` 的資料

如果你想刪除既有索引或上傳資料，可以在腳本底部取消註解：

```python
if __name__ == "__main__":
    # _delete_index()
    _create_index()
    # _upload_documents()
```

### 2. 維護索引

```bash
python azure_ai_search_index_maintenance.py
```

這個腳本會：

- 取得索引資訊
- 查詢索引文件數量
- 清除所有文件
- 記錄執行日誌

## 常用操作

### 刪除索引

在 `azure_ai_search_hotel_index.py` 中取消註解：

```python
_delete_index()
```

### 上傳資料

在 `azure_ai_search_hotel_index.py` 中取消註解：

```python
_upload_documents()
```

### 清空索引文件

在 `azure_ai_search_index_maintenance.py` 中執行：

```python
_clear_index_documents_with_wait()
```

## 執行順序建議

建議使用流程如下：

1. 建立索引
2. 上傳資料
3. 查詢文件數量
4. 需要時清除資料或刪除索引

## 日誌

程式會將資訊寫入 `app.log`，方便追蹤建立索引、上傳資料與錯誤處理的記錄。

## 注意事項

- 確認 `.env` 設定正確
- 確認 Azure AI Search API Key 有效
- 索引名稱不可重複，避免覆蓋既有索引
- 若變更資料結構，請同步更新索引欄位定義

## 參考

此範例基於 Azure AI Search Python SDK，適合用作：

- 索引建立範例
- 搜尋資料上傳範例
- 搜尋索引維護範例
- Azure AI Search 學習範例

## License

本專案僅作為教學與範例用途，若要用於正式環境，請依照 Azure 服務與公司政策進行驗證與部署。