---
title: 'Connettere il tooan di rete locale rete virtuale di Azure: VPN Site-to-Site: CLI | Documenti Microsoft'
description: "Passaggi toocreate una connessione IPsec da locale rete tooan rete virtuale di Azure su hello rete Internet pubblica. Questa procedura consentirà di creare una connessione gateway VPN da sito a sito cross-premise usando l'interfaccia della riga di comando."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>Creare una rete virtuale con una connessione VPN da sito a sito usando l'interfaccia della riga di comando

Questo articolo illustra come toouse hello Azure CLI toocreate una connessione gateway VPN da sito a sito dal toohello di rete locale rete virtuale. passaggi di Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:<br>

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagramma della connessione cross-premise gateway VPN da sito a sito](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

Una connessione gateway VPN da sito a sito viene usato tooconnect tooan rete virtuale di Azure di rete locale tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2). Questo tipo di connessione richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico accessibile pubblicamente. Per altre informazioni sui gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).

## <a name="before-you-begin"></a>Prima di iniziare

Verificare che siano stati soddisfatti i seguenti criteri prima di iniziare la configurazione di hello:

* Assicurarsi di disporre di un dispositivo VPN compatibile e un utente che è in grado di tooconfigure è. Per altre informazioni sui dispositivi VPN compatibili e sulla configurazione dei dispositivi, vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).
* Verificare di avere un indirizzo IPv4 pubblico esterno per il dispositivo VPN. L'indirizzo IP non può trovarsi dietro un NAT.
* Se non si ha familiarità con gli intervalli di indirizzi IP hello nello configurazione di rete locale, è necessario toocoordinate con qualcuno in grado di fornire i dettagli per l'utente. Quando si crea questa configurazione, è necessario specificare i prefissi intervallo indirizzi IP hello che Azure indirizzerà percorso locale tooyour. Nessuna delle subnet hello della rete locale può in giro con subnet della rete virtuale che si desidera tooconnect per hello.
* Verificare di aver installato la versione più recente di comandi CLI di hello (2.0 o versione successiva). Per informazioni sull'installazione di comandi CLI hello, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli) e [Introduzione a Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).

### <a name="example"></a>Valori di esempio

È possibile utilizzare hello seguente valori toocreate un ambiente di test, o fare riferimento a valori toothese toobetter comprendere esempi hello in questo articolo:

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1. Connettere tooyour sottoscrizione

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. Creare un gruppo di risorse

Hello seguente viene creato un gruppo di risorse denominato 'TestRG1' nel percorso 'eastus' hello. Se si dispone già di un gruppo di risorse nell'area di hello che si desidera toocreate la rete virtuale, è possibile utilizzare invece che uno.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. Crea rete virtuale

Se si dispone già di una rete virtuale, crearne uno utilizzando hello [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create) comando. Quando si crea una rete virtuale, assicurarsi che gli spazi degli indirizzi hello specificato non si sovrappongano agli hello gli spazi degli indirizzi presenti nella rete locale.

Hello seguente viene creata una rete virtuale denominata 'TestVNet1' e una subnet, 'Subnet1'.

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Creare subnet del gateway hello

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

Per questa configurazione, è necessaria anche una subnet del gateway. gateway di rete virtuale Hello utilizza una subnet del gateway che contiene gli indirizzi IP hello utilizzate dai servizi gateway VPN di hello. Quando si crea una subnet del gateway, deve essere denominata "GatewaySubnet". Se si assegna un nome diverso, la subnet viene creata, ma non verrà trattata da Azure come una subnet del gateway.

dimensioni Hello di subnet del gateway hello specificati dipendono dalla configurazione di gateway VPN hello che si desidera toocreate. Sebbene sia possibile toocreate assuma /29 una subnet del gateway, è consigliabile creare una subnet più grande che include più indirizzi selezionando /27 o /28. Utilizzando una subnet del gateway più grande consente sufficiente IP indirizzi tooaccommodate future configurazioni possibili.

