---
title: Esempio di script di Azure PowerShell - Connettere un'app Web a un account di archiviazione | Microsoft Docs
description: Esempio di script di Azure PowerShell - Connettere un'app Web a un account di archiviazione
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
ms.openlocfilehash: 481f3efdb1cbbeba328183da7e320c7e5b819b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="3c07f-103">Connettere un'App Web a un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3c07f-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="3c07f-104">Questo scenario illustra come creare un account di archiviazione di Azure e un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c07f-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="3c07f-105">L'account di archiviazione viene quindi collegato all'App Web usando le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="3c07f-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="3c07f-106">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="3c07f-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="3c07f-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="3c07f-107">Sample script</span></span>

<span data-ttu-id="3c07f-108">[!code-powershell[principale](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connettere un'app Web a un account di archiviazione")]</span><span class="sxs-lookup"><span data-stu-id="3c07f-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3c07f-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="3c07f-109">Clean up deployment</span></span> 

<span data-ttu-id="3c07f-110">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="3c07f-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3c07f-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="3c07f-111">Script explanation</span></span>

<span data-ttu-id="3c07f-112">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3c07f-112">This script uses the following commands.</span></span> <span data-ttu-id="3c07f-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="3c07f-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3c07f-114">Comando</span><span class="sxs-lookup"><span data-stu-id="3c07f-114">Command</span></span> | <span data-ttu-id="3c07f-115">Note</span><span class="sxs-lookup"><span data-stu-id="3c07f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3c07f-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3c07f-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3c07f-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="3c07f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3c07f-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3c07f-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="3c07f-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="3c07f-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3c07f-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3c07f-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="3c07f-121">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="3c07f-121">Creates a web app.</span></span> |
| [<span data-ttu-id="3c07f-122">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="3c07f-122">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="3c07f-123">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c07f-123">Creates a Storage account.</span></span> |
| [<span data-ttu-id="3c07f-124">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="3c07f-124">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="3c07f-125">Ottiene le chiavi di accesso per l'account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c07f-125">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="3c07f-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3c07f-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="3c07f-127">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="3c07f-127">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3c07f-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c07f-128">Next steps</span></span>

<span data-ttu-id="3c07f-129">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c07f-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3c07f-130">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="3c07f-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
