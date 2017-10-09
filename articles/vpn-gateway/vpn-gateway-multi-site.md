---
title: 'Connettere i siti di toomultiple una rete virtuale tramite il Gateway VPN e PowerShell: classico | Documenti Microsoft'
description: "In questo articolo verrà illustrata la connessione più locale siti tooa rete virtuale usando un Gateway VPN per il modello di distribuzione classica hello."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Aggiungere un tooa di connessione da sito a sito rete virtuale con una connessione di gateway VPN esistente (classica)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (classico)](vpn-gateway-multi-site.md)
>
>

Questo articolo viene illustrato l'utilizzo di PowerShell tooadd da sito a sito (S2S) connessioni tooa gateway VPN con una connessione esistente. Questo tipo di connessione è spesso tooas cui una configurazione "multi-site". Hello passaggi in questo articolo si applicano le reti toovirtual create utilizzando il modello di distribuzione classica hello (noto anche come servizio di gestione). Questi passaggi non vengono applicano le configurazioni di connessione coesistenti tooExpressRoute/Site-to-Site.

### <a name="deployment-models-and-methods"></a>Metodi e modelli di distribuzione

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Questa tabella viene aggiornata man mano che per questa configurazione diventano disponibili nuovi articoli e altri strumenti. Quando un articolo è disponibile, è un collegamento direttamente tooit da questa tabella.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>Informazioni sulla connessione

È possibile connettere più locale siti tooa singola rete virtuale. Ciò è particolarmente interessante per la creazione di soluzioni per cloud ibride. Creazione di un gateway di rete virtuale di Azure tooyour connessione multisito è simile toocreating altre connessioni da sito a sito. In effetti, è possibile utilizzare un gateway VPN di Azure esistente, purché il gateway hello è dinamico (basato su route).

Se si dispone già di una rete virtuale connessa tooyour di gateway statico, è possibile modificare hello gateway tipo toodynamic senza la necessità di rete virtuale di toorebuild hello in più siti di ordine tooaccommodate. Prima di modificare il tipo di routing hello, assicurarsi che il gateway VPN locale supporta le configurazioni VPN basate su route.

![diagramma multisito](./media/vpn-gateway-multi-site/multisite.png "multisito")

## <a name="points-tooconsider"></a>Tooconsider punti

**Non sarà di rete virtuale di toouse in grado di hello toomake portale modifiche toothis.** È necessario toomake file di configurazione di rete toohello a modifiche anziché portale hello. Se si apportano modifiche nel portale di hello, queste sovrascrivono le impostazioni di riferimenti multisito per la rete virtuale.

È consigliabile familiarizzare tramite file di configurazione di rete hello ora hello termine procedura multisito hello. Tuttavia, se si dispone di più persone che lavorano alla configurazione di rete, è necessario assicurarsi che siano tutte a conoscenza questa limitazione toomake. Questo non significa che è possibile usare il portale di hello affatto. È possibile utilizzare, per tutti gli altri, ad eccezione di rete virtuale specifica toothis configurazione modifiche apportare.

## <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare la configurazione, verificare di aver seguito hello:

* Hardware VPN compatibile per ogni sede locale. Controllare [informazioni sui dispositivi VPN per la connettività di rete virtuale](vpn-gateway-about-vpn-devices.md) tooverify se hello periferica che si desidera toouse noto toobe compatibile.
* Un indirizzo IP IPv4 pubblico esterno per ogni dispositivo VPN. indirizzo IP di Hello non può trovarsi dietro un NAT. Questo è un requisito.
* È necessario tooinstall hello più recente di hello cmdlet di Azure PowerShell. Assicurarsi di installare versione di gestione del servizio (SM) hello nella versione di gestione risorse toohello aggiunta. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni.
* Una persona esperta nella configurazione di hardware VPN. È necessario toohave un'ottima conoscenza delle procedure tooconfigure il dispositivo VPN o con un utente che esegue il lavoro.
* intervalli di indirizzi IP Hello che si desidera toouse per la rete virtuale (se è ancora stato creato uno).
* intervalli di indirizzi IP Hello per ognuno dei siti di rete locale hello che si sarà possibile connettersi. È necessario assicurarsi che per ognuno dei siti di rete locale hello che si desidera tooconnect toodo non si sovrappongono gli intervalli di indirizzi IP di hello toomake. In caso contrario, il portale di hello o hello API REST rifiuterà configurazione hello in fase di caricamento.<br>Ad esempio, se si dispone di due siti di rete locale che contengono entrambe hello IP indirizzo intervallo 10.2.3.0/24 e di disporre di un pacchetto con un indirizzo di destinazione 10.2.3.3, Azure non saprà quale sito sono intervalli di indirizzi hello toosend hello pacchetto toobecause sovrapposti. problemi di routing tooprevent, Azure non consente tooupload un file di configurazione con intervalli sovrapposti.

