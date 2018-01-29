---
title: 'Interfaccia della riga di comando di Azure: creare un database SQL | Microsoft Docs'
description: Come creare un server logico di database SQL, una regola del firewall a livello di server e un database usando l'interfaccia della riga di comando di Azure.
keywords: esercitazione sul database sql, creare un database sql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: On Demand
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: quickstart
ms.date: 10/11/2017
ms.author: carlrab
ms.openlocfilehash: 5076a9fcbfb0c46a0aebf858d5ec1dcbee839946
ms.sourcegitcommit: dfd49613fce4ce917e844d205c85359ff093bb9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/31/2017
---
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a>Creare un singolo database SQL di Azure usando l'interfaccia della riga di comando di Azure

L'interfaccia della riga di comando di Azure viene usata per creare e gestire le risorse di Azure dalla riga di comando o negli script. Questa guida illustra in dettaglio l'uso dell'interfaccia della riga di comando di Azure per distribuire un database SQL di Azure in un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) in un [server logico del database SQL di Azure](sql-database-features.md).

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure. Eseguire `az --version` per trovare la versione. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="define-variables"></a>Definire le variabili

Definire le variabili da usare negli script di questa guida introduttiva.

```azurecli-interactive
# The data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# The logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# The ip address range that you want to allow to access your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# The database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) con il comando [az group create](/cli/azure/group#az_group_create). Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo. Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella posizione `westeurope`.

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>Creare un server logico

Creare un [server logico del database SQL di Azure](sql-database-features.md) con il comando [az sql server create](/cli/azure/sql/server#az_sql_server_create). Un server logico contiene un gruppo di database gestiti come gruppo. L'esempio seguente crea un server con un nome casuale nel gruppo di risorse con un account di accesso amministratore denominato `ServerAdmin` e la password `ChangeYourAdminPassword1`. Sostituire questi valori predefiniti con quelli desiderati.

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>Configurare una regola del firewall del server

Creare una [regola del firewall del server del database SQL di Azure](sql-database-firewall-configure.md) con il comando [az sql server firewall create](/cli/azure/sql/server/firewall-rule#az_sql_server_firewall_rule_create). Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio SQL Server Management Studio o l'utility SQLCMD, di connettersi a un database SQL tramite il firewall del servizio di database SQL. Nell'esempio seguente, il firewall è aperto solo per altre risorse di Azure. Per abilitare la connettività esterna, modificare l'indirizzo IP in un indirizzo appropriato per l'ambiente. Per aprire tutti gli indirizzi IP, usare 0.0.0.0 come indirizzo IP iniziale e 255.255.255.255 come indirizzo finale.  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> Il database SQL comunica attraverso la porta 1433. Se si sta tentando di connettersi da una rete aziendale, il traffico in uscita attraverso la porta 1433 potrebbe non essere autorizzato dal firewall della rete. In questo caso, non sarà possibile connettersi al server del database SQL di Azure, a meno che il reparto IT non apra la porta 1433.
>

## <a name="create-a-database-in-the-server-with-sample-data"></a>Creare un database nel server con dati di esempio

Creare nel server un database con [livello di prestazioni S0](sql-database-service-tiers.md) con il comando [az sql db create](/cli/azure/sql/db#az_sql_db_create). L'esempio seguente crea un database denominato `mySampleDatabase` e carica i dati di esempio di AdventureWorksLT in questo database. Sostituire questi valori predefiniti con quelli desiderati. Altre guide introduttive di questa raccolta si basano sui valori di questa guida introduttiva.

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>Pulire le risorse

Altre guide introduttive di questa raccolta si basano sui valori di questa guida introduttiva. 

> [!TIP]
> Se si prevede di continuare a usare le guide introduttive successive, non eliminare le risorse create in questa guida introduttiva. Se non si prevede di continuare, seguire questa procedura per eliminare tutte le risorse create da questa guida introduttiva nel portale di Azure.
>

```azurecli-interactive
az group delete --name $resourcegroupname
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

