---
title: 'Esercitazione: Integrazione di Azure Active Directory con IBM Kenexa Survey Enterprise | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e IBM Kenexa sondaggio Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Esercitazione: Integrazione di Azure Active Directory con IBM Kenexa Survey Enterprise

In questa esercitazione, è illustrato come toointegrate IBM Kenexa sondaggio Enterprise con Azure Active Directory (Azure AD).

Integrazione di IBM Kenexa sondaggio Enterprise con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooIBM Kenexa sondaggio Enterprise.
- È possibile abilitare l'accesso agli utenti tooautomatically tooIBM Kenexa sondaggio Enterprise single sign-on (SSO) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: hello portale di Azure.

Se si desidera tooknow informazioni sul software come una servizio (SaaS) integrazione dell'applicazione con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con IBM Kenexa sondaggio Enterprise tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione IBM Kenexa Survey Enterprise abilitata per l'accesso SSO

> [!NOTE]
> Quando si testano passaggi hello in questa esercitazione, è consigliabile non utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test. scenario di Hello descritto nell'esercitazione hello è composto da due componenti principali:

* Aggiunta di IBM Kenexa sondaggio Enterprise dalla raccolta hello
* Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>Aggiungere IBM Kenexa sondaggio Enterprise dalla raccolta di hello
integrazione di hello tooconfigure di IBM Kenexa sondaggio Enterprise in Azure AD, aggiungere IBM Kenexa sondaggio Enterprise hello raccolta tooyour elenco di App SaaS gestite.

tooadd IBM Kenexa sondaggio Enterprise dalla raccolta di hello, hello seguenti:

