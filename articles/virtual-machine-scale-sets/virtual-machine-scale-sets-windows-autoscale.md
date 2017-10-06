---
title: "Set di scalabilità di macchine virtuali Windows aaaAutoscale | Documenti Microsoft"
description: "Impostare il ridimensionamento automatico per un set di scalabilità di macchine virtuali Windows tramite Azure PowerShell"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a>Ridimensionare automaticamente le macchine virtuali in un set di scalabilità di macchine virtuali
Set di scalabilità di macchine virtuali semplificano automaticamente toodeploy e gestire macchine virtuali identiche come un set. I set di scalabilità offrono un livello di calcolo scalabile e personalizzabile per applicazioni con iperscalabilità e supportano le immagini della piattaforma Windows, le immagini della piattaforma Linux, le immagini personalizzate e le estensioni. Per altre informazioni sui set di scalabilità, vedere [Set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md).

Questa esercitazione viene illustrato come un set di scalabilità di macchine virtuali di Windows e automaticamente scala hello macchine in hello toocreate impostato. Creare una scala hello e impostare il ridimensionamento per la creazione di un modello di gestione risorse di Azure e la distribuzione con Azure PowerShell. Per altre informazioni sui modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md). toolearn più sul ridimensionamento automatico del set di scalabilità, vedere [il ridimensionamento automatico e imposta la scala di macchina virtuale](virtual-machine-scale-sets-autoscale-overview.md).

In questo articolo, si distribuisce seguente hello risorse ed estensioni:

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Insights.VMDiagnosticsSettings
* Microsoft.Insights/autoscaleSettings

