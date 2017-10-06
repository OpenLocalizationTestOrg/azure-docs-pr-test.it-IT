---
title: 'Servizio di sincronizzazione Azure AD Connect: apportare modifiche alla configurazione nel servizio di sincronizzazione Azure AD Connect | Documentazione Microsoft'
description: "Viene illustrata la modalità di sincronizzazione una toohello modificare la configurazione in Azure AD Connect di toomake."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 78e96d9166831a668439c2b8aa6a0022bc472da4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomake-a-change-toohello-default-configuration"></a>Sincronizzazione di Azure AD Connect: toomake toohello una modifica la modalità di configurazione predefinite
Hello in questo argomento viene toowalk tramite come toomake cambia toohello di configurazione predefinita della sincronizzazione di Azure AD Connect. Include i passaggi per alcuni scenari comuni. Con queste informazioni, è necessario essere in grado di toomake tooyour alcune semplici modifiche proprietari configurazione basata su regole di business.

## <a name="synchronization-rules-editor"></a>Editor regole di sincronizzazione
Hello Editor regole di sincronizzazione è una configurazione predefinita hello toosee e modifica. È possibile trovarlo in hello Menu Start in hello **Azure AD Connect** gruppo.  
![Menu Start con l'editor delle regole di sincronizzazione](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)

Quando viene aperto, vedrai regole di hello predefinite out-of-box.

![Editor delle regole di sincronizzazione](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-hello-editor"></a>Spostarsi nell'editor di hello
Hello elenchi a discesa nella parte superiore di hello dell'editor di hello consentono di trovare tooquickly una particolare regola. Ad esempio, se si desidera regole hello toosee dove hello attributo proxyAddresses è incluso, modificate seguente toohello elenchi a discesa di hello:  
![Filtro nell'editor delle regole di sincronizzazione](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)  
filtro tooreset e caricamento di una configurazione aggiornata, premere **F5** tastiera hello.

toohello alto a destra, si dispone di un pulsante **Aggiungi nuova regola**. Questo pulsante viene utilizzato toocreate la propria regola personalizzata.

Nella parte inferiore di hello, si dispone di pulsanti per agire su una regola di sincronizzazione selezionato. I pulsanti **Edit** (Modifica) e **Delete** (Elimina) eseguono le operazioni previste. **Esportare** produce uno script di PowerShell per ricreare la regola di sincronizzazione hello. Questa procedura consente di una regola di sincronizzazione da un server tooanother toomove.

## <a name="create-your-first-custom-rule"></a>Creare la prima regola personalizzata
la modifica più comune di Hello è modifiche toohello flussi di attributi. dati Hello nella directory di origine potrebbero non essere in Azure AD. Nell'esempio hello in questa sezione, si desidera toomake hello specificato nome di un utente sia sempre in **corretto**.

### <a name="disable-hello-scheduler"></a>Disabilitare l'utilità di pianificazione hello
Hello [dell'utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md) viene eseguito ogni 30 minuti per impostazione predefinita. Si desidera toomake che non viene avviato quando si apportano modifiche e le nuove regole di risoluzione dei problemi. tootemporarily disabiliti hello, avviare PowerShell ed eseguire`Set-ADSyncScheduler -SyncCycleEnabled $false`

![Disabilitare l'utilità di pianificazione hello](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-hello-rule"></a>Creare una regola di hello
1. Fare clic su **Add new rule**(Aggiungi nuova regola).
2. In hello **descrizione** pagina immettere hello informazioni seguenti:  
   ![Filtro delle regole in ingresso](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)  
   * Nome: Assegnare un nome descrittivo di regola di hello.
   * Descrizione: Spiegazioni in modo da un altro utente possa comprendere quali regola hello sono per.
   * Sistema connesso: oggetto di hello sistema hello è reperibile. In questo caso, selezionare hello Active Directory Connector.
   * Connected System/Metaverse Object Type: (Tipo di oggetto sistema connesso/Tipo di oggetto metaverse) selezionare rispettivamente **User** (Utente) e **Person** (Persona).
   * Tipo di collegamento: Modificare questo valore troppo**Join**.
   * La precedenza: Fornire un valore univoco nel sistema hello. Un valore numerico inferiore indica una precedenza maggiore.
   * Tag: lasciare vuoto. È necessario popolare questa casella con un valore solo per le regole predefinite di Microsoft.
3. In hello **definizione ambito filtro** pagina, immettere **givenName ISNOTNULL**.  
   ![Filtro dell'ambito per le regole in ingresso](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)  
   In questa sezione viene utilizzato toodefine dovrà essere applicata la regola di hello oggetti. Se lasciato vuoto, la regola hello verrà applicata oggetti utente tooall. ma includerà sale riunioni, account del servizio e altri oggetti utente non di persone.
4. In hello **regole di unione**, lasciare vuoto il campo.
5. In hello **trasformazioni** pagina, modificare troppo hello FlowType**espressione**. Attributo di destinazione di hello seleziona **givenName**e nell'origine immettere `PCase([givenName])`.
   ![Trasformazioni di regole in ingresso](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)  
   il motore di sincronizzazione Hello è sia nel nome della funzione hello e nome hello dell'attributo hello tra maiuscole e minuscole. Se si digita errati, viene visualizzato un avviso quando si aggiunge la regola hello. editor Hello consente toosave e continuare, pertanto è regola hello tooreopen e regola hello corretto.
6. Fare clic su **Aggiungi** regola hello toosave.

La nuova regola personalizzata deve essere visibile con hello altre regole di sincronizzazione nel sistema hello.

### <a name="verify-hello-change"></a>Verificare la modifica hello
Con questa nuova modifica, si desidera toomake che funzioni come previsto e non genera errori. In base al numero hello di oggetti che presenti, sono disponibili due modi diversi toodo questo passaggio.

1. Eseguire una sincronizzazione completa in tutti gli oggetti
2. Eseguire un'anteprima e una sincronizzazione completa in un singolo oggetto

Avviare **servizio di sincronizzazione** dal menu di avvio hello. passaggi di Hello in questa sezione sono tutti in questo strumento.

1. **Sincronizzazione completa in tutti gli oggetti**  
   Selezionare **connettori** nella parte superiore di hello. Identificare hello connettore apportata una modifica tooin hello delle sezioni precedenti, in questo caso hello servizi di dominio Active Directory e selezionarlo. Selezionare **Run** (Esegui) in Actions (Azioni), selezionare **Full Synchronization** (Sincronizzazione completa) e quindi fare clic su **OK**.
   ![Sincronizzazione completa](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)  
   oggetti Hello vengono ora aggiornati hello Metaverse. Ora è toolook oggetto hello hello Metaverse.
2. **Anteprima e sincronizzazione completa in un singolo oggetto**  
   Selezionare **connettori** nella parte superiore di hello. Identificare hello connettore apportata una modifica tooin hello delle sezioni precedenti, in questo caso hello servizi di dominio Active Directory e selezionarlo. Selezionare **Search Connector Space**(Cerca spazio connettore). Utilizzare l'ambito toofind un oggetto a cui si desidera toouse tootest hello modifica. Selezionare l'oggetto hello e fare clic su **anteprima**. Nella schermata nuova hello selezionare **anteprima Commit**.  
   ![Commit preview](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)  
   modifica di Hello è eseguito il commit toohello metaverse.

**Esaminare hello oggetto Metaverse hello**  
Ora è toopick che alcuni oggetti toomake che hello valore di esempio è previsto e applicare tale regola hello. Selezionare **ricerca Metaverse** dall'alto hello. Aggiungere i filtri sono necessari oggetti pertinenti di toofind hello. Risultati della ricerca hello, aprire un oggetto. Esaminare i valori di attributo hello e anche verificare in hello **regole di sincronizzazione** colonna hello regola applicata come previsto.  
![Ricerca metaverse](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)  

### <a name="enable-hello-scheduler"></a>Abilita utilità di pianificazione hello
Se tutto è come previsto, è possibile abilitare nuovamente l'utilità di pianificazione hello. In PowerShell eseguire `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="other-common-attribute-flow-changes"></a>Altre modifiche comuni del flusso dell'attributo
la sezione precedente di Hello descritte come toomake cambia tooan flusso dell'attributo. In questa sezione vengono forniti alcuni esempi aggiuntivi. passaggi di Hello per la regola di sincronizzazione toocreate hello è abbreviato, ma è possibile trovare passaggi completi hello nella sezione precedente di hello.

### <a name="use-another-attribute-than-hello-default"></a>Utilizzare un altro attributo rispetto al valore predefinito di hello
Fabrikam, è presente una foresta in cui alfabeto locale hello viene utilizzato per nome, cognome e nome visualizzato. rappresentazione di caratteri latini di questi attributi Hello è reperibile in attributi di estensione hello. Quando si compila l'elenco indirizzi globale hello in Azure AD e Office 365, hello organizzazione vuole che questi toobe attributi utilizzato.

Con una configurazione predefinita, un oggetto dall'insieme di strutture locale hello simile al seguente:  
![Flusso dell'attributo 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

una regola con altri flussi di attributi, toocreate hello seguenti:

* Avviare **Editor regole di sincronizzazione** dal menu di avvio hello.
* Con **in ingresso** toohello ancora selezionato a sinistra, fare clic su pulsante hello **Aggiungi nuova regola**.
* Assegnare regola hello un nome e una descrizione. Selezionare hello locali Active Directory e hello tipi di oggetto pertinente. In **Link Type** (Tipo di collegamento) selezionare **Join** (Unisci). Per la precedenza scegliere un numero non usato da un'altra regola. le regole di out-of-box Hello iniziano con 100, pertanto il valore di hello 50 può essere utilizzato in questo esempio.
  ![Flusso dell'attributo 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)
* Lasciare vuota l'ambito (vale a dire, applicare gli oggetti utente tooall nella foresta hello).
* Lasciare regole di unione vuote (che è, consentono di hello handle out-of-box regola tutti i join).
* Nelle trasformazioni, creare hello flussi seguente:  
  ![Flusso dell'attributo 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* Fare clic su **Aggiungi** regola hello toosave.
* Andare troppo**Synchronization Service Manager**. In **connettori**, selezionare hello in cui viene aggiunta regola hello del connettore. Selezionare **Run** (Esegui) e **Full Synchronization** (Sincronizzazione completa). Una sincronizzazione completa ricalcola tutti gli oggetti utilizzando le regole correnti hello.

Questo è il risultato di hello di hello stesso oggetto con la regola personalizzata:  
![Flusso dell'attributo 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a>Lunghezza degli attributi
Gli attributi di stringa sono da toobe set predefinito indicizzabili e la lunghezza massima di hello è 448 caratteri. Se si lavora con gli attributi di stringa che potrebbero contenere più, quindi rendere seguente hello tooinclude che nel flusso di attributi hello:  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-hello-userprincipalsuffix"></a>La modifica di userPrincipalSuffix hello
attributo userPrincipalName Hello in Active Directory non è sempre noto agli utenti di hello e potrebbe non essere adatto come hello ID di accesso. Hello Azure AD Connect, installazione guidata di sincronizzazione consente di scegliere un attributo diverso, ad esempio posta elettronica. Ma in alcuni hello casi deve essere calcolato l'attributo. Ad esempio, hello società Contoso dispone di due directory di Azure AD, uno per la produzione e uno per il testing. Desiderano utenti hello in dei test tenant toouse un altro suffisso in hello ID di accesso.  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

In questa espressione, prendere tutti gli elementi a sinistra di hello innanzitutto @-sign (Word) e concatena con una stringa fissa.

### <a name="convert-a-multi-value-tooa-single-value"></a>Convertire un valore singolo tooa multivalore
Alcuni attributi in Active Directory sono multivalore nello schema hello anche se compaiono come singole con valori di Active Directory Users and Computers. Un esempio è l'attributo di descrizione hello.  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

In questa espressione nel caso in cui hello e presenta un valore, richiedere hello primo elemento () nell'attributo hello, rimuovere iniziali e finali (Trim) e quindi mantenere hello primi 448 caratteri (Left) nella stringa hello.

### <a name="do-not-flow-an-attribute"></a>Non trasmettere un attributo
Per informazioni generali su scenario hello per questa sezione, vedere [controllo processo del flusso di attributo hello](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process).

Esistono due modi toonot flusso di un attributo. Hello prima disponibile in Installazione guidata di hello ed è troppo[rimuovere gli attributi selezionati](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering). Questa opzione funziona se non si è mai sincronizzate attributo hello prima. Tuttavia, se sono stati avviati toosynchronize questo attributo e rimuoverlo in seguito a questa funzionalità, il motore di sincronizzazione hello interrompe la gestione di attributo hello e i valori esistenti di hello vengono lasciati in Azure AD.

Se si desidera tooremove hello valore di un attributo e assicurarsi che non si trasmette in hello futuro, è necessario creare una regola personalizzata.

Fabrikam, abbiamo abbiamo capito che alcuni attributi si sincronizza toohello cloud hello non deve essere presente. Vogliamo toomake che questi attributi vengono rimossi da Azure AD.  
![Attributi di estensione non validi](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* Creare una nuova regola di sincronizzazione in ingresso e popolare la descrizione hello ![descrizioni](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)
* Creare flussi di attributi di tipo **espressione** e con origine hello **AuthoritativeNull**. valore letterale Hello **AuthoritativeNull** indica che il valore di hello deve essere vuoto in hello MV anche se una regola di sincronizzazione di precedenza inferiore tenta valore hello toopopulate.
  ![Trasformazione per gli attributi di estensione](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)
* Salvare hello regola di sincronizzazione. Avviare **servizio di sincronizzazione**, trovare hello connettore, selezionare **eseguire**, e **sincronizzazione completa**. Questo passaggio consente di ricalcolare tutti i flussi degli attributi.
* Verificare che hello destinato modifiche stanno toobe esportato eseguendo una ricerca di spazio connettore hello.
  ![Eliminazione di gestione temporanea](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)

## <a name="create-rules-with-powershell"></a>Creare regole con PowerShell
Uso dell'editor regole di sincronizzazione hello funziona correttamente quando si dispone solo di alcune modifiche toomake. Se è necessario toomake numerose modifiche, PowerShell potrebbe essere un'opzione migliore. Alcune funzionalità avanzate sono disponibili solo con PowerShell.

### <a name="get-hello-powershell-script-for-an-out-of-box-rule"></a>Ottenere uno script di PowerShell hello per una regola di out-of-box
hello toosee script di PowerShell che ha creato una regola out-of-box, una regola di selezione hello nella sincronizzazione hello regole editor e fare clic su **esportare**. In questo modo di azione hello PowerShell script tale regola hello creato.

### <a name="advanced-precedence"></a>Precedenza avanzata
regole di sincronizzazione di out-of-box Hello iniziano con un valore di priorità pari a 100. Se si dispone di molti insiemi di strutture ed è necessario toomake molte modifiche personalizzate, quindi le regole di sincronizzazione 99 potrebbero non essere sufficiente.

È possibile indicare hello motore di sincronizzazione che si desidera regole aggiuntive inserite prima delle regole di hello out-of-box. tooget questo comportamento, seguire questi passaggi:

1. Regola di sincronizzazione di out-of-box prima di contrassegnare hello (questa regola è hello **In dall'utente di Active Directory Join**) in editor regole di sincronizzazione hello e selezionare **esportare**. Copiare il valore di identificatore SR hello.  
![PowerShell prima della modifica](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)  
2. Creare una nuova regola di sincronizzazione hello. È possibile utilizzare hello sincronizzazione regola editor toocreate è. Esportare uno script di PowerShell tooa hello regola.
3. Nella proprietà hello **PrecedenceBefore**, inserire il valore di identificatore hello dalla regola out-of-box hello. Set hello **precedenza** troppo**0**. Verificare che l'attributo dell'identificatore hello è univoco e non si riutilizza un GUID da un'altra regola. Assicurarsi inoltre che tale hello **ImmutableTag** non è impostata, questa proprietà deve essere impostata solo per una regola di out-of-box. Salvare uno script di PowerShell hello ed eseguirlo. il risultato di Hello è che la regola personalizzata viene assegnata il valore di precedenza hello pari a 100 e vengono incrementati tutte le altre regole out-of-box.  
![PowerShell dopo la modifica](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)  

È possibile avere molte regole di sincronizzazione personalizzate utilizzando hello stesso **PrecedenceBefore** valore quando necessario.


## <a name="enable-synchronization-of-preferreddatalocation"></a>Abilitare la sincronizzazione di PreferredDataLocation
Azure AD Connect supporta la sincronizzazione di hello **PreferredDataLocation** attributo per **utente** oggetti nella versione 1.1.524.0 e dopo. In particolare, sono state introdotte le seguenti modifiche:

* schema di Hello hello del tipo di oggetto **utente** in hello Azure Active Directory Connector è stata estesa tooinclude PreferredDataLocation attributo, che è a valore singolo ed è di tipo stringa.

* schema di Hello hello del tipo di oggetto **persona** in hello Metaverse viene esteso tooinclude PreferredDataLocation attributo, che è a valore singolo ed è di tipo stringa.

Per impostazione predefinita, i hello PreferredDataLocation attributo non è abilitato per la sincronizzazione perché non esiste alcun attributo di PreferredDataLocation corrispondente in Active Directory locale. È necessario abilitare la sincronizzazione manualmente.

> [!IMPORTANT]
> Attualmente, Azure AD consente l'attributo PreferredDataLocation hello sia sincronizzato oggetti utente e cloud toobe oggetti utente configurate direttamente con Azure AD PowerShell. Dopo aver abilitato la sincronizzazione dell'attributo PreferredDataLocation hello, è necessario arrestare tramite Azure AD PowerShell tooconfigure hello attributo su **sincronizzati gli oggetti utente** come Azure AD Connect verrà eseguirne l'override in base a valori di attributo origine Hello in Active Directory locale.

> [!IMPORTANT]
> In 2017 1 settembre, Azure AD non consentirà più attributo PreferredDataLocation hello in **sincronizzati gli oggetti utente** toobe configurate direttamente con Azure AD PowerShell. attributo PreferredLocation tooconfigure sincronizzati gli oggetti utente, è necessario utilizzare Azure AD Connect solo.

Prima di abilitare la sincronizzazione dell'attributo PreferredDataLocation hello, è necessario:

 * Prima di tutto, decidere quale toobe attributi di Active Directory locale utilizzato come attributo di origine hello. Questo deve essere di tipo **stringa** e **a valore singolo**.

 * Se è stata configurata in precedenza attributo PreferredDataLocation hello in esistenti sincronizzati gli oggetti utente di Azure AD usando Azure AD PowerShell, è necessario **backport** oggetti utente corrispondenti toohello i valori dell'attributo hello in Active Directory locale.
 
    > [!IMPORTANT]
    > In caso contrario non backport hello attributo valori toohello gli oggetti utente corrispondenti in Active Directory locale, Azure AD Connect rimuoverà i valori dell'attributo esistenti hello in Azure AD della sincronizzazione per l'attributo PreferredDataLocation hello abilitata.

 * È consigliabile configurare l'attributo di origine hello in almeno un paio di on-premise utente di Active Directory gli oggetti a questo punto, che può essere usato per la verifica in un secondo momento.
 
sincronizzazione di tooenable Hello passaggi dell'attributo PreferredDataLocation hello può essere riepilogata come:

1. Disabilitare l'utilità di pianificazione della sincronizzazione e verificare che non ci sia alcuna sincronizzazione in corso

2. Aggiungere hello origine attributo toohello Active Directory Connector locale dello schema

3. Aggiungere lo schema di PreferredDataLocation toohello connettore Azure AD

4. Creare un valore di attributo hello tooflow regola di sincronizzazione in ingresso da Active Directory locale

5. Creare un tooAzure valore relativo a sincronizzazione in uscita regola tooflow hello attributo Active Directory

6. Eseguire un ciclo di sincronizzazione completo

7. Abilitare l'utilità di pianificazione della sincronizzazione

> [!NOTE]
> resto Hello di questa sezione vengono illustrati tali passaggi nei dettagli. Vengono descritte nel contesto di hello di una distribuzione di Azure AD con topologia a foresta singola e senza regole di sincronizzazione. Se si dispone della topologia a più foreste, le regole di sincronizzazione personalizzato configurato o dispone di un server di gestione temporanea, è necessario passaggi hello tooadjust di conseguenza.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Passaggio 1: Disabilitare l'utilità di pianificazione della sincronizzazione e verificare che non ci sia alcuna sincronizzazione in corso
Verificare che viene eseguita alcuna sincronizzazione mentre si è al centro hello dell'aggiornamento di sincronizzazione regole tooavoid impreviste cambia being esportato tooAzure AD. toodisable hello sincronizzazione predefinite dell'utilità di pianificazione:

 1. Avviare una sessione di PowerShell nel server di Azure AD Connect hello.

 2. Disabilitare la sincronizzazione pianificata eseguendo di cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $false`
 
 3. Avviare hello **Synchronization Service Manager** da passare → tooSTART servizio di sincronizzazione.
 
 4. Passare toohello **operazioni** scheda e verificare che nessuna operazione il cui stato è *"in"corso.*

![Synchronization Service Manager: verificare che non ci siano operazioni in corso](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-hello-source-attribute-toohello-on-premises-ad-connector-schema"></a>Passaggio 2: Aggiungere hello origine attributo toohello Active Directory Connector locale dello schema
Non tutti gli attributi di Active Directory vengono importati in hello spazio connettore di Active Directory in locale. elenco tooadd hello origine attributo toohello di hello importati attributi:

 1. Passare toohello **connettori** scheda hello Synchronization Service Manager.
 
 2. Fare clic su hello **connettore di Active Directory locale** e selezionare **proprietà**.
 
 3. Nella finestra di dialogo popup hello, passare toohello **selezione attributi** scheda.
 
 4. Verificare che l'attributo di origine hello sia selezionata nell'elenco di attributi hello.
 
 5. Fare clic su **OK** toosave.

![Aggiungere l'attributo di origine tooon locale dello schema di Active Directory Connector](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-toohello-azure-ad-connector-schema"></a>Passaggio 3: Aggiungere dello schema di PreferredDataLocation toohello connettore Azure AD
Per impostazione predefinita, viene importato in Azure AD Connect spazio hello non attributo PreferredDataLocation hello. tooadd hello PreferredDataLocation attributo toohello elenco attributi importati:

 1. Passare toohello **connettori** scheda hello Synchronization Service Manager.

 2. Fare clic su hello **connettore Azure AD** e selezionare **proprietà**.

 3. Nella finestra di dialogo popup hello, passare toohello **selezione attributi** scheda.

 4. Assicurarsi che l'attributo PreferredDataLocation hello sia selezionata nell'elenco di attributi hello.

 5. Fare clic su **OK** toosave.

![Aggiungere l'attributo di origine tooAzure dello schema di Active Directory Connector](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-tooflow-hello-attribute-value-from-on-premises-active-directory"></a>Passaggio 4: Creare un valore di attributo hello tooflow regola di sincronizzazione in ingresso da Active Directory locale
regola di sincronizzazione in entrata Hello consente tooflow valore di attributo hello dall'attributo di origine hello da toohello di Active Directory locale Metaverse:

1. Avviare hello **Editor regole di sincronizzazione** da passare tooSTART → Editor regole di sincronizzazione.

2. Filtro di ricerca hello set **direzione** toobe **in ingresso**.

3. Fare clic su **Aggiungi nuova regola** pulsante toocreate una nuova regola in ingresso.

4. In hello **descrizione** scheda, fornire hello seguente configurazione:
 
    | Attributo | Valore | Dettagli |
    | --- | --- | --- |
    | Nome | *Specificare un nome* | Ad esempio, *"In entrata da AD - Utente PreferredDataLocation"* |
    | Descrizione | *Inserire una descrizione* |  |
    | Connected System | *Selezionare hello locale Active Directory connector* |  |
    | Connected System Object Type | **Utente** |  |
    | Metaverse Object Type | **Person** |  |
    | Tipo di collegamento | **Join** |  |
    | Precedenza | *Scegliere un numero compreso tra 1 e 99* | I numeri compresi tra 1 e 99 sono riservati alle regole di sincronizzazione personalizzate. Non scegliere un valore usato da un'altra regola di sincronizzazione. |

5. Passare toohello **definizione ambito filtro** scheda e aggiungere un **singolo gruppo di filtri ambito con hello seguente clausola**:
 
    | Attributo | operatore | Valore |
    | --- | --- | --- |
    | adminDescription | NOTSTARTWITH | Utente\_ | 
 
    L'ambito del filtro determina a quali oggetti di AD locale viene applicata la regola di sincronizzazione in entrata. In questo esempio, si usa hello stesso filtro di ambito utilizzato come *"In from AD – utente comune"* regola di sincronizzazione fuori banda, il che impedisce la regola di sincronizzazione hello applicati gli oggetti tooUser creati tramite il writeback di utenti di Azure AD funzionalità. Potrebbe essere necessario filtro di ambito hello tootweak in base tooyour distribuzione di Azure AD Connect.

6. Passare toohello **scheda trasformazione** e implementare hello seguente regola di trasformazione:
 
    | Flow Type | Target Attribute | Sorgente | Applicare una sola volta | Tipi di unione |
    | --- | --- | --- | --- | --- |
    | Diretto | PreferredDataLocation | Selezionare l'attributo di origine hello | Non selezionato | Aggiornare |

7. Fare clic su **Aggiungi** toocreate regola in ingresso di hello.

![Creare una regola di sincronizzazione in ingresso](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-tooflow-hello-attribute-value-tooazure-ad"></a>Passaggio 5: Creare un tooAzure valore relativo a sincronizzazione in uscita regola tooflow hello attributo Active Directory
regola di sincronizzazione in uscita Hello consente tooflow valore di attributo hello dall'attributo PreferredDataLocation toohello Metaverse di hello in Azure AD:

1. Passare toohello **regole di sincronizzazione** Editor.

2. Filtro di ricerca hello set **direzione** toobe **in uscita**.

3. Fare clic sul pulsante **Aggiungi nuova regola**.

4. In hello **descrizione** scheda, fornire hello seguente configurazione:

    | Attributo | Valore | Dettagli |
    | --- | --- | --- |
    | Nome | *Specificare un nome* | Ad esempio, "Out tooAAD – PreferredDataLocation utente" |
    | Descrizione | *Inserire una descrizione* |
    | Connected System | *Selezionare il connettore di Azure ad hello* |
    | Connected System Object Type | Utente ||
    | Metaverse Object Type | **Person** ||
    | Tipo di collegamento | **Join** ||
    | Precedenza | *Scegliere un numero compreso tra 1 e 99* | I numeri compresi tra 1 e 99 sono riservati alle regole di sincronizzazione personalizzate. Non scegliere un valore usato da un'altra regola di sincronizzazione. |

5. Passare toohello **definizione ambito filtro** scheda e aggiungere un **singolo gruppo di filtri ambito con due clausole**:
 
    | Attributo | operatore | Valore |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | Utente |
    | cloudMastered | NOTEQUAL | True  |

    L'ambito del filtro determina a quali oggetti di Azure AD viene applicata la regola di sincronizzazione in uscita. In questo esempio, si usa hello stesso filtro di ambito da "Out tooAD: identità dell'utente" regola di sincronizzazione fuori banda. Impedisce la regola di sincronizzazione hello tooUser applicati oggetti che non sono sincronizzati da Active Directory locale. Potrebbe essere necessario filtro di ambito hello tootweak in base tooyour distribuzione di Azure AD Connect.
    
6. Passare toohello **trasformazione** scheda e implementare hello seguente regola di trasformazione:

    | Flow Type | Target Attribute | Sorgente | Applicare una sola volta | Tipi di unione |
    | --- | --- | --- | --- | --- |
    | Diretto | PreferredDataLocation | PreferredDataLocation | Non selezionato | Aggiornare |

7. Chiudi **Aggiungi** regola in uscita di toocreate hello.

![Creare una regola di sincronizzazione in uscita](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a>Passaggio 6: Eseguire un ciclo di sincronizzazione completo
In generale, il ciclo di sincronizzazione completa è necessario perché abbiamo aggiunto hello tooboth di nuovi attributi Active Directory e lo schema di Azure Active Directory Connector e introdotto regole di sincronizzazione. È consigliabile verificare le modifiche di hello prima esportandoli tooAzure Active Directory. È possibile utilizzare hello dopo le modifiche di hello tooverify passaggi durante l'esecuzione manuale di passaggi di hello che costituiscono un ciclo di sincronizzazione completa. 

1. Eseguire **importazione completa** passaggio su hello **connettore di Active Directory locale**:

   1. Passare toohello **operazioni** scheda hello Synchronization Service Manager.

   2. Fare clic su hello **connettore di Active Directory locale** e selezionare **Esegui...**

   3. Nella finestra di dialogo popup hello, selezionare **importazione completa** e fare clic su **OK**.
    
   4. Attendere che l'operazione toocomplete.

    > [!NOTE]
    > È possibile ignorare l'importazione completa su hello locale Active Directory Connector se l'attributo di origine hello è già incluso nell'elenco di hello di attributi importati. In altre parole, non è stato toomake qualsiasi modifica durante [passaggio 2: aggiungere hello origine attributo toohello locale connettore di Active Directory schema](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema).

2. Eseguire **importazione completa** passaggio su hello **connettore Azure AD**:

   1. Fare clic su hello **connettore Azure AD** e selezionare **Esegui...**

   2. Nella finestra di dialogo popup hello, selezionare **importazione completa** e fare clic su **OK**.
   
   3. Attendere che l'operazione toocomplete.

3. Verificare le modifiche alle regole di sincronizzazione hello in un oggetto utente esistente:

attributo di origine Hello in Active Directory e PreferredDataLocation da Azure AD sono state importate nel on-premise hello rispettivo spazio connettore. Prima di procedere con il passaggio di sincronizzazione completa, è consigliabile effettuare un **anteprima** a un utente esistente oggetto hello locale spazio connettore di Active Directory. oggetto Hello selezionati deve avere l'attributo di origine hello popolato. Una corretta **anteprima** con hello PreferredDataLocation popolato nel Metaverse hello è un buon indicatore che le regole di sincronizzazione hello è stato configurato correttamente. Per informazioni su come toodo un **anteprima**, fare riferimento toosection [verificare hello modifica](#verify-the-change).

4. Eseguire **sincronizzazione completa** passaggio su hello **connettore di Active Directory locale**:

   1. Fare clic su hello **connettore di Active Directory locale** e selezionare **Esegui...**
  
   2. Nella finestra di dialogo popup hello, selezionare **sincronizzazione completa** e fare clic su **OK**.
   
   3. Attendere che l'operazione toocomplete.

5. Verificare **esportazioni in sospeso** tooAzure AD:

   1. Fare clic su hello **connettore Azure AD** e selezionare **spazio connettore ricerca**.

   2. Nella finestra popup di spazio connettore ricerca hello:

      1. Impostare **ambito** troppo**esportare in sospeso**.
      
      2. Selezionare tutte e 3 le caselle di controllo, tra cui **Aggiungi, Modifica ed Elimina**.
      
      3. Fare clic su hello **ricerca** elenco pulsanti di hello tooget degli oggetti con modifiche toobe esportato. le modifiche di hello tooexamine per un determinato oggetto, fare doppio clic su oggetto hello.
      
      4. Verificare che sono previste modifiche hello.

6. Eseguire **esportare** passaggio su hello **connettore Azure AD**
      
   1. Pulsante destro del mouse hello **connettore Azure AD** e selezionare **Esegui...**
   
   2. Nella finestra popup di hello Run Connector, selezionare **esportare** e fare clic su **OK**.
   
   3. Attendere toocomplete tooAzure Active Directory di esportazione.

> [!NOTE]
> È possibile riscontrare che hello passaggi non includono i passaggi di sincronizzazione completa hello ed esportazione su hello Azure Active Directory Connector. non sono necessari passaggi Hello poiché i valori di attributo hello flusso dal locale Active Directory tooAzure AD solo.

### <a name="step-7-re-enable-sync-scheduler"></a>Passaggio 7: Riattivare l'utilità di pianificazione della sincronizzazione
Abilitare nuovamente l'utilità di pianificazione sincronizzazione predefinite hello:

1. Avviare una sessione di PowerShell.

2. Riabilitare la sincronizzazione pianificata eseguendo di cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $true`



## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su modello di configurazione hello in [Provisioning dichiarativo comprensione](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Altre informazioni su linguaggio delle espressioni hello [informazioni sulle espressioni di Provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).

**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
