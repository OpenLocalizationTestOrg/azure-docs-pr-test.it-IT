---
title: 'Connettersi a una rete virtuale di tooanother di rete virtuale di Azure: PowerShell | Documenti Microsoft'
description: In questo articolo viene illustrata la connessione tra reti virtuali utilizzando Gestione risorse di Azure e PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>Configurare una connessione gateway VPN tra reti virtuali usando PowerShell

In questo articolo illustra come toocreate una connessione gateway VPN tra reti virtuali. Hello reti virtuali possono essere hello stesso o in aree diverse in e da hello uguali o diverse sottoscrizioni. Quando le reti virtuali connessione da sottoscrizioni diverse, le sottoscrizioni di hello non necessaria toobe associato hello stesso tenant di Active Directory. 

passaggi Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello e utilizzano PowerShell. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interfaccia della riga di comando di Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connettersi tra modelli di distribuzione diversi - Portale di Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connettersi tra modelli di distribuzione diversi - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

La connessione di una rete virtuale (VNet a VNet) tooanother di rete virtuale è simile tooconnecting un percorso di rete virtuale tooan locale del sito. Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE. Se le reti virtuali si trovano in hello stessa area, è opportuno tooconsider collegarli tramite Peering reti virtuali. Peering reti virtuali non usa un gateway VPN. Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).

La comunicazione tra reti virtuali può essere associata a configurazioni multisito. Consente di stabilire le topologie di rete che combinano connettività cross-premise con connettività di rete virtuale tra, come illustrato nel seguente diagramma hello:

