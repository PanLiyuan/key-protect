---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: Key Protect CLI plug-in, CLI reference

subcollection: key-protect

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.keymanagementserviceshort}} CLI 參考資料
{: #cli-reference}

您可以使用 {{site.data.keyword.keymanagementserviceshort}} CLI 外掛程式，以在 {{site.data.keyword.keymanagementserviceshort}} 實例中管理金鑰。
{:shortdesc}

若要安裝 CLI 外掛程式，請參閱[設定 CLI](/docs/services/key-protect?topic=key-protect-set-up-cli)。 

登入 [{{site.data.keyword.cloud_notm}} CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](/docs/cli?topic=cloud-cli-ibmcloud-cli){: new_window} 時，您會在有更新可用時收到通知。請務必將 CLI 保持最新，以便您可以使用適用於 {{site.data.keyword.keymanagementserviceshort}} CLI 外掛程式的指令及旗標。
{: tip}

## ibmcloud kp 指令
{: #ibmcloud-kp-commands}

您可以指定下列其中一個指令：

<table summary="管理金鑰用的指令">
    <thead>
        <th colspan="5">管理金鑰用的指令</th>
    </thead>
    <tbody>
        <tr>
            <td><a href="#kp-create">kp create</a></td>
            <td><a href="#kp-delete">kp delete</a></td>
            <td><a href="#kp-list">kp list</a></td>
            <td><a href="#kp-get">kp get</a></td>
            <td><a href="#kp-rotate">kp rotate</a></td>
        </tr>
        <tr>
            <td><a href="#kp-unwrap">kp unwrap</a></td>
            <td><a href="#kp-wrap">kp wrap</a></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
    <caption style="caption-side:bottom;">表 1. 管理金鑰用的指令</caption> 
 </table>

 <table summary="管理金鑰原則用的指令">
    <thead>
        <th colspan="5">管理金鑰原則用的指令</th>
    </thead>
    <tbody>
        <tr>
            <td><a href="#kp-policy-list">kp policy list</a></td>
            <td><a href="#kp-policy-get">kp policy get</a></td>
            <td><a href="#kp-policy-set">kp policy set</a></td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
    <caption style="caption-side:bottom;">表 2. 管理金鑰原則用的指令</caption> 
 </table>

## kp create
{: #kp-create}

在您指定的 {{site.data.keyword.keymanagementserviceshort}} 服務實例中[建立根金鑰](/docs/services/key-protect?topic=key-protect-create-root-keys)。 

```
ibmcloud kp create KEY_NAME -i INSTANCE_ID | $INSTANCE_ID
                   [-k, --key-material KEY_MATERIAL] 
                   [-s, --standard-key]
                   [--output FORMAT]
```
{:pre}

### 必要參數
{: #create-req-params}

<dl>
    <dt><code>KEY_NAME</code></dt>
        <dd>要指派給您的金鑰且人類可閱讀的唯一別名。</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

### 選用性參數
{: #create-opt-params}

<dl>
    <dt><code>-k, --key-material</code></dt>
        <dd>您要在服務中儲存及管理並以 base64 編碼的金鑰資料。若要匯入現有的金鑰，請提供 256 位元的金鑰。若要產生新的金鑰，請省略 <code>--key-material</code> 參數。</dd>
    <dt><code>-s, --standard-key</code></dt>
        <dd>唯有在您想要建立<a href="/docs/services/key-protect?topic=key-protect-envelope-encryption#key-types">標準金鑰</a>時才設定此參數。若要產生根金鑰，請省略 <code>--standard-key</code> 參數。</dd>
    <dt><code>--output</code></dt>
        <dd>設定 CLI 輸出格式。依預設，所有指令都會以表格格式列印。若要將輸出格式變更為 JSON，請使用 <code>--output json</code>。</dd>
</dl>

## kp delete
{: #kp-delete}

[刪除金鑰](/docs/services/key-protect?topic=key-protect-delete-keys)（儲存在您的 {{site.data.keyword.keymanagementserviceshort}} 服務中）。

```
ibmcloud kp delete KEY_ID -i INSTANCE_ID | $INSTANCE_ID
```
{: pre}

### 必要參數
{: #delete-req-params}

<dl>
   <dt><code>KEY_ID</code></dt>
   <dd>您要刪除之金鑰的 ID。若要擷取可用金鑰的清單，請執行 <a href="#kp-list">kp list</a> 指令。</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

## kp list
{: #kp-list}

列出 {{site.data.keyword.keymanagementserviceshort}} 服務實例中可用的最後 200 個金鑰。

```
ibmcloud kp list -i INSTANCE_ID | $INSTANCE_ID
```
{: pre}

### 必要參數
{: #list-req-params}

<dl>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

### 選用性參數
{: #list-opt-params}

<dl>
    <dt><code>--output</code></dt>
        <dd>設定 CLI 輸出格式。依預設，所有指令都會以表格格式列印。若要將輸出格式變更為 JSON，請使用 <code>--output json</code>。</dd>
</dl>

## kp get
{: #kp-get}

擷取金鑰的詳細資料，例如，金鑰 meta 資料和金鑰資料。

如果金鑰被指定為根金鑰，則系統無法傳回該金鑰的金鑰資料。

```
ibmcloud kp get KEY_ID -i INSTANCE_ID | $INSTANCE_ID
```
{: pre}

### 必要參數
{: #get-req-params}

<dl>
   <dt><code>KEY_ID</code></dt>
        <dd>您要擷取之金鑰的 ID。若要擷取可用金鑰的清單，請執行 <a href="#kp-list">kp list</a> 指令。</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

### 選用性參數
{: #get-opt-params}

<dl>
    <dt><code>--output</code></dt>
        <dd>設定 CLI 輸出格式。依預設，所有指令都會以表格格式列印。若要將輸出格式變更為 JSON，請使用 <code>--output json</code>。</dd>
</dl>

## kp rotate
{: #kp-rotate}

[替換根金鑰](/docs/services/key-protect?topic=key-protect-wrap-keys)（儲存在您的 {{site.data.keyword.keymanagementserviceshort}} 服務中）。

```
ibmcloud kp rotate KEY_ID -i INSTANCE_ID | $INSTANCE_ID
                 [-k, --key-material KEY_MATERIAL] 
```
{: pre}

### 必要參數
{: #rotate-req-params}

<dl>
    <dt><code>KEY_ID</code></dt>
        <dd>您要替換之根金鑰的 ID。</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

### 選用性參數
{: #rotate-opt-params}

<dl>
    <dt><code>-k, --key-material</code></dt>
        <dd>您要用於替換現有根金鑰並以 base64 編碼的金鑰資料。若要替換一開始匯入到服務的金鑰，請提供新的 256 位元金鑰。若要替換一開始在 {{site.data.keyword.keymanagementserviceshort}} 中產生的金鑰，請省略 <code>--key-material</code> 參數。</dd>
    <dt><code>--output</code></dt>
        <dd>設定 CLI 輸出格式。依預設，所有指令都會以表格格式列印。若要將輸出格式變更為 JSON，請使用 <code>--output json</code>。</dd>
</dl>

## kp wrap
{: #kp-wrap}

使用儲存在您提供之 {{site.data.keyword.keymanagementserviceshort}} 服務實例中的根金鑰來[包裝資料加密金鑰](/docs/services/key-protect?topic=key-protect-wrap-keys)。

```
ibmcloud kp wrap KEY_ID -i INSTANCE_ID | $INSTANCE_ID
                 [-p, --plaintext DATA_KEY] 
                 [-a, --aad ADDITIONAL_DATA]
```
{: pre}


### 必要參數
{: #wrap-req-params}

<dl>
    <dt><code>KEY_ID</code></dt>
        <dd>您要用於包裝之根金鑰的 ID。</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

### 選用性參數
{: #wrap-opt-params}

<dl>
    <dt><code>-a, --aad</code></dt>
        <dd>用來進一步保護金鑰的其他鑑別資料 (AAD)。如果在 wrap 提供，則在 unwrap 也必須提供。</dd>
    <dt><code>-p, --plaintext</code></dt>
        <dd>您要管理及保護並以 base64 編碼的資料加密金鑰 (DEK)。若要匯入現有的金鑰，請提供 256 位元的金鑰。若要產生並包裝新的 DEK，請省略 <code>--plaintext</code> 參數。</dd>
    <dt><code>--output</code></dt>
        <dd>設定 CLI 輸出格式。依預設，所有指令都會以表格格式列印。若要將輸出格式變更為 JSON，請使用 <code>--output json</code>。</dd>
</dl>

## kp unwrap
{: #kp-unwrap}

使用儲存在您 {{site.data.keyword.keymanagementserviceshort}} 服務實例中的根金鑰來[解除包裝資料加密金鑰](/docs/services/key-protect?topic=key-protect-unwrap-keys)。

```
ibmcloud kp unwrap KEY_ID -i INSTANCE_ID | $INSTANCE_ID 
                   CIPHERTEXT_FROM_WRAP
                   [-a, --aad ADDITIONAL_DATA, ..]
```
{: pre}

### 必要參數
{: #unwrap-req-params}

<dl>
    <dt><code>KEY_ID</code></dt>
        <dd>您用於起始 wrap 要求之根金鑰的 ID。</dd>
    <dt><code>CIPHERTEXT_FROM_WRAP</code></dt>
        <dd>在起始 wrap 作業期間傳回的已加密資料金鑰。</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

### 選用性參數
{: #unwrap-opt-params}

<dl>
    <dt><code>-a, --aad</code></dt>
        <dd><p>用來進一步保護金鑰的其他鑑別資料 (AAD)。您可以提供最多 255 個字串，每個以逗點分界。如果您在 wrap 提供 AAD，則必須在 unwrap 指定相同的 AAD。</p><p><b>重要事項：</b>{{site.data.keyword.keymanagementserviceshort}} 服務不會儲存其他的鑑別資料。如果您提供 AAD，請將資料儲存到安全的位置，以確保您可以在後續的 unwrap 要求期間存取及提供相同的 AAD。</p></dd>
    <dt><code>--output</code></dt>
        <dd>設定 CLI 輸出格式。依預設，所有指令都會以表格格式列印。若要將輸出格式變更為 JSON，請使用 <code>--output json</code>。</dd>
</dl>

## kp policy list
{: #kp-policy-list}

列出與您指定根金鑰相關聯的原則。

```
ibmcloud kp policy list KEY_ID -i INSTANCE_ID | $INSTANCE_ID
```
{: pre}

### 必要參數
{: #policy-list-req-params}

<dl>
    <dt><code>KEY_ID</code></dt>
        <dd>您要查詢之根金鑰的 ID。若要擷取可用金鑰的清單，請執行 <a href="#kp-list">kp list</a> 指令。</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

### 選用性參數
{: #policy-list-opt-params}

<dl>
    <dt><code>--output</code></dt>
        <dd>設定 CLI 輸出格式。依預設，所有指令都會以表格格式列印。若要將輸出格式變更為 JSON，請使用 <code>--output json</code>。</dd>
</dl>

## kp policy get
{: #kp-policy-get}

擷取金鑰原則的詳細資料，例如，金鑰的自動替換間隔。

```
ibmcloud kp policy get KEY_ID -i INSTANCE_ID | $INSTANCE_ID
```
{: pre}

### 必要參數
{: #policy-get-req-params}

<dl>
   <dt><code>KEY_ID</code></dt>
        <dd>您要查詢之金鑰的 ID。若要擷取可用金鑰的清單，請執行 <a href="#kp-list">kp list</a> 指令。</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

### 選用性參數
{: #policy-get-opt-params}

<dl>
    <dt><code>--output</code></dt>
        <dd>設定 CLI 輸出格式。依預設，所有指令都會以表格格式列印。若要將輸出格式變更為 JSON，請使用 <code>--output json</code>。</dd>
</dl>

## kp policy set
{: #kp-policy-set}

建立或取代與您指定根金鑰相關聯的原則。

```
ibmcloud kp policy set KEY_ID -i INSTANCE_ID | $INSTANCE_ID
                 --set-type POLICY_TYPE 
                 [--policy INTERVAL]
```
{: pre}

### 必要參數
{: #policy-set-req-params}

<dl>
   <dt><code>KEY_ID</code></dt>
        <dd>您要查詢之金鑰的 ID。若要擷取可用金鑰的清單，請執行 <a href="#kp-list">kp list</a> 指令。</dd>
   <dt><code>--set-type</code></dt>
        <dd>指定您要設定的原則類型。若要設定替換原則，請使用 <code>--set-type rotation</code>。</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>識別您 {{site.data.keyword.keymanagementserviceshort}} 服務實例的 {{site.data.keyword.cloud_notm}} 實例 ID。</dd>
</dl>

### 選用性參數
{: #policy-set-opt-params}

<dl>
   <dt><code>-p, --policy</code></dt>
        <dd>指定金鑰的替換時間間隔（以月為單位）。預設值是 1。</dd>
    <dt><code>--output</code></dt>
        <dd>設定 CLI 輸出格式。依預設，所有指令都會以表格格式列印。若要將輸出格式變更為 JSON，請使用 <code>--output json</code>。</dd>
</dl>

