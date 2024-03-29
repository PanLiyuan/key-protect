---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: key management service, kms, manage encryption keys, data encryption, data-at-rest, protect data encryption keys

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

# Tutorial de introdução
{: #getting-started-tutorial}

O {{site.data.keyword.keymanagementservicefull}} ajuda a provisionar chaves criptografadas para apps em serviços {{site.data.keyword.cloud_notm}}. Este tutorial mostra como criar e incluir chaves criptográficas existentes usando o painel do
{{site.data.keyword.keymanagementserviceshort}}, assim, é possível gerenciar a criptografia de dados de um local
central.
{: shortdesc}

## Introdução às chaves de criptografia
{: #get-started-keys}

No painel do {{site.data.keyword.keymanagementserviceshort}}, é possível criar novas chaves para criptografia
ou importar as chaves existentes. 

Escolha entre dois tipos de chave:

<dl>
  <dt>Chaves raiz</dt>
    <dd>As chaves raiz são chaves simétricas de agrupamento de chaves completamente gerenciadas em {{site.data.keyword.keymanagementserviceshort}}. É possível usar uma chave raiz para proteger outras chaves criptográficas com criptografia avançada. Para saber mais, consulte <a href="/docs/services/key-protect?topic=key-protect-envelope-encryption">Protegendo dados com criptografia de envelope</a>.</dd>
  <dt>Chaves padrão</dt>
    <dd>Chaves padrão são chaves simétricas que são usadas para criptografia. É possível usar uma chave padrão para criptografar e decriptografar dados diretamente.</dd>
</dl>

## Criando novas chaves
{: #create-keys}

[Depois de criar uma
instância do {{site.data.keyword.keymanagementserviceshort}}](https://{DomainName}/catalog/services/key-protect?taxonomyNavigation=apps), você está pronto para designar chaves no serviço. 

Conclua as etapas a seguir para criar sua primeira chave criptográfica. 

1. Na página de detalhes do aplicativo, clique em **Gerenciar** &gt; **Incluir chave**.
2. Para criar uma nova chave, selecione a janela **Criar uma chave**.

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
        <td>O <a href="/docs/services/key-protect?topic=key-protect-envelope-encryption#key-types">tipo de chave</a> que você gostaria de gerenciar no {{site.data.keyword.keymanagementserviceshort}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descrição das configurações de <b>Criar uma chave</b></caption>
    </table>

3. Quando você tiver concluído o preenchimento dos detalhes da chave, clique em **Criar chave** para confirmar. 

Chaves que são criadas no serviço são chaves simétricas de 256 bits, suportadas pelo algoritmo AES-GCM. Para segurança adicional, as chaves são geradas por módulos de segurança de hardware (HSMs) certificados FIPS 140-2 Nível 2 que estão localizados em data centers seguros do {{site.data.keyword.cloud_notm}}. 

## Importando suas próprias chaves
{: #import-keys}

É possível ativar os benefícios de segurança de Bring Your Own Key (BYOK) apresentando as suas chaves existentes para o serviço. 

Conclua as etapas a seguir para incluir uma chave existente.

1. Na página de detalhes do aplicativo, clique em **Gerenciar** &gt; **Incluir chave**.
2. Para fazer upload de uma chave existente, selecione a janela **Importar sua própria chave**.

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
        <td>O <a href="/docs/services/key-protect?topic=key-protect-envelope-encryption#key-types">tipo de chave</a> que você gostaria de gerenciar no {{site.data.keyword.keymanagementserviceshort}}.</td>
      </tr>
      <tr>
        <td>Material de chave</td>
        <td>O material da chave, como uma chave simétrica, que você deseja armazenar no serviço {{site.data.keyword.keymanagementserviceshort}}. A chave fornecida deve ser codificada em Base64.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 2. Descrição das configurações de <b>Importar sua própria chave</b></caption>
    </table>

3. Quando você tiver concluído o preenchimento dos detalhes da chave, clique em **Importar chave** para confirmar. 

No painel {{site.data.keyword.keymanagementserviceshort}}, é possível inspecionar as características gerais de suas novas chaves. 

## O que vem a seguir
{: #get-started-next-steps}

Agora é possível usar suas chaves para codificar seus apps e serviços. Se você incluiu uma chave raiz no serviço, talvez deseje aprender mais sobre o uso da chave raiz para proteger as chaves que criptografam seus dados em repouso. Veja [Agrupando chaves](/docs/services/key-protect?topic=key-protect-wrap-keys) para começar.

- Para descobrir mais sobre como gerenciar e proteger suas chaves de criptografia com uma chave raiz, confira [Protegendo dados com criptografia de envelope](/docs/services/key-protect?topic=key-protect-envelope-encryption).
- Para saber mais sobre como integrar o serviço do {{site.data.keyword.keymanagementserviceshort}} com outras soluções de dados da nuvem, o [ consulte o doc Integrações](/docs/services/key-protect?topic=key-protect-integrate-services).
- Para descobrir mais sobre como gerenciar programaticamente as suas chaves, [consulte o doc de referência da API do {{site.data.keyword.keymanagementserviceshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/key-protect){: new_window}.
