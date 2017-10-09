---
title: "set di scalabilità aaaAutomatic scalabilità e la macchina virtuale | Documenti Microsoft"
description: "Informazioni sull'utilizzo di diagnostica e le macchine virtuali di scalabilità automatica risorse tooautomatically scala in un set di scalabilità."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>Come il ridimensionamento automatico toouse e set di scalabilità di macchine virtuali
Il ridimensionamento automatico delle macchine virtuali in un set di scalabilità è la creazione di hello o l'eliminazione delle macchine in hello impostato come necessarie toomatch requisiti relativi alle prestazioni. Man mano che aumenta il volume di hello di lavoro, un'applicazione può richiedere risorse aggiuntive tooenable è tooeffectively eseguire attività.

Il ridimensionamento automatico è un processo automatico che semplifica il sovraccarico di gestione. Riducendo il sovraccarico non necessario toocontinually monitoraggio delle prestazioni di sistema o decidere come toomanage risorse. Il ridimensionamento è un processo elastico. Altre risorse possono essere aggiunti come hello carico aumenta. E come richiesta diminuisce, le risorse possono essere rimossi toominimize costi e mantenere livelli di prestazioni.

Impostare la scalabilità automatica su una scala impostata per l'utilizzo di un modello Gestione risorse di Azure, Azure PowerShell, CLI di Azure o hello portale di Azure.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>Configurare il ridimensionamento usando modelli di Resource Manager
Invece di distribuire e gestire separatamente ogni risorsa dell'applicazione, usare un modello che distribuisce tutte le risorse in un'unica operazione coordinata. Nel modello di hello, le risorse dell'applicazione sono definite e vengono specificati i parametri di distribuzione per ambienti diversi. modello Hello è costituito da JSON e le espressioni che è possibile utilizzare valori tooconstruct per la distribuzione. toolearn esaminare più, [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Nel modello di hello, specificare l'elemento capacità hello:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

Capacità identifica il numero di hello di macchine virtuali nel set di hello. È possibile modificare manualmente la capacità di hello tramite la distribuzione di un modello con un valore diverso. Se si distribuisce una capacità di hello modifica tooonly modello, è possibile includere solo elemento SKU hello con capacità di hello aggiornato.

Hello capacità del set di scala possono essere adattate automaticamente usando una combinazione di hello **autoscaleSettings** risorsa e hello estensione di diagnostica.

### <a name="configure-hello-azure-diagnostics-extension"></a>Configurare l'estensione diagnostica di Azure hello
La scalabilità automatica può essere eseguita solo se la raccolta di metriche ha esito positivo in ogni macchina virtuale nel set di scalabilità hello. Hello estensione diagnostica di Azure offre funzionalità di monitoraggio e diagnostica di hello soddisfa le esigenze di raccolta metriche hello della risorsa di scalabilità automatica hello. È possibile installare l'estensione hello come parte del modello di gestione risorse di hello.

Questo esempio mostra le variabili di hello utilizzate nell'estensione di diagnostica di hello modello tooconfigure hello:

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

I parametri vengono forniti quando viene distribuito il modello di hello. In questo esempio, il nome di hello dell'account di archiviazione hello (dove vengono archiviati dati) e hello vengono forniti nome del set di scalabilità hello (in cui vengono raccolti dati). Anche in questo esempio di Windows Server, verrà raccolti solo contatore delle prestazioni conteggio Thread hello. Tutti hello contatori delle prestazioni disponibili in Windows o Linux possono essere utilizzati toocollect informazioni di diagnostica e possono essere inclusi nella configurazione dell'estensione hello.

Questo esempio mostra la definizione hello dell'estensione hello nel modello hello:

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

