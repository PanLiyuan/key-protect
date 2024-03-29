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

# Excluindo chaves
{: #delete-keys}

É possível usar o {{site.data.keyword.keymanagementservicefull}} para excluir uma chave de criptografia e seus conteúdos, se você é um administrador para o espaço do {{site.data.keyword.cloud_notm}} ou instância de serviço {{site.data.keyword.keymanagementserviceshort}}.
{: shortdesc}

Quando você excluir uma chave, fragmentará permanentemente os seus conteúdos e os dados associados. A ação não pode ser invertida. [Destruindo recursos](/docs/services/key-protect?topic=key-protect-security-and-compliance#data-deletion) não é recomendado para ambientes de produção, mas pode ser útil para ambientes provisórios, como de teste ou QA.
{: important}

## Excluindo chaves com a GUI
{: #delete-key-gui}

Se você preferir excluir suas chaves de criptografia usando uma interface gráfica, será possível usar a GUI do {{site.data.keyword.keymanagementserviceshort}}.

[Depois de criar ou importar as chaves existentes no serviço](/docs/services/key-protect?topic=key-protect-create-root-keys),conclua as etapas a seguir para excluir a chave:

1. [Efetue login no console do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/){: new_window}.
2. Acesse **Menu** &gt; **Lista de recursos** para visualizar uma lista de seus recursos.
3. Em sua lista de recursos do {{site.data.keyword.cloud_notm}}, selecione a sua instância provisionada do {{site.data.keyword.keymanagementserviceshort}}.
4. Na página de detalhes do aplicativo, use a tabela de **Chaves** para procurar as chaves em seu serviço.
5. Clique no ícone ⋯ para abrir uma lista de opções para a chave que você deseja excluir.
6. No menu de opções, clique em **Excluir chave** e confirme a exclusão da chave na próxima tela.

Depois de excluir uma chave, a chave transita para o estado _Destruído_. As chaves nesse estado não são mais recuperáveis. Metadados que estão associados à chave, como a data de exclusão da chave, são mantidos no banco de dados do {{site.data.keyword.keymanagementserviceshort}}.

## Excluindo chaves com a API
{: #delete-key-api}

Para excluir uma chave e os seus conteúdos, faça uma chamada `DELETE` para o terminal a seguir.

```
https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID>
```

1. [Recupere suas credenciais de serviço e autenticação para trabalhar com chaves no serviço](/docs/services/key-protect?topic=key-protect-set-up-api).

2. Recupere o ID da chave que você gostaria de excluir.

    É possível recuperar o ID para uma chave especificada fazendo uma solicitação `GET /v2/keys/` ou visualizando suas chaves no painel do {{site.data.keyword.keymanagementserviceshort}}.

3. Execute o comando cURL a seguir para excluir permanentemente a chave e seus conteúdos.

    ```cURL
    curl -X DELETE \
      https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
    ```
    {: codeblock}
  
    Para trabalhar com chaves dentro de uma organização e um espaço do Cloud Foundry em sua conta, substitua `Bluemix-Instance` pelos cabeçalhos `Bluemix-org` e `Bluemix-space` apropriados. [Para obter mais informações, consulte o doc de referência da API do {{site.data.keyword.keymanagementserviceshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/key-protect){: new_window}.
    {: tip}

    Substitua as variáveis na solicitação de exemplo de acordo com a tabela a seguir.
    <table>
      <tr>
        <th>Variável</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td><strong>Necessário.</strong> A abreviação da região, como <code>us-south</code> ou <code>eu-gb</code>, que representa a área geográfica na qual reside sua instância de serviço do {{site.data.keyword.keymanagementserviceshort}}. Para obter mais informações, consulte <a href="/docs/services/key-protect?topic=key-protect-regions#endpoints">Terminais regionais em serviço</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>Necessário.</strong> O identificador exclusivo para a chave que você gostaria de excluir.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td><strong>Necessário.</strong> Seu token de acesso do {{site.data.keyword.cloud_notm}}. Inclua o conteúdo integral do token <code>IAM</code>, incluindo valor Bearer, na solicitação cURL. Para obter mais informações, veja <a href="/docs/services/key-protect?topic=key-protect-retrieve-access-token">Recuperando um token de acesso</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>Necessário.</strong> O identificador exclusivo que é designado para sua instância de serviço {{site.data.keyword.keymanagementserviceshort}}. Para obter mais informações, veja <a href="/docs/services/key-protect?topic=key-protect-retrieve-instance-ID">Recuperando um ID da instância</a>.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>Um cabeçalho que altera o comportamento do servidor para as operações <code>POST</code> e <code>DELETE</code>.</p><p>Ao configurar a variável <em>return_preference</em> para <code>return=minimal</code>, o serviço retorna uma resposta de exclusão bem-sucedida. Quando você configurar a variável para <code>return=representation</code>, o serviço retornará o material da chave e os metadados de chave.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve as variáveis que são necessárias para excluir chaves com a API do {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Se a variável _return_preference_ estiver configurada como `return=representation`, os detalhes da solicitação `DELETE` serão retornados no corpo da entidade de resposta. O objeto JSON a seguir mostra um valor retornado de exemplo.
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

    Para obter uma descrição detalhada dos parâmetros disponíveis, veja o {{site.data.keyword.keymanagementserviceshort}} [documento de referência da API de REST ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/key-protect){: new_window}.
