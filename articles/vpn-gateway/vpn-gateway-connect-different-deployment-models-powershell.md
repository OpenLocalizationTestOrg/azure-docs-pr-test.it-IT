---
title: 'Connettere le reti virtuali classiche tooAzure VNets Gestione risorse: PowerShell | Documenti Microsoft'
description: Informazioni su come toocreate una connessione VPN tra classico reti virtuali e Gestione risorse VNets tramite Gateway VPN e PowerShell
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>Connettere reti virtuali da diversi modelli di distribuzione usando PowerShell



Questo articolo illustra come tooconnect tooResource di reti virtuali classiche tooallow Manager VNets hello risorse che si trovano in toocommunicate di modelli di distribuzione separata hello tra loro. passaggi di Hello in questo articolo usano PowerShell, ma è anche possibile creare questa configurazione tramite il portale di Azure hello selezionando articolo hello da questo elenco.

> [!div class="op_single_selector"]
> * [Portale](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

La connessione di un classico tooa di rete virtuale VNet Gestione risorse è simile tooconnecting un percorso di rete virtuale tooan locale del sito. Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE. È possibile creare una connessione tra reti virtuali in sottoscrizioni diverse e in aree diverse. È inoltre possibile connettersi reti virtuali che dispone già di reti locali tooon di connessioni, come gateway hello che sono stati configurati con è dinamico o basato su route. Per ulteriori informazioni sulle connessioni di rete virtuale a, vedere hello [domande frequenti per rete virtuale a](#faq) alla fine di hello di questo articolo. 

Se le reti virtuali si trovano in hello stessa area, è opportuno prendere in considerazione tooinstead collegarli tramite Peering reti virtuali. Peering reti virtuali non usa un gateway VPN. Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md). 

## <a name="before-beginning"></a>Prima di iniziare

Hello passaggi seguenti consentono di eseguire hello le impostazioni necessarie tooconfigure un gateway dinamico o basato su route per ogni rete virtuale e creare una connessione VPN tra i gateway hello. Questa configurazione non supporta i gateway con routing statico o basati su criteri.

### <a name="prerequisites"></a>Prerequisiti

* Entrambe le reti virtuali sono già state create.
* Hello intervalli di indirizzi per hello reti virtuali non possono sovrapporsi tra loro o coincidere con tutti gli intervalli hello per le altre connessioni che il gateway hello potrebbe essere connessa di.
* È stato installato hello cmdlet più recenti di PowerShell. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni. Assicurarsi di installare hello servizio di gestione (SM) sia hello i cmdlet di gestione risorse (RM). 

### <a name="exampleref"></a>Impostazioni di esempio

È possibile utilizzare questi toocreate valori un ambiente di test, o fare riferimento toothem toobetter comprendere esempi hello in questo articolo.

**Impostazioni della rete virtuale classica**

Nome rete virtuale = ClassicVNet  <br>
Località = Stati Uniti occidentali <br>
Spazi degli indirizzi della rete virtuale = 10.0.0.0/24 <br>
Subnet-1 = 10.0.0.0/27 <br>
GatewaySubnet = 10.0.0.32/29 <br>
Nome della rete locale = RMVNetLocal <br>
GatewayType = DynamicRouting

**Impostazioni della rete virtuale di Resource Manager**

Nome della rete virtuale = RMVNet  <br>
Gruppo di risorse= RG1 <br>
Spazi degli indirizzi della rete virtuale = 192.168.0.0/16 <br>
Subnet-1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
Località = Stati Uniti orientali <br>
Nome IP pubblico del gateway = gwpip <br>
Gateway di rete locale = ClassicVNetLocal <br>
Nome gateway di rete virtuale = RMGateway <br>
Configurazione di indirizzamento IP del gateway = gwipconfig

## <a name="createsmgw"></a>Sezione 1 - configurare hello classic rete virtuale
### <a name="part-1---download-your-network-configuration-file"></a>Parte 1: Eseguire il download del file di configurazione di rete
1. Accedi tooyour account Azure nella console di PowerShell hello con diritti elevati. Hello seguente cmdlet richiede hello le credenziali di accesso per l'Account di Azure. Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell. Utilizzare hello toocomplete cmdlet PowerShell di Service Manager questa parte della configurazione di hello.

  ```powershell
  Add-AzureAccount
  ```
2. Esportare il file di configurazione di rete di Azure eseguendo hello comando seguente. È possibile modificare il percorso di hello hello tooexport tooa diversi della posizione del file se necessario.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. File con estensione XML aperti hello scaricato tooedit è. Per un esempio di file di configurazione di rete hello, vedere hello [dello Schema di configurazione di rete](https://msdn.microsoft.com/library/jj157100.aspx).

### <a name="part-2--verify-hello-gateway-subnet"></a>Parte 2 - verificare la subnet gateway hello
In hello **VirtualNetworkSites** elemento, aggiungere un tooyour subnet gateway rete virtuale se non ne è stato creato. Quando si utilizzano file di configurazione di rete hello, subnet del gateway hello devono essere denominati "GatewaySubnet" o Azure non è possibile riconoscere e utilizzarlo come una subnet del gateway.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**Esempio:**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>Parte 3: aggiungere il sito di rete locale hello
sito di rete locale Hello che è aggiungere rappresenta hello desiderato tooconnect toowhich di rete virtuale RM. Aggiungere un **LocalNetworkSites** elemento toohello file se non ne esiste già uno. A questo punto nella configurazione di hello, hello VPNGatewayAddress può essere qualsiasi indirizzo IP pubblico valido perché è non ancora creato il gateway di hello per hello VNet Gestione risorse. Quando si crea gateway hello, è necessario sostituire l'indirizzo IP segnaposto con hello corretto indirizzo IP pubblico assegnato gateway RM toohello.

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>Parte 4: associare il sito di rete locale hello hello rete virtuale
In questa sezione viene specificato il sito di rete locale hello che si desidera tooconnect hello tra. In questo caso, è hello VNet Gestione risorse che si è fatto riferimento in precedenza. In modo che nomi hello corrispondano. Questo passaggio non crea un gateway. Specifica rete locale hello hello gateway si connetterà.

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>Parte 5: salvare file hello e caricare
Salvare il file hello, quindi importarlo tooAzure eseguendo hello comando seguente. Assicurarsi di modificare il percorso di file hello come necessario per l'ambiente.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Verrà visualizzato un risultato simile che mostra che import hello ha avuto esito positivo.

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>Parte 6: creare gateway hello

Prima di eseguire questo esempio, fare riferimento toohello file di configurazione di rete che è stato scaricato per hello esatto dei nomi da Azure prevede toosee. file di configurazione di rete Hello contiene i valori hello per le reti virtuali classiche. In alcuni casi i nomi di hello per reti virtuali vengono modificate nel file di configurazione di rete hello durante la creazione di impostazioni di rete virtuale classiche in classica hello portale di Azure a causa delle differenze toohello nei modelli di distribuzione hello. Ad esempio, se si utilizza hello toocreate portale Azure, una rete virtuale classica denominato 'VNet classico' e creati in un gruppo di risorse denominato 'ClassicRG', nome hello contenuta nel file di configurazione di rete hello è convertito too'Group rete virtuale classica ClassicRG'. Quando si specifica il nome di hello di una rete virtuale che contiene spazi, utilizzare le virgolette per racchiudere valori hello.


Utilizzare hello seguente esempio toocreate un gateway con routing dinamico:

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

È possibile controllare lo stato di hello del gateway hello utilizzando hello **Get-AzureVNetGateway** cmdlet.

## <a name="creatermgw"></a>Sezione 2: Configurare il gateway di rete virtuale RM hello
un gateway VPN per rete virtuale RM, hello toocreate seguire hello attenendosi alle istruzioni. Non avviare passaggi hello fino a dopo aver recuperato l'indirizzo IP pubblico hello per gateway hello classic della rete virtuale. 

1. Accedi tooyour account Azure nella console di PowerShell hello. Hello seguente cmdlet richiede hello le credenziali di accesso per l'Account di Azure. Dopo l'accesso, le impostazioni dell'account vengono scaricate in modo che siano disponibili tooAzure PowerShell.

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  Ottenere un elenco delle sottoscrizioni di Azure se si dispone di più di una sottoscrizione.

  ```powershell
  Get-AzureRmSubscription
  ```
   
  Specificare una sottoscrizione di hello che si desidera toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Creare un gateway di rete locale. In una rete virtuale, gateway di rete locale hello si riferisce solitamente percorso locale tooyour. In questo caso, il gateway di rete locale hello fa riferimento tooyour rete virtuale classica. Assegnare un nome mediante il quale Azure può fare riferimento tooit e anche specificare prefisso dello spazio di indirizzo hello. Azure Usa prefisso dell'indirizzo IP hello è specificare tooidentify quali tooyour toosend traffico posizione locale. Se è necessario in un secondo momento, informazioni di hello tooadjust qui prima di creare il gateway, è possibile modificare i valori hello ed esempio hello esecuzione nuovamente.
   
   **-Nome** è il nome di hello da gateway di rete locale tooassign toorefer toohello.<br>
   **AddressPrefix -** è hello spazio di indirizzi per una rete virtuale classica.<br>
   **-GatewayIpAddress** è hello indirizzo IP pubblico del gateway hello classic della rete virtuale. Assicurarsi che l'indirizzo IP corretto di tooreflect hello di esempio seguenti hello toochange.<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. Richiedere un pubblico IP indirizzo toobe toohello allocato gateway di rete virtuale per Gestione risorse VNet hello. È possibile specificare l'indirizzo IP hello che si desidera toouse. indirizzo IP Hello viene allocata dinamicamente toohello gateway di rete virtuale. Tuttavia, ciò non significa modifiche all'indirizzo IP hello. tempo di Hello solo modifiche all'indirizzo IP gateway hello rete virtuale quando è hello gateway viene eliminato e ricreato. Non modifica in ridimensionamento, reimpostare o altri interni/aggiornamenti del gateway hello.

  In questo passaggio viene anche impostata una variabile che verrà usata in un passaggio successivo.

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. Verificare che la rete virtuale disponga di una subnet del gateway. Se non esiste alcuna subnet del gateway, aggiungerne una. Assicurarsi di subnet del gateway hello è denominata *GatewaySubnet*.
5. Recuperare subnet hello usata per il gateway hello eseguendo hello comando seguente. In questo passaggio, è inoltre possibile impostare una variabile toobe utilizzata nel passaggio successivo hello.
   
   **-Nome** nome hello di VNet il gestore delle risorse.<br>
   **-ResourceGroupName** è il gruppo di risorse hello che hello rete virtuale è associato. subnet del gateway Hello deve esistere per la rete virtuale e deve essere denominato *GatewaySubnet* toowork correttamente.<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. Creare una configurazione di indirizzamento IP del gateway hello. configurazione del gateway Hello definisce subnet hello e toouse di indirizzo IP pubblico hello. Utilizzare hello toocreate di esempio seguente la configurazione del gateway.

  In questo passaggio, hello **- struttura** e **- PublicIpAddressId** parametri devono essere passati proprietà id hello da hello subnet e oggetti di indirizzo IP, rispettivamente. Non è possibile usare una semplice stringa. Queste variabili vengono impostate in hello passaggio toorequest un indirizzo IP pubblico e hello passaggio tooretrieve hello subnet.

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. Creare i gateway di rete virtuale di gestione risorse di hello eseguendo hello comando seguente. Hello `-VpnType` deve essere *tipo RouteBased*. Può richiedere più di 45 minuti per toocreate gateway hello.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. Copiare l'indirizzo IP pubblico hello dopo aver creato gateway VPN hello. Utilizzare quando si configurano le impostazioni di rete locale hello per una rete virtuale classica. È possibile utilizzare hello seguente indirizzo IP pubblico di cmdlet tooretrieve hello. Hello indirizzo IP pubblico è elencato nella hello restituito come *IpAddress*.

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>Sezione 3: Modificare le impostazioni di hello classiche rete virtuale del sito locale

In questa sezione, è possibile utilizzare con hello classic rete virtuale. Sostituire l'indirizzo IP di segnaposto hello utilizzato quando si specificano le impostazioni di sito locale hello che verrà utilizzato tooconnect toohello gateway di gestione risorse VNet. 

1. Esportare i file di configurazione di rete hello.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Utilizzando un editor di testo, modificare il valore di hello per VPNGatewayAddress. Sostituire l'indirizzo IP segnaposto hello con indirizzo IP pubblico hello del gateway di gestione risorse di hello e quindi salvare le modifiche di hello.

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. Hello importazione modificato tooAzure file configurazione di rete.

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>Sezione 4: Creare una connessione tra gateway hello
Creazione di una connessione tra gateway hello richiede PowerShell. Potrebbe essere necessario tooadd la versione classica di hello toouse Account Azure hello di cmdlet di PowerShell. toodo in tal caso, utilizzare **Add-AzureAccount**.

1. Nella console di PowerShell hello, impostare la chiave condivisa. Prima di eseguire i cmdlet di hello, fare riferimento toohello file di configurazione di rete che è stato scaricato per hello esatto dei nomi da Azure prevede toosee. Quando si specifica il nome di hello di una rete virtuale che contiene spazi, utilizzare le virgolette singole per racchiudere valori hello.<br><br>Nell'esempio seguente, **- VNetName** nome hello di hello rete virtuale classica e **- LocalNetworkSiteName** hello nome specificato per il sito di rete locale hello. Hello **- SharedKey** è un valore che si generano e si specifica. Nell'esempio hello, abbiamo utilizzato "abc123", ma è possibile generare e utilizzare un nome più complesse. Hello importante cosa è il valore di hello specificato qui deve essere hello che stesso valore specificato nel passaggio successivo hello quando si crea la connessione. Hello restituito mostreranno **stato: ha esito positivo**.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. Creare una connessione VPN hello eseguendo i seguenti comandi hello:
   
  Impostare le variabili di hello.

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  Creare la connessione hello. Si noti che hello **- ConnectionType** IPSec, non Vnet2Vnet.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>Sezione 5: Verificare le connessioni

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>connessione hello tooverify il classico tooyour di rete virtuale VNet Gestione risorse

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Portale di Azure

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>connessione hello tooverify il tooyour VNet Gestione risorse di rete virtuale classica

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Portale di Azure

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

