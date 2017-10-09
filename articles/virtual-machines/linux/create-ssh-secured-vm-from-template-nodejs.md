---
title: aaaCreate una VM Linux con un modello di Azure 1.0 CLI di Azure | Documenti Microsoft
description: Creare una VM Linux in Azure mediante Azure CLI 1.0 hello e un modello di gestione risorse di Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>Come toocreate una VM Linux utilizzando hello Azure CLI 1.0 un modello di gestione risorse di Azure
Questo articolo illustra come tooquickly distribuire una macchina virtuale di Linux mediante Azure CLI 1.0 hello e un modello di gestione risorse di Azure. articolo Hello richiede:

* Un account Azure. È possibile [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Hello [CLI di Azure 1.0](../../cli-install-nodejs.md) accesso `azure login`.
* Hello Azure CLI *deve essere* modalità Azure Resource Manager `azure config mode arm`.

È possibile distribuire rapidamente un modello Linux VM utilizzando hello [portale di Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#quick-command-summary) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

## <a name="quick-command-summary"></a>Breve riepilogo del comando
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata
I modelli consentono toocreate VM in Azure con le impostazioni che si desidera toocustomize durante l'avvio di hello, impostazioni, ad esempio nomi utente e i nomi host. Per questo articolo, verrà avviato un modello di Azure utilizzando una VM Ubuntu con un gruppo di sicurezza di rete (NSG) con la porta 22 aperta per SSH.

I modelli di Azure Resource Manager sono file JSON che possono essere usati per semplici attività occasionali, ad esempio l'avvio di una VM come in questo articolo.  Modelli di Azure possono essere anche usato tooconstruct configurazioni complesse di Azure degli ambienti intera come uno stack di distribuzione di test, sviluppo o di produzione.

## <a name="create-hello-linux-vm"></a>Creare hello VM Linux
Hello seguente esempio di codice viene illustrato come toocall `azure group create` toocreate una risorsa gruppo e distribuire una VM Linux protetto SSH in hello utilizzando [questo modello di gestione risorse di Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). Tenere presente che nell'esempio sono necessari nomi toouse che si trovano ambiente tooyour univoco. Questo esempio viene utilizzato *myResourceGroup* come nome del gruppo di risorse hello, e *myVM* come nome della macchina virtuale hello.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

output di Hello dovrebbe essere simile hello dopo il blocco di output:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Tale esempio distribuita una macchina virtuale tramite hello `--template-uri` parametro.  È anche possibile scaricare o creare un modello in locale e passare il modello di hello utilizzando hello `--template-file` parametro con un file di modello toohello percorso come argomento. Hello CLI di Azure richiede i parametri di hello richiesti dal modello hello.

## <a name="next-steps"></a>Passaggi successivi
Hello ricerca [raccolta di modelli](https://azure.microsoft.com/documentation/templates/) toodiscover quali toodeploy Framework applicazione successivo.

