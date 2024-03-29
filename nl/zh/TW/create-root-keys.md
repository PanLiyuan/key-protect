---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: create root key, create key-wrapping key, create CRK, create CMK, create customer key, create root key in Key Protect, create key-wrapping key in Key Protect, create customer key in Key Protect, key-wrapping key, root key API examples

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

# 建立根金鑰
{: #create-root-keys}

您可以利用 {{site.data.keyword.keymanagementservicefull}}，以使用 {{site.data.keyword.keymanagementserviceshort}} GUI 或使用 {{site.data.keyword.keymanagementserviceshort}} API 透過程式設計方式，來建立根金鑰。
{: shortdesc}

根金鑰是用來保護雲端中已加密資料安全的對稱金鑰包裝金鑰。如需根金鑰的相關資訊，請參閱[使用封套加密保護資料](/docs/services/key-protect?topic=key-protect-envelope-encryption)。 

## 使用 GUI 建立根金鑰
{: #create-root-key-gui}

[在建立服務的實例之後](/docs/services/key-protect?topic=key-protect-provision)，請完成下列步驟以使用 {{site.data.keyword.keymanagementserviceshort}} GUI 來建立根金鑰。

1. [登入 {{site.data.keyword.cloud_notm}} 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}){: new_window}。
2. 移至**功能表** &gt; **資源清單**以檢視資源的清單。
3. 從 {{site.data.keyword.cloud_notm}} 資源清單，選取已佈建的 {{site.data.keyword.keymanagementserviceshort}} 實例。
4. 若要建立新的金鑰，請按一下**新增金鑰**，然後選取**建立金鑰**視窗。

    指定金鑰的詳細資料：

    <table>
      <tr>
        <th>設定</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>
          <p>方便識別金鑰且人類可閱讀的唯一別名。</p>
          <p>若要保護您的隱私權，請確定金鑰名稱未包含個人識別資訊 (PII)（例如您的姓名或位置）。</p>
        </td>
      </tr>
      <tr>
        <td>金鑰類型</td>
        <td>您要在 {{site.data.keyword.keymanagementserviceshort}} 中管理的<a href="/docs/services/key-protect?topic=key-protect-envelope-encryption#key-types">金鑰類型</a>。從金鑰類型清單中，選取<b>根金鑰</b>。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明<b>建立金鑰</b>設定</caption>
    </table>

5. 當您填寫完金鑰的詳細資料時，請按一下**建立金鑰**以便確認。 

在服務中所建立的金鑰是 AES-GCM 演算法所支援的對稱 256 位元金鑰。為了提高安全，金鑰是由位於安全 {{site.data.keyword.cloud_notm}} 資料中心的 FIPS 140-2 Level 2 認證硬體安全模組 (HSM) 所產生。 

## 使用 API 建立根金鑰
{: #create-root-key-api}

對下列端點發出 `POST` 呼叫來建立根金鑰。

```
https://<region>.kms.cloud.ibm.com/api/v2/keys
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/key-protect?topic=key-protect-set-up-api)。

2. 使用下列 cURL 指令，來呼叫 [{{site.data.keyword.keymanagementserviceshort}} API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/key-protect){: new_window}。

    ```cURL
    curl -X POST \
      https://<region>.kms.cloud.ibm.com/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "extractable": <key_type>
       }
     ]
    }'
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
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p><strong>必要。</strong>方便識別金鑰且人類可閱讀的唯一名稱。</p>
          <p>重要事項：若要保護您的隱私權，請不要將個人資料儲存為金鑰的 meta 資料。</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>金鑰的延伸說明。</p>
          <p>重要事項：若要保護您的隱私權，請不要將個人資料儲存為金鑰的 meta 資料。</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>系統中的金鑰到期的日期和時間，以 RFC 3339 格式表示。如果省略 <code>expirationDate</code> 屬性，則金鑰不會到期。</td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>決定金鑰資料是否可以離開服務的布林值。</p>
          <p>當您將 <code>extractable</code> 屬性設為 <code>false</code> 時，服務會建立一個根金鑰，您可以將它用於 <code>wrap</code> 或 <code>unwrap</code> 作業。</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">表 1. 說明使用 {{site.data.keyword.keymanagementserviceshort}} API 新增根金鑰所需的變數</caption>
    </table>

    若要保護您個人資料的機密性，請在將金鑰新增至服務時避免輸入個人識別資訊 (PII)（例如您的姓名或位置）。如需其他 PII 範例，請參閱 [NIST 特殊出版品 800-122 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.nist.gov/publications/guide-protecting-confidentiality-personally-identifiable-information-pii){: new_window} 的第 2.2 節。
    {: important}

    成功的 `POST api/v2/keys` 回應會傳回您金鑰的 ID 值，以及其他 meta 資料。ID 是指派給您金鑰的唯一 ID，並用於後續的 {{site.data.keyword.keymanagementserviceshort}} API 呼叫。

3. 選用項目：執行下列呼叫來瀏覽 {{site.data.keyword.keymanagementserviceshort}} 服務實例中的金鑰，確認已建立金鑰。

    ```cURL
    curl -X GET \
      https://<region>.kms.cloud.ibm.com/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>'
    ```
    {: codeblock}

    在您使用服務建立根金鑰之後，金鑰會保留在 {{site.data.keyword.keymanagementserviceshort}} 的範圍內，而且無法擷取其金鑰資料。
    {: note} 

## 下一步為何？
{: #create-root-key-next-steps}

- 若要進一步瞭解如何使用封套加密來保護金鑰，請參閱[包裝金鑰](/docs/services/key-protect?topic=key-protect-wrap-keys)。
- 若要進一步瞭解如何以程式設計方式管理您的金鑰，[請參閱 {{site.data.keyword.keymanagementserviceshort}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/key-protect){: new_window}。