Per altre informazioni sulle risorse di Resource Manager, vedere [Azure Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="step-1-install-azure-powershell"></a>Passaggio 1: installare Azure PowerShell
Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per informazioni sull'installazione hello la versione più recente di Azure PowerShell, selezionando la sottoscrizione e la firma in tooAzure.

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a>Passaggio 2: Creare un gruppo di risorse e un account di archiviazione
1. **Creare un gruppo di risorse** : tutte le risorse devono essere distribuito tooa gruppo di risorse. Utilizzare [New AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate un gruppo di risorse denominato **vmsstestrg1**.
2. **Creare un account di archiviazione** : questo account di archiviazione è in cui è archiviato il modello di hello. Utilizzare [New AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate un account di archiviazione denominato **vmsstestsa**.

## <a name="step-3-create-hello-template"></a>Passaggio 3: Creare il modello di hello
Un modello di gestione risorse di Azure rende possibile la si toodeploy e gestire le risorse di Azure insieme con una descrizione JSON delle risorse di hello e parametri di distribuzione associati.

1. Nell'editor preferito, creare file hello C:\VMSSTemplate.json e aggiungere hello iniziale JSON struttura toosupport hello modello.

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. Parametri non sono sempre necessari, ma forniscono un modo tooinput valori quando viene distribuito il modello di hello. Aggiungere i parametri che è stato aggiunto il modello di toohello nell'elemento padre parametri hello.

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * Un nome per la macchina virtuale separata hello che viene utilizzato tooaccess hello macchine nel set di scalabilità hello.
    * nome Hello hello dell'account di archiviazione in cui è archiviato il modello di hello.
    * numero di Hello di macchine virtuali tooinitially creare nel set di scalabilità hello.
    * nome Hello e la password dell'account di amministratore hello in macchine virtuali hello.
    * Imposta un prefisso del nome per le risorse di hello scala hello toosupport creati.

3. Variabili possono essere utilizzate nei valori di toospecify modello che possono cambiare frequentemente o valori che devono toobe creato da una combinazione di valori di parametro. Aggiungere queste variabili che è stato aggiunto il modello di toohello nell'elemento padre variabili hello.

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * I nomi DNS che vengono utilizzati da hello interfacce di rete.

        * i nomi degli indirizzi IP di Hello e i prefissi di rete virtuale hello e le subnet.
        * Hello nomi e gli identificatori di rete virtuale hello, bilanciamento del carico e le interfacce di rete.
        * Nomi account di archiviazione per gli account di hello associati macchine hello in set di scalabilità hello.
        * Impostazioni per l'estensione di diagnostica che viene installato nelle macchine virtuali hello hello. Per ulteriori informazioni su hello estensione di diagnostica, vedere [creare una macchina virtuale Windows con monitoraggio e diagnostica usando il modello di gestione risorse di Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

4. Aggiungere risorse di account di archiviazione hello nell'elemento padre di risorse hello che è stato aggiunto il modello di toohello. Il modello utilizza un hello toocreate ciclo consigliato cinque gli account di archiviazione in cui sono archiviati i dischi del sistema operativo hello e dati di diagnostica. Questo set di account può supportare fino a too100 di macchine virtuali in un set di scalabilità, ossia massimo corrente hello. Ogni account di archiviazione denominato con un indicatore lettera definite nelle variabili hello combinate con il prefisso hello forniti nei parametri hello per modello hello.

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. Aggiungere risorse di rete virtuale hello. Per altre informazioni, vedere [Provider di risorse di rete](../virtual-network/resource-groups-networking.md).

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. Aggiungere hello pubbliche risorse indirizzo IP utilizzati da hello bilanciamento del caricano e l'interfaccia di rete.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. Aggiungere una risorsa di bilanciamento del carico hello utilizzato dal set di scalabilità hello. Per altre informazioni, vedere [Supporto di Gestione risorse di Azure per il servizio di bilanciamento del carico](../load-balancer/load-balancer-arm.md).

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. Aggiungere risorse di interfaccia di rete hello utilizzato dalla macchina virtuale separata hello. Poiché le macchine in un set di scalabilità non sono accessibili tramite un indirizzo IP pubblico, una macchina virtuale separata viene creata in hello stesso virtuale macchine di hello tooremotely accesso di rete.

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. Aggiungere una macchina virtuale separata hello nella stessa rete set di scalabilità hello hello.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
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
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. Aggiungere una risorsa del set di scalabilità della macchina virtuale hello e specificare l'estensione diagnostica hello installato in tutte le macchine virtuali nel set di scalabilità hello. Molte delle impostazioni di hello per questa risorsa sono simili alla risorsa di macchina virtuale hello. Hello principali differenze riguardano hello capacità elemento che specifica il numero di hello di macchine virtuali nel set di scalabilità hello e upgradePolicy che specifica la modalità con cui gli aggiornamenti vengono eseguiti toovirtual macchine. Hello set di scalabilità non viene creata finché non vengono creati tutti gli account di archiviazione hello come specificato con l'elemento dependsOn hello.

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
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
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Aggiungere hello autoscaleSettings risorsa che definisce la modalità in base all'utilizzo del processore hello computer hello in set di scalabilità hello hello set di scalabilità.

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
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    Per questa esercitazione, i valori importanti sono i seguenti:
    
    * **metricName**  
    Questo valore è hello stesso come contatore delle prestazioni hello definiti nella variabile wadperfcounter hello. Utilizzo di tale variabile, hello estensione di diagnostica raccoglie hello **( totale)\% tempo processore** contatore.
    
    * **metricResourceUri**  
    Questo valore è l'identificatore di risorsa hello del set di scalabilità della macchina virtuale hello.
    
    * **timeGrain**  
    Questo valore è la granularità hello di metriche di hello che vengono raccolti. In questo modello, è impostato tooone minuto.
    
    * **statistic**  
    Questo valore determina come le metriche hello vengono combinati tooaccommodate hello azione di scalabilità automatica. Hello i valori possibili sono: Media, Min, Max. In questo modello, verrà raccolti hello totale utilizzo medio della CPU delle macchine virtuali hello.
    
    * **timeWindow**  
    Questo valore è hello intervallo di tempo in cui vengono raccolti i dati dell'istanza. Deve essere compreso tra 5 minuti e 12 ore.
    
    * **timeAggregation**  
    il suo valore determina la modalità hello i dati raccolti devono essere combinati nel tempo. valore predefinito di Hello è Media. Hello i valori possibili sono: Media, minimo, massimo, ultimo, totale, conteggio.
    
    * **operator**  
    Questo valore è l'operatore hello toocompare utilizzati hello metrica hello e dati soglia. Hello i valori possibili sono: uguale a, diverso da, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.
    
    * **threshold**  
    Questo valore è hello che attiva l'azione di scalabilità hello. In questo modello, i computer vengono aggiunti toohello scala impostata quando l'utilizzo medio della CPU hello tra le macchine nel set di hello è oltre il 50%.
    
    * **direction**  
    Questo valore determina l'azione eseguita quando viene raggiunto il valore di soglia hello hello. i valori possibili di Hello sono aumentano o diminuiscono. In questo modello, hello numero di macchine virtuali nel set di scalabilità hello viene aumentato se la soglia di hello è oltre il 50% di tempo definito hello.
    
    * **type**  
    Questo valore è di tipo hello di azione che deve essere eseguita e deve essere impostato tooChangeCount.
    
    * **value**  
    Questo valore è il numero di hello di macchine virtuali che vengono aggiunti o rimossi dal set di scalabilità hello. Questo valore deve essere uguale o maggiore di 1. valore predefinito di Hello è 1. In questo modello, hello macchine nella scala hello impostare numerose aumenta di 1 quando viene raggiunta la soglia di hello.
    
    * **cooldown**  
    Questo valore è quantità hello di toowait tempo dall'ultima azione di scalabilità hello prima che si verifichi l'azione successiva hello. Questo valore deve essere compreso tra un minuto e una settimana.

12. Salvare il file di modello hello.    

## <a name="step-4-upload-hello-template-toostorage"></a>Passaggio 4: Caricare hello modello toostorage
è possibile caricare il modello di Hello, purché si conosce il nome di hello e la chiave primaria dell'account di archiviazione hello creato nel passaggio 1.

1. Nella finestra di Microsoft Azure PowerShell hello, impostare una variabile che specifica il nome di hello hello dell'account di archiviazione creato nel passaggio 1.
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. Impostare una variabile che specifica una chiave primaria dell'account di archiviazione hello hello.
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   È possibile ottenere la chiave facendo clic sull'icona chiave hello durante la visualizzazione di risorse di account di archiviazione hello in hello portale di Azure.
3. Creare hello oggetto account di archiviazione contesto che viene utilizzato toovalidate operazioni con account di archiviazione hello.
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. Creare il contenitore di hello per archiviare il modello di hello.

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. Caricare hello modello file toohello nuovo contenitore.

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a>Passaggio 5: Distribuire il modello di hello
Ora che è stato creato il modello di hello, è possibile avviare la distribuzione delle risorse di hello. Utilizzare questo processo di hello toostart comando:

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

Quando preme INVIO, sei valori tooprovide richiesta per le variabili di hello che è assegnato. Specificare questi valori:

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

Richiede circa 15 minuti per essere distribuito tutti hello risorse toosuccessfully.

> [!NOTE]
> È possibile utilizzare anche le risorse di hello del portale hello possibilità toodeploy. Usare questo collegamento: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"
> 
> 

## <a name="step-6-monitor-resources"></a>Passaggio 6: Monitorare le risorse
Per ottenere informazioni sui set di scalabilità di macchine virtuali, è possibile usare i metodi seguenti:

* portale di Azure Hello: attualmente è possibile ottenere una quantità limitata di informazioni tramite il portale di hello.
* Hello [Esplora inventario risorse di Azure](https://resources.azure.com/) -questo strumento è hello migliore per l'esplorazione dello stato corrente di hello del set di scalabilità. Seguire questo percorso e dovrebbe essere vista istanza hello della scala hello imposta creato:
  
    sottoscrizioni > {sottoscrizioni dell'utente} > gruppi di risorse > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > macchine virtuali

* Azure PowerShell - usare questo comando tooget alcune informazioni:

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  Or
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* Connessione macchina virtuale separata toohello esattamente come si farebbe qualsiasi altro computer e quindi è possibile accedere in remoto hello le macchine virtuali in hello scala set toomonitor singoli processi.

> [!NOTE]
> Nell'articolo [Set di scalabilità di macchine virtuali](https://msdn.microsoft.com/library/mt589023.aspx)

## <a name="step-7-remove-hello-resources"></a>Passaggio 7: Rimuovere le risorse di hello
Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre un risorse toodelete buona norma che non sono più necessari. Non è necessario toodelete ogni risorsa separatamente da un gruppo di risorse. È possibile eliminare il gruppo di risorse hello e tutte le relative risorse vengono eliminate automaticamente.

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

Se si desidera tookeep il gruppo di risorse, è possibile eliminare solo set di scalabilità di hello.

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a>Passaggi successivi
* Gestire i set di scalabilità hello appena creata utilizzando informazioni hello in [gestire macchine virtuali in un Set di scalabilità della macchina virtuale](virtual-machine-scale-sets-windows-manage.md).
* Altre informazioni sull'aumento delle prestazioni sono disponibili in [Scalabilità automatica verticale con set di scalabilità di macchine virtuali](virtual-machine-scale-sets-vertical-scale-reprovision.md)
* Per alcuni esempi delle funzionalità di monitoraggio in Monitoraggio di Azure, vedere [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md) (Esempi di avvio rapido di PowerShell per Monitoraggio di Azure).
* Informazioni sulle funzionalità di notifica di [utilizzare scalabilità automatica azioni toosend posta elettronica e ai webhook notifiche di avviso in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* Informazioni su come troppo[i log di controllo di utilizzare le notifiche degli avvisi di posta elettronica e ai webhook toosend in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

