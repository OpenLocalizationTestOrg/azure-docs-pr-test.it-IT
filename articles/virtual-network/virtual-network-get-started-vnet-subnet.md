---
title: il primo virtuale di Azure di rete aaaCreate | Documenti Microsoft
description: Informazioni su come connettere due macchine virtuali (VM) toohello rete virtuale, toocreate una rete virtuale di Azure (VNet) e connettere le macchine virtuali toohello.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2016
ms.author: jdial
ms.openlocfilehash: 1981524cf706d5ebc83b1ff77735617550ff058a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-virtual-network"></a>Creare la prima rete virtuale

Informazioni su come toocreate una rete virtuale (VNet) con due subnet, creare due macchine virtuali (VM) e connettersi tooone ogni macchina virtuale delle subnet hello, come illustrato nella seguente immagine hello:

![Diagramma della rete virtuale](./media/virtual-network-get-started-vnet-subnet/vnet-diagram.png)

Una rete virtuale di Azure (VNet) è una rappresentazione della rete nel cloud hello. È possibile controllare le impostazioni della rete di Azure network e definire blocchi di indirizzi DHCP, impostazioni DNS, criteri di sicurezza e routing. informazioni sui concetti di rete virtuale, leggere hello toolearn [Panoramica di rete virtuale](virtual-networks-overview.md) articolo. Risorse di hello toocreate mostrate nell'immagine hello i passaggi seguenti di hello completa:

