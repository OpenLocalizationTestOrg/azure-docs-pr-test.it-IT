---
title: Esempio di Script di PowerShell - caricamento file tooa app web tramite FTP aaaAzure | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - caricamento file tooa app web tramite FTP
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
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="12b31-103">Caricare file tooa web app tramite FTP</span><span class="sxs-lookup"><span data-stu-id="12b31-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="12b31-104">Questo script di esempio crea un'App Web nel servizio app con le risorse correlate e quindi distribuisce il codice dell'App Web tramite FTP (con [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="12b31-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="12b31-105">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="12b31-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="12b31-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="12b31-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="12b31-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="12b31-107">Clean up deployment</span></span> 

<span data-ttu-id="12b31-108">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="12b31-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="12b31-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="12b31-109">Script explanation</span></span>

<span data-ttu-id="12b31-110">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="12b31-110">This script uses hello following commands.</span></span> <span data-ttu-id="12b31-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="12b31-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="12b31-112">Comando</span><span class="sxs-lookup"><span data-stu-id="12b31-112">Command</span></span> | <span data-ttu-id="12b31-113">Note</span><span class="sxs-lookup"><span data-stu-id="12b31-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="12b31-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="12b31-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="12b31-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="12b31-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="12b31-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="12b31-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="12b31-117">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="12b31-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="12b31-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="12b31-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="12b31-119">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="12b31-119">Creates a web app.</span></span> |
| [<span data-ttu-id="12b31-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="12b31-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="12b31-121">Ottenere un profilo di pubblicazione delle app Web.</span><span class="sxs-lookup"><span data-stu-id="12b31-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="12b31-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12b31-122">Next steps</span></span>

<span data-ttu-id="12b31-123">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="12b31-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="12b31-124">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="12b31-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
