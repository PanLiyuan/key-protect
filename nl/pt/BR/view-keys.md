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

# Visualizando chaves
{: #view-keys}

O {{site.data.keyword.keymanagementservicefull}} fornece um sistema centralizado para visualizar, gerenciar e auditar suas chaves de criptografia. Audite as suas chaves e as restrições de acesso às chaves para garantir a segurança de seus recursos.
{: shortdesc}

Audite a configuração de chaves com regularidade:

- Examine quando as chaves foram criadas e determine se é hora de girar a chave.
- [Monitorar chamadas API para {{site.data.keyword.keymanagementserviceshort}} com {{site.data.keyword.cloudaccesstrailshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/cloud-activity-tracker/tutorials?topic=cloud-activity-tracker-kp){: new_window}.
- Inspecione quais usuários têm acesso a chaves e se o nível de acesso é apropriado.

Para obter mais informações sobre o acesso de auditoria a seus recursos, consulte [Gerenciando acesso de usuário com o Cloud IAM](/docs/services/key-protect?topic=key-protect-manage-access).

## Visualizando chaves com a GUI
{: #view-keys-gui}

Se você preferir inspecionar as chaves em seu serviço usando uma interface gráfica, será possível usar o painel {{site.data.keyword.keymanagementserviceshort}}.

[Depois de criar ou importar suas chaves existentes para o serviço](/docs/services/key-protect?topic=key-protect-create-root-keys), conclua as etapas a seguir para visualizar suas chaves.

1. [Efetue login no console do {{site.data.keyword.cloud_notm}}
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/).
2. Acesse **Menu** &gt; **Lista de recursos** para visualizar uma lista de seus recursos.
3. Em sua lista de recursos do {{site.data.keyword.cloud_notm}}, selecione a sua instância provisionada do {{site.data.keyword.keymanagementserviceshort}}.
4. Procure as características gerais de suas chaves por meio da página de detalhes do aplicativo:

    <table>
      <tr>
        <th>Coluna</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>O alias único, legível para o ser humano que foi designado à sua chave.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>Um ID de chave exclusiva que foi designado à sua chave pelo serviço do {{site.data.keyword.keymanagementserviceshort}}. É possível usar o valor de ID para fazer chamadas para o serviço com a API do [{{site.data.keyword.keymanagementserviceshort}}![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/key-protect).</td>
      </tr>
      <tr>
        <td>Estado</td>
        <td>O [estado de chave](/docs/services/key-protect?topic=key-protect-key-states) baseado em [NIST Special Publication 800-57, Recomendação para gerenciamento de chave ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0). Esses estados incluem <i>Pré-ativo</i>, <i>Ativo</i>, <i>Desativado</i> e <i>Destruído</i>.</td>
      </tr>
      <tr>
        <td>Tipo</td>
        <td>O [Tipo de chave](/docs/services/key-protect?topic=key-protect-envelope-encryption#key-types) que descreve o propósito designado de sua chave dentro do serviço.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve o <b>Chaves</b> tabela</caption>
    </table>

## Visualizando chaves com a API
{: #view-keys-api}

É possível recuperar os conteúdos de suas chaves usando a API do {{site.data.keyword.keymanagementserviceshort}}.

### Recuperando uma lista de suas chaves
{: #retrieve-keys-api}

Para uma visualização de alto nível, é possível procurar chaves que são gerenciadas em sua instância provisionada do {{site.data.keyword.keymanagementserviceshort}} fazendo uma chamada `GET` para o terminal a seguir.

```
https://<region>.kms.cloud.ibm.com/api/v2/keys
```
{: codeblock}

1. [Recupere suas credenciais de serviço e autenticação para trabalhar com chaves no serviço](/docs/services/key-protect?topic=key-protect-set-up-api).

2. Execute o comando cURL a seguir para visualizar características gerais sobre suas chaves.

    ```cURL
    curl -X GET \
    https://<region>.kms.cloud.ibm.com/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
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
        <td><varname>IAM_token</varname></td>
        <td><strong>Necessário.</strong> Seu token de acesso do {{site.data.keyword.cloud_notm}}. Inclua o conteúdo integral do token <code>IAM</code>, incluindo valor Bearer, na solicitação cURL. Para obter mais informações, veja <a href="/docs/services/key-protect?topic=key-protect-retrieve-access-token">Recuperando um token de acesso</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>Necessário.</strong> O identificador exclusivo que é designado para sua instância de serviço {{site.data.keyword.keymanagementserviceshort}}. Para obter mais informações, veja <a href="/docs/services/key-protect?topic=key-protect-retrieve-instance-ID">Recuperando um ID da instância</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>O identificador exclusivo que é usado para rastrear e correlacionar transações.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 2. Descreve as variáveis que são necessárias para visualizar chaves com a API do {{site.data.keyword.keymanagementserviceshort}}</caption>
    </table>

    Uma solicitação `GET api/v2/keys` bem-sucedida retorna uma coleção de chaves que estão disponíveis em sua instância de serviço do {{site.data.keyword.keymanagementserviceshort}}.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "...", "type": "application/vnd.ibm.kms.key+json", "name": "Standard key", "description": "...", "state": 1, "crn": "...", "algorithmType": "AES", "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256", "mode": "GCM"
          },
          "extractable": true,
          "imported": false
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...", "state": 1, "crn": "...", "algorithmType": "AES", "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastRotateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256", "mode": "GCM"
          },
          "extractable": false,
          "imported": true
        }
      ]
    }
    ```
    {:screen}

    Por padrão, `GET api/v2/keys` retorna as suas primeiras 2000 chaves, mas é possível ajustar esse limite usando o parâmetro `limit` no tempo de consulta. Para saber mais sobre o `limit` e o `offset`, veja [Recuperando um subconjunto de chaves](#retrieve-subset-keys-api).
    {: tip}

### Recuperando um subconjunto de chaves
{: #retrieve-subset-keys-api}

Especificando os parâmetros `limit` e `offset` no tempo de consulta, é possível recuperar um subconjunto de suas chaves, começando com o valor `offset` que você especifica. 

Por exemplo, você pode ter um total de 3000 chaves que são armazenadas em sua instância de serviço do {{site.data.keyword.keymanagementserviceshort}}, mas você deseja recuperar de 200 a 300 chaves quando faz uma solicitação `GET /keys`. 

É possível usar a solicitação de exemplo a seguir para recuperar um conjunto diferente de chaves.

  ```cURL
  curl -X GET \
  https://<region>.kms.cloud.ibm.com/api/v2/keys?offset=<offset>&limit=<limit> \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  ```
  {: codeblock}

  Substitua as variáveis `limit` e `offset` em sua solicitação de acordo com a tabela a seguir.
  <table>
    <tr>
      <th>Variável</th>
      <th>Descrição</th>
    </tr>
    <tr>
      <td><p><varname>offset</varname></p></td>
      <td>
        <p>O número de chaves a serem ignoradas.</p> 
        <p>Por exemplo, se você tiver 50 chaves em sua instância e desejar listar 26 a 50 chaves, use
            <code>../keys?offset=25</code>. Também é possível fazer par de <code>offset</code> com <code>limit</code> para percorrer os seus recursos disponíveis.</p>
      </td>
    </tr>
    <tr>
      <td><p><varname>limit</varname></p></td>
      <td>
        <p>O número de chaves a serem recuperadas.</p> 
        <p>Por exemplo, se você tiver 100 chaves em sua instância e desejar listar apenas 10 chaves, use
            <code>../keys?limit=10</code>. O valor máximo para <code>limit</code> é 5000.</p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">Tabela 2. Descreve as variáveis <code>limit</code> e <code>offset</code></caption>
  </table>

Para obter notas de uso, verifique os exemplos a seguir para configurar os seus parâmetros de consulta `limit` e `offset`.

<table>
  <tr>
    <th>URL</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td><code>.../keys</code></td>
    <td>Lista todos os recursos disponíveis, até as primeiras 2000 chaves.</td>
  </tr>
  <tr>
    <td><code>.../keys?limit=10</code></td>
    <td>Lista os primeiros 10 chaves.</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=25 & limit=50</code></td>
    <td>Lista chaves 26-50.</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=30 00 & limit=50</code></td>
    <td>Lista chaves 3001-3050.</td>
  </tr>
  <caption style="caption-side:bottom;">Tabela 3. Fornece notas de uso para os parâmetros de consulta limit e offset</caption>
</table>

Deslocamento é o local de uma determinada chave em um conjunto de dados. O valor `offset` é baseado em zero, o que significa que a décima chave de criptografia em um conjunto de dados está no deslocamento 9.
{: tip}

### Recuperando uma chave por ID
{: #retrieve-key-api}

Para visualizar informações detalhadas sobre uma chave específica, é possível fazer uma chamada `GET` para o terminal a seguir.

```
https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Recupere suas credenciais de serviço e autenticação para trabalhar com chaves no serviço](/docs/services/key-protect?topic=key-protect-set-up-api).

2. Recupere o ID da chave que você gostaria de acessar ou gerenciar.

    O valor do ID é usado para acessar informações detalhadas sobre a chave, como o próprio material da chave. É possível recuperar o ID para uma chave especificada fazendo uma solicitação `GET /v2/keys` ou acessando a GUI do {{site.data.keyword.keymanagementserviceshort}}.

3. Execute o comando cURL a seguir para obter detalhes sobre a chave e o material da chave.

    ```cURL
    curl -X GET \
      https://<region>.kms.cloud.ibm.com/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Substitua as variáveis na solicitação de exemplo de acordo com a tabela a seguir.

    <table>
      <tr>
        <th>Variável</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td><strong>Necessário.</strong> A abreviação da região, como <code>us-south</code> ou <code>eu-gb</code>, que representa a área geográfica na qual reside sua instância de serviço do {{site.data.keyword.keymanagementserviceshort}}. Veja <a href="/docs/services/key-protect?topic=key-protect-regions#endpoints">Terminais em serviço regionais</a> para obter mais informações.</td>
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
        <td><varname>correlation_ID</varname></td>
        <td>O identificador exclusivo que é usado para rastrear e correlacionar transações.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>Necessário.</strong> O identificador para a chave que você recuperou na [etapa 1](#retrieve-keys-api).</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 4. Descreve as variáveis que são necessárias para visualizar uma chave especificada com a API do {{site.data.keyword.keymanagementserviceshort}}</caption>
    </table>

    Uma `GET api/v2/keys/<key_ID>` bem-sucedida retorna detalhes sobre a sua chave e o material da chave. O objeto JSON a seguir mostra um valor retornado de exemplo para uma chave padrão.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
            "id": "...", "type": "application/vnd.ibm.kms.key+json", "name": "Standard key", "description": "...", "state": 1, "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256", "mode": "GCM"
            },
            "extractable": true,
            "imported": false
        }
      ]
    }
    ```
    {:screen}

    Para obter uma descrição detalhada dos parâmetros disponíveis, veja o {{site.data.keyword.keymanagementserviceshort}} [documento de referência da API de REST ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/key-protect){: new_window}.
