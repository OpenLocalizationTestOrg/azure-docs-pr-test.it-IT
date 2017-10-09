## <a name="prerequisites"></a>Prerequisiti
Prima di è possibile scrivere codice per la gestione della rete CDN, è necessario toodo alcuni tooenable preparazione toointeract il nostro codice con hello Azure Resource Manager.  toodo, è necessario:

* Creare un hello toocontain gruppo di risorse profilo CDN è stato creato in questa esercitazione
* Configurare l'autenticazione tooprovide di Azure Active Directory per l'applicazione
* Applicare le autorizzazioni di gruppo di risorse toohello in modo che solo utenti autorizzati da nostri tenant di Azure AD è possibile interagire con il profilo CDN

### <a name="creating-hello-resource-group"></a>Creazione del gruppo di risorse hello
1. Accedere al hello [portale Azure](https://portal.azure.com).
2. Fare clic su hello **New** pulsante nella parte superiore sinistra hello e quindi **Management**, e **gruppo di risorse**.

    ![Creazione di un nuovo gruppo di risorse](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. Assegnare al gruppo di risorse il nome *CdnConsoleTutorial*.  Selezionare la sottoscrizione e scegliere un percorso locale.  Se si desidera, è possibile fare clic su hello **toodashboard Pin** casella di controllo toopin hello risorsa toohello dashboard del gruppo nel portale di hello.  Questo rende più semplice toofind in un secondo momento.  Dopo avere eseguito le selezioni, fare clic su **Crea**.

    ![Gruppo di risorse hello denominazione](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. Dopo aver creato il gruppo di risorse hello, se si non blocca tooyour dashboard, è possibile trovare facendo **Sfoglia**, quindi **gruppi di risorse**.  Fare clic su tooopen gruppo di risorse hello è.  Annotare l' **ID sottoscrizione**.  Sarà necessario più avanti.

    ![Gruppo di risorse hello denominazione](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>Creazione di un'applicazione hello Azure AD e l'applicazione di autorizzazioni
Esistono due approcci tooapp l'autenticazione con Azure Active Directory: singoli utenti o a un'entità servizio. Un'entità servizio è simile tooa account del servizio di Windows.  Anziché concedere un toointeract autorizzazioni utente specifico con i profili di rete CDN hello, è invece autorizzazioni hello toohello servizio principale.  Le entità servizio in genere vengono usate per i processi automatizzati e non interattivi.  Anche se in questa esercitazione è la scrittura di un'app console interattiva, ci concentreremo sull'approccio principale hello del servizio.

La creazione di un'entità servizio è costituita da diversi passaggi, compresa la creazione di un'applicazione Azure Active Directory.  toodo, verrà troppo[seguire questa esercitazione](../articles/resource-group-create-service-principal-portal.md).

> [!IMPORTANT]
> Essere toofollow che tutti i passaggi hello hello [esercitazione collegato](../articles/resource-group-create-service-principal-portal.md).  È *estremamente importante* eseguirla esattamente come descritto.  Verificare che toonote il **ID tenant**, **nome dominio tenant** (comunemente un *. c o m* dominio a meno che non è stato specificato un dominio personalizzato), **ID client** , e **chiave di autenticazione client**, come è necessario in seguito.  Essere tooguard prestare particolare attenzione i **ID client** e **chiave di autenticazione client**, come le credenziali possono essere usata da chiunque tooexecute operazioni come entità servizio hello.
>
> Quando si ottiene toohello passaggio denominato Configura applicazione multi-tenant, selezionare **n**.
>
> Quando si otterrà passaggio toohello [assegnare applicazione toorole](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role), gruppo di risorse hello utilizzo creato in precedenza, *CdnConsoleTutorial*, ma anziché hello **lettore** ruolo, assegnare Hello **collaboratore profilo CDN** ruolo.  Dopo aver assegnato hello applicazione hello **collaboratore profilo CDN** ruolo in un gruppo di risorse, esercitazione toothis restituito. 
>
>

Dopo aver creato il hello principale e assegnati di servizio **collaboratore profilo CDN** ruolo, hello **utenti** pannello per il gruppo di risorse dovrebbe essere simile toothis.

![Pannello Utenti](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>Autenticazione utente interattiva
Se, invece di un'entità servizio, invece si desidera utilizzare l'autenticazione utente interattivo, il processo di hello è molto simile toothat per un'entità servizio.  In effetti, sarà necessario toofollow hello stessa procedura, ma alcune modifiche minori.

> [!IMPORTANT]
> Solo, seguire questa procedura se si sceglie l'autenticazione utente toouse anziché un'entità servizio.
>
>

1. Quando si crea l'applicazione, invece di **Applicazione Web** scegliere **Applicazione nativa**.

    ![Applicazione nativa](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. Nella pagina successiva di hello, verrà richiesto di immettere un **URI di reindirizzamento**.  Hello URI non verrà convalidato, ma tenere presente i valori immessi.  Sarà necessario più avanti.
3. Nessun toocreate necessità è un **chiave di autenticazione client**.
4. Invece di assegnare un toohello dell'entità servizio **collaboratore profilo CDN** ruolo, verrà tooassign singoli utenti o gruppi.  In questo esempio, si noterà che è stato assegnato *utente Demo CDN* toohello **collaboratore profilo CDN** ruolo.  

    ![Accesso del singolo utente](./media/cdn-app-dev-prep/cdn-aad-user-include.png)
