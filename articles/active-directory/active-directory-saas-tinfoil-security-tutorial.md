---
title: 'Esercitazione: Integrazione di Azure Active Directory con TINFOIL SECURITY | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TINFOIL SECURITY.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>Esercitazione: Integrazione di Azure Active Directory con TINFOIL SECURITY

In questa esercitazione, è illustrato come toointegrate TINFOIL SECURITY con Azure Active Directory (Azure AD).

Integrazione di TINFOIL SECURITY con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooTINFOIL, sicurezza
- È possibile abilitare l'utenti tooautomatically get connesso tooTINFOIL sicurezza (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con TINFOIL SECURITY tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di TINFOIL SECURITY abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiungere TINFOIL SECURITY dalla raccolta di hello
2. Configurare e testare l'accesso Single Sign-On di Azure AD

## <a name="add-tinfoil-security-from-hello-gallery"></a>Aggiungere TINFOIL SECURITY dalla raccolta di hello
integrazione hello tooconfigure di TINFOIL SECURITY in Azure AD, è necessario tooadd TINFOIL SECURITY dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd TINFOIL SECURITY dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **TINFOIL SECURITY**selezionare **TINFOIL SECURITY** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![TINFOIL SECURITY dalla raccolta](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TINFOIL SECURITY con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in TINFOIL SECURITY è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in TINFOIL SECURITY richiede toobe stabilita.

In TINFOIL SECURITY, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con TINFOIL SECURITY, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente di test di TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave un equivalente di Britta Simon in TINFOIL SECURITY che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione TINFOIL SECURITY.

**Azure AD tooconfigure single sign-on con TINFOIL SECURITY, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **TINFOIL SECURITY** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Accesso basato su SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. In hello **TINFOIL SECURITY dominio e gli URL** sezione, hello utente non dispone di tooperform tutte le operazioni come l'applicazione hello è già pre-integrata con Azure.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore.

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. mapping di attributi tooadd hello necessario, eseguire hello alla procedura seguente:
    
    ![Attributi](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributi")
    
    | Nome attributo    |   Valore attributo |
    | ------------------- | -------------------- |
    | accountid | UXXXXXXXXXXXXX |
    
    a. Fare clic su **Aggiungi attributo utente**.
    
    ![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")
    
    ![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")
    
    b. In hello **nome dell'attributo** casella tipo **accountid**.
    
    c. In hello **valore dell'attributo** casella di testo, incollare hello ID valore dell'account che verrà visualizzato in un secondo momento esercitazione hello.
    
    d. Fare clic su **OK**.    

6. Fare clic sul pulsante **Salva** .

    ![Pulsante per il salvataggio](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. In hello **TINFOIL SECURITY Configuration** fare clic su **configurare TINFOIL SECURITY** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurazione di TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. In un'altra finestra del Web browser accedere al sito aziendale TINFOIL SECURITY come amministratore.

9. Nella barra degli strumenti hello in primo piano hello, fare clic su **Account personale**.
   
    ![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")

10. Fare clic su **Security**.
   
    ![Sicurezza](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Sicurezza")

11. In hello **Single Sign-On** configurazione eseguire hello alla procedura seguente:
   
    ![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")
   
    a. Selezionare **Enable SAML**.
   
    b. Fare clic su **Configurazione manuale**.
   
    c. In **SAML Post URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure
   
    d. In **SAML Certificate Fingerprint** casella di testo, hello Incolla valore **identificazione personale** che è stato copiato da **certificato di firma SAML** sezione.
  
    e. Copia **Your Account ID** valore e incollare il valore di hello in **valore dell'attributo** casella di testo in **Aggiungi attributo** sezione nel portale di Azure.
   
    f. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Utenti e gruppi -> Tutti gli utenti ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Utente](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-a-tinfoil-security-test-user"></a>Creare un utente test di TINFOIL SECURITY

In ordine tooenable Azure AD utenti toolog a TINFOIL SECURITY, è necessario eseguirne il provisioning in TINFOIL SECURITY. Nel caso di hello di TINFOIL SECURITY, il provisioning è un'attività manuale.

**tooget viene eseguito il provisioning, eseguire hello alla procedura seguente:**

1. Se l'utente hello fa parte di un account aziendale, è necessario troppo[contattare il team di supporto di TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) account utente di hello tooget creato.

2. Se l'utente di hello è un normale utente SaaS di TINFOIL SECURITY, utente hello aggiungere tooany un collaboratore del sito hello dell'utente. Questo trigger toosend un processo specificato toohello un invito tramite posta elettronica toocreate un nuovo account utente TINFOIL SECURITY.

> [!NOTE]
> È possibile usare qualsiasi altro TINFOIL SECURITY utente account strumento di creazione o le API fornite da TINFOIL SECURITY tooprovision degli account utente di Azure AD.
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTINFOIL sicurezza.

![Assegna utente][200] 

**tooassign Britta Simon tooTINFOIL protezione, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **TINFOIL SECURITY**.

    ![selezionare TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro TINFOIL SECURITY hello in hello Pannello di accesso, è necessario ottenere applicazione TINFOIL SECURITY tooyour automaticamente firmato-on. Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

