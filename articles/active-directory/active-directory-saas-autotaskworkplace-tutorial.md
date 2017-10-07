---
title: 'Esercitazione: Integrazione di Azure Active Directory con Autotask Workplace | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Autotask all'area di lavoro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a>Esercitazione: Integrazione di Azure Active Directory con Autotask Workplace

In questa esercitazione, è illustrato come toointegrate Autotask all'area di lavoro con Azure Active Directory (Azure AD).

Integrazione Autotask all'area di lavoro con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooAutotask all'area di lavoro
- È possibile abilitare l'utenti tooautomatically get connesso tooAutotask all'area di lavoro (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con Autotask all'area di lavoro, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Autotask Workplace abilitata per l'accesso Single Sign-On
- È necessario essere un amministratore o un amministratore con privilegi avanzati in Workplace.
- È necessario un account amministratore hello Azure AD.
- utenti Hello che utilizzano questa funzionalità devono avere un account all'interno di hello Azure AD e luogo di lavoro e i relativi indirizzi di posta elettronica per entrambi devono corrispondere.

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta all'area di lavoro Autotask dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-autotask-workplace-from-hello-gallery"></a>Aggiunta all'area di lavoro Autotask dalla raccolta hello
integrazione hello tooconfigure di Autotask all'area di lavoro in Azure AD, è necessario tooadd Autotask all'area di lavoro dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Autotask all'area di lavoro Raccolta hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Autotask all'area di lavoro**selezionare **Autotask all'area di lavoro** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Nell'elenco dei risultati Autotask all'area di lavoro in hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Autotask Workplace usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nell'area di lavoro Autotask è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nell'area di lavoro Autotask deve toobe stabilita.

Nell'area di lavoro Autotask, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Autotask all'area di lavoro, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente di test all'area di lavoro Autotask](#create-an-autotask-workplace-test-user)**  -toohave un equivalente di Britta Simon Autotask area di lavoro che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Autotask all'area di lavoro.

**Azure AD tooconfigure single sign-on con Autotask all'area di lavoro, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Autotask all'area di lavoro** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. Se si desidera un'applicazione hello tooconfigure in **IDP** , modalità iniziata da eseguire hello seguendo i passaggi hello **Autotask all'area di lavoro dominio e gli URL** sezione:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Autotask Workplace per IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`

4. Se si desidera in un'applicazione hello tooconfigure **SP** modalità avviata, controllo **Mostra URL impostazioni avanzate** ed eseguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Autotask Workplace per SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.awp.autotask.net/loginsso`
     
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. Contatto [team di supporto Client all'area di lavoro Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget questi valori. 

5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. In una finestra del web browser, l'accesso utilizzando Online tooWorkplace hello le credenziali di amministratore.

    >[!Note]
    >Quando si configura hello IdP, un sottodominio sarà necessario toobe specificato. tooconfirm hello corretto sottodominio tooWorkplace accesso Online. Una volta effettuato l'accesso, è possibile apportare sottodominio toohello nota in hello URL.
    >sottodominio Hello fa parte di hello tra hello "https://" e ".awp.autotask.net/" e deve essere Stati Uniti, Europa, autorità di certificazione o Australia.

8. Andare troppo**configurazione** > **Single Sign-On** ed eseguire hello alla procedura seguente:

    ![Configurazione Single Sign-On per Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    a. Seleziona hello **File di metadati XML** opzione e quindi caricare hello **Metadata XML** scaricato dal portale di Azure.

    b. Fare clic su **Enable SSO** (Abilita SSO).
    
    ![Approvazione della configurazione Single Sign-On per Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    c. Seleziona hello **verificare queste informazioni siano corrette e il provider di identità attendibili** casella di controllo.

    d. Fare clic su **Approve** (Approva).
     
>[!Note]
>Se si richiede assistenza nella configurazione Autotask all'area di lavoro, vedere [questa pagina](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistenza con l'account aziendale.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.

### <a name="create-an-autotask-workplace-test-user"></a>Creare un utente di test di Autotask Workplace

In questa sezione viene creato un utente di nome Britta Simon in Autotask. Rivolgersi [team di supporto all'area di lavoro Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd utenti hello hello piattaforma Autotask all'area di lavoro.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAutotask all'area di lavoro.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooAutotask all'area di lavoro, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Autotask all'area di lavoro**.

    ![collegamento all'area di lavoro Autotask nell'elenco delle applicazioni hello Hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello all'area di lavoro Autotask riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Autotask all'area di lavoro.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

