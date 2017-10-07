---
title: 'Esercitazione: Integrazione di Azure Active Directory con MOVEit Transfer - Azure AD integration | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e trasferimento MOVEit - integrazione di Azure AD.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>Esercitazione: Integrazione di Azure Active Directory con MOVEit Transfer - Azure AD integration

In questa esercitazione, è illustrato come toointegrate MOVEit trasferimento - integrazione di Azure AD con Azure Active Directory (Azure AD).

L'integrazione di trasferimento MOVEit - integrazione di Azure AD con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooMOVEit trasferimento - integrazione di Azure AD.
- È possibile abilitare l'utenti tooautomatically get connesso tooMOVEit trasferimento - integrazione di Azure AD (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con trasferimento MOVEit - integrazione di Azure AD, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di MOVEit Transfer - Azure AD integration abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di trasferimento MOVEit - integrazione di Azure AD dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>Aggiunta di trasferimento MOVEit - integrazione di Azure AD dalla raccolta hello
integrazione di hello tooconfigure di trasferimento MOVEit - integrazione di Azure AD in Azure AD, è necessario tooadd MOVEit trasferimento - integrazione di Azure AD dall'elenco di tooyour hello della raccolta di App SaaS gestite.

**tooadd MOVEit trasferimento - integrazione di Azure AD dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **MOVEit trasferimento - integrazione di Azure AD**selezionare **MOVEit trasferimento - integrazione di Azure AD** dal pannello risultati quindi fare clic su **Aggiungi** hello tooadd pulsante applicazione.

    ![Trasferimento MOVEit - integrazione di Azure AD nell'elenco risultati hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con MOVEit Transfer - Azure AD integration usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello trasferimento MOVEit - integrazione di Azure AD è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in trasferimento MOVEit - integrazione di Azure AD deve toobe stabilita.

Trasferimento MOVEit - integrazione di Azure AD, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con trasferimento MOVEit - integrazione di Azure AD, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un trasferimento MOVEit - utente test di integrazione di Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave un equivalente di Britta Simon MOVEit trasferimento - integrazione di Azure AD che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nel trasferimento di MOVEit - applicazione di integrazione di Azure AD.

**Azure AD tooconfigure single sign-on con trasferimento MOVEit - integrazione di Azure AD, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **MOVEit trasferimento - integrazione di Azure AD** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. In hello **MOVEit trasferimento - integrazione di Azure AD, dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://contoso.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://contoso.com/<tenatid>`

    c. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On. È possibile fare riferimento a questi valori in un secondo momento in **URL dei metadati del servizio Provider** sezione o un contatto [MOVEit trasferimento - team di supporto Client di integrazione di Azure AD](https://community.ipswitch.com/s/support) tooget questi valori.

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. Accesso tooyour MOVEit trasferimento tenant come amministratore.

7. Nel riquadro di spostamento a sinistra di hello, fare clic su **impostazioni**.

    ![Sezione delle impostazioni sul lato dell'app](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. Fare clic sul collegamento **Single Signon** (Single Sign-On) in **Security Policies -> User Auth** (Criteri di sicurezza -> Autenticazione utente).

    ![Criteri di sicurezza sul lato dell'app](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Fare clic su documento di metadati hello collegamento toodownload hello URL dei metadati.

    ![URL dei metadati del provider di servizi](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * Verificare **entityID** corrisponde **identificatore** in hello **MOVEit trasferimento - integrazione di Azure AD, dominio e gli URL** sezione.
    * Verificare **AssertionConsumerService** percorso URL corrisponde a **URL di risposta** in hello **MOVEit trasferimento - integrazione di Azure AD, dominio e gli URL** sezione.
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. Fare clic su **Add Identity Provider** pulsante tooadd un nuovo Provider di identità federata.

    ![Aggiungi provider di identità](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. Fare clic su **Sfoglia...**  tooselect hello file di metadati che è stato scaricato dal portale di Azure, quindi fare clic su **Add Identity Provider** hello tooupload download del file.

    ![Provider di identità SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. Selezionare "**Sì**" come **abilitato** in hello **Modifica impostazioni di Provider di identità federata...**  pagina e fare clic su **salvare**.

    ![Impostazioni provider di identità federato](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. In hello **modifica Federated Identity Provider di impostazioni utente** eseguire hello seguenti azioni:
    
    ![Modifica delle impostazioni del provider di identità federato](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. Selezionare **SAML NameID** (ID nome SAML) per **Login name** (Nome di accesso).
    
    b. Selezionare **altri** come **nome completo** e hello **nome dell'attributo** casella di testo inserire il valore di hello: `http://schemas.microsoft.com/identity/claims/displayname`.
    
    c. Selezionare **altri** come **posta elettronica** e hello **nome dell'attributo** casella di testo inserire il valore di hello: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    d. Selezionare **Yes** (Sì) per **Auto-create account on signon** (Crea automaticamente account all'accesso).
    
    e. Fare clic sul pulsante **Salva** .

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>Creare un utente di test di MOVEit Transfer - Azure AD integration

obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon MOVEit trasferimento - integrazione di Azure AD. MOVEit Transfer - Azure AD integration supporta il provisioning JIT, che è stato abilitato. Non è necessario alcun intervento dell'utente in questa sezione. Durante un tooaccess tentativo di trasferimento MOVEit - integrazione di Azure AD se non esiste ancora, viene creato un nuovo utente.

>[!NOTE]
>Se è necessario un utente toocreate manualmente, è necessario hello toocontact [MOVEit trasferimento - team di supporto Client di integrazione di Azure AD](https://community.ipswitch.com/s/support).

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMOVEit trasferimento - integrazione di Azure AD.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooMOVEit trasferimento - integrazione di Azure AD, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **MOVEit trasferimento - integrazione di Azure AD**.

    ![integrazione di Azure AD di Hello MOVEit trasferimento - collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.

Quando si fa clic su hello MOVEit trasferimento - riquadro integrazione di Azure AD in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour MOVEit trasferimento - applicazione di integrazione di Azure AD. 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

