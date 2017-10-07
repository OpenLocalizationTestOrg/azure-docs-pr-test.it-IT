---
title: 'Azure PowerShell: creare un database SQL | Microsoft Docs'
description: Informazioni su come toocreate un server logico di Database SQL regola del firewall a livello di server e database hello portale di Azure.
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
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a>Creare un singolo database SQL di Azure usando PowerShell

PowerShell viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script. Un database SQL di Azure in questa Guida. dettagli utilizzando PowerShell toodeploy un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) in un [server logico di Database SQL di Azure](sql-database-features.md).

Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.

Questa esercitazione richiede hello Azure PowerShell versione 4.0 o versione successiva del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps). 

## <a name="log-in-tooazure"></a>Accedi tooAzure

Accedi tooyour sottoscrizione di Azure utilizzando hello [Aggiungi AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) comando e seguire hello le direzioni.

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a>Creare le variabili

Definire le variabili da usare negli script hello in questa Guida introduttiva.

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) utilizzando hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando. Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo. esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westeurope` percorso.

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a>Creare un server logico

Creare un [server logico di Database SQL di Azure](sql-database-features.md) utilizzando hello [New AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) comando. Un server logico contiene un gruppo di database gestiti come gruppo. Hello seguente viene creato un server denominato in modo casuale nel gruppo di risorse con un account di accesso amministratore denominato `ServerAdmin` e la password `ChangeYourAdminPassword1`. Sostituire questi valori predefiniti con quelli desiderati.

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a>Configurare una regola del firewall del server

Creare un [regola del firewall a livello di server Database SQL di Azure](sql-database-firewall-configure.md) utilizzando hello [New AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) comando. Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio SQL Server Management Studio o hello SQLCMD utility tooconnect tooa database SQL tramite firewall del servizio Database SQL hello. Nell'esempio seguente di hello, firewall hello è aperta solo per le altre risorse di Azure. connettività esterna tooenable, modifica hello tooan appropriato indirizzo per l'ambiente. tooopen tutti gli indirizzi IP, utilizzare 0.0.0.0 come hello avvio indirizzo IP e 255.255.255.255 come hello indirizzo finale.

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> Il database SQL comunica attraverso la porta 1433. Se si sta tentando di tooconnect da una rete aziendale, può non essere consentito il traffico in uscita sulla porta 1433 dal firewall della rete. In questo caso, non sarà server di Database SQL di Azure in grado di tooconnect tooyour, a meno che il reparto IT consente di aprire la porta 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Creare un database in server hello con dati di esempio

Creare un database con un [livello di prestazioni S0](sql-database-service-tiers.md) nel server di hello tramite hello [New AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) comando. esempio Hello crea un database denominato `mySampleDatabase` e carica i dati di esempio AdventureWorksLT di hello in questo database. Sostituire questi predefiniti i valori in base alle esigenze (altre guide introduttive in questa compilazione insieme ai valori hello in questa Guida introduttiva).

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a>Pulire le risorse

Altre guide introduttive di questa raccolta si basano sui valori di questa guida introduttiva. 

> [!TIP]
> Se si intende toocontinue toowork con avvio rapido successive, non pulire le risorse di hello create in questa Guida introduttiva avviato. Se non si prevede toocontinue, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa Guida introduttiva in hello portale di Azure.
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un database, è possibile connettersi ed eseguire query usando gli strumenti preferiti. Per altre informazioni, scegliere uno strumento di seguito:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.JS](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

