---
title: 'Esercitazione: Integrazione di Azure Active Directory con Druva| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Druva.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a>Esercitazione: Integrazione di Azure Active Directory con Druva

In questa esercitazione, è illustrato come toointegrate Druva con Azure Active Directory (Azure AD).

Integrazione di Druva con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooDruva.
- È possibile abilitare l'utenti tooautomatically get connesso tooDruva (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Druva tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Druva abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Druva dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-druva-from-hello-gallery"></a>Aggiunta di Druva dalla raccolta hello
integrazione hello tooconfigure di Druva in Azure AD, è necessario tooadd Druva dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Druva dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Druva**selezionare **Druva** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Nell'elenco risultati hello Druva](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Druva in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Druva è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Druva deve toobe stabilita.

In Druva, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Druva, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Druva](#create-a-druva-test-user)**  -toohave un equivalente di Britta Simon in Druva che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Druva.

**Azure AD tooconfigure single sign-on con Druva, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Druva** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. In hello **Druva dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://cloud.druva.com/home`

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. L'applicazione Druva prevede asserzioni SAML hello in un formato specifico, che richiede il tooyour mapping di attributi personalizzati tooadd **attributi Token SAML** configurazione. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine precedente hello ed eseguire hello alla procedura seguente:

    | Nome attributo      | Valore attributo      |
    | ------------------- | -------------------- |
    | insync\_auth\_token |Immettere valore generato token hello |
    
    a. Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    b. In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.

    c. Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga. valore del token generato Hello è illustrato più avanti nell'esercitazione.
    
    d. Fare clic su **OK**.    

7. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. In hello **Druva configurazione** fare clic su **configurare Druva** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. In una finestra del web browser, accedere come amministratore nel sito della società Druva di tooyour.

10. Andare troppo**Gestisci \> impostazioni**.

    ![Impostazioni](./media/active-directory-saas-druva-tutorial/ic795091.png "Impostazioni")

11. Nella finestra di dialogo Impostazioni di Single Sign-On hello eseguire hello alla procedura seguente:

    ![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")
    
    a. Incolla **SAML Single Sign-On Service URL** valore, che è stato copiato dal portale di Azure hello in hello **ID Provider Login URL** casella di testo.
    
    b. Incolla **Sign-Out URL** valore, che è stato copiato dal portale di Azure hello in hello **ID Provider Logout URL** casella di testo.
    
     c. Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **ID Provider Certificate** casella di testo
     
     d. hello tooopen **impostazioni** pagina, fare clic su **salvare**.

12. In hello **impostazioni** pagina, fare clic su **Generate SSO Token**.

    ![Impostazioni](./media/active-directory-saas-druva-tutorial/ic795093.png "Impostazioni")

13. In hello **Single Sign-on Authentication Token** finestra di dialogo, eseguire hello alla procedura seguente:

    ![Token SSO](./media/active-directory-saas-druva-tutorial/ic795094.png "Token SSO")
    
    a. Fare clic su **copia**, Incolla copiato valore hello **valore** casella di testo in hello **Aggiungi attributo** sezione.
    
    b. Fare clic su **Close**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

   ![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.

    ![pulsante Aggiungi Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:

    ![finestra di dialogo utente Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.

    c. Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.

    d. Fare clic su **Crea**.
 
### <a name="create-a-druva-test-user"></a>Creare un utente test Druva

In ordine tooenable Azure AD utenti toolog in tooDruva, è necessario eseguirne il provisioning in Druva. Nel caso di hello di Druva, il provisioning è un'attività manuale.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Accedi tooyour **Druva** sito aziendale come amministratore.

2. Andare troppo**Gestisci \> utenti**.
   
   ![Gestione utenti](./media/active-directory-saas-druva-tutorial/ic795097.png "Gestione utenti")

3. Fare clic su **Create New**.
   
   ![Gestione utenti](./media/active-directory-saas-druva-tutorial/ic795098.png "Gestione utenti")

4. Nella finestra di dialogo Create New User hello eseguire hello alla procedura seguente:
   
   ![Crea nuovo utente](./media/active-directory-saas-druva-tutorial/ic795099.png "Crea nuovo utente")
   
   a. In hello **indirizzo di posta elettronica** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .
   
   b. In hello **nome** casella di testo, immettere il nome di hello dell'utente come **BrittaSimon**.
   
   c. Fare clic su **Create User**.

>[!NOTE]
>È possibile usare qualsiasi altro Druva utente account strumento di creazione o le API fornite da Druva tooprovision degli account utente di Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooDruva.

![Assegnazione del ruolo utente hello][200] 

**tooassign Britta Simon tooDruva, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Druva**.

    ![collegamento di Druva Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Druva hello in hello Pannello di accesso, è necessario ottenere l'applicazione Druva tooyour automaticamente firmato-on.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

