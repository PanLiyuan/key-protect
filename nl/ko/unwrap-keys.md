---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-13"

keywords: unwrap key, decrypt key, decrypt data encryption key, access data encryption key, envelope encryption API examples

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

# 키 랩핑 해제
{: #unwrap-keys}

권한 있는 사용자인 경우 {{site.data.keyword.keymanagementservicefull}} API를 사용하여 해당 컨텐츠에 액세스하도록 데이터 암호화 키(DEK)를 랩핑 해제할 수 있습니다. DEK를 랩핑 해제하면 해당 컨텐츠의 무결성이 복호화되고 검사되며, 원래 키 자료가 {{site.data.keyword.cloud_notm}} 데이터 서비스에 리턴됩니다.
{: shortdesc}

키 랩핑을 통해 클라우드에서 저장 데이터의 보안을 제어하는 방법을 알아보려면 [엔벨로프 암호화로 데이터 보호](/docs/services/key-protect?topic=key-protect-envelope-encryption)를 참조하십시오.

## API를 사용하여 키 랩핑 해제
{: #unwrap-key-api}

[서비스에 대한 랩핑 호출을 작성하면](/docs/services/key-protect?topic=key-protect-wrap-keys) 다음 엔드포인트에 대한 `POST` 호출을 작성하여 해당 컨텐츠에 액세스하도록 지정된 데이터 암호화 키(DEK)를 랩핑 해제할 수 있습니다.

```
https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_id>?action=unwrap
```
{: codeblock}

1. [서비스 및 인증용 인증 정보를 검색하여 서비스에서 키에 대한 작업을 수행](/docs/services/key-protect?topic=key-protect-set-up-api)하십시오.

2. 초기 랩핑 요청을 수행하는 데 사용한 루트 키의 ID를 복사하십시오.

    `GET /v2/keys` 요청을 작성하거나 {{site.data.keyword.keymanagementserviceshort}} GUI에서 키를 확인하여 키의 ID를 검색할 수 있습니다.

3. 초기 랩핑 요청 중에 리턴된 `ciphertext` 값을 복사하십시오.

4. 다음 cURL 명령을 실행하여 키 자료를 복호화하고 인증하십시오.

    ```cURL
    curl -X POST \
      'https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -d '{
      "ciphertext": "<encrypted_data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
    }'
    ```
    {: codeblock}

    계정에서 Cloud Foundry 조직과 영역 내의 키에 대한 작업을 수행하려면 `Bluemix-Instance`를 적절한 `Bluemix-org` 및 `Bluemix-space` 헤더로 바꾸십시오. 자세한 정보는 [{{site.data.keyword.keymanagementserviceshort}} API 참조 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/key-protect){: new_window}를 참조하십시오.
    {: tip}

    다음 표에 따라 예제 요청의 변수를 대체하십시오.
    <table>
      <tr>
        <th>변수</th>
        <th>설명</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td><strong>필수.</strong> {{site.data.keyword.keymanagementserviceshort}} 서비스 인스턴스가 상주하는 지리적 영역을 표시하는 지역 약어(예: <code>us-south</code> 또는 <code>eu-gb</code>)입니다. 자세한 정보는 <a href="/docs/services/key-protect?topic=key-protect-regions#endpoints">지역 서비스 엔드포인트</a>를 참조하십시오.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>필수.</strong> 초기 랩핑 요청에 사용한 루트 키의 고유 ID입니다.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td><strong>필수.</strong> 사용자의 {{site.data.keyword.cloud_notm}} 액세스 토큰입니다. cURL 요청에 Bearer 값 등 <code>IAM</code> 토큰의 전체 컨텐츠를 포함하십시오. 자세한 정보는 <a href="/docs/services/key-protect?topic=key-protect-retrieve-access-token">액세스 토큰 검색</a>을 참조하십시오.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>필수.</strong> {{site.data.keyword.keymanagementserviceshort}} 서비스 인스턴스에 지정된 고유 ID입니다. 자세한 정보는 <a href="/docs/services/key-protect?topic=key-protect-retrieve-instance-ID">인스턴스 ID 검색</a>을 참조하십시오.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>트랜잭션을 추적하고 상관시키는 데 사용되는 고유 ID입니다.</td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>키를 보안하는 데 사용되는 추가 인증 데이터(AAD)입니다. 각 문자열은 최대 255자입니다. 서비스에 대한 랩핑 호출을 작성할 때 AAD를 제공하는 경우에는 랩핑 해제 호출 중에 동일한 AAD를 지정해야 합니다.</td>
      </tr>
      <tr>
        <td><varname>encrypted_data_key</varname></td>
        <td><strong>필수.</strong> 랩핑 오퍼레이션 중에 리턴된 <code>ciphertext</code> 값입니다.</td>
      </tr>
      <caption style="caption-side:bottom;">표 1. {{site.data.keyword.keymanagementserviceshort}}에서 키를 랩핑 해제하는 데 필요한 변수에 대한 설명</caption>
    </table>

    원래 키 자료는 응답 엔티티-본문에 리턴됩니다. 다음 JSON 오브젝트는 예제 리턴값을 표시합니다.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg=="
    }
    ```
    {:screen}
