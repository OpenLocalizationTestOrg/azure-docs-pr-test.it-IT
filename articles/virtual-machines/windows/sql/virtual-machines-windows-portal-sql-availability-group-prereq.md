---
title: "disponibilità Server aaaSQL gruppi - macchine virtuali di Azure - prerequisiti | Documenti Microsoft"
description: "Questa esercitazione viene illustrato come raggruppare i prerequisiti di hello tooconfigure per la creazione di una disponibilità di SQL Server Always On nelle macchine virtuali di Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: c492db4c-3faa-4645-849f-5a1a663be55a
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: eed0729ead25c7793bb17a04cd7fd996c7dc8c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-prerequisites-for-creating-always-on-availability-groups-on-azure-virtual-machines"></a>Completare hello prerequisiti per la creazione di gruppi di disponibilità Always On su macchine virtuali di Azure

Questa esercitazione viene illustrato come toocomplete hello prerequisiti per la creazione di un [SQL Server Always On gruppo di disponibilità nelle macchine virtuali di Azure (VM)](virtual-machines-windows-portal-sql-availability-group-tutorial.md). Al termine dei prerequisiti di hello, è un controller di dominio, due macchine virtuali di SQL Server e un server di controllo in un singolo gruppo di risorse.

**Tempo stimato**: potrebbe richiedere alcune ore prerequisiti hello toocomplete. Il tempo è dedicato principalmente alla creazione delle macchine virtuali.

Hello diagramma seguente illustra ciò che si compila in esercitazione hello.

