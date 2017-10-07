---
title: aaaAzure Script di PowerShell di esempio - connettersi a un database SQL di web app tooa | Documenti Microsoft
description: 'Script di Azure PowerShell di esempio: la connessione a un database SQL tooa app web'
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
ms.openlocfilehash: 8f80b940378d020cbcaec2c1bbc28bae1a3ef35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="5ce14-103">La connessione a un database SQL tooa app web</span><span class="sxs-lookup"><span data-stu-id="5ce14-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="5ce14-104">In questo scenario si apprenderà come toocreate un database SQL di Azure e un Azure web app.</span><span class="sxs-lookup"><span data-stu-id="5ce14-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="5ce14-105">Quindi si procederà al collegamento hello SQL database toohello web app con le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="5ce14-105">Then you will link hello SQL database toohello web app using app settings.</span></span>

<span data-ttu-id="5ce14-106">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="5ce14-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="5ce14-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5ce14-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app tooa SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5ce14-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="5ce14-108">Clean up deployment</span></span> 

<span data-ttu-id="5ce14-109">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="5ce14-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="5ce14-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5ce14-110">Script explanation</span></span>

<span data-ttu-id="5ce14-111">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="5ce14-111">This script uses hello following commands.</span></span> <span data-ttu-id="5ce14-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="5ce14-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5ce14-113">Comando</span><span class="sxs-lookup"><span data-stu-id="5ce14-113">Command</span></span> | <span data-ttu-id="5ce14-114">Note</span><span class="sxs-lookup"><span data-stu-id="5ce14-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5ce14-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5ce14-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5ce14-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5ce14-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5ce14-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5ce14-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="5ce14-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="5ce14-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5ce14-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5ce14-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="5ce14-120">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="5ce14-120">Creates a web app.</span></span> |
| [<span data-ttu-id="5ce14-121">Nuovo AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="5ce14-121">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="5ce14-122">Creare un server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="5ce14-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="5ce14-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="5ce14-123">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="5ce14-124">Creare una nuova regola del firewall per un server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="5ce14-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="5ce14-125">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="5ce14-125">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="5ce14-126">Crea un database o un database elastico.</span><span class="sxs-lookup"><span data-stu-id="5ce14-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="5ce14-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5ce14-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="5ce14-128">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="5ce14-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5ce14-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5ce14-129">Next steps</span></span>

<span data-ttu-id="5ce14-130">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5ce14-130">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5ce14-131">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5ce14-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
