---
title: errori di estensione di macchina virtuale Windows aaaTroubleshooting | Documenti Microsoft
description: Informazioni sulla risoluzione degli errori delle estensioni della macchina virtuale Windows di Azure
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="84c2c-103">Risoluzione degli errori delle estensioni di macchina virtuale Windows di Azure</span><span class="sxs-lookup"><span data-stu-id="84c2c-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="84c2c-104">Visualizzazione dello stato dell'estensione</span><span class="sxs-lookup"><span data-stu-id="84c2c-104">Viewing extension status</span></span>
<span data-ttu-id="84c2c-105">I modelli di Azure Resource Manager possono essere eseguiti da Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84c2c-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="84c2c-106">Quando viene eseguita modello hello, lo stato dell'estensione hello può essere visualizzato da Esplora inventario risorse di Azure o hello strumenti da riga di comando.</span><span class="sxs-lookup"><span data-stu-id="84c2c-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="84c2c-107">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="84c2c-107">Here is an example:</span></span>

<span data-ttu-id="84c2c-108">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="84c2c-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="84c2c-109">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="84c2c-109">Here is hello sample output:</span></span>

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  <span data-ttu-id="84c2c-110">]</span><span class="sxs-lookup"><span data-stu-id="84c2c-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="84c2c-111">Risoluzione degli errori delle estensioni</span><span class="sxs-lookup"><span data-stu-id="84c2c-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="84c2c-112">Eseguire nuovamente l'estensione hello in hello VM</span><span class="sxs-lookup"><span data-stu-id="84c2c-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="84c2c-113">Se si eseguono gli script nella macchina virtuale utilizzando l'estensione dello Script personalizzata hello, in alcuni casi è possibile eseguire un errore in cui VM è stato creato ma script hello non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="84c2c-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="84c2c-114">In queste condizioni, hello consigliato modo toorecover da questo errore è tooremove hello estensione e nuovamente il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="84c2c-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="84c2c-115">Nota: In futuro, questa funzionalità sarebbe tooremove avanzata hello necessità di disinstallazione dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="84c2c-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="84c2c-116">Rimuovere l'estensione hello da Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="84c2c-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="84c2c-117">Una volta hello estensione è stata rimossa, il modello di hello può essere rieseguita toorun hello gli script hello VM.</span><span class="sxs-lookup"><span data-stu-id="84c2c-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

