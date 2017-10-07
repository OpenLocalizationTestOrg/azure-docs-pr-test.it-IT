---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zscaler Two| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Zscaler Two.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1fd8a940-7320-47e0-a176-2dd4eeca6db2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: dcd13d399f093f24a945f234401cd5b7e527ed34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-two"></a>Esercitazione: Integrazione di Azure Active Directory con Zscaler Two

In questa esercitazione, è illustrato come toointegrate Zscaler Two con Azure Active Directory (Azure AD).

Integrazione di Zscaler Two con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooZscaler due
- È possibile abilitare l'utenti tooautomatically get connesso tooZscaler due (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Zscaler Two tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Zscaler Two abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Zscaler Two dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-zscaler-two-from-hello-gallery"></a>Aggiunta di Zscaler Two dalla raccolta hello
integrazione hello tooconfigure di Zscaler Two in Azure AD, è necessario tooadd Zscaler Two dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Zscaler Two dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Zscaler Two**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_search.png)

5. Nel riquadro dei risultati hello, selezionare **Zscaler Two**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zscaler Two usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Zscaler Two è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Zscaler Two deve toobe stabilita.

In Zscaler Two, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure single sign-on AD con Zscaler Two, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Configurazione delle impostazioni proxy](#configuring-proxy-settings)**  -impostazioni del proxy tooconfigure hello in Internet Explorer
3. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
4. **[Creazione di un utente test Zscaler Two](#creating-a-zscaler-two-test-user)**  -toohave un equivalente di Britta Simon in Zscaler Two che è la rappresentazione toohello collegato Azure AD dell'utente.
5. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
6. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Zscaler Two.

**Azure AD tooconfigure single sign-on con Zscaler Two, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Zscaler Two** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_samlbase.png)

3. In hello **Zscaler due dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_url.png)

   Nella casella di testo URL accesso hello digitare l'URL di hello usato da tooyour il toosign a utenti dell'applicazione ZScaler Two.

    > [!NOTE] 
    > Si dispone di tooupdate questo valore con hello URL effettivo Sign-On. Contatto [team di supporto di Zscaler due Client](https://www.zscaler.com/company/contact) tooget questi valori.

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_400.png)

6. In hello **configurazione con due Zscaler** fare clic su **configurare Zscaler Two** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_configure.png) 

7. In una finestra del web browser, accedere come amministratore nel sito della società ZScaler Two tooyour.

8. Scegliere dal menu hello in primo piano hello **amministrazione**.
   
    ![Amministrazione](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Amministrazione")

9. In **Manage Administrators & Roles** (Gestisci amministratori e ruoli) fare clic su **Manage Users & Authentication** (Gestisci utenti e autenticazione).   
            
    ![Gestire utenti e autenticazione](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Gestire utenti e autenticazione")

10. In hello **scegliere le opzioni di autenticazione per l'organizzazione** seguire hello alla procedura seguente:   
                
    ![Autenticazione](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Autenticazione")
   
    a. Selezionare **Authenticate using SAML Single Sign-On**.

    b. Fare clic su **Configure SAML Single Sign-On Parameters**.

11. In hello **Configure SAML Single Sign-On Parameters** pagina eseguire hello alla procedura seguente e quindi fare clic su **eseguita**

    ![Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Single Sign-On")
    
    a. Hello Incolla **SAML Single Sign-On Service URL** valore, che è stato copiato dal portale di Azure hello in hello **URL utenti toowhich del portale SAML hello vengono inviati per l'autenticazione** casella di testo.
    
    b. In hello **attributo che contiene il nome di account di accesso** casella tipo **NameID**.
    
    c. tooupload il certificato scaricato, fare clic su **Zscaler pem**.
    
    d. Selezionare **Enable SAML Auto-Provisioning**.

12. In hello **Configure User Authentication** finestra di dialogo eseguire hello alla procedura seguente:

    ![Amministrazione](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Amministrazione")
    
    a. Fare clic su **Salva**.

    b. Fare clic su **Attiva subito**.

## <a name="configuring-proxy-settings"></a>Configurazione delle impostazioni proxy
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>impostazioni del proxy in Internet Explorer tooconfigure hello

1. Avviare **Internet Explorer**.

2. Selezionare **Opzioni Internet** da hello **strumenti** menu per aprire hello **Opzioni Internet** finestra di dialogo.   
    
     ![Opzioni Internet](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Opzioni Internet")

3. Fare clic su hello **connessioni** scheda.   
  
     ![Connessioni](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Connessioni")

4. Fare clic su **impostazioni LAN** tooopen hello **impostazioni LAN** finestra di dialogo.

5. Nella sezione server Proxy hello, eseguire hello alla procedura seguente:   
   
    ![Server proxy](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Server proxy")

    a. Selezionare **Usa un server proxy per la LAN**.

    b. Nella casella di testo indirizzo hello digitare **gateway.zscalertwo.net**.

    c. Nella casella di testo porta hello digitare **80**.

    d. Selezionare **Ignora server proxy per indirizzi locali**.

    e. Fare clic su **OK** tooclose hello **Impostazioni rete locale (LAN)** finestra di dialogo.

6. Fare clic su **OK** tooclose hello **Opzioni Internet** finestra di dialogo.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-zscaler-two-test-user"></a>Creazione di un utente di test di Zscaler Two

toolog agli utenti di Azure AD tooenable in due tooZScaler, devono essere sottoposte a provisioning tooZScaler due. Nel caso di hello di ZScaler Two, il provisioning è un'attività manuale.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:

1. Accedi tooyour **Zscaler Two** tenant.

2. Fare clic su **Administration**.   
   
    ![Amministrazione](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Amministrazione")

3. Fare clic su **User Management**.   
        
     ![Aggiungi](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Aggiungi")

4. In hello **utenti** scheda, fare clic su **Aggiungi**.
      
    ![Aggiungi](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Aggiungi")

5. Nella sezione Aggiungi utente hello, eseguire hello alla procedura seguente:
        
    ![Aggiungere un utente](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Aggiungere un utente")
   
    a. Hello tipo **UserID**, **nome visualizzato utente**, **Password**, **Conferma Password**, quindi selezionare **gruppi**hello e **reparto** di Azure un valido account di Active Directory, si desidera tooprovision.

    b. Fare clic su **Salva**.

> [!NOTE]
> È possibile usare qualsiasi altro ZScaler Two utente account strumento di creazione o le API fornite da ZScaler Two tooprovision degli account utente di Azure AD.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooZscaler due.

![Assegna utente][200] 

**tooassign Britta Simon tooZscaler Two, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Zscaler Two**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello riquadro Zscaler Two in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Zscaler Two.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_203.png