Quando viene eseguita l'estensione di diagnostica hello, dati hello archiviati e raccolti in una tabella, nell'account di archiviazione hello specificato. In hello **WADPerformanceCounters** tabella, è possibile trovare i dati raccolti hello:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>La configurazione di risorsa autoScaleSettings hello
risorsa autoscaleSettings Hello utilizza informazioni hello hello diagnostica estensione toodecide se tooincrease o diminuire il numero di hello delle macchine virtuali in scala di hello impostata.

Questo esempio mostra la configurazione hello della risorsa hello nel modello hello:

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

Nell'esempio hello sopra, vengono create due regole per la definizione di azioni di scalabilità automatica hello. prima regola Hello definisce l'azione di scalabilità orizzontale hello e regola secondo hello hello scala-azione. Questi valori sono disponibili nelle regole di hello:

| Regola | Descrizione |
| ---- | ----------- |
| metricName        | Questo valore è hello stesso come contatore delle prestazioni hello che siano definiti nella variabile wadperfcounter hello per l'estensione diagnostica hello. Nell'esempio hello sopra, il contatore di conteggio Thread hello è utilizzato.    |
| metricResourceUri | Questo valore è l'identificatore di risorsa hello del set di scalabilità della macchina virtuale hello. Questo identificatore contiene nome hello hello del gruppo di risorse, hello nome del provider di risorse hello e nome hello di hello scala set tooscale. |
| timeGrain         | Questo valore è la granularità hello di metriche di hello che vengono raccolti. In hello sopra riportato, i dati vengono raccolti in un intervallo di un minuto. Questo valore viene usato con timeWindow. |
| statistic         | Questo valore determina come le metriche hello vengono combinati tooaccommodate hello azione di scalabilità automatica. Hello i valori possibili sono: Media, Min, Max. |
| timeWindow        | Questo valore è hello intervallo di tempo in cui vengono raccolti i dati dell'istanza. Deve essere compreso tra 5 minuti e 12 ore. |
| timeAggregation   | Questo valore determina la modalità hello i dati raccolti devono essere combinati nel tempo. valore predefinito di Hello è Media. Hello i valori possibili sono: Media, minimo, massimo, ultimo, totale, conteggio. |
| operator          | Questo valore è l'operatore hello toocompare utilizzati hello metrica hello e dati soglia. Hello i valori possibili sono: uguale a, diverso da, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual. |
| threshold         | Questo valore è hello che attiva l'azione di scalabilità hello. Essere tooprovide che una differenza tra valori di soglia hello per hello sufficiente **scalabilità orizzontale** e **scala aggiuntivo** azioni. Se si impostano hello stessi valori per entrambe le azioni, il sistema hello prevede costante evoluzione, che ne impedisce l'implementazione di un'azione di scalabilità. Ad esempio, l'impostazione entrambi too600 i thread nel precedente esempio hello non funziona. |
| direction         | Questo valore determina l'azione eseguita quando viene raggiunto il valore di soglia hello hello. i valori possibili di Hello sono aumentano o diminuiscono. |
| type              | Questo valore è di tipo hello di azione che deve essere eseguita e deve essere impostato tooChangeCount. |
| value             | Questo valore è il numero di hello di macchine virtuali che vengono aggiunti tooor rimosso dal set di scalabilità hello. Questo valore deve essere uguale o maggiore di 1. |
| cooldown          | Questo valore è quantità hello di toowait tempo dall'ultima azione di scalabilità hello prima che si verifichi l'azione successiva hello. Questo valore deve essere compreso tra un minuto e una settimana. |

A seconda del contatore delle prestazioni di hello, si utilizza, alcuni degli elementi di hello nella configurazione del modello hello vengono utilizzati in modo diverso. In hello sopra riportato, contatore delle prestazioni hello è il conteggio Thread, il valore di soglia hello è 650 per un'azione di scalabilità orizzontale e il valore di soglia hello è 550 per azione di scalabilità hello. Se si utilizza un contatore, ad esempio % tempo processore, il valore di soglia hello è toohello percentuale di utilizzo della CPU che determinano un'azione di scalabilità.

