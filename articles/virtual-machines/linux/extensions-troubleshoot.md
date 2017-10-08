---
title: VM Linux aaaTroubleshooting errori estensione | Documenti Microsoft
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
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="7f617-103">Risoluzione degli errori delle estensioni della macchina virtuale Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="7f617-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="7f617-104">Visualizzazione dello stato dell'estensione</span><span class="sxs-lookup"><span data-stu-id="7f617-104">Viewing extension status</span></span>
<span data-ttu-id="7f617-105">Modelli di gestione risorse di Azure possono essere eseguiti da hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f617-105">Azure Resource Manager templates can be executed from hello  Azure CLI.</span></span> <span data-ttu-id="7f617-106">Quando viene eseguita modello hello, lo stato dell'estensione hello può essere visualizzato da Esplora inventario risorse di Azure o hello strumenti da riga di comando.</span><span class="sxs-lookup"><span data-stu-id="7f617-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="7f617-107">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="7f617-107">Here is an example:</span></span>

<span data-ttu-id="7f617-108">Interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="7f617-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="7f617-109">Ecco l'output di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="7f617-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="7f617-110">]</span><span class="sxs-lookup"><span data-stu-id="7f617-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="7f617-111">Risoluzione degli errori delle Estensioni:</span><span class="sxs-lookup"><span data-stu-id="7f617-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="7f617-112">Eseguire nuovamente l'estensione hello in hello VM</span><span class="sxs-lookup"><span data-stu-id="7f617-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="7f617-113">Se si eseguono gli script nella macchina virtuale utilizzando l'estensione dello Script personalizzata hello, in alcuni casi è possibile eseguire un errore in cui VM è stato creato ma script hello non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="7f617-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="7f617-114">In queste condizioni, hello consigliato modo toorecover da questo errore è tooremove hello estensione e nuovamente il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="7f617-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="7f617-115">Nota: In futuro, questa funzionalità sarebbe tooremove avanzata hello necessità di disinstallazione dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="7f617-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-cli"></a><span data-ttu-id="7f617-116">Rimuovi estensione hello dalla CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="7f617-116">Remove hello extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="7f617-117">Dove "nome-per Publisher" corrispondente tipo di estensione toohello dall'output di hello di "get-istanza-view macchina virtuale di azure" e hello nome della risorsa di estensione hello dal modello hello</span><span class="sxs-lookup"><span data-stu-id="7f617-117">Where "publsher-name" corresponds toohello extension type from hello output of "azure vm get-instance-view" and name is hello name of hello extension resource from hello template</span></span>

<span data-ttu-id="7f617-118">Una volta hello estensione è stata rimossa, il modello di hello può essere rieseguita toorun hello gli script hello VM.</span><span class="sxs-lookup"><span data-stu-id="7f617-118">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

