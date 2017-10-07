---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jobscience | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Jobscience.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a>Esercitazione: Integrazione di Azure Active Directory con Jobscience

In questa esercitazione, è illustrato come toointegrate Jobscience con Azure Active Directory (Azure AD).

Integrazione di Jobscience con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooJobscience
- È possibile abilitare l'utenti tooautomatically get connesso tooJobscience (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Jobscience tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Jobscience abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Jobscience dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-jobscience-from-hello-gallery"></a>Aggiunta di Jobscience dalla raccolta hello
integrazione hello tooconfigure di Jobscience in Azure AD, è necessario tooadd Jobscience dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Jobscience dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Jobscience**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. Nel riquadro dei risultati hello, selezionare **Jobscience**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Jobscience in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Jobscience è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Jobscience richiede toobe stabilita.

In Jobscience, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure single sign-on AD con Jobscience, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Jobscience](#creating-a-jobscience-test-user)**  -toohave un equivalente di Britta Simon in Jobscience che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Jobscience.

**Azure AD tooconfigure single sign-on con Jobscience, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Jobscience** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. In hello **Jobscience dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`http://<company name>.my.salesforce.com`
    
    > [!NOTE] 
    > Poiché non è reale, Aggiorna il valore con hello URL effettivo Sign-On. Ottenere questo valore per [team di supporto Client di Jobscience](https://www.jobscience.com/support) o dal profilo SSO hello si creeranno descritta più avanti nell'esercitazione di hello. 
 
4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. In hello **Jobscience configurazione** fare clic su **configurare Jobscience** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. Accedi tooyour sito della società Jobscience come amministratore.

8. Andare troppo**installazione**.
   
   ![Installazione](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Installazione")

9. Nel riquadro di spostamento a sinistra, hello hello **Amministra** fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain** hello tooopen  **Il mio dominio** pagina. 
   
   ![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")

10. tooverify che il dominio è stato configurato correttamente, assicurarsi che sia in "**passaggio 4 distribuito tooUsers**" ed esaminare il "**impostazioni dominio personali**".

    ![Dominio distribuito tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser distribuite del dominio")

11. Nel sito della società Jobscience hello scegliere **controlli di sicurezza**, quindi fare clic su **Single Sign-On Settings**.
    
    ![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")

12. In hello **Single Sign-On Settings** seguire hello alla procedura seguente:
    
    ![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")
    
    a. Selezionare **Abilitato SAML**.

    b. Fare clic su **New**.

13. In hello **SAML Single Sign-On Setting Edit** finestra di dialogo, eseguire hello alla procedura seguente:
    
    ![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")
    
    a. In hello **nome** casella di testo, digitare un nome per la configurazione.

    b. In **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.

    c. In hello **Id entità** casella di testo, tipo`https://salesforce-jobscience.com`

    d. Fare clic su **Sfoglia** tooupload il certificato di Azure AD.

    e. Come **tipo di identità SAML**selezionare **l'asserzione contiene l'ID di federazione di hello dall'oggetto utente hello**.

    f. Come **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentfier hello di hello Subject statement**.

    g. In **Identity Provider Login URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.

    h. In **Identity Provider Logout URL** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.

    i. Fare clic su **Salva**.

14. Nel riquadro di spostamento a sinistra, hello hello **Amministra** fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain** hello tooopen  **Il mio dominio** pagina. 
    
    ![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")

15. In hello **My Domain** pagina hello **personalizzazione pagina di accesso** fare clic su **modifica**.
    
    ![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")

16. In hello **personalizzazione pagina di accesso** pagina hello **servizio di autenticazione** sezione, il nome di hello del **SAML SSO Settings** viene visualizzato. Selezionarlo e quindi fare clic su **Save**.
    
    ![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")

17. hello tooget SP ha avviato l'accesso Single Sign, fare clic su URL di accesso su hello **impostazioni Single Sign-On** in hello **controlli di sicurezza** sezione del menu.

    ![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")
    
    Fare clic su profilo SSO hello creato nel passaggio hello precedente. Questa pagina vengono visualizzati hello Single Sign in URL per l'azienda (ad esempio, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).    

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-jobscience-test-user"></a>Creazione di un utente test di Jobscience

In ordine tooenable Azure AD utenti toolog in tooJobscience, è necessario eseguirne il provisioning in Jobscience. Nel caso di hello di Jobscience, il provisioning è un'attività manuale.

>[!NOTE]
>È possibile usare qualsiasi altro Jobscience utente account strumento di creazione o le API fornite da Jobscience tooprovision Azure Active Directory gli account utente.
>  
        
**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Accedi tooyour **Jobscience** sito aziendale come amministratore.

2. Passare tooSetup.
   
   ![Installazione](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Installazione")
3. Andare troppo**Gestisci utenti \> utenti**.
   
   ![Utenti](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Utenti")
4. Fare clic su **Nuovo utente**.
   
   ![Tutti gli utenti](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Tutti gli utenti")
5. In hello **modifica utente** finestra di dialogo, eseguire hello alla procedura seguente:
   
   ![Modifica dell'utente](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Modifica dell'utente")
   
   a. In hello **nome** casella di testo, digitare un nome dell'utente hello come Laura.
   
   b. In hello **cognome** casella di testo, specificare un cognome dell'utente hello come Simon.
   
   c. In hello **Alias** casella di testo, digitare un nome di alias dell'utente hello come brittas.

   d. In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.

   e. In hello **nome utente** , digitare un nome utente dell'utente come Brittasimon@contoso.com.

   f. In hello **nome alternativo** casella di testo, digitare un nome alternativo dell'utente come Simon.

   g. Fare clic su **Salva**.

    
> [!NOTE]
> titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica e segue il proprio account tooconfirm un collegamento prima che diventi attivo.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooJobscience.

![Assegna utente][200] 

**tooassign Britta Simon tooJobscience, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Jobscience**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Jobscience hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Jobscience applicazione.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

