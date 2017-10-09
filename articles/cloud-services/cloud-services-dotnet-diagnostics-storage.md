---
title: aaaStore e visualizza i dati di diagnostica in archiviazione di Azure | Documenti Microsoft
description: Trasferire i dati di diagnostica di Azure in un account di archiviazione di Azure e visualizzarli
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>Archiviare e visualizzare i dati di diagnostica nell'account di archiviazione Azure
Dati di diagnostica non vengono archiviati in modo permanente solo se vengono trasferiti toohello emulatore di archiviazione di Microsoft Azure o archiviazione tooAzure. Una volta trasferiti nella risorsa di archiviazione, sono disponibili diversi strumenti per visualizzarli.

## <a name="specify-a-storage-account"></a>Specificare un account di archiviazione
Specificare hello account di archiviazione che si desidera toouse nel file ServiceConfiguration. cscfg hello. informazioni sull'account Hello è definiti come una stringa di connessione in un'impostazione di configurazione. Hello riportato di seguito stringa di connessione predefinita hello creato per un nuovo progetto di servizio Cloud in Visual Studio:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

È possibile modificare queste informazioni di account di tooprovide stringa di connessione per un account di archiviazione di Azure.

In base al tipo di dati di diagnostica che si desidera raccogliere hello diagnostica Azure Usa servizio Blob hello o del servizio tabelle hello. Hello nella tabella seguente mostra le origini dati hello che vengono rese persistenti e il relativo formato.

| Origine dati | Formato di archiviazione |
| --- | --- |
| Log di Azure |Tabella |
| Log di IIS 7.0 |BLOB |
| Log dell'infrastruttura Diagnostica di Azure |Tabella |
| Log di analisi delle richieste non riuscite |BLOB |
| Registri eventi di Windows |Tabella |
| Contatori delle prestazioni |Tabella |
| Dump di arresto anomalo del sistema |BLOB |
| Log degli errori personalizzati |BLOB |

## <a name="transfer-diagnostic-data"></a>Trasferire i dati di diagnostica
Per SDK 2.5 e versioni successive, dati di diagnostica di hello richiesta tootransfer possono verificarsi tramite file di configurazione hello. È possibile trasferire dati di diagnostica a intervalli pianificati, come specificato nella configurazione di hello.

Per SDK 2.4 e precedente è possibile richiedere dati di diagnostica hello tootransfer tramite file di configurazione hello anche a livello di codice. approccio a livello di codice Hello consente trasferimenti su richiesta toodo.

> [!IMPORTANT]
> Quando si trasferiscono dati di diagnostica tooan account di archiviazione di Azure, si devono sostenere i costi per le risorse di archiviazione hello che utilizza i dati di diagnostica.
> 
> 

## <a name="store-diagnostic-data"></a>Archiviare i dati di diagnostica
Dati di log vengono archiviati nell'archiviazione Blob o tabella con hello seguenti nomi:

**Tabelle**

* **WadLogsTable** - log scritto in codice utilizzando il listener di traccia hello.
* **WADDiagnosticInfrastructureLogsTable** : monitor di diagnostica e modifiche di configurazione.
* **WADDirectoriesTable** : directory esegue il monitoraggio di tale monitor di diagnostica hello.  Sono inclusi i log di IIS, i log delle richieste non riuscite di IIS e le directory personalizzate.  percorso Hello hello blob del file di log viene specificato nel campo Container hello e nome hello del blob hello nel campo RelativePath hello.  campo AbsolutePath Hello indica hello percorso e il nome del file hello esistente nella macchina virtuale di Azure hello.
* **WADPerformanceCountersTable** : contatori delle prestazioni.
* **WADWindowsEventLogsTable** : registri eventi di Windows.

**BLOB**

* **wad-control-container** – (solo per SDK 2.4 e precedenti) contiene file di configurazione XML hello che controlla hello diagnostica Windows Azure.
* **wad-iis-failedreqlogfiles** : contiene informazioni provenienti dai log delle richieste non riuscite di IIS.
* **wad-iis-logfiles** : contiene informazioni sui log di IIS.
* **"custom"** : contenitore personalizzato basato sulle directory monitorate da Monitoraggio diagnostica hello di configurazione.  nome Hello di questo contenitore blob verrà specificato in WADDirectoriesTable.

## <a name="tools-tooview-diagnostic-data"></a>Dati di diagnostica tooview degli strumenti
Sono inoltre numerosi strumenti dati hello tooview disponibile dopo essere stato trasferito toostorage. ad esempio:

* Esplora server in Visual Studio - se è stato installato hello Azure Tools per Microsoft Visual Studio, è possibile utilizzare il nodo di archiviazione di Azure hello in Esplora Server tooview-blob e tabelle dati di sola lettura dagli account di archiviazione di Azure. È possibile visualizzare i dati dall'account dell'emulatore di archiviazione locale e anche dagli account di archiviazione creati per Azure. Per altre informazioni, vedere [Esplorazione e gestione delle risorse di archiviazione con Esplora server](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'applicazione autonoma che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, OSX e Linux.
* [Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) include Azure Diagnostics Manager che consente di tooview, scaricare e gestire dati di diagnostica hello raccolti dalle applicazioni hello in esecuzione in Azure.

## <a name="next-steps"></a>Passaggi successivi
[Tracciare il flusso di hello in un'applicazione di servizi Cloud con diagnostica di Azure](cloud-services-dotnet-diagnostics-trace-flow.md)

