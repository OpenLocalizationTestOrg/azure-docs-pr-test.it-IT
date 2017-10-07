---
title: 'Connettere una rete virtuale tooa computer Point-to-Site e certificato di autenticazione: portale di Azure | Documenti Microsoft'
description: Consente di connettersi in modo sicuro un tooyour computer rete virtuale di Azure tramite la creazione di una connessione di gateway VPN Point-to-Site utilizzando l'autenticazione del certificato. In questo articolo si applica al modello di distribuzione di gestione delle risorse toohello e utilizza hello portale di Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>Configurare un tooa connessione Point-to-Site rete virtuale utilizzando l'autenticazione del certificato: portale di Azure

In questo articolo viene illustrato come una rete virtuale con una connessione Point-to-Site nel modello di distribuzione di gestione delle risorse hello utilizzando toocreate hello portale di Azure. Questa configurazione utilizza hello tooauthenticate certificati connessione del client. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Un gateway VPN da punto a sito (P2S) consente di creare una rete virtuale tooyour di connessione protetta da un computer client. Le connessioni VPN Point-to-Site sono utili quando si desidera tooconnect tooyour rete virtuale da una posizione remota, ad esempio quando sono il telelavoro da casa o di una conferenza. Una VPN P2S è anche un toouse soluzione utile anziché una VPN da sito a sito quando si dispone solo alcuni client che richiedono tooconnect tooa rete virtuale. 

Usa P2S hello SSTP Secure Socket Tunneling Protocol (), che è un protocollo di rete VPN basata su SSL. Viene stabilita una connessione di VPN P2S avviandolo dal computer client hello.

