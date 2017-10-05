---
title: Esempio di script di Azure PowerShell - Caricare i file in un'app Web usando FTP | Microsoft Docs
description: Esempio di script di Azure PowerShell - Caricare i file in un'app Web usando FTP
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 96b99110b63b037746fcc40eb15db5d718eb71a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-to-a-web-app-using-ftp"></a><span data-ttu-id="afe9a-103">Caricare i file in un'app Web tramite FTP</span><span class="sxs-lookup"><span data-stu-id="afe9a-103">Upload files to a web app using FTP</span></span>

<span data-ttu-id="afe9a-104">Questo script di esempio crea un'App Web nel servizio app con le risorse correlate e quindi distribuisce il codice dell'App Web tramite FTP (con [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="afe9a-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="afe9a-105">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="afe9a-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="afe9a-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="afe9a-106">Sample script</span></span>

<span data-ttu-id="afe9a-107">[!code-powershell[principale](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Caricare i file in un'app Web tramite FTP")]</span><span class="sxs-lookup"><span data-stu-id="afe9a-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files to a web app using FTP")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="afe9a-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="afe9a-108">Clean up deployment</span></span> 

<span data-ttu-id="afe9a-109">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="afe9a-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="afe9a-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="afe9a-110">Script explanation</span></span>

<span data-ttu-id="afe9a-111">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="afe9a-111">This script uses the following commands.</span></span> <span data-ttu-id="afe9a-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="afe9a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="afe9a-113">Comando</span><span class="sxs-lookup"><span data-stu-id="afe9a-113">Command</span></span> | <span data-ttu-id="afe9a-114">Note</span><span class="sxs-lookup"><span data-stu-id="afe9a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="afe9a-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="afe9a-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="afe9a-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="afe9a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="afe9a-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="afe9a-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="afe9a-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="afe9a-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="afe9a-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="afe9a-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="afe9a-120">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="afe9a-120">Creates a web app.</span></span> |
| [<span data-ttu-id="afe9a-121">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="afe9a-121">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="afe9a-122">Ottenere un profilo di pubblicazione delle app Web.</span><span class="sxs-lookup"><span data-stu-id="afe9a-122">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="afe9a-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="afe9a-123">Next steps</span></span>

<span data-ttu-id="afe9a-124">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="afe9a-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="afe9a-125">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="afe9a-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
