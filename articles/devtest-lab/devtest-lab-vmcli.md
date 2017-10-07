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
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a><span data-ttu-id="2a43c-103">Creare e gestire macchine virtuali con DevTest Labs utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="2a43c-103">Create and manage virtual machines with DevTest Labs using hello Azure CLI</span></span>
<span data-ttu-id="2a43c-104">Questa guida introduttiva illustra la creazione, l'avvio, la connessione, l'aggiornamento e la pulizia di una macchina di sviluppo nel lab.</span><span class="sxs-lookup"><span data-stu-id="2a43c-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="2a43c-105">Prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="2a43c-105">Before you begin:</span></span>

* <span data-ttu-id="2a43c-106">Se il lab non è stato creato, le istruzioni sono disponibili [qui](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="2a43c-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="2a43c-107">[Installare l'interfaccia della riga di comando 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2a43c-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="2a43c-108">toostart, esecuzione az accesso toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="2a43c-108">toostart, run az login toocreate a connection with Azure.</span></span> 

## <a name="create-and-verify-hello-virtual-machine"></a><span data-ttu-id="2a43c-109">Creare e verificare una macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="2a43c-109">Create and verify hello virtual machine</span></span> 
<span data-ttu-id="2a43c-110">Creare una macchina virtuale da un'immagine del Marketplace con autenticazione SSH.</span><span class="sxs-lookup"><span data-stu-id="2a43c-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="2a43c-111">Inserire hello **gruppo di risorse del lab** nome hello - parametro gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2a43c-111">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="2a43c-112">Se si desidera toocreate una macchina virtuale utilizzando una formula, utilizzare hello - parametro formula in [creare vm lab az](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2a43c-112">If you want toocreate a VM using a formula, use hello --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="2a43c-113">Verificare che hello macchina virtuale è disponibile.</span><span class="sxs-lookup"><span data-stu-id="2a43c-113">Verify that hello VM is available.</span></span>
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

## <a name="start-and-connect-toohello-virtual-machine"></a><span data-ttu-id="2a43c-114">Avviare e connettere la macchina virtuale di toohello</span><span class="sxs-lookup"><span data-stu-id="2a43c-114">Start and connect toohello virtual machine</span></span>
<span data-ttu-id="2a43c-115">Avviare una VM.</span><span class="sxs-lookup"><span data-stu-id="2a43c-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="2a43c-116">Inserire hello **gruppo di risorse del lab** nome hello - parametro gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2a43c-116">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="2a43c-117">Connettersi tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) o [Desktop remoto](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="2a43c-117">Connect tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a><span data-ttu-id="2a43c-118">Aggiornare la macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="2a43c-118">Update hello virtual machine</span></span>
<span data-ttu-id="2a43c-119">Applicare gli elementi tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2a43c-119">Apply artifacts tooa VM.</span></span>
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

<span data-ttu-id="2a43c-120">Elencare gli elementi disponibili nell'ambiente lab hello.</span><span class="sxs-lookup"><span data-stu-id="2a43c-120">List artifacts available in hello lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a><span data-ttu-id="2a43c-121">Arrestare ed eliminare la macchina virtuale di hello</span><span class="sxs-lookup"><span data-stu-id="2a43c-121">Stop and delete hello virtual machine</span></span>    
<span data-ttu-id="2a43c-122">Arrestare una VM.</span><span class="sxs-lookup"><span data-stu-id="2a43c-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="2a43c-123">Eliminare una VM.</span><span class="sxs-lookup"><span data-stu-id="2a43c-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]