![Informazioni sulle connessioni](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>Perché connettere reti virtuali?

Si consiglia le reti virtuali tooconnect per hello seguenti motivi:

* **Presenza e ridondanza in più aree geografiche**

  * È possibile configurare la sincronizzazione o la replica geografica con connettività sicura senza passare da endpoint con connessione Internet.
  * Con Gestione traffico e il servizio di bilanciamento del carico di Azure è possibile configurare il carico di lavoro a disponibilità elevata con ridondanza geografica in più aree di Azure. Un esempio importante è tooset SQL Always on con gruppi di disponibilità, la distribuzione tra più aree di Azure.
* **Applicazioni multilivello in singole aree geografiche con isolamento o limite amministrativo**

  * Hello nella stessa area, è possibile configurare applicazioni multilivello con più reti virtuali connesse a causa di tooisolation o i requisiti amministrativi.

Per ulteriori informazioni sulle connessioni di rete virtuale a, vedere hello [domande frequenti per rete virtuale a](#faq) alla fine di hello di questo articolo.

## <a name="which-set-of-steps-should-i-use"></a>Quale procedura è consigliabile seguire?

Questo articolo riporta due diverse procedure. Un set di passaggi per [hello di reti virtuali che si trovano nella stessa sottoscrizione](#samesub)e un altro per [reti virtuali che risiedono in diverse sottoscrizioni](#difsub). Hello differenza principale tra set hello è se è possibile creare e configurare tutte le risorse virtuali rete e gateway all'interno di hello stessa sessione di PowerShell.

Hello passaggi in questo articolo usano le variabili dichiarate all'inizio di hello di ogni sezione. Se si sono già lavorando con le reti virtuali esistenti, modificare impostazioni di hello variabili tooreflect hello nel proprio ambiente. Per usare la risoluzione dei nomi per le reti virtuali, vedere [Risoluzione dei nomi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

## <a name="samesub"></a>Come tooconnect reti virtuali che si trovano in hello stessa sottoscrizione

![Diagramma V2V](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare, è necessario tooinstall hello più recente dei cmdlet di Azure Resource Manager PowerShell hello, almeno 4.0 o versione successivo. Per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

### <a name="Step1"></a>Passaggio 1: Pianificare gli intervalli di indirizzi IP

In hello alla procedura seguente, vengono create due reti virtuali insieme le subnet gateway rispettivi e configurazioni. È quindi creare una connessione VPN tra hello due reti virtuali. È importante tooplan hello indirizzi IP per la configurazione di rete. Tenere presente che è necessario assicurarsi che nessuno di intervalli di rete virtuale o intervalli di rete locale si sovrappongano in alcun modo. In questi esempi non viene incluso un server DNS. Per usare la risoluzione dei nomi per le reti virtuali, vedere [Risoluzione dei nomi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Utilizziamo hello seguente i valori negli esempi di hello:

**Valori per TestVNet1:**

* Nome della rete virtuale: TestVNet1
* Gruppo di risorse: TestRG1
* Location: Stati Uniti orientali
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* IP pubblico: VNet1GWIP
* VPNType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Valori per TestVNet4:**

* Nome della rete virtuale: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Gruppo di risorse: TestRG4
* Località: Stati Uniti occidentali
* GatewayName: VNet4GW
* IP pubblico: VNet4GWIP
* VPNType: RouteBased
* Connessione: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Step2"></a>Passaggio 2: Creare e configurare TestVNet1

1. Dichiarare le variabili. In questo esempio dichiara variabili di hello utilizzando valori hello per questo esercizio. Nella maggior parte dei casi, è necessario sostituire i valori hello con valori personalizzati. Tuttavia, è possibile utilizzare queste variabili, se si eseguono tramite hello passaggi toobecome familiarità con questo tipo di configurazione. Modificare le variabili di hello se necessario, quindi copiare e incollarli nella console di PowerShell.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Connettere tooyour account. Utilizzare hello toohelp esempio che ci si connette seguenti:

  ```powershell
  Login-AzureRmAccount
  ```

  Controllare le sottoscrizioni di hello per account hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Specificare una sottoscrizione di hello che si desidera toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. Creare un nuovo gruppo di risorse.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. Creazione di configurazioni di subnet per TestVNet1 hello. L'esempio seguente mostra come creare una rete virtuale denominata TestVNet1 e tre subnet, denominate rispettivamente GatewaySubnet, FrontEnd e Backend. Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet. Se si assegnano altri nomi, la creazione del gateway ha esito negativo.

  Hello esempio seguente usa le variabili di hello impostato in precedenza. In questo esempio subnet del gateway hello utilizza un /27. Sebbene sia possibile toocreate assuma /29 una subnet del gateway, è consigliabile creare una subnet più grande che include più indirizzi selezionando almeno /28 o /27. In questo modo per sufficiente indirizzi tooaccommodate possibili configurazioni aggiuntive che è possibile in hello future.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. Creare TestVNet1.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. Pubblica IP indirizzo toobe toohello allocato gateway che si creerà per la rete virtuale della richiesta. Si noti che hello AllocationMethod è dinamico. È possibile specificare l'indirizzo IP hello che si desidera toouse. È il gateway tooyour allocata in modo dinamico. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Creare una configurazione del gateway hello. configurazione del gateway Hello definisce subnet hello e toouse di indirizzo IP pubblico hello. Utilizzare toocreate esempio hello la configurazione del gateway.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. Creare il gateway hello per TestVNet1. In questo passaggio viene creato il gateway di rete virtuale hello per le TestVNet1. Le configurazioni da rete virtuale a rete virtuale richiedono un tipo di VpnType RouteBased. Creazione di un gateway può richiedere spesso 45 minuti o più, a seconda di gateway selezionato hello SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>Passaggio 3 - Creare e configurare TestVNet4

Dopo aver configurato TestVNet1, creare TestVNet4. Eseguire operazioni di hello seguenti, sostituendo i valori hello con il proprio quando necessario. Questo passaggio può essere eseguito nell'hello stessa sessione di PowerShell perché si trova in hello stessa sottoscrizione.

1. Dichiarare le variabili. Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. Creare un nuovo gruppo di risorse.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Creazione di configurazioni di subnet per TestVNet4 hello.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. Creare TestVNet4.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. Richiedere un indirizzo IP pubblico.

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Creare una configurazione del gateway hello.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Creare il gateway TestVNet4 hello. Creazione di un gateway può richiedere spesso 45 minuti o più, a seconda di gateway selezionato hello SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>Passaggio 4: creare connessioni hello

1. Ottenere entrambi i gateway di rete virtuale. Se entrambi i gateway hello hello stessa sottoscrizione, come nell'esempio hello, è possibile completare questo passaggio in hello stessa sessione di PowerShell.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Creare hello TestVNet1 tooTestVNet4 connessione. In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet4. Verrà visualizzata una chiave condivisa a cui fa riferimento negli esempi di hello. È possibile utilizzare i valori per la chiave condivisa hello. cosa è la chiave condivisa hello importante Hello deve corrispondere per entrambe le connessioni. Creazione di una connessione può richiedere poco toocomplete.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Creare hello TestVNet4 tooTestVNet1 connessione. Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet4 tooTestVNet1. Assicurarsi che le chiavi condivise hello corrispondano. verrà stabilita connessione Hello dopo alcuni minuti.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. Verificare la connessione. Vedere la sezione hello [come tooverify connessione](#verify).

## <a name="difsub"></a>Come tooconnect reti virtuali che si trovano in sottoscrizioni diverse

![Diagramma V2V](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

In questo scenario vengono connesse le reti virtuali TestVNet1 e TestVNet5, che si trovano in sottoscrizioni diverse. le sottoscrizioni di Hello non è necessario toobe associato hello stesso tenant di Active Directory. Hello differenza tra questi passaggi e il set precedente hello consiste nel fatto che alcuni dei passaggi di configurazione hello necessario toobe eseguita in una sessione di PowerShell separata nel contesto di hello di sottoscrizione secondo hello. In particolare quando le sottoscrizioni di hello due appartengono toodifferent organizzazioni.

### <a name="step-5---create-and-configure-testvnet1"></a>Passaggio 5: Creare e configurare TestVNet1

È necessario completare [passaggio 1](#Step1) e [passaggio 2](#Step2) da hello precedente sezione toocreate e configurare TestVNet1 hello Gateway VPN per TestVNet1. Per questa configurazione, non è necessario toocreate TestVNet4 dalla sezione precedente hello, sebbene se viene creato, non creerà conflitti con questa procedura. Dopo aver completato i passaggi 1 e 2 di passaggio, continuare con passaggio 6 toocreate TestVNet5. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>Passaggio 6: verificare gli intervalli di indirizzi IP hello

È importante toomake assicurarsi che lo spazio di indirizzi IP hello di hello nuova rete virtuale, TestVNet5, non si sovrapponga ad altri di intervalli di rete virtuale o intervalli di gateway di rete locale. In questo esempio, le reti virtuali hello possono appartenere toodifferent organizzazioni. Per questo esercizio, è possibile utilizzare i seguenti valori per hello TestVNet5 hello:

**Valori per TestVNet5:**

* Nome della rete virtuale: TestVNet5
* Gruppo di risorse: TestRG5
* Ubicazione: Giappone orientale
* TestVNet5: 10.51.0.0/16 e 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* IP pubblico: VNet5GWIP
* VPNType: RouteBased
* Connessione: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>Passaggio 7: Creare e configurare TestVNet5

Questo passaggio deve essere eseguito nel contesto di hello della nuova sottoscrizione hello. Questa parte può essere eseguita dall'amministratore di hello in un'altra organizzazione che possiede la sottoscrizione hello.

1. Dichiarare le variabili. Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Connettersi toosubscription 5. Aprire la console di PowerShell e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

  ```powershell
  Login-AzureRmAccount
  ```

  Controllare le sottoscrizioni di hello per account hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Specificare una sottoscrizione di hello che si desidera toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. Creare un nuovo gruppo di risorse.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Creazione di configurazioni di subnet per TestVNet5 hello.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. Creare TestVNet5.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. Richiedere un indirizzo IP pubblico.

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Creare una configurazione del gateway hello.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Creare il gateway TestVNet5 hello.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>Passaggio 8: creare connessioni hello

In questo esempio, perché sono gateway hello in diverse sottoscrizioni hello, è stato suddividere questo passaggio in due sessioni di PowerShell contrassegnate come [sottoscrizione 1] e [sottoscrizione 5].

1. **[Sottoscrizione 1]**  Get gateway di rete virtuale hello per sottoscrizione 1. Accedere e connettersi tooSubscription 1 prima di eseguire l'esempio seguente hello:

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Copia output di hello di hello segue gli elementi e inviare questi amministratore toohello 5 sottoscrizione tramite posta elettronica o un altro metodo.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  Questi due elementi avrà toohello simile a valori output di esempio riportato di seguito:

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[Sottoscrizione 5]**  Get gateway di rete virtuale hello per 5 di sottoscrizione. Accedere e connettersi tooSubscription 5 prima di eseguire l'esempio seguente hello:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Copia output di hello di hello segue gli elementi e inviare questi amministratore toohello 1 sottoscrizione tramite posta elettronica o un altro metodo.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  Questi due elementi avrà toohello simile a valori output di esempio riportato di seguito:

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[Sottoscrizione 1]**  Creare hello TestVNet1 tooTestVNet5 connessione. In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet5. Hello differenza è che vnet5gw $ non è possibile ottenere direttamente perché si trova in una sottoscrizione diversa. È necessario toocreate un nuovo oggetto di PowerShell con i valori hello comunicati dal 1 sottoscrizione nei passaggi hello precedenti. Utilizzare l'esempio hello riportato di seguito. Sostituire i valori hello Name, Id e chiave condivisa. cosa è la chiave condivisa hello importante Hello deve corrispondere per entrambe le connessioni. Creazione di una connessione può richiedere poco toocomplete.

  Connettersi tooSubscription 1 prima di eseguire l'esempio seguente hello:

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[Sottoscrizione 5]**  Creare hello TestVNet5 tooTestVNet1 connessione. Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet5 tooTestVNet1. Hello stesso processo di creazione di un oggetto di PowerShell in base ai valori hello ottenuti da 1 a sottoscrizione applicabile in questo caso anche. In questo passaggio, assicurarsi che le chiavi condivise hello corrispondano.

  Connettersi tooSubscription 5 prima di eseguire l'esempio seguente hello:

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>Come tooverify una connessione

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Passaggi successivi

* Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Vedere hello [macchine virtuali-documentazione](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) per ulteriori informazioni.
* Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