![Diagramma da punto a sito](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

Connessioni di autenticazione Point-to-Site certificato requisiti hello:

* Un gateway VPN RouteBased.
* Hello chiave pubblica (file con estensione cer) per un certificato radice, ovvero tooAzure caricato. Una volta caricato il certificato di hello, viene considerato un certificato attendibile e viene utilizzato per l'autenticazione.
* Un certificato client è generato dal certificato radice hello e installato in ogni computer client che si connetteranno toohello rete virtuale. Questo certificato viene usato per l'autenticazione client.
* Un pacchetto di configurazione del client VPN. pacchetto di configurazione client VPN Hello contiene le informazioni necessarie hello per hello client tooconnect toohello rete virtuale. pacchetto di Hello Configura hello esistente client VPN è toohello nativo del sistema operativo Windows. Ogni client che si connette devono essere configurate tramite il pacchetto di configurazione di hello.

Le connessioni da punto a sito non richiedono un dispositivo VPN o un indirizzo IP pubblico locale. connessione VPN Hello viene creato tramite SSTP (Secure Socket Tunneling Protocol). Sul lato server hello è supporta le versioni SSTP 1.0, 1.1 e 1.2. client Hello decide quali toouse versione. Per Windows 8.1 e versioni successive, SSTP usa per impostazione predefinita la versione 1.2.

Per ulteriori informazioni sulle connessioni Point-to-Site, vedere hello [Point-to-Site domande frequenti su](#faq) alla fine di hello di questo articolo.

#### <a name="example"></a>Valori di esempio

È possibile utilizzare hello seguente valori toocreate un ambiente di test, o fare riferimento a valori toothese toobetter comprendere esempi hello in questo articolo:

* **Nome della rete virtuale:** VNet1
* **Spazio indirizzi:** 192.168.0.0/16<br>Per questo esempio, viene usato un solo spazio indirizzi. È possibile avere più di uno spazio indirizzi per la rete virtuale.
* **Nome subnet:** FrontEnd
* **Intervallo di indirizzi subnet:** 192.168.1.0/24
* **Sottoscrizione:** se si dispone di più di una sottoscrizione, verificare che si sta utilizzando hello corretto.
* **Gruppo di risorse:** TestRG
* **Località:** Stati Uniti orientali
* **GatewaySubnet:** 192.168.200.0/24<br>
* **Server DNS:** (facoltativo) l'indirizzo IP del server DNS hello che si vuole toouse per la risoluzione dei nomi.
* **Nome gateway di rete virtuale:** VNet1GW
* **Tipo di gateway:** VPN
* **Tipo VPN:** Basato su route
* **Nome indirizzo IP pubblico:** VNet1GWpip
* **Tipo di connessione:** Da punto a sito
* **Pool di indirizzi client:** 172.16.201.0/24<br>I client VPN che si connettono a una rete virtuale usando questa connessione Point-to-Site toohello ricevono un indirizzo IP dal pool di indirizzi hello client.

## <a name="createvnet"></a>1. Crea rete virtuale

Prima di iniziare, verificare di possedere una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial).

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Aggiungere una subnet del gateway

Prima della connessione del gateway di rete virtuale tooa, è necessario innanzitutto subnet del gateway hello toocreate per hello toowhich di rete virtuale si desidera tooconnect. il servizio gateway Hello utilizza indirizzi IP hello specificati nella subnet del gateway hello. Se possibile, creare una subnet del gateway con un blocco CIDR di /28 o /27 tooprovide sufficiente IP risolve i requisiti di configurazione futura aggiuntiva tooaccommodate.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. Specificare un server DNS (facoltativo)

Dopo aver creato la rete virtuale, è possibile aggiungere l'indirizzo IP hello una DNS server toohandle di risoluzione dei nomi. server DNS Hello è facoltativo per questa configurazione, ma è obbligatorio se si desidera la risoluzione dei nomi. Se si specifica un valore, non verrà creato un nuovo server DNS. Hello indirizzo IP del server DNS specificato deve essere in grado di risolvere nomi hello per le risorse di hello a che ci si connette un server DNS. In questo esempio è stato usato un indirizzo IP privato, ma è probabile che non si tratta di indirizzo IP di hello del server DNS. Essere toouse che i valori personalizzati.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. Creare un gateway di rete virtuale

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. Generare i certificati

I certificati utilizzati dai client di Azure tooauthenticate connessione tooa rete virtuale tramite una connessione VPN Point-to-Site. Una volta ottenuto un certificato radice, è [caricare](#uploadfile) hello tooAzure informazioni sulla chiave pubblica. certificato radice Hello viene quindi considerato 'trusted' da Azure per la connessione in rete virtuale di P2S toohello. Inoltre generare i certificati client da hello certificato radice attendibile e quindi installarli in ogni computer client. certificato client hello è client hello tooauthenticate utilizzato quando avvia toohello una connessione tra reti virtuali. 

### <a name="getcer"></a>1. Ottenere il file con estensione cer hello per il certificato radice hello

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. Generazione di un certificato client

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Aggiungere pool di indirizzi hello client

pool di indirizzi Hello client è un intervallo di indirizzi IP privati specificati. i client di Hello che si connettono tramite una VPN Point-to-Site ricevono un indirizzo IP da questo intervallo. Utilizzare un intervallo di indirizzi IP privato che non si sovrapponga con percorso locale hello che ci si connette da o rete virtuale che si desidera tooconnect per hello.

1. Dopo aver creato il gateway di rete virtuale hello, passare toohello **impostazioni** sezione della pagina di gateway di rete virtuale hello. In hello **impostazioni** fare clic su **configurazionePoint-to-site** tooopen hello **punto-a-configurazione del sito-** pagina.

  ![Pagina Configurazione da punto a sito](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. In hello **punto-a-configurazione del sito-** pagina, è possibile eliminare l'intervallo di hello riempimento automatico, quindi aggiungere hello privata intervallo di indirizzi IP che si desidera toouse. Fare clic su **salvare** toovalidate e salvare le impostazioni di hello.

  ![Pool di indirizzi client](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Caricare i dati di un certificato pubblico certificato radice hello

Dopo hello gateway è stato creato, caricare informazioni sulla chiave pubblica hello per tooAzure certificato radice di hello. Dopo aver caricati i dati di un certificato pubblico hello, Azure può usarlo tooauthenticate client che hanno installato un certificato client generato da hello certificato radice attendibile. È possibile caricare totale tooa dei certificati radice attendibili aggiuntivi di 20.

1. I certificati vengono aggiunti alla hello **configurazionePoint-to-site** pagina hello **certificato radice** sezione.  
2. Assicurarsi che sia stato esportato certificato radice hello come file x. 509 (. cer) con codifica Base 64. È necessario il certificato hello tooexport nel formato in modo è possibile aprire il certificato di hello con l'editor di testo.
3. Aprire il certificato di hello con un editor di testo, ad esempio Blocco note. Quando si copiano i dati del certificato hello, assicurarsi di copiare testo hello come un'unica riga continua senza ritorni a capo o avanzamenti riga. Potrebbe essere necessario toomodify la visualizzazione nel too'Show editor di testo hello simbolo/Mostra avanzamenti di riga e restituisce un ritorno a capo hello toosee di tutti i caratteri. Copiare solo hello seguente sezione come una linea continua:

  ![Dati del certificato](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Incollare i dati del certificato hello in hello **dati del certificato pubblico** campo. **Nome** hello certificato e quindi fare clic su **salvare**. È possibile aggiungere i certificati radice attendibili too20.

  ![Caricamento del certificato](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. Generare e installare il pacchetto di configurazione client VPN di hello

tooconnect tooa virtuale usando una VPN Point-to-Site, è necessario installare ogni client di un pacchetto di configurazione di client che consente di configurare i client VPN nativo hello con le impostazioni di hello e file di rete virtuale di toohello tooconnect necessarie. pacchetto di configurazione client VPN Hello configura i client VPN di Windows nativo hello, non installa un client VPN di nuovo o diverso.

È possibile utilizzare hello stessa configurazione del client VPN del pacchetto in ogni computer client, come versione di hello corrisponda architettura hello per client hello. Per hello l'elenco dei sistemi operativi client supportati, vedere hello [connessioniPoint-to-Sitedomande frequenti su](#faq) alla fine di hello di questo articolo.

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>Passaggio 1: generare e scaricare il pacchetto di configurazione client hello

1. In hello **configurazionePoint-to-site** pagina, fare clic su **client VPN scaricare** tooopen hello **client VPN scaricare** pagina. Accetta un o due minuti per hello pacchetto toogenerate.

  ![Download del client VPN 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. Selezionare pacchetto di hello corretto per il client e quindi fare clic su **scaricare**. Salvare il file di pacchetto di hello configurazione. Installare il pacchetto di configurazione client VPN di hello in ogni computer client che si connette la rete virtuale toohello.

  ![Download del client VPN 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>Passaggio 2: pacchetto di configurazione installazione hello client

1. File di configurazione hello Copia localmente toohello computer, che si desidera rete virtuale di tooconnect tooyour. 
2. Fare doppio clic sul pacchetto hello tooinstall hello .exe file nel computer client hello. Poiché è stato creato il pacchetto di configurazione di hello, che non è firmata e venga visualizzato un avviso. Se viene visualizzato un popup Windows SmartScreen, fare clic su **informazioni** (sul lato sinistro hello), quindi **eseguire comunque** pacchetto hello tooinstall.
3. Installare i pacchetti hello in computer client hello. Se viene visualizzato un popup Windows SmartScreen, fare clic su **informazioni** (sul lato sinistro hello), quindi **eseguire comunque** pacchetto hello tooinstall.
4. In un computer client hello passare troppo**le impostazioni di rete** e fare clic su **VPN**. connessione VPN Hello Mostra il nome di hello della rete virtuale hello che si connette a.

## <a name="installclientcert"></a>9. Installare un certificato client esportato

Se si desidera un P2S toocreate connessione da un computer client diverso hello è utilizzato i certificati di toogenerate hello client, è necessario tooinstall un certificato client. Quando si installa un certificato client, è necessario password hello creata quando è stato esportato il certificato di client hello. In genere, è sufficiente fare doppio clic sul certificato hello e installarlo.

Verificare che il certificato di client hello è stato esportato come un file pfx con hello intera catena di certificati (ovvero hello (impostazione predefinita). In caso contrario, non è presente nel computer client hello informazioni del certificato radice hello e client hello non saranno in grado di tooauthenticate correttamente. Per altre informazioni, vedere [Installare un certificato client esportato](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>10. Connettersi tooAzure

1. tooconnect tooyour rete virtuale, computer client hello passare tooVPN connessioni e individuare la connessione VPN hello creato. Il file è denominato hello stesso nome della rete virtuale. Fare clic su **Connetti**. Che fa riferimento il certificato di hello toousing viene visualizzato un messaggio popup. Fare clic su **continua** toouse privilegi elevati.

2. In hello **connessione** pagina di stato, fare clic su **Connetti** connessione hello toostart. Se viene visualizzato un **Seleziona certificato** schermata, verificare che hello certificato client visualizzato sia hello uno che si desidera toouse tooconnect. In caso contrario, utilizzare hello freccia tooselect hello corretto certificato e quindi fare clic su **OK**.

  ![I client VPN si connette tooAzure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. Verrà stabilita la connessione.

  ![Connessione stabilita](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Risoluzione dei problemi delle connessioni P2S

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. Verificare la connessione

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

## <a name="add"></a>Aggiungere o rimuovere certificati radice attendibili

È possibile aggiungere e rimuovere certificati radice attendibili da Azure. Quando si rimuove un certificato radice, i client che dispongono di un certificato generato da tale radice non sarà in grado di tooauthenticate e pertanto non essere in grado di tooconnect. Se si desidera tooauthenticate un client e la connessione, è necessario tooinstall un nuovo certificato client generato da un certificato radice attendibile tooAzure (caricato).

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd un certificato radice attendibile

È possibile aggiungere backup too20 attendibili radice certificato con estensione cer file tooAzure. Per istruzioni, vedere la sezione hello [caricare un certificato radice attendibile](#uploadfile) in questo articolo.

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove un certificato radice attendibile

1. un certificato radice attendibile, tooremove passare toohello **configurazionePoint-to-site** pagina per il gateway di rete virtuale.
2. In hello **certificato radice** sezione della pagina di hello, individuare il certificato di hello che si vuole tooremove.
3. Fare clic su Avanti toohello certificato di hello i puntini di sospensione e quindi fare clic su 'Remove'.

## <a name="revokeclient"></a>Revocare un certificato client

È possibile revocare i certificati client. certificato Hello elenco di revoche di certificati consente tooselectively negare connettività Point-to-Site in base a singoli certificati client. Questa operazione è diversa rispetto alla rimozione di un certificato radice attendibile. Se si rimuove un CER del certificato radice attendibile da Azure, comporta la revoca l'accesso per tutti i certificati client generato firmato dall'autorità di certificazione revocata hello hello. Revoca di un certificato client, anziché certificato radice hello consente hello altri certificati che sono stati generati da hello radice certificato toocontinue toobe utilizzato per l'autenticazione.

pratica comune Hello è accesso toouse hello radice certificato toomanage livelli team o dell'organizzazione, durante l'utilizzo dei certificati client revocati per il controllo di accesso con granularità fine per utenti singoli.

### <a name="toorevoke-a-client-certificate"></a>toorevoke un certificato client

È possibile revocare un certificato client tramite l'aggiunta di elenco di revoche toohello hello identificazione personale.

1. Recuperare l'identificazione personale del certificato client di hello. Per ulteriori informazioni, vedere [come tooretrieve hello identificazione personale del certificato](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copiare l'editor di testo hello informazioni tooa e rimuovere tutti gli spazi in modo che sia una stringa continua.
3. Passare il gateway di rete virtuale toohello **punto-a-configurazione del sito-** pagina. Si tratta di hello stessa pagina in cui è stato utilizzato troppo[caricare un certificato radice attendibile](#uploadfile).
4. In hello **i certificati revocati** sezione, immettere un nome descrittivo per il certificato di hello (che non ha Credenziali del certificato hello toobe).
5. Copiare e incollare toohello stringa di identificazione personale hello **identificazione personale** campo.
6. identificazione personale Hello convalida e viene aggiunto automaticamente toohello elenco di revoche di certificati. Viene visualizzato un messaggio nella schermata di hello che hello Aggiorna l'elenco. 
7. Dopo l'aggiornamento è stata completata, il certificato di hello non può più essere utilizzato tooconnect. I client che tentano di tooconnect usando questo certificato, ricevono un messaggio che informa che il certificato hello non è più valido.

## <a name="faq"></a>Domande frequenti sulla connettività da punto a sito

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand informazioni sulle reti e macchine virtuali, vedere [Cenni preliminari sulla rete di Azure e VM Linux](../virtual-machines/linux/azure-vm-network-overview.md).
