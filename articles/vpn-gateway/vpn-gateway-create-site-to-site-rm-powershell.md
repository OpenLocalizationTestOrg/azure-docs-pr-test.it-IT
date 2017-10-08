---
title: 'Connettere il tooan di rete locale rete virtuale di Azure: VPN Site-to-Site: PowerShell | Documenti Microsoft'
description: "Passaggi toocreate una connessione IPsec da locale rete tooan rete virtuale di Azure su hello rete Internet pubblica. Questa procedura consentirà di creare una connessione gateway VPN da sito a sito cross-premise usando PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>Creare una rete virtuale con una connessione VPN da sito a sito usando PowerShell e Azure Resource Manager

Questo articolo illustra come connessione di PowerShell toocreate una Site-to-Site VPN gateway da locale toouse rete toohello rete virtuale. passaggi di Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Portale classico (versione classica)](vpn-gateway-site-to-site-create.md)
> 
>


Una connessione gateway VPN da sito a sito viene usato tooconnect tooan rete virtuale di Azure di rete locale tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2). Questo tipo di connessione richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico accessibile pubblicamente. Per altre informazioni sui gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).

![Diagramma della connessione cross-premise gateway VPN da sito a sito](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>Prima di iniziare

Verificare che siano stati soddisfatti i seguenti criteri prima di iniziare la configurazione di hello:

* Assicurarsi di disporre di un dispositivo VPN compatibile e un utente che è in grado di tooconfigure è. Per altre informazioni sui dispositivi VPN compatibili e sulla configurazione dei dispositivi, vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).
* Verificare di avere un indirizzo IPv4 pubblico esterno per il dispositivo VPN. L'indirizzo IP non può trovarsi dietro un NAT.
* Se non si ha familiarità con gli intervalli di indirizzi IP hello nello configurazione di rete locale, è necessario toocoordinate con qualcuno in grado di fornire i dettagli per l'utente. Quando si crea questa configurazione, è necessario specificare i prefissi intervallo indirizzi IP hello che Azure indirizzerà percorso locale tooyour. Nessuna delle subnet hello della rete locale può in giro con subnet della rete virtuale che si desidera tooconnect per hello.
* Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure. I cmdlet di PowerShell vengono aggiornati di frequente e sarà in genere necessario tooupdate il PowerShell cmdlet tooget hello funzionalità più recenti funzionalità. Se non vengono aggiornati i cmdlet di PowerShell, i valori hello specificati potrebbero non riuscire. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni su come scaricare e installare i cmdlet di PowerShell.

### <a name="example"></a>Valori di esempio

esempi di Hello in questo articolo utilizzano hello seguenti valori. È possibile utilizzare questi toocreate valori un ambiente di test, o fare riferimento toothem toobetter comprendere esempi hello in questo articolo.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Connettere tooyour sottoscrizione

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. Creare una rete virtuale e una subnet del gateway

Se non si ha una rete virtuale, crearne una. Quando si crea una rete virtuale, assicurarsi che gli spazi degli indirizzi hello specificato non si sovrappongano agli hello gli spazi degli indirizzi presenti nella rete locale.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate una rete virtuale e una subnet del gateway

