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

# Schlüssel löschen
{: #delete-keys}

Sie können {{site.data.keyword.keymanagementservicefull}} verwenden, um einen Verschlüsselungsschlüssel und seinen Inhalt zu löschen, wenn Sie der Administrator Ihres {{site.data.keyword.cloud_notm}}-Bereichs oder der {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz sind.
{: shortdesc}

Wenn Sie einen Schlüssel löschen, werden der Schlüsselinhalt und die zugehörigen Daten permanent zerstört. Die Aktion kann nicht rückgängig gemacht werden. Das [Löschen von Ressourcen](/docs/services/key-protect?topic=key-protect-security-and-compliance#data-deletion) wird für Produktionsumgebungen nicht empfohlen, kann aber für temporäre Umgebungen wie Test- oder QS-Umgebungen nützlich sein.
{: important}

## Schlüssel mit GUI löschen
{: #delete-key-gui}

Wenn Sie die Löschung von Verschlüsselungsschlüssel über eine grafische Oberfläche bevorzugen, dann können Sie hierzu die {{site.data.keyword.keymanagementserviceshort}}-GUI verwenden.

[Nach dem Erstellen oder Importieren der vorhandenen Schlüssel in den Service](/docs/services/key-protect?topic=key-protect-create-root-keys) müssen Sie die folgenden Schritte ausführen, um einen Schlüssel zu löschen:

1. [Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/){: new_window} an.
2. Rufen Sie **Menü** &gt; **Ressourcenliste** auf, um eine Liste Ihrer Ressourcen anzuzeigen.
3. Wählen Sie in der {{site.data.keyword.cloud_notm}}-Ressourcenliste die bereitgestellte Instanz von {{site.data.keyword.keymanagementserviceshort}} aus.
4. Verwenden Sie auf der Seite mit den Anwendungsdetails die Tabelle **Schlüssel**, um die Schlüssel im Service zu durchsuchen.
5. Klicken Sie auf das Symbol ⋯, um eine Liste mit Optionen für den Schlüssel zu öffnen, den Sie löschen möchten.
6. Klicken Sie im Auswahlmenü auf **Schlüssel löschen** und bestätigen Sie die Schlüssellöschung in der nächsten Anzeige.

Sobald der Schlüssel gelöscht wurde, nimmt der Schlüssel den Status _Gelöscht_ an. Schlüssel, die sich in diesem Status befinden, sind nicht wiederherstellbar. Die zugehörigen Metadaten für den Schlüssel (z. B. das Löschdatum des Schlüssels) werden in der {{site.data.keyword.keymanagementserviceshort}}-Datenbank aufbewahrt.

## Schlüssel mit API löschen
{: #delete-key-api}

Um einen Schlüssel und seinen Inhalt zu löschen, müssen Sie einen `DELETE`-Aufruf für den folgenden Endpunkt ausführen.

```
https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID>
```

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/key-protect?topic=key-protect-set-up-api)

2. Rufen Sie die ID des Schlüssels ab, den Sie löschen möchten.

    Sie können die ID für einen angegebenen Schlüssel abrufen, indem Sie die Anforderung `GET /v2/keys/` absetzen oder indem Sie die Schlüssel im {{site.data.keyword.keymanagementserviceshort}}-Dashboard anzeigen.

3. Führen Sie den folgenden cURL-Befehl aus, um den Schlüssel und seinen Inhalt dauerhaft zu löschen.

    ```cURL
    curl -X DELETE \
      https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
    ```
    {: codeblock}
  
    Um mit Schlüsseln in Cloud Foundry-Organisationen und -Bereichen zu arbeiten, ersetzen Sie `Bluemix-Instance` durch die entsprechenden Header `Bluemix-org` und `Bluemix-space`. [Weitere Informationen finden Sie in der {{site.data.keyword.keymanagementserviceshort}}-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/key-protect){: new_window}.
    {: tip}

    Ersetzen Sie die Variablen in der Beispielanforderung anhand der Angaben in der folgenden Tabelle.
    <table>
      <tr>
        <th>Variable</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td><strong>Erforderlich.</strong> Die Regionsabkürzung, z. B. <code>us-south</code> oder <code>eu-gb</code>, die den geografischen Bereich darstellt, in dem sich Ihre {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz befindet. Weitere Informationen finden Sie in <a href="/docs/services/key-protect?topic=key-protect-regions#endpoints">Regionale Serviceendpunkte</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>Erforderlich.</strong> Die eindeutige ID für den Schlüssel, der gelöscht werden soll.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td><strong>Erforderlich.</strong> Ihr {{site.data.keyword.cloud_notm}}-Zugriffstoken. Nehmen Sie den vollständigen Inhalt des <code>IAM</code>-Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf. Weitere Informationen finden Sie in <a href="/docs/services/key-protect?topic=key-protect-retrieve-access-token">Zugriffstoken abrufen</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>Erforderlich.</strong> Die eindeutige ID, die Ihrer {{site.data.keyword.keymanagementserviceshort}}-Serviceinstanz zugewiesen ist. Weitere Informationen finden Sie in <a href="/docs/services/key-protect?topic=key-protect-retrieve-instance-ID">Instanz-ID abrufen</a>.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>Ein Header, der das Serververhalten für <code>POST</code>- und <code>DELETE</code>-Operationen ändert.</p><p>Wenn Sie die Variable <em>return_preference</em> auf <code>return=minimal</code> festlegen, gibt der Service eine erfolgreiche Antwort auf das Löschen zurück. Wenn Sie für die Variable <code>return=representation</code> festlegen, werden sowohl die Schlüsselinformationen als auch die Metadaten des Schlüssels zurückgegeben.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Variablen, die zum Löschen von Schlüsseln mit der {{site.data.keyword.keymanagementserviceshort}}-API erforderlich sind.</caption>
    </table>

    Wenn für die Variable _return_preference_ der Wert `return=representation` festgeleg wird, werden die Details der Anforderung `DELETE` im Entitätshauptteil der Antwort zurückgegeben. Das folgende JSON-Objekt zeigt ein Beispiel für einen zurückgegebenen Wert.
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

    Eine detaillierte Beschreibung der verfügbaren Parameter finden Sie in der [REST-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/key-protect){: new_window} für {{site.data.keyword.keymanagementserviceshort}}.
