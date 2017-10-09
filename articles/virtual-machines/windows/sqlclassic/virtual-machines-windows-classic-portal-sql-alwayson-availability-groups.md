---
title: "aaaConfigure sempre nel gruppo di disponibilità in macchine virtuali di Azure (versione classica) | Documenti Microsoft"
description: "Creare un gruppo di disponibilità AlwaysOn con le macchine virtuali di Azure. Questa esercitazione viene utilizzato principalmente interfaccia utente di hello e strumenti anziché di scripting."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 8d48a3d2-79f8-4ab0-9327-2f30ee0b2ff1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: f428ad994a55378c281c959f4696fdcaf50632b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-virtual-machines-classic"></a>Configurare un gruppo di disponibilità AlwaysOn in macchine virtuali di Azure (distribuzione classica)
> [!div class="op_single_selector"]
> * [Classica: interfaccia utente](../classic/portal-sql-alwayson-availability-groups.md)
> * [Classica: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Prima di iniziare, considerare che ora è possibile completare questa attività nel modello Azure Resource Manager. Per le nuove distribuzioni è consigliabile usare il modello Azure Resource Manager. Vedere [gruppi di disponibilità Always On di SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT] 
> Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Azure offre due toocreate di modelli di distribuzione diversi e utilizzare le risorse: [Resource Manager e classica](../../../azure-resource-manager/resource-manager-deployment-model.md). Questo articolo spiega come toouse hello modello di distribuzione classica. 

vedere questa attività con il modello di gestione risorse di Azure hello toocomplete [SQL Server Always On gruppi di disponibilità in macchine virtuali di Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

In questa esercitazione end-to-end viene illustrato come i gruppi disponibilità tooimplement utilizzando SQL Server Always On nelle macchine virtuali di Azure.

Al fine di hello dell'esercitazione hello, la soluzione SQL Server Always On in Azure sarà composta dagli hello seguenti elementi:

* Una rete virtuale contenente più subnet, tra cui una subnet front-end e una back-end
* Un controller di dominio con un dominio di Active Directory (Azure AD)
* Due macchine virtuali che eseguono SQL Server e sono subnet back-end toohello distribuito e dominio toohello unita in join Azure AD
* Un cluster di failover di tre nodi con modello di quorum maggioranza dei nodi hello
* Un gruppo di disponibilità che ha due repliche di commit sincrono di un database di disponibilità

Hello nella figura seguente è una rappresentazione grafica della soluzione hello.

![Architettura di lab di test per gruppi di disponibilità in Azure](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC791912.png)

Si tratta di una possibile configurazione. Ad esempio, è possibile ridurre il numero di hello di macchine virtuali per un gruppo di disponibilità con due repliche. Questa configurazione vengono salvate in ore di calcolo in Azure utilizzando controller di dominio hello come hello quorum condivisione file di controllo in un cluster a due nodi. Questo metodo riduce il numero di macchine virtuali di hello uno dalla configurazione hello illustrato.

Questa esercitazione si presuppone l'esempio hello:

* Si dispone già di un account Azure.
* Si conosce già la modalità toouse hello GUI in hello macchina virtuale raccolta tooprovision una classica macchina virtuale che esegue SQL Server.
* Si dispone già una conoscenza approfondita dei gruppi di disponibilità AlwaysOn. Per altre informazioni, vedere [Gruppi di disponibilità AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Se si è interessati all'uso di gruppi di disponibilità AlwaysOn con SharePoint, vedere anche [Configurare gruppi di disponibilità AlwaysOn di SQL Server 2012 per SharePoint 2013](https://technet.microsoft.com/library/jj715261.aspx).
> 
> 

## <a name="create-hello-virtual-network-and-domain-controller-server"></a>Creare la rete virtuale di hello e server del controller di dominio
Si inizia con un nuovo account di prova di Azure. Dopo aver configurato l'account, è necessario nella schermata iniziale di hello di hello portale di Azure classico.

1. Fare clic su hello **New** hello nell'angolo sinistro della parte inferiore di hello della pagina hello, come illustrato nella seguente schermata hello in.
   
    ![Fare clic su nuovo nel portale di hello](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665511.gif)
2. Fare clic su **servizi di rete** > **rete virtuale** > **creazione personalizzata**, come illustrato nella seguente schermata hello.
   
    ![Crea rete virtuale](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665512.gif)
3. In hello **crea rete virtuale** finestra di dialogo casella, creare una nuova rete virtuale avanzando pagine hello e utilizzando le impostazioni di hello in hello nella tabella seguente. 
   
   | Page | Impostazioni |
   | --- | --- |
   | Dettagli della rete virtuale |**NOME = ContosoNET**<br/>**AREA = Stati Uniti occidentali** |
   | Server DNS e connettività VPN |Nessuno |
   | Spazi di indirizzi della rete virtuale |Impostazioni sono illustrate nella seguente schermata hello: ![Crea rete virtuale](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784620.png) |
4. Creare una macchina virtuale hello che verrà utilizzato come controller di dominio hello (DC). Fare clic su **New** > **calcolo** > **macchina virtuale** > **dalla raccolta**, come illustrato Hello seguente schermata.
   
    ![Creare una macchina virtuale](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784621.png)
5. In hello **crea macchina virtuale** finestra di dialogo casella, configurare una nuova macchina virtuale avanzando pagine hello e utilizzando le impostazioni di hello in hello nella tabella seguente. 
   
   | Page | Impostazioni |
   | --- | --- |
   | Sistema operativo della macchina virtuale selezionare hello |Windows Server 2012 R2 Datacenter |
   | Configurazione macchina virtuale |**DATA DI RILASCIO VERSIONE** = (più recente)<br/>**NOME MACCHINA VIRTUALE** = ContosoDC<br/>**PIANO** = STANDARD<br/>**DIMENSIONI** = A2 (2 core)<br/>**NUOVO NOME UTENTE** = AzureAdmin<br/>**NUOVA PASSWORD** = Contoso!000<br/>**CONFERMA** = Contoso!000 |
   | Configurazione macchina virtuale |**SERVIZIO CLOUD** = creare un nuovo servizio cloud<br/>**NOME DNS DEL SERVIZIO CLOUD** = nome univoco del servizio cloud<br/>**NOME DNS** = nome univoco (ad esempio: ContosoDC123)<br/>**AREA/GRUPPO DI AFFINITÀ/RETE VIRTUALE** = ContosoNET<br/>**SUNET RETE VIRTUALE** = Back(10.10.2.0/24)<br/>**ACCOUNT DI ARCHIVIAZIONE**: usare un account di archiviazione generato automaticamente<br/>**SET DI DISPONIBILITÀ** = (Nessuno) |
   | Opzioni macchina virtuale |Valori predefiniti |

Dopo aver configurato hello nuova macchina virtuale, attendere l'esecuzione del relativo provisioning toobe hello macchina virtuale. Questo processo richiede alcune toofinish ora. Se si fa clic hello **macchina virtuale** scheda hello Azure classico portale, è possibile visualizzare gli stati da ciclista ContosoDC da **avvio in corso (Provisioning)** troppo**arrestato**, **Avvio**, **in esecuzione (Provisioning)**e infine **esecuzione**.

provisioning del server del controller di dominio Hello ora correttamente. Successivamente, si configurerà il dominio di Active Directory hello in questo server di controller di dominio.

## <a name="configure-hello-domain-controller"></a>Configurare il controller di dominio hello
In operazioni di hello, configurare macchina virtuale ContosoDC hello come controller di dominio per corp.contoso.com.

1. Nel portale di hello selezionare hello **ContosoDC** macchina. In hello **Dashboard** scheda, fare clic su **Connetti** tooopen file desktop remoto (RDP) per l'accesso desktop remoto.
   
    ![Connettersi tooVritual macchina](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784622.png)
2. Accedere con l'account amministratore (**\AzureAdmin**) e la password (**Contoso!000**) configurati.
3. Per impostazione predefinita, hello **Server Manager** dashboard deve essere visualizzato.
4. Fare clic su hello **Aggiungi ruoli e funzionalità** collegamento nel dashboard di hello.
   
    ![Aggiunta ruoli Esplora server](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784623.png)
5. Fare clic su **Avanti** fino a ottenere toohello **i ruoli del Server** sezione.
6. Seleziona hello **servizi di dominio Active Directory** e **Server DNS** ruoli. Quando richiesto, aggiungere altre funzionalità richieste da questi ruoli.
   
   > [!NOTE]
   > Verrà visualizzato un avviso di convalida che indica che non esiste alcun indirizzo IP statico. Se si sta testando configurazione hello, fare clic su **continua**. Per gli scenari di produzione [utilizzare PowerShell tooset hello indirizzo IP statico del computer controller di dominio hello](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   > 
   > 
   
    ![Finestra di dialogo Aggiungi ruoli](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784624.png)
7. Fare clic su **Avanti** fino a raggiungere hello **conferma** sezione. Seleziona hello **riavvio del server di destinazione hello automaticamente se necessario** casella di controllo.
8. Fare clic su **Installa**.
9. Dopo l'installazione delle funzionalità di hello, tornare toohello **Server Manager** dashboard.
10. Seleziona hello nuovo **AD DS** opzione hello riquadro a sinistra.
11. Fare clic su hello **più** collegamento sulla barra di avviso gialla hello.
    
     ![Finestra di dialogo Servizi di dominio di Active Directory nella macchina virtuale del server DNS](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784625.png)
12. In hello **azione** colonna di hello **tutti i Server-dettagli attività** la finestra di dialogo, fare clic su **alzare di livello questo controller di dominio server tooa**.
13. In hello **guidata configurazione di servizi di dominio di Active Directory**, utilizzare hello seguenti valori:
    
    | Page | Impostazione |
    | --- | --- |
    | Configurazione distribuzione |**Aggiungi una nuova foresta** = selezionata<br/>**Nome di dominio radice** = corp.contoso.com |
    | Opzioni controller di dominio |**Password** = Contoso!000<br/>**Conferma password** = Contoso!000 |
14. Fare clic su **Avanti** toogo tramite hello altre pagine della procedura guidata hello. In hello **controllo dei prerequisiti** pagina, verificare che venga visualizzato hello seguente messaggio: **tutti i controlli dei prerequisiti sono riusciti**. Si noti che è consigliabile esaminare tutti i messaggi di avviso applicabile, ma è possibile toocontinue con installazione hello.
15. Fare clic su **Installa**. Hello **ContosoDC** macchina virtuale verrà riavviato automaticamente.

## <a name="configure-domain-accounts"></a>Configurare gli account di dominio
passaggi successivi Hello configurare gli account di Active Directory hello per un uso successivo.

1. Eseguire nuovamente l'accesso toohello **ContosoDC** macchina.
2. In **Server Manager** fare clic su **Strumenti** > **Centro di amministrazione di Active Directory**.
   
    ![Centro di amministrazione di Active Directory](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784626.png)
3. In hello **il centro di amministrazione di Active Directory**selezionare **corp (locale)** nel riquadro di sinistra hello.
4. In hello destra **attività** riquadro, fare clic su **New** > **utente**. Utilizzare hello seguenti impostazioni:
   
   | Impostazione | Valore |
   | --- | --- |
   | **Nome** |Installa |
   | **Utente SamAccountName** |Installa |
   | **Password** |Contoso!000 |
   | **Conferma password** |Contoso!000 |
   | **Altre opzioni password** |Selezionato |
   | **Nessuna scadenza password** |Selezionato |
5. Fare clic su **OK** toocreate hello **installare** utente. Questo account sarà utilizzato tooconfigure hello failover cluster e hello gruppo di disponibilità.
6. Creare due utenti aggiuntivi, **CORP\SQLSvc1** e **CORP\SQLSvc2**, con hello stessi passaggi. Questi account verranno usati per le istanze di SQL Server hello. Successivamente, è necessario toogive **CORP\Install** hello delle autorizzazioni necessarie tooconfigure Windows del clustering di failover.
7. In hello **il centro di amministrazione di Active Directory**, fare clic su **corp (locale)** nel riquadro di sinistra hello. In hello **attività** riquadro, fare clic su **proprietà**.
   
    ![Proprietà utente CORP](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784627.png)
8. Selezionare **estensioni**, quindi fare clic su hello **avanzate** pulsante hello **sicurezza** scheda.
9. In hello **impostazioni di sicurezza avanzate per corp** la finestra di dialogo, fare clic su **Aggiungi**.
10. Fare clic su **Seleziona un'entità**, cercare **CORP\Install** e quindi fare clic su **OK**.
11. Seleziona hello **Leggi tutte le proprietà** e **crea oggetti Computer** autorizzazioni.
    
     ![Autorizzazioni utente Corp](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784628.png)
12. Fare clic su **OK** e quindi di nuovo clic su **OK**. Finestra proprietà di corp hello Chiudi.

Ora che è configurato Active Directory e gli oggetti utente hello, si crea tre macchine virtuali di SQL Server e aggiungerle toothis dominio.

## <a name="create-hello-sql-server-virtual-machines"></a>Creare hello macchine virtuali di SQL Server
Creare tre macchine virtuali, una per un nodo del cluster e due per SQL Server. toocreate delle macchine virtuali di hello, Vai indietro toohello portale di Azure classico, fare clic su **New** > **calcolo** > **macchina virtuale**  >  **Dalla raccolta**. Quindi, è possibile utilizzare modelli di hello nella seguente tabella toohelp si creano macchine virtuali hello hello.

| Page | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Sistema operativo della macchina virtuale selezionare hello |**Windows Server 2012 R2 Datacenter** |**SQL Server 2014 RTM Enterprise** |**SQL Server 2014 RTM Enterprise** |
| Configurazione macchina virtuale |**DATA DI RILASCIO VERSIONE** = (più recente)<br/>**NOME MACCHINA VIRTUALE** = ContosoWSFCNode<br/>**PIANO** = STANDARD<br/>**DIMENSIONI** = A2 (2 core)<br/>**NUOVO NOME UTENTE** = AzureAdmin<br/>**NUOVA PASSWORD** = Contoso!000<br/>**CONFERMA** = Contoso!000 |**DATA DI RILASCIO VERSIONE** = (più recente)<br/>**NOME MACCHINA VIRTUALE** = ContosoSQL1<br/>**PIANO** = STANDARD<br/>**DIMENSIONI** = A3 (4 core)<br/>**NUOVO NOME UTENTE** = AzureAdmin<br/>**NUOVA PASSWORD** = Contoso!000<br/>**CONFERMA** = Contoso!000 |**DATA DI RILASCIO VERSIONE** = (più recente)<br/>**NOME MACCHINA VIRTUALE** = ContosoSQL2<br/>**PIANO** = STANDARD<br/>**DIMENSIONI** = A3 (4 core)<br/>**NUOVO NOME UTENTE** = AzureAdmin<br/>**NUOVA PASSWORD** = Contoso!000<br/>**CONFERMA** = Contoso!000 |
| Configurazione macchina virtuale |**SERVIZIO CLOUD** = nome DNS univoco del servizio cloud creato in precedenza (ad esempio: ContosoDC123)<br/>**AREA/GRUPPO DI AFFINITÀ/RETE VIRTUALE** = ContosoNET<br/>**SUNET RETE VIRTUALE** = Back(10.10.2.0/24)<br/>**ACCOUNT DI ARCHIVIAZIONE**: usare un account di archiviazione generato automaticamente<br/>**SETDI DISPONIBILITÀ** = creare un set di disponibilità<br/>**NOME SET DI DISPONIBILITÀ** = SQLHADR |**SERVIZIO CLOUD** = nome DNS univoco del servizio cloud creato in precedenza (ad esempio: ContosoDC123)<br/>**AREA/GRUPPO DI AFFINITÀ/RETE VIRTUALE** = ContosoNET<br/>**SUNET RETE VIRTUALE** = Back(10.10.2.0/24)<br/>**ACCOUNT DI ARCHIVIAZIONE**: usare un account di archiviazione generato automaticamente<br/>**SET di disponibilità** = SQLHADR (è possibile configurare anche hello set di disponibilità dopo hello macchina è stata creata. Tutti e tre i computer devono essere assegnati toohello set di disponibilità SQLHADR.) |**SERVIZIO CLOUD** = nome DNS univoco del servizio cloud creato in precedenza (ad esempio: ContosoDC123)<br/>**AREA/GRUPPO DI AFFINITÀ/RETE VIRTUALE** = ContosoNET<br/>**SUNET RETE VIRTUALE** = Back(10.10.2.0/24)<br/>**ACCOUNT DI ARCHIVIAZIONE**: usare un account di archiviazione generato automaticamente<br/>**SET di disponibilità** = SQLHADR (è possibile configurare anche hello set di disponibilità dopo hello macchina è stata creata. Tutti e tre i computer devono essere assegnati toohello set di disponibilità SQLHADR.) |
| Opzioni macchina virtuale |Valori predefiniti |Valori predefiniti |Valori predefiniti |

<br/>

> [!NOTE]
> la configurazione precedente Hello suggerisce macchine virtuali di livello STANDARD, poiché il computer di livello BASIC non supportano endpoint con bilanciamento del carico. È necessario endpoint con carico bilanciato toocreate successive un listener del gruppo di disponibilità. Inoltre, le dimensioni delle macchine hello che qui suggerite sono concepite per il testing di gruppi di disponibilità in macchine virtuali di Azure. Per prestazioni ottimali di hello sui carichi di lavoro di produzione, visualizzare le raccomandazioni hello per le dimensioni della macchina SQL Server e la configurazione in [prestazioni ottimali per SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-performance.md).
> 
> 

Al termine hello e tre le macchine virtuali sono provisioning, è necessario toojoin li toohello **corp.contoso.com** dominio e concedere le macchine toohello CORP\Install diritti amministrativi. toodo hello, questo uso seguendo i passaggi per ognuna delle macchine virtuali hello tre.

1. Modificare in primo luogo, l'indirizzo del server DNS preferito hello. Scaricare una directory locale di ogni macchina virtuale RDP file tooyour selezionando macchina virtuale hello hello elenco e facendo clic su hello **Connetti** pulsante. tooselect una macchina virtuale, fare clic in un punto qualsiasi ma hello prima cella hello riga, come illustrato nella seguente schermata hello.
   
    ![Scaricare il file RDP hello](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664953.jpg)
2. Aprire hello RDP file scaricato e accedere utilizzando l'account amministratore configurato macchina virtuale toohello (**BUILTIN\AzureAdmin**) e la password (**Contoso! 000**).
3. Dopo l'accesso, dovrebbe essere hello **Server Manager** dashboard. Fare clic su **Server locale** nel riquadro di sinistra hello.
4. Fare clic su hello **indirizzo IPv4 assegnato da DHCP, compatibile IPv6** collegamento.
5. In hello **connessioni di rete** finestra di dialogo fare clic sull'icona di rete hello.
   
    ![Server DNS di macchina virtuale preferito hello modifica](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784629.png)
6. Nella barra dei comandi di hello, fare clic su **modificare le impostazioni di hello di questa connessione**. (A seconda delle dimensioni di hello della finestra, potrebbe essere tooclick hello doppia freccia a destra toosee questo comando).
7. Selezionare **Protocollo Internet versione 4 (TCP/IPv4)** e quindi fare clic su **Proprietà**.
8. Selezionare **hello utilizzare seguenti indirizzi server DNS** e quindi specificare **10.10.2.4** in **server DNS preferito**.
9. Hello **10.10.2.4** indirizzo è hello che è assegnato tooa di macchina virtuale nella subnet 10.10.2.0/24 hello in una rete virtuale di Azure. e la macchina virtuale è **ContosoDC**. tooverify **ContosoDC**dell'indirizzo IP, utilizzare **nslookup contosodc** nella finestra del prompt dei comandi hello, come illustrato nella seguente schermata hello.
   
    ![Utilizzare l'indirizzo IP toofind NSLOOKUP per controller di dominio](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664954.jpg)
10. Fare clic su **OK** > **Chiudi** modifiche hello toocommit. È ora possibile aggiungere macchina virtuale hello troppo**corp.contoso.com**.
11. In hello **Server locale** finestra, fare clic su hello **WORKGROUP** collegamento.
12. In hello **nome Computer** fare clic su **modifica**.
13. Seleziona hello **dominio** nella casella di controllo **corp.contoso.com** in hello casella di testo e quindi fare clic su **OK**.
14. In hello **la sicurezza di Windows** finestra di dialogo specificare le credenziali di hello per account di amministratore di dominio predefinito hello (**CORP\AzureAdmin**) e la password di hello (**Contoso! 000**).
15. Quando viene visualizzato il messaggio "dominio corp.contoso.com toohello iniziale" hello, fare clic su **OK**.
16. Fare clic su **Chiudi** > **Riavvia ora** nella finestra di dialogo hello.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-virtual-machine"></a>Aggiungi utente Corp\Install hello come amministratore in ogni macchina virtuale
1. Attendere il riavvio della macchina virtuale hello e quindi aprire hello RDP file nuovamente toosign nella macchina virtuale toohello tramite hello **BUILTIN\AzureAdmin** account.
2. In **Server Manager** fare clic su **Strumenti** > **Gestione computer**.
   
    ![Gestione computer](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784630.png)
3. In hello **Gestione Computer** finestra di dialogo espandere **utenti e gruppi locali**, quindi fare clic su **gruppi**.
4. Fare doppio clic su hello **amministratori** gruppo.
5. In hello **proprietà amministratori** finestra di dialogo fare clic su hello **Aggiungi** pulsante.
6. Immettere nome utente hello **CORP\Install**, quindi fare clic su **OK**. Quando vengono richieste le credenziali, utilizzare hello **AzureAdmin** account con hello **Contoso! 000** password.
7. Fare clic su **OK** tooclose hello **proprietà amministratore** la finestra di dialogo.

### <a name="add-hello-failover-clustering-feature-tooeach-virtual-machine"></a>Aggiungere il Clustering di Failover hello macchina virtuale tooeach con funzionalità
1. In hello **Server Manager** dashboard, fare clic su **Aggiungi ruoli e funzionalità**.
2. In hello **Aggiunta guidata ruoli e funzionalità**, fare clic su **Avanti** fino a ottenere toohello **funzionalità** pagina.
3. Selezionare **Clustering di failover**. Quando richiesto, aggiungere altre funzionalità dipendenti.
   
    ![Aggiungere funzionalità di Clustering di Failover toovirtual macchina](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784631.png)
4. Fare clic su **Avanti**, quindi fare clic su **installare** su hello **conferma** pagina.
5. Quando hello **Clustering di Failover** completato l'installazione di funzionalità, fare clic su **Chiudi**.
6. Disconnettersi da macchina virtuale hello.
7. Ripetere i passaggi in questa sezione per tutti e tre i server hello: **ContosoWSFCNode**, **ContosoSQL1**, e **ContosoSQL2**.

Hello ora provisioning delle macchine virtuali di SQL Server e in esecuzione, ma ciascuno con le opzioni predefinite di hello per SQL Server.

## <a name="create-hello-failover-cluster"></a>Creare il cluster di failover di hello
In questa sezione, creare i cluster di failover hello che ospiterà il gruppo di disponibilità hello che verrà creato in un secondo momento. A questo punto, si sono state eseguite hello tooeach delle macchine virtuali hello tre che verrà utilizzato in cluster di failover hello seguenti:

* Hello completo di macchina virtuale in Azure
* È stato aggiunto hello macchina virtuale toohello dominio
* Aggiunto **CORP\Install** toohello gruppo di amministratori locali
* Funzionalità di clustering di failover aggiunto hello

Tutte queste operazioni sono prerequisiti in ogni macchina virtuale prima poter creare un join toohello cluster di failover.

Inoltre, si noti che hello rete virtuale di Azure non si comportano in hello stesso come una rete locale. È necessario cluster hello toocreate in hello seguente ordine:

1. Creare un cluster a nodo singolo in uno dei nodi (**ContosoSQL1**).
2. Modificare tooan indirizzo IP del cluster di hello indirizzo IP inutilizzato (**10.10.2.101**).
3. Portare online nome del cluster hello.
4. Aggiungere altri nodi hello (**ContosoSQL2** e **ContosoWSFCNode**).

Utilizzare i seguenti passaggi toocomplete hello attività che consentono di configurare completamente il cluster hello hello.

1. Il file RDP hello Open per **ContosoSQL1**e accedere utilizzando account di dominio hello **CORP\Install**.
2. In hello **Server Manager** dashboard, fare clic su **strumenti** > **gestione Cluster di Failover**.
3. Nel riquadro di sinistra hello, fare doppio clic su **gestione Cluster di Failover**, quindi fare clic su **creare un Cluster**, come illustrato nella seguente schermata hello.
   
    ![Creare cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784632.png)
4. In hello Creazione guidata Cluster, creare un cluster a un nodo avanzando pagine hello e utilizzando le impostazioni di hello in hello nella tabella seguente:
   
   | Page | Impostazioni |
   | --- | --- |
   | Prima di iniziare |Valori predefiniti |
   | Selezione dei server |Digitare **ContosoSQL1** in **Immettere il nome del server** e fare clic su **Aggiungi** |
   | Avviso di convalida |Selezionare **Nr I non è necessario supporto da Microsoft per questo cluster e pertanto non si desidera che la convalida di hello toorun test. Quando fa clic su Avanti, continuare con la creazione di cluster hello**. |
   | Punto di accesso per hello amministrazione Cluster |Digitare **Cluster1** in **Nome cluster** |
   | Conferma |Usare le impostazioni predefinite a meno a meno che non si usino spazi di archiviazione. Vedere l'avviso hello segue questa tabella. |
   
   > [!WARNING]
   > Se si utilizza [spazi di archiviazione](https://technet.microsoft.com/library/hh831739), che raggruppa più dischi nel pool di archiviazione, è necessario deselezionare hello **aggiungere tutte le risorse di archiviazione idonee toohello cluster** casella di controllo hello **conferma** pagina. Se non si deseleziona questa opzione, i dischi virtuali hello verranno disconnesso durante il processo di clustering hello. Di conseguenza, verranno inoltre non visualizzati in Gestione disco o Esplora fino a quando gli spazi di archiviazione hello vengono rimossi dal cluster hello e ricollegati tramite PowerShell.
   > 
   > 
5. Nel riquadro sinistro hello espandere **gestione Cluster di Failover**, quindi fare clic su **Cluster1.corp.contoso.com**.
6. Nel riquadro centrale di hello, scorrere verso il basso toohello **risorse principali del Cluster** sezione ed espandere hello **nome: Clutser1** dettagli. Dovrebbe essere entrambi hello **nome** hello e **indirizzo IP** risorse hello **Failed** stato. Hello risorsa indirizzo IP non può essere portata online perché il cluster hello è assegnato hello nello stesso indirizzo IP computer hello stesso, ovvero un indirizzo duplicato.
7. Hello pulsante destro del mouse non è stato possibile **indirizzo IP** risorsa e quindi fare clic su **proprietà**.
   
    ![Proprietà del cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784633.png)
8. Selezionare **indirizzo IP statico**, specificare **10.10.2.101** in hello **indirizzo** casella di testo e quindi fare clic su **OK**.
9. In hello **risorse principali del Cluster** sezione destro del mouse su **nome: Cluster1**, quindi fare clic su **in linea**. Attendere finché entrambe le risorse non siano online. Quando risorsa del nome cluster hello torna online, il server di controller di dominio hello viene aggiornato con un nuovo account computer di Active Directory. Verrà utilizzato l'account di Active Directory toorun hello del gruppo di disponibilità del servizio cluster in un secondo momento.
10. Aggiungere hello cluster toohello nodi rimanenti. Nella struttura di browser hello, fare doppio clic su **Cluster1.corp.contoso.com**, quindi fare clic su **aggiunta del nodo**, come illustrato nella seguente schermata hello.
    
     ![Aggiungi nodo toohello cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784634.png)
11. In hello **Aggiunta guidata nodi**, fare clic su **Avanti** su hello **selezione dei server** pagina, aggiungere **ContosoSQL2** e **ContosoWSFCNode**  toohello elenco digitando il nome server hello in **immettere il nome del server** e quindi fare clic su **Aggiungi**. Al termine dell'operazione, scegliere **Avanti**.
12. In hello **avviso di convalida** pagina, fare clic su **n**, anche se in uno scenario di produzione, è necessario eseguire il test di convalida hello. Quindi fare clic su **Next**.
13. In hello **conferma** pagina, fare clic su **Avanti** nodi hello tooadd.
    
    > [!WARNING]
    > Se si utilizza [spazi di archiviazione](https://technet.microsoft.com/library/hh831739), che raggruppa più dischi nel pool di archiviazione, è necessario deselezionare hello **aggiungere tutte le risorse di archiviazione idonee toohello cluster** casella di controllo. Se non si deseleziona questa opzione, i dischi virtuali hello verranno disconnesso durante il processo di clustering hello. Di conseguenza, essi non appariranno anche in Gestione disco o Esplora fino a quando non vengono rimossi gli spazi di archiviazione di hello dal cluster e ricollegati tramite PowerShell.
    > 
    > 
14. Una volta aggiungono i nodi di hello toohello cluster, fare clic su **fine**. Gestione Cluster di failover devono ora mostrare che il cluster dispone di tre nodi ed elencarli in hello **nodi** contenitore.
15. Disconnettersi dalla sessione desktop remoto hello.

## <a name="prepare-hello-sql-server-instances-for-availability-groups"></a>Preparare le istanze di SQL Server hello per i gruppi di disponibilità
In questa sezione verranno effettuate hello seguente sia **ContosoSQL1** e **contosoSQL2**:

* Aggiungere un account di accesso per **NT AUTHORITY\System** impostando toohello istanza di SQL Server predefinita delle autorizzazioni necessarie.
* Aggiungere **CORP\Install** come un'istanza di SQL Server sysadmin ruolo toohello predefinito.
* Aprire il firewall hello per l'accesso remoto di SQL Server.
* Abilitare hello Always On funzionalità di gruppi di disponibilità.
* Modificare anche l'account del servizio SQL Server hello**CORP\SQLSvc1** e **CORP\SQLSvc2**, rispettivamente.

Queste azioni possono essere eseguite in qualsiasi ordine. Tuttavia, hello passaggi verrà illustrati in ordine. Ripetere i passaggi di hello per entrambi **ContosoSQL1** e **ContosoSQL2**:

1. Se non è stato firmato dalla sessione desktop remoto di hello per la macchina virtuale hello, farlo ora.
2. I file aperto hello RDP per **ContosoSQL1** e **ContosoSQL2**ed eseguire l'accesso come **BUILTIN\AzureAdmin**.
3. Aggiungere **NT AUTHORITY\System** toohello gli account di accesso SQL Server con le autorizzazioni necessarie. Aprire **SQL Server Management Studio**.
4. Fare clic su **Connetti** istanza di SQL Server tooconnect toohello predefinita.
5. In **Esplora oggetti**, espandere **Sicurezza**, quindi espandere **Account di accesso**.
6. Pulsante destro del mouse hello **NT AUTHORITY\System** account di accesso e quindi fare clic su **proprietà**.
7. In hello **entità a protezione diretta** pagina server locale hello, selezionare **Grant** per hello queste autorizzazioni e quindi fare clic su **OK**.
   
   * Alterare eventuali gruppi di disponibilità
   * Connettersi a SQL
   * Visualizzare lo stato del server
8. Aggiungere **CORP\Install** come un **sysadmin** istanza di SQL Server predefinita toohello ruolo. In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Account di accesso** e quindi scegliere **Nuovo account di accesso**.
9. Digitare **CORP\Install** in **Nome account di accesso**.
10. In hello **i ruoli del Server** selezionare **sysadmin**, quindi fare clic su **OK**. Dopo aver creato l'account di accesso hello, è possibile visualizzarlo espandendo **gli account di accesso** in **Esplora oggetti**.
11. una regola del firewall per SQL Server, su hello toocreate **avviare** schermata aprirlo **Windows Firewall con sicurezza avanzata**.
12. Nel riquadro sinistro hello selezionare **regole connessioni in entrata**. Nel riquadro di destra hello, fare clic su **nuova regola**.
13. In hello **tipo di regola** pagina, fare clic su **programma** > **Avanti**.
14. In hello **programma** selezionare **percorso programma**, tipo **%ProgramFiles%\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn\sqlservr.exe** in hello casella di testo e quindi fare clic su **Avanti**. Se si stanno seguendo le istruzioni ma con SQL Server 2012, la directory di SQL Server hello è **MSSQL11. MSSQLSERVER**.
15. In hello **azione** pagina, mantenere **Consenti connessione hello** selezionata e quindi fare clic su **Avanti**.
16. In hello **profilo** pagina, accettare le impostazioni predefinite di hello e quindi fare clic su **Avanti**.
17. In hello **nome** , specificare un nome di regola, ad esempio **SQL Server (regola di programma)**, in hello **nome** testo e quindi fare clic su **fine**.
18. hello tooenable **gruppi di disponibilità AlwaysOn** hello funzionalità **avviare** schermata aprirlo **Gestione configurazione SQL Server**.
19. Nella struttura di browser hello, fare clic su **servizi di SQL Server**, hello rapida **SQL Server (MSSQLSERVER)** del servizio e quindi fare clic su **proprietà**.
20. Fare clic su hello **disponibilità elevata Always On** , selezionare **abilitare gruppi di disponibilità AlwaysOn**, come illustrato nell'hello seguenti schermata e quindi fare clic su **applica**. Fare clic su **OK** in hello la finestra di dialogo, quindi si chiude hello **proprietà** ancora la finestra di dialogo. Dopo aver modificato l'account del servizio hello verrà riavviato il servizio di SQL Server hello.
    
     ![Abilita gruppi di disponibilità AlwaysOn](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665520.gif)
21. hello toochange account del servizio SQL Server, fare clic su hello **accesso** digitare **CORP\SQLSvc1** (per **ContosoSQL1**) o **CORP\SQLSvc2** ( per **ContosoSQL2**) in **nome Account**, inserire e confermare la password hello e quindi fare clic su **OK**.
22. Nella finestra di dialogo di hello visualizzata, fare clic su **Sì** toorestart hello servizio SQL Server. Dopo il riavvio del servizio SQL Server hello, modifiche apportate in hello **proprietà** la finestra di dialogo vengono applicate.
23. Disconnettersi da macchine virtuali hello.

## <a name="create-hello-availability-group"></a>Creare il gruppo di disponibilità hello
Si è ora pronto tooconfigure un gruppo di disponibilità. Di seguito è riportata una descrizione delle azioni da eseguire:

* Creare un nuovo database (**MyDB1**) in **ContosoSQL1**.
* Eseguire un backup completo e un backup del log delle transazioni del database hello.
* Ripristinare hello completo e backup del log troppo**ContosoSQL2** con hello **NORECOVERY** opzione.
* Creare il gruppo di disponibilità hello (**AG1**) con commit sincrono, il failover automatico e repliche secondarie leggibili.

### <a name="create-hello-mydb1-database-on-contososql1"></a>Creare database MyDB1 hello in ContosoSQL1
1. Se non già effettuata da sessioni di desktop remoto hello per **ContosoSQL1** e **ContosoSQL2**, procedere ora.
2. Il file RDP hello Open per **ContosoSQL1**ed eseguire l'accesso come **CORP\Install**.
3. In **Esplora file** creare in **C:\\** una directory denominata **backup** Si verrà utilizzata questa tooback directory e ripristinare il database.
4. Fare doppio clic su nuova directory hello, scegliere troppo**condividere con**, quindi fare clic su **utenti specifici**, come illustrato nella seguente schermata hello.
   
    ![Creare una cartella di backup](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665521.gif)
5. Aggiungere **CORP\SQLSvc1**e quindi assegnargli hello **lettura/scrittura** autorizzazione. Aggiungere **CORP\SQLSvc2**e quindi assegnargli hello **lettura** autorizzazione, come illustrato nell'hello seguenti schermata e quindi fare clic su **condivisione**. Dopo aver completato il processo di condivisione file hello, fare clic su **eseguita**.
   
    ![Concedere le autorizzazioni per la cartella di backup](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665522.gif)
6. database hello toocreate, da hello **avviare** menu aprirlo **SQL Server Management Studio**e quindi fare clic su **Connetti** istanza di SQL Server tooconnect toohello predefinita.
7. In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Database** e quindi fare clic su **Nuovo database**.
8. In **Nome database** digitare **MyDB1** e quindi fare clic su **OK**.

### <a name="make-a-full-backup-of-mydb1-and-restore-it-on-contososql2"></a>Eseguire un backup completo di MyDB1 e ripristinarlo in ContosoSQL2
1. in un backup completo di hello database toomake **Esplora oggetti**, espandere **database**, fare doppio clic su **MyDB1**, punto troppo**attività**, e quindi fare clic su **backup**.
2. In hello **origine** sezione, mantenere **tipo Backup** impostare troppo**completo**. In hello **destinazione** fare clic su **rimuovere** tooremove hello percorso predefinito file di backup hello.
3. In hello **destinazione** fare clic su **Aggiungi**.
4. In hello **nome File** nella casella di testo  **\\ContosoSQL1\backup\MyDB1.bak**, fare clic su **OK**, quindi fare clic su **OK** nuovamente tooback backup database hello. Al termine dell'operazione di backup hello, fare clic su **OK** nuovamente tooclose hello finestra di dialogo.
5. backup del database di hello, del log toomake una transazione **Esplora oggetti**, espandere **database**, fare doppio clic su **MyDB1**, punto troppo**attività**, quindi fare clic su **backup**.
6. In **Tipo backup** selezionare **Log delle transazioni**. Mantenere hello **destinazione** file percorso set toohello uno specificato in precedenza e quindi fare clic su **OK**. Al termine dell'operazione di backup hello, fare clic su **OK** nuovamente.
7. hello toorestore completo e transazione i backup del log **ContosoSQL2**aprire file hello RDP per **ContosoSQL2**ed eseguire l'accesso come **CORP\Install**. Lasciare hello sessione desktop remoto per **ContosoSQL1** aprire.
8. Da hello **avviare** menu aprirlo **SQL Server Management Studio**, quindi fare clic su **Connetti** istanza di SQL Server predefinita toohello tooconnect.
9. In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Database** e quindi scegliere **Ripristina database**.
10. In hello **origine** selezionare **dispositivo**e fare clic sui puntini di sospensione hello **...** .
11. In **Seleziona dispositivi di backup**, fare clic su **Aggiungi**.
12. In **Percorso file di backup** digitare **\\ContosoSQL1\backup**, fare clic su **Aggiorna**, selezionare **MyDB1.bak**, fare clic su **OK** e quindi fare clic di nuovo su **OK**. Dovrebbe essere hello backup completi e backup del log hello hello **toorestore set di Backup** riquadro.
13. Passare toohello **opzioni** selezionare **RESTORE WITH NORECOVERY** in **Stato ripristino**e quindi fare clic su **OK** database hello toorestore. Dopo aver hello al termine dell'operazione di ripristino, fare clic su **OK**.

### <a name="create-hello-availability-group"></a>Creare il gruppo di disponibilità hello
1. Passare nuovamente toohello sessione desktop remoto per **ContosoSQL1**. In **Esplora oggetti** in SQL Server Management Studio, fare doppio clic su **disponibilità elevata Always On**, quindi fare clic su **Creazione guidata nuovo gruppo di disponibilità**, come illustrato nell'hello cattura di schermata seguente.
   
    ![Avviare la Creazione guidata del nuovo gruppo di disponibilità](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665523.gif)
2. In hello **Introduzione** pagina, fare clic su **Avanti**. In hello **Specifica nome del gruppo di disponibilità** , digitare **AG1** in **nome gruppo di disponibilità**, quindi fare clic su **Avanti** nuovamente.
   
    ![Creazione guidata del nuovo gruppo di disponibilità: specifica del nome del gruppo di disponibilità](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665524.gif)
3. In hello **Seleziona database** selezionare **MyDB1**, quindi fare clic su **Avanti**. database Hello soddisfi i prerequisiti di hello per un gruppo di disponibilità perché non si è effettuato almeno un backup completo sulla replica primaria prevista hello.
   
    ![Creazione guidata del nuovo gruppo di disponibilità: selezione dei database](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665525.gif)
4. in hello **specifica repliche** pagina, fare clic su **Aggiungi Replica**.
   
    ![Creazione guidata del nuovo gruppo di disponibilità: specifica delle repliche](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665526.gif)
5. In hello **connettersi tooServer** della finestra di dialogo tipo **ContosoSQL2** in **nome del Server**, quindi fare clic su **Connetti**.
   
    ![Creazione guidata nuovo gruppo di disponibilità, Connetti tooserver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665527.gif)
6. In hello **specifica repliche** pagina, dovrebbe essere **ContosoSQL2** elencati in **repliche disponibili**. Configurare le repliche di hello, come illustrato nella seguente schermata hello. Al termine dell'operazione, scegliere **Avanti**.
   
    ![Creazione guidata del nuovo gruppo di disponibilità: specifica delle repliche (completata)](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665528.gif)
7. In hello **seleziona sincronizzazione dati iniziale** selezionare **solo Join**, quindi fare clic su **Avanti**. È già stata eseguita la sincronizzazione dei dati manualmente quando reso backup completo e delle transazioni di hello in **ContosoSQL1** e sono stati ripristinati in **ContosoSQL2**. È possibile scegliere di non tooperform hello operazioni di backup e ripristino del database e selezionare invece **completo** toolet hello Creazione guidata nuovo gruppo di disponibilità di eseguire la sincronizzazione dei dati. Questa opzione, tuttavia, non è consigliata per i database di dimensioni molto grandi presenti in alcune organizzazioni.
   
    ![Creazione guidata del nuovo gruppo di disponibilità: selezione della sincronizzazione dei dati iniziale](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665529.gif)
8. In hello **convalida** pagina, fare clic su **Avanti**. Questa pagina dovrebbe essere simile toohello seguente schermata. Si verifica un avviso per la configurazione del listener hello poiché non è stato configurato un listener del gruppo di disponibilità. È possibile ignorare questo avviso, poiché l'esercitazione non configura alcun listener. listener di hello tooconfigure dopo aver completato questa esercitazione, vedere [configurare un listener di bilanciamento del carico interno per gruppi di disponibilità AlwaysOn in Azure](../classic/ps-sql-int-listener.md).
   
    ![Creazione guidata del nuovo gruppo di disponibilità: convalida](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665530.gif)
9. In hello **riepilogo** pagina, fare clic su **fine**e quindi attendere hello guidata consente di configurare il nuovo gruppo di disponibilità hello. In hello **lo stato di avanzamento** pagina, è possibile fare clic su **ulteriori dettagli** tooview hello dettagliate lo stato di avanzamento. Al termine della procedura guidata hello, controllare hello **risultati** tooverify pagina tale gruppo di disponibilità hello viene creata correttamente, come illustrato nella seguente schermata hello e quindi fare clic su **Chiudi** tooexit hello procedura guidata.
   
    ![Creazione guidata del nuovo gruppo di disponibilità: risultati](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665531.gif)
10. In **Esplora oggetti** espandere **Disponibilità elevata AlwaysOn** e quindi espandere **Gruppi di disponibilità**. Dovrebbe essere hello nuovo gruppo di disponibilità in questo contenitore. Fare clic con il pulsante destro del mouse su **AG1 (Primary)** (AG1 (Primario)) e selezionare **Show Dashboard** (Mostra dashboard).
    
     ![Visualizzare il dashboard del gruppo di disponibilità](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665532.gif)
11. Il **Dashboard Always On** deve esaminare simile toohello uno in hello seguente schermata. È possibile visualizzare le repliche di hello, la modalità di failover di ogni replica e lo stato di sincronizzazione hello hello.
    
     ![Dashboard del gruppo di disponibilità](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665533.gif)
12. Restituire troppo**Server Manager**, fare clic su **strumenti**e quindi aprire **gestione Cluster di Failover**.
13. Espandere **Cluster1.corp.contoso.com**, quindi espandere **Servizi e applicazioni**. Selezionare **ruoli** e prendere nota di tale hello **AG1** ruolo del gruppo di disponibilità è stato creato. Si noti che AG1 non dispone di un indirizzo IP per il database a cui i client possono connettersi toohello gruppo di disponibilità, perché non è stato configurato un listener. È possibile connettersi direttamente toohello nodo primario per le operazioni di lettura / scrittura e il nodo secondario di hello per le query di sola lettura.
    
     ![Gruppo di disponibilità in Gestione cluster di failover](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665534.gif)

> [!WARNING]
> Non tentare toofail sul gruppo di disponibilità hello da hello gestione Cluster di Failover. Tutte le operazioni di failover devono essere eseguite in **Dashboard AlwaysOn** in SQL Server Management Studio. Per ulteriori informazioni, vedere [le restrizioni sull'utilizzo hello gestione Cluster di Failover con gruppi di disponibilità](https://msdn.microsoft.com/library/ff929171.aspx).
> 
> 

## <a name="next-steps"></a>Passaggi successivi
SQL Server AlwaysOn è stato correttamente implementato mediante la creazione di un gruppo di disponibilità in Azure. tooconfigure un listener per questo gruppo di disponibilità, vedere [configurare un listener del bilanciamento del carico interno per gruppi di disponibilità AlwaysOn in Azure](../classic/ps-sql-int-listener.md).

Per altre informazioni sull'uso di SQL Server in Azure, vedere [SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

