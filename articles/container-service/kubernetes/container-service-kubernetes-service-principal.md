---
title: "entità aaaService per cluster di Azure Kubernetes | Documenti Microsoft"
description: "Creare e gestire un'entità servizio di Azure Active Directory per un cluster Kubernetes nel servizio contenitore di Azure"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Configurare un'entità servizio di Azure AD per un cluster Kubernetes nel servizio contenitore


Nel servizio contenitore di Azure, è necessario un cluster Kubernetes un [dell'entità servizio di Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract con le API di Azure. Hello dell'entità servizio è necessario toodynamically gestire le risorse, ad esempio [le route definite dall'utente](../../virtual-network/virtual-networks-udr-overview.md) hello e [servizio di bilanciamento del carico di Azure di livello 4](../../load-balancer/load-balancer-overview.md). 


Questo articolo illustra tooset diverse opzioni di un servizio principale per il cluster Kubernetes. Ad esempio, se è installato e configurato hello [CLI di Azure 2.0](/cli/azure/install-az-cli2), è possibile eseguire hello [ `az acs create` ](/cli/azure/acs#create) comando toocreate hello Kubernetes cluster e hello entità servizio in hello contemporaneamente.


## <a name="requirements-for-hello-service-principal"></a>Requisiti per l'entità servizio hello

È possibile utilizzare un'entità servizio di Azure AD esistente, che soddisfa hello seguenti requisiti o crearne uno nuovo.

* **Ambito**: gruppo di risorse hello nella sottoscrizione hello utilizzato cluster Kubernetes di hello toodeploy, o (meno correggono) sottoscrizione hello cluster hello toodeploy.

* **Ruolo**: **Collaboratore**.

* **Segreto client**: deve essere una password. Non è attualmente possibile usare un'entità servizio configurata per l'autenticazione del certificato.

> [!IMPORTANT] 
> toocreate un'entità servizio, è necessario disporre delle autorizzazioni tooregister un'applicazione con il tenant di Azure AD e ruolo di tooa applicazione hello tooassign nella sottoscrizione. toosee se si dispone delle autorizzazioni necessarie hello, [archivia hello portale](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions). 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>Opzione 1: creare un'entità servizio in Azure AD

Se si desidera toocreate un'entità servizio di Azure AD prima di distribuire il cluster Kubernetes, Azure fornisce diversi metodi. 

Hello comandi di esempio seguenti illustrano come toodo con hello [CLI di Azure 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md). In alternativa creare un servizio principale utilizzando [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), o altri metodi.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

L'output è simile seguente toohello (illustrato di seguito redatta):

![Creare un’entità servizio](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

Sono hello **ID client** (`appId`) e hello **segreto client** (`password`) utilizzati come parametri dell'entità servizio per la distribuzione di cluster.


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>Specificare l'entità servizio durante la creazione di cluster Kubernetes hello

Fornire hello **ID client** (detto anche hello `appId`, per l'ID applicazione) e **segreto client** (`password`) di un'entità come parametri quando si crea hello servizio esistente Kubernetes cluster. Assicurarsi che un'entità servizio hello soddisfi i requisiti di hello in hello a partire da questo articolo.

È possibile specificare questi parametri quando si distribuiscono cluster Kubernetes hello utilizzando hello [Azure interfaccia della riga di comando (CLI) 2.0](container-service-kubernetes-walkthrough.md), [portale di Azure](../dcos-swarm/container-service-deployment.md), o altri metodi.

>[!TIP] 
>Quando si specifica hello **ID client**, hello toouse assicurarsi di essere `appId`, non hello `ObjectId`, dell'entità servizio hello.
>

Hello esempio seguente viene illustrato un modo toopass parametri hello con hello CLI di Azure 2.0. Questo esempio viene utilizzato hello [Kubernetes delle Guide rapide modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).

1. [Scaricare](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) file dei parametri di modello hello `azuredeploy.parameters.json` da GitHub.

2. servizio hello toospecify principale, immettere i valori per `servicePrincipalClientId` e `servicePrincipalClientSecret` nel file hello. (È anche necessario tooprovide i propri valori per `dnsNamePrefix` e `sshRSAPublicKey`. Hello quest'ultimo è cluster hello tooaccess chiave pubblica SSH di hello). Salvare il file hello.

    ![Passare i parametri dell'entità servizio](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. Hello esecuzione comando seguente, usando `--parameters` tooset hello percorso toohello azuredeploy.parameters.json file. Questo comando consente di distribuire cluster hello in un gruppo di risorse creato chiamato `myResourceGroup` nell'area Stati Uniti occidentali hello.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>Opzione 2: Generare un'entità servizio durante la creazione di cluster hello con`az acs create`

Se si esegue hello [ `az acs create` ](/cli/azure/acs#create) toocreate comando hello Kubernetes cluster, è necessario hello opzione toogenerate un'entità servizio automaticamente.

Analogamente alle altre opzioni di creazione del cluster Kubernetes, è possibile specificare i parametri per un'entità servizio esistente quando si esegue `az acs create`. Tuttavia, quando si omettono i parametri, hello CLI di Azure viene creata una automaticamente per l'utilizzo con il servizio di contenitore. Questo avviene in modo trasparente durante la distribuzione di hello. 

Hello seguente comando crea un cluster Kubernetes e genera le chiavi SSH e le credenziali dell'entità servizio:

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Se l'account non dispone di hello Azure AD e sottoscrizione autorizzazioni toocreate un'entità servizio, il comando hello genera un errore simile troppo`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>Considerazioni aggiuntive

* Se non si dispone delle autorizzazioni toocreate un'entità servizio nella sottoscrizione, potrebbe essere necessario tooask Azure AD o sottoscrizione amministratore tooassign hello delle autorizzazioni necessarie o chiedere un toouse dell'entità servizio con il servizio contenitore di Azure. 

* entità servizio Hello per Kubernetes è una parte hello della configurazione del cluster. Tuttavia, non utilizzare cluster di hello identità toodeploy hello.

* Ogni entità servizio è associata a un'applicazione Azure AD. Hello dell'entità servizio per un cluster Kubernetes può essere associata a qualsiasi valido di Azure nome applicazione Active Directory (ad esempio: `https://www.contoso.org/example`). Hello URL per un'applicazione hello privo di toobe un endpoint di tipo real.

* Quando si specifica un'entità servizio hello **ID Client**, è possibile utilizzare il valore di hello di hello `appId` (come illustrato in questo articolo) o entità servizio corrispondente hello `name` (ad esempio,`https://www.contoso.org/example`).

* Nel master hello e agente di macchine virtuali in cluster Kubernetes hello, vengono archiviate le credenziali dell'entità servizio di hello in /etc/kubernetes/azure.json file hello.

* Quando si utilizza hello `az acs create` comando dell'entità servizio di hello toogenerate automaticamente, le credenziali dell'entità servizio di hello vengono scritti toohello file ~/.azure/acsServicePrincipal.json computer hello utilizzato comando hello toorun. 

* Quando si utilizza hello `az acs create` comando dell'entità servizio di hello toogenerate automaticamente, entità servizio hello possono anche eseguire l'autenticazione con un [Registro di sistema di contenitore di Azure](../../container-registry/container-registry-intro.md) creato in hello stessa sottoscrizione.




## <a name="next-steps"></a>Passaggi successivi

* [Introduzione a Kubernetes](container-service-kubernetes-walkthrough.md) nel cluster del servizio contenitore.

* tootroubleshoot hello entità servizio per Kubernetes, vedere hello [documentazione del motore di ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).


