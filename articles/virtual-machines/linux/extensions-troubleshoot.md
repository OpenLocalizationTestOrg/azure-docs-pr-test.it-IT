---
title: Risoluzione degli errori delle estensioni della macchina virtuale Linux | Microsoft Docs
description: Informazioni sulla risoluzione degli errori delle estensioni della macchina virtuale di Azure
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 589890de379d0b729de1f1ba9e604e0ec0496f50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="a3a0b-103">Risoluzione degli errori delle estensioni della macchina virtuale Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="a3a0b-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="a3a0b-104">Visualizzazione dello stato dell'estensione</span><span class="sxs-lookup"><span data-stu-id="a3a0b-104">Viewing extension status</span></span>
<span data-ttu-id="a3a0b-105">I modelli di Azure Resource Manager possono essere eseguiti dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a0b-105">Azure Resource Manager templates can be executed from the  Azure CLI.</span></span> <span data-ttu-id="a3a0b-106">Una volta che il modello viene eseguito, è possibile visualizzare lo stato dell'estensione da Esplora risorse di Azure o dagli strumenti da riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a3a0b-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="a3a0b-107">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="a3a0b-107">Here is an example:</span></span>

<span data-ttu-id="a3a0b-108">Interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="a3a0b-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="a3a0b-109">Di seguito è riportato l'output di esempio:</span><span class="sxs-lookup"><span data-stu-id="a3a0b-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="a3a0b-110">]</span><span class="sxs-lookup"><span data-stu-id="a3a0b-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="a3a0b-111">Risoluzione degli errori delle Estensioni:</span><span class="sxs-lookup"><span data-stu-id="a3a0b-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="a3a0b-112">Eseguire nuovamente l'estensione nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a3a0b-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="a3a0b-113">Se si eseguono gli script nella macchina virtuale usando l'estensione script personalizzato, è possibile riscontrare in alcuni casi un errore in cui la creazione della macchina virtuale è riuscita, ma lo script ha avuto esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a3a0b-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="a3a0b-114">In queste condizioni, il metodo consigliato per risolvere il problema consiste nel rimuovere l'estensione e eseguire nuovamente il modello.</span><span class="sxs-lookup"><span data-stu-id="a3a0b-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="a3a0b-115">Nota: In futuro, questa funzionalità potrebbe essere migliorata in modo da eliminare la necessità di disinstallazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="a3a0b-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-cli"></a><span data-ttu-id="a3a0b-116">Rimuovere l'estensione dall'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a3a0b-116">Remove the extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="a3a0b-117">Dove "publsher-name" corrisponde al tipo di estensione dall'output di "azure vm get-instance-view" e nome è il nome della risorsa di estensione dal modello</span><span class="sxs-lookup"><span data-stu-id="a3a0b-117">Where "publsher-name" corresponds to the extension type from the output of "azure vm get-instance-view" and name is the name of the extension resource from the template</span></span>

<span data-ttu-id="a3a0b-118">Una volta rimossa l'estensione, il modello può essere eseguito nuovamente per eseguire gli script nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a3a0b-118">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

