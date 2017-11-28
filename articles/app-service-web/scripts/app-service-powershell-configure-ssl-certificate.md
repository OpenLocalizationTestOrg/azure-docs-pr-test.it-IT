---
title: Esempio di Script di PowerShell - aaaAzure associare un'app web tooa di certificato SSL personalizzata | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - Bind un'app web tooa di certificati SSL personalizzata
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="dadd5-103">Associare un'app web tooa di certificati SSL personalizzata</span><span class="sxs-lookup"><span data-stu-id="dadd5-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="dadd5-104">Questo script di esempio crea un'app web nel servizio App con le relative risorse correlate, quindi associa il certificato SSL hello di un tooit nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dadd5-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="dadd5-105">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dadd5-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="dadd5-106">Verificare inoltre se:</span><span class="sxs-lookup"><span data-stu-id="dadd5-106">Also, ensure that:</span></span>

- <span data-ttu-id="dadd5-107">Una connessione con Azure è stata creata utilizzando hello `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="dadd5-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="dadd5-108">È una pagina di configurazione del Registro di accesso tooyour dominio DNS.</span><span class="sxs-lookup"><span data-stu-id="dadd5-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="dadd5-109">È valido. Il file PFX e la relativa password per hello SSL certificato desidera tooupload e il binding.</span><span class="sxs-lookup"><span data-stu-id="dadd5-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="dadd5-110">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="dadd5-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dadd5-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="dadd5-111">Clean up deployment</span></span> 

<span data-ttu-id="dadd5-112">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="dadd5-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="dadd5-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="dadd5-113">Script explanation</span></span>

<span data-ttu-id="dadd5-114">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="dadd5-114">This script uses hello following commands.</span></span> <span data-ttu-id="dadd5-115">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="dadd5-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dadd5-116">Comando</span><span class="sxs-lookup"><span data-stu-id="dadd5-116">Command</span></span> | <span data-ttu-id="dadd5-117">Note</span><span class="sxs-lookup"><span data-stu-id="dadd5-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dadd5-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dadd5-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="dadd5-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="dadd5-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dadd5-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="dadd5-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="dadd5-121">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="dadd5-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="dadd5-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="dadd5-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="dadd5-123">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="dadd5-123">Creates a web app.</span></span> |
| [<span data-ttu-id="dadd5-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="dadd5-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="dadd5-125">Modifica il livello di prezzo di un toochange piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="dadd5-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="dadd5-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="dadd5-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="dadd5-127">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="dadd5-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="dadd5-128">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="dadd5-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="dadd5-129">Crea un'associazione al certificato SSL per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="dadd5-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dadd5-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dadd5-130">Next steps</span></span>

<span data-ttu-id="dadd5-131">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dadd5-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dadd5-132">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dadd5-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
