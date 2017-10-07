---
title: 'Servizio di sincronizzazione Azure AD Connect: configurare il filtro | Documentazione Microsoft'
description: Viene illustrato come tooconfigure il filtro di sincronizzazione di Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 880facf6-1192-40e9-8181-544c0759d506
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 97979b508c560a6de6cb091b1b621bc1d51b25c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-configure-filtering"></a>Servizio di sincronizzazione Azure AD Connect: Configurare il filtro
L'applicazione di un filtro consente di controllare quali oggetti vengono visualizzati in Azure Active Directory (Azure AD) dalla directory locale. configurazione predefinita di Hello accetta tutti gli oggetti in tutti i domini in foreste hello configurato. In generale, si tratta di hello configurazione consigliata. Gli utenti che usano i carichi di lavoro di Office 365, come Exchange Online e Skype for Business, hanno a disposizione un elenco indirizzi globale completo per inviare messaggi di posta elettronica e chiamare chiunque. Con la configurazione predefinita di hello, hanno hello che stesse funzioni che hanno con un'implementazione locale di Exchange o Lync.

In alcuni casi, tuttavia, è necessario eseguire la configurazione di predefinito toohello alcune modifiche. Di seguito sono riportati alcuni esempi:

* Si prevede di hello toouse [multi-Azure topologia di Active directory](active-directory-aadconnect-topologies.md#each-object-only-once-in-an-azure-ad-tenant). È quindi necessario tooapply toocontrol un filtro gli oggetti che vengono sincronizzati tooa particolare Azure AD directory.
* Si esegue una distribuzione pilota per Azure o Office 365 e si vuole solo un subset di utenti in Azure AD. Progetto pilota di piccole dimensioni hello, non è importante toohave una funzionalità di hello toodemonstrate elenco indirizzi globale completezza.
* Si dispone di molti account del servizio e di altri account non personali non desiderati in Azure AD.
* Per motivi di conformità, non si eliminano account utente locali, li si disabilita soltanto, Ma in Azure AD, si desidera solo gli account active toobe presente.

Questo articolo descrive come tooconfigure hello diversi metodi di filtro.

> [!IMPORTANT]
> Microsoft non supporta la modifica o l'operando di sincronizzazione di Azure AD Connect azioni hello formalmente documentate. Ognuna di queste azioni potrebbe provocare uno stato incoerente o non supportato del sevizio di sincronizzazione Azure AD Connect. Microsoft pertanto non offre il supporto tecnico per distribuzioni di questo tipo.

## <a name="basics-and-important-notes"></a>Nozioni di base e note importanti
Nel servizio di sincronizzazione Azure AD Connect è possibile abilitare il filtro in qualsiasi momento. Se si inizia con una configurazione predefinita della sincronizzazione della directory e quindi configurare il filtro, hello oggetti che vengono filtrati non sono più sincronizzati tooAzure Active Directory. A causa di questa modifica, tutti gli oggetti in Azure AD sincronizzati in precedenza, ma successivamente esclusi, verranno eliminati in Azure AD.

Prima di apportare modifiche toofiltering, assicurarsi che si [disabilitare l'attività pianificata hello](#disable-scheduled-task) in modo non accidentalmente esportate le modifiche che non è ancora stato verificato toobe corretto.

Poiché il filtro può rimuovere molti oggetti hello stesso tempo, si desidera assicurarsi che i nuovi filtri siano corretti prima di iniziare qualsiasi esportazione toomake cambia tooAzure Active Directory. Dopo aver completato i passaggi di configurazione hello, è consigliabile seguire hello [i passaggi di verifica](#apply-and-verify-changes) prima di esportare e apportare le modifiche tooAzure Active Directory.

funzionalità di eliminazione di molti oggetti accidentalmente, hello tooprotect "[impedire eliminazioni accidentali](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" è attivata per impostazione predefinita. Se si eliminano molti oggetti scadenza toofiltering (500 per impostazione predefinita), è necessario passaggi hello toofollow questo hello tooallow articolo Elimina toogo tramite tooAzure Active Directory.

Se si usa una compilazione prima di novembre 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)), apportare una tooa modificare la configurazione di filtro e utilizzare la sincronizzazione delle password, è necessario tootrigger una sincronizzazione completa di tutte le password dopo aver completato la configurazione di hello. Per i passaggi per la modalità di sincronizzazione completa tootrigger una password, vedere [attivare una sincronizzazione completa di tutte le password](active-directory-aadconnectsync-troubleshoot-password-synchronization.md#trigger-a-full-sync-of-all-passwords). Se si è in fase di compilazione 1.0.9125 o versione successiva, quindi hello regular **completo sincronizzazione** azione calcola anche se le password devono essere sincronizzate e se questo passaggio aggiuntivo non è più necessario.

Se **utente** gli oggetti sono stati eliminati inavvertitamente in Azure AD a causa di un errore di filtro, è possibile ricreare gli oggetti utente hello in Azure AD rimuovendo le configurazioni di filtro. e successivamente sincronizzare nuovamente le directory. Questa azione consente di ripristinare gli utenti di hello dal Cestino hello in Azure AD. Non è tuttavia possibile annullare l'eliminazione di altri tipi di oggetto. Ad esempio, se si elimina accidentalmente un gruppo di sicurezza ed era utilizzato tooACL una risorsa, gruppo hello e il relativo ACL non può essere recuperato.

Azure AD Connect Elimina solo gli oggetti che è considerata una volta toobe nell'ambito. Se in Azure AD sono presenti oggetti creati da un altro motore di sincronizzazione, ma non compresi nell'ambito, l'aggiunta del filtro non ne determina la rimozione. Ad esempio, se si dispone di un server DirSync che ha creato una copia completa dell'intera directory di Azure AD e si installa un nuovo server di sincronizzazione di Azure AD Connect in parallelo con il filtro attivato dall'inizio di hello, Azure AD Connect non rimuove hello aggiuntivo oggetti creati tramite DirSync.

configurazione del filtro Hello viene mantenuto quando si installa o aggiorna tooa la versione più recente di Azure AD Connect. È sempre un migliore tooverify di procedure consigliate che hello configurazione non è stata modificata inavvertitamente dopo una versione più recente aggiornamento tooa prima di eseguire hello come primo ciclo di sincronizzazione.

Se si dispone di più di una foresta, quindi è necessario applicare il filtro delle configurazioni descritte in questa foresta tooevery argomento hello (presupponendo che si desideri hello stessa configurazione per tutti gli elementi).

### <a name="disable-hello-scheduled-task"></a>Disabilitare l'attività pianificata hello
toodisable hello predefinite dell'utilità di pianificazione che attiva un ciclo di sincronizzazione ogni 30 minuti, seguire questi passaggi:

1. Passare tooa prompt di PowerShell.
2. Eseguire `Set-ADSyncScheduler -SyncCycleEnabled $False` dell'utilità di pianificazione di toodisable hello.
3. Apportare modifiche hello sono documentate in questo articolo.
4. Eseguire `Set-ADSyncScheduler -SyncCycleEnabled $True` tooenable hello dell'utilità di pianificazione nuovamente.

**Se si usa una build di Azure AD Connect precedente a 1.1.105.0**  
toodisable hello attività pianificata che attiva un ciclo di sincronizzazione ogni tre ore, seguire questi passaggi:

1. Avviare **utilità di pianificazione** da hello **avviare** menu.
2. Direttamente sotto **libreria utilità di pianificazione**, attività di ricerca hello denominata **Azure AD Sync Scheduler**, pulsante destro del mouse e selezionare **disabilitare**.  
   ![Utilità di pianificazione](./media/active-directory-aadconnectsync-configure-filtering/taskscheduler.png)  
3. È possibile apportare modifiche alla configurazione ed eseguire manualmente il motore di sincronizzazione hello da hello **Synchronization Service Manager** console.

Dopo aver completato tutte le modifiche di filtro, non dimenticare toocome nuovamente e **abilitare** attività hello nuovamente.

## <a name="filtering-options"></a>Opzioni di filtro
È possibile applicare hello filtro configurazione tipi toohello directory dello strumento di sincronizzazione seguenti:

* [**In base al gruppo**](#group-based-filtering): il filtro basato su un singolo gruppo può essere configurato solo durante l'installazione iniziale utilizzando Installazione guidata di hello.
* [**Basato su dominio**](#domain-based-filtering): con questa opzione, è possibile selezionare i domini che sincronizza tooAzure Active Directory. È anche possibile aggiungere e rimuovere i domini dalla configurazione del motore di sincronizzazione hello quando si effettua l'infrastruttura locale di tooyour le modifiche apportate dopo l'installazione di sincronizzazione di Azure AD Connect.
* [**Unità organizzativa (OU) – basato su**](#organizational-unitbased-filtering): tramite questa opzione, è possibile selezionare le unità organizzative sincronizzare tooAzure Active Directory. Questa opzione è disponibile in tutti i tipi di oggetto nelle unità organizzative selezionate.
* [**Basato su attributi**](#attribute-based-filtering): con questa opzione, è possibile filtrare gli oggetti in base ai valori di attributo per gli oggetti hello. È anche possibile avere filtri diversi a seconda del tipo di oggetto.

È possibile utilizzare più opzioni di filtro in hello contemporaneamente. Ad esempio, è possibile utilizzare il filtro basato su unità Organizzativa tooonly includere gli oggetti in un'unità Organizzativa. AT hello stesso tempo, è possibile utilizzare ulteriori oggetti filtro toofilter hello basati su attributo. Quando si utilizzano più metodi di filtro, i filtri di hello utilizzano un operatore logico "AND" tra i filtri di hello.

## <a name="domain-based-filtering"></a>Filtro basato su dominio
Questa sezione vengono fornite hello passaggi tooconfigure il filtro basato su dominio. Se è stato aggiunto o rimosso domini della foresta dopo l'installazione di Azure AD Connect, è necessario anche hello tooupdate configurazione del filtro.

Hello preferito modo toochange basato su dominio filtro installazione guidata di hello e modificando [dominio e unità Organizzativa filtro](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). installazione guidata di Hello consente di automatizzare tutte le attività hello sono documentate in questo argomento.

È necessario seguire questi passaggi solo se non si ha l'installazione guidata di hello toorun non è possibile per qualche motivo.

La configurazione del filtro basato su dominio prevede questi passaggi:

1. [Selezionare i domini hello](#select-domains-to-be-synchronized) che si desidera tooinclude sincronizzazione hello.
2. Per ogni stato aggiunto e rimosso dominio, regolare hello [profili di esecuzione](#update-run-profiles).
3. [Applicare e verificare le modifiche](#apply-and-verify-changes)

### <a name="select-hello-domains-toobe-synchronized"></a>Hello selezionare domini toobe sincronizzato
dominio hello tooset filtrare, hello i passaggi seguenti:

1. Accedi toohello server che esegue la sincronizzazione di Azure AD Connect utilizzando un account che è un membro di hello **ADSyncAdmins** gruppo di sicurezza.
2. Avviare **servizio di sincronizzazione** da hello **avviare** menu.
3. Selezionare **connettori**e in hello **connettori** selezionare hello connettore con tipo di hello **servizi di dominio Active Directory**. In **Actions** (Azioni) selezionare **Properties** (Proprietà).  
   ![Proprietà del connettore](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Fare clic su **Configure Directory Partitions**.
5. In hello **seleziona partizioni di directory** elenco, selezionare e deselezionare i domini in base alle esigenze. Verificare che siano selezionate solo le partizioni di hello che si desidera toosynchronize.  
   ![Partizioni](./media/active-directory-aadconnectsync-configure-filtering/connectorpartitions.png)  
   Se hai modificato l'infrastruttura di Active Directory locale e aggiungere o rimuovere domini dalla foresta hello, quindi fare clic su hello **aggiornamento** pulsante tooget un elenco aggiornato. Quando si esegue l'aggiornamento, vengono richieste le credenziali. Fornire le credenziali con accesso in lettura tooWindows Server Active Directory. Non ha utente hello toobe che viene popolato preliminarmente nella finestra di dialogo hello.  
   ![Aggiornamento necessario](./media/active-directory-aadconnectsync-configure-filtering/refreshneeded.png)  
6. Al termine, chiudere hello **proprietà** finestra di dialogo, fare clic su **OK**. Se sono stati rimossi i domini dalla foresta hello, viene visualizzato un messaggio popup che è stato rimosso un dominio e che la configurazione verrà eseguita la pulizia.
7. Continuare hello tooadjust [profili di esecuzione](#update-run-profiles).

### <a name="update-hello-run-profiles"></a>Aggiornare i profili di esecuzione hello
Se è stato aggiornato il filtro basato su dominio, è necessario anche i profili di esecuzione hello tooupdate.

1. In hello **connettori** elenco, verificare che tale hello connettore che sono stati modificati nel passaggio precedente hello è selezionata. In **Actions** (Azioni) selezionare **Configure Run Profiles** (Configura profili di esecuzione).  
   ![Profili di esecuzione del connettore 1](./media/active-directory-aadconnectsync-configure-filtering/connectorrunprofiles1.png)  
2. Individuare e identificare hello profili seguenti:
    * Importazione completa
    * sincronizzazione completa
    * Importazione differenziale
    * Sincronizzazione differenziale
    * Esporta
3. Per ogni profilo, regolare hello **aggiunto** e **rimosso** domini.
    1. Per ogni profilo hello cinque, hello i passaggi seguenti per ogni **aggiunto** dominio:
        1. Selezionare il profilo di esecuzione hello e fare clic su **nuovo passaggio**.
        2. In hello **Configure Step** pagina hello **tipo** dal menu a discesa tipo di passaggio hello selezionare con hello stesso nome come hello del profilo che si sta configurando. Quindi fare clic su **Next**.  
        ![Profili di esecuzione del connettore 2](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep1.png)  
        3. In hello **configurazione connettore** pagina hello **partizione** dal menu a discesa, nome selezionare hello del dominio di hello aggiunti tooyour filtro basato su dominio.  
        ![Profili di esecuzione del connettore 3](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep2.png)  
        4. hello tooclose **Configure Run Profile** finestra di dialogo, fare clic su **fine**.
    2. Per ogni profilo hello cinque, hello i passaggi seguenti per ogni **rimosso** dominio:
        1. Selezionare il profilo di esecuzione hello.
        2. Se hello **valore** di hello **partizione** attributo è un GUID, seleziona hello esecuzione passaggio e fare clic su **Delete Step**.  
        ![Profili di esecuzione del connettore 4](./media/active-directory-aadconnectsync-configure-filtering/runprofilesdeletestep.png)  
    3. Verificare la modifica. Ogni dominio che si desidera toosynchronize dovrebbe essere elencato come un passaggio in ogni profilo di esecuzione.
4. hello tooclose **Configure Run Profiles** finestra di dialogo, fare clic su **OK**.
5.  configurazione di hello toocomplete, è necessario toorun un **importazione completa** e **sincronizzazione Delta**. Continuare a leggere la sezione hello [applica e verificare le modifiche](#apply-and-verify-changes).

## <a name="organizational-unitbased-filtering"></a>Filtro basato su unità organizzative
Hello preferito modalità di filtraggio basato su unità Organizzativa di toochange installazione guidata di hello e modificando [dominio e unità Organizzativa filtro](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). installazione guidata di Hello consente di automatizzare tutte le attività hello sono documentate in questo argomento.

È necessario seguire questi passaggi solo se non si ha l'installazione guidata di hello toorun non è possibile per qualche motivo.

tooconfigure aziendale basato sull'unità filtro, hello i passaggi seguenti:

1. Accedi toohello server che esegue la sincronizzazione di Azure AD Connect utilizzando un account che è un membro di hello **ADSyncAdmins** gruppo di sicurezza.
2. Avviare **servizio di sincronizzazione** da hello **avviare** menu.
3. Selezionare **connettori**e in hello **connettori** selezionare hello connettore con tipo di hello **servizi di dominio Active Directory**. In **Actions** (Azioni) selezionare **Properties** (Proprietà).  
   ![Proprietà del connettore](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Fare clic su **Configura partizioni di Directory**selezionare dominio hello che desidera tooconfigure e quindi fare clic su **contenitori**.
5. Quando richiesto, fornire le credenziali con accesso in lettura tooyour locale di Active Directory. Non ha utente hello toobe che viene popolato preliminarmente nella finestra di dialogo hello.
6. In hello **selezionare contenitori** la finestra di dialogo, le unità organizzative crittografato hello non desidera toosynchronize con la directory cloud hello e quindi fare clic su **OK**.  
   ![Unità organizzative nella finestra di dialogo Seleziona contenitori hello](./media/active-directory-aadconnectsync-configure-filtering/ou.png)  
   * Hello **computer** contenitore deve essere selezionato per il toobe computer Windows 10 siano stati sincronizzati correttamente tooAzure Active Directory. Se i computer aggiunti a un dominio si trovano in altre unità organizzative, verificare che queste ultime siano selezionate.
   * Hello **ForeignSecurityPrincipals** contenitore deve essere selezionato se si dispone di più foreste con trust. Questo contenitore consente toobe l'appartenenza al gruppo di sicurezza tra foreste risolto.
   * Hello **RegisteredDevices** unità Organizzativa deve essere selezionata se è abilitata la funzionalità di writeback dispositivi hello. Se si usa un'altra funzionalità di writeback, ad esempio il writeback dei gruppi, verificare che queste posizioni siano selezionate.
   * Selezionare le altre unità organizzative in cui si trovano Users, iNetOrgPersons, Groups, Contacts e Computers. Nell'immagine di hello, tutte queste unità organizzative sono posizionate in hello ManagedObjects OU.
   * Se si utilizza il filtro basato sul gruppo, hello unità Organizzativa in cui si trova il gruppo di hello deve essere incluso.
   * Si noti che è possibile configurare se nuove unità organizzative che vengono aggiunti al termine della configurazione del filtro hello sono state sincronizzate o non è sincronizzate. Vedere hello sezione successiva per informazioni dettagliate.
7. Al termine, chiudere hello **proprietà** finestra di dialogo, fare clic su **OK**.
8. configurazione di hello toocomplete, è necessario toorun un **importazione completa** e **sincronizzazione Delta**. Continuare a leggere la sezione hello [applica e verificare le modifiche](#apply-and-verify-changes).

### <a name="synchronize-new-ous"></a>Sincronizzare nuove unità organizzative
Le nuove unità organizzative create dopo la configurazione del filtro vengono sincronizzate per impostazione predefinita. Questo stato è indicato da una casella di controllo selezionata. È anche possibile deselezionare alcune unità organizzative secondarie. tooget questo comportamento, fare clic su casella hello finché diventa bianco con un segno di spunta blu (stato predefinito). Deselezionare qualsiasi OU secondarie che non si desidera toosynchronize.

Se tutte le unità organizzative secondaria sono sincronizzate, quindi casella hello è bianco con un segno di spunta blu.  
![Unità organizzativa con tutte le caselle selezionate](./media/active-directory-aadconnectsync-configure-filtering/ousyncnewall.png)

Se alcuni OU secondarie siano stati deselezionati, casella hello è grigio con un segno di spunta bianco.  
![Unità organizzativa con alcune unità organizzative secondarie deselezionate](./media/active-directory-aadconnectsync-configure-filtering/ousyncnew.png)

In questa configurazione una nuova unità organizzativa creata in ManagedObjects è sincronizzata.

installazione guidata di Hello Azure AD Connect è Crea sempre questa configurazione.

### <a name="dont-synchronize-new-ous"></a>Non sincronizzare nuove unità organizzative
È possibile configurare la sincronizzazione di hello motore toonot sincronizzare nuove unità organizzative termine hello configurazione del filtro. Questo stato è indicato nell'interfaccia utente dalla casella hello visualizzati grigio a tinta unita senza segno di spunta hello. tooget questo comportamento, fare clic su casella hello finché diventa bianco con alcun segno di spunta. Selezionare quindi hello sub-unità organizzative che si desidera toosynchronize.

![Unità Organizzativa con radice hello deselezionato](./media/active-directory-aadconnectsync-configure-filtering/oudonotsyncnew.png)

In questa configurazione una nuova unità organizzativa creata in ManagedObjects non è sincronizzata.

## <a name="attribute-based-filtering"></a>Filtro basato su attributo
Assicurarsi che si usi hello novembre 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) o compilazione successive per questi passi toowork.

Filtraggio basato su un attributo è hello più flessibile come toofilter degli oggetti. È possibile utilizzare power hello di [provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md) toocontrol quasi ogni aspetto di quando un oggetto è sincronizzato tooAzure Active Directory.

È possibile applicare [in ingresso](#inbound-filtering) filtro dal metaverse toohello Active Directory, e [in uscita](#outbound-filtering) il filtraggio di hello metaverse tooAzure Active Directory. Si consiglia di applicare il filtro in ingresso perché è più semplice toomaintain di hello. Utilizzare solo il filtro in uscita se è necessario toojoin oggetti da più di una foresta prima valutazione hello può avvenire.

### <a name="inbound-filtering"></a>Filtri in ingresso
Filtro in ingresso utilizza configurazione predefinita di hello, in cui degli oggetti diretti AD tooAzure è necessario impostare hello metaverse attributo cloudFiltered non tooa valore toobe sincronizzato. Se il valore dell'attributo è impostato troppo**True**, quindi l'oggetto hello non è sincronizzato. Non deve essere impostata troppo**False**, per impostazione predefinita. toomake avere altre regole hello possibilità toocontribute un valore, questo attributo è previsto solo i valori hello toohave **True** o **NULL** (assente).

Applicazione dei filtri in ingresso, utilizzare potenza hello **ambito** toodetermine oggetti toosynchronize o non eseguire la sincronizzazione. Si tratta in cui si apportano modifiche toofit requisiti dell'organizzazione. modulo ambito Hello è un **gruppo** e **clausola** toodetermine quando una regola di sincronizzazione è nell'ambito. Un gruppo contiene una o più clausole. Tra più clausole viene inserito un operatore AND logico e tra più gruppi un operatore OR logico.

Ecco un esempio:   
![Ambito](./media/active-directory-aadconnectsync-configure-filtering/scope.png)  
Deve essere letto come **(department = IT) OR (department = Sales AND c = US)**.

In hello seguenti esempi e procedure, utilizzare l'oggetto utente hello ad esempio, ma è possibile utilizzare questo per tutti i tipi di oggetto.

In hello seguendo gli esempi, il valore di precedenza hello inizia a 50. Può trattarsi di un numero qualsiasi non in uso, ma deve essere minore di 100.

#### <a name="negative-filtering-do-not-sync-these"></a>Filtro negativo (non sincronizzare gli elementi indicati)
Nell'esempio seguente di hello, si esclude (non sincronizzare) tutti gli utenti in cui **extensionAttribute15** ha valore hello **NoSync**.

1. Accedi toohello server che esegue la sincronizzazione di Azure AD Connect utilizzando un account che è un membro di hello **ADSyncAdmins** gruppo di sicurezza.
2. Avviare **Editor regole di sincronizzazione** da hello **avviare** menu.
3. Verifica che sia selezionata l'opzione **Inbound** (In ingresso) e fare clic su **Add New Rule** (Aggiungi nuova regola).
4. Assegnare regola hello un nome descrittivo, ad esempio "*In from AD – utente DoNotSyncFilter*". Selezionare hello corretto insieme di strutture, selezionare **utente** come hello **tipo di oggetto CS**e selezionare **persona** come hello **tipo di oggetto MV**. In **Link Type** (Tipo di collegamento) selezionare **Join** (Unisci). In **Precedence** (Precedenza) digitare un valore attualmente non usato da un'altra regola di sincronizzazione, ad esempio 50, e quindi fare clic su **Next** (Avanti).  
   ![Descrizione in ingresso 1](./media/active-directory-aadconnectsync-configure-filtering/inbound1.png)  
5. In **Scoping filter** (Filtro ambito) fare clic su **Add Group** (Aggiungi gruppo) e quindi fare clic su **Add Clause** (Aggiungi clausola). In **Attribute** (Attributo) selezionare **ExtensionAttribute15**. Assicurarsi che **operatore** è troppo**uguale**, quindi digitare il valore di hello **NoSync** in hello **valore** casella. Fare clic su **Avanti**.  
   ![Ambito in ingresso 2](./media/active-directory-aadconnectsync-configure-filtering/inbound2.png)  
6. Lasciare hello **Join** regole vuota e quindi fare clic su **Avanti**.
7. Fare clic su **Aggiungi trasformazione**selezionare hello **FlowType** come **costante**e selezionare **cloudFiltered** come hello  **Attributo di destinazione**. In hello **origine** nella casella di testo **True**. Fare clic su **Aggiungi** regola hello toosave.  
   ![Trasformazione in ingresso 3](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)
8. configurazione di hello toocomplete, è necessario toorun un **sincronizzazione completa**. Continuare a leggere la sezione hello [applica e verificare le modifiche](#apply-and-verify-changes).

#### <a name="positive-filtering-only-sync-these"></a>Filtro positivo (sincronizzare solo gli elementi indicati)
Espressione filtro positivo può essere più complessa perché si dispone anche di oggetti tooconsider che non sono evidenti toobe sincronizzati, ad esempio le sale riunioni. Sono anche filtro predefinito di corso toooverride hello nella regola out-of-box hello **In ingresso da AD – User Join**. Quando si crea filtro personalizzato, verificare che toonot includono oggetti di sistema critici, gli oggetti dei conflitti di replica, le cassette postali speciali e gli account del servizio hello per Azure AD Connect.

opzione di filtro positivo Hello richiede due regole di sincronizzazione. È necessaria una regola (o più) con ambito corretto hello toosynchronize oggetti. È necessaria anche una seconda regola di sincronizzazione catch-all che esclude tutti gli oggetti non ancora identificati come oggetti da sincronizzare.

Nell'esempio seguente di hello, si sincronizzano soltanto gli oggetti utente in cui attributo department hello ha valore hello **vendite**.

1. Accedi toohello server che esegue la sincronizzazione di Azure AD Connect utilizzando un account che è un membro di hello **ADSyncAdmins** gruppo di sicurezza.
2. Avviare **Editor regole di sincronizzazione** da hello **avviare** menu.
3. Verifica che sia selezionata l'opzione **Inbound** (In ingresso) e fare clic su **Add New Rule** (Aggiungi nuova regola).
4. Assegnare regola hello un nome descrittivo, ad esempio "*In from AD – utente vendite di sincronizzazione*". Selezionare hello corretto insieme di strutture, selezionare **utente** come hello **tipo di oggetto CS**e selezionare **persona** come hello **tipo di oggetto MV**. In **Link Type** (Tipo di collegamento) selezionare **Join** (Unisci). In **Precedence** (Precedenza) digitare un valore attualmente non usato da un'altra regola di sincronizzazione, ad esempio 51, e quindi fare clic su **Next** (Avanti).  
   ![Destinazione in ingresso 4](./media/active-directory-aadconnectsync-configure-filtering/inbound4.png)  
5. In **Scoping filter** (Filtro ambito) fare clic su **Add Group** (Aggiungi gruppo) e quindi fare clic su **Add Clause** (Aggiungi clausola). In **Attribute** (Attributo) selezionare **department**. Verificare che l'operatore viene impostato troppo**uguale**, quindi digitare il valore di hello **Sales** in hello **valore** casella. Fare clic su **Avanti**.  
   ![Ambito in ingresso 5](./media/active-directory-aadconnectsync-configure-filtering/inbound5.png)  
6. Lasciare hello **Join** regole vuota e quindi fare clic su **Avanti**.
7. Fare clic su **Aggiungi trasformazione**selezionare **costante** come hello **FlowType**e seleziona hello **cloudFiltered** come hello  **Attributo di destinazione**. In hello **origine** digitare **False**. Fare clic su **Aggiungi** regola hello toosave.  
   ![Trasformazione in ingresso 6](./media/active-directory-aadconnectsync-configure-filtering/inbound6.png)  
   Questo è un caso speciale in cui è impostato esplicitamente cloudFiltered troppo**False**.
8. È ora disponibile regola di sincronizzazione di catch-all toocreate hello. Assegnare regola hello un nome descrittivo, ad esempio "*In from AD – filtro utente Catch-all*". Selezionare hello corretto insieme di strutture, selezionare **utente** come hello **tipo di oggetto CS**e selezionare **persona** come hello **tipo di oggetto MV**. In **Link Type** (Tipo di collegamento) selezionare **Join** (Unisci). In **Precedence** (Precedenza) digitare un valore attualmente non usato da un'altra regola di sincronizzazione, ad esempio 99. È stato selezionato un valore di precedenza che è una precedenza più alta (inferiore) di una regola di sincronizzazione precedente hello. Ma che hai lasciato spazio anche in modo che è possibile aggiungere più regole filtro di sincronizzazione in un secondo momento, quando si desidera che la sincronizzazione di altri reparti toostart. Fare clic su **Avanti**.  
   ![Descrizione in ingresso 7](./media/active-directory-aadconnectsync-configure-filtering/inbound7.png)  
9. Lasciare vuoto **Scoping filter** e fare clic su **Next**. Un filtro vuoto indica che tale regola hello è oggetti tooall toobe applicato.
10. Lasciare hello **Join** regole vuota e quindi fare clic su **Avanti**.
11. Fare clic su **Aggiungi trasformazione**selezionare **costante** come hello **FlowType**e selezionare **cloudFiltered** come hello  **Attributo di destinazione**. In hello **origine** digitare **True**. Fare clic su **Aggiungi** regola hello toosave.  
    ![Trasformazione in ingresso 3](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)  
12. configurazione di hello toocomplete, è necessario toorun un **sincronizzazione completa**. Continuare a leggere la sezione hello [applica e verificare le modifiche](#apply-and-verify-changes).

Se si desidera, è possibile creare altre regole del primo tipo hello in cui si includono più oggetti sincronizzazione hello.

### <a name="outbound-filtering"></a>Filtri in uscita
In alcuni casi, è necessario toodo hello filtraggio solo dopo aver unito gli hello hello metaverse. Ad esempio, potrebbe essere necessario toolook all'attributo mail hello dalla foresta di risorse hello e attributo userPrincipalName hello dalla foresta di account hello, toodetermine se un oggetto deve essere sincronizzato. In questi casi, crei hello filtro nella regola in uscita hello.

In questo esempio, modificare hello filtro in modo che solo gli utenti che hanno sia posta elettronica che termina userPrincipalName @contoso.com sono sincronizzati:

1. Accedi toohello server che esegue la sincronizzazione di Azure AD Connect utilizzando un account che è un membro di hello **ADSyncAdmins** gruppo di sicurezza.
2. Avviare **Editor regole di sincronizzazione** da hello **avviare** menu.
3. In **Rules Type** (Tipo di regola) fare clic su **Outbound** (In uscita).
4. Regola di hello trova denominata **Out tooAAD – User Join**, fare clic su **modifica**.
5. Nel menu a comparsa hello, rispondere **Sì** toocreate una copia della regola hello.
6. In hello **descrizione** pagina, modificare **precedenza** tooan valore inutilizzato, ad esempio 50.
7. Fare clic su **definizione ambito filtro** hello navigazione a sinistra e quindi fare clic su **Aggiungi clausola**. In **Attribute** (Attributo) selezionare **mail**. In **Operator** (Operatore) selezionare **ENDSWITH** (TERMINACON). In **Value** (Valore) digitare **@contoso.com** e quindi fare clic su **Add clause** (Aggiungi clausola). In **Attribute** (Attributo) selezionare **userPrincipalName**. In **Operator** (Operatore) selezionare **ENDSWITH** (TERMINACON). In **Value** (Valore) digitare **@contoso.com**.
8. Fare clic su **Salva**.
9. configurazione di hello toocomplete, è necessario toorun un **sincronizzazione completa**. Continuare a leggere la sezione hello [applica e verificare le modifiche](#apply-and-verify-changes).

## <a name="apply-and-verify-changes"></a>Applicare e verificare le modifiche
Dopo aver apportato le modifiche di configurazione, è necessario applicare a tali oggetti toohello che sono già presenti nel sistema hello. È anche possibile che gli oggetti di hello che non sono attualmente nel motore di sincronizzazione hello devono essere elaborati (e il motore di sincronizzazione hello deve sistema di origine hello tooread tooverify nuovamente il relativo contenuto).

Se è stata modificata la configurazione hello utilizzando **dominio** o **unità organizzativa** filtro, è necessario toodo un **importazione completa**, seguito da **Delta sincronizzazione**.

Se è stata modificata la configurazione hello utilizzando **attributo** filtro, è necessario toodo un **completo sincronizzazione**.

Hello i passaggi seguenti:

1. Avviare **servizio di sincronizzazione** da hello **avviare** menu.
2. Selezionare **Connectors** (Connettori). In hello **connettori** selezionare hello connettore in cui è effettuato una modifica di configurazione in precedenza. In **Actions** (Azioni) selezionare **Run** (Esegui).  
   ![Esecuzione del connettore](./media/active-directory-aadconnectsync-configure-filtering/connectorrun.png)  
3. In **Run profiles**, selezionare l'operazione hello indicato nella sezione precedente hello. Se è necessario toorun due azioni, esecuzione hello hello secondo dopo la prima è stata completata. (hello **stato** colonna **Idle** per connettore hello selezionata.)

Dopo la sincronizzazione di hello, tutte le modifiche sono toobe staging esportato. Prima di apportare effettivamente le modifiche di hello in Azure AD, si desidera tooverify che tutte le modifiche siano corrette.

1. Avviare un prompt dei comandi e passare troppo`%Program Files%\Microsoft Azure AD Sync\bin`.
2. Eseguire `csexport "Name of Connector" %temp%\export.xml /f:x`.  
   nome Hello di hello connettore è servizio di sincronizzazione. Include un too"contoso.com simile nome-AAD" per Azure AD.
3. Eseguire `CSExportAnalyzer %temp%\export.xml > %temp%\export.csv`.
4. A questo punto si avrà un file denominato export.csv in %temp%, che può essere esaminato in Microsoft Excel. Questo file contiene tutte le modifiche di hello che stanno toobe esportato.
5. Apportare le modifiche necessarie hello toohello dati o di configurazione ed eseguire questi passaggi nuovamente (importazione, sincronizzazione e verifica) fino a quando hello modifiche che stanno toobe esportato sono quelle previste.

Al termine dell'operazione, esportare hello modifiche tooAzure Active Directory.

1. Selezionare **Connectors** (Connettori). In hello **connettori** selezionare hello Azure Active Directory Connector. In **Actions** (Azioni) selezionare **Run** (Esegui).
2. In **Run profiles** (Profili di esecuzione) selezionare **Export** (Esporta).
3. Se le modifiche di configurazione eliminano molti oggetti, viene visualizzato un errore nell'esportazione hello quando hello numero è maggiore del limite di hello configurato (per impostazione predefinita 500). Se viene visualizzato questo errore, quindi è necessario tootemporarily disable hello "[impedire eliminazioni accidentali](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" funzionalità.

Ora è dell'utilità di pianificazione di tempo tooenable hello nuovamente.

1. Avviare **utilità di pianificazione** da hello **avviare** menu.
2. Direttamente sotto **libreria utilità di pianificazione**, attività di ricerca hello denominata **Azure AD Sync Scheduler**, pulsante destro del mouse e selezionare **abilitare**.

## <a name="group-based-filtering"></a>Filtri basati sui gruppi
È possibile configurare in base al gruppo filtro hello prima volta che viene installato Azure AD Connect usando [installazione personalizzata](active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups). È progettato per una distribuzione pilota, in cui si desidera solo un piccolo set di oggetti toobe sincronizzato. Dopo essere stato disabilitato, il filtro basato su gruppi non può essere abilitato nuovamente. Ha *non supportato* toouse in base al gruppo filtro in una configurazione personalizzata. Ma è supportato solo tooconfigure questa funzionalità utilizzando Installazione guidata di hello. Dopo aver completato la distribuzione pilota, quindi utilizzare uno dei hello altre opzioni di filtro in questo argomento. Quando si usa filtro basato su unità Organizzativa in combinazione con l'applicazione di filtri basata su gruppo, è necessario inclusa hello OU dove si trovano gruppo hello e i relativi membri.

Quando si sincronizzano più foreste di AD, è possibile configurare i filtri basati sui gruppi specificando un gruppo diverso per ogni istanza di AD Connector. Se si desidera toosynchronize un utente in una foresta di Active Directory e hello stesso utente contiene uno o più corrispondente FSP (entità di protezione esterna) gli oggetti in altre foreste di Active Directory, è necessario verificare l'oggetto utente hello e tutti corrispondente oggetti FSP rientrano in base al gruppo ambito del filtro. Se uno o più oggetti FSP hello sono esclusi dal filtro in base al gruppo, oggetto utente hello non sarà sincronizzato tooAzure Active Directory.

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni sulla configurazione del [servizio di sincronizzazione Azure AD Connect](active-directory-aadconnectsync-whatis.md).
- Altre informazioni sull'[integrazione di identità locali con Azure AD](active-directory-aadconnect.md).
