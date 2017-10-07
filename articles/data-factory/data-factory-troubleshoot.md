---
title: problemi di Azure Data Factory aaaTroubleshoot
description: Informazioni su come tootroubleshoot problemi con Data Factory di Azure.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a>Risolvere i problemi di Data factory
Questo articolo contiene suggerimenti per la risoluzione dei problemi correlati all'uso di Azure Data Factory. In questo articolo non sono elencati tutti i possibili problemi di hello quando si utilizza servizio hello, ma comprende alcuni problemi e suggerimenti sulla risoluzione dei problemi generali.   

## <a name="troubleshooting-tips"></a>Suggerimenti per la risoluzione dei problemi
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>Errore: hello sottoscrizione non è registrato toouse dello spazio dei nomi 'Microsoft. DataFactory'
Se si riceve questo errore, provider di risorse hello Azure Data Factory non è stato registrato nel computer. Hello seguenti:

1. Avviare Azure PowerShell.
2. Accedi tooyour account Azure tramite hello comando seguente.

    ```powershell
    Login-AzureRmAccount
    ```
3. Eseguire i seguenti provider di Azure Data Factory di comandi tooregister hello hello.

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Problema: errore di mancata autorizzazione quando si esegue un cmdlet di Data factory
Probabilmente non utilizza destra hello account Azure o una sottoscrizione con hello Azure PowerShell. Utilizzare hello cmdlet tooselect hello destra toouse di account e la sottoscrizione Azure con hello Azure PowerShell seguente.

1. Account di accesso-AzureRmAccount - ID utente di utilizzare hello e una password
2. Get-AzureRmSubscription - Visualizza tutte le sottoscrizioni per account hello di hello.
3. Selezionare AzureRmSubscription &lt;nome sottoscrizione&gt; -selezionare hello destra sottoscrizione. Utilizzare hello stesso che si utilizza una data factory toocreate su hello portale di Azure.

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>Problema: Non toolaunch installazione di Express Data Management Gateway dal portale di Azure
installazione di Express Hello per Gateway di gestione dati hello richiede Internet Explorer o un browser compatibile Microsoft ClickOnce. Se l'installazione di Express hello ha esito negativo toostart, effettuare uno dei seguenti hello:

* Usare Internet Explorer o un Web browser compatibile con Microsoft ClickOnce.

    Se si utilizza Chrome, andare toohello [archivio web Chrome](https://chrome.google.com/webstore/), eseguire la ricerca con la parola chiave "ClickOnce", scegliere una delle estensioni di ClickOnce hello e installarlo.

    Hello stesso per Firefox (Installa componente aggiuntivo). Fare clic sul pulsante Apri Menu sulla barra degli strumenti hello (tre linee orizzontali nell'angolo superiore destro hello), fare clic su componenti aggiuntivi, eseguire la ricerca con la parola chiave "ClickOnce", scegliere una delle estensioni di ClickOnce hello e installarlo.
* Hello utilizzare **l'installazione manuale** collegamento visualizzato in hello stesso pannello nel portale di hello. Utilizzare questo file di installazione toodownload approccio ed eseguirlo manualmente. Dopo l'installazione di hello ha esito positivo, vengono visualizzati la finestra di dialogo di configurazione di Gateway di gestione dati hello. Hello copia **chiave** dalla schermata di portale hello e utilizzare in hello configuration manager toomanually registrare gateway hello hello servizio.  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>Problema: Non tooconnect tooon locale SQL Server
Avviare **Gestione configurazione di Gateway di gestione di dati** hello computer gateway e utilizzare hello **Troubleshooting** scheda tootest hello connessione tooSQL Server dal computer del gateway hello. Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Problema: le sezioni di input rimangono nello stato Waiting
le sezioni Hello potrebbe essere in **in attesa** dello stato a causa di motivi toovarious. Uno dei motivi comuni hello è tale hello **esterno** non è impostata troppo**true**. Qualsiasi set di dati che è l'ambito di prodotti hello all'esterno di Azure Data Factory deve essere contrassegnato con **esterno** proprietà. Questa proprietà indica che i dati di hello esterni e non è supportato da qualsiasi pipeline all'interno di data factory di hello. le sezioni di dati Hello sono contrassegnate come **pronto** quando dati hello sono disponibili nell'archivio rispettivi hello.

Vedere l'esempio per l'utilizzo di hello di hello seguente hello **esterno** proprietà. È possibile specificare facoltativamente **externalData*** quando si imposta tootrue esterno.

Per altre informazioni su questa proprietà, vedere [Set di dati in Azure Data Factory](data-factory-create-datasets.md) .

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

tooresolve hello errore, aggiungere hello **esterno** proprietà e hello facoltativo **externalData** sezione Definizione JSON toohello della tabella di input hello e ricreare la tabella hello.

### <a name="problem-hybrid-copy-operation-fails"></a>Problema: l'operazione di copia ibrida non riesce
Vedere [risolvere i problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) per passaggi tootroubleshoot problemi con la copia da e verso un dati locali archiviano utilizzando hello Gateway di gestione dati.

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Problema: non è possibile eseguire il provisioning di HDInsight su richiesta
Quando si utilizza un servizio collegato di tipo HDInsightOnDemand, è necessario toospecify un linkedServiceName che punta tooan archiviazione Blob di Azure. Servizio Data Factory viene utilizzata questa archiviazione toostore registri e i file di supporto per il cluster HDInsight su richiesta.  In alcuni casi il provisioning di un cluster di HDInsight su richiesta non riesce con hello errore seguente:

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Questo errore indica generalmente che il percorso di hello hello dell'account di archiviazione specificato in linkedServiceName hello non hello posizione in cui avviene il provisioning di HDInsight hello stesso data center. Esempio: se la data factory negli Stati Uniti occidentali e hello archiviazione di Azure in Stati Uniti orientali, hello su richiesta ha esito negativo provisioning negli Stati Uniti occidentali.

È anche disponibile una seconda proprietà JSON additionalLinkedServiceNames in cui è possibile specificare account di archiviazione aggiuntivi in HDInsight su richiesta. Tali account di archiviazione collegato aggiuntivi hello stessa località del cluster HDInsight hello o ha esito negativo con hello deve essere lo stesso errore.

### <a name="problem-custom-net-activity-fails"></a>Problema: l'attività .NET personalizzata non riesce
Per una procedura dettagliata, vedere la sezione [Eseguire il debug della pipeline](data-factory-use-custom-activities.md#troubleshoot-failures) .

## <a name="use-azure-portal-tootroubleshoot"></a>Utilizzare tootroubleshoot portale di Azure
### <a name="using-portal-blades"></a>Uso dei pannelli del portale
Per una procedura dettagliata, vedere la sezione [Monitorare la pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .

### <a name="using-monitor-and-manage-app"></a>Uso dell'app di monitoraggio e gestione
Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md) .

## <a name="use-azure-powershell-tootroubleshoot"></a>Usare Azure PowerShell tootroubleshoot
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>Usare Azure PowerShell tootroubleshoot un errore
Per informazioni su come monitorare le pipeline di Data Factory con Azure PowerShell, vedere la sezione [Monitorare la pipeline](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) .

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
