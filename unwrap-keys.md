---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-14"

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

# Unwrapping keys
{: #unwrap-keys}

You can unwrap a data encryption key (DEK) to access its contents by using the {{site.data.keyword.keymanagementservicefull}} API, if you are a privileged user. Unwrapping a DEK decrypts and checks the integrity of its contents, returning the original key material to your {{site.data.keyword.cloud_notm}} data service.
{: shortdesc}

To learn how key wrapping helps you control the security of at-rest data in the cloud, see [Protecting data with envelope encryption](/docs/services/key-protect?topic=key-protect-envelope-encryption).

## Unwrapping keys by using the API
{: #unwrap-key-api}

[After you make a wrap call to the service](/docs/services/key-protect?topic=key-protect-wrap-keys), you can unwrap a specified data encryption key (DEK) to access its contents by making a `POST` call to the following endpoint.

```
https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_id>?action=unwrap
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/services/key-protect?topic=key-protect-set-up-api).

2. Copy the ID of the root key that you used to perform the initial wrap request.

    You can retrieve the ID for a key by making a `GET /v2/keys` request, or by viewing your keys in the {{site.data.keyword.keymanagementserviceshort}} GUI.

3. Copy the `ciphertext` value that was returned during the initial wrap request.

4. Run the following cURL command to decrypt and authenticate the key material.

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

    Replace the variables in the example request according to the following table.
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td><strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>eu-gb</code>, that represents the geographic area where your {{site.data.keyword.keymanagementserviceshort}} service instance resides. For more information, see <a href="/docs/services/key-protect?topic=key-protect-regions#service-endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier for the root key that you used for the initial wrap request.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td><strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/services/key-protect?topic=key-protect-retrieve-access-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. For more information, see <a href="/docs/services/key-protect?topic=key-protect-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>The additional authentication data (AAD) that is used to further secure the key. Each string can hold up to 255 characters. If you supply AAD when you make a wrap call to the service, you must specify the same AAD during the unwrap call.</td>
      </tr>
      <tr>
        <td><varname>encrypted_data_key</varname></td>
        <td><strong>Required.</strong> The <code>ciphertext</code> value that was returned during a wrap operation.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables that are needed to unwrap keys in {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    The original key material is returned in the response entity-body. The following JSON object shows an example returned value.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg=="
    }
    ```
    {:screen}