Hello utilizzare [creare subnet della rete virtuale rete az](/cli/azure/network/vnet/subnet#create) subnet del gateway hello toocreate comando.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Creare il gateway di rete locale hello

gateway di rete locale Hello si riferisce solitamente percorso locale tooyour. Assegnare un nome mediante il quale Azure può fare riferimento tooit, quindi specificare l'indirizzo IP hello a sito di hello di toowhich di dispositivo VPN locale hello verrà creata una connessione. È inoltre possibile specificare i prefissi di indirizzo IP hello che verranno distribuiti tramite il dispositivo VPN toohello di hello VPN gateway. specificare i prefissi di indirizzo Hello sono prefissi hello presenti nella rete locale. Se la rete locale viene modificata, è possibile aggiornare facilmente i prefissi hello.

Utilizzare hello seguenti valori:

* Hello *--indirizzo ip del gateway* hello di indirizzo IP del dispositivo VPN locale. Il dispositivo VPN non può trovarsi dietro un NAT.
* Hello *-prefissi di indirizzi locale* sono di spazi degli indirizzi locale.

Hello utilizzare [locale-gateway di rete az creare](/cli/azure/network/local-gateway#create) comando tooadd un gateway di rete locale con più prefissi di indirizzo:

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. Richiedere un indirizzo IP pubblico

Un gateway VPN deve avere un indirizzo IP pubblico. Richiesta innanzitutto la risorsa indirizzo IP hello e fare riferimento tooit durante la creazione del gateway di rete virtuale. indirizzo IP Hello viene assegnata dinamicamente toohello risorsa quando viene creato gateway VPN hello. Il gateway VPN supporta attualmente solo l'allocazione degli indirizzi IP pubblici *dinamici*. Non è possibile richiedere un'assegnazione degli indirizzi IP pubblici statici. Tuttavia, ciò non significa che l'indirizzo IP hello cambia dopo che è stato assegnato come gateway VPN tooyour. Hello unica volta in cui le modifiche all'indirizzo IP pubblico hello quando è hello gateway viene eliminato e ricreato. Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway VPN.

Hello utilizzare [az rete public-ip creare](/cli/azure/network/public-ip#create) comando toorequest un indirizzo IP pubblico dinamica.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Creare il gateway VPN hello

Creare il gateway VPN di rete virtuale hello. Creazione di un gateway VPN può richiedere too45 minuti o più toocomplete.

Utilizzare hello seguenti valori:

* Hello *-tipo di gateway* per un sito a sito è configurazione *Vpn*. tipo di gateway Hello è sempre configurazione toohello specifico che si sta implementando. Per altre informazioni, vedere [Tipi di gateway](vpn-gateway-about-vpn-gateway-settings.md#gwtype).
* Hello *- vpn-tipo* può essere *tipo RouteBased* (definita tooas un Gateway dinamico nella parte della documentazione), o *basato su criteri* (tooas un Gateway statico in alcune definito documentazione). impostazione di Hello è toorequirements specifico del dispositivo hello che si desidera connettersi. Per altre informazioni sui tipi di gateway VPN, vedere [Informazioni sulle impostazioni di configurazione del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).
* Selezionare hello SKU di Gateway che si desidera toouse. Esistono limitazioni di configurazione per alcuni SKU. Per altre informazioni, vedere [SKU del gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

Creare il gateway VPN hello utilizzando hello [creare reti virtuali-gateway di rete az](/cli/azure/network/vnet-gateway#create) comando. Se si esegue questo comando hello utilizzando il parametro '-- Nessun - wait', non sono visibili eventuali commenti e suggerimenti o output. Questo parametro consente toocreate gateway hello in background hello. Sono necessari circa 45 minuti toocreate un gateway.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. Configurare il dispositivo VPN

Rete locale tooan di connessioni da sito a sito richiedono un dispositivo VPN. In questo passaggio viene configurato il dispositivo VPN. Quando si configura il dispositivo VPN, è necessario hello segue:

- Chiave condivisa. Questo è hello stesso condiviso chiave specificate al momento della creazione della connessione VPN da sito a sito. In questi esempi viene usata una chiave condivisa semplice. Si consiglia di generare un toouse chiave più complesse.
- Hello indirizzo IP pubblico del gateway di rete virtuale. È possibile visualizzare l'indirizzo IP pubblico hello utilizzando hello portale di Azure, PowerShell o CLI. toofind hello indirizzo IP pubblico del gateway di rete virtuale, utilizzare hello [elenco public-ip di rete az](/cli/azure/network/public-ip#list) comando. Per facilitare la lettura, output di hello è elenco hello toodisplay formattato di indirizzi IP pubblici in formato tabella.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Creare la connessione VPN hello

Creare la connessione VPN Site-to-Site hello tra il gateway di rete virtuale e il dispositivo VPN locale. Retribuzione particolare attenzione toohello condiviso valore chiave, che deve corrispondere a hello configurato condivisa valore della chiave per il dispositivo VPN.

Creare una connessione hello utilizzando hello [az vpn di rete-connessione creare](/cli/azure/network/vpn-connection#create) comando.

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

Poco dopo, hello connessione verrà stabilita.

## <a name="toverify"></a>10. Verificare una connessione VPN hello

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

Se si desidera toouse un altro metodo tooverify la connessione, vedere [verificare una connessione VPN Gateway](vpn-gateway-verify-connection-resource-manager.md).

## <a name="connectVM"></a>macchina virtuale di tooconnect tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>Attività comuni

Questa sezione contiene i comandi comuni che risultano utili quando si usano configurazioni da sito a sito. Per hello l'elenco completo di comandi CLI di rete, vedere [CLI di Azure - rete](/cli/azure/network).

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>Passaggi successivi

* Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Per informazioni sul tunneling forzato, vedere [Informazioni sul tunneling forzato](vpn-gateway-forced-tunneling-rm.md).
* Per informazioni sulle connessioni da rete attiva a rete attiva a disponibilità elevata, vedere [Connettività cross-premise e da rete virtuale a rete virtuale a disponibilità elevata](vpn-gateway-highlyavailable.md).
* Per un elenco di comandi dell'interfaccia della riga di comando di Azure di rete, vedere [Azure CLI](https://docs.microsoft.com/cli/azure/network) (Interfaccia della riga di comando di Azure).