Questo esempio crea una rete virtuale e una subnet del gateway. Se si dispone già di una rete virtuale, è necessario tooadd una subnet del gateway per visualizzare [tooadd una gateway subnet tooa rete virtuale è già stato creato](#gatewaysubnet).

Creare un gruppo di risorse:

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

Creare la rete virtuale.

1. Impostare le variabili di hello.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Creare hello rete virtuale.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>una rete virtuale di subnet tooa gateway tooadd è già stato creato

1. Impostare le variabili di hello.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Creare subnet del gateway hello.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Impostare la configurazione hello.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Creare il gateway di rete locale hello

gateway di rete locale Hello si riferisce solitamente percorso locale tooyour. Assegnare un nome mediante il quale Azure può fare riferimento tooit, quindi specificare l'indirizzo IP hello a sito di hello di toowhich di dispositivo VPN locale hello verrà creata una connessione. È inoltre possibile specificare i prefissi di indirizzo IP hello che verranno distribuiti tramite il dispositivo VPN toohello di hello VPN gateway. specificare i prefissi di indirizzo Hello sono prefissi hello presenti nella rete locale. Se la rete locale viene modificata, è possibile aggiornare facilmente i prefissi hello.

Utilizzare hello seguenti valori:

* Hello *GatewayIPAddress* hello di indirizzo IP del dispositivo VPN locale. Il dispositivo VPN non può trovarsi dietro un NAT.
* Hello *AddressPrefix* sono locale lo spazio degli indirizzi.

tooadd un gateway di rete locale con un singolo prefisso di indirizzo:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

tooadd un gateway di rete locale con più prefissi di indirizzo:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

toomodify prefissi di indirizzi IP per il gateway di rete locale:<br>
Talvolta è possibile modificare i prefissi del gateway di rete locale. passaggi di Hello vengono toomodify l'indirizzo IP prefissi dipendono dal fatto di aver creato una connessione gateway VPN. Vedere hello [prefissi di indirizzi IP di modifica di un gateway di rete locale](#modify) sezione di questo articolo.

## <a name="PublicIP"></a>4. Richiedere un indirizzo IP pubblico

Un gateway VPN deve avere un indirizzo IP pubblico. Richiesta innanzitutto la risorsa indirizzo IP hello e fare riferimento tooit durante la creazione del gateway di rete virtuale. indirizzo IP Hello viene assegnata dinamicamente toohello risorsa quando viene creato gateway VPN hello. Il gateway VPN supporta attualmente solo l'allocazione degli indirizzi IP pubblici *dinamici*. Non è possibile richiedere un'assegnazione degli indirizzi IP pubblici statici. Tuttavia, ciò non significa che l'indirizzo IP hello cambia dopo che è stato assegnato come gateway VPN tooyour. Hello unica volta in cui le modifiche all'indirizzo IP pubblico hello quando è hello gateway viene eliminato e ricreato. Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway VPN.

Richiedere un indirizzo IP pubblico che verrà assegnato tooyour di gateway VPN di rete virtuale.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Creare una configurazione di indirizzamento IP del gateway hello

configurazione del gateway Hello definisce subnet hello e toouse di indirizzo IP pubblico hello. Utilizzare la configurazione del gateway di hello toocreate riportato di seguito:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Creare il gateway VPN hello

Creare il gateway VPN di rete virtuale hello. Creazione di un gateway VPN può richiedere too45 minuti o più toocomplete.

Utilizzare hello seguenti valori:

* Hello *- il tipo di gateway* per un sito a sito è configurazione *Vpn*. tipo di gateway Hello è sempre configurazione toohello specifico che si sta implementando. Ad esempio, altre configurazioni di gateway possono richiedere -GatewayType ExpressRoute.
* Hello *- VpnType* può essere *tipo RouteBased* (definita tooas un Gateway dinamico nella parte della documentazione), o *basato su criteri* (denominato tooas un Gateway statico in una parte della documentazione ). Per altre informazioni sui tipi di gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).
* Selezionare hello SKU di Gateway che si desidera toouse. Esistono limitazioni di configurazione per alcuni SKU. Per altre informazioni, vedere [SKU del gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku). Se si verifica un errore durante la creazione di gateway VPN hello riguardanti hello - GatewaySku, verificare di aver installato una versione più recente di hello hello di cmdlet di PowerShell.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. Configurare il dispositivo VPN

Rete locale tooan di connessioni da sito a sito richiedono un dispositivo VPN. In questo passaggio viene configurato il dispositivo VPN. Quando si configura il dispositivo VPN, è necessario hello segue:

- Chiave condivisa. Questo è hello stesso condiviso chiave specificate al momento della creazione della connessione VPN da sito a sito. In questi esempi viene usata una chiave condivisa semplice. Si consiglia di generare un toouse chiave più complesse.
- Hello indirizzo IP pubblico del gateway di rete virtuale. È possibile visualizzare l'indirizzo IP pubblico hello utilizzando hello portale di Azure, PowerShell o CLI. hello toofind indirizzo IP pubblico del gateway di rete virtuale con PowerShell, usare hello esempio seguente:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Creare la connessione VPN hello

Creare quindi connessione Site-to-Site VPN hello tra il gateway di rete virtuale e il dispositivo VPN. Essere certi tooreplace hello i valori con valori personalizzati. chiave condivisa Hello deve corrispondere il valore di hello utilizzato per la configurazione del dispositivo VPN. Si noti che hello '-ConnectionType' per il sito a sito è *IPsec*.

1. Impostare le variabili di hello.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Creare la connessione hello.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

Poco dopo, hello connessione verrà stabilita.

## <a name="toverify"></a>9. Verificare una connessione VPN hello

Esistono alcuni modi diversi tooverify la connessione VPN.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>macchina virtuale di tooconnect tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>Modificare i prefissi degli indirizzi IP per un gateway di rete locale

Se i prefissi di indirizzi IP hello indirizzato percorso locale tooyour da modificano, è possibile modificare il gateway di rete locale hello. Sono disponibili due set di istruzioni. istruzioni di Hello che prescelto variano a seconda se è già stato creato la connessione del gateway.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>Modificare l'indirizzo IP del gateway hello per un gateway di rete locale

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Passaggi successivi

*  Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
