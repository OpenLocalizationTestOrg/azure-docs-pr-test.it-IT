---
title: 'Esercitazione: Configurazione di Workday per il provisioning utenti automatico con Active Directory locale e Azure Active Directory | Microsoft Docs'
description: "Informazioni su come toouse Workday come origine dei dati di identità per Active Directory e Azure Active Directory."
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a>Esercitazione: Configurazione di Workday per il provisioning utenti automatico con Active Directory locale e Azure Active Directory
obiettivo di Hello di questa esercitazione è tooshow hello passaggi tooperform tooimport utenti da Workday in Active Directory e Azure Active Directory, con writeback facoltativo di tooWorkday alcuni attributi. 



## <a name="overview"></a>Panoramica

Hello [servizio di provisioning di utenti di Azure Active Directory](active-directory-saas-app-provisioning.md) si integra con hello [Workday risorse umane API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) in ordine tooprovision gli account utente. Azure AD Usa questo hello tooenable connessione flussi di lavoro di provisioning utente di seguenti:

* **Provisioning utenti tooActive Directory** -sincronizzare i set selezionato di utenti da Workday in uno o più foreste di Active Directory. 

* **Provisioning utenti solo cloud tooAzure Active Directory** -possano eseguirne il provisioning di utenti ibrida presenti in Active Directory e Azure Active Directory in utilizzando quest'ultimo hello [AAD Connect](connect/active-directory-aadconnect.md). Tuttavia, è possono effettuare il provisioning degli utenti che sono solo cloud direttamente da Workday tramite Active Directory tooAzure hello utente Azure AD di provisioning del servizio.

* **Writeback di posta elettronica indirizzi tooWorkday** -servizio il provisioning degli utenti hello Azure AD è possono scrivere selezionato AD Azure utente attributi indietro tooWorkday, ad esempio indirizzo di posta elettronica hello.

### <a name="scenarios-covered"></a>Scenari possibili

i flussi di lavoro supportati dal servizio di provisioning dell'utente di Azure AD hello il provisioning degli utenti Hello Workday consente l'automazione di hello seguenti scenari di gestione del ciclo di vita delle risorse umane e identità:

* **Assunzione di nuovi dipendenti** : quando un nuovo dipendente viene aggiunto tooWorkday, verrà creato automaticamente un account utente in Active Directory, Azure Active Directory e, facoltativamente, Office 365 e [altre applicazioni SaaS supportate da Azure AD ](active-directory-saas-app-provisioning.md), con scrittura parte posteriore tooWorkday indirizzo di posta elettronica hello.

* **Aggiornamenti di attributi e profili dei dipendenti**: se il record di un dipendente viene aggiornato in Workday (ad esempio, il nome, il titolo o il manager), il relativo account utente verrà aggiornato automaticamente in Active Directory, Azure Active Directory e, facoltativamente, in Office 365 e [altre applicazioni SaaS supportate da Azure AD](active-directory-saas-app-provisioning.md).

* **Eliminazione di dipendenti**: quando un dipendente viene eliminato in Workday, il relativo account utente viene disabilitato automaticamente in Active Directory, Azure Active Directory e, facoltativamente, in Office 365 e [altre applicazioni SaaS supportate da Azure AD](active-directory-saas-app-provisioning.md).

* **Dipendente nuovamente hires** : quando un dipendente è rehired in Workday, il vecchio account possono essere riattivati automaticamente oppure tooActive di nuovo effettuato il provisioning (a seconda delle preferenze) Directory, Azure Active Directory e, facoltativamente, Office 365 e [altre applicazioni SaaS supportate da Azure AD](active-directory-saas-app-provisioning.md).


## <a name="planning-your-solution"></a>Pianificazione della soluzione

Prima di iniziare l'integrazione Workday, controllare i prerequisiti di hello di sotto e lettura hello seguenti informazioni aggiuntive su come toomatch l'architettura di Active Directory e i requisiti con il provisioning degli utenti hello soluzioni fornite da Azure Active Directory.

### <a name="prerequisites"></a>Prerequisiti

scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:

