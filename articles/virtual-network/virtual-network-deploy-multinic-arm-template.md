---
title: "aaaCreate una macchina virtuale con più schede di rete: modello di gestione risorse di Azure | Documenti Microsoft"
description: "Creare una VM con più schede di interfaccia di rete mediante un modello di Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>Creare una macchina virtuale con più schede di interfaccia di rete usando un modello
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](virtual-network-deploy-multinic-classic-ps.md).
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

i passaggi seguenti Hello utilizzano un gruppo di risorse denominato *IaaSStory* per i server WEB di hello e un gruppo di risorse denominato *IaaSStory-back-end* per i server hello DB.

## <a name="prerequisites"></a>Prerequisiti
Prima di poter creare hello server di database, è necessario hello toocreate *IaaSStory* gruppo di risorse con tutte le risorse necessarie hello per questo scenario. completare queste risorse, toocreate hello i passaggi seguenti:

1. Passare troppo[pagina modello hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Nella pagina toohello destra del modello di hello **gruppo di risorse padre**, fare clic su **distribuire tooAzure**.
3. Se necessario, modificare i valori di parametro hello, quindi seguire i passaggi hello nel gruppo di risorse hello toodeploy portale hello anteprima di Azure.

> [!IMPORTANT]
> Assicurarsi che i nomi degli account di archiviazione siano univoci. In Azure non sono infatti ammessi nomi di account di archiviazione duplicati.
> 

## <a name="understand-hello-deployment-template"></a>Comprendere il modello di distribuzione hello
Prima di distribuire il modello di hello fornito con questa documentazione, assicurarsi che comprendere le funzionalità. Hello passaggi fornita una buona panoramica del modello di hello:

1. Passare troppo[pagina modello hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Fare clic su **azuredeploy.json** tooopen file di modello hello.
3. Hello preavviso *osType* parametro elencato di seguito. Questo parametro è utilizzato tooselect quali toouse immagine di macchina virtuale per server di database hello, insieme al sistema operativo più le impostazioni correlate.

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. Scorrere verso il basso toohello elenco di variabili e controllare la definizione di hello per hello **dbVMSetting** variabili, elencate di seguito. Riceve uno degli elementi di matrice hello contenuti in hello **dbVMSettings** variabile. Se si ha familiarità con la terminologia di sviluppo software, è possibile visualizzare hello **dbVMSettings** variabile come una tabella hash o un dizionario.

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. È possibile decidere toodeploy macchine virtuali di Windows in esecuzione SQL in hello back-end. Quindi hello valore per **osType** sarebbe *Windows*, hello e **dbVMSetting** variabile conterrebbe elemento hello elencato di seguito, che rappresenta il valore prima di hello in hello **dbVMSettings** variabile.

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. Hello preavviso **vmSize** contiene il valore di hello *Standard_DS3*. Solo determinate dimensioni di macchina virtuale consentono di utilizzare hello di più schede di rete. È possibile verificare le dimensioni delle macchine Virtuali supportano più schede di rete tramite la lettura di hello [dimensioni delle macchine Virtuali di Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [le dimensioni di VM Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articoli.

7. Scorrere verso il basso troppo**risorse** e hello primo elemento. Questo descrive un account di archiviazione Questo account di archiviazione sarà dischi di dati utilizzati toomaintain hello utilizzati da ogni macchina virtuale del database. In questo scenario, ogni macchina virtuale del database dispone di un disco del sistema operativo archiviato nell'archiviazione consueta e due dischi dati archiviati nell'archiviazione dell'unità SSD (premium).

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. Scorrere verso il basso toohello risorsa successiva, come indicato di seguito. Questa risorsa rappresenta hello che NIC utilizzato per l'accesso al database in ogni macchina virtuale del database. Utilizzo di hello preavviso di hello **copia** funzione in questa risorsa. modello Hello consente toodeploy come più macchine virtuali che si desidera, in base a hello **dbCount** parametro. È pertanto necessario toocreate hello stessa quantità di schede di rete per l'accesso al database, uno per ogni macchina virtuale.

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. Scorrere verso il basso toohello risorsa successiva, come indicato di seguito. Questa risorsa rappresenta hello che NIC utilizzato per la gestione in ogni macchina virtuale del database. Ancora una volta, è necessaria una di queste schede di interfaccia di rete per ogni macchina virtuale del database. Hello preavviso **sicurezza di rete** elemento, il collegamento di un gruppo che consente accesso tooRDP/SSH toothis NIC solo.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. Scorrere verso il basso toohello risorsa successiva, come indicato di seguito. Questa risorsa rappresenta un toobe di set di disponibilità condiviso da tutte le macchine virtuali di database. In questo modo si garantisce che sarà sempre presente una macchina virtuale in hello impostata in esecuzione durante la manutenzione.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. Scorrere verso il basso toohello successiva risorsa. Questa risorsa rappresenta database hello macchine virtuali, come illustrato in hello innanzitutto alcune righe elencate di seguito. Utilizzo di hello preavviso di hello **copia** di nuovo, assicurando che vengano create più macchine virtuali in base a hello **dbCount** parametro. Si noti inoltre hello **dependsOn** insieme. Vengono elencati due schede di rete viene toobe necessarie creato prima macchina virtuale viene distribuita insieme al set di disponibilità hello e account di archiviazione hello hello.

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. Scorrere verso il basso hello VM risorsa toohello **profilo** elemento, come indicato di seguito. Si noti che sono presenti due schede di interfaccia di rete a cui ogni macchina virtuale fa riferimento. Quando si creano più schede di rete per una macchina virtuale, è necessario impostare hello **primario** proprietà di una delle schede di rete hello troppo*true*, e hello rest troppo*false*.

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Distribuire il modello ARM hello utilizzando fare clic su toodeploy

> [!IMPORTANT]
> È necessario seguire hello [prerequisiti](#Pre-requisites) passaggi prima di seguire le istruzioni di hello seguenti.
> 

modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra. toodeploy questo modello utilizzando fare clic su toodeploy, seguire [questo collegamento](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello destra **gruppo di risorse di back-end (vedere la documentazione)** fare clic su **distribuire tooAzure**, sostituire Hello valori di parametro predefiniti se necessario e seguire le istruzioni di hello nel portale di hello.

Figura Hello seguente mostra i contenuti di hello del hello nuovo gruppo di risorse, dopo la distribuzione.

![Gruppo di risorse di back-end](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>Distribuire il modello di hello tramite PowerShell
modello di hello toodeploy scaricato tramite PowerShell, installare e configurare PowerShell completando i passaggi hello hello [installare e configurare PowerShell](/powershell/azure/overview) articolo e quindi completare hello alla procedura seguente:

Eseguire hello  **`New-AzureRmResourceGroup`**  toocreate cmdlet un gruppo di risorse utilizzando hello modello.

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

Output previsto:

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Distribuire il modello di hello utilizzando hello CLI di Azure
modello di hello toodeploy utilizzando hello CLI di Azure, seguire i passaggi di hello seguenti.

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello  **`azure config mode`**  tooswitch tooResource Manager modalità comando, come illustrato di seguito.

    ```azurecli
    azure config mode arm
    ```

    Hello è previsto output indicato di seguito:

        info:    New mode is arm

3. Aprire hello [file dei parametri](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), selezionare il contenuto e salvarlo tooa file nel computer. Per questo esempio, sono stati salvati i file di parametri hello troppo*parameters.json*.
4. Eseguire hello  **`azure group deployment create`**  cmdlet toodeploy hello nuova rete virtuale utilizzando il modello di hello e parametro file scaricato e modificato in precedenza. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    Output previsto:
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

