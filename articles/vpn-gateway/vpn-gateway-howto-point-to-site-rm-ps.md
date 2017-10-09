---
title: 'Connettersi a una rete virtuale di Azure utilizzando Point-to-Site di tooan computer e l''autenticazione del certificato: PowerShell | Documenti Microsoft'
description: Consente di connettersi in modo sicuro una rete virtuale di tooyour computer mediante la creazione di una connessione di gateway VPN Point-to-Site utilizzando l'autenticazione del certificato. In questo articolo si applica al modello di distribuzione di gestione delle risorse toohello e utilizza PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>Configurare un tooa connessione Point-to-Site rete virtuale utilizzando l'autenticazione del certificato: PowerShell

In questo articolo viene illustrato come una rete virtuale con una connessione Point-to-Site nella distribuzione di gestione risorse di hello toocreate modello tramite PowerShell. Questa configurazione utilizza hello tooauthenticate certificati connessione del client. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Un gateway VPN da punto a sito (P2S) consente di creare una rete virtuale tooyour di connessione protetta da un computer client. Le connessioni VPN Point-to-Site sono utili quando si desidera tooconnect tooyour rete virtuale da una posizione remota, ad esempio quando sono il telelavoro da casa o di una conferenza. Una VPN P2S è anche un toouse soluzione utile anziché una VPN da sito a sito quando si dispone solo alcuni client che richiedono tooconnect tooa rete virtuale.

Usa P2S hello SSTP Secure Socket Tunneling Protocol (), che è un protocollo di rete VPN basata su SSL. Viene stabilita una connessione di VPN P2S avviandolo dal computer client hello.

