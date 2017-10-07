---
title: 'Connettere una rete virtuale tooa computer Point-to-Site e certificato di autenticazione: classica portale di Azure | Documenti Microsoft'
description: Una connessione sicura tooyour classico rete virtuale di Azure tramite la creazione di una connessione di gateway VPN Point-to-Site utilizzando hello portale di Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>Configurare un tooa connessione Point-to-Site rete virtuale utilizzando l'autenticazione del certificato (versione classica): il portale di Azure

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

In questo articolo viene illustrato come una rete virtuale con una connessione Point-to-Site nel modello di distribuzione classica hello utilizzando toocreate hello portale di Azure. Questa configurazione utilizza hello tooauthenticate certificati connessione del client. È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

Un gateway VPN da punto a sito (P2S) consente di creare una rete virtuale tooyour di connessione protetta da un computer client. Le connessioni VPN Point-to-Site sono utili quando si desidera tooconnect tooyour rete virtuale da una posizione remota, ad esempio quando sono il telelavoro da casa o di una conferenza. Una VPN P2S è anche un toouse soluzione utile anziché una VPN da sito a sito quando si dispone solo alcuni client che richiedono tooconnect tooa rete virtuale. 

Usa P2S hello SSTP Secure Socket Tunneling Protocol (), che è un protocollo di rete VPN basata su SSL. Viene stabilita una connessione di VPN P2S avviandolo dal computer client hello.


