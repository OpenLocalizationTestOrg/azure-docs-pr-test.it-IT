---
title: 'Esercitazione: Integrazione di Azure Active Directory con etouches | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed etouches.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a>Esercitazione: Integrazione di Azure Active Directory con eTouches

In questa esercitazione, è illustrato come etouches toointegrate con Azure Active Directory (Azure AD).

Integrazione etouches con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooetouches
- È possibile abilitare l'utenti tooautomatically get connesso tooetouches (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con etouches tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di etouches abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di etouches dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-etouches-from-hello-gallery"></a>Aggiunta di etouches dalla raccolta hello
integrazione hello tooconfigure di etouches in Azure AD, è necessario etouches tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.

**etouches tooadd dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **etouches**selezionare **etouches** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Nell'elenco risultati hello etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con etouches usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in etouches è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in etouches deve toobe stabilita.

In etouches, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con etouches, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test etouches](#create-an-etouches-test-user)**  -toohave un equivalente di Britta Simon in etouches che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione etouches.

**Azure AD tooconfigure single sign-on con etouches, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **etouches** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. In hello **etouches dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.eiseverywhere.com/<instance name>`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Si aggiorna il valore di hello con hello effettivo accesso URL e l'identificatore, illustrato più avanti nell'esercitazione di hello.
    > 

4. applicazione di etouches prevede asserzioni SAML hello in un formato specifico. Configurare hello seguendo le attestazioni per questa applicazione. È possibile gestire i valori hello di questi attributi da hello **attributo utente** di un'applicazione hello. Hello seguente schermata mostra un esempio per questo oggetto. 

    ![Attributo utente](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nella figura hello ed eseguire hello alla procedura seguente:
    
    | Nome attributo | Valore attributo |
    | ------------------- | -------------------- |
    | Email | user.mail |    
    
    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.

    ![Aggiungi attributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Finestra di dialogo Aggiungi attributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.

    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.
    
    d. Fare clic su **OK**. 

6. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. tooget SSO configurato per l'applicazione, attenersi alla procedura seguente in un'applicazione hello etouches hello: 

    ![Configurazione di etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    a. Account di accesso troppo**etouches** applicazione utilizzando i diritti di amministratore hello.
   
    b. Passare toohello **SAML** configurazione.

    c. In hello **impostazioni generali** sezione, aprire il certificato scaricato dal portale di Azure nel blocco note, hello copia il contenuto e quindi incollarlo nella casella di testo hello IDP metadati. 

    d. Fare clic su hello **Salva e rimanere** pulsante.
  
    e. Fare clic su hello **i metadati degli aggiornamenti** pulsante nella sezione dei metadati SAML hello. 

    f. Verrà visualizzata hello pagina ed esegue SSO. Una volta hello SSO sta quindi è possibile impostare il nome utente hello.

    g. Nel campo nome utente hello selezionare hello **emailaddress** come illustrato nell'immagine di hello riportata di seguito. 

    h. Hello copia **ID entità SP** valore e incollarlo in hello **identificatore** casella di testo, ovvero in **etouches dominio e gli URL** sezione nel portale di Azure.

    i. Hello copia **URL SSO / ACS** valore e incollarlo in hello **URL di accesso** casella di testo, ovvero in **etouches dominio e gli URL** sezione nel portale di Azure.
   
> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-an-etouches-test-user"></a>Creare un utente di test di etouches

In questa sezione viene creato un utente di nome Britta Simon in etouches. Lavorare con [team di supporto Client etouches](https://www.etouches.com/event-software/support/customer-support/) utenti hello tooadd nella piattaforma etouches hello.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooetouches.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooetouches, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **etouches**.

    ![Hello etouches collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On


obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.

Quando si fa clic hello etouches riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour etouches applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

