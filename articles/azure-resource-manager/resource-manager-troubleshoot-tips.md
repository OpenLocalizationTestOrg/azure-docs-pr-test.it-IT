---
title: errori di distribuzione di Azure aaaUnderstand | Documenti Microsoft
description: Viene descritto come toolearn sugli errori di distribuzione di Azure.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Errore di distribuzione, distribuzione di azure, distribuire tooazure
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a>Informazioni sugli errori di distribuzione di Azure
In questo argomento vengono descritti gli errori di distribuzione e le modalità per reperire altre informazioni sull'errore. Per errori di distribuzione toocommon risoluzioni, vedere [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="two-types-of-errors"></a>Due tipi di errori
I possibili errori sono di due tipi:

* errori di convalida
* errori di distribuzione

Hello seguente immagine mostra il registro attività hello per una sottoscrizione. Rappresenta due distribuzioni. In una distribuzione modello hello convalida non riuscita (**convalida**) e non è stata eseguita. In hello altra distribuzione, il modello di hello ha superato la convalida, ma non riuscita durante la creazione di risorse hello (**scrivere distribuzioni**). 

![mostra codice di errore](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

Gli errori di convalida sono causati da scenari già determinati prima della distribuzione. Errori di sintassi includono nel modello o durante il tentativo risorse toodeploy superano il quote della sottoscrizione. Errori di distribuzione sono causati da condizioni che si verificano durante il processo di distribuzione hello. È incluso il tentativo di tooaccess una risorsa che viene distribuita in parallelo.

Entrambi i tipi di errori restituito un codice di errore di utilizzare tootroubleshoot hello distribuzione. Entrambi i tipi di errori vengono visualizzati in hello [log attività](resource-group-audit.md). Tuttavia, gli errori di convalida non vengono visualizzati nella cronologia di distribuzione perché la distribuzione di hello mai avviata.

## <a name="determine-error-code"></a>Determinare il codice di errore

Per informazioni sull'errore esaminando il messaggio di errore hello e codice di errore hello. Hello [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md) articolo vengono elencati le risoluzioni da codice di errore. Questo argomento viene illustrato come toouse hello codice di errore hello toodiscover portale Azure.

### <a name="validation-errors"></a>Errori di convalida

Durante la distribuzione tramite il portale di hello, viene visualizzato un errore di convalida dopo l'invio dei valori.

![vista dell'errore di convalida nel portale](./media/resource-manager-troubleshoot-tips/validation-error.png)

Selezionare il messaggio hello per altri dettagli. Nella seguente immagine di hello, vedrai un **InvalidTemplateDeployment** errore e un messaggio che indica un criterio di distribuzione sia bloccato.

![visualizzare le informazioni di convalida](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a>Errori di distribuzione

Quando l'operazione di hello supera la convalida, ma non riesce durante la distribuzione, viene visualizzato l'errore di hello nelle notifiche hello. Selezionare hello notifica.

![Notifica di errore](./media/resource-manager-troubleshoot-tips/notification.png)

Visualizzare ulteriori dettagli sulla distribuzione di hello. Selezionare hello opzione toofind ulteriori informazioni sull'errore hello.

![distribuzione non riuscita](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

Vedere i codici di errore e messaggi di errore hello. Si noti che sono presenti due codici di errore. Hello primo codice di errore (**DeploymentFailed**) è un errore generale che non fornisce i dettagli di hello è necessario errore hello toosolve. Hello secondo codice di errore (**StorageAccountNotFound**) fornisce i dettagli di hello è necessario. 

![dettagli dell'errore](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a>Abilitazione della registrazione di debug
Talvolta è necessario ulteriori informazioni su hello richiesta e risposta toodiscover la causa dell'errore. Con PowerShell o l'interfaccia della riga di comando di Azure è possibile richiedere la registrazione di informazioni aggiuntive durante la distribuzione.

- PowerShell

   In PowerShell, impostare hello **DeploymentDebugLogLevel** parametro tooAll, ResponseContent o RequestContent.

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   Esaminare il contenuto di richiesta hello con hello seguente cmdlet:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   In alternativa, hello risposta contenuto con:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   Queste informazioni consentono di determinare se un valore nel modello di hello è impostato in modo non corretto.

- Interfaccia della riga di comando di Azure

   Esaminare le operazioni di distribuzione hello con hello comando seguente:

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- Modello annidato

   informazioni di debug toolog per un modello annidato, utilizzare hello **debugSetting** elemento.

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a>Creare un modello per la risoluzione dei problemi
In alcuni casi, hello tootroubleshoot modo più semplice del modello è tootest parti di esso. È possibile creare un modello semplificato che consente di toofocus parte hello che si ritiene che sta provocando errore hello. Si supponga, ad esempio, di ricevere un errore quando si fa riferimento a una risorsa. Anziché gestire un intero modello, creare un modello che restituisce parte di hello che potrebbe causare il problema. Consentono di determinare se si sta passando parametri corretti hello, correttamente, l'utilizzo delle funzioni di modello e recupero hello risorsa desiderato.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

In alternativa, si supponga che si rilevano errori di distribuzione che si ritengono correlati tooincorrectly impostare le dipendenze. Testare il modello suddividendolo in modelli semplificati. Creare innanzitutto un modello che distribuisce una sola risorsa (ad esempio SQL Server). Quando si è certi che la risorsa sia definita correttamente, aggiungere una risorsa che dipende da essa (ad esempio un database SQL). Una volta definite correttamente queste due risorse, aggiungere altre risorse che dipendono da esse (ad esempio criteri di controllo). Tra ogni distribuzione di test, eliminare hello gruppo toomake che è adeguata test hello dipendenze delle risorse. 

## <a name="check-deployment-sequence"></a>Controllare la sequenza di distribuzione

Molti errori di distribuzione si verificano quando le risorse vengono distribuite secondo una sequenza imprevista. Questi errori vengono generati quando le dipendenze non sono impostate correttamente. Quando manca una dipendenza necessaria, una risorsa tenta toouse che un valore per un'altra risorsa mentre altri hello non esiste ancora. e viene visualizzato un errore che indica che non è stata trovata una risorsa. Questo tipo di errore possono verificarsi a intermittenza perché hello tempo di distribuzione per ogni risorsa può variare. Ad esempio, il primo toodeploy tentativo le risorse ha esito positivo perché una risorsa necessaria viene completato in modo casuale in tempo. Tuttavia, il secondo tentativo ha esito negativo perché hello necessarie risorse non è stata completata nel tempo. 

Tuttavia, si desidera tooavoid impostazione delle dipendenze che non è necessari. Se si dispone di dipendenze non necessari, si prolungare durata hello della distribuzione hello impedendo le risorse che non sono interdipendenti vengano distribuiti in parallelo. Inoltre, è possibile creare dipendenze circolari che bloccano la distribuzione di hello. Hello [riferimento](resource-group-template-functions-resource.md#reference) funzione crea una relazione implicita sulla risorsa a cui fa riferimento hello, quando tale risorsa è distribuita in hello stesso modello. Pertanto, è possibile altre dipendenze di dipendenze di hello specificate in hello **dependsOn** proprietà. Hello [resourceId](resource-group-template-functions-resource.md#resourceid) funzione non creare una relazione implicita o verificare l'esistenza di risorse hello.

Quando si verificano problemi di dipendenza, è necessario comprendere toogain ordine hello di distribuzione di risorse. ordine di hello tooview di operazioni di distribuzione:

1. Selezionare la cronologia della distribuzione hello per il gruppo di risorse.

   ![selezionare la cronologia delle distribuzioni](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. Selezionare una distribuzione dalla cronologia hello e **eventi**.

   ![selezionare gli eventi di distribuzione](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. Esaminare la sequenza hello di eventi per ogni risorsa. Si paga stato toohello attenzione di ogni operazione. Ad esempio, hello immagine seguente mostra tre degli account di archiviazione distribuito in parallelo. Si noti che hello tre account di archiviazione vengono avviate in hello contemporaneamente.

   ![distribuzione parallela](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   immagine successiva Hello mostra tre account di archiviazione che non vengono distribuiti in parallelo. account di archiviazione secondo Hello dipende dal primo account di archiviazione hello e account di archiviazione terzo hello dipende dall'account di archiviazione secondo hello. Pertanto, il primo account di archiviazione hello è avviato, accettati e completata prima che venga avviata hello accanto.

   ![distribuzione sequenziale](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

Anche per scenari più complessi, è possibile utilizzare hello stessa tecnica toodiscover quando la distribuzione è avviata e completata per ogni risorsa. Se la sequenza hello è diversa da quello previsto, esaminare il toosee gli eventi di distribuzione. In questo caso, valutare di nuovo le dipendenze di hello per questa risorsa.

Resource Manager identifica le dipendenze circolari durante la convalida del modello. Restituisce quindi un messaggio di errore che indica specificamente la presenza di una dipendenza circolare. toosolve una dipendenza circolare:

1. Nel modello, trovare la risorsa hello identificata una dipendenza circolare hello. 
2. Per tale risorsa, esaminare hello **dependsOn** proprietà e gli utilizzi di hello **riferimento** toosee le risorse dipende dalla funzione. 
3. Esaminare tali toosee risorse quali risorse cui dipendono. Seguire le dipendenze di hello finché non si nota una risorsa che dipende dalla risorsa originale hello.
5. Per le risorse hello coinvolti in una dipendenza circolare hello, esaminare attentamente tutte le occorrenze di hello **dependsOn** tooidentify proprietà tutte le dipendenze che non sono necessari. Rimuovere tali dipendenze. Se non si è certi che una dipendenza sia necessaria, provare a rimuoverla. 
6. Ridistribuire il modello di hello.

Rimuovere i valori dal hello **dependsOn** proprietà può causare errori quando si distribuisce il modello di hello. Se si verifica un errore, aggiungere una dipendenza hello nel modello di hello. 

Se tale approccio non consente di risolvere una dipendenza circolare hello, è consigliabile spostare parte della logica di distribuzione in risorse figlio (ad esempio estensioni o le impostazioni di configurazione). Dopo le risorse di hello coinvolte in una dipendenza circolare hello, configurare tali toodeploy risorse figlio. Si supponga, ad esempio, si distribuiscono due macchine virtuali, ma è necessario impostare proprietà su ciascuna di esse che fanno riferimento altri toohello. È possibile distribuirli in hello seguente ordine:

1. VM 1
2. VM 2
3. L'estensione in VM 1 dipende da VM 1 e VM 2. estensione Hello imposta valori per vm1 ottenute da vm2.
4. L'estensione in VM 2 dipende da VM 1 e VM 2. estensione Hello imposta valori per vm2 ottenute da vm1.

Hello stesso approccio funziona per le applicazioni di servizio App. Provare a spostare i valori di configurazione in una risorsa figlio della risorsa app hello. È possibile distribuire due App web in hello seguente ordine:

1. App Web 1
2. App Web 2
3. La configurazione per App Web 1 dipende da App Web 1 e App Web 2. Contiene impostazioni dell'app con valori di App Web 2.
4. La configurazione per App Web 2 dipende da App Web 1 e App Web 2. Contiene impostazioni dell'app con valori di App Web 1.


## <a name="next-steps"></a>Passaggi successivi
* Per errori di distribuzione toocommon risoluzioni, vedere [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn sul controllo delle azioni, vedere [controllare le operazioni con Gestione risorse di](resource-group-audit.md).
* toolearn sugli errori di hello toodetermine azioni durante la distribuzione, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).
