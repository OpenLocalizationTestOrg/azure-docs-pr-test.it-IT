---
title: supporto aaaMulti tenant per la replica di VM VMware tooAzure (programma CSP) | Documenti Microsoft
description: Viene descritto come toodeploy Azure Site Recovery in un ambiente multi-tenant tooorchestrate replica, il failover e il ripristino di on-premise tooAzure di macchine virtuali (VM) VMware tramite il programma CSP hello utilizzando hello portale di Azure
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 9be555c9a438f66e6d3dfcdc9f507a84763846d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-tooazure-through-csp"></a>Supporto di multi-tenant in Azure Site Recovery per la replica tooAzure di macchine virtuali VMware tramite CSP

Azure Site Recovery supporta ambienti multi-tenant per sottoscrizioni tenant. Supporta inoltre multi-tenancy per le sottoscrizioni di tenant che vengono create e gestite tramite il programma di Provider di soluzioni Cloud (CSP) Microsoft hello. In questo articolo illustra in dettaglio indicazioni hello per implementare e gestire gli scenari di VMware in Azure multi-tenant. Sono illustrate anche la creazione e la gestione di sottoscrizioni tenant tramite CSP.

Questa Guida consente di disegnare notevolmente dalla documentazione esistente di hello per la replica tooAzure macchine virtuali VMware. Per ulteriori informazioni, vedere [tooAzure di macchine virtuali VMware replicare con il ripristino del sito](site-recovery-vmware-to-azure.md).

## <a name="multi-tenant-environments"></a>Ambienti multi-tenant
Esistono tre modelli multi-tenant principali:

* **Provider di servizi di Hosting (HSP) condiviso**: partner hello proprietaria dell'infrastruttura fisica hello e utilizza le risorse condivise (vCenter, Data Center, l'archiviazione fisica e così via) toohost hello di macchine virtuali di più tenant nella stessa infrastruttura. Hello partner includono Gestione ripristino di emergenza come un servizio gestito, o tenant hello può possedere il ripristino di emergenza come soluzione self-service.

* **Provider di servizi di Hosting dedicato**: hello partner sia il proprietario dell'infrastruttura fisica hello ma utilizza risorse dedicate (più vCenter, archivi dati fisici e così via) toohost macchine virtuali di ogni tenant in un'infrastruttura separata. Hello partner includono Gestione ripristino di emergenza come un servizio gestito, o tenant hello possono disporre di una soluzione self-service.

* **Il Provider di servizi (MSP) gestiti**: cliente hello possiede hello dell'infrastruttura che ospita macchine virtuali hello e partner hello include l'abilitazione del ripristino di emergenza e la gestione.

## <a name="shared-hosting-multi-tenant-guidance"></a>Indicazioni per il multi-tenant di hosting condiviso
Questa sezione descrive uno scenario di hosting condiviso di hello in modo dettagliato. altri due scenari Hello sono subset dello scenario di hosting condiviso hello e usano hello stessi principi. vengono descritte le differenze di Hello alla fine di hello del materiale sussidiario di hosting condiviso hello.

requisito di base in uno scenario di multi-tenant Hello è tooisolate hello tenant diversi. Un tenant non deve tooobserve in grado di ciò che ha ospitato un altro tenant. In un ambiente gestito dal partner, questo requisito non è importante come in un ambiente self-service, dove invece può essere fondamentale. Queste indicazioni presuppongono che sia necessario isolare i tenant.

architettura di Hello viene visualizzato nel seguente diagramma hello:

![Provider di servizi di hosting condiviso con un vCenter](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)  
**Scenario di hosting condiviso con un vCenter**

Come osservato nel diagramma precedente hello, ogni cliente ha un server di gestione separata. Questa configurazione limiti tenant accesso tootenant specifiche macchine virtuali e abilita l'isolamento dei tenant. Uno scenario di replica di macchina virtuale VMware utilizza hello configurazione server toomanage account toodiscover macchine virtuali e installare gli agenti. Si seguirà hello stessi principi per ambienti multi-tenant, con l'aggiunta di hello di limitare l'individuazione di macchina virtuale tramite vCenter controllo di accesso.

