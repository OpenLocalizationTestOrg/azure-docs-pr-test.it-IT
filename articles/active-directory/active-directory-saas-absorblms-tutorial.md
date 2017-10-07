---
title: 'Esercitazione: Integrazione di Azure Active Directory con Absorb LMS | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e assorbire LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Esercitazione: Integrazione di Azure Active Directory con Absorb LMS

In questa esercitazione, è illustrato come toointegrate Absorb LMS con Azure Active Directory (Azure AD).

Integrazione di assorbire LMS con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooAbsorb LMS
- È possibile abilitare l'utenti tooautomatically get connesso tooAbsorb LMS (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere. [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con assorbire LMS tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Absorb LMS abilitata per l'accesso Single Sign-On.

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di assorbire LMS dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-absorb-lms-from-hello-gallery"></a>Aggiunta di assorbire LMS dalla raccolta hello
integrazione hello tooconfigure di assorbire LMS in tooAzure Active Directory, è necessario tooadd Absorb LMS dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Absorb LMS dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **assorbire LMS**selezionare **assorbire LMS** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Assorbire LMS nell'elenco risultati hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Absorb LMS usando un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in assorbire LMS è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello assorbire LMS deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in assorbire LMS.

tooconfigure e prova AD Azure single sign-on con assorbire LMS, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test assorbire LMS](#create-an-absorb-lms-test-user)**  -toohave un equivalente di Britta Simon in LMS assorbire che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione assorbire LMS.

**Azure AD tooconfigure single sign-on con assorbire LMS, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **assorbire LMS** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. In hello **assorbire LMS dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.myabsorb.com/Account/SAML`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > Questi valori non sono hello reale. Aggiornare questi valori con URL di risposta e identificatore effettivo hello. Contatto [team di supporto Client di LMS assorbire](https://www.absorblms.com/support) tooget questi valori. 

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. In hello **assorbire configurazione LMS** fare clic su **configurare LMS assorbire** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurazione di Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. In una finestra del web browser, accedere come amministratore nel sito della società di assorbire LMS tooyour.

9. Fare clic su hello **icona Account** sull'interfaccia di amministrazione di hello. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/1.png)

10. Fare clic su **Impostazioni portale**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Fare clic su hello **utenti** scheda.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Eseguire hello seguendo i passaggi tooaccess hello Single Sign-On i campi della configurazione:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/4.png)

    a. Seleziona hello appropriato **modalità**.

    b. Aprire hello certificato scaricato dal portale di Azure nel blocco note, hello rimuovere hello **---BEGIN CERTIFICATE---** e **---END CERTIFICATE---** tag e quindi incollare hello rimanente contenuto in Hello **chiave** casella di testo.
    
    c. In hello **Id proprietà**, selezionare hello attributo appropriato che è stato configurato come hello identificatore utente in hello Azure Active Directory (ad esempio, se viene selezionato userprinciplename hello in Azure AD, nome utente potrebbe essere selezionato qui).

    d. In hello **URL di accesso**, incollare hello **"SAML Single Sign-On Service URL"** valore copiato da hello **Configura sign-on** finestra di hello portale di Azure.

    e. In hello **Logout URL**, incollare hello **"Sign-Out URL"** valore copiato da hello **Configura sign-on** finestra di hello portale di Azure.

13. Abilitare **Only Allow SSO Login** (Consenti solo accesso SSO).

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/5.png)

14. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.

### <a name="create-an-absorb-lms-test-user"></a>Creare un utente di test di Absorb LMS

toolog agli utenti di Azure AD tooenable in tooAbsorb LMS, è necessario eseguirne il provisioning in tooAbsorb LMS.  
In Absorb LMS il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour sito della società assorbire LMS come amministratore.

2. Fare clic sulla scheda **Utenti** scheda.

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. Fare clic su **utenti** in hello **utenti** scheda.

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  Dal menu a discesa **Aggiungi nuovo** selezionare **Utente**.

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. In hello **Aggiungi utente** eseguire hello alla procedura seguente:

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/user.png)

    a. In hello **nome** casella di testo, nome del primo tipo hello come Laura.

    b. In hello **cognome** casella di testo, digitare hello cognome come Simon.
    
    c. In hello **Username** casella di testo, digitare il nome utente hello come Britta Simon.

    d. In hello **Password** casella di testo, digitare la password di Britta Simon hello.

    e. In hello **Conferma Password** casella di testo, hello tipo stessa password.
    
    f. Rendere la password **attiva**.   

6. Fare clic su **Salva**.
 
### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAbsorb LMS.

![Assegnazione del ruolo utente hello][200]

**tooassign Britta Simon tooAbsorb LMS, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **assorbire LMS**.

    ![Hello assorbire LMS collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Fare clic su hello assorbire LMS riquadro in hello Pannello di accesso, si otterranno applicazione assorbire LMS tooyour automaticamente firmato-on. Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

