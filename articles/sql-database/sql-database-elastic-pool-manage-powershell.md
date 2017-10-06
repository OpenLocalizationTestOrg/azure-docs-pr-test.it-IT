---
title: 'PowerShell: creare e gestire un pool elastico SQL di Azure | Microsoft Docs'
description: Informazioni su come toouse PowerShell toomanage un pool elastico.
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Creare e gestire un pool elastico con PowerShell
In questo argomento illustra come toocreate e gestire scalabile [pool elastici](sql-database-elastic-pool.md) con PowerShell.  È anche possibile creare e gestire un pool elastico Azure utilizzando hello [portale di Azure](https://portal.azure.com/), l'API REST o [c#](sql-database-elastic-pool-manage-csharp.md). È anche possibile creare e spostare database verso e dai pool elastici usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Creare un pool elastico
Hello [New AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet crea un pool elastico. i valori Hello per eDTU per pool e min Dtu massime sono vincolati dal valore del livello servizio hello (Basic, Standard, Premium o RS Premium). Vedere [Limiti di archiviazione e di eDTU per pool elastici e database in pool](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Creare un nuovo database in pool in un pool elastico
Hello utilizzare [New AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet e set hello **ElasticPoolName** pool di destinazione toohello di parametro. toomove un database esistente in un pool elastico, vedere [spostare un database in un pool elastico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Script completo
Questo script crea un gruppo di risorse di Azure e un server. Quando richiesto, fornire un nome utente amministratore e una password per nuovo server di hello (non le credenziali di Azure).

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Creare un pool elastico e aggiungere più database in pool
Creazione di molti database in un pool elastico può richiedere tempo al termine della hello portale o i cmdlet di PowerShell che creano solo un singolo database alla volta. creazione di tooautomate in un pool elastico, vedere [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Spostare un database in un pool elastico
È possibile spostare un database interno o all'esterno di un pool elastico con hello [Set AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Modificare le impostazioni delle prestazioni di un pool elastico
Quando le prestazioni risultano lente, è possibile modificare impostazioni hello di crescita di hello pool tooaccommodate. Hello utilizzare [Set AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet. Impostare hello - Dtu parametro toohello Edtu per pool. Per i valori possibili, vedere [Limiti di archiviazione e di eDTU dei pool elastici e dei database elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>Modificare il limite di archiviazione hello per un pool elastico

Hello utilizzare [Set AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _- StorageMB_ parametro. Specificare il limite di archiviazione hello in MB (ad esempio, 2097152 imposta hello archiviazione limite too2 TB). Per i valori possibili, vedere [Limiti di archiviazione e di eDTU dei pool elastici e dei database elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

> [!IMPORTANT]
> archiviazione di dati max Hello predefinita per ogni pool per pool Premium con 1500 Edtu o più sono 750 GB. hello tooobtain superiore _max dimensioni di archiviazione di dati per ogni pool_, il limite di archiviazione hello deve essere impostato in modo esplicito. Pool Premium con più di 750 GB di spazio di archiviazione è attualmente in anteprima pubblica di hello seguenti aree: Stati Uniti orientali 2, Stati Uniti occidentali, ci Gov Virginia, Europa occidentale, Germania centrale, Asia sudorientale, Giappone orientale, Australia orientale, Canada centrale e in Canada orientale.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>Ottenere lo stato di hello delle operazioni del pool
La creazione di un pool elastico può richiedere tempo. stato hello tootrack delle operazioni del pool inclusi la creazione e gli aggiornamenti, utilizzare hello [Get AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Ottenere lo stato di hello di spostamento di un database in e da un pool elastico
Lo spostamento di un database può richiedere tempo. Tenere traccia di uno stato di spostamento tramite hello [Get AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Ottenere i dati di utilizzo delle risorse per un pool elastico
Metriche che possono essere recuperate come percentuale del limite di pool di risorse hello:

| Nome metrica | Descrizione |
|:--- |:--- |
| cpu\_percent |Utilizzo di calcolo Media in percentuale del limite di hello del pool di hello. |
| physical\_data\_read\_percent |Utilizzo medio dei / o in percentuale hello limite del pool di hello. |
| log\_write\_percent |Medio scrittura utilizzo delle risorse in percentuale del limite di hello del pool di hello. |
| DTU\_consumption\_percent |Utilizzo di eDTU medio espresso come percentuale del limite di eDTU per pool hello |
| storage\_percent |Utilizzo di spazio di archiviazione medio espresso come percentuale del limite di archiviazione hello del pool di hello. |
| workers\_percent |Massimi simultanee processi di lavoro (richieste), espresso in percentuale basata sul limite di hello del pool di hello. |
| sessions\_percent |Numero massimo di sessioni simultaneo espresso come percentuale sul limite di hello del pool di hello. |
| eDTU_limit |Impostazione del numero massimo DTU del pool elastico corrente per questo pool elastico durante l'intervallo. |
| storage\_limit |Impostazione del limite massimo di archiviazione del pool elastico corrente per questo pool elastico espresso in megabyte durante l'intervallo. |
| eDTU\_used |Numero di Edtu Media utilizzata dal pool hello in questo intervallo. |
| storage\_used |Spazio di archiviazione medio utilizzato dal pool hello in questo intervallo, in byte |

**Granularità della metrica/periodi di conservazione:**

* I dati vengono restituiti con una granularità di 5 minuti.  
* La conservazione dei dati è di 35 giorni.  

Questa API e i cmdlet limita il numero di hello di righe che possono essere recuperati in un'unica chiamata too1000 righe (circa 3 giorni di dati con granularità di 5 minuti). Ma questo comando può essere chiamato più volte con tooretrieve intervalli di tempo iniziale o finale di diversi altri dati

metrica di hello tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Ottenere i dati di utilizzo delle risorse per un database in un pool elastico
Queste API sono hello stesso hello API utilizzate per il monitoraggio di utilizzo delle risorse di un singolo database, ad eccezione delle seguenti differenze semantiche hello hello: le metriche recuperate sono espresse come percentuale di hello per ogni database max Edtu (o equivalente cap per hello sottostante metrica come CPU o dei / o) impostato per tale pool. 50% di utilizzo di uno qualsiasi di queste metriche, ad esempio, indica che il consumo di risorse specifico hello al 50% di hello al limite di database per tale risorsa nel pool di hello padre.

metrica di hello tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Aggiungere una risorsa del pool elastico tooan avviso
È possibile aggiungere regole di avviso tooan pool elastico toosend notifiche tramite posta elettronica o l'avviso stringhe troppo[endpoint URL](https://msdn.microsoft.com/library/mt718036.aspx) quando pool elastico hello raggiunga una soglia di utilizzo impostato. Utilizzare il cmdlet Add-AzureRmMetricAlertRule hello.

> [!IMPORTANT]
> Il monitoraggio dell'uso delle risorse per i pool elastici viene eseguito con un ritardo di almeno 5 minuti. Al momento non è possibile impostare avvisi inferiori ai 10 minuti per i pool elastici. Eventuali avvisi impostato per il pool elastico con un punto (parametro denominato "-WindowSize" nell'API di PowerShell) di meno di 10 minuti non può essere avviata. Verificare che gli avvisi definiti per i pool elastici usino un periodo (WindowSize) di almeno 10 minuti.
>
>

In questo esempio viene aggiunto un avviso per ricevere una notifica quando il consumo di eDTU del pool elastico supera una soglia stabilita.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

Per altre informazioni, vedere [Usare il portale di Azure per creare avvisi per il database SQL di Azure](sql-database-insights-alerts-portal.md).

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>Aggiungere database tooall degli avvisi in un pool elastico
È possibile aggiungere regole di avviso database tooall in un pool elastico di toosend notifiche tramite posta elettronica o l'avviso stringhe troppo[endpoint URL](https://msdn.microsoft.com/library/mt718036.aspx) quando una risorsa raggiunga una soglia di utilizzo impostata dall'avviso hello.

> [!IMPORTANT]
> Il monitoraggio dell'uso delle risorse per i pool elastici viene eseguito con un ritardo di almeno 5 minuti. Al momento non è possibile impostare avvisi inferiori ai 10 minuti per i pool elastici. Eventuali avvisi impostato per il pool elastico con un punto (parametro denominato "-WindowSize" nell'API di PowerShell) di meno di 10 minuti non può essere avviata. Verificare che gli avvisi definiti per i pool elastici usino un periodo (WindowSize) di almeno 10 minuti.
>

Questo esempio viene aggiunto un avviso tooeach dei database hello in un pool elastico per ricevere notifiche quando il consumo di DTU del database supera determinata soglia.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Raccogliere e monitorare i dati sull'utilizzo delle risorse in più pool in una sottoscrizione
Quando si dispone di molti database in una sottoscrizione, è scomodo toomonitor ogni elastica pool separatamente. Al contrario, i cmdlet PowerShell di database SQL e query T-SQL possono essere toocollect combinati i dati di utilizzo di risorse di più pool e i relativi database per il monitoraggio e analisi dell'utilizzo delle risorse. Oggetto [implementazione di esempio](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) di un set di questo tipo di powershell script è reperibile nel repository di esempi di hello GitHub SQL Server insieme documentazione su vengono eseguite e come toouse è.

toouse questa implementazione di esempio, eseguire la procedura seguente.

1. Scaricare hello [script e la documentazione](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Modificare gli script hello per l'ambiente. Specificare uno o più server in cui sono ospitati i pool elastici.
3. Specificare un database di telemetria in hello metriche raccolte sono toobe archiviati.
4. Personalizzare hello script toospecify hello Durata esecuzione degli script hello.

In generale, gli script hello hello seguenti:

* Enumera tutti i server in una determinata sottoscrizione di Azure (o in determinato elenco di server).
* Esegue un processo in background per ogni server. il processo di Hello viene eseguito in un ciclo a intervalli regolari e raccoglie i dati di telemetria per tutti i pool di hello in server hello. Quindi carica hello raccolti dati nel database specificato telemetria hello.
* Enumera un elenco di database in ogni pool toocollect hello database risorse sull'utilizzo di dati. Quindi carica hello raccolti dati nel database di telemetria hello.

Hello metriche raccolte nel database di telemetria hello possono essere analizzati toomonitor hello integrità del pool elastico e database hello in essa contenuti. script Hello installa anche una funzione con valori di tabella predefinita (TVF) in metriche hello telemetria database toohelp hello aggregazione per un intervallo di tempo specificato. Ad esempio, possono essere i risultati di hello TVF utilizzato tooshow "top N pool elastici con l'utilizzo di eDTU massimo hello in un determinato intervallo di tempo." Facoltativamente, usare strumenti analitici come Excel o Power BI tooquery e analizzare i dati raccolti hello.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Esempio: recuperare le metriche di consumo di risorse per un pool elastico e i relativi database
In questo esempio recupera le metriche di utilizzo hello per un determinato pool elastico e tutti i database. I dati raccolti sono formattati e scritti tooa file in formato CSV. file Hello può essere visualizzati con Excel.

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a>Latenza delle operazioni dei pool elastici
* Modifica hello min Edtu per database o un numero massimo di Edtu per ogni database in genere viene completata entro 5 minuti o meno.
* Modifica hello Edtu per pool dipende dalla quantità totale di hello dello spazio utilizzato da tutti i database nel pool di hello. Le modifiche richiedono una media di 90 minuti o meno per 100 GB. Ad esempio, se lo spazio totale hello utilizzato da tutti i database nel pool di hello è 200 GB, quindi hello prevista latenza per la modifica hello pool eDTU per pool è 3 ore o minore.



## <a name="next-steps"></a>Passaggi successivi
* [Creare processi elastici](sql-database-elastic-jobs-overview.md) elastici processi consentono di eseguire script T-SQL in un numero qualsiasi di database nel pool di hello.
* Vedere [scalabilità orizzontale con Database SQL di Azure](sql-database-elastic-scale-introduction.md): utilizzare strumenti elastico tooscale out, spostare i dati, eseguire una query o creare transazioni.