requisiti di isolamento dei dati Hello richiede che tutte le informazioni riservate dell'infrastruttura (ad esempio le credenziali di accesso) rimangono tootenants riservato. Per questo motivo, è consigliabile che tutti i componenti del server di gestione di hello rimangano sotto il controllo esclusivo della hello del partner hello. i componenti server di gestione di Hello sono:
* Server di configurazione
* Server di elaborazione
* Server di destinazione master 

PS un scalabilità orizzontale è anche sotto il controllo del partner hello.

### <a name="every-cs-in-hello-multi-tenant-scenario-uses-two-accounts"></a>Ogni CS in uno scenario di multi-tenant hello vengono utilizzati due account

- **account di accesso vCenter**: usare questo tenant toodiscover account macchine virtuali. Disponga delle autorizzazioni di accesso vCenter assegnate tooit (come descritto nella sezione successiva hello). toohelp evitare la perdita di accesso accidentale, è consigliabile che i partner immettere le credenziali stesse nello strumento di configurazione hello.

- **Account di accesso alla macchina virtuale**: usare questo agente di mobilità hello tooinstall account nel tenant hello macchine virtuali tramite un push automatico. In genere è un account di dominio che un tenant potrebbe fornire tooa partner oppure che, in alternativa, partner hello può gestire direttamente. Se un tenant non desidera che i dettagli di hello tooshare con partner hello direttamente, egli può essere consentito credenziali hello tooenter periodo di tempo limitato accesso toohello CS o con l'assistenza del partner di hello, installare manualmente agenti di mobilità.

### <a name="requirements-for-a-vcenter-access-account"></a>Requisiti per l'account di accesso a vCenter

Come indicato nella precedente sezione hello, è necessario configurare hello CS con un account che dispone di un tooit speciali ruolo assegnato. assegnazione di ruolo Hello deve essere applicata toohello vCenter account di accesso per ogni oggetto vCenter e non propagata gli oggetti figlio toohello. Questa configurazione assicura l'isolamento dei tenant, in quanto oggetti tooother accesso accidentale può provocare la propagazione di accesso.

