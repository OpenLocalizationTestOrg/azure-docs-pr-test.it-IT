---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zoho | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Zoho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a>Esercitazione: Integrazione di Azure Active Directory con Zoho

In questa esercitazione, è illustrato come toointegrate Zoho con Azure Active Directory (Azure AD).

Integrazione di Zoho con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooZoho.
- È possibile abilitare l'utenti tooautomatically get connesso tooZoho (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Zoho tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Zoho abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Zoho dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-zoho-from-hello-gallery"></a>Aggiunta di Zoho dalla raccolta hello
integrazione hello tooconfigure di Zoho in Azure AD, è necessario tooadd Zoho dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Zoho dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Zoho**selezionare **Zoho** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Nell'elenco risultati hello Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zoho usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Zoho è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Zoho deve toobe stabilita.

In Zoho, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Zoho, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Zoho](#create-a-zoho-test-user)**  -toohave un equivalente di Britta Simon in Zoho che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Zoho.

**Azure AD tooconfigure single sign-on con Zoho, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Zoho** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. In hello **Zoho dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.zohomail.com`

    > [!NOTE] 
    > Poiché non è reale, Aggiorna il valore con hello URL effettivo Sign-On. Contatto [team di supporto Client di Zoho](https://www.zoho.com/mail/contact.html) tooget questo valore. 
 
4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. In hello **Zoho configurazione** fare clic su **configurare Zoho** tooopen **Configura sign-on** finestra. Hello copia **URL Sign-Out e Modifica URL Password SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configurazione di Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. In un'altra finestra del Web browser accedere al sito aziendale di Zoho Mail come amministratore.

8. Passare toohello **Pannello di controllo**.
   
    ![Pannello di controllo](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Pannello di controllo")

9. Fare clic su hello **SAML Authentication** scheda.
   
    ![Autenticazione SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Autenticazione SAML")

10. In hello **SAML Authentication Details** seguire hello alla procedura seguente:
   
    ![Dettagli dell'autenticazione SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Dettagli dell'autenticazione SAML")
   
    a. In hello **URL di accesso** casella di testo, incollare **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.
   
    b. In hello **Logout URL** casella di testo, incollare **Sign-Out URL** che è stato copiato dal portale di Azure.
   
    c. In hello **Modifica URL Password** casella di testo, incollare **Modifica URL Password** che è stato copiato dal portale di Azure.
       
    d. Aprire il certificato con codifica base 64 scaricato dal portale di Azure nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **PublicKey** casella di testo.
   
    e. In **Algorithm** (Algoritmo) selezionare **RSA**.
   
    f. Fare clic su **OK**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-a-zoho-test-user"></a>Creare un utente di test di Zoho

In ordine tooenable Azure AD utenti toolog a Zoho Mail, è necessario eseguirne il provisioning in Zoho Mail. Nel caso di hello di Zoho Mail, il provisioning è un'attività manuale.

> [!NOTE]
> È possibile usare qualsiasi altro Zoho Mail utente account strumento di creazione o qualsiasi API fornita da Zoho Mail tooprovision account utente di AAD.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision un account utente, eseguire hello alla procedura seguente:

1. Accedi tooyour **Zoho Mail** sito aziendale come amministratore.

2. Andare troppo**Pannello di controllo \> posta elettronica e documenti**.

3. Andare troppo**dettagli utente \> Aggiungi utente**.
   
    ![Aggiungere un utente](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Aggiungere un utente")

4. In hello **aggiungere utenti** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Aggiungere un utente](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Aggiungere un utente")
   
    a. In hello **nome** casella Tipo hello nome dell'utente come **Laura**.

    b. In hello **cognome** casella di testo, digitare hello cognome dell'utente come **Simon**.

    c. In hello **ID di posta elettronica** casella di testo, id di tipo hello posta elettronica dell'utente come  **brittasimon@contoso.com** .

    d. In hello **Password** casella di testo, immettere la password dell'utente.
   
    e. Fare clic su **OK**.  
      
    > [!NOTE]
    > titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica con un account di hello tooconfirm collegamento prima che diventi attivo.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooZoho.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooZoho, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Zoho**.

    ![collegamento di Zoho Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Zoho hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Zoho applicazione.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

