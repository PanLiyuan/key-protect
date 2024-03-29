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

# Criando chaves raiz
{: #create-root-keys}

É possível usar o {{site.data.keyword.keymanagementservicefull}} para criar chaves raiz usando a GUI do {{site.data.keyword.keymanagementserviceshort}} ou programaticamente com a API do {{site.data.keyword.keymanagementserviceshort}}.
{: shortdesc}

Chaves raiz são chaves simétricas de quebra de chaves usadas para proteger a segurança dos dados criptografados na nuvem. Para obter mais informações sobre chaves raiz, consulte [Protegendo dados com criptografia de envelope](/docs/services/key-protect?topic=key-protect-envelope-encryption). 

## Criando chaves raiz com a GUI
{: #create-root-key-gui}

[Depois de criar uma instância do serviço](/docs/services/key-protect?topic=key-protect-provision), conclua as etapas a seguir para criar uma chave raiz com a GUI do {{site.data.keyword.keymanagementserviceshort}}.

1. [Efetue login no console do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}){: new_window}.
2. Acesse **Menu** &gt; **Lista de recursos** para visualizar uma lista de seus recursos.
3. Em sua lista de recursos do {{site.data.keyword.cloud_notm}}, selecione a sua instância provisionada do {{site.data.keyword.keymanagementserviceshort}}.
4. Para criar uma nova chave, clique em **Incluir chave** e selecione a janela **Criar uma chave**.

    Especifique os detalhes da chave:

    <table>
      <tr>
        <th>Configuração</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>
          <p>Um alias exclusivo, legível para fácil identificação de sua chave.</p>
          <p>Para proteger sua privacidade, assegure-se de que o nome da chave não contenha informações pessoalmente identificáveis (PII), como seu nome ou local.</p>
        </td>
      </tr>
      <tr>
        <td>Tipo de chave</td>
        <td>O <a href="/docs/services/key-protect?topic=key-protect-envelope-encryption#key-types">tipo de chave</a> que você gostaria de gerenciar no {{site.data.keyword.keymanagementserviceshort}}. Na lista de tipos de chave, selecione <b>Chave raiz</b>.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve as configurações <b>Criar uma chave</b></caption>
    </table>

5. Quando você tiver concluído o preenchimento dos detalhes da chave, clique em **Criar chave** para confirmar. 

Chaves que são criadas no serviço são chaves simétricas de 256 bits, suportadas pelo algoritmo AES-GCM. Para segurança adicional, as chaves são geradas por módulos de segurança de hardware (HSMs) certificados FIPS 140-2 Nível 2 que estão localizados em data centers seguros do {{site.data.keyword.cloud_notm}}. 

## Criando chaves raiz com a API
{: #create-root-key-api}

Crie uma chave raiz fazendo uma chamada `POST` para o terminal a seguir.

```
https://<region>.kms.cloud.ibm.com/api/v2/keys
```
{: codeblock}

1. [Recupere suas credenciais de serviço e autenticação para trabalhar com chaves no serviço](/docs/services/key-protect?topic=key-protect-set-up-api).

2. Chame a API do [{{site.data.keyword.keymanagementserviceshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/key-protect){: new_window} com o comando cURL a seguir.

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
       "type": "application/vnd.ibm.kms.key+json", "name": "<key_alias>", "description": "<key_description>", "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>", "extractable": <key_type> }
     ]
    }'
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
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p><strong>Necessário.</strong> Um nome exclusivo legível para fácil identificação da sua chave.</p>
          <p>Importante: para proteger sua privacidade, não armazene seus dados pessoais como metadados para sua chave.</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>Uma descrição estendida de sua chave.</p>
          <p>Importante: para proteger sua privacidade, não armazene seus dados pessoais como metadados para sua chave.</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>A data e hora em que a chave expira no sistema, em formato RFC 3339. Se o atributo <code>expirationDate</code> for omitido, a chave não expirará. </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>Um valor booleano determina se o material de chave pode sair do serviço.</p>
          <p>Ao configurar o atributo <code>extractable</code> para <code>false</code>, o serviço cria uma chave raiz que pode ser usada para operações de <code>wrap</code> ou <code>unwrap</code>.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabela 1. Descreve as variáveis que são necessárias para incluir uma chave raiz com a API do {{site.data.keyword.keymanagementserviceshort}}</caption>
    </table>

    Para proteger a confidencialidade de seus dados pessoais, evite inserir informações pessoalmente identificáveis (PII), como seu nome ou local, ao incluir chaves no serviço. Para obter mais exemplos de PII, consulte a seção 2.2 do [NIST Special Publication 800-122 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.nist.gov/publications/guide-protecting-confidentiality-personally-identifiable-information-pii){: new_window}.
    {: important}

    Uma resposta `POST api/v2/keys` bem-sucedida retorna o valor de ID para a sua chave, junto com outros metadados. O ID é um identificador exclusivo que é designado para sua chave e é usado para chamadas subsequentes para a API do {{site.data.keyword.keymanagementserviceshort}}.

3. Opcional: verifique se a chave foi criada executando a chamada a seguir para procurar as chaves na instância de serviço do {{site.data.keyword.keymanagementserviceshort}}.

    ```cURL
    curl -X GET \
      https://<region>.kms.cloud.ibm.com/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>'
    ```
    {: codeblock}

    Após criar uma chave raiz com o serviço, a chave permanece dentro dos limites do {{site.data.keyword.keymanagementserviceshort}} e seu material de chave não pode ser recuperado.
    {: note} 

## O que vem a seguir
{: #create-root-key-next-steps}

- Para descobrir mais sobre como proteger chaves com criptografia de envelope, consulte [Chaves de quebra](/docs/services/key-protect?topic=key-protect-wrap-keys).
- Para descobrir mais sobre como gerenciar programaticamente as suas chaves, [consulte o doc de referência da API do {{site.data.keyword.keymanagementserviceshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/key-protect){: new_window}.
