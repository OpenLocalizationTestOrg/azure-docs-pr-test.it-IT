---
title: Esempio di script di Azure PowerShell - Associare un certificato SSL personalizzato a un'app Web | Microsoft Docs
description: Esempio di script di Azure PowerShell - Associare un certificato SSL personalizzato a un'app Web
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
ms.openlocfilehash: de8deccadcd9571be75447a117888bf2b3f571a0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="599a8-103">Associare un certificato SSL personalizzato a un'app Web</span><span class="sxs-lookup"><span data-stu-id="599a8-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="599a8-104">Questo script di esempio crea un'app Web nel servizio app con le relative risorse correlate, quindi associa ad essa il certificato SSL di un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="599a8-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> 

<span data-ttu-id="599a8-105">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="599a8-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="599a8-106">Verificare inoltre se:</span><span class="sxs-lookup"><span data-stu-id="599a8-106">Also, ensure that:</span></span>

- <span data-ttu-id="599a8-107">È stata creata una connessione con Azure usando il comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="599a8-107">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="599a8-108">Si disponga dell'accesso alla pagina di configurazione DNS del registrar.</span><span class="sxs-lookup"><span data-stu-id="599a8-108">You have access to your domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="599a8-109">Si disponga di un file con estensione PFX valido e della relativa password per il certificato SSL da caricare e per cui si desidera eseguire l'associazione.</span><span class="sxs-lookup"><span data-stu-id="599a8-109">You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="599a8-110">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="599a8-110">Sample script</span></span>

<span data-ttu-id="599a8-111">[!code-powershell[principale](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Associare un certificato SSL personalizzato a un'app Web")]</span><span class="sxs-lookup"><span data-stu-id="599a8-111">[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="599a8-112">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="599a8-112">Clean up deployment</span></span> 

<span data-ttu-id="599a8-113">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="599a8-113">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="599a8-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="599a8-114">Script explanation</span></span>

<span data-ttu-id="599a8-115">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="599a8-115">This script uses the following commands.</span></span> <span data-ttu-id="599a8-116">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="599a8-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="599a8-117">Comando</span><span class="sxs-lookup"><span data-stu-id="599a8-117">Command</span></span> | <span data-ttu-id="599a8-118">Note</span><span class="sxs-lookup"><span data-stu-id="599a8-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="599a8-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="599a8-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="599a8-120">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="599a8-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="599a8-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="599a8-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="599a8-122">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="599a8-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="599a8-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="599a8-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="599a8-124">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="599a8-124">Creates a web app.</span></span> |
| [<span data-ttu-id="599a8-125">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="599a8-125">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="599a8-126">Modifica un piano di servizio app per cambiarne il piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="599a8-126">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="599a8-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="599a8-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="599a8-128">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="599a8-128">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="599a8-129">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="599a8-129">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="599a8-130">Crea un'associazione al certificato SSL per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="599a8-130">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="599a8-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="599a8-131">Next steps</span></span>

<span data-ttu-id="599a8-132">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="599a8-132">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="599a8-133">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="599a8-133">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
