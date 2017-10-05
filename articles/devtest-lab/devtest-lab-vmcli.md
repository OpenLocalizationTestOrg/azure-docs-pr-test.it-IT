---
title: Creare e gestire macchine virtuali in DevTest Labs con l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Informazioni su come usare Azure DevTest Labs per creare e gestire le macchine virtuali con l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: 42b0448c1bcdfa909715abd5075353d63cab8389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-the-azure-cli"></a><span data-ttu-id="03849-103">Creare e gestire macchine virtuali con DevTest Labs tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="03849-103">Create and manage virtual machines with DevTest Labs using the Azure CLI</span></span>
<span data-ttu-id="03849-104">Questa guida introduttiva illustra la creazione, l'avvio, la connessione, l'aggiornamento e la pulizia di una macchina di sviluppo nel lab.</span><span class="sxs-lookup"><span data-stu-id="03849-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="03849-105">Prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="03849-105">Before you begin:</span></span>

* <span data-ttu-id="03849-106">Se il lab non è stato creato, le istruzioni sono disponibili [qui](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="03849-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="03849-107">[Installare l'interfaccia della riga di comando 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="03849-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="03849-108">Per iniziare, eseguire az login per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="03849-108">To start, run az login to create a connection with Azure.</span></span> 

## <a name="create-and-verify-the-virtual-machine"></a><span data-ttu-id="03849-109">Creare e verificare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="03849-109">Create and verify the virtual machine</span></span> 
<span data-ttu-id="03849-110">Creare una macchina virtuale da un'immagine del Marketplace con autenticazione SSH.</span><span class="sxs-lookup"><span data-stu-id="03849-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="03849-111">Inserire il nome del **gruppo di risorse lab** nel parametro --resource-group.</span><span class="sxs-lookup"><span data-stu-id="03849-111">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="03849-112">Se si vuole creare una macchina virtuale tramite una formula, usare il parametro --formula in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="03849-112">If you want to create a VM using a formula, use the --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="03849-113">Verificare che la VM sia disponibile.</span><span class="sxs-lookup"><span data-stu-id="03849-113">Verify that the VM is available.</span></span>
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

## <a name="start-and-connect-to-the-virtual-machine"></a><span data-ttu-id="03849-114">Avviare e connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="03849-114">Start and connect to the virtual machine</span></span>
<span data-ttu-id="03849-115">Avviare una VM.</span><span class="sxs-lookup"><span data-stu-id="03849-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="03849-116">Inserire il nome del **gruppo di risorse lab** nel parametro --resource-group.</span><span class="sxs-lookup"><span data-stu-id="03849-116">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="03849-117">Connettersi a una VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) o [Desktop remoto](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="03849-117">Connect to a VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-the-virtual-machine"></a><span data-ttu-id="03849-118">Aggiornare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="03849-118">Update the virtual machine</span></span>
<span data-ttu-id="03849-119">Applicare elementi a una VM.</span><span class="sxs-lookup"><span data-stu-id="03849-119">Apply artifacts to a VM.</span></span>
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

<span data-ttu-id="03849-120">Elencare gli elementi disponibili nel lab.</span><span class="sxs-lookup"><span data-stu-id="03849-120">List artifacts available in the lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-the-virtual-machine"></a><span data-ttu-id="03849-121">Arrestare ed eliminare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="03849-121">Stop and delete the virtual machine</span></span>    
<span data-ttu-id="03849-122">Arrestare una VM.</span><span class="sxs-lookup"><span data-stu-id="03849-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="03849-123">Eliminare una VM.</span><span class="sxs-lookup"><span data-stu-id="03849-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]