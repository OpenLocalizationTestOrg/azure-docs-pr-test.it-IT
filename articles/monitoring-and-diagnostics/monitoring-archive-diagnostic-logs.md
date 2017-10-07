---
title: aaaArchive i log di diagnostica di Azure | Documenti Microsoft
description: Informazioni su come tooarchive registra la diagnostica di Azure per la conservazione a lungo termine in un account di archiviazione.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a>Archiviare i log di diagnostica di Azure
In questo articolo viene illustrato come è possibile utilizzare hello portale di Azure PowerShell Cmdlets CLI, o REST API tooarchive il [i log di diagnostica Azure](monitoring-overview-of-diagnostic-logs.md) in un account di archiviazione. Questa opzione è utile se si desidera tooretain la diagnostica registra con un criterio di conservazione facoltativo per backup, di analisi statica o di controllo. account di archiviazione Hello non presenti toobe hello stessa sottoscrizione di risorse hello la creazione di log come utente di hello che configura l'impostazione di hello dispone di sottoscrizioni di tooboth accesso RBAC appropriate.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, è necessario troppo[creare un account di archiviazione](../storage/storage-create-storage-account.md) toowhich è possibile archiviare i log di diagnostica. Si consiglia di non utilizzare un account di archiviazione esistente che dispone di altri, non di monitoraggio di dati in essa archiviati in modo che è possibile controllare meglio toomonitoring accedere ai dati. Tuttavia, se si desidera archiviare anche il registro attività e account di archiviazione tooa metriche di diagnostica, può avere senso toouse tale account di archiviazione per il log di diagnostica anche tookeep tutti i dati di monitoraggio in una posizione centrale. account di archiviazione Hello utilizzato deve essere un account di archiviazione generico, non un account di archiviazione blob.

## <a name="diagnostic-settings"></a>Impostazioni di diagnostica
tooarchive la diagnostica registra utilizzando uno dei seguenti metodi di hello, impostare un **impostazione diagnostica** per una particolare risorsa. Un'impostazione di diagnostica per una risorsa definisce le categorie di hello di log e dati di metrica inviati destinazione tooa (account di archiviazione, spazio dei nomi di hub eventi o Analitica Log). Definisce inoltre i criteri di conservazione hello (numero di giorni tooretain) per gli eventi di ogni categoria di log e dati di metrica archiviati in un account di archiviazione. Se un criterio di conservazione è impostato toozero, gli eventi per tale categoria di log vengono archiviati in modo permanente (che è sempre toosay,). Diversamente, un criterio di conservazione può essere qualsiasi numero di giorni compreso tra 1 e 2147483647. [Altre informazioni sulle impostazioni di diagnostica sono disponibili qui](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings). Criteri di conservazione vengono applicati al giorno, verranno eliminati in modo a hello fine di un giorno (UTC), i log da giorno hello che si trova ora oltre i criteri di conservazione hello. Ad esempio, se si dispone di un criterio di conservazione di un giorno, all'inizio di hello del giorno hello oggi hello registri hello ieri verrebbero eliminati