1. [Creare una rete virtuale con due subnet](#create-vnet)
2. [Creare due macchine virtuali, ciascuno con un'interfaccia di rete (NIC)](#create-vms)e associare un tooeach di gruppo () di sicurezza di rete NIC
3. [Connettersi tooand da hello macchine virtuali](#connect-to-from-vms)
4. [Eliminare tutte le risorse](#delete-resources). Si incorrere in costi per alcune delle risorse di hello create in questo esercizio, mentre si esegue il provisioning. gli addebiti di hello toominimize, dopo aver completato l'esercizio hello, assicurarsi hello toocomplete i passaggi in questa sezione toodelete hello delle risorse create.

Si avrà una conoscenza di base di come è possibile utilizzare una rete virtuale dopo il completamento hello i passaggi in questo articolo. Passaggi successivi vengono forniti in modo da acquisire ulteriori informazioni su toouse reti virtuali a un livello più profondo.

## <a name="create-vnet"></a>Creare una rete virtuale con due subnet

toocreate una rete virtuale con due subnet, passaggi hello completo. Subnet diverse sono in genere utilizzato flusso hello toocontrol del traffico tra subnet.

1. Accedi toohello [portale di Azure](<https://portal.azure.com>). Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free). 
2. In hello **Preferiti** riquadro, del portale di hello, fare clic su **New**.
3. In hello **New** pannello, fare clic su **rete**. In hello **rete** pannello, fare clic su **rete virtuale**, come illustrato nella seguente immagine hello:

    ![Diagramma della rete virtuale](./media/virtual-network-get-started-vnet-subnet/virtual-network.png)

4.  In hello **rete virtuale** pannello, lasciare *Gestione risorse* selezionata come modello di distribuzione hello, fare clic su **crea**.
5.  In hello **blade di rete virtuale crea** che viene visualizzata, immettere i seguenti valori hello, quindi fare clic su **crea**:

    |**Impostazione**|**Valore**|**Dettagli**|
    |---|---|---|
    |**Nome**|*MyVNet*|nome Hello deve essere univoco nel gruppo di risorse hello.|
    |**Spazio degli indirizzi**|*10.0.0.0/16*|È possibile specificare uno spazio degli indirizzi a piacere usando la notazione CIDR.|
    |**Nome della subnet**|*Front-end*|nome della subnet Hello deve essere univoco nella rete virtuale hello.|
    |**Intervallo di indirizzi subnet**|*10.0.0.0/24*| intervallo di Hello specificato deve essere presente nello spazio di indirizzi hello che è definito per la rete virtuale hello.|
    |**Sottoscrizione**|*[Sottoscrizione in uso]*|Selezionare un hello toocreate sottoscrizione rete virtuale in. Una rete virtuale può essere presente all'interno di una sola sottoscrizione.|
    |**Gruppo di risorse**|**Crea nuovo:** *MyRG*|Creare un gruppo di risorse. nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata. ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) articolo introduttivo.|
    |**Posizione**|*Stati Uniti occidentali*| In genere viene selezionata percorso hello ubicazione tooyour più vicino.|

    Hello accetta di rete virtuale toocreate di pochi secondi. Una volta creato, viene visualizzato hello Azure dashboard del portale.

6. Con la rete virtuale di hello creato, nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**. Fare clic su hello **MyVNet** rete virtuale in hello **tutte le risorse** blade. Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere *MyVNet* in hello **filtrare in base al nome...** hello accesso casella tooeasily rete virtuale.
7. Hello **MyVNet** pannello apre e Visualizza informazioni su hello rete virtuale, come illustrato nella seguente immagine hello:

    ![Diagramma della rete virtuale](./media/virtual-network-get-started-vnet-subnet/myvnet.png)

8. Come illustrato nell'immagine precedente hello, fare clic su **subnet** toodisplay un elenco di subnet hello all'interno di hello rete virtuale. Hello solo subnet esistente è **front-end**, hello subnet creato nel passaggio 5.
9. In hello MyVNet - pannello subnet, fare clic su **+ Subnet** toocreate una subnet con hello seguenti informazioni e fare clic su **OK** subnet hello toocreate:

    |**Impostazione**|**Valore**|**Dettagli**|
    |---|---|---|
    |**Nome**|*Back-end*|nome Hello deve essere univoco nella rete virtuale hello.|
    |**Intervallo di indirizzi**|*10.0.1.0/24*|intervallo di Hello specificato deve essere presente nello spazio di indirizzi hello che è definito per la rete virtuale hello.|
    |**Gruppo di sicurezza di rete** e **Tabella di route**|*Nessuno* (impostazione predefinita)|I gruppi di sicurezza di rete sono descritti più avanti in questo articolo. altre informazioni sulle route definite dall'utente, leggere hello toolearn [le route definite dall'utente](virtual-networks-udr-overview.md) articolo.|

10. Dopo l'aggiunta di nuova subnet hello toohello rete virtuale, è possibile chiudere hello **MyVNet – subnet** pannello, quindi chiudere hello **tutte le risorse** blade.

## <a name="create-vms"></a>Creare macchine virtuali

Con hello tra reti virtuali e subnet creata, è possibile creare le macchine virtuali hello. Per questo esercizio, entrambe le macchine virtuali eseguire hello del sistema operativo di Windows Server, tuttavia possono eseguire qualsiasi sistema operativo supportato da Azure, incluse diverse diverse distribuzioni di Linux.

### <a name="create-web-server-vm"></a>Creare una macchina virtuale del server web hello

toocreate hello web macchina virtuale del server, hello completo alla procedura seguente:

1. Nel riquadro di hello Preferiti portale Azure, fare clic su **New**, **calcolo**, quindi **Data Center di Windows Server 2016**.
2. In hello **Data Center di Windows Server 2016** pannello, fare clic su **crea**.
3. In hello **nozioni di base** blade che viene visualizzata, immettere o selezionare hello i valori seguenti e fare clic su **OK**:

    |**Impostazione**| **Valore**|**Dettagli**|
    |---|---|---|
    |**Nome**|*MyWebServer*|Questa VM funge da server Web a cui si connettono le risorse Internet.|
    |**Tipo di disco VM**|*SSD*|
    |**Nome utente**|*A scelta dell'utente*|
    |**Password e Conferma password**|*A scelta dell'utente*|
    | **Sottoscrizione**|*<Your subscription>*|deve essere sottoscrizione Hello hello stessa sottoscrizione selezionata nel passaggio 5 di hello [creare una rete virtuale con due subnet](#create-vnet) sezione di questo articolo. rete virtuale si connette un toomust VM Hello esiste in hello stessa sottoscrizione, come hello macchina virtuale.|
    |**Gruppo di risorse**|**Usare il gruppo di risorse esistente:** Selezionare *MyRG*|Se viene usata nello stesso gruppo di risorse, come è stato fatto per la rete virtuale, hello hello hello risorse non presenti tooexist hello stesso gruppo di risorse.|
    |**Posizione**|*Stati Uniti occidentali*|deve trattarsi di Hello hello stesso percorso specificato nel passaggio 5 di hello [creare una rete virtuale con due subnet](#create-vnet) sezione di questo articolo. Macchine virtuali e reti virtuali che si connettono toomust hello un esiste in hello stesso percorso.|

4. In hello **scegliere una dimensione** pannello, fare clic su *DS1_V2 Standard*, quindi fare clic su **selezionare**. Hello lettura [dimensioni delle macchine Virtuali di Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo per un elenco di tutte le dimensioni di macchina virtuale di Windows supportate da Azure.
5. In hello **impostazioni** pannello, immettere o selezionare i seguenti valori hello e fare clic su **OK**:

    |**Impostazione**|**Valore**|**Dettagli**|
    |---|---|---|
    |**Archiviazione: Usa dischi gestiti**|*Sì*||
    |**Rete virtuale**| Selezionare *MyVNet*|È possibile selezionare qualsiasi rete virtuale presente in hello stesso percorso come hello macchina virtuale che si sta creando. altre informazioni sulle reti virtuali e le subnet, leggere hello toolearn [rete virtuale](virtual-networks-overview.md) articolo.|
    |**Subnet**|Selezionare *Front-end*|È possibile selezionare qualsiasi subnet che esiste all'interno di hello rete virtuale.|
    |**Indirizzo IP pubblico**|Accettare l'impostazione predefinita hello|Consente a un indirizzo IP pubblico è tooconnect toohello VM da hello Internet. informazioni su indirizzi IP pubblici, leggere hello toolearn [gli indirizzi IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) articolo.|
    |**Gruppo di sicurezza di rete (firewall)**|Accettare l'impostazione predefinita hello|Fare clic su hello **MyWebServer (nuovo)-nsg** portale hello di gruppo predefinito creato tooview le relative impostazioni. In hello **Crea gruppo di sicurezza di rete** blade che viene aperto, si noti che è una regola in entrata che consenta il traffico TCP/3389 (RDP) da qualsiasi indirizzo IP di origine.|
    |**Tutti gli altri valori**|Accettare le impostazioni predefinite hello|altre informazioni sulle impostazioni, leggere hello rimanenti hello toolearn [sulla VM](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.|

    Gruppi di sicurezza di rete (gruppo) consentono di toocreate le regole in entrata e in uscita per il tipo di hello del traffico di rete che può propagare tooand da hello VM. Per impostazione predefinita, tutto il traffico in entrata toohello VM viene negato. È possibile aggiungere altre regole in ingresso per TCP/80 (HTTP) e TCP/443 (HTTPS) per un server Web di produzione. Non sono presenti regole per il traffico in uscita perché tutto il traffico in uscita è consentito per impostazione predefinita. È possibile aggiungere/rimuovere traffico toocontrol regole per i criteri. Hello lettura [gruppi di sicurezza di rete](virtual-networks-nsg.md) toolearn articolo ulteriori informazioni sulla NSGs.

6.  In hello **riepilogo** pannello, rivedere le impostazioni di hello e fare clic su **OK** toocreate hello macchina virtuale. Un riquadro di stato viene visualizzato nel dashboard del portale hello come hello che crea macchina virtuale. Potrebbe richiedere alcuni minuti toocreate. Non è necessario toowait per tale toocomplete. È possibile continuare toohello il passaggio successivo durante la creazione della macchina virtuale hello.

### <a name="create-database-server-vm"></a>Creare server di database hello VM

toocreate hello server di database VM, hello completo alla procedura seguente:

1.  Nel riquadro di hello Preferiti, fare clic su **New**, **calcolo**, quindi **Data Center di Windows Server 2016**.
2.  In hello **Data Center di Windows Server 2016** pannello, fare clic su **crea**.
3.  In hello **pannello nozioni di base**, immettere o selezionare i seguenti valori hello, quindi fare clic su **OK**:

    |**Impostazione**|**Valore**|**Dettagli**|
    |---|---|---|
    |**Nome**|*MyDBServer*|Questa macchina virtuale funge da un server di database che hello web server si connette a, ma tale hello Internet non è possibile connettersi.|
    |**Tipo di disco VM**|*SSD*||
    |**Nome utente**|A scelta dell'utente||
    |**Password e Conferma password**|A scelta dell'utente||
    |**Sottoscrizione**|<Your subscription>|deve essere sottoscrizione Hello hello stessa sottoscrizione selezionata nel passaggio 5 di hello [creare una rete virtuale con due subnet](#create-vnet) sezione di questo articolo.|
    |**Gruppo di risorse**|**Usare il gruppo di risorse esistente:** Selezionare *MyRG*|Se viene usata nello stesso gruppo di risorse, come è stato fatto per la rete virtuale, hello hello hello risorse non presenti tooexist hello stesso gruppo di risorse.|
    |**Posizione**|*Stati Uniti occidentali*|deve trattarsi di Hello hello stesso percorso specificato nel passaggio 5 di hello [creare una rete virtuale con due subnet](#create-vnet) sezione di questo articolo.|

4.  In hello **scegliere una dimensione** pannello, fare clic su *DS1_V2 Standard*, quindi fare clic su **selezionare**.
5.  In hello **impostazioni** pannello, immettere o selezionare i seguenti valori hello e fare clic su **OK**:

    |**Impostazione**|**Valore**|**Dettagli**|
    |----|----|---|
    |**Archiviazione: Usa dischi gestiti**|*Sì*||
    |**Rete virtuale**|Selezionare *MyVNet*|È possibile selezionare qualsiasi rete virtuale presente in hello stesso percorso come hello macchina virtuale che si sta creando.|
    |**Subnet**|Selezionare *Back-end* facendo hello **Subnet** casella, quindi selezionando **Back-end** da hello **scegliere una subnet** pannello|È possibile selezionare qualsiasi subnet che esiste all'interno di hello rete virtuale.|
    |**Indirizzo IP pubblico**|None: fare clic su indirizzo predefinito hello, quindi fare clic su **Nessuno** da hello **scegliere l'indirizzo IP pubblico** pannello|Senza un indirizzo IP pubblico, è possibile connettersi solo toohello macchina virtuale da un'altra macchina virtuale connessa toohello stessa rete virtuale. È possibile connettersi tooit direttamente da Internet hello.|
    |**Gruppo di sicurezza di rete (firewall)**|Accettare l'impostazione predefinita hello| Predefinito hello che NSG creati anche per hello VM MyWebServer, questo gruppo è hello stessa impostazione predefinita la regola in ingresso. È possibile aggiungere un'altra regola in ingresso per TCP/1433 (MS SQL) per un server di database. Non sono presenti regole per il traffico in uscita perché tutto il traffico in uscita è consentito per impostazione predefinita. È possibile aggiungere/rimuovere traffico toocontrol regole per i criteri.|
    |**Tutti gli altri valori**|Accettare le impostazioni predefinite hello||

6.  In hello **riepilogo** pannello, rivedere le impostazioni di hello e fare clic su **OK** toocreate hello macchina virtuale. Un riquadro di stato viene visualizzato nel dashboard del portale hello come hello che crea macchina virtuale. Potrebbe richiedere alcuni minuti toocreate. Non è necessario toowait per tale toocomplete. È possibile continuare toohello il passaggio successivo durante la creazione della macchina virtuale hello.

## <a name="review"></a>Esaminare le risorse

Quando si crea una rete virtuale e due macchine virtuali, portale di Azure create diverse risorse aggiuntive nel gruppo di risorse MyRG hello hello. Esaminare il contenuto di hello del gruppo di risorse MyRG hello completando hello alla procedura seguente:

1. In hello **Preferiti** riquadro, fare clic su **più servizi**.
2. In hello **più servizi** riquadro, digitare *gruppi di risorse* nella casella hello che contiene la parola hello *filtro* in essa contenuti. Fare clic su **gruppi di risorse** quando viene visualizzato in hello elenco filtrato.
3. In hello **gruppi di risorse** riquadro, fare clic su hello *MyRG* gruppo di risorse. Se si dispone di molti gruppi di risorse esistente nella sottoscrizione, è possibile digitare *MyRG* nella casella hello contenente testo hello *filtrare in base al nome...* gruppo di risorse MyRG hello accesso tooquickly.
4.  In hello **MyRG** pannello viene visualizzato il gruppo di risorse hello include 12 risorse, come illustrato nella seguente immagine hello:

    ![Contenuto del gruppo di risorse](./media/virtual-network-get-started-vnet-subnet/resource-group-contents.png)

altre informazioni sulle macchine virtuali, dischi e gli account di archiviazione, leggere hello toolearn [macchina virtuale](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [disco](../virtual-machines/windows/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-network%2ftoc.json), e [account di archiviazione](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articoli Panoramica. È possibile visualizzare hello due NSGs hello portale predefinito creato. È inoltre possibile visualizzare il portale di hello creato due risorse di rete (NIC) di interfaccia. Una scheda di rete consente una risorsa di macchina virtuale tooconnect tooother su hello rete virtuale. Hello lettura [NIC](virtual-network-network-interface.md) toolearn articolo ulteriori informazioni sulle schede di rete. portale Hello creata anche una risorsa di indirizzo IP pubblico. Un indirizzo IP pubblico consiste in una singola impostazione per una risorsa indirizzo IP pubblico. informazioni su indirizzi IP pubblici, leggere hello toolearn [gli indirizzi IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) articolo.

## <a name="connect-to-from-vms"></a>Connettere le macchine virtuali toohello

Con la rete virtuale e due macchine virtuali create, è ora possibile connettersi le macchine virtuali toohello completando i passaggi hello hello le sezioni seguenti:

### <a name="connect-from-internet"></a>Connessione macchina virtuale del server web toohello da hello Internet

tooconnect toohello server web VM hello Internet, hello completo alla procedura seguente:

1. Nel portale di hello, gruppo di risorse MyRG hello aprire completando hello passaggi hello [risorse](#review) sezione di questo articolo.
2. In hello **MyRG** pannello, fare clic su hello **MyWebServer** macchina virtuale.
3. In hello **MyWebServer** pannello, fare clic su **Connetti**, come illustrato nella seguente immagine hello:

    ![Connettere il server tooweb VM](./media/virtual-network-get-started-vnet-subnet/webserver.png)

4. Consenti il hello toodownload browser *MyWebServer.rdp* file, quindi aprirlo.
5. Se si riceve una casella di finestra di dialogo che informa è il server di pubblicazione hello di connessione remota hello non può essere verificato, fare clic su **Connetti**.
6. Quando si immettono le credenziali, assicurarsi di accedere al nome utente hello e la password specificati nel passaggio 3 di hello [macchina virtuale del server web crea hello](#create-web-server-vm) sezione di questo articolo. Se hello **la sicurezza di Windows** visualizzata non vengono elencati le credenziali corrette hello, potrebbe essere necessario tooclick **altre scelte**, quindi **utilizzare un account diverso**, in modo da poter specificare il nome utente corretto hello e password). Fare clic su **OK** tooconnect toohello macchina virtuale.
7. Se si riceve un **connessione Desktop remoto** casella che informa che l'identità del computer remoto hello hello non è possibile verificare, fare clic su **Sì**.
8. Questo punto si è connesso toohello MyWebServer VM da hello Internet. Lasciare la connessione di desktop remoto di hello passaggi hello toocomplete aperto nella sezione successiva hello.

connessione remota Hello è l'indirizzo IP pubblico toohello assegnato toohello pubblica IP indirizzo risorse hello portale creato nel passaggio 5 di hello [creare una rete virtuale con due subnet](#create-vnet) sezione di questo articolo. connessione Hello è consentita perché la regola predefinita di hello creato in hello **MyWebServer nsg** NSG consentito TCP/3389 (RDP) in entrata toohello macchina virtuale da qualsiasi indirizzo IP di origine. Se si tenta di tooconnect toohello VM su qualsiasi altra porta, hello connessione ha esito negativo, a meno che non si aggiunge ulteriori regole connessioni in entrata toohello NSG consentendo hello porte aggiuntive.

>[!NOTE]
>Se si aggiunta altre regole in entrata toohello NSG, verificare che hello stesse porte sono aperte sul firewall di Windows hello o hello connessione ha esito negativo.
>

### <a name="connect-to-internet"></a>Connettersi a Internet toohello dalla macchina virtuale del server web hello

tooconnect toohello in uscita Internet dal server web hello VM, hello completo alla procedura seguente:

1. Se si dispone già di una connessione remota di toohello MyWebServerVM aprire, rendere toohello una connessione remota VM completando i passaggi hello hello [Connetti toohello server web VM hello Internet](#connect-from-internet) sezione di questo articolo.
2. Dal desktop di Windows hello, aprire Internet Explorer. In hello **programma di installazione di Internet Explorer 11** la finestra di dialogo, fare clic su **non usano le impostazioni consigliate**, quindi fare clic su **OK**. È consigliato tooaccept hello impostazioni consigliata per un server di produzione.
3. Nella barra degli indirizzi di Internet Explorer hello, immettere [bing.com](http:www.bing.com). Se si riceve una finestra di dialogo di Internet Explorer, fare clic su **Aggiungi**, quindi **Aggiungi** in hello **siti attendibili** la finestra di dialogo e fare clic su **Chiudi**. Ripetere questa procedura per qualsiasi altra finestra di dialogo di Internet Explorer.
4. Pagina di ricerca in Bing hello, immettere *whatsmyipaddress*, quindi fare clic su pulsante di ingrandimento hello. Bing restituisce hello pubblica risorsa indirizzo IP assegnato toohello pubblica IP indirizzo creata dal portale hello hello macchina virtuale. Se si esaminano le impostazioni di hello per hello **MyWebServer ip** risorse, vedere hello stesso indirizzo IP assegnato a risorsa di indirizzo IP pubblico toohello, come mostrato nell'immagine di hello che segue. Hello IP indirizzo assegnato tooyour macchina virtuale è diverso, tuttavia.

    ![Connettere il server tooweb VM](./media/virtual-network-get-started-vnet-subnet/webserver-pip.png)

5.  Lasciare la connessione di desktop remoto di hello passaggi hello toocomplete aperto nella sezione successiva hello.

Si è in grado di tooconnect toohello Internet da hello macchina virtuale perché la connettività in uscita dalla VM hello è consentita per impostazione predefinita. È possibile limitare la connettività in uscita tramite l'aggiunta di addizione regole toohello NSG applicato toohello NIC, hello subnet toohello connessa, o entrambi.

Se hello VM viene inserita nella hello arrestato (deallocato) tramite il portale di hello, indirizzo IP pubblico hello è possibile modificare. Se è necessario l'indirizzo IP pubblico hello indirizzo mai modificare, è possibile utilizzare il metodo di allocazione statica hello per indirizzo IP di hello, anziché come metodo di allocazione dinamica di hello (ovvero hello (impostazione predefinita). altre informazioni sulle toolearn hello differenze tra i metodi di allocazione, leggere hello [tipi e metodi di allocazione di indirizzi IP](virtual-network-ip-addresses-overview-arm.md) articolo.

### <a name="webserver-to-dbserver"></a>Connettere il server di database toohello macchina virtuale dalla macchina virtuale del server web hello

tooconnect toohello passava VM dal server web hello VM, hello completo alla procedura seguente:

1. Se si dispone già di un toohello di connessione remota VM MyWebServer aprire, rendere toohello una connessione remota VM completando i passaggi hello hello [Connetti toohello server web VM hello Internet](#connect-from-internet) sezione di questo articolo.
2. Fare clic sul pulsante Start hello nell'angolo inferiore sinistro di hello del desktop di Windows hello, quindi iniziare a digitare *desktop remoto*. Quando viene visualizzato elenco a menu Start hello **connessione Desktop remoto**, farvi clic sopra.
3. In hello **connessione Desktop remoto** finestra di dialogo immettere *MyDBServer* per nome computer hello e fare clic su **Connetti**.
4. Immettere nome utente hello e la password immessa nel passaggio 3 di hello [VM del server di database crea hello](#create-database-server-vm) sezione di questo articolo, quindi fare clic su **OK**.
5. Se si riceve una casella di finestra di dialogo che informa è l'identità del computer remoto hello hello non può essere verificato, fare clic su **Sì**.
6. Lasciare la connessione di desktop remoto di hello server tooboth hello toocomplete aprire i passaggi nella sezione successiva hello.

Si è in grado di toomake hello connessione toohello database server VM da hello web VM per hello seguenti motivi:

- Le connessioni in entrata TCP/3389 sono abilitate per qualsiasi indirizzo IP di origine predefinita hello gruppo creato nel passaggio 5 di hello [VM del server di database crea hello](#create-database-server-vm) sezione di questo articolo.
- Si è iniziata la connessione di hello dal server web hello VM, che è connesso toohello stessa rete virtuale come macchina virtuale del server database hello. tooconnect tooa macchina virtuale che non dispone di un tooit di indirizzo IP pubblico, è necessario connettersi da un'altra macchina virtuale connessa toohello stessa rete virtuale, anche se hello macchina virtuale è connessa tooa diverse subnet.
- Anche se le macchine virtuali hello toodifferent connesso subnet, Azure crea route predefinite che consentono la connettività tra subnet. È possibile eseguire l'override di route predefinite hello creando un proprio tuttavia. Hello lettura [le route definite dall'utente](virtual-networks-udr-overview.md) toolearn articolo informazioni sul routing in Azure.

Se si tenta di tooinitiate un server di database di toohello di connessione remota VM da hello Internet, come in hello [Connetti toohello server web VM hello Internet](#connect-from-internet) sezione di questo articolo, vedrai che hello **Connect** opzione è disattivata. La connessione non è disponibile perché non esiste alcun toohello di indirizzo assegnato IP pubblico VM, tooit le connessioni in ingresso da Internet hello non sono possibili.

### <a name="connect-toohello-internet-from-hello-database-server-vm"></a>Connettersi a Internet toohello dal server di database hello VM

Connessione in uscita toohello Internet dal server di database hello VM completando hello alla procedura seguente:

1. Se si dispone già di un toohello di connessione remota VM MyDBServer aprire dalla VM MyWebServer hello, hello completato i passaggi in hello [connessione server di database toohello macchina virtuale dalla macchina virtuale del server web hello](#webserver-to-dbserver) sezione di questo articolo.
2. Dal desktop di Windows hello in hello MyDBServer VM, aprire Internet Explorer e rispondere a finestre di dialogo toohello seguendo i passaggi 2 e 3 di hello [connettersi toohello Internet dalla macchina virtuale del server web hello](#connect-to-internet) sezione di questo articolo.
3. Nella barra degli indirizzi hello immettere [bing.com](http:www.bing.com).
4. Fare clic su **Aggiungi** in hello Internet Explorer finestra di dialogo visualizzata, quindi **Aggiungi**, quindi **Chiudi** in hello **attendibili** la finestra di dialogo di siti. Seguire questa procedura nelle altre finestre di dialogo eventualmente visualizzate.
5. Pagina di ricerca in Bing hello, immettere *whatsmyipaddress*, quindi fare clic su pulsante di ingrandimento hello. Bing restituisce hello pubblica IP indirizzo attualmente assegnato toohello VM hello dell'infrastruttura di Azure. 6. Chiudere hello remote desktop toohello MyDBServer VM da hello MyWebServer VM, quindi chiudere toohello di connessione remota hello MyWebServer VM.

connessione in uscita di Hello toohello Internet è consentita perché tutto il traffico in uscita è consentito per impostazione predefinita, anche se non è una risorsa di indirizzo IP pubblica assegnata toohello MyDBServer VM. Tutte le macchine virtuali, per impostazione predefinita, sono in grado di tooconnect in uscita toohello Internet, con o senza un toohello di risorse assegnata indirizzo VM IP pubblico. Non sono in grado di tooconnect toohello pubblica di indirizzi IP da Internet hello, tuttavia, come è stato in grado di toofor hello MyWebServer VM con un indirizzo IP pubblico risorse assegnato.

## <a name="delete-resources"></a>Eliminare tutte le risorse

toodelete tutte le risorse create in questo articolo, hello completo alla procedura seguente:

1. tooview gruppo di risorse MyRG hello creato in questo articolo completo i passaggi da 1 a 3 in hello [risorse](#review) sezione di questo articolo. Ancora una volta, esaminare le risorse di hello nel gruppo di risorse hello. Se si crea gruppo di risorse MyRG hello, per i passaggi precedenti, è visualizzato 12 risorse hello mostrate nell'immagine di hello nel passaggio 4.
2. Nel pannello MyRG hello, fare clic su hello **eliminare** pulsante.
3. Hello portale richiede nome hello tootype di hello tooconfirm di gruppo di risorse che si desidera toodelete è. Se viene visualizzato risorse diverso da risorse hello indicate nel passaggio 4 di hello [risorse](#review) sezione di questo articolo, fare clic su **Annulla**. Se viene visualizzato solo le risorse hello 12 create come parte di questo articolo, digitare *MyRG* per nome gruppo di risorse hello, quindi fare clic su **eliminare**. Elimina un gruppo di risorse, tutte le risorse nel gruppo di risorse hello, pertanto sempre certi tooconfirm contenuto hello di un gruppo di risorse prima di eliminarlo. portale Hello Elimina tutte le risorse contenute nel gruppo di risorse hello, quindi Elimina gruppo di risorse hello stesso. Questo processo richiede alcuni minuti.

## <a name="next-steps"></a>Passaggi successivi

In questo esercizio sono state create una rete virtuale e due VM. Durante la creazione delle VM sono state specificate alcune impostazioni personalizzate e sono state accettate diverse impostazioni predefinite. È consigliabile leggere hello seguenti articoli, prima della distribuzione di produzione, le reti virtuali e macchine virtuali, tooensure è comprendere tutte le impostazioni disponibili:

- [Reti virtuali](virtual-networks-overview.md)
- [Indirizzi IP pubblici](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)
- [Interfacce di rete](virtual-network-network-interface.md)
- [Gruppi di sicurezza di rete](virtual-networks-nsg.md)
- [Macchine virtuali](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
