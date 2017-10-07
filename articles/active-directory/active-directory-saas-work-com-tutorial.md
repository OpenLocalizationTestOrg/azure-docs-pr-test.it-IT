---
title: 'Esercitazione: Integrazione di Azure Active Directory con Work.com | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Work.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Esercitazione: Integrazione di Azure Active Directory con Work.com

In questa esercitazione, è illustrato come toointegrate Work.com con Azure Active Directory (Azure AD).

Integrazione di Work.com con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooWork.com
- È possibile abilitare l'utenti tooautomatically get connesso tooWork.com (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Work.com tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Work.com abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiungere Work.com dalla raccolta di hello
2. Configurare e testare l'accesso Single Sign-On di Azure AD

## <a name="add-workcom-from-hello-gallery"></a>Aggiungere Work.com dalla raccolta di hello
integrazione hello tooconfigure di Work.com in Azure AD, è necessario tooadd Work.com dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Work.com dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Work.com**selezionare **Work.com** dal riquadro dei risultati, quindi scegliere **Aggiungi** pulsante applicazione hello tooadd.

    ![Aggiungere dalla raccolta](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Work.com usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Work.com è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Work.com deve toobe stabilita.

In Work.com, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Work.com, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Work.com](#create-a-workcom-test-user)**  -toohave un equivalente di Britta Simon in Work.com che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Work.com.

>[!NOTE]
>tooconfigure accesso single sign-on, è necessario un nome di dominio personalizzato Work.com toosetup ancora. È necessario almeno un dominio toodefine nome, verificare il nome di dominio e distribuirlo tooyour intera organizzazione.

**Azure AD tooconfigure single sign-on con Work.com, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Work.com** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Accesso basato su SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. In hello **Work.com dominio e gli URL** sezione, eseguire l'esempio hello:

    ![Sezione URL e dominio Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`http://<companyname>.my.salesforce.com`

    > [!NOTE] 
    > Poiché non è reale, Aggiorna il valore con hello URL effettivo Sign-On. Contatto [team di supporto Client di Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget questo valore. 

4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante per il salvataggio](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. In hello **Work.com configurazione** fare clic su **configurare Work.com** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Sezione Configurazione di Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. Accedi tooyour tenant di Work.com come amministratore.

8. Andare troppo**installazione**.
   
    ![Installazione](./media/active-directory-saas-work-com-tutorial/ic794108.png "Installazione")

9. Nel riquadro di spostamento a sinistra, hello hello **Amministra** fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain** hello tooopen  **Il mio dominio** pagina. 
   
    ![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")

10. tooverify che il dominio è stato configurato correttamente, assicurarsi che sia in "**passaggio 4 distribuito tooUsers**" ed esaminare il "**impostazioni dominio personali**".
   
    ![Dominio distribuito tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser distribuite del dominio")

11. Accedi tooyour tenant di Work.com.

12. Andare troppo**installazione**.
    
    ![Installazione](./media/active-directory-saas-work-com-tutorial/ic794108.png "Installazione")

13. Espandere hello **controlli di sicurezza** menu e quindi fare clic su **Single Sign-On Settings**.
    
    ![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")

14. In hello **Single Sign-On Settings** finestra di dialogo eseguire hello alla procedura seguente:
    
    ![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")
    
    a. Selezionare **Abilitato SAML**.
    
    b. Fare clic su **New**.

15. In hello **SAML Single Sign-On Settings** seguire hello alla procedura seguente:
    
    ![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")
    
    a. In hello **nome** casella di testo, digitare un nome per la configurazione.  
       
    > [!NOTE]
    > Fornisce un valore per **nome** popolare automaticamente hello **nome API** casella di testo.
    
    b. In **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.
    
    c. certificato di tooupload hello scaricato dal portale di Azure, fare clic su **Sfoglia**.
    
    d. In hello **Id entità** casella tipo `https://salesforce-work.com`.
    
    e. Come **tipo di identità SAML**selezionare **l'asserzione contiene l'ID di federazione di hello dall'oggetto utente hello**.
    
    f. Come **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentfier hello di hello Subject statement**.
    
    g. In **Identity Provider Login URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.

    h. In **Identity Provider Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.
    
    i. In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP Post**.
    
    j. Fare clic su **Salva**.

16. Nel portale classico a Work.com, nel riquadro di spostamento a sinistra di hello, fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain** tooopen hello **My Domain**pagina. 
    
    ![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")

17. In hello **My Domain** pagina hello **personalizzazione pagina di accesso** fare clic su **modifica**.
    
    ![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")

14. In hello **personalizzazione pagina di accesso** pagina hello **servizio di autenticazione** sezione, il nome di hello del **SAML SSO Settings** viene visualizzato. Selezionarlo e quindi fare clic su **Save**.
    
    ![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Utenti e gruppi -> Tutti gli utenti](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Add](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-a-workcom-test-user"></a>Creare un utente di test di Work.com
Per Azure Active Directory gli utenti toobe in grado di toosign in devono essere tooWork.com provisioning. Nel caso di hello di Work.com, il provisioning è un'attività manuale.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:
1. Accesso tooyour sito della società Work.com come amministratore.

2. Andare troppo**installazione**.
   
    ![Installazione](./media/active-directory-saas-work-com-tutorial/IC794108.png "Installazione")
3. Andare troppo**Gestisci utenti \> utenti**.
   
    ![Gestione utenti](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gestione utenti")

4. Fare clic su **Nuovo utente**.
   
    ![Tutti gli utenti](./media/active-directory-saas-work-com-tutorial/IC794117.png "Tutti gli utenti")

5. Nella sezione User Edit hello, eseguire hello alla procedura seguente, negli attributi di un valido di Azure nelle caselle di testo relative all'account di Active Directory desiderata tooprovision in hello:
   
    ![Modifica dell'utente](./media/active-directory-saas-work-com-tutorial/ic794118.png "Modifica dell'utente")
   
    a. In hello **nome** casella di testo, hello tipo **nome** dell'utente hello **Laura**.
    
    b. In hello **cognome** casella di testo, hello tipo **cognome** dell'utente hello **Simon**.
    
    c. In hello **Alias** casella di testo, hello tipo **nome** dell'utente hello **BrittaS**.
    
    d. In hello **posta elettronica** casella di testo, hello tipo **indirizzo di posta elettronica** dell'utente  **Brittasimon@contoso.com** .
    
    e. In hello **nome utente** , digitare un nome utente dell'utente come  **Brittasimon@contoso.com** .
    
    f. In hello **nome alternativo** casella di testo, digitare un **nome alternativo** dell'utente **Simon**.
    
    g. Selezionare **Role** (Ruolo), **User License**(Licenza utente) e **Profile** (Profilo).
    
    h. Fare clic su **Salva**.  
      
    > [!NOTE]
    > titolare dell'account di Azure AD di Hello riceverà un messaggio di posta elettronica tra un account di hello tooconfirm collegamento prima che diventi attivo.
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWork.com.

![Assegna utente][200] 

**tooassign Britta Simon tooWork.com, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Work.com**.

    ![Work.com nell'elenco delle app](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Work.com hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Work.com applicazione.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