## <a name="1-create-a-site-to-site-vpn"></a>1. Creare una VPN da sito a sito
Se già si dispone di una VPN da sito a sito con un gateway di routing dinamico, eseguire l'operazione seguente. È possibile procedere troppo[esportare le impostazioni di configurazione di rete virtuale hello](#export). In caso contrario, hello seguenti:

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>Se già si ha a disposizione una rete virtuale da sito a sito, ma con un gateway di routing statico basato su criteri:
1. Modificare il ciclo di gateway tipo toodynamic. Una VPN multisito richiede un gateway di routing dinamico, ovvero basato su route. digitare il gateway toochange, sarà necessario toofirst delete hello esistente gateway, quindi crearne uno nuovo. Per istruzioni, vedere [come toochange hello tipo per il gateway di routing VPN](vpn-gateway-configure-vpn-gateway-mp.md).  
2. Configurare il nuovo gateway e creare il proprio tunnel VPN. Per istruzioni, vedere [configurare un Gateway VPN nel portale di Azure classico hello](vpn-gateway-configure-vpn-gateway-mp.md). In primo luogo, modificare il ciclo di gateway tipo toodynamic.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>Se non si ha a disposizione una rete virtuale da sito a sito:
1. Creare la rete virtuale da sito a sito usando queste istruzioni: [creare una rete virtuale con una connessione VPN da sito a sito nel portale di Azure classico hello](vpn-gateway-site-to-site-create.md).  
2. Configurare un gateway di routing dinamico usando le istruzioni seguenti: [Configurare un gateway VPN](vpn-gateway-configure-vpn-gateway-mp.md). Tooselect assicurarsi di essere **routing dinamico** per il tipo di gateway.

## <a name="export"></a>2. Esportare i file di configurazione di rete hello
Esportare il file di configurazione di rete di Azure eseguendo hello comando seguente. È possibile modificare il percorso di hello hello tooexport tooa diversi della posizione del file se necessario.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. File di configurazione di rete aprire hello
Aprire i file di configurazione di rete hello scaricato nell'ultimo passaggio hello. Usare qualsiasi editor xml desiderato. file Hello dovrebbe essere simile toohello seguenti:

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Aggiungere riferimenti a più siti
Quando si aggiungono o rimuovono informazioni di riferimento del sito, si apportano modifiche di configurazione toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef. Aggiunta di un nuovo riferimento al sito locale attiva toocreate Azure un nuovo tunnel. Nell'esempio hello seguente la configurazione di rete hello è per la connessione a un singolo sito. Dopo aver apportato le modifiche, salvare file hello.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

tooadd altri riferimenti a siti (creare una configurazione multisita), è sufficiente aggiungere le righe aggiuntive "LocalNetworkSiteRef", come illustrato nell'esempio hello riportato di seguito:

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. File di configurazione di rete hello importazione
Importare i file di configurazione di rete hello. Quando si importa questo file con modifiche hello, verranno aggiunti nuovi tunnel hello. Hello che useranno gateway dinamico hello creato in precedenza. È possibile utilizzare portale classico hello o file hello tooimport di PowerShell.

## <a name="6-download-keys"></a>6. Chiavi di download
Dopo aver aggiunto i nuovi tunnel, usare hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello chiavi IPsec/IKE già condivise per ogni tunnel.

ad esempio:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

Se si preferisce, è possibile utilizzare anche hello *Get Virtual Network Gateway Shared Key* tooget API REST hello chiavi già condivise.

## <a name="7-verify-your-connections"></a>7. Verificare le connessioni
Controllare lo stato di hello tunnel multisito. Dopo aver scaricato le chiavi di hello per ogni tunnel, è opportuno tooverify connessioni. Utilizzare tooget 'Get-AzureVnetConnection' tunnel un elenco di rete virtuale, come illustrato nel seguente esempio hello. VNet1 è il nome di hello di hello rete virtuale.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

Esempio restituito:

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni sui gateway VPN, vedere [sul gateway VPN](vpn-gateway-about-vpngateways.md).
