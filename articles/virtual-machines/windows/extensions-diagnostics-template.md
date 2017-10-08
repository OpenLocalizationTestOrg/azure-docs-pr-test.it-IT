---
title: aaaAdd tooan di monitoraggio e diagnostica macchina virtuale di Azure | Documenti Microsoft
description: Utilizzare un toocreate modello di gestione risorse di Azure una nuova macchina virtuale Windows con estensione diagnostica di Azure.
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Usare monitoraggio e diagnostica con una macchina virtuale Windows e modelli di Azure Resource Manager
Hello estensione diagnostica di Azure fornisce il monitoraggio di hello e funzionalità di diagnostica in un Windows basato su macchina virtuale di Azure. È possibile abilitare queste funzionalità nella macchina virtuale hello includendo l'estensione hello come parte del modello di gestione risorse di azure hello. Per altre informazioni sull'inclusione di un'estensione come parte di un modello di macchina virtuale, vedere [Creazione di modelli di Gestione risorse di Azure con le estensioni di macchina virtuale](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) . Questo articolo descrive come è possibile aggiungere il modello di macchina virtuale windows hello diagnostica Azure estensione tooa.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Aggiungere la definizione di risorsa VM hello diagnostica Azure estensione toohello
estensione di diagnostica tooenable hello nella macchina virtuale Windows è necessario estensione hello tooadd come una risorsa di macchina virtuale in hello il modello di gestione di risorse.

Per un semplice gestore di risorse basato su macchina virtuale aggiunta hello estensione configurazione toohello *risorse* matrice hello macchina virtuale: 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


Un'altra convenzione comune viene aggiunta una configurazione estensione hello al nodo di risorse hello radice del modello di hello anziché definirla in nodo risorse della macchina virtuale hello. Con questo approccio è necessario tooexplicitly specificare una relazione gerarchica tra estensione hello e macchina virtuale hello con hello *nome* e *tipo* valori. ad esempio: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

estensione Hello è sempre associata a una macchina virtuale hello, è possibile sia direttamente definire direttamente nel nodo risorse della macchina virtuale hello o definirlo a livello di base hello e utilizzare hello tooassociate gerarchica convenzione di denominazione con hello virtuale macchina.

Per le estensioni di set di scalabilità di macchine virtuali hello configurazione viene specificata in hello *extensionProfile* proprietà di hello *VirtualMachineProfile*.

Hello *publisher* proprietà con valore hello **Microsoft.Azure.Diagnostics** hello e *tipo* proprietà con valore hello **IaaSDiagnostics** identificare in modo univoco l'estensione di diagnostica Azure hello.

valore di hello Hello *nome* proprietà può essere utilizzato toorefer toohello estensione nel gruppo di risorse hello. Impostarlo in modo specifico troppo**Microsoft.Insights.VMDiagnosticsSettings** consentirà di toobe facilmente identificato da hello garantire portale Azure che hello monitoraggio grafici visualizzati correttamente in hello portale di Azure.

Hello *typeHandlerVersion* specifica versione di hello dell'estensione hello desideri toouse. Impostazione *autoUpgradeMinorVersion* la versione secondaria troppo**true** assicura che si otterranno versione secondaria più recente di hello di estensione hello è disponibile. È consigliabile impostare sempre *autoUpgradeMinorVersion* tooalways essere **true** in modo che sia sempre possibile ottenere toouse hello più recente disponibile estensione di diagnostica con tutti i bug e le nuove funzionalità di hello correzioni. 

