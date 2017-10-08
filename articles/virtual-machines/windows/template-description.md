---
title: aaaVirtual macchine in un modello di gestione risorse di Azure | Microsoft Azure
description: "Altre informazioni su come risorsa di macchina virtuale hello è definito in un modello di gestione risorse di Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a>Macchine virtuali in un modello di Azure Resource Manager

In questo articolo descrive alcuni aspetti di un modello di gestione risorse di Azure che si applicano toovirtual macchine. L'articolo descrive un modello completo per la creazione di una macchina virtuale; a tale scopo sono necessarie definizioni di risorse per gli account di archiviazione, le interfacce di rete, gli indirizzi IP pubblici e le reti virtuali. Per ulteriori informazioni su come queste risorse possono essere definite insieme, vedere hello [procedura dettagliata di modello di gestione risorse](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Esistono molti [modelli raccolta hello](https://azure.microsoft.com/documentation/templates/?term=VM) che includono una risorsa di macchina virtuale hello. Di seguito sono descritti solo alcuni elementi che possono essere inclusi in un modello.

Questo esempio mostra una sezione di risorse tipica di un modello per la creazione di un numero specificato di VM:

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
>Questo esempio si basa su un account di archiviazione creato in precedenza. È possibile creare account di archiviazione hello mediante la distribuzione da modello hello. esempio Hello si basa inoltre su un'interfaccia di rete e le risorse dipendenti che deve essere definite nel modello di hello. Queste risorse non vengono visualizzate nell'esempio hello.
>
>

## <a name="api-version"></a>Versione dell'API

Quando si distribuiscono un modello di risorse, è possibile toospecify una versione di hello API toouse. esempio Hello Mostra una risorsa di macchina virtuale hello tramite questo elemento apiVersion:

```
"apiVersion": "2016-04-30-preview",
```

versione di Hello di API specificate nel modello di hello interessa le proprietà che è possibile definire nel modello di hello. In generale, selezionare versione API più recente di hello durante la creazione di modelli. Per i modelli esistenti, è possibile decidere se si desidera toocontinue utilizzando una versione precedente di API o aggiornare il modello per hello più recente versione tootake le nuove funzionalità.

Utilizzare queste opportunità per ottenere le versioni dell'API più recente hello:

