---
title: aaaCreate una macchina virtuale con un indirizzo IP pubblico statico - modello di gestione risorse di Azure | Documenti Microsoft
description: Informazioni su come toocreate una macchina virtuale con un indirizzo IP pubblico statico di indirizzi utilizzando un modello di gestione risorse di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>Creare una VM con un indirizzo IP pubblico statico mediante un modello di Azure Resource Manager

> [!div class="op_single_selector"]
> * [Portale di Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Modello](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>Risorse indirizzo IP pubblico in un file di modello
È possibile visualizzare e scaricare hello [modello di esempio](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).

Hello nella sezione seguente viene illustrata hello definizione di risorsa IP pubblica hello, a seconda dello scenario hello precedente:

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

Hello preavviso **publicIPAllocationMethod** proprietà, che è stata impostata troppo*statico*. Questa proprietà può essere *Dinamico* (valore predefinito) o *Statico*. Impostazione toostatic garantisce che l'indirizzo IP pubblico hello assegnato non verrà mai modificato.

Hello nella sezione seguente viene illustrato associazione hello dell'indirizzo IP pubblico hello con un'interfaccia di rete:

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

Hello preavviso **publicIPAddress** proprietà verso toohello **Id** di una risorsa denominata **variables('webVMSetting').pipName**. Che è il nome di hello della risorsa IP pubblica hello illustrato in precedenza.

Infine, l'interfaccia di rete hello precedente è elencato in hello **profilo** proprietà di hello macchina virtuale da creare.

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Distribuire il modello di hello utilizzando fare clic su toodeploy

modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra. toodeploy questo modello utilizzando fare clic su toodeploy, fare clic su **distribuire tooAzure** file Readme.md hello per hello [macchina virtuale con indirizzo PIP statico](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) modello. Sostituire i valori dei parametri predefiniti hello se lo si desidera, immettere valori per parametri vuoti hello.  Seguire le istruzioni hello hello portale toocreate una macchina virtuale con un indirizzo IP pubblico statico.

## <a name="deploy-hello-template-by-using-powershell"></a>Distribuire il modello di hello tramite PowerShell

modello di hello toodeploy scaricato tramite PowerShell, seguire i passaggi di hello seguenti.

1. Se non si è mai usato Azure PowerShell, hello completato i passaggi in hello [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.
2. Nella console di PowerShell, eseguire hello `New-AzureRmResourceGroup` cmdlet toocreate un nuovo gruppo di risorse, se necessario. Se si dispone già di un gruppo di risorse creato, andare toostep 3.

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    Output previsto:
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. Nella console di PowerShell, eseguire hello `New-AzureRmResourceGroupDeployment` modello hello toodeploy di cmdlet.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    Output previsto:
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Distribuire il modello di hello utilizzando hello CLI di Azure
modello di hello toodeploy utilizzando hello CLI di Azure, hello completo alla procedura seguente:

1. Se non si è mai usato CLI di Azure, seguire hello hello [installare e configurare hello Azure CLI](../cli-install-nodejs.md) articolo tooinstall e configurarlo.
2. Eseguire hello `azure config mode` tooswitch tooResource Manager modalità comando, come illustrato di seguito.

    ```azurecli
    azure config mode arm
    ```

    Hello è previsto un output di hello comando precedente:

        info:    New mode is arm

3. Aprire hello [file dei parametri](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), selezionare il contenuto e salvarlo tooa file nel computer. Per questo esempio, i parametri di hello vengono salvati i file tooa denominato *parameters.json*. I valori dei parametri hello nel file hello se lo si desidera modificare, ma come minimo, è consigliabile modificare il valore di hello per hello adminPassword parametro tooa complesso password univoca.
4. Eseguire hello `azure group deployment create` cmd toodeploy hello nuova rete virtuale utilizzando il modello di hello e parametro file scaricato e modificato in precedenza. Nel comando hello seguente, sostituire <path> con percorso hello è stato salvato file hello. 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    Output previsto (elenca i valori usati per i parametri):

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

