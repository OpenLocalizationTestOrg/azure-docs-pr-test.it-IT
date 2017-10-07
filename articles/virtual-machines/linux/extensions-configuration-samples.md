---
title: configurazione aaaSample per le estensioni VM Linux | Documenti Microsoft
description: Configurazione di esempio per la creazione di modelli con le estensioni per le macchine virtuali di Linux.
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f50e6b2-fce0-41ef-823d-df433957601a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/13/2016
ms.author: kundanap
ms.openlocfilehash: bc19b8d7d6fdb1783be99ec7fdd5cde5e1f8ca80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="linux-vm-extension-configuration-samples"></a><span data-ttu-id="e3fec-103">Esempi di configurazione dell’estensione delle macchine virtuali di Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fec-103">Linux VM extension configuration samples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3fec-104">PowerShell - Modello</span><span class="sxs-lookup"><span data-stu-id="e3fec-104">PowerShell - Template</span></span>](../windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [<span data-ttu-id="e3fec-105">Interfaccia della riga di comando - Modello</span><span class="sxs-lookup"><span data-stu-id="e3fec-105">CLI - Template</span></span>](../windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="e3fec-106">Questo articolo fornisce una configurazione di esempio per la configurazione di estensioni di macchina virtuale di Azure per macchine virtuali di Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fec-106">This article provides sample configuration for configuring Azure VM extensions for Linux VMs.</span></span>

<span data-ttu-id="e3fec-107">ulteriori informazioni su queste estensioni fare clic qui toolearn: [Cenni preliminari sulle estensioni VM di Azure.](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e3fec-107">toolearn more about these extensions click here : [Azure VM Extensions Overview.](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="e3fec-108">informazioni sulla creazione di modelli di estensione fare clic qui toolearn: [la creazione di modelli di estensione.](../windows/extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e3fec-108">toolearn more about authoring extension templates click here : [Authoring Extension Templates.](../windows/extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="e3fec-109">Questo articolo vengono elencati i valori di configurazione previsto per alcune delle estensioni di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e3fec-109">This article lists expected configuration values for some of hello Linux Extensions.</span></span>

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="e3fec-110">Frammento di modello di esempio per le estensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3fec-110">Sample template snippet for VM Extensions.</span></span>
<span data-ttu-id="e3fec-111">Hello modello frammento di codice per la distribuzione ha un aspetto estensioni come riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e3fec-111">hello template snippet for Deploying extensions looks as following:</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "autoUpgradeMinorVersion":true,
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a><span data-ttu-id="e3fec-112">Frammento di modello di esempio per le estensioni VM con set di scalabilità di VM.</span><span class="sxs-lookup"><span data-stu-id="e3fec-112">Sample template snippet for VM Extensions with VM Scale Sets.</span></span>
          {
           "type":"Microsoft.Compute/virtualMachineScaleSets",
          ....
                 "extensionProfile":{
                 "extensions":[
                   {
                     "name":"extension Name",
                     "properties":{
                       "publisher":"Publisher Namespace",
                       "type":"extension Name",
                       "typeHandlerVersion":"extension version",
                       "autoUpgradeMinorVersion":true,
                       "settings":{
                       // Extension specific configuration goes in here.
                       }
                     }
                    }
                  }
                }

<span data-ttu-id="e3fec-113">Prima di distribuire l'estensione hello verificare versione più recente dell'estensione hello e sostituire typeHandlerVersion"hello" con la versione più recente di hello corrente.</span><span class="sxs-lookup"><span data-stu-id="e3fec-113">Before deploying hello extension please check hello latest extension version and replace hello "typeHandlerVersion" with hello current latest version.</span></span>

<span data-ttu-id="e3fec-114">Articolo hello fornisce configurazioni di esempio per le estensioni VM Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fec-114">Rest of hello article provides sample configurations for Linux VM Extensions.</span></span>

### <a name="cloudlink-securevm-agent"></a><span data-ttu-id="e3fec-115">Agente di macchine virtuali CloudLink Secure</span><span class="sxs-lookup"><span data-stu-id="e3fec-115">CloudLink SecureVM Agent</span></span>
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMLinuxAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN tooCloudLinkCenter"
            }
          }

### <a name="customscript-extension-for-linux"></a><span data-ttu-id="e3fec-116">Estensione CustomScript per Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fec-116">CustomScript Extension for Linux.</span></span>
    {
        "publisher": " Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
            ],
            "commandToExecute": "powershell.exe-ExecutionPolicyUnrestricted-Filestart.ps1"
        }
    }


### <a name="datadog-agent"></a><span data-ttu-id="e3fec-117">Agente Datadog</span><span class="sxs-lookup"><span data-stu-id="e3fec-117">Datadog Agent</span></span>
        {
          "publisher": "Datadog.Agent",
          "type": "DatadogLinuxAgent",
          "typeHandlerVersion": "0.4",
          "settings": {
            "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
          }
        }

### <a name="chef-agent"></a><span data-ttu-id="e3fec-118">Agente Chef</span><span class="sxs-lookup"><span data-stu-id="e3fec-118">Chef Agent</span></span>
        {
          "publisher": "Chef.Bootstrap.WindowsAzure",
          "type": "CentosChefClient|LinuxChefClient",
          "typeHandlerVersion": "1210.12",
          "settings": {
            "validation_key" : " Validation key",
            "client_rb" : "client_rb file",
            "runlist" : "Optional runlist"
          }
        }

### <a name="vm-access-extension-password-reset"></a><span data-ttu-id="e3fec-119">Estensione accesso alle macchine virtuali (Reimpostazione della Password)</span><span class="sxs-lookup"><span data-stu-id="e3fec-119">VM Access Extension (Password Reset)</span></span>
<span data-ttu-id="e3fec-120">Per schema aggiornato vedere toohello [VMAccessForLinux documentazione](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)</span><span class="sxs-lookup"><span data-stu-id="e3fec-120">For updated schema refer toohello [VMAccessForLinux Documentation](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)</span></span>

        {
          "publisher": "Microsoft.OSTCExtensions",
          "type": "VMAccessForLinux",
          "typeHandlerVersion": "1.2",
          "protectedSettings": {
            "username": "(required, string) hello name of hello user",
            "password": "(optional, string) hello password of hello user",
            "reset_ssh": "(optional, boolean) whether or not reset hello ssh",
            "ssh_key": "(optional, string) hello public key of hello user, base64 encoded pem",
            "remove_user": "(optional, string) hello user name tooremove"
          }
        }

### <a name="os-patching"></a><span data-ttu-id="e3fec-121">Applicazione di patch del SO</span><span class="sxs-lookup"><span data-stu-id="e3fec-121">OS Patching</span></span>
<span data-ttu-id="e3fec-122">Per schema aggiornato vedere toohello [OSPatching documentazione](https://github.com/Azure/azure-linux-extensions/tree/master/OSPatching)</span><span class="sxs-lookup"><span data-stu-id="e3fec-122">For updated schema refer toohello [OSPatching Documentation](https://github.com/Azure/azure-linux-extensions/tree/master/OSPatching)</span></span>

        {
        "publisher": "Microsoft.OSTCExtensions",
        "type": "OSPatchingForLinux",
        "typeHandlerVersion": "2.9",
        "Settings": {
          "disabled": false,
          "stop": false,
          "rebootAfterPatch": "RebootIfNeed|Required|NotRequired|Auto",
          "category": "Important|ImportantAndRecommended",
          "installDuration": "<hr:min>",
          "oneoff": false,
          "intervalOfWeeks": "<number>",
          "dayOfWeek": "Sunday|Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Everyday",
          "startTime": "<hr:min>",
          "vmStatusTest": {
              "local": false,
              "idleTestScript": "<path_to_idletestscript>",
              "healthyTestScript": "<path_to_healthytestscript>"
          }
        }
        }

### <a name="docker-extension"></a><span data-ttu-id="e3fec-123">Estensione Docker</span><span class="sxs-lookup"><span data-stu-id="e3fec-123">Docker Extension</span></span>
<span data-ttu-id="e3fec-124">Per schema aggiornato vedere toohello [documentazione estensione Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md#1-configuration-schema)</span><span class="sxs-lookup"><span data-stu-id="e3fec-124">For updated schema refer toohello [Docker Extension Documentation](https://github.com/Azure/azure-docker-extension/blob/master/README.md#1-configuration-schema)</span></span>

        {
          "publisher": "Microsoft.Azure.Extensions ",
          "type": "DockerExtension ",
          "typeHandlerVersion": "1.0",
          "Settings": {
            "docker":{
                "port": "2376",
                "options": ["-D", "--dns=8.8.8.8"]
            },
            "compose": {
                "cache" : {
                    "image" : "memcached",
                    "ports" : ["11211:11211"]
                },
                "blog": {
                    "image": "ghost",
                    "ports": ["80:2368"]
                }
            }
            }
        }

        ### Linux Diagnostics Extension
        {
        "storageAccountName": "storage account tooreceive data",
        "storageAccountKey": "key of hello account",
        "perfCfg": [
        {
            "query": "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
            "table": "LinuxMemory"
        }
        ],
        "fileCfg": [
        {
            "file": "/var/log/mysql.err",
            "table": "mysqlerr"
        }
        ]
        }

<span data-ttu-id="e3fec-125">Negli esempi di hello precedenti, sostituire il numero di versione di hello con numero di versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="e3fec-125">In hello examples above, replace hello version number with hello latest version number.</span></span>

<span data-ttu-id="e3fec-126">Di seguito è riportato un modello di macchina virtuale completo per la creazione di una VM Linux con un'estensione:</span><span class="sxs-lookup"><span data-stu-id="e3fec-126">Here is a full VM template for creating a Linux VM with an extension:</span></span>

[<span data-ttu-id="e3fec-127">Estensione di script personalizzato in una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="e3fec-127">Custom Script Extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

