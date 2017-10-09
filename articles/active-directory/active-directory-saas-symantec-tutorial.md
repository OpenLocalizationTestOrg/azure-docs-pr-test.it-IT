---
title: 'Esercitazione: Integrazione di Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e servizio di sicurezza Web Symantec (WSS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>Esercitazione: Integrazione di Azure Active Directory con Symantec Web Security Service (WSS)

In questa esercitazione si apprenderà come toointegrate il servizio di sicurezza Web Symantec (WSS) account con il proprio account Azure Active Directory (Azure AD) in modo da WSS può autenticare un utente finale il provisioning in hello Azure AD utilizzando l'autenticazione SAML e applicare l'utente o regole di livello dei criteri di gruppo.

Integrazione del servizio di sicurezza Web Symantec (WSS) con Azure AD fornisce hello seguenti vantaggi:

- Gestire tutti gli utenti finali di hello e i gruppi utilizzati per l'account WSS dal portale di Azure AD. 

- Consentire tooauthenticate gli utenti finali di hello WSS utilizzando le proprie credenziali di Azure AD.

- Abilitare l'applicazione hello di utente e gruppo di regole di livello dei criteri definite nell'account di WSS.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con Symantec Web Security Service (WSS), è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Account Symantec Web Security Service (WSS)

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un account WSS utilizzato a scopo di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare per i test un account WSS attualmente in uso nell'ambiente di produzione, a meno che ciò non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione, configurare il AD Azure tooenable single sign-on tooWSS utilizzando le credenziali utente finale di hello definite nell'account di Azure AD.
scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di applicazione di servizio di sicurezza Web Symantec (WSS) hello dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>Aggiunta del servizio di sicurezza Web Symantec (WSS) dalla raccolta hello
integrazione di hello di tooconfigure Symantec Web Security Service (WSS) in Azure AD, è necessario tooadd Symantec Web Security Service (WSS) dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Symantec Web Security Service (WSS) dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Symantec Web Security Service (WSS)**selezionare **Symantec Web Security Service (WSS)** dal pannello risultati quindi fare clic su **Aggiungi** hello tooadd pulsante applicazione.

    ![Symantec Web Security Service (WSS) nell'elenco risultati hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Symantec Web Security Service (WSS) usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Symantec Web Security Service (WSS) è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello Symantec Web Security Service (WSS) richiede toobe stabilita.

In Symantec Web Security Service (WSS), assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test di Azure AD single sign-on con Symantec Web Security Service (WSS), è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente di test del servizio di sicurezza Web Symantec (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave un equivalente di Britta Simon in Symantec Web Security Service (WSS) che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione del servizio di sicurezza Web Symantec (WSS).

**tooconfigure AD Azure single sign-on con Symantec Web Security Service (WSS), eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Symantec Web Security Service (WSS)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. In hello **URL e dominio del servizio (WSS) sicurezza Web Symantec** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    a. In hello **identificatore** casella di testo, digitare l'URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`

    b. In hello **URL di risposta** casella di testo, digitare l'URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`

    > [!NOTE]
    > Contattare hello [team di supporto Client di servizio di sicurezza Web Symantec (WSS)](https://www.symantec.com/contact-us) se i valori hello per hello **identificatore** e **URL di risposta** non funzionano per qualche motivo.

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. tooconfigure single sign-on sul hello lato servizio di sicurezza Web Symantec (WSS), consultare la documentazione online di toohello WSS. Hello scaricato **Metadata XML** file sarà necessario toobe importati nel portale WSS hello. Contatto hello [team di supporto del servizio di sicurezza Web Symantec (WSS)](https://www.symantec.com/contact-us) assistenza con la configurazione nel portale WSS hello hello.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a>Creare un utente di test di Symantec Web Security Service (WSS)

In questa sezione viene creato un utente di nome Britta Simon in Symantec Web Security Service (WSS). nome utente di fine corrispondente Hello può essere creato manualmente nel portale WSS hello o è possibile attendere hello utenti o gruppi è stato eseguito il provisioning nel portale di hello Azure AD sincronizzati toobe toohello WSS dopo pochi minuti (~ 15 minuti). Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On. indirizzo IP pubblico di Hello del computer di utenti hello, che sarà siti Web toobrowse usato è inoltre necessario toobe il provisioning nel portale di hello Symantec Web Security Service (WSS).

> [!NOTE]
> . [Fare clic qui](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget del computer pubblico IPaddress.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSymantec Web Security Service (WSS).

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooSymantec Web Security Service (WSS), eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Symantec Web Security Service (WSS)**.

    ![collegamento di Hello Symantec Web Security Service (WSS) nell'elenco delle applicazioni hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione verrà testato funzionalità hello single sign-on dopo aver configurato il toouse account WSS Azure AD per l'autenticazione SAML.

Dopo aver configurato il traffico tooproxy del browser web tooWSS, quando si apre il browser e prova toobrowse tooa sito, quindi si verrà reindirizzati pagina toohello Azure sign-on. Immettere le credenziali di hello dell'utente finale di prova hello che è stato eseguito il provisioning in hello Azure AD (vale a dire BrittaSimon) e la password associata. Una volta autenticato, sarà in grado di toobrowse sito Web di toohello scelto. È necessario creare una regola dei criteri in hello WSS lato tooblock BrittaSimon dal sito tooa particolare è possibile vedere hello WSS blocco pagina quando si tenta di toobrowse toothat sito come utente BrittaSimon.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

