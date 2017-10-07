---
title: aaaAzure Script di PowerShell di esempio - connettersi a un account di archiviazione web app tooa | Documenti Microsoft
description: Script di Azure PowerShell di esempio - connettersi a un account di archiviazione tooa app web
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="7f795-103">Connettersi a un account di archiviazione tooa app web</span><span class="sxs-lookup"><span data-stu-id="7f795-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="7f795-104">In questo scenario si apprenderà come toocreate un account di archiviazione di Azure e un Azure web app.</span><span class="sxs-lookup"><span data-stu-id="7f795-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="7f795-105">Quindi si procederà al collegamento hello archiviazione toohello web app dell'account utilizzando le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="7f795-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="7f795-106">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="7f795-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="7f795-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="7f795-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7f795-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="7f795-108">Clean up deployment</span></span> 

<span data-ttu-id="7f795-109">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="7f795-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="7f795-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="7f795-110">Script explanation</span></span>

<span data-ttu-id="7f795-111">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="7f795-111">This script uses hello following commands.</span></span> <span data-ttu-id="7f795-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="7f795-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7f795-113">Comando</span><span class="sxs-lookup"><span data-stu-id="7f795-113">Command</span></span> | <span data-ttu-id="7f795-114">Note</span><span class="sxs-lookup"><span data-stu-id="7f795-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7f795-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7f795-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7f795-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="7f795-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7f795-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7f795-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="7f795-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="7f795-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7f795-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7f795-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="7f795-120">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="7f795-120">Creates a web app.</span></span> |
| [<span data-ttu-id="7f795-121">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="7f795-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="7f795-122">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7f795-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="7f795-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="7f795-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="7f795-124">Ottiene le chiavi di accesso hello per un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f795-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="7f795-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7f795-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="7f795-126">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="7f795-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7f795-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f795-127">Next steps</span></span>

<span data-ttu-id="7f795-128">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7f795-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7f795-129">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7f795-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