1. In hello [portale di Azure](https://portal.azure.com)in hello riquadro sinistro, fare clic su hello **Azure Active Directory** pulsante. 

    ![pulsante di Hello Azure Active Directory][1]

2. Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd un'applicazione, fare clic su hello **nuova applicazione** pulsante.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **IBM Kenexa sondaggio Enterprise**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. Selezionare dall'elenco risultati hello **IBM Kenexa sondaggio Enterprise**, quindi fare clic su hello **Aggiungi** pulsante applicazione hello tooadd.

    ![IBM Kenexa sondaggio aziendale nell'elenco risultati hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso SSO di Azure AD con IBM Kenexa Survey Enterprise con un utente test di nome "Britta Simon".

Per toowork SSO, Azure AD deve controparte di tooidentify hello IBM Kenexa sondaggio Enterprise utente in Azure AD. In altre parole, Azure AD deve stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in IBM Kenexa Survey Enterprise.

relazione di collegamento hello tooestablish, assegnare un valore di hello hello **nome utente** in IBM Kenexa sondaggio Enterprise come valore di hello di hello **Username** in Azure AD.

tooconfigure e SSO AD Azure con IBM Kenexa sondaggio Enterprise, completo di test hello blocchi predefiniti di hello nelle due sezioni successive.

### <a name="configure-azure-ad-sso"></a>Configurare l'accesso SSO di Azure AD

In questa sezione abilitare SSO AD Azure nel portale di Azure hello e configurare SSO nell'applicazione IBM Kenexa sondaggio Enterprise eseguendo hello seguenti:

1. Nel portale di Azure su hello hello **IBM Kenexa sondaggio Enterprise** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![IBM Kenexa Survey Enterprise Configurazione collegamento Single Sign-On][4]

2. In hello **Single sign-on** della finestra di dialogo hello **modalità** , quindi selezionare **basato su SAML Sign-on** tooenable SSO.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. In hello **IBM Kenexa sondaggio Enterprise dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL con hello seguente motivo:`https://surveys.kenexa.com/<companycode>`

    b. In hello **URL di risposta** casella di testo, digitare un URL con hello seguente motivo:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > Hello valori precedenti non sono reali. Aggiornarli con identificatore effettivo hello e URL di risposta. i valori effettivi, hello contatto di hello tooobtain [team di supporto IBM Kenexa sondaggio Enterprise](https://www.ibm.com/support/home/?lnk=fcw).

4. In **certificato di firma SAML**, fare clic su **certificato (Base64)**e quindi salvare computer tooyour file certificato di hello.

    ![collegamento al download del certificato (Base64) Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    applicazione aziendale di sondaggio Kenexa IBM Hello prevede le asserzioni di sicurezza asserzioni Markup Language (SAML) hello tooreceive in un formato specifico, che richiede di tooadd attributo personalizzato configurazione dei mapping toohello degli attributi token SAML. Hello valore dell'attestazione utente identificatore hello in risposta hello deve corrispondere hello ID SSO configurato nel sistema Kenexa hello. toomap hello identificatore utente appropriato all'interno dell'organizzazione come SSO Internet Datagram Protocol (IDP), il lavoro con hello [team di supporto IBM Kenexa sondaggio Enterprise](https://www.ibm.com/support/home/?lnk=fcw). 

    Per impostazione predefinita, Azure AD imposta l'identificatore utente hello come valore del nome principale (UPN) utente hello. È possibile modificare questo valore su hello **attributo** scheda, come illustrato nella seguente schermata hello. integrazione di Hello funziona solo dopo aver completato correttamente il mapping di hello.
    
    ![finestra di dialogo attributi di utente Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. Fare clic su **Salva**.

    ![Hello configurare single sign-on pulsante Salva](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. hello tooopen **Configura sign-on** finestra, in **IBM Kenexa sondaggio Enterprise configurazione**, fare clic su **configurare IBM Kenexa sondaggio Enterprise**. 
 
    ![collegamento di Hello configurare IBM Kenexa sondaggio Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. Hello copia **Sign-Out URL**, **ID entità SAML**, e **SAML single sign-on Service URL** valori hello **riferimento rapido** sezione.

8. In hello **Configura sign-on** finestra, in **riferimento rapido**, hello copia **Sign-Out URL**, **ID entità SAML**, e  **SAML single sign-on Service URL** valori.

9. tooconfigure SSO su hello **IBM Kenexa sondaggio Enterprise** sul lato, inviare hello scaricato **certificato (Base64)**, **Sign-Out URL**, **ID entità SAML**, e **SAML single sign-on Service URL** valori toohello [team di supporto IBM Kenexa sondaggio Enterprise](https://www.ibm.com/support/home/?lnk=fcw).

> [!TIP]
> È possibile fare riferimento tooa versione concisa di queste istruzioni in hello [portale di Azure](https://portal.azure.com) mentre si stanno impostando app hello. Dopo aver aggiunto l'applicazione hello da hello **Active Directory** > **applicazioni aziendali** fare semplicemente clic su hello **accesso single sign-on** scheda e quindi accedere Hello incorporato documentazione tramite hello **configurazione** sezione alla fine di hello. toolearn più feature hello documentazione incorporati, vedere [AD Azure incorporato documentazione](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
In questa sezione è creare utente test Britta Simon nel portale di Azure hello eseguendo hello seguenti:

![Creare un utente test di Azure AD][100]

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>Creare un utente test di IBM Kenexa Survey Enterprise

In questa sezione viene creato un utente chiamato Britta Simon in IBM Kenexa Survey Enterprise. 

utenti toocreate hello sistema IBM Kenexa sondaggio Enterprise e hello mappa ID SSO per essi, è possibile utilizzare hello [team di supporto IBM Kenexa sondaggio Enterprise](https://www.ibm.com/support/home/?lnk=fcw). Il valore dell'ID di SSO deve inoltre essere eseguito il mapping di valore dell'identificatore utente toohello da Azure AD. È possibile modificare questa impostazione predefinita su hello **attributo** scheda.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare utente Britta Simon toouse SSO Azure concessione dell'accesso tooIBM Kenexa sondaggio Enterprise.

![Assegnazione del ruolo utente hello][200] 

utente tooassign tooIBM Britta Simon Kenexa sondaggio Enterprise, hello seguenti:

1. Nel portale di Azure hello, aprire hello **applicazioni** visualizzare, andare toohello **Directory** visualizzazione, selezionare **applicazioni aziendali**, quindi fare clic su **tutti applicazioni**.

    ![Hello "applicazioni aziendali" e i collegamenti di "Tutte le applicazioni"][201] 

2. In hello **applicazioni** elenco, selezionare **IBM Kenexa sondaggio Enterprise**.

    ![collegamento a IBM Kenexa sondaggio Enterprise Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. Nel riquadro di sinistra hello, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. Fare clic su hello **Aggiungi** pulsante e quindi nel hello **Aggiungi** riquadro, selezionare **utenti e gruppi**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In hello **utenti e gruppi** della finestra di dialogo hello **utenti** elenco, selezionare **Britta Simon**.

6. In hello **utenti e gruppi** finestra di dialogo fare clic su hello **selezionare** pulsante.

7. In hello **Aggiungi** finestra di dialogo fare clic su hello **assegnare** pulsante.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione verificare la configurazione di SSO AD Azure tramite hello Pannello di accesso.

Quando si fa clic su hello **IBM Kenexa sondaggio Enterprise** hello di riquadro nel Pannello di accesso, è necessario essere connessi automaticamente tooyour applicazione aziendale di sondaggio Kenexa IBM.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
