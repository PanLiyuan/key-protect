---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: delete key, delete key API examples

subcollection: key-protect

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 刪除金鑰
{: #delete-keys}

如果您是 {{site.data.keyword.cloud_notm}} 空間或 {{site.data.keyword.keymanagementserviceshort}} 服務實例的管理者，可以使用 {{site.data.keyword.keymanagementservicefull}} 來刪除加密金鑰及其內容。
{: shortdesc}

當您刪除金鑰時，會永久地清除其內容及相關聯的資料。無法回復此動作。不建議在正式作業環境下[破壞資源](/docs/services/key-protect?topic=key-protect-security-and-compliance#data-deletion)，但可能適用於測試或 QA 這類暫時性環境。
{: important}

## 使用 GUI 刪除金鑰
{: #delete-key-gui}

如果您偏好使用圖形介面來刪除加密金鑰，可以使用 {{site.data.keyword.keymanagementserviceshort}} GUI。

[在建立金鑰或將現有金鑰匯入到服務之後](/docs/services/key-protect?topic=key-protect-create-root-keys)，請完成下列步驟來刪除金鑰：

1. [登入 {{site.data.keyword.cloud_notm}} 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/){: new_window}。
2. 移至**功能表** &gt; **資源清單**以檢視資源的清單。
3. 從 {{site.data.keyword.cloud_notm}} 資源清單，選取已佈建的 {{site.data.keyword.keymanagementserviceshort}} 實例。
4. 在應用程式詳細資料頁面上，使用**金鑰**表格，以瀏覽服務中的金鑰。
5. 按一下 ⋯ 圖示，以開啟您要刪除之金鑰的選項清單。
6. 從選項功能表，按一下**刪除金鑰**，並在下一個畫面中確認刪除金鑰。

刪除金鑰之後，金鑰會轉移至_已破壞_ 狀態。無法再回復這種狀態下的金鑰。與金鑰相關聯的 meta 資料（例如金鑰刪除日期）會保存在 {{site.data.keyword.keymanagementserviceshort}} 資料庫中。

## 使用 API 刪除金鑰
{: #delete-key-api}

若要刪除金鑰及其內容，請對下列端點進行 `DELETE` 呼叫。

```
https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID>
```

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/key-protect?topic=key-protect-set-up-api)。

2. 擷取您要刪除之金鑰的 ID。

    您可以擷取指定金鑰的 ID，方法是提出 `GET /v2/keys/` 要求，或在 {{site.data.keyword.keymanagementserviceshort}} 儀表板中檢視金鑰。

3. 執行下列 cURL 指令，以永久地刪除金鑰及其內容。

    ```cURL
    curl -X DELETE \
      https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
    ```
    {: codeblock}
  
    若要在您帳戶的 Cloud Foundry 組織及空間內使用金鑰，請將 `Bluemix-Instance` 取代為適當的 `Bluemix-org` 及 `Bluemix-space` 標頭。[如需相關資訊，請參閱 {{site.data.keyword.keymanagementserviceshort}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/key-protect){: new_window}。
    {: tip}

    根據下表取代範例要求中的變數。
    <table>
      <tr>
        <th>變數</th>
        <th>說明</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td><strong>必要。</strong>代表 {{site.data.keyword.keymanagementserviceshort}} 服務實例所在地理區域的地區縮寫，例如 <code>us-south</code> 或 <code>eu-gb</code>。如需相關資訊，請參閱<a href="/docs/services/key-protect?topic=key-protect-regions#endpoints">地區服務端點</a>。</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>必要。</strong>您要刪除之金鑰的唯一 ID。</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td><strong>必要。</strong>您的 {{site.data.keyword.cloud_notm}} 存取記號。請在 cURL 要求中包含 <code>IAM</code> 記號的完整內容，包括 Bearer 值。如需相關資訊，請參閱<a href="/docs/services/key-protect?topic=key-protect-retrieve-access-token">擷取存取記號</a>。</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>必要。</strong>指派給您的 {{site.data.keyword.keymanagementserviceshort}} 服務實例的唯一 ID。如需相關資訊，請參閱<a href="/docs/services/key-protect?topic=key-protect-retrieve-instance-ID">擷取實例 ID</a>。</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>變更 <code>POST</code> 及 <code>DELETE</code> 作業之伺服器行為的標頭。</p><p>當您將 <em>return_preference</em> 變數設為 <code>return=minimal</code> 時，服務會傳回成功刪除回應。當您將變數設為 <code>return=representation</code> 時，服務會傳回金鑰資料及金鑰 meta 資料。</p></td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明使用 {{site.data.keyword.keymanagementserviceshort}} API 刪除金鑰所需的變數。</caption>
    </table>

    如果 _return_preference_ 變數設為 `return=representation`，則 `DELETE` 要求的詳細資料會在回應實體內文中傳回。下列 JSON 物件顯示回覆值範例。
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
      },
      "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    如需可用參數的詳細說明，請參閱 {{site.data.keyword.keymanagementserviceshort}} [REST API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/key-protect){: new_window}。
