---
title: 'Connettere il tooan di rete locale rete virtuale di Azure: VPN Site-to-Site: portale | Documenti Microsoft'
description: Passaggi toocreate una connessione IPsec da locale rete tooan rete virtuale di Azure su hello rete Internet pubblica. Questi passaggi consentono di creare una connessione Site-to-Site VPN Gateway cross-premise usando il portale di hello.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Creare una connessione Site-to-Site nel portale di Azure hello

Questo articolo illustra come toouse hello toocreate portale Azure una connessione gateway VPN da sito a sito dal toohello di rete locale rete virtuale. passaggi di Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Una connessione gateway VPN da sito a sito viene usato tooconnect tooan rete virtuale di Azure di rete locale tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2). Questo tipo di connessione richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico accessibile pubblicamente. Per altre informazioni sui gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).

![Diagramma della connessione cross-premise gateway VPN da sito a sito](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Prima di iniziare

Verificare che siano stati soddisfatti i seguenti criteri prima di iniziare la configurazione di hello:

* Assicurarsi di disporre di un dispositivo VPN compatibile e un utente che è in grado di tooconfigure è. Per altre informazioni sui dispositivi VPN compatibili e sulla configurazione dei dispositivi, vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).
* Verificare di avere un indirizzo IPv4 pubblico esterno per il dispositivo VPN. L'indirizzo IP non può trovarsi dietro un NAT.
* Se non si ha familiarità con gli intervalli di indirizzi IP hello nello configurazione di rete locale, è necessario toocoordinate con qualcuno in grado di fornire i dettagli per l'utente. Quando si crea questa configurazione, è necessario specificare i prefissi intervallo indirizzi IP hello che Azure indirizzerà percorso locale tooyour. Nessuna delle subnet hello della rete locale può in giro con subnet della rete virtuale che si desidera tooconnect per hello. 

### <a name="values"></a>Valori di esempio

esempi di Hello in questo articolo utilizzano hello seguenti valori. È possibile utilizzare questi toocreate valori un ambiente di test, o fare riferimento toothem toobetter comprendere esempi hello in questo articolo.

* **Nome della rete virtuale:** TestVNet1
* **Spazio di indirizzi:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (facoltativo per questo esercizio)
* **Subnet:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (facoltativo per questo esercizio)
* **GatewaySubnet:** 10.11.255.0/27
* **Gruppo di risorse:** TestRG1
* **Località:** Stati Uniti orientali
* **Server DNS:** facoltativo. indirizzo IP di Hello del server DNS.
* **Nome gateway di rete virtuale:** VNet1GW
* **IP pubblico:** VNet1GWIP
* **Tipo VPN:** Basato su route
* **Tipo di connessione:** Da sito a sito (IPSec)
* **Tipo di gateway:** VPN
* **Nome del gateway di rete locale:** Site2
* **Nome connessione:** VNet1toSite2

## <a name="CreatVNet"></a>1. Crea rete virtuale

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Specificare un server DNS

DNS non è necessario toocreate una Site-to-Site connessione. Tuttavia, se si desidera la risoluzione dei nomi toohave per le risorse di rete virtuale tooyour distribuito, specificare un server DNS. Questa impostazione consente di specificare i server DNS hello che si vuole toouse per la risoluzione dei nomi per la rete virtuale. Non comporta la creazione di un server DNS. Per altre informazioni sulla risoluzione dei nomi, vedere [Risoluzione dei nomi per le macchine virtuali e le istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Creare subnet del gateway hello

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Creare il gateway VPN hello

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Creare il gateway di rete locale hello

gateway di rete locale Hello si riferisce solitamente percorso locale tooyour. Assegnare un nome mediante il quale Azure può fare riferimento tooit, quindi specificare l'indirizzo IP hello a sito di hello di toowhich di dispositivo VPN locale hello verrà creata una connessione. È inoltre possibile specificare i prefissi di indirizzo IP hello che verranno distribuiti tramite il dispositivo VPN toohello di hello VPN gateway. specificare i prefissi di indirizzo Hello sono prefissi hello presenti nella rete locale. Se le modifiche di rete locale o è necessario toochange hello indirizzo IP dispositivo VPN hello, è possibile aggiornare facilmente valori hello in un secondo momento.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Configurare il dispositivo VPN

Rete locale tooan di connessioni da sito a sito richiedono un dispositivo VPN. In questo passaggio viene configurato il dispositivo VPN. Quando si configura il dispositivo VPN, è necessario hello segue:

- Chiave condivisa. Questo è hello stesso condiviso chiave specificate al momento della creazione della connessione VPN da sito a sito. In questi esempi viene usata una chiave condivisa semplice. Si consiglia di generare un toouse chiave più complesse.
- Hello indirizzo IP pubblico del gateway di rete virtuale. È possibile visualizzare l'indirizzo IP pubblico hello utilizzando hello portale di Azure, PowerShell o CLI. hello toofind indirizzo IP pubblico del gateway VPN usando il portale di Azure, hello passare troppo**gateway di rete virtuale**, quindi fare clic su nome hello del gateway.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Creare la connessione VPN hello

Creare la connessione VPN Site-to-Site hello tra il gateway di rete virtuale e il dispositivo VPN locale.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Verificare una connessione VPN hello

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>macchina virtuale di tooconnect tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>Come tooreset un gateway VPN

La reimpostazione del gateway VPN di Azure è utile se si perde la connettività VPN cross-premise in uno o più tunnel VPN da sito a sito. In questo caso, i dispositivi VPN locali sono tutte le funzioni correttamente, ma sono tooestablish non è possibile tunnel IPsec con gateway VPN di Azure hello. Per la procedura da seguire, vedere [Reimpostare un gateway VPN](vpn-gateway-resetgw-classic.md).

## <a name="resize"></a>Come toochange un gateway SKU (ridimensionare un gateway)

Per hello passaggi toochange un SKU di gateway, vedere [SKU di Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="next-steps"></a>Passaggi successivi

* Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Per informazioni sul tunneling forzato, vedere [Informazioni sul tunneling forzato](vpn-gateway-forced-tunneling-rm.md).
* Per informazioni sulle connessioni da rete attiva a rete attiva a disponibilità elevata, vedere [Connettività cross-premise e da rete virtuale a rete virtuale a disponibilità elevata](vpn-gateway-highlyavailable.md).
