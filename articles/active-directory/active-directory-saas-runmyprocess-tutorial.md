---
title: 'Esercitazione: Integrazione di Azure Active Directory con RunMyProcess | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e RunMyProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a>Esercitazione: Integrazione di Azure Active Directory con RunMyProcess

In questa esercitazione, è illustrato come toointegrate RunMyProcess con Azure Active Directory (Azure AD).

Integrazione di RunMyProcess con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooRunMyProcess
- È possibile abilitare l'utenti tooautomatically get connesso tooRunMyProcess (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con RunMyProcess tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di RunMyProcess abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di RunMyProcess dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-runmyprocess-from-hello-gallery"></a>Aggiunta di RunMyProcess dalla raccolta hello
integrazione hello tooconfigure di RunMyProcess in Azure AD, è necessario tooadd RunMyProcess dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd RunMyProcess dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **RunMyProcess**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. Nel riquadro dei risultati hello, selezionare **RunMyProcess**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con RunMyProcess in base a un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in RunMyProcess è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in RunMyProcess deve toobe stabilita.

In RunMyProcess, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con RunMyProcess, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave un equivalente di Britta Simon in RunMyProcess che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione RunMyProcess.

**Azure AD tooconfigure single sign-on con RunMyProcess, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **RunMyProcess** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. In hello **RunMyProcess dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://live.runmyprocess.com/live/<tenant id>`

    > [!NOTE] 
    > il valore di Hello non è di tipo real. Il valore di hello aggiornamento con hello URL effettivo Sign-On. Contatto [team di supporto Client di RunMyProcess](mailto:support@runmyprocess.com) valore hello tooget. 

4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. In hello **RunMyProcess configurazione** fare clic su **configurare RunMyProcess** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. In una finestra del web browser, accesso tooyour tenant di RunMyProcess come amministratore.

8. Nel pannello di spostamento a sinistra fare clic su **Account** e selezionare **Configuration** (Configurazione).
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. Andare troppo**metodo di autenticazione** sezione ed eseguire i passaggi successivi:
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    a. In **Metodo** selezionare **SSO con Samlv2**. 

    b. In hello **reindirizzamento SSO** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.

    c. In hello **reindirizzamento disconnessione** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.

    d. In hello **formato Id nome** casella di testo, hello tipo valore **Name Identifier Format** come **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: emailAddress**.

    e. Copiare il contenuto di hello hello scaricato del file di certificato e quindi incollarlo hello **certificato** casella di testo. 
 
    f. Fare clic sull'icona di **salvataggio**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-runmyprocess-test-user"></a>Creazione di un utente test di RunMyProcess

In ordine tooenable Azure AD utenti toolog in tooRunMyProcess, è necessario eseguirne il provisioning in RunMyProcess. Nel caso di hello di RunMyProcess, il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour sito della società RunMyProcess come amministratore.

2. Nel pannello di spostamento a sinistra fare clic su **Account** e selezionare **Users** (Utenti), quindi fare clic su **New User** (Nuovo utente).
   
    ![Nuovo utente](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Nuovo utente")

3. In hello **impostazioni utente** seguire hello alla procedura seguente:
   
    ![Profilo](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profilo") 
  
    a. Hello tipo **nome** e **posta elettronica** di Azure un valido relative all'account di Active Directory desiderata tooprovision in hello nelle caselle di testo. 

    b. Selezionare una **lingua IDE**, una **lingua** e un **profilo**. 

    c. Selezionare **inviare toome di posta elettronica di creazione account**. 

    d. Fare clic su **Salva**.
   
    >[!NOTE]
    >È possibile usare qualsiasi altro RunMyProcess utente account strumento di creazione o le API fornite da RunMyProcess tooprovision Azure Active Directory gli account utente. 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRunMyProcess.

![Assegna utente][200] 

**tooassign Britta Simon tooRunMyProcess, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **RunMyProcess**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.

Quando si fa clic hello RunMyProcess riquadro in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in RunMyProcess applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

