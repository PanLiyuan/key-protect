---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: list encryption keys, view encryption key, retrieve encryption key, retrieve key API examples

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

# 檢視金鑰
{: #view-keys}

{{site.data.keyword.keymanagementservicefull}} 提供集中化的系統，以便檢視、管理及審核您的加密金鑰。請審核您的金鑰及對於金鑰的存取權限制，以確保資源安全。
{: shortdesc}

定期審核您的金鑰配置：

- 檢查金鑰的建立時間，並決定是否應該替換金鑰。
- [使用 {{site.data.keyword.cloudaccesstrailshort}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示") 監視對 {{site.data.keyword.keymanagementserviceshort}} 的 API 呼叫](/docs/services/cloud-activity-tracker/tutorials?topic=cloud-activity-tracker-kp){: new_window}。
- 檢查哪些使用者可以存取金鑰，以及存取層次是否適當。

如需審核資源存取權的相關資訊，請參閱[使用 Cloud IAM 管理使用者存取](/docs/services/key-protect?topic=key-protect-manage-access)。

## 使用 GUI 檢視金鑰
{: #view-keys-gui}

如果您偏好使用圖形介面來檢查服務中的金鑰，則可以使用 {{site.data.keyword.keymanagementserviceshort}} 儀表板。

[在建立金鑰或將現有金鑰匯入到服務之後](/docs/services/key-protect?topic=key-protect-create-root-keys)，請完成下列步驟來檢視金鑰。

1. [登入 {{site.data.keyword.cloud_notm}} 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/)。
2. 移至**功能表** &gt; **資源清單**以檢視資源的清單。
3. 從 {{site.data.keyword.cloud_notm}} 資源清單，選取已佈建的 {{site.data.keyword.keymanagementserviceshort}} 實例。
4. 從應用程式詳細資料頁面，瀏覽金鑰的一般特徵：

    <table>
      <tr>
        <th>直欄</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>已指派給您的金鑰且人類可閱讀的唯一別名。</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>{{site.data.keyword.keymanagementserviceshort}} 服務已指派給您金鑰的唯一金鑰 ID。您可以使用 ID 值，利用 [{{site.data.keyword.keymanagementserviceshort}} API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/key-protect) 來呼叫服務。</td>
      </tr>
      <tr>
        <td>狀態</td>
        <td>根據 [NIST 特殊出版品 800-57 的金鑰管理建議 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0) 的[金鑰狀態](/docs/services/key-protect?topic=key-protect-key-states)。這些狀態包括<i>啟動前</i>、<i>作用中</i>、<i>取消啟動</i> 及<i>已破壞</i>。</td>
      </tr>
      <tr>
        <td>類型</td>
        <td>說明服務內金鑰指定用途的[金鑰類型](/docs/services/key-protect?topic=key-protect-envelope-encryption#key-types)。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明<b>金鑰</b>表格</caption>
    </table>

## 使用 API 檢視金鑰
{: #view-keys-api}

您可以使用 {{site.data.keyword.keymanagementserviceshort}} API 擷取金鑰的內容。

### 擷取金鑰清單
{: #retrieve-keys-api}

如需高階視圖，您可以對下列端點發出 `GET` 呼叫，來瀏覽已佈建之 {{site.data.keyword.keymanagementserviceshort}} 實例中管理的金鑰。

```
https://<region>.kms.cloud.ibm.com/api/v2/keys
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/key-protect?topic=key-protect-set-up-api)。

2. 執行下列 cURL 指令，以檢視金鑰的一般特徵。

    ```cURL
    curl -X GET \
    https://<region>.kms.cloud.ibm.com/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
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
        <td><varname>IAM_token</varname></td>
        <td><strong>必要。</strong>您的 {{site.data.keyword.cloud_notm}} 存取記號。請在 cURL 要求中包含 <code>IAM</code> 記號的完整內容，包括 Bearer 值。如需相關資訊，請參閱<a href="/docs/services/key-protect?topic=key-protect-retrieve-access-token">擷取存取記號</a>。</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>必要。</strong>指派給您的 {{site.data.keyword.keymanagementserviceshort}} 服務實例的唯一 ID。如需相關資訊，請參閱<a href="/docs/services/key-protect?topic=key-protect-retrieve-instance-ID">擷取實例 ID</a>。</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>用來追蹤及關聯交易的唯一 ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. 說明使用 {{site.data.keyword.keymanagementserviceshort}} API 檢視金鑰所需的變數</caption>
    </table>

    成功的 `GET api/v2/keys` 要求會傳回您的 {{site.data.keyword.keymanagementserviceshort}} 服務實例中可用的金鑰集合。

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
      "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true,
          "imported": false
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastRotateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false,
          "imported": true
        }
      ]
    }
    ```
    {:screen}

    依預設，`GET api/v2/keys` 會傳回前 2000 個金鑰，但您可以在查詢時間使用 `limit` 參數來調整此限制。若要進一步瞭解 `limit` 及 `offset`，請參閱[擷取金鑰子集](#retrieve-subset-keys-api)。
    {: tip}

### 擷取金鑰子集
{: #retrieve-subset-keys-api}

在查詢時間指定 `limit` 及 `offset` 參數，即可擷取金鑰子集，並從您指定的 `offset` 值開始。 

例如，您的 {{site.data.keyword.keymanagementserviceshort}} 服務實例中所儲存的金鑰可能共有 3000 個，但您在發出 `GET /keys` 要求時要擷取 200 - 300 個金鑰。 

您可以使用下列範例要求來擷取一組不同的金鑰。

  ```cURL
  curl -X GET \
  https://<region>.kms.cloud.ibm.com/api/v2/keys?offset=<offset>&limit=<limit> \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  ```
  {: codeblock}

  根據下表，取代要求中的 `limit` 及 `offset` 變數。
  <table>
    <tr>
      <th>變數</th>
      <th>說明</th>
    </tr>
    <tr>
      <td><p><varname>offset</varname></p></td>
      <td>
        <p>要跳過的金鑰數目。</p> 
        <p>例如，如果您的實例中有 50 個金鑰，而且您要列出 26 - 50 個金鑰，則請使用 <code>../keys?offset=25</code>。您也可以將 <code>offset</code> 與 <code>limit</code> 配對，以翻看可用資源。</p>
      </td>
    </tr>
    <tr>
      <td><p><varname>limit</varname></p></td>
      <td>
        <p>要擷取的金鑰數目。</p> 
        <p>例如，如果您的實例中有 100 個金鑰，而且您只要列出 10 個金鑰，則請使用 <code>../keys?limit=10</code>。<code>limit</code> 的最大值是 5000。</p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">表 2. 說明 <code>limit</code> 及 <code>offset</code> 變數</caption>
  </table>

如需使用注意事項，請參閱下列範例來設定 `limit` 及 `offset` 查詢參數。

<table>
  <tr>
    <th>URL</th>
    <th>說明</th>
  </tr>
  <tr>
    <td><code>.../keys</code></td>
    <td>列出您的所有可用資源，最多可列出前 2000 個金鑰。</td>
  </tr>
  <tr>
    <td><code>.../keys?limit=10</code></td>
    <td>列出前 10 個金鑰。</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=25&limit=50</code></td>
    <td>列出金鑰 26 - 50。</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=3000&limit=50</code></td>
    <td>列出金鑰 3001 - 3050。</td>
  </tr>
  <caption style="caption-side:bottom;">表 3. 提供 limit 及 offset 查詢參數的使用注意事項</caption>
</table>

偏移是資料集中特定金鑰的位置。`offset` 值是以零起始，這表示資料集中的第 10 個加密金鑰位於偏移 9。
{: tip}

### 依 ID 擷取金鑰
{: #retrieve-key-api}

若要檢視特定金鑰的詳細資訊，您可以對下列端點發出 `GET` 呼叫。

```
https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID>
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/key-protect?topic=key-protect-set-up-api)。

2. 擷取您想要存取或管理之金鑰的 ID。

    ID 值是用來存取金鑰的詳細資訊，例如金鑰資料本身。您可以擷取指定金鑰的 ID，方法是提出 `GET /v2/keys` 要求，或存取 {{site.data.keyword.keymanagementserviceshort}} GUI。

3. 執行下列 cURL 指令，以取得金鑰的詳細資料及金鑰資料。

    ```cURL
    curl -X GET \
      https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

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
        <td><varname>IAM_token</varname></td>
        <td><strong>必要。</strong>您的 {{site.data.keyword.cloud_notm}} 存取記號。請在 cURL 要求中包含 <code>IAM</code> 記號的完整內容，包括 Bearer 值。如需相關資訊，請參閱<a href="/docs/services/key-protect?topic=key-protect-retrieve-access-token">擷取存取記號</a>。</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>必要。</strong>指派給您的 {{site.data.keyword.keymanagementserviceshort}} 服務實例的唯一 ID。如需相關資訊，請參閱<a href="/docs/services/key-protect?topic=key-protect-retrieve-instance-ID">擷取實例 ID</a>。</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>用來追蹤及關聯交易的唯一 ID。</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>必要。</strong>您在[步驟 1](#retrieve-keys-api) 中擷取之金鑰的 ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 4. 說明使用 {{site.data.keyword.keymanagementserviceshort}} API 檢視指定金鑰所需的變數</caption>
    </table>

    成功的 `GET api/v2/keys/<key_ID>` 回應會傳回金鑰的詳細資料及金鑰資料。下列 JSON 物件顯示標準金鑰的回覆值範例。

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
        "resources": [
            {
                "id": "...",
            "type": "application/vnd.ibm.kms.key+json",
            "name": "Standard key",
            "description": "...",
            "state": 1,
            "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
                "mode": "GCM"
            },
            "extractable": true,
            "imported": false
        }
      ]
    }
    ```
    {:screen}

    如需可用參數的詳細說明，請參閱 {{site.data.keyword.keymanagementserviceshort}} [REST API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/key-protect){: new_window}。