* Una sottoscrizione di Azure AD Premium P1 valida con accesso di amministratore globale
* Un tenant per l'implementazione di Workday a scopo di test e integrazione
* Le autorizzazioni di amministratore di Workday toocreate un utente di integrazione di sistema e verificare i dati dei dipendenti tootest modifiche a scopo di test
* Per tooActive Directory di provisioning dell'utente, un server di dominio in esecuzione il servizio di Windows 2012 o versione successiva è richiesto toohost hello [l'agente di sincronizzazione locale](https://go.microsoft.com/fwlink/?linkid=847801)
* [Azure AD Connect](connect/active-directory-aadconnect.md) per la sincronizzazione tra Active Directory e Azure AD

> [!NOTE]
> Se il tenant di Azure Active Directory si trova in Europa, vedere hello [problemi noti](#known-issues) sezione riportata di seguito.


### <a name="solution-architecture"></a>Architettura della soluzione

Azure AD fornisce un'ampia gamma di provisioning toohelp connettori per risolvere il provisioning e l'identità di gestione del ciclo di vita da Workday tooActive Directory, Azure AD, le app SaaS e oltre. Le funzionalità a cui si utilizzeranno e per la configurazione di soluzione hello varia a seconda di ambiente e i requisiti dell'organizzazione. Come primo passaggio, prendere nota di quante seguenti hello sono presenti e distribuito nell'organizzazione:

* Quante foreste di Active Directory sono in uso?
* Quanti domini di Active Directory sono in uso?
* Quante unità organizzative di Active Directory sono in uso?
* Quanti tenant di Azure Active Directory sono in uso?
* Sono presenti utenti che necessitano di tooboth toobe provisioning Active Directory e Azure Active Directory (ad esempio, gli utenti "ibrido")?
* Sono presenti utenti che necessitano di tooAzure toobe provisioning Active Directory, ma non di Active Directory (ad esempio, "cloud solo" utenti)?
* Indirizzi di posta elettronica utente necessario toobe riscritti tooWorkday?

Dopo aver creato le risposte toothese domande, è possibile pianificare il giorno lavorativo provisioning distribuzione dal seguente materiale sussidiario hello seguente.

#### <a name="using-provisioning-connector-apps"></a>Uso di app di connettori di provisioning

Azure Active Directory supporta connettori di provisioning preintegrati per Workday e molte altre applicazioni SaaS. 

Un singolo connettore provisioning interfacce con hello API di un singolo sistema di origine e aiuta a disposizione dati tooa bersaglio singolo sistema. La maggior parte dei connettori di provisioning supportati da Azure AD per una sola origine e il sistema di destinazione (ad esempio tooServiceNow di Azure AD) e possono essere l'installazione aggiungendo semplicemente l'applicazione hello in questione dalla raccolta di app di Azure AD hello (ad esempio ServiceNow). 

È presente una relazione uno-a-uno tra le istanze dei connettori di provisioning e le istanze delle app in Azure AD:

| Sistema di origine | Sistema di destinazione |
| ---------- | ---------- | 
| Tenant di Azure AD | Applicazione SaaS |


Tuttavia, quando si lavora con Workday e Active Directory, esistono più toobe sistemi di origine e destinazione considerati:

| Sistema di origine | Sistema di destinazione | Note |
| ---------- | ---------- | ---------- |
| Workday | Foresta di Active Directory | Ogni foresta viene considerata come un sistema di destinazione distinto |
| Workday | Tenant di Azure AD | Come richiesto per gli utenti solo cloud |
| Foresta di Active Directory | Tenant di Azure AD | Questo flusso è attualmente gestito da AAD Connect |
| Tenant di Azure AD | Workday | Per il writeback degli indirizzi di posta elettronica |

toofacilitate questi più flussi di lavoro toomultiple origine e destinazione sistemi, Azure AD fornisce più App connettore provisioning che è possibile aggiungere dalla raccolta di app hello Azure AD:

![Raccolta di app di AAD](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* **WorkDay tooActive il Provisioning della Directory** -questa app semplifica il provisioning di account utente da Workday tooa singola foresta Active Directory. Se si dispone di più foreste, è possibile aggiungere un'istanza di questa app dalla raccolta di app di Azure AD hello per ogni foresta di Active Directory per che è necessario tooprovision.

* **WorkDay tooAzure AD Provisioning** -mentre AAD Connect è lo strumento di hello che deve essere tooAzure agli utenti di Active Directory toosynchronize utilizzato Active Directory, questa applicazione può essere utilizzato toofacilitate il provisioning degli utenti solo cloud da Workday tooa singolo Tenant di Azure Active Directory.

* **Writeback WorkDay** -questa app semplifica il writeback degli indirizzi di posta elettronica dell'utente da Azure Active Directory tooWorkday.

> [!TIP]
> app "Workday" regolare Hello viene utilizzato per la configurazione di single sign-on tra Azure Active Directory e di Workday. 

Come tooset e configurare questi speciali provisioning connettore App è soggetto hello di hello restanti sezioni di questa esercitazione. App che si sceglie tooconfigure dipenderà dai sistemi sui quali è necessario tooprovision e il numero di foreste di Active Directory e Azure AD i tenant sono nell'ambiente in uso.

![Panoramica](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a>Configurare un utente di integrazione dei sistemi in Workday
Un requisito comune di tutti i connettori provisioning Workday hello è che richiedono le credenziali per un giorno lavorativo sistema integrazione account tooconnect toohello Workday risorse umane API. In questa sezione viene descritto come l'account toocreate integratore di un giorno lavorativo.

> [!NOTE]
> È possibile toobypass questa procedura e usare invece un account di amministratore globale di Workday come account del sistema di integrazione hello. Questa soluzione è utilizzabile a scopo dimostrativo, ma non è consigliata per le distribuzioni di produzione.

### <a name="create-an-integration-system-user"></a>Creare un utente del sistema di integrazione

**toocreate un utente del sistema di integrazione:**

1. Accedere al tenant di Workday usando un account amministratore. In hello **Workbench Workday**, immettere creare utente nella casella di ricerca hello e quindi fare clic su **Crea utente del sistema di integrazione**. 
   
    ![Creare un utente](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Creare un utente")
2. Hello completo **Crea utente del sistema di integrazione** attività fornendo un nome utente e una password per un nuovo utente di sistema di integrazione.  
 * Lasciare hello **Richiedi nuova Password al successivo accesso** opzione è deselezionata, perché l'utente effettuerà l'accesso a livello di codice. 
 * Lasciare hello **minuti di Timeout della sessione** con valore predefinito pari a 0, che impedirà hello le sessioni utente di timeout in modo anomalo. 
   
    ![Creare un utente del sistema di integrazione](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Creare un utente del sistema di integrazione")

### <a name="create-a-security-group"></a>Creare un gruppo di sicurezza
È necessario toocreate un gruppo di sicurezza di sistema di integrazione non vincolato e assegnare tooit utente hello.

**toocreate un gruppo di sicurezza:**

1. Immettere, creare un gruppo di sicurezza nella casella di ricerca hello e quindi fare clic su **Crea gruppo di sicurezza**. 
   
    ![Creare un gruppo di sicurezza](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "Creare un gruppo di sicurezza")
2. Hello completo **Crea gruppo di sicurezza** attività.  
3. Seleziona gruppo di protezione sistema integrazione-non vincolato dall'hello **tipo di gruppo di sicurezza con tenant** elenco a discesa.
4. Creare un toowhich gruppo di sicurezza verranno aggiunti membri in modo esplicito. 
   
    ![Creare un gruppo di sicurezza](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "Creare un gruppo di sicurezza")

### <a name="assign-hello-integration-system-user-toohello-security-group"></a>Assegnare il gruppo di sicurezza toohello hello integrazione sistema utente

**utente del sistema di integrazione tooassign hello:**

1. Immettere il gruppo di sicurezza di modifica nella casella di ricerca hello e quindi fare clic su **Modifica gruppo di sicurezza**. 
   
    ![Modificare un gruppo di sicurezza](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Modificare un gruppo di sicurezza")
2. Cercare e selezionare il nuovo gruppo di sicurezza integrazione di hello in base al nome. 
   
    ![Modificare un gruppo di sicurezza](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Modificare un gruppo di sicurezza")
3. Aggiungere hello nuova integrazione system toohello nuovo gruppo di protezione utente. 
   
    ![Gruppo di sicurezza del sistema](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "Gruppo di sicurezza del sistema")  

### <a name="configure-security-group-options"></a>Configurare le opzioni del gruppo di sicurezza
In questo passaggio, si concedono toohello nuovo sicurezza gruppo le autorizzazioni per **ottenere** e **inserire** operazioni su oggetti hello protetti da hello seguenti criteri di sicurezza del dominio:

* External Account Provisioning
* Worker Data: Public Worker Reports
* Worker Data: All Positions
* Worker Data: Current Staffing Information
* Dati lavoratore - Qualifica riportata sul profilo

**opzioni di gruppo di sicurezza tooconfigure:**

1. Immettere i criteri di sicurezza del dominio nella casella di ricerca hello e quindi fare clic sul collegamento di hello **criteri di sicurezza di dominio per Area funzionale**.  
   
    ![Criteri di sicurezza di dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Criteri di sicurezza di dominio")  
2. Ricerca di sistema e seleziona hello **sistema** area funzionale.  Fare clic su **OK**.  
   
    ![Criteri di sicurezza di dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Criteri di sicurezza di dominio")  
3. Nell'elenco dei criteri di sicurezza per area funzionale sistema hello hello espandere **amministrazione della sicurezza** e selezionare il criterio di protezione dominio hello **Provisioning Account esterno**.  
   
    ![Criteri di sicurezza di dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Criteri di sicurezza di dominio")  
4. Fare clic su **Modifica autorizzazioni**, quindi scegliere hello **Modifica autorizzazioni**finestra di dialogo pagina, aggiungere hello nuova protezione toohello l'elenco dei gruppi di sicurezza con **ottenere** e **Inserire** autorizzazioni di integrazione. 
   
    ![Modificare un'autorizzazione](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Modificare un'autorizzazione")  
5. Ripetere il passaggio 1 sopra tooreturn toohello schermata per la selezione delle aree funzionali e questa volta, cercare "personale", selezionare hello **area funzionale personale** e fare clic su **OK**.
   
    ![Criteri di sicurezza di dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Criteri di sicurezza di dominio")  
6. Nell'elenco dei criteri di sicurezza per area funzionale personale hello hello espandere **dati lavoratore: personale** e ripetere il passaggio 4 riportato sopra per ciascuno dei rimanenti criteri di sicurezza:

   * Worker Data: Public Worker Reports
   * Worker Data: All Positions
   * Worker Data: Current Staffing Information
   * Dati lavoratore - Qualifica riportata sul profilo
   
7. Ripetere il passaggio 1, sopra, tooreturn toohello schermata per la selezione di aree funzionali e questo punto, cercare **le informazioni di contatto**, selezionare l'area funzionale personale hello e fare clic su **OK**.

8.  Nell'elenco dei criteri di sicurezza per area funzionale personale hello hello espandere **dati lavoratore: le informazioni di contatto lavoro**e ripetere il passaggio 4 sopra riportato per i criteri di sicurezza hello riportato di seguito:

    * Worker Data: Work Email

    ![Criteri di sicurezza di dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Criteri di sicurezza di dominio")  
    
### <a name="activate-security-policy-changes"></a>Attivare le modifiche apportate ai criteri di sicurezza

**modifiche ai criteri di sicurezza tooactivate:**

1. Immettere nella casella di ricerca hello attivare e quindi fare clic sul collegamento di hello **attivare modifiche ai criteri di sicurezza in sospeso**. 
   
    ![Attivare](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Attivare") 
2. Begin hello attività immettendo un commento a fini di controllo Attiva modifiche ai criteri di sicurezza in sospeso e quindi fare clic su **OK**. 
   
    ![Attivare la sicurezza in sospeso](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Attivare la sicurezza in sospeso")   
3. Attività di completamento hello nella schermata successiva di hello selezionando la casella di controllo hello **conferma**, quindi fare clic su **OK**. 
   
    ![Attivare la sicurezza in sospeso](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Attivare la sicurezza in sospeso")  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a>Configurazione del provisioning utenti da Workday tooActive Directory
Seguire questi account utente di tooconfigure istruzioni provisioning da Workday tooeach foresta di Active Directory necessari per il provisioning.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Parte 1: Aggiunta di hello provisioning connettore app e la creazione di hello connessione tooWorkday

**tooconfigure Workday tooActive il provisioning della Directory:**

1.  Andare troppo<https://portal.azure.com>

2.  Nella barra di spostamento a sinistra di hello, selezionare **Azure Active Directory**

3.  Selezionare **Applicazioni aziendali** e quindi **Tutte le applicazioni**.

4.  Selezionare **aggiungere un'applicazione**e seleziona hello **tutti** categoria.

5.  Cercare **tooActive Workday Provisioning Directory**e aggiungere tale applicazione dalla raccolta di hello.

6.  Dopo aver hello viene aggiunto l'app e schermata dei dettagli hello app viene visualizzata, selezionare **Provisioning**

7.  Hello modifica **Provisioning** **modalità** troppo**automatico**

8.  Hello completo **credenziali di amministratore** sezione come indicato di seguito:

   * **Admin Username** – immettere nome utente di hello dell'account di sistema di integrazione Workday, hello con nome di dominio tenant hello aggiunto. **Dovrebbe essere simile a: username@contoso4**

   * **Password di amministratore:** immettere una password di account di sistema di integrazione Workday hello hello

   * **: URL del tenant** immettere l'endpoint dei servizi web Workday toohello URL hello per il tenant. Questo dovrebbe essere simile: https://wd3-impl-services1.workday.com/ccx/service/contoso4, dove contoso4 viene sostituito con il nome del tenant corretto e wd3 impl viene sostituito con stringa di ambiente corretto hello.

   * **Foresta di Active Directory -** hello "Name" della foresta di Active Directory, come restituito dal cmdlet Get-ADForest hello. In genere si tratta di una stringa simile a: *contoso.com*

   * **Contenitore di Active Directory -** immettere hello contenitore stringa che contiene tutti gli utenti nella foresta Active Directory. Esempio: *OU=Standard Users,OU=Users,DC=contoso,DC=test*

   * **Indirizzo di posta elettronica per le notifiche:** immettere l'indirizzo di posta elettronica e selezionare la casella di controllo "Invia una notifica di posta elettronica in caso di errore".

   * Fare clic su hello **Test connessione** pulsante. Se il test di connessione hello ha esito positivo, fare clic su hello **salvare** pulsante nella parte superiore di hello. In caso contrario, verificare che le credenziali di Workday hello siano valide in Workday. 

![Portale di Azure](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a>Parte 2: Configurare i mapping degli attributi 

In questa sezione verrà configurato il flusso dei dati utente da Workday in Active Directory.

1.  Nella scheda Provisioning hello in **mapping**, fare clic su **sincronizzare lavoratori Workday tooOnPremises**.

2.  In hello **ambito dell'oggetto di origine** campo, è possibile selezionare quali insiemi di utenti in Workday devono trovarsi nell'ambito per il provisioning tooAD, definendo un set di filtri basati su attributi. ambito predefinito Hello è "tutti gli utenti in Workday". Filtri di esempio:

   * Esempio: Ambito toousers con ID di lavoro tra 1000000 e 2000000

      * Attributo: WorkerID

      * Operatore: Corrispondenza REGEX

      * Valore: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Esempio: Solo i dipendenti, senza i lavoratori occasionali 

      * Attributo: EmployeeID

      * Operatore: NON È NULL

3.  In hello **azioni dell'oggetto destinazione** campo, è possibile applicare un filtro a livello globale le azioni consentite toobe eseguite su Active Directory. **Creazione** e **Aggiornamento** sono le più comuni.

4.  In hello **attributo mapping** sezione, è possibile definire Workday come singoli attributi di Directory tooActive eseguire il mapping di attributi.

5. Fare clic su un tooupdate di mapping di attributi esistente oppure fare clic su **aggiungere nuovo mapping** nella parte inferiore di hello del nuovo mapping di hello schermata tooadd. Il mapping di un singolo attributo supporta queste proprietà:

      * **Tipo di mapping**

         * **Diretto** – scrive il valore di hello del hello Workday toohello AD attributo, senza modifiche

         * **Costante** -scrivere l'attributo hello AD un valore stringa costante, statici

         * **Espressione** : consente un valore personalizzato all'attributo hello Active Directory, in base a uno o più attributi di Workday toowrite. [Per altre informazioni, vedere questo articolo sulle espressioni](active-directory-saas-writing-expressions-for-attribute-mappings.md).

      * **Attributo di origine** -attributo utente hello da Workday.

      * **Valore predefinito**: facoltativo. Se l'attributo di origine hello ha un valore vuoto, il mapping di hello scriverà questo valore.
            Configurazione più comune è tooleave questo vuoto.

      * **Attributo di destinazione** : attributo utente hello in Active Directory.

      * **Associare gli oggetti utilizzando l'attributo** : questo mapping deve essere utilizzato o meno toouniquely identificare gli utenti tra Workday e Active Directory. È in genere impostato sul campo ID ruolo di lavoro per Workday, in genere viene eseguito il mapping a uno degli attributi ID dipendente hello in Active Directory.

      * **Precedenza abbinamento**: è possibile impostare più attributi corrispondenti. Se sono presenti più attributi, vengono valutati nell'ordine definito da questo campo. Quando viene rilevata una corrispondenza la valutazione degli attributi corrispondenti termina.

      * **Applica questo mapping**
       
         * **Sempre**: applica il mapping sia all'azione di creazione che all'azione di aggiornamento dell'utente

         * **Only during creation** (Solo durante la creazione): applica il mapping solo alle azioni di creazione dell'utente

6. i mapping, fare clic su toosave **salvare** nella parte superiore di hello della sezione del Mapping di attributi.

![Portale di Azure](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

**Di seguito sono riportati alcuni esempi di mapping degli attributi tra Workday e Active Directory, con alcune espressioni comuni**

-   espressione di Hello che esegue il mapping toohello parentDistinguishedName AD attributo può essere utilizzato tooprovision tooa un utente specifica unità Organizzativa in base a uno o più attributi di origine di Workday. In questo esempio, gli utenti vengono inseriti in unità organizzative diverse a seconda dei dati sulla città in Workday.

-   espressione Hello che esegue il mapping di attributo userPrincipalName AD toohello crea un nome UPN di firstName.LastName@contoso.com. Sostituisce inoltre i caratteri speciali non validi.

-   [La documentazione sulla scrittura delle espressioni è disponibile qui](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| ATTRIBUTO DI WORKDAY | ATTRIBUTO DI ACTIVE DIRECTORY |  ID CORRISPONDENTE? | CREAZIONE / AGGIORNAMENTO |
| ---------- | ---------- | ---------- | ---------- |
|  **WorkerID**  |  EmployeeID | **Sì** | Scritto solo al momento della creazione | 
|  **Municipality**   |   l   |     | Creazione e aggiornamento |
|  **Company**         | company   |     |  Creazione e aggiornamento |
|  **CountryReferenceTwoLetter**      |   co |     |   Creazione e aggiornamento |
| **CountryReferenceTwoLetter**    |  c  |     |         Creazione e aggiornamento |
| **SupervisoryOrganization**  | department  |     |  Creazione e aggiornamento |
|  **PreferredNameData**  |  displayName |     |   Creazione e aggiornamento |
| **EmployeeID**    |  cn    |   |   Scritto solo al momento della creazione |
| **Fax**      | facsimileTelephoneNumber     |     |    Creazione e aggiornamento |
| **FirstName**   | givenName       |     |    Creazione e aggiornamento |
| **Switch(\[Active\], , "0", "True", "1",)** |  accountDisabled      |     | Creazione e aggiornamento |
| **Mobile**  |    mobile       |     |       Scritto solo al momento della creazione |
| **EmailAddress**    | mail    |     |     Creazione e aggiornamento |
| **ManagerReference**   | manager  |     |  Creazione e aggiornamento |
| **WorkSpaceReference** | physicalDeliveryOfficeName    |     |  Creazione e aggiornamento |
| **PostalCode**  |   postalCode  |     | Creazione e aggiornamento |
| **LocalReference** |  preferredLanguage  |     |  Creazione e aggiornamento |
| **Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**      |    sAMAccountName            |     |         Scritto solo al momento della creazione |
| **LastName**   |   sn   |     |  Creazione e aggiornamento |
| **CountryRegionReference** |  st     |     | Creazione e aggiornamento |
| **AddressLineData**    |  streetAddress  |     |   Creazione e aggiornamento |
| **PrimaryWorkTelephone**  |  telephoneNumber   |     | Scritto solo al momento della creazione |
| **BusinessTitle**   |  title     |     |  Creazione e aggiornamento |
| **Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**   | userPrincipalName     |     | Creazione e aggiornamento                                                   
| **Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**  | parentDistinguishedName     |     |  Creazione e aggiornamento |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a>Parte 3: Configurare l'agente di sincronizzazione locale hello

In ordine tooprovision tooActive Directory locale, è necessario installare un agente in un server di dominio in desiderio hello foresta di Active Directory. Amministratore di dominio (o Enterprise admin) sono necessarie le credenziali per completare la procedura hello.

**[È possibile scaricare qui agente di sincronizzazione locale hello](https://go.microsoft.com/fwlink/?linkid=847801)**

Dopo aver installato l'agente, eseguire i comandi di Powershell hello seguito agente hello tooconfigure per l'ambiente.

**Comando 1**

> cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent

> import-module AADSyncAgent.psd1

**Comando 2**

> Add-ADSyncAgentActiveDirectoryConfiguration

* Input: Per "Nome Directory", immettere il nome di foresta hello Active Directory, come immesse in parte \#2
* Input: nome utente e password di amministratore per la foresta di Active Directory

**Comando 3**

> Add-ADSyncAgentAzureActiveDirectoryConfiguration

* Input: nome utente e password di amministratore globale per il tenant di Azure AD

**Comando 4**

> Get-AdSyncAgentProvisioningTasks

* Azione: verificare che i dati vengano restituiti. Questo comando individua automaticamente le app di provisioning Workday nel tenant di Azure AD. Output di esempio:

> Name          : My AD Forest
>
> Enabled       : True
>
> DirectoryName : mydomain.contoso.com
>
> Credentialed  : False
>
> Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203

**Comando 5**

> Start-AdSyncAgentSynchronization -Automatic

**Comando 6**

> net stop aadsyncagent

**Comando 7**

> net start aadsyncagent

### <a name="part-4-start-hello-service"></a>Parte 4: Avviare il servizio di hello
Dopo aver completate le parti 1-3, è possibile avviare il provisioning del servizio nel portale di gestione Azure hello hello.

1.  In hello **Provisioning** scheda, hello set **lo stato di Provisioning** a **su**.

2. Fare clic su **Salva**.

3. Verrà avviata la sincronizzazione iniziale hello, che può accettare un numero variabile di ore a seconda di quanti sono gli utenti in Workday.

4. Gli eventi di sincronizzazione, ad esempio gli utenti che vengono letti da Workday e successivamente aggiunti o aggiornati tooActive Directory, possono essere visualizzate in hello **i log di controllo** scheda. **[Vedere hello provisioning reporting guide per informazioni dettagliate su come i log di controllo di hello tooread](active-directory-saas-provisioning-reporting.md)**

5.  il registro applicazioni di Windows Hello sul computer agente hello mostrerà tutte le operazioni eseguite tramite l'agente di hello.

6. Al termine verrà scritto un report di riepilogo di controllo nella scheda **Provisioning**, come illustrato di seguito.

![Portale di Azure](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a>Configurazione di Active Directory tooAzure di provisioning dell'utente
Come si configura provisioning tooAzure Active Directory dipende dei requisiti di provisioning, come descritto in dettaglio nella tabella hello riportata di seguito.

| Scenario | Soluzione |
| -------- | -------- |
| **Gli utenti devono toobe provisioning tooActive Directory e Azure AD** | Usare  **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Gli utenti è necessario il provisioning toobe tooActive Directory solo** | Usare  **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Gli utenti devono toobe provisioning tooAzure AD solo (solo cloud)** | Hello utilizzare **Workday tooAzure Active Directory provisioning** app nella raccolta di app hello |

Per istruzioni sulla configurazione di Azure AD Connect, vedere hello [documentazione di Azure AD Connect](connect/active-directory-aadconnect.md).

Hello le sezioni seguenti descritta la configurazione di una connessione tra Workday e Azure AD tooprovision solo cloud degli utenti.

> [!IMPORTANT]
> Se sono presenti solo cloud utenti che richiedono il provisioning toobe tooAzure AD e non in Active Directory locale solo attenersi alla procedura hello riportata di seguito.

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Parte 1: Aggiunta di hello Azure AD provisioning connettore app e la creazione di hello connessione tooWorkday

**tooconfigure Workday tooAzure Active Directory di provisioning per gli utenti solo cloud:**

1.  Andare troppo<https://portal.azure.com>.

2.  Nella barra di spostamento a sinistra di hello, selezionare **Azure Active Directory**

3.  Selezionare **Applicazioni aziendali** e quindi **Tutte le applicazioni**.

4.  Selezionare **aggiungere un'applicazione**, quindi selezionare hello **tutti** categoria.

5.  Cercare **Workday tooAzure AD provisioning**e aggiungere tale applicazione dalla raccolta di hello.

6.  Dopo aver hello viene aggiunto l'app e schermata dei dettagli hello app viene visualizzata, selezionare **Provisioning**

7.  Hello modifica **Provisioning** **modalità** troppo**automatico**

8.  Hello completo **credenziali di amministratore** sezione come indicato di seguito:

   * **Admin Username** – immettere nome utente di hello dell'account di sistema di integrazione Workday, hello con nome di dominio tenant hello aggiunto. Dovrebbe essere simile a: username@contoso4

   * **Password di amministratore:** immettere una password di account di sistema di integrazione Workday hello hello

   * **: URL del tenant** immettere l'endpoint dei servizi web Workday toohello URL hello per il tenant. Questo dovrebbe essere simile: https://wd3-impl-services1.workday.com/ccx/service/contoso4, dove contoso4 viene sostituito con il nome del tenant corretto e wd3 impl viene sostituito con stringa di ambiente corretto hello (se necessario).

   * **Indirizzo di posta elettronica per le notifiche:** immettere l'indirizzo di posta elettronica e selezionare la casella di controllo "Invia una notifica di posta elettronica in caso di errore".

   * Fare clic su hello **Test connessione** pulsante.

   * Se il test di connessione hello ha esito positivo, fare clic su hello **salvare** pulsante nella parte superiore di hello. In caso contrario, controllare che hello Workday URL e credenziali sono valide nella giornata lavorativa.


### <a name="part-2-configure-attribute-mappings"></a>Parte 2: Configurare i mapping degli attributi 

In questa sezione verrà configurato il flusso dei dati utente da Workday in Azure Active Directory per gli utenti solo cloud.

1.  Nella scheda Provisioning hello in **mapping**, fare clic su **tooAzure lavoratori sincronizzare AD**.

2.   In hello **ambito dell'oggetto di origine** campo, è possibile selezionare quali insiemi di utenti in Workday devono trovarsi nell'ambito per il provisioning tooAzure AD, definendo un set di filtri basati su attributi. ambito predefinito Hello è "tutti gli utenti in Workday". Filtri di esempio:

   * Esempio: Ambito toousers con ID di lavoro tra 1000000 e 2000000

      * Attributo: WorkerID

      * Operatore: Corrispondenza REGEX

      * Valore: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Esempio: Solo i lavoratori occasionali, senza i dipendenti

      * Attributo: ContingentID

      * Operatore: NON È NULL

3.  In hello **azioni dell'oggetto destinazione** campo, è possibile applicare un filtro a livello globale le azioni consentite toobe eseguite in Azure AD. **Creazione** e **Aggiornamento** sono le più comuni.

4.  In hello **attributo mapping** sezione, è possibile definire Workday come singoli attributi di Directory tooActive eseguire il mapping di attributi.

5. Fare clic su un tooupdate di mapping di attributi esistente oppure fare clic su **aggiungere nuovo mapping** nella parte inferiore di hello del nuovo mapping di hello schermata tooadd. Il mapping di un singolo attributo supporta queste proprietà:

   * **Tipo di mapping**

      * **Diretto** – scrive il valore di hello del hello Workday toohello AD attributo, senza modifiche

      * **Costante** -scrivere l'attributo hello AD un valore stringa costante, statici

      * **Espressione** : consente un valore personalizzato all'attributo hello Active Directory, in base a uno o più attributi di Workday toowrite. [Per altre informazioni, vedere questo articolo sulle espressioni](active-directory-saas-writing-expressions-for-attribute-mappings.md).

   * **Attributo di origine** -attributo utente hello da Workday.

   * **Valore predefinito**: facoltativo. Se l'attributo di origine hello ha un valore vuoto, il mapping di hello scriverà questo valore.
            Configurazione più comune è tooleave questo vuoto.

   * **Attributo di destinazione** : attributo utente hello in Azure AD.

   * **Associare gli oggetti utilizzando l'attributo** : questo mapping deve essere utilizzato o meno toouniquely identificare gli utenti tra Workday e Azure AD. È in genere impostato sul campo ID ruolo di lavoro per la giornata lavorativa, che in genere è mappata a un attributo ID dipendente hello (nuovo) o un attributo di estensione in Azure AD.

   * **Precedenza abbinamento**: è possibile impostare più attributi corrispondenti. Se sono presenti più attributi, vengono valutati nell'ordine definito da questo campo. Quando viene rilevata una corrispondenza la valutazione degli attributi corrispondenti termina.

   * **Applica questo mapping**

     * **Sempre**: applica il mapping sia all'azione di creazione che all'azione di aggiornamento dell'utente

     * **Only during creation** (Solo durante la creazione): applica il mapping solo alle azioni di creazione dell'utente

6. i mapping, fare clic su toosave **salvare** nella parte superiore di hello della sezione del Mapping di attributi.

### <a name="part-3-start-hello-service"></a>Parte 3: Avviare il servizio di hello
Dopo aver completate le parti 1-2, è possibile avviare hello provisioning del servizio.

1.  In hello **Provisioning** scheda, hello set **lo stato di Provisioning** a **su**.

2. Fare clic su **Salva**.

3. Verrà avviata la sincronizzazione iniziale hello, che può accettare un numero variabile di ore a seconda di quanti sono gli utenti in Workday.

4. Eventi di sincronizzazione possono essere visualizzati in hello **i log di controllo** scheda. **[Vedere hello provisioning reporting guide per informazioni dettagliate su come i log di controllo di hello tooread](active-directory-saas-provisioning-reporting.md)**

5. Al termine verrà scritto un report di riepilogo di controllo nella scheda **Provisioning**, come illustrato di seguito.


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a>Configurazione del writeback di tooWorkday gli indirizzi di posta elettronica
Seguire questi writeback tooconfigure istruzioni di indirizzi di posta elettronica utente tooWorkday di Azure Active Directory.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Parte 1: Aggiunta di hello provisioning connettore app e la creazione di hello connessione tooWorkday

**tooconfigure Workday tooActive il provisioning della Directory:**

1.  Andare troppo<https://portal.azure.com>

2.  Nella barra di spostamento a sinistra di hello, selezionare **Azure Active Directory**

3.  Selezionare **Applicazioni aziendali** e quindi **Tutte le applicazioni**.

4.  Selezionare **aggiungere un'applicazione**, quindi selezionare hello **tutti** categoria.

5.  Cercare **Workday Writeback**e aggiungere tale applicazione dalla raccolta di hello.

6.  Dopo aver hello viene aggiunto l'app e schermata dei dettagli hello app viene visualizzata, selezionare **Provisioning**

7.  Hello modifica **Provisioning** **modalità** troppo**automatico**

8.  Hello completo **credenziali di amministratore** sezione come indicato di seguito:

   * **Admin Username** – immettere nome utente di hello dell'account di sistema di integrazione Workday, hello con nome di dominio tenant hello aggiunto. Dovrebbe essere simile a: username@contoso4

   * **Password di amministratore:** immettere una password di account di sistema di integrazione Workday hello hello

   * **: URL del tenant** immettere l'endpoint dei servizi web Workday toohello URL hello per il tenant. Questo dovrebbe essere simile: https://wd3-impl-services1.workday.com/ccx/service/contoso4, dove contoso4 viene sostituito con il nome del tenant corretto e wd3 impl viene sostituito con stringa di ambiente corretto hello (se necessario).

   * **Indirizzo di posta elettronica per le notifiche:** immettere l'indirizzo di posta elettronica e selezionare la casella di controllo "Invia una notifica di posta elettronica in caso di errore".

   * Fare clic su hello **Test connessione** pulsante. Se il test di connessione hello ha esito positivo, fare clic su hello **salvare** pulsante nella parte superiore di hello. In caso contrario, controllare che hello Workday URL e credenziali sono valide nella giornata lavorativa.


### <a name="part-2-configure-attribute-mappings"></a>Parte 2: Configurare i mapping degli attributi 


In questa sezione verrà configurato il flusso dei dati utente da Workday in Active Directory.

1.  Nella scheda Provisioning hello in **mapping**, fare clic su **tooWorkday agli utenti di sincronizzazione Azure AD**.

2.  In hello **ambito dell'oggetto di origine** campo, è possibile scegliere di filtrare quali gruppi di utenti di Azure Active Directory devono avere i relativi indirizzi di posta elettronica riscritti tooWorkday. ambito predefinito Hello è "tutti gli utenti di Azure AD". 

3.  In hello **attributo mapping** sezione, è possibile definire Workday come singoli attributi di Directory tooActive eseguire il mapping di attributi. È presente un mapping per l'indirizzo di posta elettronica hello per impostazione predefinita. Tuttavia, hello ID corrispondente deve essere aggiornato toomatch utenti in Azure Active Directory con le voci corrispondenti in Workday. Un metodo comune corrispondente è toosynchronize hello Workday lavoro ID o employee ID tooextensionAttribute1-15 in Azure AD e quindi utilizzare questo attributo in utenti di Azure AD toomatch nella giornata lavorativa.

4.  i mapping, fare clic su toosave **salvare** nella parte superiore di hello di hello Mapping di attributi di sezione.

### <a name="part-3-start-hello-service"></a>Parte 3: Avviare il servizio di hello
Dopo aver completate le parti 1-2, è possibile avviare hello provisioning del servizio.

1.  In hello **Provisioning** scheda, hello set **lo stato di Provisioning** a **su**.

2. Fare clic su **Salva**.

3. Verrà avviata la sincronizzazione iniziale hello, che può accettare un numero variabile di ore a seconda di quanti sono gli utenti in Workday.

4. Eventi di sincronizzazione possono essere visualizzati in hello **i log di controllo** scheda. **[Vedere hello provisioning reporting guide per informazioni dettagliate su come i log di controllo di hello tooread](active-directory-saas-provisioning-reporting.md)**

5. Al termine verrà scritto un report di riepilogo di controllo nella scheda **Provisioning**, come illustrato di seguito.

## <a name="known-issues"></a>Problemi noti

* **Controllare i registri in impostazioni locali europee** - come della versione di hello di questa technical preview, si verifica un problema noto con hello [log di controllo](active-directory-saas-provisioning-reporting.md) per hello Workday connettore App non presenti nel hello [portalediAzure](https://portal.azure.com) se tenant hello Azure Active Directory si trova in un centro dati. Presto sarà disponibile una correzione per questo problema. Controllare questo spazio tra hello prossimo futuro per gli aggiornamenti. 

## <a name="additional-resources"></a>Risorse aggiuntive
* [Esercitazione sulla configurazione dell'accesso Single Sign-On tra Workday e Azure Active Directory](active-directory-saas-workday-tutorial.md)
* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni su modalità di registrazione tooreview e ottengono report sull'attività di provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