![Diagramma da punto a sito](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


Connessioni di autenticazione Point-to-Site certificato requisiti hello:

* Un gateway VPN dinamico.
* Hello chiave pubblica (file con estensione cer) per un certificato radice, ovvero tooAzure caricato. Questo viene considerato un certificato attendibile e viene usato per l'autenticazione.
* Un certificato client generato dal certificato radice hello e installato in ogni computer client che si connetterà. Questo certificato viene usato per l'autenticazione client.
* Un pacchetto di configurazione client VPN deve essere generato e installato in ogni computer client che effettua la connessione. pacchetto di configurazione client Hello configura i client VPN nativo hello che è già presente nel sistema operativo hello con hello le informazioni necessarie tooconnect toohello rete virtuale.

Le connessioni da punto a sito non richiedono un dispositivo VPN o un indirizzo IP pubblico locale. connessione VPN Hello viene creato tramite SSTP (Secure Socket Tunneling Protocol). Sul lato server hello è supporta le versioni SSTP 1.0, 1.1 e 1.2. client Hello decide quali toouse versione. Per Windows 8.1 e versioni successive, SSTP usa per impostazione predefinita la versione 1.2. 

Per ulteriori informazioni sulle connessioni Point-to-Site, vedere hello [Point-to-Site domande frequenti su](#faq) alla fine di hello di questo articolo.

### <a name="example-settings"></a>Impostazioni di esempio

È possibile utilizzare hello seguente valori toocreate un ambiente di test, o fare riferimento a valori toothese toobetter comprendere esempi hello in questo articolo:

* **Nome: VNet1**
* **Spazio indirizzi: 192.168.0.0/16**<br>Per questo esempio, viene usato un solo spazio indirizzi. È possibile avere più di uno spazio indirizzi per la rete virtuale.
* **Nome subnet: FrontEnd**
* **Intervallo di indirizzi subnet: 192.168.1.0/24**
* **Sottoscrizione:** se si dispone di più di una sottoscrizione, verificare che si sta utilizzando hello corretto.
* **Gruppo di risorse: TestRG**
* **Località: Stati Uniti orientali**
* **Tipo di connessione: Da punto a sito**
* **: 172.16.201.0/24**. I client VPN che si connettono toohello virtuale usando questa connessione Point-to-Site riceve un indirizzo IP da hello pool specificato.
* **GatewaySubnet: 192.168.200.0/24**. subnet del Gateway Hello è necessario utilizzare il nome di hello 'GatewaySubnet'.
* **Dimensioni:** gateway hello selezionare SKU che si desidera toouse.
* **Tipo di routing: Dinamico**

## <a name="vnetvpn"></a>1. Creare una rete virtuale e un gateway VPN

Prima di iniziare, verificare di possedere una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial).

### <a name="createvnet"></a>Parte 1: Creare una rete virtuale

Se non si ha una rete virtuale, crearne una. Gli screenshot sono forniti come esempio. Essere certi tooreplace hello i valori con valori personalizzati. una rete virtuale utilizzando toocreate hello portale di Azure, utilizzare hello alla procedura seguente:

1. Da un browser, passare toohello [portale di Azure](http://portal.azure.com) e, se necessario, accedere con l'account di Azure.
2. Fare clic su **New**. In hello **marketplace hello ricerca** , digitare 'Rete virtuale'. Individuare **rete virtuale** hello restituito elenco e fare clic su hello tooopen **rete virtuale** pagina.

  ![pagina di ricerca della rete virtuale](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Nella parte inferiore di hello della pagina rete virtuale hello da hello **selezionare un modello di distribuzione** selezionare **classico**, quindi fare clic su **crea**.

  ![Selezionare il modello di distribuzione](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. In hello **crea rete virtuale** pagina, configurare le impostazioni di rete virtuale hello. Aggiungere a questa pagina il primo spazio di indirizzi e l'intervallo di indirizzi di una subnet singola. Al termine della creazione hello rete virtuale, è possibile tornare indietro e aggiungere altre subnet e gli spazi degli indirizzi.

  ![Pagina Crea rete virtuale](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. Verificare che hello **sottoscrizione** è hello corretto. È possibile modificare le sottoscrizioni con elenco a discesa hello.
6. Fare clic su **Gruppo di risorse** e selezionare un gruppo di risorse esistente o crearne uno nuovo digitandone il nome. Se si sta creando un nuovo gruppo di risorse, gruppo di risorse hello nome base tooyour pianificato i valori di configurazione. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Selezionare quindi hello **percorso** le impostazioni per la rete virtuale. posizione di Hello determina in cui risiederà risorse hello distribuire toothis rete virtuale.
8. Selezionare **Pin toodashboard** se si desidera che la rete virtuale con facilità in dashboard hello toofind in grado di toobe e quindi fare clic su **crea**.

  ![PIN toodashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. Dopo aver fatto clic su Crea, viene visualizzato un riquadro nel dashboard che riflette lo stato di avanzamento hello di una rete virtuale. le modifiche apportate al riquadro Hello come hello rete virtuale viene creato.

  ![Pannello Creazione della rete virtuale](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. Dopo aver creata la rete virtuale, vedere **creato** sotto **stato** nella pagina reti hello hello portale di Azure classico.
11. Aggiungere un server DNS (facoltativo). Dopo aver creato la rete virtuale, è possibile aggiungere l'indirizzo IP hello di un server DNS per la risoluzione dei nomi. Hello indirizzo IP del server DNS specificato deve essere indirizzo hello di un server DNS in grado di risolvere nomi hello per le risorse di hello in una rete virtuale.<br>tooadd un server DNS, aprire le impostazioni di hello per la rete virtuale, fare clic su server DNS e aggiungere l'indirizzo IP di hello del server DNS hello che si desidera toouse.

### <a name="gateway"></a>Parte 2: Creare una subnet del gateway e un gateway di routing dinamico

In questo passaggio vengono creati una subnet del gateway e un gateway di routing dinamico. Nel portale di Azure per il modello di distribuzione classica hello hello, la creazione di subnet del gateway hello e gateway hello possono essere eseguita tramite hello stesso pagine di configurazione.

1. Nel portale di hello passare toohello rete virtuale per cui si desidera toocreate un gateway.
2. Nella pagina di hello per la rete virtuale, sul hello **Panoramica** pagina, nella sezione relativa alle connessioni VPN hello, fare clic su **Gateway**.

  ![Fare clic su un gateway toocreate](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. In hello **nuova connessione VPN** selezionare **Point-to-site**.

  ![Tipo di connessione da punto a sito](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. Per **spazio degli indirizzi Client**, aggiungere l'intervallo di indirizzi IP hello. Questo è l'intervallo di hello da cui i client VPN hello riceveranno un indirizzo IP durante la connessione. Utilizzare un intervallo di indirizzi IP privato che non si sovrapponga con percorso locale hello che verrà effettuata la connessione da o con rete virtuale che si desidera tooconnect per hello. È possibile eliminare l'intervallo di hello riempimento automatico, quindi aggiungere hello privata intervallo di indirizzi IP che si desidera toouse.

  ![Spazio indirizzi client](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. Seleziona hello **crea gateway immediatamente** casella di controllo.

  ![Crea gateway immediatamente](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. Fare clic su **configurazione del gateway facoltativo** tooopen hello **configurazione del Gateway** pagina.

  ![Fare clic su Configurazione gateway facoltativa](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. Fare clic su **Subnet configurare le impostazioni obbligatorie** tooadd hello **subnet del gateway**. Sebbene sia possibile toocreate assuma /29 una subnet del gateway, è consigliabile creare una subnet più grande che include più indirizzi selezionando almeno /28 o /27. In questo modo per sufficiente indirizzi tooaccommodate possibili configurazioni aggiuntive che è possibile in hello future. Quando si utilizzano subnet gateway, evitare di associazione di una subnet del gateway rete toohello sicurezza gruppo (). Associazione di una subnet della rete sicurezza gruppo toothis può causare il toostop gateway VPN funziona come previsto.

  ![Aggiungere GatewaySubnet](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. Gateway hello selezionare **dimensioni**. dimensioni Hello sono gateway hello SKU per il gateway di rete virtuale. Nel portale di hello hello predefinito SKU è **base**. Per altre informazioni sugli SKU di gateway, vedere [Informazioni sulle impostazioni del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

  ![Dimensioni del gateway](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. Seleziona hello **tipo di Routing** per il gateway. Le configurazioni P2S richiedono il tipo di routing **Dinamico**. Al termine della configurazione della pagina, fare clic su **OK**.

  ![Configurare il tipo di routing](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. In hello **nuova connessione VPN** pagina, fare clic su **OK** nella parte inferiore di hello di hello pagina toobegin la creazione del gateway di rete virtuale. Un gateway VPN può richiedere too45 minuti toocomplete, a seconda della sku di gateway hello selezionato.

## <a name="generatecerts"></a>2. Creare i certificati

I certificati usati dai client VPN di Azure tooauthenticate per le connessioni VPN Point-to-Site. Informazioni sulla chiave pubblica hello di hello radice certificato tooAzure caricare. la chiave pubblica di Hello viene quindi considerata 'trusted'. I certificati client devono essere generati dal certificato radice attendibile hello e quindi installati in ogni computer client nell'archivio di certificati utente corrente di certificati/personale hello. certificato di Hello è client hello tooauthenticate utilizzato quando avvia toohello una connessione tra reti virtuali. 

Se usati, i certificati autofirmati devono essere creati con parametri specifici. È possibile creare un certificato autofirmato utilizzando le istruzioni di hello per [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md), o [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). È importante seguire passaggi hello in queste istruzioni quando si utilizzano i certificati radice autofirmati e generazione di certificati client da hello certificato radice autofirmato. In caso contrario, non sono compatibili con le connessioni P2S hello i certificati creati e si riceverà un errore di connessione.

### <a name="cer"></a>Parte 1: Ottenere la chiave pubblica hello (con estensione cer) per il certificato radice hello

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>Parte 2: Generare un certificato client

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Caricare file con estensione cer del certificato radice hello

Dopo aver creato il gateway di hello, è possibile caricare hello file con estensione cer, che contiene informazioni sulla chiave pubblica di hello, per un tooAzure certificato radice attendibile. La chiave privata per hello radice certificato tooAzure hello non caricate. Una volta caricato il file a.cer, Azure può utilizzarlo tooauthenticate client che hanno installato un certificato client generato da hello certificato radice attendibile. È possibile caricare i file di certificato radice attendibile - backup tooa totale di 20, in un secondo momento, se necessario.  

1. In hello **le connessioni VPN** sezione della pagina di hello per la rete virtuale, fare clic su hello **client** tooopen grafici hello **Point-to-site VPN connessione** pagina.

  ![Client](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. In hello **connessionePoint-to-site** pagina, fare clic su **gestire i certificati** tooopen hello **certificati** pagina.<br>

  ![Pagina Certificati](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. In hello **certificati** pagina, fare clic su **caricare** tooopen hello **carica certificato** pagina.<br>

    ![Pagina Carica certificato](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Fare clic su hello toobrowse grafici di cartella per il file con estensione cer hello. Selezionare il file hello, quindi fare clic su **OK**. Aggiornamento hello pagina toosee hello caricato certificato hello **certificati** pagina.

  ![Caricamento del certificato](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Configurare hello client

tooconnect tooa virtuale usando una VPN Point-to-Site, è necessario installare client VPN di Windows nativo un pacchetto tooconfigure hello ogni client. pacchetto di configurazione Hello Configura client VPN di Windows nativo hello con la rete virtuale toohello hello impostazioni tooconnect necessarie.

È possibile utilizzare hello stessa configurazione del client VPN del pacchetto in ogni computer client, come versione di hello corrisponda architettura hello per client hello. Per hello l'elenco dei sistemi operativi client supportati, vedere hello [connessioniPoint-to-Sitedomande frequenti su](#faq) alla fine di hello di questo articolo.

### <a name="generateconfigpackage"></a>Parte 1: Generare e installare il pacchetto di configurazione client VPN di hello

1. Nel portale di Azure in hello hello **Panoramica** pagina per la rete virtuale, **le connessioni VPN**, fare clic su hello tooopen grafici di hello client **Point-to-site VPN connessione** pagina.
2. Nella parte superiore di hello di hello **Point-to-site VPN connessione** pagina, fare clic su pacchetto di download di hello corrispondente toohello sistema operativo di client in cui verrà installato:

  * Per client a 64 bit, selezionare **Client VPN (64 bit)**.
  * Per client a 32 bit, selezionare **Client VPN (32 bit)**.

  ![Scaricare il pacchetto di configurazione del client VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. Una volta hello incluso nel pacchetto viene generato l'errore, scaricarlo e installarlo nel computer client. Se viene visualizzato un popup SmartScreen, fare clic su **Altre informazioni** e quindi su **Esegui comunque** per installare il pacchetto. È inoltre possibile salvare tooinstall pacchetti hello in altri computer client.

### <a name="installclientcert"></a>Parte 2: Certificato client hello installazione

Se si desidera un P2S toocreate connessione da un computer client diverso hello è utilizzato i certificati di toogenerate hello client, è necessario tooinstall un certificato client. Quando si installa un certificato client, è necessario password hello creata quando è stato esportato il certificato di client hello. In genere si tratta semplicemente doppio clic sul certificato hello e installarlo. Per altre informazioni, vedere [Installare un certificato client esportato](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>5. Connettersi tooAzure

### <a name="connect-tooyour-vnet"></a>La connessione di rete virtuale tooyour

1. tooconnect tooyour rete virtuale, computer client hello passare tooVPN connessioni e individuare la connessione VPN hello creato. Il file è denominato hello stesso nome della rete virtuale. Fare clic su **Connetti**. Che fa riferimento il certificato di hello toousing viene visualizzato un messaggio popup. In questo caso, fare clic su **continua** toouse privilegi elevati.
2. In hello **connessione** pagina di stato, fare clic su **Connetti** connessione hello toostart. Se viene visualizzato un **Seleziona certificato** schermata, verificare che hello certificato client visualizzato sia hello uno che si desidera toouse tooconnect. In caso contrario, utilizzare hello freccia tooselect hello corretto certificato e quindi fare clic su **OK**.

  ![Connessione del client VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. Verrà stabilita la connessione.

  ![Connessione stabilita](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Risoluzione dei problemi delle connessioni P2S

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Verificare una connessione VPN hello

1. tooverify che la connessione VPN sia attiva, aprire un prompt dei comandi con privilegi elevati ed eseguire *ipconfig/all*.
2. Visualizzare i risultati di hello. Si noti che l'indirizzo IP hello che è stato ricevuto uno degli indirizzi hello compresi nell'intervallo di indirizzi di connettività Point-to-Site hello specificato al momento della creazione della rete virtuale. i risultati di Hello saranno simili toothis esempio:

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Connettere la macchina virtuale di tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>Aggiungere o rimuovere certificati radice attendibili

È possibile aggiungere e rimuovere certificati radice attendibili da Azure. Quando si rimuove un certificato radice, i client che dispongono di un certificato generato da tale radice non sarà in grado di tooauthenticate e pertanto non essere in grado di tooconnect. Se si desidera tooauthenticate un client e la connessione, è necessario tooinstall un nuovo certificato client generato da un certificato radice attendibile tooAzure (caricato).

### <a name="addtrustedroot"></a>tooadd un certificato radice attendibile

È possibile aggiungere backup too20 attendibili radice certificato con estensione cer file tooAzure. Per istruzioni, vedere [sezione 3 - file con estensione cer del certificato radice hello caricamento](#upload).

### <a name="removetrustedroot"></a>tooremove un certificato radice attendibile

1. In hello **le connessioni VPN** sezione della pagina di hello per la rete virtuale, fare clic su hello **client** tooopen grafici hello **Point-to-site VPN connessione** pagina.

  ![Client](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. In hello **connessionePoint-to-site** pagina, fare clic su **gestire i certificati** tooopen hello **certificati** pagina.<br>

  ![Pagina Certificati](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. In hello **certificati** pagina, fare clic hello i puntini di sospensione Avanti toohello certificato che desidera tooremove, quindi fare clic su **eliminare**.

  ![Eliminare un certificato radice](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>Revocare un certificato client

È possibile revocare i certificati client. certificato Hello elenco di revoche di certificati consente tooselectively negare connettività Point-to-Site in base a singoli certificati client. Questa operazione è diversa rispetto alla rimozione di un certificato radice attendibile. Se si rimuove un CER del certificato radice attendibile da Azure, comporta la revoca l'accesso per tutti i certificati client generato firmato dall'autorità di certificazione revocata hello hello. Revoca di un certificato client, anziché certificato radice hello consente hello altri certificati che sono stati generati da hello radice certificato toocontinue toobe utilizzato per l'autenticazione per la connessione hello Point-to-Site.

pratica comune Hello è accesso toouse hello radice certificato toomanage livelli team o dell'organizzazione, durante l'utilizzo dei certificati client revocati per il controllo di accesso con granularità fine per utenti singoli.

### <a name="revokeclientcert"></a>toorevoke un certificato client

È possibile revocare un certificato client tramite l'aggiunta di elenco di revoche toohello hello identificazione personale.

1. Recuperare l'identificazione personale del certificato client di hello. Per ulteriori informazioni, vedere [procedura: recuperare hello identificazione personale del certificato](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copiare l'editor di testo hello informazioni tooa e rimuovere tutti gli spazi in modo che sia una stringa continua.
3. Passare toohello **'nome di rete virtuale classica' > connessione VPN Point-to-site > certificati** pagina e quindi fare clic su **elenco di revoche di certificati** pagina elenco di revoche di certificati hello tooopen. 
4. In hello **elenco di revoche di certificati** pagina, fare clic su **+ Aggiungi certificato** tooopen hello **elenco toorevocation di Aggiungi certificato** pagina.
5. In hello **elenco toorevocation di Aggiungi certificato** pagina, incollare l'identificazione personale del certificato hello come una linea continua di testo, senza spazi. Fare clic su **OK** nella parte inferiore di hello della pagina hello.
6. Dopo l'aggiornamento è stata completata, il certificato di hello non può più essere utilizzato tooconnect. I client che tentano di tooconnect usando questo certificato, ricevono un messaggio che informa che il certificato hello non è più valido.

## <a name="faq"></a>Domande frequenti sulla connettività da punto a sito

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand informazioni sulle reti e macchine virtuali, vedere [Cenni preliminari sulla rete di Azure e VM Linux](../virtual-machines/linux/azure-vm-network-overview.md).
