---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: rotate encryption key, encryption key rotation, rotate key API examples 

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

# Rotating keys on-demand
{: #rotate-keys}

You can rotate your root keys on-demand by using {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

When you rotate your root key, you shorten the lifetime of the key, and you limit the amount of information that is protected by that key.   

To learn how key rotation helps you meet industry standards and cryptographic best practices, see [Rotating your encryption keys](/docs/services/key-protect?topic=key-protect-key-rotation).

Rotation is available only for root keys. To learn more about your key rotation options in {{site.data.keyword.keymanagementserviceshort}}, check out [Comparing your key rotation options](/docs/services/key-protect?topic=key-protect-key-rotation#compare-key-rotation-options).
{: note}

## Rotating root keys with the GUI
{: #rotate-key-gui}

If you prefer to rotate your root keys by using a graphical interface, you can use the {{site.data.keyword.keymanagementserviceshort}} GUI.

[After you create or import your existing root keys into the service](/docs/services/key-protect?topic=key-protect-create-root-keys), complete the following steps to rotate a key:

1. [Log in to the {{site.data.keyword.cloud_notm}} console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/){: new_window}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.keymanagementserviceshort}}.
4. On the application details page, use the **Keys** table to browse the keys in your service.
5. Click the ⋯ icon to open a list of options for the key that you want to rotate.
6. From the options menu, click **Rotate key** and confirm the rotation in the next screen.

If you imported the root key initially, you must provide new base64 encoded key material to rotate the key. For more information, see [Importing root keys with the GUI](/docs/services/key-protect?topic=key-protect-import-root-keys#import-root-key-gui).
{: note}

## Rotating root keys by using the API
{: #rotate-key-api}

[After you designate a root key in the service](/docs/services/key-protect?topic=key-protect-create-root-keys), you can rotate your key by making a `POST` call to the following endpoint.

```
https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service.](/docs/services/key-protect?topic=key-protect-set-up-api)

2. Copy the ID of the root key that you want to rotate.

3. Run the following cURL command to replace the key with new key material.

    ```cURL
    curl -X POST \
      'https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID>?action=rotate' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -d '{
        'payload: <key_material>'
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
        <td><strong>Required.</strong> The unique identifier for the root key that you want to rotate.</td>
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
        <td><varname>key_material</varname></td>
        <td>
          <p>The base64 encoded key material that you want to store and manage in the service. This value is required if you initially imported the key material when you added the key to the service.</p>
          <p>To rotate a key that was initially generated by {{site.data.keyword.keymanagementserviceshort}}, omit the <code>payload</code> attribute and pass an empty request entity-body. To rotate an imported key, provide a key material that meets the following requirements:</p>
          <p>
            <ul>
              <li>The key must be 128, 192, or 256 bits.</li>
              <li>The bytes of data, for example 32 bytes for 256 bits, must be encoded by using base64 encoding.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables that are needed to rotate a specified key in {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    A successful rotation request returns an HTTP `204 No Content` response, which indicates that your root key was replaced by new key material.

4. Optional: Verify that the key was rotated by running the following call to browse the keys in your {{site.data.keyword.keymanagementserviceshort}} service instance.

    ```cURL
    curl -X GET \
    https://<region>.kms.cloud.ibm.com/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>'
    ```
    {: codeblock}
  
    Review the `lastRotateDate` value in the response entity-body to inspect the date and time that your key was last rotated.
    