Quando viene attivata un'azione di scalabilità, ad esempio un carico elevato, hello del set di hello viene aumentata in base a valore hello nel modello di hello. Ad esempio, in una scala imposta in capacità hello è impostata too3 e hello scala azione è impostato too1:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

Hello quando la corrente parte delle thread medio hello degli cause carico conteggio toogo superiore alla soglia hello di 650:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

Oggetto **scalabilità orizzontale** viene attivata l'azione che causa hello capacità di hello set toobe incrementato di uno:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

il risultato di Hello è che una macchina virtuale viene aggiunto il set di scalabilità toohello:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

Dopo un periodo di raffreddamento di cinque minuti, se il numero medio di hello dei thread nelle macchine hello rimane 600, un altro computer viene aggiunto toohello set. Se il numero di thread medio hello resta di sotto di 550, capacità hello del set di scalabilità hello viene ridotto di uno e un computer viene rimosso dal set di hello.

## <a name="set-up-scaling-using-azure-powershell"></a>Impostare la scalabilità con Azure PowerShell

esaminare toosee esempi dell'utilizzo di PowerShell tooset backup il ridimensionamento automatico [Azure monitoraggio PowerShell quick start esempi](../monitoring-and-diagnostics/insights-powershell-samples.md).

## <a name="set-up-scaling-using-azure-cli"></a>Impostare la scalabilità con l'interfaccia della riga di comando di Azure

esaminare toosee esempi dell'utilizzo di tooset CLI di Azure backup per la scalabilità automatica, [CLI multipiattaforma di Azure monitoraggio rapido avviare esempi](../monitoring-and-diagnostics/insights-cli-samples.md).

## <a name="set-up-scaling-using-hello-azure-portal"></a>Impostare la scalabilità utilizzando hello portale di Azure

un esempio di utilizzo toosee hello tooset portale Azure backup per la scalabilità automatica, cercare in [creare un hello portale di Azure utilizzando Set di scalabilità macchina virtuale](virtual-machine-scale-sets-portal-create.md).

## <a name="investigate-scaling-actions"></a>Analisi delle azioni di ridimensionamento

* **Portale di Azure**  
Attualmente, è possibile ottenere una quantità limitata di informazioni tramite il portale di hello.

* **Esplora risorse di Azure**  
Questo strumento è hello migliore per l'esplorazione dello stato corrente di hello del set di scalabilità. Seguire questo percorso e dovrebbe essere vista istanza hello della scala hello imposta creato:  
**Subscriptions > {sottoscrizione dell'utente} > resourceGroups > {gruppo di risorse dell'utente} > providers > Microsoft.Compute > virtualMachineScaleSets > {set di scalabilità dell'utente} > virtualMachines**

* **Azure PowerShell**  
Utilizzare questo comando tooget alcune informazioni:

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Connessione macchina virtuale di toohello jumpbox esattamente come si farebbe qualsiasi altro computer e quindi è possibile accedere in remoto hello le macchine virtuali in hello scala set toomonitor singoli processi.

## <a name="next-steps"></a>Passaggi successivi
* Esaminare [ridimensionare automaticamente le macchine in un Set di scalabilità della macchina virtuale](virtual-machine-scale-sets-windows-autoscale.md) toosee un esempio di come toocreate imposta una scala con il ridimensionamento automatico configurato.

* Per alcuni esempi delle funzionalità di monitoraggio in Monitoraggio di Azure, vedere [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md) (Esempi di avvio rapido di PowerShell per Monitoraggio di Azure).

* Informazioni sulle funzionalità di notifica di [utilizzare scalabilità automatica azioni toosend posta elettronica e ai webhook notifiche di avviso in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).

* Informazioni su come troppo[i log di controllo di utilizzare le notifiche degli avvisi di posta elettronica e ai webhook toosend in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* Informazioni sugli [scenari di scalabilità automatica avanzata](virtual-machine-scale-sets-advanced-autoscale.md).
