---
title: aaaAzure Cosmos DB automazione - gestione con Powershell | Documenti Microsoft
description: Usare Azure Powershell per gestire gli account di Azure Cosmos DB.
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>Creare un account di Azure Cosmos DB mediante PowerShell

Hello Guida seguente vengono descritti comandi tooautomate gestione degli account di database DB Cosmos Azure con Azure Powershell. Include inoltre le chiavi dell'account toomanage comandi e le priorità di failover in [account database multiarea][scaling-globally]. Aggiornamento account del database consente di criteri di verifica coerenza toomodify e aree di aggiunta o rimozione. Per la gestione dell'account di Azure Cosmos DB multipiattaforma, è possibile utilizzare [CLI di Azure](cli-samples.md), hello [API REST del Provider di risorse][rp-rest-api], o hello [Azure portale](create-documentdb-dotnet.md#create-account).

## <a name="getting-started"></a>Introduzione

Seguire le istruzioni hello [come tooinstall e configurare Azure PowerShell] [ powershell-install-configure] tooinstall e log in Gestione risorse di Azure tooyour account in Powershell.

### <a name="notes"></a>Note

* Se si desidera hello tooexecute seguenti comandi senza richiedere conferma all'utente, aggiungere hello `-Force` flag toohello comando.
* Hello tutti i seguenti comandi sono sincroni.

## <a id="create-documentdb-account-powershell"></a> Creare un account di Azure Cosmos DB

Questo comando consente un account di database di Azure Cosmos DB toocreate. Configurare il nuovo account del database come ad area singola o [a più aree][scaling-globally] con un determinato [criterio di coerenza](consistency-levels.md).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`nome di percorso Hello di hello scrivere area dell'account database hello. Questo percorso è toohave richiesto un valore di priorità di failover pari a 0. Deve essere presente esattamente un'area di scrittura per ogni account di database.
* `<read-region-location>`nome di percorso Hello di hello letto area dell'account database hello. Questo percorso è toohave richiesto un valore di priorità di failover di maggiore di 0. Possono essere presenti più aree di lettura per ogni account di database.
* `<ip-range-filter>`Specifica il set di hello di indirizzi IP o intervalli di indirizzi IP in toobe formato CIDR inclusa come hello consentito l'elenco di IP client per un account di database specificato. Gli intervalli di indirizzi IP o i singoli indirizzi IP devono essere delimitati da virgole e non devono contenere spazi. Per altre informazioni, vedere [Azure Cosmos DB Firewall Support](firewall-support.md) (Supporto al firewall di Azure Cosmos DB)
* `<default-consistency-level>`livello di coerenza Hello predefinito di hello account Azure Cosmos DB. Per altre informazioni, vedere [Livelli di coerenza in Azure Cosmos DB](consistency-levels.md).
* `<max-interval>`Se utilizzato con la coerenza con obsolescenza associata, questo valore rappresenta hello ora quantità di obsolescenza (in secondi), che è consentito. L'intervallo consentito per questo valore è compreso tra 1 e 100.
* `<max-staleness-prefix>`Se utilizzato con la coerenza con obsolescenza associata, questo valore rappresenta il numero di hello di richieste non aggiornate, che è consentito. L'intervallo consentito per questo valore è compreso tra 1 e 2.147.483.647.
* `<resource-group-name>`nome Hello di hello [il gruppo di risorse di Azure] [ azure-resource-groups] toowhich hello nuovo Azure Cosmos DB account di database appartiene.
* `<resource-group-location>`percorso di Hello di hello il gruppo di risorse di Azure toowhich hello nuovo Azure Cosmos DB account del database a cui appartiene.
* `<database-account-name>`nome Hello di hello Azure Cosmos DB database account toobe creato. È possibile utilizzare solo lettere minuscole, numeri, hello '-' caratteri e deve essere compresa tra 3 e 50 caratteri.

Esempio: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>Note
* Hello precedente viene creato un account di database con due aree. È inoltre possibile toocreate un account di database con una regione (che viene designata come area di scrittura hello e un valore di priorità di failover pari a 0) o più di due aree. Per altre informazioni, vedere gli [account di database tra più aree][scaling-globally].
* percorsi di Hello devono essere aree geografiche in cui è in genere disponibile Azure Cosmos DB. Hello elenco corrente di aree di su hello [pagina aree di Azure](https://azure.microsoft.com/regions/#services).

## <a id="update-documentdb-account-powershell"></a> Aggiornare un account di database DocumentDB

Questo comando consente tooupdate proprietà dell'account database Azure Cosmos DB. Sono inclusi i criteri di verifica coerenza hello e percorsi hello quali account di database hello presente in.

> [!NOTE]
> Questo comando consente di tooadd e rimuovere le aree, ma non è possibile toomodify le priorità di failover. toomodify le priorità di failover, vedere [sotto](#modify-failover-priority-powershell).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`nome di percorso Hello di hello scrivere area dell'account database hello. Questo percorso è toohave richiesto un valore di priorità di failover pari a 0. Deve essere presente esattamente un'area di scrittura per ogni account di database.
* `<read-region-location>`nome di percorso Hello di hello letto area dell'account database hello. Questo percorso è toohave richiesto un valore di priorità di failover di maggiore di 0. Possono essere presenti più aree di lettura per ogni account di database.
* `<default-consistency-level>`livello di coerenza Hello predefinito di hello account Azure Cosmos DB. Per altre informazioni, vedere [Livelli di coerenza in Azure Cosmos DB](consistency-levels.md).
* `<ip-range-filter>`Specifica il set di hello di indirizzi IP o intervalli di indirizzi IP in toobe formato CIDR inclusa come hello consentito l'elenco di IP client per un account di database specificato. Gli intervalli di indirizzi IP o i singoli indirizzi IP devono essere delimitati da virgole e non devono contenere spazi. Per altre informazioni, vedere [Azure Cosmos DB Firewall Support](firewall-support.md) (Supporto al firewall di Azure Cosmos DB)
* `<max-interval>`Se utilizzato con la coerenza con obsolescenza associata, questo valore rappresenta hello ora quantità di obsolescenza (in secondi), che è consentito. L'intervallo consentito per questo valore è compreso tra 1 e 100.
* `<max-staleness-prefix>`Se utilizzato con la coerenza con obsolescenza associata, questo valore rappresenta il numero di hello di richieste non aggiornate, che è consentito. L'intervallo consentito per questo valore è compreso tra 1 e 2.147.483.647.
* `<resource-group-name>`nome Hello di hello [il gruppo di risorse di Azure] [ azure-resource-groups] toowhich hello nuovo Azure Cosmos DB account di database appartiene.
* `<resource-group-location>`percorso di Hello di hello il gruppo di risorse di Azure toowhich hello nuovo Azure Cosmos DB account del database a cui appartiene.
* `<database-account-name>`nome Hello di hello Azure Cosmos DB database account toobe aggiornato.

Esempio: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a> Eliminare un account di database DocumentDB

Questo comando consente un account di database esistente di Azure Cosmos DB toodelete.

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`nome Hello di hello [il gruppo di risorse di Azure] [ azure-resource-groups] toowhich hello nuovo Azure Cosmos DB account di database appartiene.
* `<database-account-name>`nome Hello di hello Azure Cosmos DB database account toobe eliminato.

Esempio:

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a> Ottenere le proprietà di un account di database DocumentDB

Questo comando consente di proprietà hello tooget di un account di database DB Cosmos Azure esistente.

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nome Hello di hello [il gruppo di risorse di Azure] [ azure-resource-groups] toowhich hello nuovo Azure Cosmos DB account di database appartiene.
* `<database-account-name>`nome Hello di hello Azure Cosmos DB account del database.

Esempio:

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a> Tag di aggiornamento dell'account del database Azure Cosmos DB

Hello seguente descrive come tooset [i tag delle risorse Azure] [ azure-resource-tags] per il database di Azure Cosmos account del database.

> [!NOTE]
> Questo comando può essere combinato con hello creare o aggiornare i comandi aggiungendo hello `-Tags` flag con parametro corrispondente hello.

Esempio:

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a> Elencare le chiavi dell'account

Quando si crea un account Azure Cosmos DB, il servizio di hello genera due chiavi di accesso generale che possono essere utilizzate per l'autenticazione quando si accede a hello account Azure Cosmos DB. Fornendo due chiavi di accesso, Azure Cosmos DB consente chiavi hello tooregenerate con nessun tooyour interruzione account Azure Cosmos DB. Sono disponibili anche chiavi di sola lettura per l'autenticazione delle operazioni di sola lettura. Esistono due chiavi di lettura/scrittura (primaria e secondaria) e due chiavi di sola lettura (primaria e secondaria).

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nome Hello di hello [il gruppo di risorse di Azure] [ azure-resource-groups] toowhich hello nuovo Azure Cosmos DB account di database appartiene.
* `<database-account-name>`nome Hello di hello Azure Cosmos DB account del database.

Esempio:

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a> Elencare le stringhe di connessione

Per gli account di MongoDB, hello tooconnect di stringa di connessione che l'account del database MongoDB toohello app può essere recuperato tramite hello comando seguente.

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nome Hello di hello [il gruppo di risorse di Azure] [ azure-resource-groups] toowhich hello nuovo Azure Cosmos DB account di database appartiene.
* `<database-account-name>`nome Hello di hello Azure Cosmos DB account del database.

Esempio:

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a> Rigenerare una chiave dell'account

È necessario impostare account di Azure Cosmos DB tooyour di hello accesso chiavi periodicamente toohelp rendere più sicuro le connessioni. Due chiavi di accesso assegnate tooenable si toomaintain connessioni toohello account Azure Cosmos DB usando una chiave di accesso, mentre si rigenera hello altre chiavi di accesso.

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`nome Hello di hello [il gruppo di risorse di Azure] [ azure-resource-groups] toowhich hello nuovo Azure Cosmos DB account di database appartiene.
* `<database-account-name>`nome Hello di hello Azure Cosmos DB account del database.
* `<key-kind>`Uno dei tipi di hello quattro delle chiavi: ["Primary" | " Secondario "|" PrimaryReadonly "|" SecondaryReadonly"] che si desidera tooregenerate.

Esempio:

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a> Modificare la priorità di failover di un account del database Azure Cosmos DB

Per gli account di database con più aree, è possibile modificare la priorità di failover hello di hello diverse aree geografiche che hello Azure Cosmos DB account del database esiste nel. Per altre informazioni sul failover nell'account del database Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB][distribute-data-globally].

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`nome di percorso Hello di hello scrivere area dell'account database hello. Questo percorso è toohave richiesto un valore di priorità di failover pari a 0. Deve essere presente esattamente un'area di scrittura per ogni account di database.
* `<read-region-location>`nome di percorso Hello di hello letto area dell'account database hello. Questo percorso è toohave richiesto un valore di priorità di failover di maggiore di 0. Possono essere presenti più aree di lettura per ogni account di database.
* `<resource-group-name>`nome Hello di hello [il gruppo di risorse di Azure] [ azure-resource-groups] toowhich hello nuovo Azure Cosmos DB account di database appartiene.
* `<database-account-name>`nome Hello di hello Azure Cosmos DB account del database.

Esempio:

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>Passaggi successivi

* tooconnect usando .NET, vedere [Connect e query con .NET](create-documentdb-dotnet.md).
* tooconnect usando .NET Core, vedere [Connect e query con .NET Core](create-documentdb-dotnet-core.md).
* tooconnect con Node.js, vedere [Connect e query con Node.js e un'app di MongoDB](create-mongodb-nodejs.md).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
