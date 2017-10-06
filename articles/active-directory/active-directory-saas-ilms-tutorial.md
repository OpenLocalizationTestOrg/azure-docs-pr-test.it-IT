---
title: 'Esercitazione: integrazione di Azure Active Directory con iLMS | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e iLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>Esercitazione: Integrazione di Azure Active Directory con iLMS

In questa esercitazione, è illustrato come iLMS toointegrate con Azure Active Directory (Azure AD).

Integrazione iLMS con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooiLMS
- È possibile abilitare l'utenti tooautomatically get connesso tooiLMS (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con iLMS tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di iLMS abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di iLMS dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-ilms-from-hello-gallery"></a>Aggiunta di iLMS dalla raccolta hello
integrazione hello tooconfigure di iLMS in Azure AD, è necessario iLMS tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.

**iLMS tooadd dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **iLMS**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. Nel riquadro dei risultati hello, selezionare **iLMS**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con iLMS in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in iLMS è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in iLMS deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in iLMS.

tooconfigure e prova AD Azure single sign-on con iLMS, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test iLMS](#creating-an-ilms-test-user)**  -toohave un equivalente di Britta Simon in iLMS toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione iLMS.

**Azure AD tooconfigure single sign-on con iLMS, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **iLMS** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. In hello **iLMS dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    a. In hello **identificatore** casella di testo, incollare hello **identificatore** valore copiate da **Provider di servizi** sezione delle impostazioni di SAML nel portale di amministrazione iLMS.

    b. In hello **URL di risposta** casella di testo, incollare hello **Endpoint (URL)** valore copiate da **Provider di servizi** sezione delle impostazioni di SAML nel portale di amministrazione iLMS con seguente hello modello`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >Questo '123456' è un valore di esempio dell'identificatore.

4. Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    In hello **Sign-on URL** casella di testo, incollare hello **Endpoint (URL)** valore copiate da **Provider di servizi** sezione delle impostazioni di SAML nel portale di amministrazione iLMS come`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable JIT provisioning, iLMS prevista dall'applicazione asserzioni SAML hello in un formato specifico. Configurare hello seguendo le attestazioni per questa applicazione. È possibile gestire i valori hello di questi attributi da hello **gli attributi utente** sezione nella pagina di integrazione dell'applicazione. Hello seguente schermata mostra un esempio per questo oggetto.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/4.png)
    
    Creare **reparto, area** e **divisione** gli attributi e aggiungere il nome di hello di questi attributi in iLMS. Tutti gli attributi indicati sopra sono obbligatori.    

    > [!NOTE] 
    > Si dispone di tooenable **creare Account utente Un-recognized** in iLMS toomap questi attributi. Seguire le istruzioni di hello [qui](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget un'idea configurazione attributi hello.

6. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:
    
    | Nome attributo | Valore attributo |
    | ---------------| --------------- |    
    | divisione | user.department |
    | region | user.state |
    | department | user. jobtitle |

    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.
    
    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.
    
    d. Fare clic su **Ok**

7. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. In una finestra del web browser, accedere tooyour **il portale di amministrazione di iLMS** come amministratore.

10. Fare clic su **SSO:SAML** in **impostazioni** scheda Impostazioni SAML tooopen ed eseguire hello alla procedura seguente:
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/1.png) 

    a. Espandere hello **Provider di servizi** hello sezione e copia **identificatore** e **Endpoint (URL)** valore.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. Nella sezione **Provider di identità** fare clic su **Import metadata** (Importa metadati).
    
    c. Seleziona hello **metadati** file scaricato dal portale di Azure dalla **certificato di firma SAML** sezione.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. Se si desidera tooenable JIT provisioning toocreate iLMS account per annullare-riconosce gli utenti, seguire i passaggi seguenti:
        
       - Selezionare **Create Un-recognized User Account** (Crea account utente non riconosciuto).
       
       ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Eseguire il mapping di attributi hello in Azure AD con attributi hello in iLMS. Nella colonna attributo hello, specificare gli attributi hello hello nome o il valore predefinito.

    e. Andare troppo**regole Business** scheda ed eseguire hello alla procedura seguente: 
        
       ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/5.png)

       - Controllare **creare aree Un-recognized, divisioni e i reparti** toocreate aree, divisioni e i reparti che non esistono già in fase di hello di Single Sign-on.
        
       - Controllare **profilo utente aggiornamento durante Accedi** toospecify se hello del profilo utente viene aggiornata con ogni Single Sign-on. 
        
       - Se hello **"Aggiornamento vuoto valori per Non campi nel profilo utente obbligatorio"** opzione è selezionata, i campi facoltativi profilo vuoti al momento dell'accesso verrà inoltre causano hello iLMS profilo utente toocontain valori vuoti per i campi.
        
       - Controllare **inviare posta elettronica di notifica di errore** e immettere la posta elettronica hello dell'utente hello in cui si desidera tooreceive hello errore notifica tramite posta elettronica.

11. Fare clic su **salvare** pulsante Impostazioni hello toosave.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-an-ilms-test-user"></a>Creazione di un utente test di iLMS

L'applicazione supporta solo in tempo il provisioning dell'utente e dopo l'autenticazione degli utenti viene creato automaticamente in un'applicazione hello. JIT funzionerà, se si è scelto di hello **creare Account utente Un-recognized** casella di controllo durante l'impostazione di configurazione SAML nel portale di amministrazione iLMS.

Se è necessario un utente toocreate manualmente, quindi seguire i passaggi successivi:

1. Accedere nel sito della società di tooyour iLMS come amministratore.

2. Fare clic su **"Registrazione utente"** in **utenti** scheda tooopen **registrazione utente** pagina. 
   
   ![Aggiungere un dipendente](./media/active-directory-saas-ilms-tutorial/3.png)

3. In hello **"Registrazione utente"** eseguire hello alla procedura seguente.

    ![Aggiungere un dipendente](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    a. In hello **nome** casella Tipo hello Laura nome.
   
    b. In hello **cognome** casella di testo, hello tipo cognome Simon.

    c. In hello **ID di posta elettronica** casella di testo, digitare hello indirizzo di posta elettronica dell'account di Britta Simon.

    d. In hello **area** elenco a discesa valore selezionare hello per area.

    e. In hello **divisione** elenco a discesa valore selezionare hello per la divisione.

    f. In hello **reparto** elenco a discesa valore selezionare hello per reparto.

    g. Fare clic su **Salva**.

    > [!NOTE] 
    > È possibile inviare toouser di posta elettronica di registrazione selezionando **invia messaggi di registrazione** casella di controllo.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooiLMS proprio accesso.

![Assegna utente][200] 

**tooassign Britta Simon tooiLMS, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **iLMS**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello iLMS riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour iLMS applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

