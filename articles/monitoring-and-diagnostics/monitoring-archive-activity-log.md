---
title: "hello aaaArchive Log attività di Azure | Documenti Microsoft"
description: "Informazioni su come tooarchive accedere l'attività di Azure per la conservazione a lungo termine in un account di archiviazione."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a>Archiviare hello Log attività di Azure
In questo articolo, ecco come è possibile utilizzare hello portale di Azure, PowerShell Cmdlets o tooarchive CLI multipiattaforma il [ **Log attività Azure** ](monitoring-overview-activity-logs.md) in un account di archiviazione. Questa opzione è utile se si desidera tooretain il Log attività di più di 90 giorni (con controllo completo sui criteri di conservazione hello) per controllare, analisi statica, o eseguire il backup. Se è necessario solo tooretain gli eventi per 90 giorni o meno è tooset tooa dell'archivio account di archiviazione, non è necessario poiché gli eventi del registro attività vengono conservati per 90 giorni senza abilitare archiviazione nella piattaforma Azure hello.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, è necessario troppo[creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich è possibile archiviare i Log di attività. Si consiglia di non utilizzare un account di archiviazione esistente che dispone di altri, non di monitoraggio di dati in essa archiviati in modo che è possibile controllare meglio toomonitoring accedere ai dati. Tuttavia, se si desidera archiviare anche i log di diagnostica e account di archiviazione tooa metriche, può avere senso toouse tale account di archiviazione per l'attività di Log anche tookeep tutti i dati di monitoraggio in una posizione centrale. account di archiviazione Hello utilizzato deve essere un account di archiviazione generico, non un account di archiviazione blob. account di archiviazione Hello non presenti toobe hello stessa sottoscrizione come sottoscrizione hello la creazione di log come utente di hello che configura l'impostazione di hello dispone di sottoscrizioni di tooboth accesso RBAC appropriate.

