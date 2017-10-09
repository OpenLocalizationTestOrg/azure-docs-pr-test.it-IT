# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Uso di Managed Disks nei modelli di Azure Resource Manager

Questo documento descrive come differenze hello tra dischi gestiti e quando si usano macchine virtuali di Azure Resource Manager modelli tooprovision. Ciò consentirà di modelli tooupdate esistenti con i dischi toomanaged di dischi non gestiti. Per riferimento, usiamo hello [windows semplice di vm 101](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) modello come guida. È possibile visualizzare il modello di hello utilizzando entrambi [dischi gestiti](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) e una versione precedente utilizzando [non gestita dischi](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) se si desidera toodirectly confrontarli.

## <a name="unmanaged-disks-template-formatting"></a>Formattazione del modello per dischi non gestiti

toobegin, verranno esaminate in dischi come non gestiti vengono distribuiti. Durante la creazione di dischi non gestiti, è necessario un file VHD di hello toohold di account di archiviazione. È possibile creare un nuovo account di archiviazione o usarne uno già esistente. In questo articolo viene illustrato come toocreate un nuovo account di archiviazione. tooaccomplish, è necessario una risorsa di account di archiviazione in blocco di risorse hello, come illustrato di seguito.

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

Oggetto macchina virtuale hello, abbiamo bisogno di una dipendenza tooensure di account di archiviazione hello che ha creato prima macchina virtuale hello. All'interno di hello `storageProfile` sezione, è quindi possibile specificare un URI completo della posizione del disco rigido virtuale che fa riferimento all'account di archiviazione hello ed è necessario per il disco del sistema operativo hello e qualsiasi disco dati hello hello. 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a>Formattazione del modello per dischi gestiti

Con i dischi gestiti di Azure, disco hello diventa una risorsa di primo livello e non richiede più un toobe di account di archiviazione creato dall'utente hello. Dischi gestiti prima esposte nel hello `2016-04-30-preview` versione dell'API, sono disponibili in tutte le versioni API successive e sono di tipo di disco predefinito hello. Hello nelle sezioni seguenti vengono dettagliatamente le impostazioni predefinite di hello e in dettaglio come toofurther personalizzare i dischi.

> [!NOTE]
> È consigliabile toouse un'API versione successiva a quella `2016-04-30-preview` come sono state eseguite modifiche di rilievo tra `2016-04-30-preview` e `2017-03-30`.
>
>

### <a name="default-managed-disk-settings"></a>Impostazioni predefinite per i dischi gestiti

toocreate una macchina virtuale con dischi gestiti, non sono più necessari risorsa account di archiviazione hello toocreate e può aggiornare la risorsa di macchina virtuale come indicato di seguito. In particolare si noti che hello `apiVersion` riflette `2017-03-30` hello e `osDisk` e `dataDisks` non è più fare riferimento tooa URI specifico per hello disco rigido virtuale. Quando si distribuisce senza specificare proprietà aggiuntive, verrà utilizzato il disco hello [archiviazione con ridondanza locale Standard](../articles/storage/common/storage-redundancy.md). Se viene specificato alcun nome, ha formato hello `<VMName>_OsDisk_1_<randomstring>` per il disco del sistema operativo hello e `<VMName>_disk<#>_<randomstring>` per ogni disco dati. Per impostazione predefinita, la crittografia del disco di Azure è disabilitata; la memorizzazione nella cache è di lettura/scrittura per il disco del sistema operativo hello e Nessuno per i dischi dati. È possibile riscontrare nel seguente esempio hello che sia ancora disponibile una dipendenza di account di archiviazione, anche se questo è solo per l'archiviazione di diagnostica e non è necessaria per l'archiviazione su disco.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a>Uso di una risorsa disco gestito di primo livello

Come una configurazione del disco hello toospecifying alternativo nell'oggetto macchina virtuale hello, è possibile creare una risorsa disco di primo livello e associarlo come parte della creazione della macchina virtuale hello. Ad esempio, è possibile creare una risorsa disco, come indicato di seguito toouse come disco dati.

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

Oggetto VM hello, è possibile fare riferimento questo toobe di oggetto disco collegato. Specifica dell'ID di risorsa hello di hello gestiti disco creata in hello `managedDisk` proprietà consente di collegare hello unità disco hello come hello viene creata la VM. Si noti che hello `apiVersion` per hello risorsa macchina virtuale è troppo`2017-03-30`. Si noti inoltre che abbiamo creato una dipendenza su hello disco risorse tooensure che è stato creato correttamente prima della creazione della macchina virtuale. 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>Creare set di disponibilità gestiti con macchine virtuali che usano dischi gestiti

toocreate gestiti disponibilità set con macchine virtuali con dischi gestiti, aggiungere hello `sku` disponibilità toohello oggetto set di risorse e set hello `name` proprietà troppo`Aligned`. In questo modo si garantisce che i dischi di hello per ogni macchina virtuale sono sufficientemente isolati tra loro tooavoid singoli punti di errore. Si noti inoltre che hello `apiVersion` per risorsa del set di disponibilità hello è troppo`2017-03-30`.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a>Altri scenari e personalizzazioni

toofind informazioni complete sulle specifiche di hello API REST, vedere hello [creare un disco gestito documentazione dell'API REST](/rest/api/manageddisks/disks/disks-create-or-update). Sono disponibili ulteriori scenari, così come impostazione predefinita e i valori accettabili che possono essere inviati toohello API tramite distribuzioni modello. 

## <a name="next-steps"></a>Passaggi successivi

* Per i modelli completi che usano dischi gestiti visitare hello seguenti collegamenti repository Guida introduttiva di Azure.
    * [Macchina virtuale Windows con disco gestito](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [Macchina virtuale Linux con disco gestito](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [Elenco completo dei modelli con disco gestito](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Visitare hello [Panoramica di dischi gestiti di Azure](../articles/virtual-machines/windows/managed-disks-overview.md) documento toolearn ulteriori informazioni sui dischi gestiti.
* Esaminare la documentazione di riferimento di modello hello per le risorse della macchina virtuale, visitare hello [riferimento a un modello Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) documento.
* Esaminare la documentazione di riferimento di modello hello per le risorse disco visitando hello [riferimento a un modello Microsoft.Compute/disks](/templates/microsoft.compute/disks) documento.
 
