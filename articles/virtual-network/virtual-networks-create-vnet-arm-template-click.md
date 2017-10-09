---
title: aaaCreate una rete virtuale | Modello di gestione risorse di Azure | Documenti Microsoft
description: Informazioni su come toocreate un virtuale di rete utilizzando un modello di gestione risorse di Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Creare una rete virtuale usando un modello di Azure Resource Manager

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica. Si consiglia di creare risorse modello di distribuzione di gestione risorse di hello. altre informazioni sulle toolearn hello le differenze tra hello due modelli, leggere hello [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md) articolo.
 
In questo articolo viene illustrato come una rete virtuale tramite la distribuzione di gestione risorse di hello toocreate modello utilizzando un modello di gestione risorse di Azure. È anche possibile creare una rete virtuale tramite Gestione risorse di usare altri strumenti o creare una rete virtuale tramite il modello di distribuzione classica hello selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
- [Portale](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [CLI](virtual-networks-create-vnet-arm-cli.md)
- [Modello](virtual-networks-create-vnet-arm-template-click.md)
- [Portale (versione classica)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (versione classica)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [Interfaccia della riga di comando (versione classica)](virtual-networks-create-vnet-classic-cli.md)

Si apprenderà come toodownload e modificare esistente modello ARM da GitHub e distribuire il modello di hello da GitHub, PowerShell e hello CLI di Azure.

Se si distribuisce il modello ARM hello direttamente da GitHub, senza alcuna modifica, semplicemente ignorare troppo[distribuire un modello da github](#deploy-the-arm-template-by-using-click-to-deploy).

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Scaricare e comprendere il modello di Azure Resource Manager hello
È possibile scaricare hello modello esistente per la creazione di una rete virtuale e due subnet da GitHub, apportare le modifiche potrebbe essere necessario e riutilizzarlo. toodo in tal caso, completare hello alla procedura seguente:

1. Passare troppo[pagina modello di esempio hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
2. Fare clic su **azuredeploy.json**, quindi fare clic su **RAW**.
3. Salvare tooa file hello una cartella locale nel computer.
4. Se si ha familiarità con i modelli, è possibile ignorare toostep 7.
5. Aprire file hello appena salvato e osservare il contenuto di hello in **parametri** nella riga 5. I parametri del modello ARM costituiscono un segnaposto per i valori che possono essere compilati durante la distribuzione.
   
   | Parametro | Descrizione |
   | --- | --- |
   | **location** |Area in cui verrà creato hello rete virtuale di Azure |
   | **vnetName** |Nome per hello nuova rete virtuale |
   | **addressPrefix** |Spazio di indirizzi per hello rete virtuale, nel formato CIDR |
   | **subnet1Name** |Nome per hello prima rete virtuale |
   | **subnet1Prefix** |Blocco CIDR per la prima subnet hello |
   | **subnet2Name** |Nome per hello seconda rete virtuale |
   | **subnet2Prefix** |Blocco CIDR per subnet secondo hello |
   
   > [!IMPORTANT]
   > I modelli di Gestione risorse di Azure conservati in GitHub possono cambiare nel tempo. Accertarsi di controllare il modello di hello prima di utilizzarlo.
   > 
   > 
6. Controllare il contenuto hello **risorse** e osservare l'esempio hello:
   
   * **type**. Tipo di risorsa viene creato dal modello hello. In questo caso, **Microsoft.Network/virtualNetworks**, che rappresenta una rete virtuale.
   * **name**. Nome per la risorsa hello. Avviso hello utilizzo di **[parameters('vnetName')]**, che significa hello verrà nome fornito come input utente hello o un file dei parametri durante la distribuzione.
   * **properties**. Elenco di proprietà per la risorsa hello. Questo modello Usa proprietà spazio e la subnet dell'indirizzo hello durante la creazione della rete virtuale.
7. Passare troppo[pagina modello di esempio hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
8. Fare clic su **azuredeploy-parameters.json** e quindi su **RAW**.
9. Salvare tooa file hello una cartella locale nel computer.
10. Aprire il file hello che appena salvato e modificare i valori hello per i parametri di hello. Utilizzare hello seguente i valori inferiori toodeploy hello rete virtuale descritto nello scenario hello:

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. Salvare il file hello.


## <a name="deploy-hello-template-using-powershell"></a>Distribuire il modello di hello tramite PowerShell

Completare hello dopo passaggi toodeploy hello template che è stato scaricato tramite PowerShell:

1. Installare e configurare Azure PowerShell, completare i passaggi hello hello [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.
2. Eseguire hello successivo comando toocreate un nuovo gruppo di risorse:

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    comando Hello crea un gruppo di risorse denominato *TestRG* in hello *centrale Usa* area di azure. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).

    Output previsto:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. Eseguire hello toodeploy hello nuova rete virtuale utilizzando i file modello/parametro hello è stato scaricato e modificato di sopra di comando seguente:

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    Output previsto:
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. Comando che segue hello esecuzione proprietà hello tooview di hello nuova rete virtuale:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    Output previsto:

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a>Distribuire il modello di hello utilizzando fare clic su da distribuire

È possibile riutilizzare predefiniti repository di GitHub di tooa caricati modelli, Gestione risorse di Azure gestiti da Microsoft e aprire toohello community. Questi modelli possono essere distribuiti direttamente da GitHub, o scaricati e modificati toofit le proprie esigenze. toodeploy un modello che crea una rete virtuale con due subnet, hello completo alla procedura seguente:

1. Da un browser, passare troppo[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
2. Scorrere verso il basso l'elenco di hello dei modelli e fare clic su **101-rete virtuale due subnet**. Controllare hello **README.md** file, come illustrato di seguito.

    ![File READEME.md in github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. Fare clic su **distribuire tooAzure**. Se necessario, immettere le credenziali di accesso di Azure. 
4. In hello **parametri** pannello, immettere i valori hello desidera toouse toocreate nuova rete virtuale e quindi fare clic su **OK**. Hello nella figura seguente mostra i valori hello per uno scenario di hello:
   
    ![Parametri del modello ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. Fare clic su **gruppo di risorse** e selezionare un tooadd gruppo di risorse hello tra oppure fare clic su **Crea nuovo** tooadd hello rete virtuale tooa nuovo gruppo di risorse. Hello nella figura seguente mostra hello di risorse di gruppo per un nuovo gruppo di risorse denominato **TestRG**:

    ![Gruppo di risorse](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. Se necessario, modificare hello **sottoscrizione** e **percorso** le impostazioni per la rete virtuale.
7. Se non si desidera toosee hello rete virtuale come un riquadro in hello **schermata iniziale**, disabilitare **tooStartboard Pin**.
8. Fare clic su **legali**, leggere le condizioni di hello e fare clic su **acquistare** tooagree. 
9. Fare clic su **crea** toocreate hello rete virtuale.
   
    ![Invio del riquadro di distribuzione nel portale di anteprima](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Una volta completata la distribuzione di hello, hello portale di Azure selezionare **più servizi**, tipo *reti virtuali* nella casella Filtro hello visualizzata, quindi fare clic su Pannello di reti virtuali di virtuale reti toosee hello. Nel Pannello di hello, fare clic su *TestVNet*. In hello *TestVNet* pannello, fare clic su **subnet** subnet hello creato toosee, come illustrato nella seguente immagine hello:
    
     ![Creare una rete virtuale nel portale di anteprima](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooconnect:

- Una rete virtuale tooa di macchina virtuale (VM) da lettura hello [creare una macchina virtuale Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) o [creare una VM Linux](../virtual-machines/linux/quick-create-portal.md) articoli. Anziché creare una rete virtuale e subnet nei passaggi hello degli articoli hello, è possibile selezionare una rete virtuale esistente e subnet tooconnect una macchina virtuale.
- Hello reti virtuali di rete virtuale tooother leggendo hello [connettere reti virtuali](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) articolo.
- rete locale tooan rete virtuale Hello utilizza una rete privata virtuale (VPN) da sito a sito o un circuito ExpressRoute. Ulteriori informazioni, leggere hello [connettere una rete locale tooan di rete virtuale tramite una VPN site-to-site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [collegare un circuito ExpressRoute di tooan rete virtuale](../expressroute/expressroute-howto-linkvnet-arm.md) articoli.