## <a name="archive-diagnostic-logs-using-hello-portal"></a>Archivio di log di diagnostica tramite il portale di hello
1. Nel portale di hello passare tooAzure Monitor e fare clic su **le impostazioni di diagnostica**

    ![Sezione relativa al monitoraggio di Monitoraggio di Azure](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. Se lo si desidera filtrare l'elenco hello in base al tipo di risorsa o gruppo di risorse, fare clic sul risorse hello per il quale si desidera tooset un'impostazione di diagnostica.

3. Se nessuna impostazione esistano nella risorsa hello selezionata, verrà richiesta toocreate un'impostazione. Fare clic su "Attiva diagnostica".

   ![Aggiungi impostazione di diagnostica - Nessuna impostazione esistente](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   Se sono presenti le impostazioni esistenti sulla risorsa hello, vedrai un elenco di impostazioni già configurato per questa risorsa. Fare clic su "Add diagnostic setting" (Aggiungi impostazione di diagnostica).

   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. Assegnare un nome all'impostazione e casella hello per **esportare tooStorage Account**, quindi selezionare un account di archiviazione. Facoltativamente, impostare il numero di giorni tooretain questi log tramite hello **conservazione (giorni)** dispositivi di scorrimento. La riserva di zero giorni registri hello vengono archiviati per un periodo illimitato.
   
   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Fare clic su **Salva**.

Dopo alcuni istanti, hello nuova impostazione è visualizzata nell'elenco delle impostazioni per questa risorsa e i log di diagnostica vengono archiviati toothat storage account appena nuovi dati di evento viene generati.

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>Archiviare i log di diagnostica tramite Azure PowerShell
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| Proprietà | Obbligatorio | Descrizione |
| --- | --- | --- |
| ResourceId |Sì |ID risorsa della risorsa di hello in cui si desidera tooset un'impostazione di diagnostica. |
| StorageAccountId |No |ID di risorsa dell'Account di archiviazione di hello toowhich i log di diagnostica deve essere salvato. |
| Categorie |No |Elenco delimitato da virgole di tooenable categorie log. |
| Enabled |Sì |Valore booleano che indica se la diagnostica viene abilitata o disabilitata per questa risorsa. |
| RetentionEnabled |No |Valore booleano che indica se un criterio di conservazione è abilitato per questa risorsa. |
| RetentionInDays |No |Numero di giorni per cui gli eventi devono essere conservati, compreso tra 1 e 2147483647. Un valore pari a zero registri hello vengono archiviati per un periodo illimitato. |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>Log di diagnostica di archiviazione tramite hello CLI multipiattaforma
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| Proprietà | Obbligatorio | Descrizione |
| --- | --- | --- |
| ResourceId |Sì |ID risorsa della risorsa di hello in cui si desidera tooset un'impostazione di diagnostica. |
| storageId |No |ID di risorsa di log di diagnostica toowhich hello Account di archiviazione deve essere salvato. |
| Categorie |No |Elenco delimitato da virgole di tooenable categorie log. |
| Enabled |Sì |Valore booleano che indica se la diagnostica viene abilitata o disabilitata per questa risorsa. |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>Log di diagnostica di archiviazione tramite hello API REST
[Vedere il documento](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) per informazioni su come è possibile configurare un'impostazione di diagnostica mediante hello API REST di monitoraggio di Azure.

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Schema dei log di diagnostica nell'account di archiviazione hello
Dopo aver configurato archiviazione, un contenitore di archiviazione viene creato nell'account di archiviazione hello non appena si verifica un evento in una delle categorie log hello che è stata abilitata. BLOB Hello all'interno del contenitore hello seguire hello stesso formato in log di diagnostica e hello Log attività. struttura Hello di tali BLOB è:

> insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{nome gruppo risorse}/PROVIDERS/{nome provider risorse}/{tipo risorsa}/{nome risorsa}/y={anno numerico a quattro cifre}/m={mese numerico a due cifre}/d={giorno numerico a due cifre}/h={ora in formato 24 ore a due cifre}/m=00/PT1H.json
> 
> 

O più semplicemente,

> insights-logs-{nome categoria log}/resourceId=/{ID risorsa}/y={anno numerico a quattro cifre}/m={mese numerico a due cifre}/d={giorno numerico a due cifre}/h={ora in formato 24 ore a due cifre}/m=00/PT1H.json
> 
> 

Ad esempio, un nome BLOB potrebbe essere:

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Ciascun blob PT1H.json contiene un blob JSON di eventi che si sono verificati entro ora hello specificata nell'URL blob hello (ad esempio, h = 12). Durante l'ora presenta hello, gli eventi sono accodati toohello PT1H.json file che si verificano. valore dei minuti Hello (m = 00) è sempre 00, poiché gli eventi di log di diagnostica sono suddivisi in singoli BLOB all'ora.

Nel file PT1H.json hello, ogni evento viene archiviato nella matrice di record"hello", il formato seguente:

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| Nome dell'elemento | Descrizione |
| --- | --- |
| time |Timestamp dell'evento hello è stato generato da hello di elaborazione del servizio Azure hello richiesta evento hello corrispondente. |
| resourceId |ID di risorsa di hello influisce sulle risorse. |
| operationName |Nome dell'operazione di hello. |
| category |Categoria di log dell'evento hello. |
| properties |Set di `<Key, Value>` coppie (ad esempio Dictionary) che descrive hello dettagli dell'evento hello. |

> [!NOTE]
> proprietà Hello e l'utilizzo di tali proprietà può variare a seconda delle risorse di hello.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione all'archivio BLOB di Azure con .NET](../storage/storage-dotnet-how-to-use-blobs.md)
* [Flusso diagnostica registra lo spazio dei nomi di hub eventi tooan](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Altre informazioni sui log di diagnostica](monitoring-overview-of-diagnostic-logs.md)
