---
title: 'Azure PowerShell: creare un database SQL | Microsoft Docs'
description: Informazioni su come creare un server logico di database SQL, una regola del firewall a livello di server e database nel portale di Azure.
keywords: esercitazione sul database sql, creare un database sql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 44ed4a603977617c898315c4fc0b2d3dd3a8f16a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="9462c-104">Creare un singolo database SQL di Azure usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="9462c-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="9462c-105">PowerShell viene usato per creare e gestire le risorse di Azure dalla riga di comando o negli script.</span><span class="sxs-lookup"><span data-stu-id="9462c-105">PowerShell is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="9462c-106">Questa guida illustra in dettaglio l'uso di PowerShell per distribuire un database SQL di Azure in un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) in un [server logico di database SQL di Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="9462c-106">This guide details using PowerShell to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="9462c-107">Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="9462c-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="9462c-108">Questa esercitazione richiede il modulo Azure PowerShell 4.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="9462c-108">This tutorial requires the Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="9462c-109">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="9462c-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="9462c-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere come [installare il modulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="9462c-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="9462c-111">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="9462c-111">Log in to Azure</span></span>

<span data-ttu-id="9462c-112">Accedere alla sottoscrizione di Azure con il comando [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="9462c-112">Log in to your Azure subscription using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="9462c-113">Creare le variabili</span><span class="sxs-lookup"><span data-stu-id="9462c-113">Create variables</span></span>

<span data-ttu-id="9462c-114">Definire le variabili da usare negli script di questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="9462c-114">Define variables for use in the scripts in this quick start.</span></span>

```powershell
# The data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# The logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# The login information for the server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The ip address range that you want to allow to access your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# The database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="9462c-115">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="9462c-115">Create a resource group</span></span>

<span data-ttu-id="9462c-116">Creare un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) con il comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="9462c-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="9462c-117">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="9462c-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="9462c-118">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella posizione `westeurope`.</span><span class="sxs-lookup"><span data-stu-id="9462c-118">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="9462c-119">Creare un server logico</span><span class="sxs-lookup"><span data-stu-id="9462c-119">Create a logical server</span></span>

<span data-ttu-id="9462c-120">Creare un [server logico di database SQL di Azure](sql-database-features.md) con il comando [New AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver).</span><span class="sxs-lookup"><span data-stu-id="9462c-120">Create an [Azure SQL Database logical server](sql-database-features.md) using the [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="9462c-121">Un server logico contiene un gruppo di database gestiti come gruppo.</span><span class="sxs-lookup"><span data-stu-id="9462c-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="9462c-122">L'esempio seguente crea un server con un nome casuale nel gruppo di risorse con un account di accesso amministratore denominato `ServerAdmin` e la password `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="9462c-122">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="9462c-123">Sostituire questi valori predefiniti con quelli desiderati.</span><span class="sxs-lookup"><span data-stu-id="9462c-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="9462c-124">Configurare una regola del firewall del server</span><span class="sxs-lookup"><span data-stu-id="9462c-124">Configure a server firewall rule</span></span>

<span data-ttu-id="9462c-125">Creare una [regola del firewall a livello di server di database SQL di Azure](sql-database-firewall-configure.md) con il comando [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule).</span><span class="sxs-lookup"><span data-stu-id="9462c-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="9462c-126">Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio SQL Server Management Studio o l'utility SQLCMD, di connettersi a un database SQL tramite il firewall del servizio di database SQL.</span><span class="sxs-lookup"><span data-stu-id="9462c-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="9462c-127">Nell'esempio seguente, il firewall è aperto solo per altre risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9462c-127">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="9462c-128">Per abilitare la connettività esterna, modificare l'indirizzo IP in un indirizzo appropriato per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="9462c-128">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="9462c-129">Per aprire tutti gli indirizzi IP, usare 0.0.0.0 come indirizzo IP iniziale e 255.255.255.255 come indirizzo finale.</span><span class="sxs-lookup"><span data-stu-id="9462c-129">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="9462c-130">Il database SQL comunica attraverso la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="9462c-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="9462c-131">Se si sta tentando di connettersi da una rete aziendale, il traffico in uscita attraverso la porta 1433 potrebbe non essere autorizzato dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="9462c-131">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="9462c-132">In questo caso, non sarà possibile connettersi al server del database SQL di Azure, a meno che il reparto IT non apra la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="9462c-132">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="9462c-133">Creare un database nel server con dati di esempio</span><span class="sxs-lookup"><span data-stu-id="9462c-133">Create a database in the server with sample data</span></span>

<span data-ttu-id="9462c-134">Creare un database con [livello di prestazioni S0](sql-database-service-tiers.md) nel server con il comando [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase).</span><span class="sxs-lookup"><span data-stu-id="9462c-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="9462c-135">L'esempio seguente crea un database denominato `mySampleDatabase` e carica i dati di esempio di AdventureWorksLT in questo database.</span><span class="sxs-lookup"><span data-stu-id="9462c-135">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="9462c-136">Sostituire questi valori predefiniti con quelli desiderati. Altre guide introduttive di questa raccolta si basano sui valori di questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="9462c-136">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="9462c-137">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="9462c-137">Clean up resources</span></span>

<span data-ttu-id="9462c-138">Altre guide introduttive di questa raccolta si basano sui valori di questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="9462c-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="9462c-139">Se si prevede di continuare a usare le guide introduttive successive, non eliminare le risorse create in questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="9462c-139">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="9462c-140">Se non si prevede di continuare, seguire questa procedura per eliminare tutte le risorse create da questa guida introduttiva nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9462c-140">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="9462c-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9462c-141">Next steps</span></span>

<span data-ttu-id="9462c-142">Dopo aver creato un database, è possibile connettersi ed eseguire query usando gli strumenti preferiti.</span><span class="sxs-lookup"><span data-stu-id="9462c-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="9462c-143">Per altre informazioni, scegliere uno strumento di seguito:</span><span class="sxs-lookup"><span data-stu-id="9462c-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="9462c-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="9462c-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="9462c-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9462c-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="9462c-146">.NET</span><span class="sxs-lookup"><span data-stu-id="9462c-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="9462c-147">PHP</span><span class="sxs-lookup"><span data-stu-id="9462c-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="9462c-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="9462c-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="9462c-149">Java</span><span class="sxs-lookup"><span data-stu-id="9462c-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="9462c-150">Python</span><span class="sxs-lookup"><span data-stu-id="9462c-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="9462c-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="9462c-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

