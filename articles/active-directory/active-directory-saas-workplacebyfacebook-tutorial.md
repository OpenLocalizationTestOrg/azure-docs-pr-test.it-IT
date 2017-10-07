---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e all'area di lavoro da Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook

In questa esercitazione, è illustrato come toointegrate all'area di lavoro da Facebook con Azure Active Directory (Azure AD).

L'integrazione all'area di lavoro da Facebook con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooWorkplace da Facebook
- È possibile abilitare l'utenti tooautomatically get connesso tooWorkplace da Facebook (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con area di lavoro da Facebook tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione di Workplace by Facebook abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta all'area di lavoro da Facebook dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>Aggiunta all'area di lavoro da Facebook dalla raccolta hello
integrazione hello tooconfigure di lavoro da Facebook in Azure AD, è necessario tooadd all'area di lavoro da Facebook dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd all'area di lavoro da Facebook dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **all'area di lavoro da Facebook**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. Nel riquadro dei risultati hello, selezionare **all'area di lavoro da Facebook**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workplace by Facebook usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nell'area di lavoro da Facebook è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello nell'area di lavoro da Facebook deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nell'area di lavoro da Facebook.

tooconfigure e prova AD Azure single sign-on con area di lavoro da Facebook, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Configurazione di frequenza di riautenticazione](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt di lavoro per un controllo di SAML.
3. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
4. **[Creazione di una rete aziendale da Facebook test utente](#creating-a-workplace-by-facebook-test-user)**  -toohave un equivalente di Britta Simon nell'area di lavoro da Facebook che è la rappresentazione toohello collegato Azure AD dell'utente.
5. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
6. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'area di lavoro dall'applicazione Facebook.

**Azure AD tooconfigure single sign-on con all'area di lavoro da Facebook, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **all'area di lavoro da Facebook** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. In hello **all'area di lavoro al dominio di Facebook e URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<instancename>.facebook.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > Questi valori non sono hello reale. Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [all'area di lavoro dal team di supporto Client di Facebook](https://workplace.fb.com/faq/) tooget questi valori. 

4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. In hello **all'area di lavoro dalla configurazione di Facebook** fare clic su **configurare all'area di lavoro da Facebook** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. In una finestra del web browser, account di accesso tooyour all'area di lavoro dal sito della società di Facebook come amministratore.
  
   > [!NOTE] 
   > Come parte del processo di autenticazione SAML hello, all'area di lavoro può utilizzare le stringhe di query di backup too2.5 kilobyte in ordine toopass parametri tooAzure Active Directory.

8. In hello **Dashboard aziendali**, visitare toohello **autenticazione** scheda.

9. In **SAML Authentication**selezionare **SSO solo** dall'elenco a discesa hello.

10. I valori di input hello copiati da **all'area di lavoro dalla configurazione di Facebook** sezione del portale di Azure nei campi corrispondenti hello hello:

    *   In **SAML URL** casella di testo, hello Incolla valore **URL servizio Single Sign-On**, che è stato copiato dal portale di Azure.
    *   In **casella di testo URL autorità di certificazione SAML**, incollare il valore di hello di **ID entità SAML**, che è stato copiato dal portale di Azure.
    *   In **SAML Logout Redirect** (facoltativo), incollare il valore di hello di **Sign-Out URL**, che è stato copiato dal portale di Azure.
    *   Aprire il **certificato con codifica base 64** nel blocco note scaricato dal portale di Azure, copiarne contenuto hello negli Appunti e quindi incollarlo toothe **SAML Certificate** casella di testo.

11. Potrebbe essere necessario tooenter hello URL pubblico, URL destinatario, e l'URL ACS (servizio Consumer di asserzione) elencati in hello **configurazione SAML** sezione.

12. Scorrere nella parte inferiore toohello della sezione hello e fare clic su hello **SSO Test** pulsante. Si ottiene una finestra popup visualizzata con la pagina di accesso di Azure AD. Immettere le credenziali in come tooauthenticate normale. 

    **Risoluzione dei problemi:** indirizzo di posta elettronica hello verificare restituito da Azure AD è hello stesso hello account aziendale con cui si è connessi.

13. Una volta test hello è stato completato, scorrere toohello parte inferiore della pagina hello e fare clic su hello **salvare** pulsante.

14. Tutti gli utenti che usano Workplace visualizzeranno ora una pagina di accesso di Azure AD per l'autenticazione.

15. **Reindirizzamento disconnessione SAML (facoltativo)** - 

    È possibile scegliere toooptionally configurare un Url di disconnessione SAML, che può essere utilizzato toopoint nella pagina di disconnessione di Azure AD. Quando questa impostazione è abilitata e configurata, l'utente hello non saranno pagina di disconnessione toohello diretti all'area di lavoro. In alternativa, utente hello sarà reindirizzato toohello url che è stato aggiunto in base alle impostazioni di reindirizzamento disconnessione SAML hello.


> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>Configurazione della frequenza di riautenticazione

È possibile configurare tooprompt all'area di lavoro per un controllo SAML ogni giorno, tre giorni, settimane, due settimane, mesi o mai.

> [!NOTE] 
>Hello valore minimo per il controllo SAML hello in applicazioni per dispositivi mobili è impostata tooone settimana.

È inoltre possibile forzare un SAML reimpostare per tutti gli utenti utilizzando il pulsante hello: SAML richiedono l'autenticazione per tutti gli utenti ora.


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Creazione di un utente test di Workplace by Facebook

In questa sezione si crea un utente di nome Britta Simon in Workplace by Facebook. Workplace by Facebook supporta il provisioning JIT, abilitato per impostazione predefinita.

Non è necessaria alcuna azione dell'utente in questa sezione. Se un utente non esiste nell'area di lavoro da Facebook, una nuova istanza viene creata quando si tenta di tooaccess all'area di lavoro da Facebook.

>[!Note]
>Se è necessario toocreate manualmente, contattare l'utente [all'area di lavoro dal team di supporto Client di Facebook](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWorkplace da Facebook.

![Assegna utente][200] 

**tooassign tooWorkplace Britta Simon da Facebook, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **all'area di lavoro da Facebook**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configura provisioning utenti](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

