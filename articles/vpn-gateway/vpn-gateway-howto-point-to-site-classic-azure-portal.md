---
title: 'Connettere un computer a una rete virtuale da punto a sito con l''autenticazione del certificato: portale di Azure classico | Microsoft Docs'
description: Connettersi in modo sicuro a una rete virtuale di Azure classica creando una connessione gateway VPN da punto a sito con il portale di Azure.
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
ms.openlocfilehash: 7805e7c91c49fe1ef2d92b64c62bbfd15ab492b5
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-certificate-authentication-classic-azure-portal"></a>Configurare una connessione da punto a sito a una rete virtuale usando l'autenticazione del certificato (versione classica): portale di Azure

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Questo articolo illustra come creare una rete virtuale con una connessione da punto a sito nel modello di distribuzione classica usando il portale di Azure. Questa configurazione usa i certificati per autenticare il client di connessione. È anche possibile creare questa configurazione usando strumenti o modelli di distribuzione diversi selezionando un'opzione differente nell'elenco seguente:

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portale di Azure (classico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

Un gateway VPN da punto a sito (P2S) consente di creare una connessione sicura alla rete virtuale da un singolo computer client. Le connessioni VPN da punto a sito sono utili per connettersi alla rete virtuale da una posizione remota, ad esempio nel caso di telecomunicazioni da casa o durante una riunione. Una VPN P2S è anche una soluzione utile da usare al posto di una VPN da sito a sito quando solo pochi client devono connettersi a una rete virtuale. 

P2S usa Secure Socket Tunneling Protocol (SSTP), un protocollo VPN basato su SSL. Una connessione VPN P2S viene stabilita avviandola dal computer client.


![Diagramma da punto a sito](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


Le connessioni da punto a sito con l'autenticazione del certificato richiedono gli elementi seguenti:

* Un gateway VPN dinamico.
* La chiave pubblica (file CER) per un certificato radice, caricato in Azure. Questo viene considerato un certificato attendibile e viene usato per l'autenticazione.
* Un certificato client generato dal certificato radice e installato in ogni computer client che effettuerà la connessione. Questo certificato viene usato per l'autenticazione client.
* Un pacchetto di configurazione client VPN deve essere generato e installato in ogni computer client che effettua la connessione. Il pacchetto di configurazione client configura il client VPN nativo già disponibile nel sistema operativo con le informazioni necessarie per la connessione alla rete virtuale.

Le connessioni da punto a sito non richiedono un dispositivo VPN o un indirizzo IP pubblico locale. La connessione VPN viene creata tramite SSTP (Secure Sockets Tunneling Protocol). Sul lato server sono supportate le versioni 1.0, 1.1 e 1.2 di SSTP. Il client decide quale versione usare. Per Windows 8.1 e versioni successive, SSTP usa per impostazione predefinita la versione 1.2. 

Per altre informazioni sulla connettività da punto a sito, consultare le [Domande frequenti sulla connettività da punto a sito](#faq) alla fine di questo articolo.

### <a name="example-settings"></a>Impostazioni di esempio

È possibile usare i valori seguenti per creare un ambiente di test o fare riferimento a questi valori per comprendere meglio gli esempi di questo articolo:

* **Nome: VNet1**
* **Spazio indirizzi: 192.168.0.0/16**<br>Per questo esempio, viene usato un solo spazio indirizzi. È possibile avere più di uno spazio indirizzi per la rete virtuale.
* **Nome subnet: FrontEnd**
* **Intervallo di indirizzi subnet: 192.168.1.0/24**
* **Sottoscrizione:** se si hanno più sottoscrizioni, verificare di usare quella corretta.
* **Gruppo di risorse: TestRG**
* **Località: Stati Uniti orientali**
* **Tipo di connessione: Da punto a sito**
* **: 172.16.201.0/24**. I client VPN che si connettono alla rete virtuale con questa connessione da punto a sito ricevono un indirizzo IP dal pool specificato.
* **GatewaySubnet: 192.168.200.0/24**. La subnet del gateway deve usare il nome "GatewaySubnet".
* **Dimensioni:** selezionare lo SKU di gateway da usare.
* **Tipo di routing: Dinamico**

## <a name="vnetvpn"></a>1. Creare una rete virtuale e un gateway VPN

Prima di iniziare, verificare di possedere una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial).

### <a name="createvnet"></a>Parte 1: Creare una rete virtuale

Se non si ha una rete virtuale, crearne una. Gli screenshot sono forniti come esempio. Assicurarsi di sostituire i valori con i propri. Per creare una rete virtuale usando il portale di Azure, seguire questa procedura:

1. In un browser passare al [portale di Azure](http://portal.azure.com) e, se necessario, accedere con l'account Azure.
2. Fare clic su **New**. Nel campo **Cerca nel Marketplace** digitare "Rete virtuale". Individuare **Rete virtuale** nell'elenco restituito e fare clic per aprire la pagina **Rete virtuale**.

  ![pagina di ricerca della rete virtuale](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Nella parte inferiore della pagina Rete virtuale selezionare **Classica** nell'elenco **Selezionare un modello di distribuzione** e quindi fare clic su **Crea**.

  ![Selezionare il modello di distribuzione](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. Nella pagina **Crea rete virtuale** configurare le impostazioni della rete virtuale. Aggiungere a questa pagina il primo spazio di indirizzi e l'intervallo di indirizzi di una subnet singola. Dopo aver creato la rete virtuale, è possibile tornare indietro e aggiungere altre subnet e altri spazi di indirizzi.

  ![Pagina Crea rete virtuale](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. Verificare che la **sottoscrizione** sia quella corretta. È possibile cambiare sottoscrizione tramite l'elenco a discesa.
6. Fare clic su **Gruppo di risorse** e selezionare un gruppo di risorse esistente o crearne uno nuovo digitandone il nome. Se si crea un nuovo gruppo di risorse, denominare il gruppo in base ai valori di configurazione pianificati. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Selezionare quindi le impostazioni relative alla **località** per la rete virtuale. La località determina la posizione in cui risiedono le risorse distribuite in questa rete virtuale.
8. Selezionare **Aggiungi al dashboard** se si vuole trovare facilmente la rete virtuale nel dashboard e quindi fare clic su **Crea**.

  ![Aggiungi al dashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. Dopo aver fatto clic su Crea, nel dashboard viene visualizzato un riquadro che riflette lo stato di avanzamento della rete virtuale. Il riquadro cambia durante la creazione della rete virtuale.

  ![Pannello Creazione della rete virtuale](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. Al termine della creazione della rete virtuale, nella pagina Reti del portale di Azure classico verrà visualizzato **Creato** in **Stato**.
11. Aggiungere un server DNS (facoltativo). Dopo aver creato la rete virtuale, è possibile aggiungere l'indirizzo IP di un server DNS per la risoluzione dei nomi. L'indirizzo IP del server DNS specificato deve essere l'indirizzo di un server DNS in grado di risolvere i nomi per le risorse della rete virtuale.<br>Per aggiungere un server DNS, aprire le impostazioni della rete virtuale, fare clic su Server DNS e aggiungere l'indirizzo IP del server DNS da usare.

### <a name="gateway"></a>Parte 2: Creare una subnet del gateway e un gateway di routing dinamico

In questo passaggio vengono creati una subnet del gateway e un gateway di routing dinamico. Nel portale di Azure per il modello di distribuzione classica è possibile creare la subnet del gateway e il gateway usando le stesse pagine di configurazione.

1. Nel portale passare alla rete virtuale per cui si vuole creare un gateway.
2. Nella pagina **Panoramica** della pagina della rete virtuale fare clic su **Gateway** nella sezione Connessioni VPN.

  ![Fare clic per creare un gateway](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. Nella pagina **Nuova connessione VPN** selezionare **Da punto a sito**.

  ![Tipo di connessione da punto a sito](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. In **Spazio indirizzi client** aggiungere l'intervallo di indirizzi IP, da cui i client VPN ricevono un indirizzo IP al momento della connessione. Usare un intervallo di indirizzi IP privati che non si sovrapponga con la posizione locale da cui verrà effettuata la connessione o con la rete virtuale a cui ci si vuole connettere. È possibile eliminare l'intervallo compilato automaticamente e quindi aggiungere l'intervallo di indirizzi IP privati da usare.

  ![Spazio indirizzi client](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. Selezionare la casella di controllo **Crea gateway immediatamente**.

  ![Crea gateway immediatamente](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. Fare clic su **Configurazione gateway facoltativa** per aprire la pagina **Configurazione gateway**.

  ![Fare clic su Configurazione gateway facoltativa](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. Fare clic su **Subnet Configure required settings** (Configura impostazioni necessarie subnet) per aggiungere la **subnet del gateway**. Nonostante sia possibile creare una subnet del gateway con dimensioni di /29 soltanto, è consigliabile crearne una più grande che includa più indirizzi selezionando almeno /28 o /27. In questo modo saranno disponibili indirizzi sufficienti per supportare in futuro le possibili configurazioni aggiuntive desiderate. Quando si usano le subnet del gateway, evitare di associare un gruppo di sicurezza di rete (NSG) alla subnet del gateway. Se si associa un gruppo di sicurezza di rete a tale subnet, il gateway VPN potrebbe smettere di funzionare come previsto.

  ![Aggiungere GatewaySubnet](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. Selezionare le **dimensioni** del gateway, che rappresentano lo SKU di gateway per il gateway di rete virtuale. Nel portale, lo SKU predefinito è **Basic**. Per altre informazioni sugli SKU di gateway, vedere [Informazioni sulle impostazioni del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

  ![Dimensioni del gateway](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. Selezionare il **tipo di routing** per il gateway. Le configurazioni P2S richiedono il tipo di routing **Dinamico**. Al termine della configurazione della pagina, fare clic su **OK**.

  ![Configurare il tipo di routing](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. Nella pagina **Nuova connessione VPN** fare clic su **OK** nella parte inferiore per iniziare a creare il gateway di rete virtuale. Per il completamento di un gateway VPN possono essere necessari fino a 45 minuti, in base allo SKU selezionato per il gateway.

## <a name="generatecerts"></a>2. Creare i certificati

I certificati vengono usati da Azure per autenticare i client VPN per VPN da punto a sito. È necessario caricare le informazioni della chiave pubblica del certificato radice in Azure. La chiave pubblica viene quindi considerata "attendibile". I certificati client devono essere generati dal certificato radice attendibile e quindi installati in ogni computer client nell'archivio certificati Certificati - Utente corrente/Personale. Il certificato viene usato per l'autenticazione del client all'avvio di una connessione alla rete virtuale. 

Se usati, i certificati autofirmati devono essere creati con parametri specifici. È possibile creare un certificato autofirmato seguendo le istruzioni per [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md) o [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). È importante seguire i passaggi di queste istruzioni quando si usano i certificati radice autofirmati e si generano certificati client dal certificato radice autofirmato. In caso contrario, i certificati creati non saranno compatibili con le connessioni P2S e si riceverà un errore di connessione.

### <a name="cer"></a>Parte 1: Ottenere il file di chiave pubblica (con estensione cer) per il certificato radice

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>Parte 2: Generare un certificato client

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Caricare il file CER del certificato radice

Dopo la creazione del gateway, è possibile caricare il file con estensione cer, che contiene le informazioni sulla chiave pubblica, per un certificato radice attendibile in Azure. Non si può caricare la chiave privata per il certificato radice in Azure. Al termine del caricamento di un file CER, Azure lo può usare per autenticare i client che hanno installato un certificato client generato dal certificato radice attendibile. È possibile caricare fino a 20 file di certificato radice attendibile aggiuntivi in un secondo momento, se necessario.  

1. Nella sezione **Connessioni VPN** della pagina della rete virtuale fare clic sull'icona **client** per aprire la pagina **Connessione VPN da punto a sito**.

  ![Client](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Nella pagina **Connessione VPN da punto a sito** fare clic su **Gestisci certificato** per aprire la pagina **Certificati**.<br>

  ![Pagina Certificati](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Nella pagina **Certificati** fare clic su **Carica** per aprire la pagina **Carica certificato**.<br>

    ![Pagina Carica certificato](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Fare clic sull'icona della cartella per cercare il file CER. Selezionare il file e quindi fare clic su **OK**. Aggiornare la pagina per visualizzare il certificato caricato nella pagina **Certificati**.

  ![Caricamento del certificato](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Configurare il client

Per connettersi a una rete virtuale tramite VPN da punto a sito, ogni client deve installare un pacchetto per configurare il client VPN di Windows nativo. Il pacchetto di configurazione configura il client VPN nativo di Windows con le impostazioni necessarie per la connessione alla rete virtuale.

È possibile usare lo stesso pacchetto di configurazione del client VPN in ogni computer client, a condizione che la versione corrisponda all'architettura del client. Per l'elenco dei sistemi operativi client supportati, vedere [Domande frequenti sulla connettività da punto a sito](#faq) alla fine di questo articolo.

### <a name="generateconfigpackage"></a>Parte 1: Generare e installare il pacchetto di configurazione del client VPN

1. Nella pagina **Panoramica** della rete virtuale nel portale di Azure fare clic sull'icona relativa ai client in **Connessioni VPN** per aprire la pagina **Connessione VPN da punto a sito**.
2. Nella parte superiore della pagina **Connessione VPN da punto a sito** fare clic sul pacchetto di download corrispondente al sistema operativo client in cui verrà installato:

  * Per client a 64 bit, selezionare **Client VPN (64 bit)**.
  * Per client a 32 bit, selezionare **Client VPN (32 bit)**.

  ![Scaricare il pacchetto di configurazione del client VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. Dopo che è stato generato, scaricare e installare il pacchetto nel computer client. Se viene visualizzato un popup SmartScreen, fare clic su **Altre informazioni** e quindi su **Esegui comunque** per installare il pacchetto. È anche possibile salvare il pacchetto per l'installazione su altri computer client.

### <a name="installclientcert"></a>Parte 2: Installare il certificato client

Se si vuole creare una connessione da punto a sito da un computer client diverso da quello usato per generare i certificati client, è necessario installare un certificato client. Quando si installa un certificato client, è necessaria la password che è stata creata durante l'esportazione del certificato client. In genere è sufficiente fare doppio clic sul certificato e installarlo. Per altre informazioni, vedere [Installare un certificato client esportato](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>5. Connect to Azure

### <a name="connect-to-your-vnet"></a>Connettersi alla rete virtuale

1. Per connettersi alla rete virtuale, nel computer client passare alle connessioni VPN e individuare quella creata, che ha lo stesso nome della rete virtuale locale. Fare clic su **Connetti**. È possibile che venga visualizzato un messaggio popup che fa riferimento all'uso del certificato. In questo caso, fare clic su **Continua** per usare privilegi elevati.
2. Nella pagina **Stato connessione** fare clic su **Connetti** per avviare la connessione. Se viene visualizzato un **Seleziona certificato** dello schermo, verificare che il certificato client visualizzato sia quello che si desidera utilizzare per la connessione. In caso contrario, usare la freccia a discesa per selezionare il certificato corretto e quindi fare clic su **OK**.

  ![Connessione del client VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. Verrà stabilita la connessione.

  ![Connessione stabilita](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Risoluzione dei problemi delle connessioni P2S

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Verificare la connessione VPN

1. Per verificare che la connessione VPN è attiva, aprire un prompt dei comandi con privilegi elevati ed eseguire *ipconfig/all*.
2. Visualizzare i risultati. Si noti che l'indirizzo IP ricevuto è uno degli indirizzi compresi nell'intervallo di indirizzi di connettività da punto a sito specificato al momento della creazione della rete virtuale. I risultati dovrebbero essere simili all'esempio seguente:

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

## <a name="connectVM"></a>Connettersi a una macchina virtuale

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>Aggiungere o rimuovere certificati radice attendibili

È possibile aggiungere e rimuovere certificati radice attendibili da Azure. Quando si rimuove un certificato radice, i client con un certificato generato da tale radice non potranno eseguire l'autenticazione e quindi non potranno connettersi. Per consentire ai client di eseguire l'autenticazione e connettersi, è necessario installare un nuovo certificato client generato da un certificato radice considerato attendibile (caricato) in Azure.

### <a name="addtrustedroot"></a>Per aggiungere un certificato radice attendibile

In Azure è possibile aggiungere fino a 20 file CER di certificato radice trusted. Per istruzioni, vedere [Sezione 3: Caricare il file CER del certificato radice](#upload).

### <a name="removetrustedroot"></a>Per rimuovere un certificato radice attendibile

1. Nella sezione **Connessioni VPN** della pagina della rete virtuale fare clic sull'icona **client** per aprire la pagina **Connessione VPN da punto a sito**.

  ![Client](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Nella pagina **Connessione VPN da punto a sito** fare clic su **Gestisci certificato** per aprire la pagina **Certificati**.<br>

  ![Pagina Certificati](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Nella pagina **Certificati** fare clic sui puntini di sospensione accanto al certificato che si vuole rimuovere e quindi fare clic su **Elimina**.

  ![Eliminare un certificato radice](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>Revocare un certificato client

È possibile revocare i certificati client. L'elenco di revoche di certificati consente di negare in modo selettivo la connettività da punto a sito basata sui singoli certificati client. Questa operazione è diversa rispetto alla rimozione di un certificato radice attendibile. Se si rimuove un file con estensione cer del certificato radice attendibile da Azure, viene revocato l'accesso per tutti i certificati client generati o firmati dal certificato radice revocato. La revoca di un certificato client, anziché del certificato radice, consente di continuare a usare gli altri certificati generati dal certificato radice per l'autenticazione per la connessione da punto a sito.

La regola generale è quella di usare il certificato radice per gestire l'accesso a livello di team o organizzazione, usando i certificati client revocati per il controllo di accesso con granularità fine su singoli utenti.

### <a name="revokeclientcert"></a>Per revocare un certificato client

È possibile revocare un certificato client aggiungendo l'identificazione personale all'elenco di revoche di certificati.

1. Ottenere l'identificazione personale del certificato client. Per altre informazioni, vedere [Procedura: recuperare l'identificazione personale di un certificato](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copiare le informazioni in un editor di testo e rimuovere tutti gli spazi in modo che sia una stringa continua.
3. Passare alla pagina **"nome rete virtuale classica" > Connessione VPN da punto a sito > Certificati** e quindi fare clic su **Elenco di revoche** per aprire la pagina Elenco di revoche. 
4. Nella pagina **Elenco di revoche** fare clic su **+Aggiungi certificato** per aprire la pagina **Aggiungi certificato all'elenco di revoche**.
5. Nella pagina **Aggiungi certificato all'elenco di revoche** incollare l'identificazione personale del certificato come una riga di testo continua, senza spazi. Fare clic su **OK** nella parte inferiore della pagina.
6. Dopo aver completato l'aggiornamento, il certificato non può più essere usato per la connessione. Ai client che provano a connettersi con questo certificato verrà visualizzato un messaggio che informa che il certificato non è più valido.

## <a name="faq"></a>Domande frequenti sulla connettività da punto a sito

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-faq-point-to-site-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver completato la connessione, è possibile aggiungere macchine virtuali alle reti virtuali. Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). Per altre informazioni sulla rete e sulle macchine virtuali, vedere [Panoramica di rete delle macchine virtuali Linux e Azure](../virtual-machines/linux/azure-vm-network-overview.md).