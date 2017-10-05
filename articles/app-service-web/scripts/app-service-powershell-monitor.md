---
title: Esempio di script di Azure PowerShell - Monitorare un'app Web con i log del server Web | Microsoft Docs
description: Esempio di script di Azure PowerShell - Monitorare un'app Web con i log del server Web
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 34a3dd318cb9896342fce870922ecd113b3ed08d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="d5fff-103">Monitorare un'App Web con i log del server Web</span><span class="sxs-lookup"><span data-stu-id="d5fff-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="d5fff-104">In questo scenario verrà creato un gruppo di risorse, un piano di servizio app e un'App Web e verrà configurata l'App Web per abilitare i log del server Web.</span><span class="sxs-lookup"><span data-stu-id="d5fff-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="d5fff-105">Quindi si scaricheranno i file di log per visionarli.</span><span class="sxs-lookup"><span data-stu-id="d5fff-105">You will then download the log files for review.</span></span>

<span data-ttu-id="d5fff-106">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="d5fff-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d5fff-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="d5fff-107">Sample script</span></span>

<span data-ttu-id="d5fff-108">[!code-powershell[principale](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitorare un'app Web con i log del server Web")]</span><span class="sxs-lookup"><span data-stu-id="d5fff-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d5fff-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d5fff-109">Clean up deployment</span></span> 

<span data-ttu-id="d5fff-110">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="d5fff-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d5fff-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="d5fff-111">Script explanation</span></span>

<span data-ttu-id="d5fff-112">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d5fff-112">This script uses the following commands.</span></span> <span data-ttu-id="d5fff-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="d5fff-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d5fff-114">Comando</span><span class="sxs-lookup"><span data-stu-id="d5fff-114">Command</span></span> | <span data-ttu-id="d5fff-115">Note</span><span class="sxs-lookup"><span data-stu-id="d5fff-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d5fff-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d5fff-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d5fff-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="d5fff-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d5fff-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d5fff-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d5fff-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="d5fff-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d5fff-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d5fff-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d5fff-121">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="d5fff-121">Creates a web app.</span></span> |
| [<span data-ttu-id="d5fff-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d5fff-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="d5fff-123">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="d5fff-123">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="d5fff-124">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="d5fff-124">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="d5fff-125">Ottiene la metrica di un'app web.</span><span class="sxs-lookup"><span data-stu-id="d5fff-125">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d5fff-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5fff-126">Next steps</span></span>

<span data-ttu-id="d5fff-127">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d5fff-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d5fff-128">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d5fff-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