![Hello propaga tooChild Objects-opzione](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

alternativa Hello è l'account utente di tooassign hello e ruolo in corrispondenza dell'oggetto Data Center hello e propagarle gli oggetti figlio toohello. Assegnare account hello un *Nessun accesso* ruolo per ogni oggetto (ad esempio, le macchine virtuali degli altri tenant) che deve essere accessibile tooa particolare tenant. Questa configurazione è un'operazione complessa, ed espone i controlli di accesso accidentale, perché ogni nuovo oggetto figlio viene automaticamente concessa anche accesso che viene ereditato dal padre hello. È pertanto consigliabile utilizzare primo approccio hello.

procedura di accesso di account vCenter Hello è come segue:

1. Creare un nuovo ruolo clonando hello predefinito *Read-only* ruolo e assegnargli un nome appropriato (ad esempio Azure_Site_Recovery, come illustrato in questo esempio).

2. Assegnare hello ruolo toothis le autorizzazioni seguenti:

    * **Datastore** (Archivio dati): Allocate space (Alloca spazio), Browse datastore (Sfoglia archivio dati), Low level file operations (Operazioni file di livello basso), Remove file (Rimuovi file), Update virtual machine files (Aggiorna file macchina virtuale)

    * **Network** (Rete): Network assign (Assegnazione rete)

    * **Risorsa**: assegnare tooresource pool di macchine Virtuali, migrazione lo spegnimento macchina virtuale, migrazione acceso VM

    * **Tasks** (Attività): Create task (Crea attività), Update task (Aggiorna attività)

    * **Virtual machine** (Macchina virtuale): 
        * Configuration (Configurazione) > all (tutto)
        * Interaction (Interazione) > Answer question (Rispondi alla domanda), Device connection (Connessione dispositivo), Configure CD media (Configura supporto CD), Configure floppy media (Configura supporto floppy), Power off (Spegni), Power on (Accendi), VMware tools install (Installazione strumenti VMware)
        * Inventory (Inventario) > Create from existing (Crea da esistente), Create new (Crea nuovo), Register (Registra), Unregister (Annulla registrazione)
        * Provisioning > Allow virtual machine download (Consenti download macchina virtuale), Allow virtual machine files upload (Consenti upload file macchina virtuale)
        * Snapshot management (Gestione snapshot) > Remove snapshots (Rimuovi snapshot)

    ![finestra di dialogo Modifica ruolo Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. Assegnare livelli toohello vCenter account di accesso (utilizzato nel tenant di hello. CS) per vari oggetti, come segue:

>| Oggetto | Ruolo | Osservazioni |
>| --- | --- | --- |
>| vCenter | Read-Only | VCenter tooallow solo accesso necessario per la gestione di oggetti diversi. È possibile rimuovere questa autorizzazione se account hello non verrà mai toobe fornito tooa tenant o utilizzato per tutte le operazioni di gestione hello vCenter. |
>| Data center | Azure_Site_Recovery |  |
>| Host e cluster host | Azure_Site_Recovery | Nuovo garantisce che l'accesso a livello di oggetto hello, in modo che gli host accessibili solo macchine virtuali tenant prima del failover e dopo il failback. |
>| Archivio dati e cluster archivio dati | Azure_Site_Recovery | Come sopra. |
>| Rete | Azure_Site_Recovery |  |
>| Server di gestione | Azure_Site_Recovery | Include i componenti di tooall di accesso (CS PS e MT) se sono di fuori di hello CS macchina. |
>| Macchine virtuali tenant | Azure_Site_Recovery | Assicura che qualsiasi nuovo tenant di macchine virtuali di un particolare tenant anche ottenere l'accesso o non sarà individuabile tramite hello portale di Azure. |

Hello vCenter account di accesso è stata completata. Questo passaggio sia appropriato per operazioni di failback toocomplete requisito hello autorizzazioni minime. Queste autorizzazioni di accesso possono essere usate anche con i criteri esistenti. Modificare solo le autorizzazioni set tooinclude ruolo le autorizzazioni esistenti al passaggio 2, dettagliate in precedenza.

operazioni di ripristino di emergenza toorestrict fino a quando lo stato di failover hello (vale a dire, senza le funzionalità di failback), attenersi alla procedura, con un'eccezione precedente hello: invece di assegnare hello *Azure_Site_Recovery* ruolo account di accesso vCenter toohello, assegnare solo un *Read-Only* toothat account membro del ruolo. Questo set di autorizzazioni consente il failover e la replica delle macchine virtuali e non consente il failback. Tutti gli altri elementi hello precedente rimane processo come è. tooensure l'isolamento del tenant e l'individuazione VM, ciascuna autorizzazione è ancora assegnato al livello toochild solo e non propagata di oggetti di hello.

## <a name="other-multi-tenant-environments"></a>Altri ambienti multi-tenant

Hello precedente sezione descritto come tooset di un ambiente multi-tenant per una soluzione di hosting condiviso. Hello altre due soluzioni principali sono hosting dedicato e del servizio gestito. architettura di Hello per le soluzioni è descritto in hello le sezioni seguenti.

### <a name="dedicated-hosting-solution"></a>Soluzione di hosting dedicato

Come illustrato nel seguente diagramma hello, differenza dell'architettura di hello in una soluzione di hosting dedicata è che ogni tenant impostato l'infrastruttura per il solo tale tenant. Poiché i tenant sono isolati tramite vCenter separato, provider di hosting hello devono effettuare i passaggi CSP hello forniti per l'hosting condiviso, ma non è necessario tooworry sull'isolamento dei tenant. La configurazione CSP resta invariata.

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)  
**Scenario di hosting dedicato con più vCenter**

### <a name="managed-service-solution"></a>Soluzione di servizi gestiti

Come hello illustrato nel diagramma seguente, differenza dell'architettura di hello in una soluzione del servizio gestito è che infrastruttura di ogni tenant sia fisicamente separata dall'infrastruttura degli altri tenant. Questo scenario si verifica in genere quando tenant hello proprietaria infrastruttura hello e richiede un ripristino di emergenza toomanage di provider di soluzioni. Nuovamente, poiché i tenant sono fisicamente isolati tramite infrastrutture differenti, partner hello deve toofollow hello CSP procedura per l'hosting condiviso, ma non è necessario tooworry sull'isolamento dei tenant. Il provisioning CSP resta invariato.

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)  
**Scenario di servizi gestiti con più vCenter**

