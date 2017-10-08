---
title: Origine OpenShift tooAzure aaaDeploy | Documenti Microsoft
description: Informazioni su origine OpenShift toodeploy tooAzure le macchine virtuali.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>Distribuzione di origine OpenShift tooAzure macchine virtuali 

[ OpenShift Origin](https://www.openshift.org/) è una piattaforma contenitore open source basata su [Kubernetes](https://kubernetes.io/). Semplifica il processo di hello di distribuzione, scalabilità e gestione di applicazioni multi-tenant. 

Questa guida descrive come toodeploy OpenShift origine sull'uso di macchine virtuali di Azure hello Azure CLI e modelli di gestione risorse di Azure. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un toomanage KeyVault chiavi SSH per cluster OpenShift hello.
> * Distribuire un cluster OpenShift in macchine virtuali di Azure. 
> * Installare e configurare hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) cluster hello toomanage.
> * Personalizzare la distribuzione OpenShift hello.

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

Questa Guida introduttiva richiede hello Azure CLI versione 2.0.8 o versione successiva. versione di hello toofind, eseguire `az --version`. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>Accedi tooAzure 
Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello direzioni o fare clic su **provarla** toouse Shell Cloud.

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>Creare un insieme di credenziali delle chiavi
Creare un hello toostore KeyVault chiavi SSH per il cluster hello con hello [keyvault az creare](/cli/azure/keyvault#create) comando.  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>Creare una chiave SSH 
Una chiave SSH è necessario toosecure accesso toohello cluster OpenShift origine. Creare una coppia di chiavi SSH utilizzando hello `ssh-keygen` comando. 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> coppia di chiavi SSH crei Hello non deve avere una passphrase.

Per ulteriori informazioni sulle chiavi SSH in Windows, [come toocreate SSH chiavi in Windows](/azure/virtual-machines/linux/ssh-from-windows).

## <a name="store-ssh-private-key-in-key-vault"></a>Archiviare la chiave privata SSH nell'insieme di credenziali per le chiavi
Hello OpenShift distribuzione utilizza la chiave SSH hello creato accesso toosecure toohello OpenShift master. tooenable hello distribuzione toosecurely recuperare la chiave SSH hello, archivia la chiave di hello nell'insieme di credenziali chiave usando hello comando seguente.

# <a name="enabled-for-template-deployment"></a>Distribuzione abilitata per modello
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>Creare un'entità servizio 
OpenShift comunica con Azure usando un nome utente e una password o un'entità servizio. Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come OpenShift. È controllare e definire le autorizzazioni di hello come entità di servizio toowhat operazioni hello è possibile eseguire in Azure. sicurezza tooimprove su per fornire un nome utente e una password, questo esempio crea un servizio di base dell'entità.

Creare un servizio principale con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) e le credenziali di hello output OpenShift deve:

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
Prendere nota della proprietà appId hello restituito dal comando hello.
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > Non creare una password non sicura.  Attenersi alle istruzioni relative a [regole e limitazioni sulle password di Azure AD](/azure/active-directory/active-directory-passwords-policy).

Per altre informazioni sulle entità servizio, vedere [Creare un'entità servizio di Azure con l'interfaccia della riga di comando di Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="deploy-hello-openshift-origin-template"></a>Distribuire il modello di origine OpenShift hello
A questo punto distribuire OpenShift Origin usando un modello di Azure Resource Manager. 

> [!NOTE] 
> il comando seguente Hello richiede az CLI 2.0.8 o versione successiva. È possibile verificare hello az CLI versione con hello `az --version` comando. hello tooupdate versione CLI, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).

Hello utilizzare `appId` valore dall'entità servizio hello creato in precedenza per hello `aadClientId` parametro.

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
distribuzione di Hello potrebbe richiedere too20 minuti toocomplete. Hello URL della console OpenShift hello e il nome DNS di hello OpenShift master viene stampato toohello terminal al completamento distribuzione hello.

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Connettere il cluster di OpenShift toohello
Al termine della distribuzione di hello, connettersi toohello OpenShift console tramite browser hello utilizzando hello `OpenShift Console Uri`. In alternativa, è possibile connettersi toohello OpenShift master utilizzando hello comando seguente.

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>Pulire le risorse
Quando non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comando gruppo di risorse hello tooremove OpenShift cluster e tutte le relative risorse.

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

Questa esercitazione ha illustrato come:
> [!div class="checklist"]
> * Creare un toomanage KeyVault chiavi SSH per cluster OpenShift hello.
> * Distribuire un cluster OpenShift in macchine virtuali di Azure. 
> * Installare e configurare hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) cluster hello toomanage.

A questo punto il cluster OpenShift Origin è stato distribuito. È possibile seguire OpenShift esercitazioni toolearn come toodeploy la prima applicazione e usare hello OpenShift strumenti. Vedere [Guida introduttiva a origine OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget avviato. 
