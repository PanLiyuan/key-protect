---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-03"

keywords: service instance, create service instance, KMS service instance, Key Protect service instance

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

# Mise à disposition du service
{: #provision}

Vous pouvez créer une instance de {{site.data.keyword.keymanagementservicefull}} à l'aide de la console {{site.data.keyword.cloud_notm}} ou de l'interface de ligne de commande d'{{site.data.keyword.cloud_notm}}.
{: shortdesc}

## Mise à disposition à partir de la console {{site.data.keyword.cloud_notm}}
{: #provision-gui}

Pour mettre à disposition une instance de {{site.data.keyword.keymanagementserviceshort}} à partir de la console {{site.data.keyword.cloud_notm}}, procédez comme suit :

1. [Connectez-vous à votre compte {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}){: new_window}.
2. Cliquez sur **Catalogue** pour afficher la liste des services disponibles sur {{site.data.keyword.cloud_notm}}.
3. Dans le panneau de navigation Toutes les catégories, cliquez sur la catégorie **Sécurité et identité**.
4. Dans la liste de services, cliquez sur la vignette **{{site.data.keyword.keymanagementserviceshort}}**.
5. Sélectionnez un plan de service et cliquez sur **Créer** pour mettre à disposition une instance de {{site.data.keyword.keymanagementserviceshort}} dans le compte, la région et le groupe de ressources auxquels vous êtes connecté.

## Mise à disposition à partir de l'interface de ligne de commande d'{{site.data.keyword.cloud_notm}}
{: #provision-cli}

Vous pouvez également mettre à disposition une instance de {{site.data.keyword.keymanagementserviceshort}} à l'aide de l'interface de ligne de commande d'{{site.data.keyword.cloud_notm}}. 

1. Connectez-vous à {{site.data.keyword.cloud_notm}} via l'[interface de ligne de commande d'{{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-ibmcloud-cli){: new_window}.

    ```sh
    ibmcloud login 
    ```
    {: pre}
    **Remarque :** si la connexion échoue, exécutez la commande `ibmcloud login --sso` pour effectuer une nouvelle tentative. Le paramètre `--sso` est requis quand vous vous connectez avec un ID fédéré. Si cette option est utilisée, accédez au lien figurant dans la sortie de l'interface de ligne de commande pour générer un code d'accès à usage unique.

2. Sélectionnez le compte, la région et le groupe de ressources où vous souhaitez créer une instance de service {{site.data.keyword.keymanagementserviceshort}}.

    Vous pouvez également utiliser la commande ci-dessous pour définir votre région et votre groupe de ressources cible.

    ```sh
    ibmcloud target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

3. Mettez à disposition une instance de {{site.data.keyword.keymanagementserviceshort}} dans ce compte et ce groupe de ressources.

    ```sh
    ibmcloud resource service-instance-create <instance_name> kms tiered-pricing
    ```
    {: pre}

    Remplacez `<instance_name>` par un alias unique de votre instance de service.

4. Facultatif : Vérifiez que l'instance de service a été créée.

    ```sh
    ibmcloud resource service-instances
    ```
    {: pre}

## Etapes suivantes
{: #provision-service-next-steps}

Pour plus d'informations sur la gestion de vos clés à l'aide d'un programme, voir la [documentation de référence de l'API {{site.data.keyword.keymanagementserviceshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/key-protect){: new_window}.
