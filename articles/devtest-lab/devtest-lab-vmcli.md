---
title: aaaCreate e gestire macchine virtuali in DevTest Labs con CLI di Azure | Documenti Microsoft
description: Informazioni su come toouse Azure DevTest Labs toocreate e gestire macchine virtuali con 2.0 CLI di Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a>Creare e gestire macchine virtuali con DevTest Labs utilizzando hello CLI di Azure
Questa guida introduttiva illustra la creazione, l'avvio, la connessione, l'aggiornamento e la pulizia di una macchina di sviluppo nel lab. 

Prima di iniziare:

* Se il lab non è stato creato, le istruzioni sono disponibili [qui](devtest-lab-create-lab.md).

* [Installare l'interfaccia della riga di comando 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). toostart, esecuzione az accesso toocreate una connessione con Azure. 

## <a name="create-and-verify-hello-virtual-machine"></a>Creare e verificare una macchina virtuale hello 
Creare una macchina virtuale da un'immagine del Marketplace con autenticazione SSH.
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> Inserire hello **gruppo di risorse del lab** nome hello - parametro gruppo di risorse.
>

Se si desidera toocreate una macchina virtuale utilizzando una formula, utilizzare hello - parametro formula in [creare vm lab az](https://docs.microsoft.com/cli/azure/lab/vm#create).


Verificare che hello macchina virtuale è disponibile.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-toohello-virtual-machine"></a>Avviare e connettere la macchina virtuale di toohello
Avviare una VM.
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> Inserire hello **gruppo di risorse del lab** nome hello - parametro gruppo di risorse.
>

Connettersi tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) o [Desktop remoto](../virtual-machines/windows/connect-logon.md).
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a>Aggiornare la macchina virtuale hello
Applicare gli elementi tooa macchina virtuale.
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

Elencare gli elementi disponibili nell'ambiente lab hello.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a>Arrestare ed eliminare la macchina virtuale di hello    
Arrestare una VM.
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

Eliminare una VM.
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]