![Connettersi a una rete virtuale di Azure - diagramma di connessione Point-to-Site di tooan computer](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

Connessioni di autenticazione Point-to-Site certificato requisiti hello:

* Un gateway VPN RouteBased.
* Hello chiave pubblica (file con estensione cer) per un certificato radice, ovvero tooAzure caricato. Una volta caricato il certificato di hello, viene considerato un certificato attendibile e viene utilizzato per l'autenticazione.
* Un certificato client è generato dal certificato radice hello e installato in ogni computer client che si connetteranno toohello rete virtuale. Questo certificato viene usato per l'autenticazione client.
* Un pacchetto di configurazione del client VPN. pacchetto di configurazione client VPN Hello contiene le informazioni necessarie hello per hello client tooconnect toohello rete virtuale. pacchetto di Hello Configura hello esistente client VPN è toohello nativo del sistema operativo Windows. Ogni client che si connette devono essere configurate tramite il pacchetto di configurazione di hello.

Le connessioni da punto a sito non richiedono un dispositivo VPN o un indirizzo IP pubblico locale. connessione VPN Hello viene creato tramite SSTP (Secure Socket Tunneling Protocol). Sul lato server hello è supporta le versioni SSTP 1.0, 1.1 e 1.2. client Hello decide quali toouse versione. Per Windows 8.1 e versioni successive, SSTP usa per impostazione predefinita la versione 1.2. 

Per ulteriori informazioni sulle connessioni Point-to-Site, vedere hello [Point-to-Site domande frequenti su](#faq) alla fine di hello di questo articolo.

## <a name="before-beginning"></a>Prima di iniziare

* Verificare di possedere una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial).
* Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure. Per ulteriori informazioni sull'installazione dei cmdlet di PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

### <a name="example"></a>Valori di esempio

È possibile utilizzare toocreate valori di esempio hello un ambiente di test, o fare riferimento a valori toothese toobetter comprendere esempi hello in questo articolo. Le variabili di hello è impostata nella sezione [1](#declare) dell'articolo hello. È possibile utilizzare i passaggi di hello come una procedura dettagliata e utilizzare i valori hello senza alcuna modifica o modificarle tooreflect l'ambiente. 

* **Nome: VNet1**
* **Spazio degli indirizzi: 192.168.0.0/16** e **10.254.0.0/16**<br>Per questo esempio, utilizziamo tooillustrate spazio di indirizzi più che il funzionamento della configurazione con più spazi degli indirizzi. ma per questa configurazione non sono necessari più spazi indirizzi.
* **Nome subnet: FrontEnd**
  * **Intervallo di indirizzi subnet: 192.168.1.0/24**
* **Nome subnet: BackEnd**
  * **Intervallo di indirizzi subnet: 10.254.1.0/24**
* **Nome subnet: GatewaySubnet**<br>nome della Subnet Hello *GatewaySubnet* è obbligatorio per toowork gateway VPN di hello.
  * **Intervallo di indirizzi subnet del gateway: 192.168.200.0/24** 
* **Pool di indirizzi client VPN: 172.16.201.0/24**<br>I client VPN che si connettono a una rete virtuale usando questa connessione Point-to-Site toohello riceveranno un indirizzo IP da pool di indirizzi del client VPN hello.
* **Sottoscrizione:** se si dispone di più di una sottoscrizione, verificare che si sta utilizzando hello corretto.
* **Gruppo di risorse: TestRG**
* **Località: Stati Uniti orientali**
* **Server DNS: Indirizzo IP** del server DNS hello che si vuole toouse per la risoluzione dei nomi.
* **Nome del gateway: Vnet1GW**
* **Nome dell'IP pubblico: VNet1GWPIP**
* **VpnType: RouteBased** 

## <a name="declare"></a>1. Accedere e impostare le variabili

In questa sezione si accedere e dichiarare i valori hello usati per questa configurazione. Hello dichiarato valori vengono utilizzati negli script di esempio hello. Modificare tooreflect valori hello al proprio ambiente. In alternativa, è possibile utilizzare valori dichiarati hello ed eseguono passaggi hello come esercizio.

1. Aprire la console di PowerShell con privilegi elevati e Accedi tooyour account Azure. Questo cmdlet richiede le credenziali di accesso hello. Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell.

  ```powershell
  Login-AzureRmAccount
  ```
2. Ottenere un elenco delle sottoscrizioni di Azure.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Specificare una sottoscrizione di hello che si desidera toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. Dichiarare le variabili di hello che si desidera toouse. Utilizzare hello di esempio seguente, sostituendo i valori hello per la propria quando necessario.

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2. Configurare una rete virtuale

1. Creare un gruppo di risorse.

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. Creazione di configurazioni di subnet per la rete virtuale hello, denominarli hello *front-end*, *back-end*, e *GatewaySubnet*. I prefissi devono far parte di hello spazio degli indirizzi di rete virtuale che è stato dichiarato.

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. Creare la rete virtuale hello.

  In questo esempio, i server DNS hello è facoltativo. Se si specifica un valore, non verrà creato un nuovo server DNS. Hello indirizzo IP del server DNS specificato deve essere in grado di risolvere nomi hello per le risorse di hello a che ci si connette un server DNS. In questo esempio è stato usato un indirizzo IP privato, ma è probabile che non si tratta di indirizzo IP di hello del server DNS. Essere toouse che i valori personalizzati.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. Specificare le variabili di hello per la rete virtuale di hello che è stato creato.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. Un gateway VPN deve avere un indirizzo IP pubblico. Richiesta innanzitutto la risorsa indirizzo IP hello e fare riferimento tooit durante la creazione del gateway di rete virtuale. indirizzo IP Hello viene assegnata dinamicamente toohello risorsa quando viene creato gateway VPN hello. Il gateway VPN supporta attualmente solo l'allocazione degli indirizzi IP pubblici *dinamici*. Non è possibile richiedere un'assegnazione degli indirizzi IP pubblici statici. Tuttavia, questo non significa che l'indirizzo IP hello cambia dopo che è stato assegnato come gateway VPN tooyour. Hello unica volta in cui le modifiche all'indirizzo IP pubblico hello quando è hello gateway viene eliminato e ricreato. Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway VPN.

  Richiedere un indirizzo IP pubblico assegnato dinamicamente.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3. Creare il gateway VPN hello

Configurare e creare il gateway di rete virtuale hello per la rete virtuale.

* Hello *- il tipo di gateway* deve essere **Vpn** hello e *- VpnType* deve essere **tipo RouteBased**.
* Un gateway VPN può richiedere fino a too45 minuti toocomplete, a seconda di hello [sku di gateway](vpn-gateway-about-vpn-gateway-settings.md) selezionate.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4. Aggiungere pool di indirizzi di client VPN hello

Al termine gateway VPN hello creazione, è possibile aggiungere hello client indirizzi della VPN. pool di indirizzi del client VPN Hello è intervallo hello da cui i client VPN hello riceveranno un indirizzo IP durante la connessione. Utilizzare un intervallo di indirizzi IP privato che non si sovrapponga con percorso locale hello che ci si connette da, o con rete virtuale che si desidera tooconnect per hello. In questo esempio hello pool di indirizzi del client VPN viene dichiarato come un [variabile](#declare) nel passaggio 1.

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5. Generare i certificati

I certificati usati dai client VPN di Azure tooauthenticate per le connessioni VPN Point-to-Site. Informazioni sulla chiave pubblica hello di hello radice certificato tooAzure caricare. la chiave pubblica di Hello viene quindi considerata 'trusted'. I certificati client devono essere generati dal certificato radice attendibile hello e quindi installati in ogni computer client nell'archivio di certificati utente corrente di certificati/personale hello. certificato di Hello è client hello tooauthenticate utilizzato quando avvia toohello una connessione tra reti virtuali. 

Se usati, i certificati autofirmati devono essere creati con parametri specifici. È possibile creare un certificato autofirmato utilizzando le istruzioni di hello per [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md), o, se non si dispone di Windows 10, è possibile utilizzare [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). È importante seguire i passaggi delle hello hello istruzioni durante la generazione di certificati radice autofirmati e certificati client. In caso contrario, generare i certificati di hello non sono compatibili con le connessioni P2S e si riceverà un errore di connessione.

### <a name="cer"></a>1. Ottenere il file con estensione cer hello per il certificato radice hello

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2. Generazione di un certificato client

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6. Carica informazioni sulla chiave pubblica certificato radice di hello

Verificare che la creazione del gateway VPN sia stata completata. Una volta completata, è possibile caricare hello file con estensione cer, che contiene informazioni sulla chiave pubblica di hello, per un tooAzure certificato radice attendibile. Una volta caricato il file a.cer, Azure può utilizzarlo tooauthenticate client che hanno installato un certificato client generato da hello certificato radice attendibile. È possibile caricare i file di certificato radice attendibile - backup tooa totale di 20, in un secondo momento, se necessario.

1. Dichiarare la variabile hello per il nome del certificato, sostituendo il valore di hello con valori personalizzati.

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. Sostituire il percorso di file hello con valori personalizzati e quindi eseguire i cmdlet di hello.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. Caricare hello tooAzure di informazioni sulla chiave pubblica. Una volta caricati, informazioni sul certificato hello Azure considera questa toobe un certificato radice attendibile.

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7. Scaricare il pacchetto di configurazione client VPN di hello

tooconnect tooa virtuale usando una VPN Point-to-Site, è necessario installare ogni client di un pacchetto di configurazione di client che consente di configurare i client VPN nativo hello con le impostazioni di hello e file di rete virtuale di toohello tooconnect necessarie. pacchetto di configurazione client VPN Hello configura i client VPN di Windows nativo hello, non installa un client VPN di nuovo o diverso. 

È possibile utilizzare hello stessa configurazione del client VPN del pacchetto in ogni computer client, come versione di hello corrisponda architettura hello per client hello. Per hello l'elenco dei sistemi operativi client supportati, vedere hello [connessioniPoint-to-Sitedomande frequenti su](#faq) alla fine di hello di questo articolo.

1. Dopo aver creato il gateway di hello, è possibile generare e scaricare il pacchetto di configurazione client hello. In questo esempio Scarica il pacchetto di hello per i client a 64 bit. Se si desidera client a 32 bit hello toodownload, sostituire 'Amd64' con 'x86'. È anche possibile scaricare client VPN hello utilizzando hello portale di Azure.

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. Copiare e incollare il collegamento hello restituito tooa browser toodownload hello pacchetto web, prestando attenzione virgolette hello tooremove circostanti collegamento hello. 
3. Scaricare e installare i pacchetti hello in computer client hello. Se viene visualizzato un popup SmartScreen, fare clic su **Altre informazioni** e quindi su **Esegui comunque** per installare il pacchetto. È inoltre possibile salvare tooinstall pacchetti hello in altri computer client.
4. In un computer client hello passare troppo**le impostazioni di rete** e fare clic su **VPN**. connessione VPN Hello Mostra il nome di hello della rete virtuale hello che si connette a.

## <a name="clientcertificate"></a>8. Installare un certificato client esportato

Se si desidera un P2S toocreate connessione da un computer client diverso hello è utilizzato i certificati di toogenerate hello client, è necessario tooinstall un certificato client. Quando si installa un certificato client, è necessario password hello creata quando è stato esportato il certificato di client hello. In genere, è sufficiente fare doppio clic sul certificato hello e installarlo.

Verificare che il certificato di client hello è stato esportato come un file pfx con hello intera catena di certificati (ovvero hello (impostazione predefinita). In caso contrario, non è presente nel computer client hello informazioni del certificato radice hello e client hello non saranno in grado di tooauthenticate correttamente. Per altre informazioni, vedere [Installare un certificato client esportato](vpn-gateway-certificates-point-to-site.md#install). 

## <a name="connect"></a>9. Connettersi tooAzure

1. tooconnect tooyour rete virtuale, computer client hello passare tooVPN connessioni e individuare la connessione VPN hello creato. Il file è denominato hello stesso nome della rete virtuale. Fare clic su **Connetti**. Che fa riferimento il certificato di hello toousing viene visualizzato un messaggio popup. Fare clic su **continua** toouse privilegi elevati. 
2. In hello **connessione** pagina di stato, fare clic su **Connetti** connessione hello toostart. Se viene visualizzato un **Seleziona certificato** schermata, verificare che hello certificato client visualizzato sia hello uno che si desidera toouse tooconnect. In caso contrario, utilizzare hello freccia tooselect hello corretto certificato e quindi fare clic su **OK**.

  ![I client VPN si connette tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. Verrà stabilita la connessione.

  ![Connessione stabilita](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Risoluzione dei problemi delle connessioni P2S

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10. Verificare la connessione

1. tooverify che la connessione VPN sia attiva, aprire un prompt dei comandi con privilegi elevati ed eseguire *ipconfig/all*.
2. Visualizzare i risultati di hello. Si noti che l'indirizzo IP hello che è stato ricevuto uno degli indirizzi hello all'interno di hello Point-to-Site VPN Client Pool di indirizzi specificato nella configurazione. risultati di Hello sono simili toothis esempio:

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Connettere la macchina virtuale di tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="addremovecert"></a>Aggiungere o rimuovere un certificato radice

È possibile aggiungere e rimuovere certificati radice attendibili da Azure. Quando si rimuove un certificato radice, i client che dispongono di un certificato generato dal certificato radice hello non è possibile eseguire l'autenticazione e non saranno in grado di tooconnect. Se si desidera tooauthenticate un client e la connessione, è necessario tooinstall un nuovo certificato client generato da un certificato radice attendibile tooAzure (caricato).

### <a name="addtrustedroot"></a>tooadd un certificato radice attendibile

È possibile aggiungere backup too20 radice certificato con estensione cer file tooAzure. esempio Hello i passaggi della Guida si aggiunge un certificato radice:

#### <a name="certmethod1"></a>Metodo 1

Si tratta di tooupload metodo più efficiente di hello un certificato radice.

1. Preparare tooupload di file con estensione cer hello:

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Caricare file hello. È possibile caricare un solo file alla volta.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. tooverify che il file di certificato caricato hello:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>Metodo 2

Questo metodo è ha ulteriori passaggi rispetto al metodo 1, ma è hello stesso risultato. È incluso in caso di necessità di dati del certificato tooview hello.

1. Creare e preparare hello nuovo certificato tooadd tooAzure radice. Esportare la chiave pubblica hello come x. 509 con codifica Base 64 (. CER) e aprirlo con un editor di testo. Copiare i valori hello, come illustrato nell'esempio seguente hello:

  ![certificato](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > Quando si copiano i dati del certificato hello, assicurarsi di copiare testo hello come un'unica riga continua senza ritorni a capo o avanzamenti riga. Potrebbe essere necessario toomodify la visualizzazione nel too'Show editor di testo hello simbolo/Mostra avanzamenti di riga e restituisce un ritorno a capo hello toosee di tutti i caratteri.
  >
  >

2. Specificare il nome di certificato hello e informazioni sulla chiave come una variabile. Sostituire le informazioni di hello personalizzata, come illustrato in hello nell'esempio seguente:

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. Aggiungi nuovo certificato radice di hello. È possibile aggiungere solo un certificato alla volta.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. È possibile verificare che il nuovo certificato hello è stata aggiunta correttamente utilizzando hello di esempio seguente:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove un certificato radice

1. Dichiarare le variabili di hello.

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. Rimuovere il certificato di hello.

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. Hello utilizzare seguente tooverify di esempio che hello certificato è stato rimosso correttamente.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>Revocare un certificato client

È possibile revocare i certificati client. certificato Hello elenco di revoche di certificati consente tooselectively negare connettività Point-to-Site in base a singoli certificati client. Questa operazione è diversa rispetto alla rimozione di un certificato radice attendibile. Se si rimuove un CER del certificato radice attendibile da Azure, comporta la revoca l'accesso per tutti i certificati client generato firmato dall'autorità di certificazione revocata hello hello. Revoca di un certificato client, anziché certificato radice hello consente hello altri certificati che sono stati generati da hello radice certificato toocontinue toobe utilizzato per l'autenticazione.

pratica comune Hello è accesso toouse hello radice certificato toomanage livelli team o dell'organizzazione, durante l'utilizzo dei certificati client revocati per il controllo di accesso con granularità fine per utenti singoli.

### <a name="revokeclientcert"></a>toorevoke un certificato client

1. Recuperare l'identificazione personale del certificato client di hello. Per ulteriori informazioni, vedere [come tooretrieve hello identificazione personale del certificato](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copiare l'editor di testo hello informazioni tooa e rimuovere tutti gli spazi in modo che sia una stringa continua. Questa stringa è dichiarata come variabile nel passaggio successivo hello.
3. Dichiarare le variabili di hello. Verificare l'identificazione personale di hello toodeclare che è stato recuperato nel passaggio precedente hello.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. Aggiungere l'elenco di toohello hello identificazione personale dei certificati revocati. Viene visualizzato "Succeeded" quando è stato aggiunto l'identificazione personale hello.

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. Verificare che tale identificazione digitale hello è stato aggiunto l'elenco di revoche di certificati toohello.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. Dopo l'aggiunta di identificazione personale hello, certificato hello non può più essere utilizzato tooconnect. I client che tentano di tooconnect usando questo certificato, ricevono un messaggio che informa che il certificato hello non è più valido.

### <a name="reinstateclientcert"></a>tooreinstate un certificato client

È possibile ripristinare un certificato client rimuovendo l'identificazione personale hello dall'elenco di hello dei certificati client revocati.

1. Dichiarare le variabili di hello. Verificare che si dichiara hello corretta identificazione digitale certificato hello che si desidera tooreinstate.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. Rimuovere l'identificazione personale del certificato hello dall'elenco di revoche di certificati hello.

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. Controllare se identificazione personale hello viene rimosso dall'elenco di revocati hello.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>Domande frequenti sulla connettività da punto a sito

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand informazioni sulle reti e macchine virtuali, vedere [Cenni preliminari sulla rete di Azure e VM Linux](../virtual-machines/linux/azure-vm-network-overview.md).