- API REST: [Elencare tutti i provider di risorse](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)
- PowerShell: [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)
- Interfaccia della riga di comando di Azure 2.0: [az provider show](https://docs.microsoft.com/cli/azure/provider#show)

## <a name="parameters-and-variables"></a>Parametri e variabili

[I parametri](../../resource-group-authoring-templates.md) semplificano automaticamente toospecify valori per il modello di hello al momento dell'esecuzione. In questa sezione parametri viene utilizzata nell'esempio hello:

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

Quando si distribuisce il modello di esempio hello, immettere valori per nome hello e la password dell'account amministratore hello in ogni macchina virtuale e hello il numero di macchine virtuali toocreate. È possibile hello specificando i valori dei parametri in un file distinto che viene gestito con il modello di hello o fornire valori quando richiesto.

[Le variabili](../../resource-group-authoring-templates.md) semplificano automaticamente tooset i valori nel modello di hello utilizzate ripetutamente in corso o che possono cambiare nel tempo. In questa sezione variabili viene utilizzata nell'esempio hello:

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

Quando si distribuisce il modello di esempio hello, vengono utilizzati i valori delle variabili per nome hello e l'identificatore dell'account di archiviazione hello creato in precedenza. Le variabili sono anche le impostazioni di hello tooprovide utilizzato per l'estensione di diagnostica hello. Hello utilizzare [procedure consigliate per la creazione di modelli di Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp si decide come toostructure hello parametri e variabili del modello.

## <a name="resource-loops"></a>cicli di risorse

Quando sono necessarie più macchine virtuali per l'applicazione, è possibile usare un elemento di copia in un modello. Questo elemento facoltativo consente di scorrere la creazione di hello numero di macchine virtuali che è specificato come parametro:

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

Inoltre, si noti nell'esempio hello che hello indice ciclo viene utilizzato quando alcuni hello specificando i valori per la risorsa hello. Ad esempio, se è stato immesso un numero di istanze di tre, i nomi di hello dei dischi del sistema operativo hello sono myOSDisk1 myOSDisk2 e myOSDisk3:

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
>In questo esempio utilizza dischi gestiti per le macchine virtuali hello.
>
>

Tenere presente che la creazione di un ciclo per una risorsa modello di hello potrebbe richiedere si toouse hello ciclo durante la creazione o l'accesso alle altre risorse. Ad esempio, più macchine virtuali non è possibile utilizzare hello stessa interfaccia di rete in modo se il modello esegue un ciclo tramite la creazione di tre macchine virtuali anche necessario scorrere la creazione di tre interfacce di rete. Quando si assegna un tooa di interfaccia di rete VM, indice ciclo hello è tooidentify utilizzato è:

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a>Dipendenze

La maggior parte delle risorse dipendono altri toowork risorse correttamente. Macchine virtuali deve essere associate a una rete virtuale e toodo richiede che un'interfaccia di rete. Hello [dependsOn](../../resource-group-define-dependencies.md) elemento è utilizzato toomake interfaccia di rete hello sia pronto toobe utilizzato prima della creazione di macchine virtuali hello:

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

Resource Manager consente di distribuire in parallelo le risorse la cui distribuzione non dipende da un'altra risorsa. Prestare attenzione quando si impostano le dipendenze in quanto si può rallentare inavvertitamente la distribuzione, specificando dipendenze non necessarie. Le dipendenze possono concatenare più risorse. Ad esempio, l'interfaccia di rete hello dipende indirizzo IP pubblico hello e risorse di rete virtuale.

Come è possibile stabilire se è necessaria una dipendenza? Esaminare i valori hello che è impostato nel modello di hello. Se un elemento nella definizione di risorsa di macchina virtuale hello punta tooanother risorsa che viene distribuito in hello stesso modello, è necessario una dipendenza. Ad esempio, la macchina virtuale di esempio definisce un profilo di rete:

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

tooset questa proprietà, l'interfaccia di rete hello deve esistere. Pertanto, è necessaria una dipendenza. È necessario anche tooset una dipendenza quando è definita una risorsa (figlio) all'interno di un'altra risorsa (un elemento padre). Ad esempio, le impostazioni di diagnostica hello e le estensioni degli script personalizzati sono entrambi definiti come risorse figlio di una macchina virtuale hello. Non è possibile creare fino a quando non esistono macchine virtuali hello. Di conseguenza, entrambe le risorse sono contrassegnate come dipendenti nella macchina virtuale hello.

## <a name="profiles"></a>Profili

Quando si definisce una risorsa di macchina virtuale, vengono usati diversi elementi di profilo. Alcuni sono necessari e alcuni sono facoltativi. Ad esempio, gli elementi hardwareProfile, osProfile, storageProfile e profilo di hello sono obbligatori, ma diagnosticsProfile hello è facoltativo. Questi profili definiscono impostazioni, ad esempio:
   
- [dimensione](sizes.md)
- [nome](/architecture/best-practices/naming-conventions) e credenziali
- disco e [impostazioni del sistema operativo](cli-ps-findimage.md)
- [interfaccia di rete](../../virtual-network/virtual-networks-multiple-nics.md) 
- diagnostica di avvio

## <a name="disks-and-images"></a>Dischi e immagini
   
In Azure i file del disco rigido virtuale possono rappresentare [dischi o immagini](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Quando il sistema operativo hello in un file vhd è specializzato toobe una macchina virtuale specifica, è tooas di cui si fa riferimento un disco. Il sistema operativo hello in un file di disco rigido virtuale generalizzato toobe usato toocreate più macchine virtuali, è un'immagine di tooas cui viene fatto riferimento.   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a>Creare nuove macchine virtuali e nuovi dischi da un'immagine della piattaforma

Quando si crea una macchina virtuale, è necessario decidere quali toouse del sistema operativo. elemento imageReference Hello è usato toodefine hello operativo di una nuova macchina virtuale. esempio Hello viene illustrata una definizione per un sistema operativo Windows Server:

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

Se si desidera toocreate un sistema operativo Linux, è possibile utilizzare questa definizione:

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

Impostazioni di configurazione per disco del sistema operativo hello assegnate con elemento osDisk hello. Hello esempio definisce un nuovo disco gestito con la memorizzazione nella cache in modalità set troppo hello**ReadWrite** e tale disco hello viene creato da un [immagine della piattaforma](cli-ps-findimage.md):

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a>Creare nuove macchine virtuali da dischi gestiti esistenti

Se si desidera toocreate le macchine virtuali dai dischi esistenti, rimuovere imageReference hello e gli elementi di osProfile hello e definire queste impostazioni del disco:

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a>Creare nuove macchine virtuali da un'immagine gestita

Se si desidera toocreate una macchina virtuale da un'immagine gestita, modificare l'elemento imageReference hello e definire queste impostazioni del disco:

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a>Collegare i dischi dei dati

È possibile aggiungere facoltativamente toohello dischi dati le macchine virtuali. Hello [numero di dischi](sizes.md) dipende dalle dimensioni hello del disco del sistema operativo in uso. Dimensioni delle macchine virtuali hello hello impostare tooStandard_DS1_v2, numero massimo di hello di dischi dati che è stato possibile aggiungere toohello li è due. Nell'esempio hello, un disco dati gestiti viene aggiunto tooeach VM:

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a>Estensioni

Sebbene [estensioni](extensions-features.md) sono una risorsa distinta, tooVMs strettamente collegati. Le estensioni possono essere aggiunte come risorsa figlio di hello macchina virtuale o come una risorsa distinta. esempio Hello Mostra hello [estensione diagnostica](extensions-diagnostics-template.md) da aggiungere le macchine virtuali toohello:

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

Questa risorsa di estensione Usa variabile storageName hello e i valori di tooprovide di hello delle variabili di diagnostica. Se si desiderano toochange hello i dati raccolti da questa estensione, è possibile aggiungere più variabile di wadperfcounters toohello di contatori delle prestazioni. È anche possibile scegliere i dati di diagnostica hello tooput in un account di spazio di archiviazione diverso da quello in cui sono archiviati i dischi di macchina virtuale hello.

Sono disponibili numerose estensioni che è possibile installare in una macchina virtuale, ma hello più utile è probabilmente hello [estensione Script personalizzata](extensions-customscript.md). Nell'esempio hello in ogni macchina virtuale all'avvio viene eseguito uno script di PowerShell denominato start.ps1:

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

script start.ps1 Hello può eseguire molte attività di configurazione. Ad esempio, non vengono inizializzati i dischi dati hello toohello macchine virtuali aggiunte nell'esempio hello; è possibile utilizzare un tooinitialize script personalizzato li. Se si dispone di più toodo di attività di avvio, è possibile utilizzare hello start.ps1 file toocall altri script di PowerShell nell'archiviazione di Azure. esempio Hello Usa PowerShell, ma è possibile utilizzare qualsiasi metodo di scripting che sono disponibile nel sistema operativo hello che si sta utilizzando.

È possibile visualizzare lo stato di hello delle estensioni di hello installato dalle impostazioni di estensioni hello nel portale di hello:

![Recuperare lo stato dell'estensione](./media/template-description/virtual-machines-show-extensions.png)

È anche possibile ottenere informazioni sull'estensione utilizzando hello **Get AzureRmVMExtension** PowerShell comando hello **get estensione vm** comando CLI di Azure 2.0 o hello **ottenere informazioni sull'estensione**  API REST.

## <a name="deployments"></a>Deployments

Quando si distribuisce un modello di risorse hello Azure rileva che è stato distribuito come un gruppo e automaticamente assegna un nome di gruppo toothis distribuito. nome Hello della distribuzione di hello è hello corrisponde al nome hello del modello di hello.

Se si desidera conoscere lo stato di hello delle risorse nella distribuzione di hello, è possibile utilizzare il pannello di gruppo di risorse hello in hello portale di Azure:

![Ottenere informazioni sulla distribuzione](./media/template-description/virtual-machines-deployment-info.png)
    
Non è un problema toouse hello stesso modello toocreate le risorse o le risorse esistenti tooupdate. Quando si utilizzano comandi toodeploy modelli, è necessario hello opportunità toosay che [modalità](../../resource-group-template-deploy.md) desiderato toouse. è possibile impostare modalità Hello tooeither **completa** o **incrementale**. valore predefinito di Hello è aggiornamenti incrementali toodo. Prestare attenzione nell'utilizzo hello **completa** modalità perché accidentalmente eliminate le risorse. Quando si imposta la modalità hello troppo**completa**, Gestione risorse consente di eliminare tutte le risorse nel gruppo di risorse hello che non sono presenti nel modello di hello.

## <a name="next-steps"></a>Passaggi successivi

- È possibile creare un modello personalizzato usando le informazioni presenti in [Creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).
- Distribuire il modello di hello creati usando [creare una macchina virtuale Windows con un modello di gestione risorse](ps-template.md).
- Informazioni su come toomanage hello macchine virtuali creato esaminando [creare e gestire macchine virtuali di Windows con il modulo di Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