## <a name="log-profile"></a>Profilo del log
hello tooarchive Log attività utilizzando uno dei metodi di hello indicati di seguito, si imposta hello **profilo Log** per una sottoscrizione. definisce il tipo di hello di eventi che vengono archiviate o trasmessi Hello profilo Log e gli output di hello: hub account e/o eventi di archiviazione. Definisce inoltre i criteri di conservazione hello (numero di giorni tooretain) per gli eventi archiviati in un account di archiviazione. Se i criteri di conservazione hello sono impostato toozero, gli eventi vengono archiviati in modo permanente. In caso contrario, può essere impostato tooany valore compreso tra 1 e 2147483647. Criteri di conservazione vengono applicati al giorno, verranno eliminati in modo a hello fine di un giorno (UTC), i log da giorno hello che si trova ora oltre i criteri di conservazione hello. Ad esempio, se si dispone di un criterio di conservazione di un giorno, all'inizio di hello del giorno hello oggi hello registri hello ieri dovrebbero essere eliminati. [Fare clic qui per altre informazioni sui profili dei log](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-hello-activity-log-using-hello-portal"></a>Archivio hello Log attività tramite il portale di hello
1. Nel portale di hello, fare clic su hello **Log attività** collegamento di navigazione a sinistra di hello. Se non viene visualizzato un collegamento per hello registro attività, fare clic su hello **più servizi** collegare prima.
   
    ![Passare a pannello Log tooActivity](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. Nella parte superiore di hello del Pannello di hello, fare clic su **esportare**.
   
    ![Fare clic su pulsante Esporta hello](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. Nel pannello hello che viene visualizzato, selezionare casella hello per **esportare l'account di archiviazione tooa** e selezionare un account di archiviazione.
   
    ![Impostare un account di archiviazione](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. Dispositivo di scorrimento hello o casella di testo, di definire un numero di giorni per cui gli eventi del registro attività devono essere conservati nell'account di archiviazione. Se si preferisce toohave che persistenti i dati nell'account di archiviazione hello per un periodo illimitato, impostare questo numero toozero.
5. Fare clic su **Salva**.

## <a name="archive-hello-activity-log-via-powershell"></a>Archiviare hello Log attività tramite PowerShell
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| Proprietà | Obbligatorio | Description |
| --- | --- | --- |
| StorageAccountId |No |ID di risorsa dell'Account di archiviazione di hello toowhich log attività deve essere salvato. |
| Località |Sì |Elenco delimitato da virgole delle aree per cui si desidera toocollect attività registra eventi. È possibile visualizzare un elenco di tutte le aree [visitando la pagina](https://azure.microsoft.com/en-us/regions) o utilizzando [hello API REST di gestione di Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Sì |Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647. Un valore pari a zero vengono archiviati i log di hello illimitata (sempre). |
| Categorie |Sì |Elenco delimitato da virgole di categorie di eventi che devono essere raccolti. I valori possibili sono Write, Delete e Action. |

## <a name="archive-hello-activity-log-via-cli"></a>Archiviare i Log di attività tramite CLI hello
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| Proprietà | Obbligatorio | Description |
| --- | --- | --- |
| name |Sì |Nome del profilo di log. |
| storageId |No |ID di risorsa dell'Account di archiviazione di hello toowhich log attività deve essere salvato. |
| locations |Sì |Elenco delimitato da virgole delle aree per cui si desidera toocollect attività registra eventi. È possibile visualizzare un elenco di tutte le aree [visitando la pagina](https://azure.microsoft.com/en-us/regions) o utilizzando [hello API REST di gestione di Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Sì |Numero di giorni per cui gli eventi devono essere mantenuti, compreso tra 1 e 2147483647. Un valore pari a zero verrà archiviati i log di hello in modo indefinito (sempre). |
| Categorie |Sì |Elenco delimitato da virgole di categorie di eventi che devono essere raccolti. I valori possibili sono Write, Delete e Action. |

## <a name="storage-schema-of-hello-activity-log"></a>Schema di archiviazione di hello Log attività
Dopo aver impostato dell'archivio, è verrà creato un contenitore di archiviazione nell'account di archiviazione hello non appena si verifica un evento di registro attività. BLOB Hello all'interno del contenitore hello seguire hello stesso formato in hello Log attività e i log di diagnostica. struttura Hello di tali BLOB è:

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ID sottoscrizione}/y={anno a quattro cifre}/m={mese a due cifre}/d={giorno a due cifre}/h={ora a due cifre in formato 24 ore}/m=00/PT1H.json
> 
> 

Ad esempio, un nome BLOB potrebbe essere:

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Ciascun blob PT1H.json contiene un blob JSON di eventi che si sono verificati entro ora hello specificata nell'URL blob hello (ad esempio h = 12). Durante l'ora presenta hello, gli eventi sono accodati toohello PT1H.json file che si verificano. valore dei minuti Hello (m = 00) è sempre 00, poiché gli eventi del registro attività sono suddivisi in singoli BLOB all'ora.

Nel file PT1H.json hello, ogni evento viene archiviato nella matrice di record"hello", il formato seguente:

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
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
| category |Categoria di azione hello, ad esempio. scrittura o lettura. |
| resultType |Hello tipo di risultato hello, ad esempio. operazione riuscita, esito negativo, avvio |
| resultSignature |Dipende dal tipo di risorsa hello. |
| durationMs |Durata dell'operazione di hello in millisecondi |
| callerIpAddress |Indirizzo IP dell'utente hello che ha eseguito l'operazione di hello, attestazione UPN o attestazione nome SPN in base alla disponibilità. |
| correlationId |In genere un GUID in formato stringa hello. Gli eventi che condividono un valore correlationId appartengono toohello stessa azione. |
| identity |Blob JSON che descrive le attestazioni e l'autorizzazione di hello. |
| autorizzazione |BLOB di proprietà RBAC dell'evento hello. In genere include le proprietà di "azione", "role" e "scope" hello. |
| level |Livello dell'evento hello. Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose" |
| location |Area nella quale percorso hello durante l'esecuzione (o globale). |
| properties |Set di `<Key, Value>` coppie (ad esempio Dictionary) che descrive hello dettagli dell'evento hello. |

> [!NOTE]
> proprietà Hello e l'utilizzo di tali proprietà può variare a seconda delle risorse di hello.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione all'archivio BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [Flusso hello Log attività tooEvent hub](monitoring-stream-activity-logs-event-hubs.md)
* [Per ulteriori informazioni su hello Log attività](monitoring-overview-activity-logs.md)

