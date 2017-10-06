---
title: Reimpostazione delle password self-service di Azure Ad con writeback delle password | Microsoft Docs
description: Utilizzo di Azure AD e Azure AD Connect toowriteback password tooon istanza locale di directory
services: active-directory
keywords: gestione delle password in Active Directory, gestione delle password, reimpostazione password self-service di Azure AD
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>Panoramica del writeback delle password

Writeback delle password consente che password toowrite tooconfigure Azure AD eseguire il tooyou Active Directory locale. Rimuove hello necessità tooset backup e gestire una soluzione di reimpostazione della password self-service locale complesso e fornisce un modo pratico basato su cloud per il tooreset agli utenti le proprie password locale ovunque si trovino. Il writeback delle password è un componente di [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) che può essere abilitato e usato dagli attuali sottoscrittori di [Edizioni di Azure Active Directory](active-directory-editions.md) Premium.

Writeback delle password fornisce hello seguenti caratteristiche

* **Nessun ritardo nei feedback**: il writeback delle password è un'operazione sincrona. Gli utenti ricevono una notifica immediatamente se la password non soddisfa i criteri o è stato in grado di non toobe reimpostate o modificate per qualsiasi motivo.
* **Supporta la reimpostazione delle password per gli utenti con ADFS o altre tecnologie di federazione** -con writeback delle password, purché hello gli account utente federato vengono sincronizzati nel tenant di Azure AD, sono in grado di toomanage relativi AD locale password dal cloud hello.
* **Supporta la reimpostazione delle password per gli utenti che utilizzano [sincronizzazione degli hash delle password](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  : quando il servizio di reimpostazione password hello rileva che un account utente sincronizzato è abilitato per la sincronizzazione degli hash delle password, è possibile reimpostare entrambi questo account in locale e cloud password contemporaneamente.
* **Supporta la modifica delle password da hello l'accesso pannello e Office 365** : quando federato o si password sincronizzata toochange forniti agli utenti le password scadute o non scadute, scrittura tali ambiente tooyour indietro AD locale delle password.
* **Supporta il writeback delle password quando un amministratore Reimposta da hello Azure portal** : ogni volta che un amministratore reimposta la password di un utente in hello [portale di Azure](https://portal.azure.com), se tale utente è federato o sincronizzata delle password, verrà impostata hello Consente di selezionare salve password nell'ambiente AD locale, nonché. Questo non è supportato nel portale di amministrazione di Office hello.
* **Locale applica criteri password di Active Directory** : quando un utente Reimposta la password, assicurarsi che vengano soddisfatti locale criteri Active Directory prima di averlo toothat directory. Sono inclusi cronologia, complessità, validità, filtri delle password e altre restrizioni per le password definite in AD locale.
* **Non richiede tutte le regole del firewall in entrata** -writeback della Password viene utilizzato un inoltro del Bus di servizio di Azure come canale di comunicazione sottostante, vale a dire che non si dispone tooopen porte in ingresso nel firewall per toowork questa funzionalità.
* **Non è supportato per gli account utente esistenti all'interno di gruppi protetti in Active Directory locale**: per altre informazioni sui gruppi protetti, vedere [Account protetti e gruppi in Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>Funzionamento del writeback delle password

Quando un hash federato o la password sincronizzata utente provenienti tooreset o cambiare la password nel cloud hello, si verifica hello segue:

1. Verifica toosee ha il tipo di password hello utente.
    * Se è possibile notare password hello è gestita in locale
        * Controlliamo se hello writeback servizio sia attivo e in esecuzione, questo caso, è consentire hello utente di continuare
        * Se il servizio di writeback hello non è attivo, dobbiamo utente hello che la password non può essere reimpostata ora
2. Successivamente, utente hello passa i controlli di autenticazione appropriato hello e raggiunge una schermata di hello la reimpostazione della password.
3. utente Hello seleziona una nuova password e per conferma.
4. Facendo clic su Invia password non crittografata hello è crittografare con una chiave simmetrica creato durante il processo di installazione di hello writeback.
5. Dopo la crittografia di password hello, abbiamo includerlo in un payload che viene inviato tramite un HTTPS canale tooyour specifico del tenant inoltro di service bus (che è inoltre configurati automaticamente durante il processo di installazione di hello writeback). L'inoltro è protetto da una password generata casualmente, nota solo all'installazione locale.
6. Una volta che il messaggio hello raggiunge il bus di servizio, hello endpoint di reimpostazione della password automaticamente attiva e rileva che una richiesta di reimpostazione in sospeso.
7. servizio Hello quindi Cerca utente hello in questione utilizzando l'attributo di ancoraggio cloud hello. Per questo toosucceed di ricerca:

    * l'oggetto utente Hello deve esistere in hello spazio connettore di Active Directory
    * l'oggetto utente Hello deve essere oggetto MV corrispondente toohello collegato
    * oggetto utente Hello deve essere collegato toohello corrispondente oggetto connettore di Azure ad.
    * Hello collegamento da tooMV oggetto connettore di Active Directory deve avere la regola di sincronizzazione hello `Microsoft.InfromADUserAccountEnabled.xxx` sul collegamento hello. <br> <br>
    Quando chiamata hello provenienti dal cloud hello, utilizza motore di sincronizzazione hello hello cloudAnchor attributo toolook backup oggetto spazio connettore AAD di hello segue hello collegamento back toohello MV oggetto e quindi segue toohello indietro AD oggetto collegamento di hello. Poiché è possibile che più oggetti di Active Directory (a più foreste) per hello stesso utente, il motore di sincronizzazione hello si basa su hello `Microsoft.InfromADUserAccountEnabled.xxx` hello toopick collegamento correggere uno.

    > [!Note]
    > In seguito a questa logica, Azure AD Connect deve essere in grado di toocommunicate con hello emulatore PDC per toowork di writeback delle password. Se è necessario tooenable manualmente questa operazione, è possibile connettere Azure AD Connect toohello emulatore PDC facendo clic su hello **proprietà** del connettore di sincronizzazione di Active Directory hello e quindi selezionando **configurare le partizioni di directory**. Da qui, cercare hello **impostazioni di connessione di controller di dominio** sezione e selezionare la casella di hello intitolata **utilizzare solo i controller di dominio preferito**. Anche se hello preferito che controller di dominio non è un emulatore PDC, Azure AD Connect tenterà tooconnect toohello PDC per il writeback delle password.

8. Una volta che viene trovato l'account utente di hello, si tenta di password hello tooreset direttamente nell'insieme di strutture Active Directory appropriato hello.
9. Se l'operazione di impostazione password hello ha esito positivo, si informa l'utente hello che è stata modificata la password.
    > [!NOTE]
    > In caso di hello alla password dell'utente hello viene sincronizzato tooAzure Active Directory con sincronizzazione password, è probabile che i criteri password locali di hello sono più deboli rispetto a criteri di password cloud hello. In questo caso, è comunque imporre è qualsiasi criterio locale hello e consentire invece password hash di hello toosynchronize sincronizzazione hash della password. In questo modo si garantisce che i criteri locali viene applicato nel cloud hello, indipendentemente dal fatto se si usa password sincronizzazione o la federazione tooprovide accesso single sign-on.

10. Se la password di hello impostato operazione ha esito negativo, si hello errore toohello utente e consentono di ripetere l'operazione.
    * Hello avrà esito negativo a causa delle operazioni seguenti hello
        * servizio Hello è stato premuto
        * password Hello che è selezionati non soddisfa i criteri dell'organizzazione
        * Non è stato trovato utente hello in hello AD locale

    Sono presenti uno specifico messaggio per molti di questi casi e informa l'utente di hello cosa si può fare problema hello tooresolve.

## <a name="configuring-password-writeback"></a>Configurazione del writeback delle password

È consigliabile utilizzare la funzionalità di aggiornamento automatico hello di [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) se si desidera che il writeback delle password toouse.

DirSync e Azure AD Sync non sono più supportate mezzo di articolo hello di writeback delle password di attivazione [l'aggiornamento da DirSync e Azure AD Sync](connect/active-directory-aadconnect-dirsync-deprecated.md) dispone di più informazioni toohelp con il passaggio.

Hello passaggi seguenti si presuppone che Azure AD Connect è già stato configurato nell'ambiente in uso tramite hello [Express](./connect/active-directory-aadconnect-get-started-express.md) o [personalizzato](./connect/active-directory-aadconnect-get-started-custom.md) impostazioni.

1. tooconfigure e abilitare il writeback della password Accedi tooyour Azure AD Connect server e avviare hello **Azure AD Connect** configurazione guidata.
2. Nella schermata iniziale di hello fare clic su **configura**.
3. In hello ulteriori attività dello schermo fare clic su **personalizzare le opzioni di sincronizzazione** e quindi scegliere **Avanti**.
4. Nella schermata di tooAzure AD Connect hello immettere credenziali di amministratore globale e scegliere **Avanti**.
5. Connettersi a un dominio e alle directory hello e unità Organizzativa schermate di filtro è possibile scegliere **Avanti**.
6. Nella schermata di funzionalità facoltative di hello casella di controllo hello accanto troppo**writeback delle Password** e fare clic su **Avanti**.
   ![Abilitare il writeback delle password in Azure AD Connect][Writeback]
7. Nella schermata di hello tooconfigure pronti, fare clic su **configura** e attendere toocomplete processo hello.
8. Quando si vede La configurazione è stata completata è possibile fare clic su **Esci**

## <a name="licensing-requirements-for-password-writeback"></a>Requisiti di licenza per il writeback delle password

Per informazioni sulla gestione delle licenze, vedere argomento hello [licenze necessarie per il writeback delle password](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) o hello seguenti siti

* [Sito sui prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Modalità di autenticazione locale supportate per il writeback delle password

Writeback delle password funziona per i seguenti tipi di password utente hello:

* **Utenti solo cloud**: il writeback delle password non si applica in questa situazione, perché non c'è una password locale
* **Utenti con sincronizzazione delle password**: il writeback delle password è supportato
* **Utenti federati**: il writeback delle password è supportato
* **Utenti con autenticazione pass-through**: il writeback delle password è supportato

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Attività di utenti e amministratori supportate per il writeback delle password

Le password vengono scritte in hello tutte le situazioni seguenti:

* **Attività degli utenti finali supportate**
  * Qualsiasi operazione self-service volontaria di modifica della password dell'utente finale
  * Qualsiasi operazione self-service forzata di modifica della password dell'utente finale, ad esempio in seguito a scadenza della password
  * Qualsiasi password self-service per l'utente finale reimpostazione provenienti da hello [portale di reimpostazione Password](https://passwordreset.microsoftonline.com)
* **Operazioni degli amministratori supportate**
  * Qualsiasi operazione self-service volontaria di modifica della password dell'amministratore
  * Qualsiasi operazione self-service forzata di modifica della password dell'amministratore, ad esempio in seguito a scadenza della password
  * Qualsiasi password self-service amministratore Reimposta provenienti da hello [portale di reimpostazione Password](https://passwordreset.microsoftonline.com)
  * Qualsiasi password avviata dall'amministratore dell'utente finale, reimpostare la password da hello [portale di Azure classico](https://manage.windowsazure.com)
  * Qualsiasi password avviata dall'amministratore dell'utente finale, reimpostare la password da hello [portale di Azure](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Attività di utenti e amministratori non supportate per il writeback delle password

Le password sono **non** scritta in uno qualsiasi dei hello seguenti situazioni:

* **Attività degli utenti finali non supportate**
  * Un utente di reimpostare le proprie password tramite PowerShell v1, v2 o hello API Azure AD Graph
* **Operazioni degli amministratori non supportate**
  * Qualsiasi password avviata dall'amministratore dell'utente finale, reimpostare la password da hello [il portale di gestione di Office](https://portal.office.com)
  * Reimpostare la password da PowerShell v1, v2, di qualsiasi password avviata dall'amministratore dell'utente finale o hello API Azure AD Graph

Mentre è in corso tooremove queste limitazioni, tempi che possiamo condividere ancora non si dispone.

## <a name="password-writeback-security-model"></a>Modello di sicurezza del writeback delle password

Il writeback delle password è un servizio altamente sicuro.  tooensure che le informazioni sono protette, si abilita un modello di sicurezza a 4 livelli descritta di seguito.

* **Inoltro del bus di servizio specifico del tenant**
  * Quando si configura il servizio di hello, sono stati impostati un inoltro del bus di servizio specifico del tenant protetta da una password complessa generata in modo casuale che Microsoft non ha accesso a.
* **Chiave di crittografia bloccata e crittograficamente complessa per le password**
  * Dopo la creazione di inoltro del bus di servizio hello è creare una chiave simmetrica avanzata è possibile usare password hello tooencrypt come proviene rete hello. Questa chiave è disponibile solo nell'archivio segreto della società cloud hello, che è bloccato e controllare, proprio come le password nella directory hello frequentemente.
* **TLS standard di settore**
  1. Quando una password, reimpostare o modificare operazione avviene in cloud hello, abbiamo richiedere password crittografato hello e crittografarla con la chiave pubblica.
  2. Che è quindi inserire in un messaggio HTTPS, che viene inviato tramite un canale crittografato usando l'inoltro del bus di servizio tooyour con certificati SSL di Microsoft.
  3. Dopo il messaggio hello arriva nel Bus di servizio, l'agente locale viene riattivato backup ed esegue l'autenticazione tramite Bus tooService hello password complessa generata in precedenza.
  4. L'agente locale preleva messaggio crittografato hello, li decrittografa usando la chiave privata hello che è generati.
  5. L'agente locale tenta quindi di password hello tooset tramite hello API SetPassword di AD DS.
     * Questo passaggio è ciò che consentono di tooenforce di Active Directory locale criteri password (complessità, durata, cronologia, i filtri e così via) nel cloud hello.
* **Criteri di scadenza del messaggio** 
  * Se il messaggio hello si trova nel Bus di servizio perché il servizio locale non è attivo, si verificherà il timeout e rimosso dopo diversi minuti tooincrease ulteriormente la protezione.

### <a name="password-writeback-encryption-details"></a>Informazioni dettagliate sulla crittografia del writeback delle password

passaggi di crittografia Hello attraversa una richiesta di reimpostazione password dopo l'invio, prima che arrivi nell'ambiente locale, tooensure massima affidabilità del servizio e sicurezza sono descritti di seguito.

* **Passaggio 1: la crittografia delle Password con una chiave RSA a 2048 bit** : una volta che un utente invia un toobe password riscritti tooon locale, prima di tutto, hello inviato stessa password viene crittografato con una chiave RSA a 2048 bit.
* **Passaggio 2: crittografia a livello di pacchetto con AES-GCM** - quindi hello intero pacchetto (password + i metadati necessari) viene crittografato con AES-GCM. Ciò impedisce che chiunque disponga di canale sottostante bus di servizio di accesso diretto toohello visualizzazione/alterazione hello contenuto.
* **Passaggio 3 - tutte le comunicazioni si verificano su TLS / SSL** -tutte le comunicazioni hello con bus di servizio viene eseguito in un canale SSL/TLS. Consente di proteggere il contenuto di hello di parti 3rd non autorizzate.
* **Rollover della chiave automatico ogni sei mesi** - automaticamente ogni 6 mesi, o ogni volta che il writeback delle password è disabilitato o nuovamente abilitata in Azure AD Connect, abbiamo rollover tutti questi tasti tooensure servizio massimo sulla sicurezza e protezione.

### <a name="password-writeback-bandwidth-usage"></a>Utilizzo della larghezza di banda per il writeback delle password

Writeback delle password è un servizio di larghezza di banda ridotta che invia le richieste di eseguire il backup agente locale toohello solo in hello seguenti circostanze:

1. Due messaggi inviati per l'attivazione o disattivazione delle funzionalità hello tramite Azure AD Connect.
2. Un messaggio viene inviato una volta ogni cinque minuti come un heartbeat del servizio per purché hello servizio è in esecuzione.
3. Vengono inviati due messaggi ogni volta che viene inviata una nuova password
    * Primo messaggio, come un'operazione di hello tooperform richiesta
    * Secondo messaggio, che contiene il risultato di hello dell'operazione hello e viene inviato in hello seguenti circostanze:
        * Ogni volta che viene inviata una nuova password durante la reimpostazione self-service della password utente.
        * Ogni volta che viene inviata una nuova password durante un'operazione di modifica della password utente.
        * Ogni volta che una nuova password viene inviata durante un'avviata dall'amministratore la reimpostazione delle password (da portali solo di hello Azure amministratore).

#### <a name="message-size-and-bandwidth-considerations"></a>Considerazioni sulle dimensioni dei messaggi e sulla larghezza di banda

dimensioni di Hello di ogni messaggio hello descritto in precedenza sono in genere inferiori a 1 kb, anche carichi estremi, servizio di writeback della password hello stesso utilizza alcuni kilobit al secondo di larghezza di banda. Poiché ogni messaggio viene inviato in tempo reale, solo quando richiesto da un'operazione di aggiornamento della password, e poiché la dimensione dei messaggi hello per le sue dimensioni, utilizzo della larghezza di banda hello di funzionalità di writeback hello in modo efficace è troppo piccolo toohave alcun impatto reale misurabile.

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Domande frequenti**](active-directory-passwords-faq.md) - Come Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Abilitare il writeback delle password in Azure AD Connect"