## <a name="csp-program-overview"></a>Panoramica del programma CPS
Hello [programma CSP](https://partner.microsoft.com/en-US/cloud-solution-provider) rafforza la motivazione insieme a una situazione migliore storie che offrono partner tutti i servizi cloud Microsoft, inclusi Office 365, Enterprise Mobility Suite e Microsoft Azure. Con CSP, i partner proprietari relazione end-to-end hello con clienti e diventano punto di contatto primario relazione hello. Partner possono distribuire le sottoscrizioni di Azure per i clienti e combinare le sottoscrizioni di hello con le proprie offerte a valore aggiunto, personalizzate.

Con Azure Site Recovery, i partner possono gestire soluzione di ripristino di emergenza completa hello per i clienti direttamente tramite CSP. Oppure possono utilizzare tooset CSP ambienti Site Recovery e consentire ai clienti di gestire le proprie esigenze di ripristino di emergenza in modalità self-service. In entrambi gli scenari, i partner sono collegamento hello tra il ripristino del sito e i relativi clienti. I partner della relazione cliente hello del servizio e fatturare i clienti per l'utilizzo di Site Recovery.

## <a name="create-and-manage-tenant-accounts"></a>Creare e gestire account tenant

### <a name="step-0-prerequisite-check"></a>Passaggio 0: Controllo dei prerequisiti

Hello prerequisiti VM sono hello uguali a quelli descritti in hello [documentazione di Azure Site Recovery](site-recovery-vmware-to-azure.md). Nei prerequisiti toothose aggiunta, si deve che i controlli di accesso indicato in precedenza sul posto sia hanno hello prima di procedere con la gestione di tenant e CSP. Per ogni tenant, creare un server di gestione separata in grado di comunicare con macchine virtuali tenant hello e vCenter del partner. Solo i partner di hello dispone di server toothis diritti di accesso.

### <a name="step-1-create-a-tenant-account"></a>Passaggio 1: Creare un account tenant

1. Tramite [Microsoft Partner Center](https://partnercenter.microsoft.com/), eseguire l'accesso tooyour CSP account. 
 
2. In hello **Dashboard** dal menu **clienti**.

    ![collegamento Microsoft Partner Center clienti Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. Nella pagina hello che viene aperto, fare clic su hello **Aggiungi cliente** pulsante.

    ![pulsante Aggiungi cliente Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. In hello **nuovo cliente** pagina, riempimento nei dettagli per il tenant hello informazioni dell'account hello e quindi fare clic su **Avanti: sottoscrizioni**.

    ![pagina informazioni Account Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. Nella pagina Selezione hello sottoscrizioni selezionare hello **Microsoft Azure** casella di controllo. È possibile aggiungere altre sottoscrizioni subito o in qualsiasi momento nel futuro.

    ![casella di controllo di sottoscrizione Microsoft Azure Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. In hello **revisione** pagina verificare i dettagli del tenant hello e quindi fare clic su **Invia**.

    ![pagina verifica Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    Dopo aver creato l'account tenant hello, viene visualizzata una pagina di conferma, la visualizzazione dei dettagli di hello di hello account predefinito e hello password per la sottoscrizione. 

7. Salvare le informazioni di hello e modificare la password di hello in seguito in base alle esigenze tramite hello Azure portale nella pagina di accesso.  
 
    È possibile condividere queste informazioni con tenant hello come oppure è possibile creare e condividere un account separato, se necessario.

### <a name="step-2-access-hello-tenant-account"></a>Passaggio 2: Accesso account tenant hello

È possibile accedere sottoscrizione del tenant hello tramite hello Dashboard Center ai Partner Microsoft, come descritto in "passaggio 1: creare un account del tenant." 

1. Passare toohello **clienti** pagina e quindi fare clic su nome hello dell'account tenant hello.

2. In hello **sottoscrizioni** pagina dell'account tenant hello, è possibile monitorare le sottoscrizioni degli account esistenti hello e aggiungere altre sottoscrizioni, come richiesto. Selezionare le operazioni di ripristino di emergenza del tenant di hello toomanage, **tutte le risorse (portale di Azure)**.

    ![collegamento di tutte le risorse Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    Fare clic su **tutte le risorse** consenta l'accesso le sottoscrizioni di Azure toohello del tenant. È possibile verificare l'accesso facendo clic sul collegamento di Azure Active Directory hello in hello in alto a destra di hello portale di Azure.

    ![Collegamento di Azure Active Directory](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

È ora possibile eseguire tutte le operazioni di ripristino del sito per il tenant di hello tramite hello portale di Azure e gestire le operazioni di ripristino di emergenza hello. tooaccess hello sottoscrizione tenant tramite CSP per il ripristino di emergenza gestito, seguire hello descritto in precedenza processo.

### <a name="step-3-deploy-resources-toohello-tenant-subscription"></a>Passaggio 3: Distribuire una sottoscrizione di risorse toohello tenant
1. Nel portale di Azure hello, creare un gruppo di risorse e quindi distribuire un insieme di credenziali di servizi di ripristino per ogni processo di solito hello. 
 
2. Scaricare la chiave di registrazione dell'insieme di credenziali di hello.

3. Registrare hello CS per tenant hello utilizzando la chiave di registrazione dell'insieme di credenziali hello.

4. Immettere le credenziali di hello per gli account di accesso hello due: account di accesso vCenter e VM account di accesso.

    ![Gestire gli account del server di configurazione](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-toohello-recovery-services-vault"></a>Passaggio 4: Infrastruttura di Site Recovery di registro servizi di ripristino toohello insieme di credenziali
1. Nel portale di Azure, insieme di credenziali hello creato in precedenza hello, registrare hello vCenter server toohello CS registrate in "passaggio 3: distribuire la sottoscrizione tenant toohello alle risorse." A questo scopo, utilizzare l'account di accesso vCenter hello.
2. Completare il processo di "Preparazione dell'infrastruttura" hello per il ripristino del sito per ogni processo di solito hello.
3. macchine virtuali Hello sono ora pronti toobe replicati. Verificare che solo hello macchine virtuali del tenant vengono visualizzate sui hello **selezionare le macchine virtuali** pannello hello **replicare** opzione.

    ![Elenco di macchine virtuali tenant nel Pannello di hello selezionare le macchine virtuali](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-toohello-subscription"></a>Passaggio 5: Assegnare tenant accesso toohello sottoscrizione

Per il ripristino di emergenza self-service, dettagli toohello tenant hello account, come indicato nel passaggio 6 di hello "passaggio 1: creare un account tenant" sezione. Eseguire questa azione dopo partner hello configura l'infrastruttura di ripristino di emergenza hello. Se il tipo di ripristino di emergenza hello è gestito o self-service, partner di accedere al tenant sottoscrizioni tramite portale CSP hello. Essi impostare le proprietà dell'azienda partner dell'insieme di credenziali hello e registrare le sottoscrizioni di tenant di infrastruttura toohello.

Partner inoltre possono aggiungere una nuova sottoscrizione di tenant toohello utente tramite il portale CSP hello eseguendo hello seguenti:

1. Vai a pagina di sottoscrizione del tenant toohello CSP e quindi selezionare hello **utenti e licenze** opzione.

    ![pagina di sottoscrizione del tenant CSP Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    È ora possibile creare un nuovo utente immettendo i dettagli relativi a hello e modificando le autorizzazioni o caricando elenco hello degli utenti in un file CSV.

2. Dopo aver creato un nuovo utente, tornare indietro toohello Azure portale, quindi scegliere hello **sottoscrizione** blade, sottoscrizione pertinente selezionare hello.

3. Nel pannello hello visualizzata, selezionare **il controllo di accesso (IAM)**, quindi fare clic su **Aggiungi** tooadd un utente con livello di accesso pertinenti hello.      
    gli utenti di Hello che sono stati creati tramite il portale CSP hello vengono visualizzati automaticamente nel pannello hello visualizzato dopo aver selezionato un livello di accesso.

    ![Aggiungere un utente](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    Per la maggior parte delle operazioni di gestione, hello *collaboratore* ruolo è sufficiente. Gli utenti con questo livello di accesso possono eseguire qualsiasi operazione su una sottoscrizione, tranne modificare i livelli di accesso. Per questa operazione è infatti richiesto il livello di accesso *Proprietario*. È inoltre possibile ottimizzare i livelli di accesso hello come richiesto.
