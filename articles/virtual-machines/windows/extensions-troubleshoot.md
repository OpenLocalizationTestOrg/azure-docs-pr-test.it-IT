---
title: Risoluzione degli errori delle estensioni di macchina virtuale Windows | Microsoft Docs
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
ms.openlocfilehash: 4dba196e1b838f2092b30972fb070514bd2a4b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="50c42-103">Risoluzione degli errori delle estensioni di macchina virtuale Windows di Azure</span><span class="sxs-lookup"><span data-stu-id="50c42-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="50c42-104">Visualizzazione dello stato dell'estensione</span><span class="sxs-lookup"><span data-stu-id="50c42-104">Viewing extension status</span></span>
<span data-ttu-id="50c42-105">I modelli di Azure Resource Manager possono essere eseguiti da Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50c42-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="50c42-106">Una volta che il modello viene eseguito, è possibile visualizzare lo stato dell'estensione da Esplora risorse di Azure o dagli strumenti da riga di comando.</span><span class="sxs-lookup"><span data-stu-id="50c42-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="50c42-107">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="50c42-107">Here is an example:</span></span>

<span data-ttu-id="50c42-108">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="50c42-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="50c42-109">Di seguito è riportato l'output di esempio:</span><span class="sxs-lookup"><span data-stu-id="50c42-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="50c42-110">]</span><span class="sxs-lookup"><span data-stu-id="50c42-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="50c42-111">Risoluzione degli errori delle estensioni</span><span class="sxs-lookup"><span data-stu-id="50c42-111">Troubleshooting extension failures</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="50c42-112">Eseguire nuovamente l'estensione nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="50c42-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="50c42-113">Se si eseguono gli script nella macchina virtuale usando l'estensione script personalizzato, è possibile riscontrare in alcuni casi un errore in cui la creazione della macchina virtuale è riuscita, ma lo script ha avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="50c42-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="50c42-114">In queste condizioni, il metodo consigliato per risolvere il problema consiste nel rimuovere l'estensione e eseguire nuovamente il modello.</span><span class="sxs-lookup"><span data-stu-id="50c42-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="50c42-115">Nota: In futuro, questa funzionalità potrebbe essere migliorata in modo da eliminare la necessità di disinstallazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="50c42-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-powershell"></a><span data-ttu-id="50c42-116">Rimuovere l'estensione da Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="50c42-116">Remove the extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="50c42-117">Una volta rimossa l'estensione, il modello può essere eseguito nuovamente per eseguire gli script nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="50c42-117">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