![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="review-availability-group-documentation"></a>Esaminare la documentazione relativa ai gruppi di disponibilità

L'esercitazione presuppone una conoscenza di base dei gruppi di disponibilità AlwaysOn di SQL Server. Se non si ha familiarità con questa tecnologia, vedere [Panoramica di gruppi di disponibilità AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).


## <a name="create-an-azure-account"></a>Creare un account Azure
È necessario un account Azure. È possibile [aprire un account Azure gratuito](/pricing/free-trial/?WT.mc_id=A261C142F) o [attivare i benefici della sottoscrizione di Visual Studio](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse
1. Accedi toohello [portale di Azure](http://portal.azure.com).
2. Fare clic su  **+**  toocreate un nuovo oggetto nel portale di hello.

   ![Nuovo oggetto](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-portalplus.png)

3. Tipo **gruppo di risorse** in hello **Marketplace** finestra di ricerca.

   ![Gruppo di risorse](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroupsymbol.png)
4. Fare clic su **Gruppo di risorse**.
5. Fare clic su **Crea**.
6. In hello **gruppo di risorse** pannello, in **nome gruppo di risorse**, digitare un nome per il gruppo di risorse hello. ad esempio digitare **sql-ha-rg**.
7. Se si dispone di più sottoscrizioni di Azure, verificare che la sottoscrizione hello hello sottoscrizione di Azure che si desidera il gruppo di disponibilità toocreate hello in.
8. Selezionare una località. percorso Hello è hello Azure area in cui il gruppo di disponibilità toocreate hello. Per questa esercitazione, verrà toobuild tutte le risorse in un'unica posizione di Azure.
9. Verificare che **toodashboard Pin** sia selezionata. Questa impostazione facoltativa viene inserito un collegamento per il gruppo di risorse hello in hello dashboard del portale di Azure.

   ![Gruppo di risorse](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroup.png)

10. Fare clic su **crea** toocreate gruppo di risorse hello.

Azure Crea gruppo di risorse hello e PIN di un gruppo di risorse toohello di scelta rapida nel portale di hello.

## <a name="create-hello-network-and-subnets"></a>Creare subnet e la rete hello
passaggio successivo Hello è toocreate hello reti e subnet nel gruppo di risorse di Azure hello.

soluzione Hello Usa una rete virtuale con due subnet. Hello [Panoramica di rete virtuale](../../../virtual-network/virtual-networks-overview.md) vengono fornite ulteriori informazioni sulle reti in Azure.

rete virtuale hello toocreate:

1. In hello portale di Azure, nel gruppo di risorse, fare clic su **+ Aggiungi**. Apre Azure hello **tutto** blade.

   ![Nuovo elemento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/02-newiteminrg.png)
2. Cercare **rete virtuale**.

     ![Cercare la rete virtuale](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/04-findvirtualnetwork.png)
3. Fare clic su **Rete virtuale**.
4. In hello **rete virtuale** pannello, fare clic su hello **Gestione risorse** modello di distribuzione e quindi fare clic su **crea**.

    Hello nella tabella seguente vengono mostrate hello impostazioni per la rete virtuale hello:

   | **Campo** | Valore |
   | --- | --- |
   | **Nome** |autoHAVNET |
   | **Spazio degli indirizzi** |10.33.0.0/24 |
   | **Nome della subnet** |Admin |
   | **Intervallo di indirizzi subnet** |10.33.0.0/29 |
   | **Sottoscrizione** |Specificare una sottoscrizione di hello che si desidera toouse. Se è disponibile una sola sottoscrizione, il valore di **Sottoscrizione** non è impostato. |
   | **Gruppo di risorse** |Scegliere **utilizzare esistente** e selezionare il nome di hello hello del gruppo di risorse. |
   | **Posizione** |Specificare hello località di Azure. |

   L'intervallo di indirizzi indirizzo spazio e la subnet potrebbe essere diverso dalla tabella hello. A seconda della sottoscrizione, hello portale viene suggerito un spazio degli indirizzi disponibili e l'intervallo di indirizzi subnet corrispondente. Se non è disponibile uno spazio indirizzi sufficiente, usare un'altra sottoscrizione.

   esempio Hello utilizza hello Nome subnet **Admin**. Questa subnet è hello ai controller di dominio.

5. Fare clic su **Crea**.

   ![Configurare la rete virtuale hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/06-configurevirtualnetwork.png)

Azure torna toohello dashboard del portale e invia una notifica quando viene creata nuova rete hello.

### <a name="create-a-second-subnet"></a>Creare una seconda subnet
nuova rete virtuale Hello presenta una subnet, denominata **Admin**. i controller di dominio hello usare questa subnet. Hello macchine virtuali di SQL Server utilizza una seconda subnet denominata **SQL**. tooconfigure questa subnet:

1. Nel dashboard, fare clic su gruppo di risorse hello che è stato creato, **SQL a disponibilità elevata-RG**. Individuare il gruppo di risorse hello in rete hello **risorse**.

    Se **SQL a disponibilità elevata-RG** non è visibile, individuarlo facendo **gruppi di risorse** e applicando un filtro per nome gruppo di risorse hello.
2. Fare clic su **autoHAVNET** nell'elenco di hello delle risorse. Azure apre il pannello di configurazione di rete hello.
3. In hello **autoHAVNET** blade di rete virtuale, in **impostazioni** , fare clic su **subnet**.

    Subnet hello si noti che già stato creato.

   ![Configurare la rete virtuale hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/07-addsubnet.png)
5. Creare una seconda subnet. Fare clic su **+ Subnet**.
6. In hello **aggiungere subnet** pannello configurare subnet hello digitando **sqlsubnet** in **nome**. Azure specifica automaticamente un **Intervallo di indirizzi**valido. Verificare che questo intervallo di indirizzi includa almeno 10 indirizzi. In un ambiente di produzione potrebbero essere necessari più indirizzi.
7. Fare clic su **OK**.

    ![Configurare la rete virtuale hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/08-configuresubnet.png)

Hello nella tabella seguente vengono riepilogate le impostazioni di configurazione di rete hello:

| **Campo** | Valore |
| --- | --- |
| **Nome** |**autoHAVNET** |
| **Spazio degli indirizzi** |Questo valore dipende da spazi di indirizzi disponibili hello nella sottoscrizione. Un valore tipico è 10.0.0.0/16. |
| **Nome della subnet** |**admin** |
| **Intervallo di indirizzi subnet** |Questo valore dipende da intervalli di indirizzi disponibili hello nella sottoscrizione. Un valore tipico è 10.0.0.0/24 |
| **Nome della subnet** |**sqlsubnet** |
| **Intervallo di indirizzi subnet** |Questo valore dipende da intervalli di indirizzi disponibili hello nella sottoscrizione. Un valore tipico è 10.0.1.0/24 |
| **Sottoscrizione** |Specificare una sottoscrizione di hello che si desidera toouse. |
| **Gruppo di risorse** |**SQL-HA-RG** |
| **Posizione** |Specificare hello stesso percorso scelto per il gruppo di risorse hello. |

## <a name="create-availability-sets"></a>Creare set di disponibilità

Prima di creare macchine virtuali, è necessario toocreate set di disponibilità. Set di disponibilità di riducono i tempi di inattività hello per gli eventi di manutenzione pianificato o. Un set di disponibilità di Azure è un gruppo logico di risorse che Azure inserisce in domini di errore e domini di aggiornamento fisici. Un dominio di errore garantisce che i membri del gruppo di disponibilità hello hello dispongano di risorse di rete e di alimentazione separate. Un dominio di aggiornamento assicura che i membri del gruppo di disponibilità hello non diventa inattivo per manutenzione nella hello stesso tempo. Per ulteriori informazioni, vedere [gestione hello disponibilità delle macchine virtuali](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Sono necessari due set di disponibilità, Uno è hello ai controller di dominio. in secondo luogo, Hello è per le macchine virtuali di hello SQL Server.

toocreate una disponibilità impostato, il gruppo di risorse toohello scegliere **Aggiungi**. Filtrare i risultati di hello digitando **set di disponibilità**. Fare clic su **Set di disponibilità** in hello risultati e quindi fare clic su **crea**.

Configurare due set di disponibilità in base a parametri toohello hello nella tabella seguente:

| **Campo** | Set di disponibilità del controller di dominio | Set di disponibilità di SQL Server |
| --- | --- | --- |
| **Nome** |adavailabilityset |sqlavailabilityset |
| **Gruppo di risorse** |Nome gruppo di risorse |Nome gruppo di risorse |
| **Domini di errore** |3 |3 |
| **Domini di aggiornamento** |5 |3 |

Dopo aver creato il set di disponibilità di hello, restituisce il gruppo di risorse toohello hello portale di Azure.

## <a name="create-domain-controllers"></a>Creare controller di dominio
Dopo aver creato rete hello, subnet, set di disponibilità e un servizio di bilanciamento del carico con connessione Internet, è possibile macchine virtuali di hello toocreate pronto per il controller di dominio di hello.

### <a name="create-virtual-machines-for-hello-domain-controllers"></a>Creare macchine virtuali per hello controller di dominio
toocreate e configurare il controller di dominio di hello, restituire toohello **SQL a disponibilità elevata-RG** gruppo di risorse.

1. Fare clic su **Aggiungi**. Hello **tutto** apre blade.
2. Digitare **Windows Server 2016 Datacenter**.
3. Fare clic su **Windows Server 2016 Datacenter**. In hello **Data Center di Windows Server 2016** pannello, verificare che sia il modello di distribuzione hello **Gestione risorse**e quindi fare clic su **crea**. Apre Azure hello **crea macchina virtuale** blade.

Ripetere hello precedenti passaggi toocreate due macchine virtuali. Nome hello due macchine virtuali:

* ad-primary-dc
* ad-secondary-dc

  > [!NOTE]
  > Hello **ad-secondario-dc** macchina virtuale è facoltativa, tooprovide la disponibilità elevata per servizi di dominio Active Directory.
  >
  >

Hello nella tabella seguente vengono mostrate hello impostazioni per questi due computer:

| **Campo** | Valore |
| --- | --- |
| **Nome** |Primo controller di dominio: *ad-primary-dc*.</br>Secondo controller di dominio: *ad-secondary-dc*. |
| **Tipo di disco VM** |SSD |
| **Nome utente** |DomainAdmin |
| **Password** |Contoso!0000 |
| **Sottoscrizione** |*Sottoscrizione in uso* |
| **Gruppo di risorse** |Nome gruppo di risorse |
| **Posizione** |*Località corrente* |
| **Dimensione** |DS1_V2 |
| **Archiviazione** | **Usa dischi gestiti** - **Sì** |
| **Rete virtuale** |autoHAVNET |
| **Subnet** |admin |
| **Indirizzo IP pubblico** |*Stesso nome hello VM* |
| **Gruppo di sicurezza di rete** |*Stesso nome hello VM* |
| **Set di disponibilità** |adavailabilityset </br>**Domini di errore**:2</br>**Domini di aggiornamento**:2|
| **Diagnostica** |Enabled |
| **Account di archiviazione di diagnostica** |*Creato automaticamente* |

   >[!IMPORTANT]
   >È possibile inserire una VM in un set di disponibilità solo in fase di creazione. È possibile modificare la disponibilità di hello impostata dopo la creazione di una macchina virtuale. Vedere [gestione hello disponibilità delle macchine virtuali](../manage-availability.md).

Azure consente di creare macchine virtuali hello.

Dopo aver create le macchine virtuali hello, configurare il controller di dominio di hello.

### <a name="configure-hello-domain-controller"></a>Configurare il controller di dominio hello
In hello i passaggi seguenti, configurare hello **ad-primary-dc** computer come controller di dominio per corp.contoso.com.

1. Nel portale di hello aprire hello **SQL a disponibilità elevata-RG** gruppo di risorse e seleziona hello **ad-primary-dc** macchina. In hello **ad-primary-dc** pannello, fare clic su **Connetti** tooopen un RDP file per l'accesso desktop remoto.

    ![Connettere la macchina virtuale di tooa](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/20-connectrdp.png)
2. Accedere con l'account amministratore (**\DomainAdmin**) e la password (**Contoso!0000**) configurati.
3. Per impostazione predefinita, hello **Server Manager** dashboard deve essere visualizzato.
4. Fare clic su hello **Aggiungi ruoli e funzionalità** collegamento nel dashboard di hello.

    ![Server Manager - Aggiungere ruoli](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
5. Selezionare **Avanti** fino a ottenere toohello **i ruoli del Server** sezione.
6. Seleziona hello **servizi di dominio Active Directory** e **Server DNS** ruoli. Quando richiesto, aggiungere eventuali funzionalità aggiuntive necessarie per questi ruoli.

   > [!NOTE]
   > Windows visualizza un avviso per indicare che non è presente alcun indirizzo IP statico. Se si sta testando configurazione hello, fare clic su **continua**. Per gli scenari di produzione, impostare toostatic indirizzo IP di hello in hello portale di Azure o [utilizzare PowerShell tooset hello indirizzo IP statico del computer controller di dominio hello](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   >
   >

    ![Finestra di dialogo Aggiungi ruoli](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/23-addroles.png)
7. Fare clic su **Avanti** fino a raggiungere hello **conferma** sezione. Seleziona hello **riavvio del server di destinazione hello automaticamente se necessario** casella di controllo.
8. Fare clic su **Installa**.
9. Dopo funzionalità hello completato l'installazione, restituire toohello **Server Manager** dashboard.
10. Seleziona hello nuovo **AD DS** opzione nel riquadro sinistro di hello.
11. Fare clic su hello **più** collegamento sulla barra di avviso gialla hello.

    ![Finestra di dialogo di AD DS su hello macchina virtuale di Server DNS](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/24-addsmore.png)
12. In hello **azione** colonna di hello **tutti i Server-dettagli attività** finestra di dialogo, fare clic su **alzare di livello questo controller di dominio server tooa**.
13. In hello **guidata configurazione di servizi di dominio di Active Directory**, utilizzare hello seguenti valori:

    | **Page** | Impostazione |
    | --- | --- |
    | **Configurazione distribuzione** |**Aggiungi una nuova foresta**<br/> **Nome di dominio radice** = corp.contoso.com |
    | **Opzioni controller di dominio** |**Password DSRM** = Contoso!0000<br/>**Conferma password** = Contoso!0000 |
14. Fare clic su **Avanti** toogo tramite hello altre pagine della procedura guidata hello. In hello **controllo dei prerequisiti** pagina, verificare che venga visualizzato hello seguente messaggio: **tutti i controlli dei prerequisiti sono riusciti**. È possibile esaminare i messaggi di avviso applicabile, ma è possibile toocontinue con installazione hello.
15. Fare clic su **Installa**. Hello **ad-primary-dc** macchina virtuale verrà riavviata automaticamente.

### <a name="note-hello-ip-address-of-hello-primary-domain-controller"></a>Prendere nota hello di indirizzo IP del controller di dominio primario hello

Utilizzare il controller di dominio primario hello per DNS. Nota l'indirizzo IP del controller di dominio primario hello.

Indirizzo IP di un modo tooget hello dominio primario del controller viene eseguita tramite hello portale di Azure.

1. Nel portale di Azure hello, aprire il gruppo di risorse hello.

2. Fare clic su controller di dominio primario hello.

3. Nel Pannello di controller di dominio primario hello, fare clic su **interfacce di rete**.

![Interfacce di rete](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/25-primarydcip.png)

Nota l'indirizzo IP privato hello per questo server.

### <a name="configure-hello-virtual-network-dns"></a>Configurare la rete virtuale hello DNS
Dopo aver creato il primo controller di dominio hello e abilitare il DNS nel server prima di hello, configurare hello rete virtuale toouse questo server per DNS.

1. Nel portale di Azure hello, fare clic su rete virtuale hello.

2. In **Impostazioni** fare clic su **Server DNS**.

3. Fare clic su **personalizzata**e digitare l'indirizzo IP privato hello hello primario del controller di dominio.

4. Fare clic su **Salva**.

### <a name="configure-hello-second-domain-controller"></a>Configurare il secondo controller di dominio hello
Dopo il riavvio di controller di dominio primario hello, è possibile configurare il secondo controller di dominio hello. Questo passaggio facoltativo serve a garantire una disponibilità elevata. Seguire questi passaggi tooconfigure hello secondo controller di dominio:

1. Nel portale di hello aprire hello **SQL a disponibilità elevata-RG** gruppo di risorse e seleziona hello **ad-secondario-dc** macchina. In hello **ad-secondario-dc** pannello, fare clic su **Connetti** tooopen un RDP file per l'accesso desktop remoto.
2. Accedi toohello VM utilizzando l'account amministratore configurato (**BUILTIN\DomainAdmin**) e la password (**Contoso! 0000**).
3. Modifica hello preferito DNS server toohello indirizzo hello del controller di dominio.
4. In **centro rete e condivisione**, fare clic su interfaccia di rete hello.
   ![Interfaccia di rete](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/26-networkinterface.png)

5. Fare clic su **Proprietà**.
6. Selezionare **Protocollo Internet versione 4 (TCP/IPv4)** e fare clic su **Proprietà**.
7. Selezionare **hello utilizzare seguenti indirizzi server DNS** e specificare l'indirizzo di hello del controller di dominio primario hello in **server DNS preferito**.
8. Fare clic su **OK**e quindi **Chiudi** modifiche hello toocommit. Questo punto si è in grado di toojoin hello VM troppo**corp.contoso.com**.

   >[!IMPORTANT]
   >Se si perde desktop remoto di hello connessione tooyour dopo la modifica delle impostazioni DNS hello, andare toohello portal e riavviare hello macchina virtuale di Azure.

9. Controller di dominio secondario hello toohello desktop remoto aprire **Dashboard di Server Manager**.
10. Fare clic su hello **Aggiungi ruoli e funzionalità** collegamento nel dashboard di hello.

    ![Server Manager - Aggiungere ruoli](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
11. Selezionare **Avanti** fino a ottenere toohello **i ruoli del Server** sezione.
12. Seleziona hello **servizi di dominio Active Directory** e **Server DNS** ruoli. Quando richiesto, aggiungere eventuali funzionalità aggiuntive necessarie per questi ruoli.
13. Dopo funzionalità hello completato l'installazione, restituire toohello **Server Manager** dashboard.
14. Seleziona hello nuovo **AD DS** opzione nel riquadro sinistro di hello.
15. Fare clic su hello **più** collegamento sulla barra di avviso gialla hello.
16. In hello **azione** colonna di hello **tutti i Server-dettagli attività** finestra di dialogo, fare clic su **alzare di livello questo controller di dominio server tooa**.
17. In **configurazione distribuzione**selezionare **aggiungere un controller di dominio tooan esistente dominio**.
   ![Configurazione distribuzione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/28-deploymentconfig.png)
18. Fare clic su **Seleziona**.
19. Connettersi con un account amministratore hello (**CORP. Contoso.COM\domainadmin**) e la password (**Contoso! 0000**).
20. In **selezionare un dominio dalla foresta hello**, selezionare il dominio e quindi fare clic su **OK**.
21. In **opzioni Controller di dominio**, utilizzare i valori predefiniti di hello e una password modalità ripristino servizi directory.

   >[!NOTE]
   >Hello **opzioni DNS** pagina potrebbe informare l'utente che non è possibile creare una delega per questo server DNS. È possibile ignorare questo avviso in ambienti non di produzione.
22. Fare clic su **Avanti** fino hello nella finestra di dialogo hello **prerequisiti** controllare. Fare clic su **Installa**.

Dopo aver hello server termina modifiche alla configurazione di hello, riavviare il server hello.

### <a name="add-hello-private-ip-address-toohello-second-domain-controller-toohello-vpn-dns-server"></a>Aggiungere l'indirizzo IP privato toohello secondo dominio controller toohello Server DNS VPN hello

Nel portale di Azure in rete virtuale, hello modificare l'indirizzo IP del controller di dominio secondario hello hello Server DNS tooinclude hello. In questo modo la ridondanza del servizio DNS di hello.

### <a name=DomainAccounts></a>Configurare gli account di dominio hello

Nei passaggi successivi hello, configurare gli account di Active Directory hello. Hello nella tabella seguente mostra gli account hello:

| |Account di installazione<br/> |sqlserver-0 <br/>Account del servizio SQL Agent e SQL Server |sqlserver-1<br/>Account del servizio SQL Agent e SQL Server
| --- | --- | --- | ---
|**Nome** |Installa |SQLSvc1 | SQLSvc2
|**Utente SamAccountName** |Installa |SQLSvc1 | SQLSvc2

Questa procedura hello utilizzare toocreate ogni account.

1. Accedi toohello **ad-primary-dc** macchina.
2. In **Server Manager** selezionare **Strumenti** e quindi fare clic su **Centro di amministrazione di Active Directory**.   
3. Selezionare **corp (locale)** hello nel riquadro di sinistra.
4. In hello destra **attività** riquadro, selezionare **New**, quindi fare clic su **utente**.
   ![Centro di amministrazione di Active Directory](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/29-addcnewuser.png)

   >[!TIP]
   >Impostare una password complessa per ogni account.<br/> Per gli ambienti non di produzione, toonever di account utente hello set scadrà.

5. Fare clic su **OK** utente hello toocreate.
6. Ripetere i passaggi precedenti per ognuno dei tre account hello hello.

### <a name="grant-hello-required-permissions-toohello-installation-account"></a>Concedere le autorizzazioni di hello necessario account di installazione toohello
1. In hello **il centro di amministrazione di Active Directory**selezionare **corp (locale)** nel riquadro di sinistra hello. Quindi nella finestra di destra hello **attività** riquadro, fare clic su **proprietà**.

    ![Proprietà utente CORP](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/31-addcproperties.png)
2. Selezionare **estensioni**, quindi fare clic su hello **avanzate** pulsante hello **sicurezza** scheda.
3. In hello **impostazioni di sicurezza avanzate per corp** finestra di dialogo, fare clic su **Aggiungi**.
4. Fare clic su **Seleziona un'entità**, cercare **CORP\Install** e quindi fare clic su **OK**.
5. Seleziona hello **Leggi tutte le proprietà** casella di controllo.

6. Seleziona hello **crea oggetti Computer** casella di controllo.

     ![Autorizzazioni utente Corp](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/33-addpermissions.png)
7. Fare clic su **OK** e quindi di nuovo clic su **OK**. Chiude hello **corp** finestra Proprietà.

Ora che è stata completata la configurazione di Active Directory e gli oggetti utente hello, creare due macchine virtuali di SQL Server e un server di controllo macchina virtuale. Aggiungere quindi tutti i tre dominio toohello.

## <a name="create-sql-server-vms"></a>Creare le macchine virtuali di SQL Server

Creare altre tre macchine virtuali. soluzione Hello richiede due macchine virtuali con istanze di SQL Server. Una terza macchina virtuale fungerà da controllo. Windows Server 2016 può usare un [cloud di controllo](http://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness); tuttavia, per uniformità con sistemi operativi precedenti, in questo documento si usa una macchina virtuale come controllo.  

Prima di procedere, è consigliabile hello seguente deisign decisioni.

* **Archiviazione - Azure Managed Disks**

   Per l'archiviazione della macchina virtuale hello, utilizzare i dischi gestiti di Azure. Microsoft consiglia Managed Disks per le macchine virtuali di SQL Server. Archivio di handle di dischi in background hello gestito. Inoltre, quando le macchine virtuali con dischi gestiti sono hello stesso set di disponibilità, Azure distribuisce hello risorse tooprovide appropriato la ridondanza dell'archiviazione. Per altre informazioni, vedere [Panoramica di Azure Managed Disks](../managed-disks-overview.md). Per informazioni dettagliate sui dischi gestiti in un set di disponibilità, vedere [Usare Managed Disks per le macchine virtuali nel set di disponibilità](../manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).

* **Rete - Indirizzi IP privati nell'ambiente di produzione**

   Per le macchine virtuali hello, questa esercitazione vengono utilizzati indirizzi IP pubblici. In questo modo di connessione remota direttamente toohello di macchina virtuale tramite hello internet - semplifica i passaggi di configurazione. Negli ambienti di produzione è consigliabile solo gli indirizzi IP privati footprint della vulnerabilità hello tooreduce ordine dell'istanza di SQL Server hello risorsa macchina virtuale.

### <a name="create-and-configure-hello-sql-server-vms"></a>Creare e configurare macchine virtuali di hello SQL Server
Creare successivamente tre VM, tra cui due VM di SQL Server e una VM per un nodo del cluster aggiuntivo. toocreate delle macchine virtuali di hello, tornare indietro toohello **SQL a disponibilità elevata-RG** gruppo di risorse, fare clic su **Aggiungi**, cercare l'elemento della raccolta appropriato hello, fare clic su **macchina virtuale**e quindi Fare clic su **dalla raccolta**. Utilizzare le informazioni di hello nella seguente tabella toohelp è creare macchine virtuali hello hello:


| Page | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Selezionare l'elemento della raccolta appropriato hello |**Windows Server 2016 Datacenter** |**SQL Server 2016 SP1 Enterprise on Windows Server 2016** |**SQL Server 2016 SP1 Enterprise on Windows Server 2016** |
| **Elementi di base** |**Nome** = cluster-fsw<br/>**Nome utente** = DomainAdmin<br/>**Password** = Contoso!0000<br/>**Sottoscrizione** = sottoscrizione<br/>**Gruppo di risorse** = SQL-HA-RG<br/>**Posizione** = posizione di Azure |**Nome** = sqlserver-0<br/>**Nome utente** = DomainAdmin<br/>**Password** = Contoso!0000<br/>**Sottoscrizione** = sottoscrizione<br/>**Gruppo di risorse** = SQL-HA-RG<br/>**Posizione** = posizione di Azure |**Nome** = sqlserver-1<br/>**Nome utente** = DomainAdmin<br/>**Password** = Contoso!0000<br/>**Sottoscrizione** = sottoscrizione<br/>**Gruppo di risorse** = SQL-HA-RG<br/>**Posizione** = posizione di Azure |
| Configurazione della macchina virtuale - **Dimensioni** |**DIMENSIONI** = DS1\_V2 (1 memoria centrale, 3,5 GB) |**DIMENSIONI** = DS2\_V2 (2 memorie centrali, 7 GB)</br>dimensioni Hello devono supportare l'archiviazione sull'unità SSD (supporto per dischi Premium. )) |**DIMENSIONI** = DS2\_V2 (2 memorie centrali, 7 GB) |
| Configurazione della macchina virtuale - **Impostazioni** |**Archiviazione**: Usa dischi gestiti.<br/>**Rete virtuale** = autoHAVNET<br/>**Subnet** = sqlsubnet(10.1.1.0/24)<br/>**Indirizzo IP pubblico** generato automaticamente.<br/>**Gruppo di sicurezza di rete** = nessuno<br/>**Monitoraggio e diagnostica** = abilitato<br/>**Account di archiviazione di diagnostica**: usare un account di archiviazione generato automaticamente<br/>**Set di disponibilità** = sqlAvailabilitySet<br/> |**Archiviazione**: Usa dischi gestiti.<br/>**Rete virtuale** = autoHAVNET<br/>**Subnet** = sqlsubnet(10.1.1.0/24)<br/>**Indirizzo IP pubblico** generato automaticamente.<br/>**Gruppo di sicurezza di rete** = nessuno<br/>**Monitoraggio e diagnostica** = abilitato<br/>**Account di archiviazione di diagnostica**: usare un account di archiviazione generato automaticamente<br/>**Set di disponibilità** = sqlAvailabilitySet<br/> |**Archiviazione**: Usa dischi gestiti.<br/>**Rete virtuale** = autoHAVNET<br/>**Subnet** = sqlsubnet(10.1.1.0/24)<br/>**Indirizzo IP pubblico** generato automaticamente.<br/>**Gruppo di sicurezza di rete** = nessuno<br/>**Monitoraggio e diagnostica** = abilitato<br/>**Account di archiviazione di diagnostica**: usare un account di archiviazione generato automaticamente<br/>**Set di disponibilità** = sqlAvailabilitySet<br/> |
| Configurazione della macchina virtuale - **Impostazioni SQL Server** |Non applicabile |**Connettività SQL** = privata (nella rete virtuale)<br/>**Porta** = 1433<br/>**Autenticazione SQL** = disabilitata<br/>**Configurazione dell'archiviazione** = generale<br/>**Applicazione automatica delle patch** = domenica alle 2:00<br/>**Backup automatizzato** = disabilitato</br>**Integrazione dell'insieme di credenziali delle chiavi di Azure** = Disabilitata |**Connettività SQL** = privata (nella rete virtuale)<br/>**Porta** = 1433<br/>**Autenticazione SQL** = disabilitata<br/>**Configurazione dell'archiviazione** = generale<br/>**Applicazione automatica delle patch** = domenica alle 2:00<br/>**Backup automatizzato** = disabilitato</br>**Integrazione dell'insieme di credenziali delle chiavi di Azure** = Disabilitata |

<br/>

> [!NOTE]
> le dimensioni della macchina Hello qui suggerite sono concepite per il test di gruppi di disponibilità in macchine virtuali di Azure. Per prestazioni ottimali di hello sui carichi di lavoro di produzione, visualizzare le raccomandazioni hello per le dimensioni della macchina SQL Server e la configurazione in [procedure consigliate per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-performance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

Dopo che le macchine virtuali hello tre completamente sono a provisioning, è necessario toojoin li toohello **corp.contoso.com** dominio e concedere le macchine toohello CORP\Install diritti amministrativi.

### <a name="joinDomain"></a>Dominio hello server toohello

Si è ora in grado di toojoin hello macchine virtuali troppo**corp.contoso.com**. Esempio hello per le macchine virtuali di hello SQL Server e file hello condivisione di server di controllo:

1. Connettersi in modalità remota la macchina virtuale con toohello **BUILTIN\DomainAdmin**.
2. In **Server Manager** fare clic su **Server locale**.
3. Fare clic su hello **WORKGROUP** collegamento.
4. In hello **nome Computer** fare clic su **modifica**.
5. Seleziona hello **dominio** casella di controllo e il tipo **corp.contoso.com** nella casella di testo hello. Fare clic su **OK**.
6. In hello **la sicurezza di Windows** finestra di dialogo popup, specificare le credenziali di hello per account di amministratore di dominio predefinito hello (**CORP\DomainAdmin**) e la password di hello (**Contoso! 0000**).
7. Quando viene visualizzato il messaggio "dominio corp.contoso.com toohello iniziale" hello, fare clic su **OK**.
8. Fare clic su **Chiudi**, quindi fare clic su **Riavvia ora** nella finestra di dialogo popup hello.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-cluster-vm"></a>Aggiungere l'utente Corp\Install hello come amministratore in ogni macchina virtuale del cluster

Dopo il riavvio di ogni macchina virtuale come membro del dominio hello, aggiungere **CORP\Install** come membro del gruppo administrators locale hello.

1. Attendere fino a quando non viene riavviato hello macchina virtuale, quindi avviare nuovamente da toosign di controller di dominio primario hello in file con estensione RDP hello troppo**sqlserver 0** utilizzando hello **CORP\DomainAdmin** account.
   >[!TIP]
   >Assicurarsi che si accede con l'account amministratore di dominio hello. Nei passaggi precedenti hello, si utilizzano account di amministratore predefiniti IN hello. Dopo avere hello server dominio hello, utilizzare account di dominio hello. Nella sessione RDP specificare *DOMINIO*\\*NOME UTENTE*.

2. In **Server Manager** selezionare **Strumenti**, quindi fare clic su **Gestione computer**.
3. In hello **Gestione Computer** finestra, espandere **utenti e gruppi locali**, quindi selezionare **gruppi**.
4. Fare doppio clic su hello **amministratori** gruppo.
5. In hello **proprietà amministratori** finestra di dialogo, fare clic su hello **Aggiungi** pulsante.
6. Immettere nome utente hello **CORP\Install**, quindi fare clic su **OK**.
7. Fare clic su **OK** tooclose hello **proprietà amministratore** finestra di dialogo.
8. Ripetere i passaggi precedenti hello in **sqlserver 1** e **cluster fsw**.

### <a name="setServiceAccount"></a>Impostare gli account del servizio SQL Server hello

In ogni macchina virtuale di SQL Server, impostare l'account del servizio SQL Server hello. Utilizzare account hello creati quando si [configurato gli account di dominio hello](#DomainAccounts).

1. Aprire **Gestione configurazione SQL Server**.
2. Fare doppio clic su servizio di SQL Server hello e quindi fare clic su **proprietà**.
3. Impostare l'account hello e una password.
4. Ripetere questi passaggi in hello altre VM SQL Server.  

Per i gruppi di disponibilità di SQL Server, ogni macchina virtuale di SQL Server deve toorun come account di dominio.

### <a name="create-a-sign-in-on-each-sql-server-vm-for-hello-installation-account"></a>Creare un accesso in ogni macchina virtuale di SQL Server per l'account di installazione di hello

Utilizzare il gruppo di disponibilità hello hello installazione account (CORP\install) tooconfigure. Questo account deve toobe un membro di hello **sysadmin** ruolo predefinito del server in ogni macchina virtuale di SQL Server. Hello seguenti passaggi necessari per creare un Accedi per account di installazione hello:

1. Connessione server toohello tramite hello Remote Desktop Protocol (RDP) con hello  *\<MachineName\>\DomainAdmin* account.

1. Aprire SQL Server Management Studio e connettersi toohello istanza locale di SQL Server.

1. In **Esplora oggetti** fare clic su **Sicurezza**.

1. Fare clic con il pulsante destro del mouse su **Account di accesso**. Fare clic su **Nuovo account di accesso**.

1. In **Account di accesso - Nuovo** fare clic su **Cerca**.

1. Fare clic su **Località**.

1. Immettere le credenziali di rete hello dominio amministratore.

1. Usare l'account di installazione di hello.

1. Un membro di hello del set di hello Accedi toobe **sysadmin** ruolo predefinito del server.

1. Fare clic su **OK**.

Ripetere hello precedenti passaggi in hello altre VM SQL Server.

## <a name="add-failover-clustering-features-tooboth-sql-server-vms"></a>Aggiungere tooboth di funzionalità Clustering di Failover le macchine virtuali di SQL Server

funzionalità di Clustering di Failover tooadd, hello in entrambe le macchine virtuali di SQL Server:

1. Connettersi toohello macchina virtuale di SQL Server tramite hello Remote Desktop Protocol (RDP) con hello *CORP\install* account. Aprire **Server Manager > Dashboard**.
2. Fare clic su hello **Aggiungi ruoli e funzionalità** collegamento nel dashboard di hello.

    ![Server Manager - Aggiungere ruoli](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
3. Selezionare **Avanti** fino a ottenere toohello **funzionalità Server** sezione.
4. In **Funzionalità** selezionare **Clustering di failover**.
5. Aggiungere le altre funzionalità necessarie.
6. Fare clic su **installare** funzionalità hello tooadd.

Ripetere i passaggi di hello in hello altre VM SQL Server.

## <a name="a-nameendpoint-firewall-configure-hello-firewall-on-each-sql-server-vm"></a><a name="endpoint-firewall">Configurare firewall hello in ogni macchina virtuale di SQL Server

soluzione Hello richiede hello seguendo le porte TCP toobe aprire nel firewall hello:

- **VM di SQL Server**:<br/>
   Porta 1433 per un'istanza predefinita di SQL Server.
- **Probe di Azure Load Balancer:**<br/>
   Qualsiasi porta disponibile. Negli esempi si usa spesso 59999.
- **Endpoint del mirroring del database:** <br/>
   Qualsiasi porta disponibile. Negli esempi si usa spesso 5022.

Hello firewall porte esigenza toobe aperti in entrambe le macchine virtuali di SQL Server.

metodo Hello dell'apertura di porte hello dipende dalla soluzione di firewall hello in uso. la sezione successiva di Hello spiega come hello tooopen porte in Windows Firewall. Aprire le porte necessarie hello in ognuna delle macchine virtuali SQL Server.

### <a name="open-a-tcp-port-in-hello-firewall"></a>Aprire una porta TCP nel firewall hello

1. Nel primo Server SQL di hello **avviare** schermata, avviare **Windows Firewall con sicurezza avanzata**.
2. Nel riquadro sinistro di hello selezionare **regole connessioni in entrata**. Nel riquadro di destra hello, fare clic su **nuova regola**.
3. Per **Tipo di regola** scegliere **Porta**.
4. Per la porta hello, specificare **TCP** e hello tipo appropriato di numeri di porta. Vedere hello di esempio seguente:

   ![Firewall SQL](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/35-tcpports.png)

5. Fare clic su **Avanti**.
6. In hello **azione** pagina, mantenere **Consenti connessione hello** selezionata e quindi fare clic su **Avanti**.
7. In hello **profilo** pagina, accettare le impostazioni predefinite di hello e quindi fare clic su **Avanti**.
8. In hello **nome** , specificare un nome di regola (ad esempio **Azure LB Probe**) in hello **nome** casella di testo e quindi fare clic su **fine**.

Ripetere questi passaggi su hello seconda macchina virtuale di SQL Server.

## <a name="next-steps"></a>Passaggi successivi

* [Creare un gruppo di disponibilità AlwaysOn in Macchine virtuali di Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md)