Hello *impostazioni* elemento contiene una proprietà di configurazione per l'estensione hello che può essere impostato e leggere da estensione hello (talvolta definito tooas pubblica configurazione). Hello *xmlcfg* proprietà contiene una configurazione basata su xml per i registri di diagnostica hello, i contatori delle prestazioni e così via che verranno raccolte dall'agente di diagnostica hello. Vedere [dello Schema di configurazione di diagnostica](https://msdn.microsoft.com/library/azure/dn782207.aspx) per ulteriori informazioni sullo schema xml hello stesso. Una pratica comune è toostore hello effettivo xml di configurazione come una variabile nel modello di gestione risorse di Azure hello e quindi concatenate e base64 codificarli valore hello tooset per *xmlcfg*. Vedere la sezione hello [variabili di configurazione di diagnostica](#diagnostics-configuration-variables) toounderstand ulteriori informazioni sulla modalità toostore hello xml nelle variabili. Hello *storageAccount* proprietà specifica il nome di hello hello storage account toowhich dei dati di diagnostica verrà trasferito. 

proprietà Hello *protectedSettings* (configurazione privata tooas talvolta definito) può essere impostata ma non è possibile leggere nuovamente dopo l'impostazione. Hello natura di sola scrittura di *protectedSettings* risulta utile per l'archiviazione di segreti come chiave dell'account di archiviazione hello in cui verranno scritti i dati di diagnostica hello.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Specificare l'account di archiviazione di diagnostica come parametro
Hello diagnostica estensione json frammento di codice precedente presuppone che i due parametri *existingdiagnosticsStorageAccountName* e *existingdiagnosticsStorageResourceGroup* diagnostica hello toospecify account di archiviazione in cui verranno archiviati i dati di diagnostica. Specifica account di archiviazione di diagnostica hello come parametro, account di archiviazione di diagnostica hello toochange semplice tra ambienti diversi, ad esempio è toouse un account di archiviazione di diagnostica diversi per i test e uno per il distribuzione di produzione.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

Si tratta di best practice toospecify un account di archiviazione di diagnostica in un gruppo di risorse diverso rispetto a gruppo di risorse hello per la macchina virtuale hello. Un gruppo di risorse può essere considerato come un'unità di distribuzione con il proprio ciclo di vita toobe, una macchina virtuale può essere distribuita e ridistribuita come nuovi aggiornamenti di configurazioni vengono apportati tooit ma è opportuno archiviare i dati di diagnostica hello in hello toocontinue stesso account di archiviazione in tali distribuzioni di macchine virtuali. Con l'account di archiviazione hello in una risorsa diversa Abilita hello archiviazione account tooaccept di dati da varie distribuzioni di macchine virtuali, rendendo semplice tootroubleshoot problemi tra hello diverse versioni.

> [!NOTE]
> Se si crea un modello di macchina virtuale windows da Visual Studio potrebbe essere impostato l'account di archiviazione predefinito hello toouse hello stesso account di archiviazione in cui viene caricato hello VHD della macchina virtuale. Si tratta di toosimplify la configurazione iniziale di VM hello. È quindi consigliabile valutare nuovamente hello modello toouse un account di archiviazione diversi che può essere passato come parametro. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>variabili di configurazione diagnostica
Hello diagnostica estensione frammento di codice json precedente definisce un *accountid* toosimplify variabile recupero chiave dell'account di archiviazione per l'archiviazione di diagnostica hello hello:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Hello *xmlcfg* proprietà per l'estensione diagnostica hello è definito usando più variabili che vengono concatenate. valori Hello di queste variabili sono in xml, pertanto è necessario toobe escape correttamente quando si impostano le variabili di hello json.

di seguito Hello sono file xml di configurazione diagnostica hello che raccoglie i contatori delle prestazioni a livello di sistema standard insieme alcuni registri eventi di windows e i registri infrastruttura diagnostica. È stato sequenza di escape e formattato correttamente in modo che hello configurazione possibile direttamente incollare nella sezione variabili hello del modello. Vedere hello [dello Schema di configurazione di diagnostica](https://msdn.microsoft.com/library/azure/dn782207.aspx) per un esempio più risorse umano leggibile di hello configurazione xml.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

nodo xml di definizione Hello metriche in hello di sopra di configurazione è un elemento di configurazione importanti poiché consente di definire come i contatori delle prestazioni di hello definite in precedenza nel codice xml hello *PerformanceCounter* nodo verrà aggregato e archiviati. 

> [!IMPORTANT]
> Queste metriche unità hello avvisi nel portale di Azure hello e grafici di monitoraggio.  Hello **metriche** nodo con hello *resourceID* e **MetricAggregation** deve essere incluso nella configurazione della diagnostica hello per la macchina virtuale, se si desidera toosee hello VM dati di monitoraggio di hello portale di Azure. 
> 
> 

Hello Ecco un esempio di codice xml di hello per le definizioni delle metriche: 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Hello *resourceID* hello di macchina virtuale nella sottoscrizione che identifica in modo univoco. Assicurarsi che toouse hello subscription() e resourceGroup() funziona in modo che hello modello aggiorna automaticamente i valori in base hello sottoscrizione e della risorsa gruppo di che distribuzione.

Se si siano creando più macchine virtuali in un ciclo, si disporrà di hello toopopulate *resourceID* valore con un toocorrectly funzione copyIndex() distinguere ogni singole macchine Virtuali. Hello *xmlCfg* valore può essere aggiornato toosupport questo come segue:  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

Hello MetricAggregation valore *PT1H* e *PT1M* indicano un'aggregazione di più di un minuto e un'aggregazione di un'ora.

## <a name="wadmetrics-tables-in-storage"></a>Tabelle WADMetrics nell'archiviazione
configurazione della metrica Hello precedente genera tabelle nell'account di archiviazione di diagnostica con hello segue le convenzioni di denominazione:

* **WADMetrics** : prefisso standard per tutte le tabelle WADMetrics
* **PT1H** o **PT1M** : indica che la tabella hello contiene dati aggregati in 1 ora o 1 minuto
* **P10D** : indica la tabella hello conterrà i dati di 10 giorni da quando la tabella hello iniziato a raccogliere i dati
* **V2S** : costante di tipo stringa.
* **aaaammgg** : hello data di inizio in cui hello tabella la raccolta dei dati

Esempio: *WADMetricsPT1HP10DV2S20151108* includerà i dati aggregati delle metriche per un periodo pari a un'ora per 10 giorni a partire dall'11 nov 2015    

Ogni tabella WADMetrics conterrà hello seguenti colonne:

* **PartitionKey**: partitionkey hello viene creato in base a hello *resourceID* toouniquely valore identificare risorse VM hello. ad esempio: 002Fsubscriptions:<subscriptionID>:002FresourceGroups:002F<ResourceGroupName>:002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : formato hello segue <Descending time tick>:<Performance Counter Name>. Hello decrescente calcolo segni di graduazione time è cicli di tempo massimo meno tempo hello di inizio di hello del periodo di aggregazione hello. Ad esempio, Se il periodo di campionamento hello avviato nel novembre-10/2015 e 00:00Hrs UTC quindi hello calcolo: Ticks - (DateTime(2015,11,10,0,0,0,DateTimeKind.Utc) nuovo. Segni di graduazione). Ad esempio per hello memoria byte disponibili chiave contatori delle prestazioni hello riga avrà un aspetto: 2519551871999999999__:005CMemory:005CAvailable:0020 byte
* **CounterName** : nome hello hello del contatore delle prestazioni. Questo corrisponde hello *counterSpecifier* definito nel file di configurazione xml hello.
* **Massimo** : hello valore massimo del contatore delle prestazioni hello periodo aggregazione hello.
* **Minimo** : hello valore minimo del contatore delle prestazioni hello periodo aggregazione hello.
* **Totale** : somma hello di tutti i valori del contatore delle prestazioni hello indicato per il periodo di aggregazione hello.
* **Conteggio** : numero totale di hello di valori segnalati per contatore delle prestazioni hello.
* **Media** : hello valore Media (totale) hello del contatore delle prestazioni per il periodo di aggregazione hello.

## <a name="next-steps"></a>Passaggi successivi
* Per un modello di esempio completo di macchina virtuale Windows con estensione Diagnostica, vedere [201-vm-monitoring-diagnostics-extension](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Distribuire hello resource manager modello tramite [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [riga di comando di Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Altre informazioni sulla [Creazione di modelli di Gestione risorse di Azure](../../resource-group-authoring-templates.md)

