---
title: Esempio di script di Azure PowerShell - Connettere un'app Web a un database SQL | Microsoft Docs
description: Esempio di script di Azure PowerShell - Connettere un'app Web a un database SQL
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 5312bf6b81d1cc48490b71c3f77323cca23e1559
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="efaab-103">Connettere un'App Web a un database SQL</span><span class="sxs-lookup"><span data-stu-id="efaab-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="efaab-104">Questo scenario illustra come creare un database SQL di Azure e un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="efaab-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="efaab-105">Il database SQL viene quindi collegato all'App Web usando le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="efaab-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="efaab-106">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="efaab-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="efaab-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="efaab-107">Sample script</span></span>

<span data-ttu-id="efaab-108">[!code-powershell[principale](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connettere un'app Web a un database SQL")]</span><span class="sxs-lookup"><span data-stu-id="efaab-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="efaab-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="efaab-109">Clean up deployment</span></span> 

<span data-ttu-id="efaab-110">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="efaab-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="efaab-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="efaab-111">Script explanation</span></span>

<span data-ttu-id="efaab-112">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="efaab-112">This script uses the following commands.</span></span> <span data-ttu-id="efaab-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="efaab-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="efaab-114">Comando</span><span class="sxs-lookup"><span data-stu-id="efaab-114">Command</span></span> | <span data-ttu-id="efaab-115">Note</span><span class="sxs-lookup"><span data-stu-id="efaab-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="efaab-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="efaab-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="efaab-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="efaab-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="efaab-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="efaab-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="efaab-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="efaab-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="efaab-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="efaab-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="efaab-121">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="efaab-121">Creates a web app.</span></span> |
| [<span data-ttu-id="efaab-122">Nuovo AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="efaab-122">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="efaab-123">Creare un server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="efaab-123">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="efaab-124">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="efaab-124">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="efaab-125">Creare una nuova regola del firewall per un server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="efaab-125">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="efaab-126">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="efaab-126">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="efaab-127">Crea un database o un database elastico.</span><span class="sxs-lookup"><span data-stu-id="efaab-127">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="efaab-128">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="efaab-128">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="efaab-129">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="efaab-129">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="efaab-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="efaab-130">Next steps</span></span>

<span data-ttu-id="efaab-131">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="efaab-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="efaab-132">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="efaab-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
