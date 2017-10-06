---
title: 'Esercitazione: Integrazione di Azure Active Directory con Sprinklr | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Sprinklr.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a>Esercitazione: Integrazione di Azure Active Directory con Sprinklr

In questa esercitazione, è illustrato come toointegrate Sprinklr con Azure Active Directory (Azure AD).

Integrazione Sprinklr con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSprinklr
- È possibile abilitare l'utenti tooautomatically get connesso tooSprinklr (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Sprinklr tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Sprinklr abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Sprinklr dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-sprinklr-from-hello-gallery"></a>Aggiunta di Sprinklr dalla raccolta hello
integrazione hello tooconfigure di Sprinklr in Azure AD, è necessario tooadd Sprinklr dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Sprinklr dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Sprinklr**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. Nel riquadro dei risultati hello, selezionare **Sprinklr**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Sprinklr usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Sprinklr è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Sprinklr deve toobe stabilita.

In Sprinklr, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure single sign-on AD con Sprinklr, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Sprinklr](#creating-a-sprinklr-test-user)**  -toohave un equivalente di Britta Simon in Sprinklr che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Sprinklr.

**Azure AD tooconfigure single sign-on con Sprinklr, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Sprinklr** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. In hello **Sprinklr dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.sprinklr.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.sprinklr.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare il valore di hello con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto Sprinklr Client](https://www.sprinklr.com/contact-us/) tooget questi valori. 
 
4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. In hello **Sprinklr configurazione** fare clic su **configurare Sprinklr** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

7. In una finestra del web browser, accedere come amministratore nel sito della società Sprinklr di tooyour.

8. Andare troppo**amministrazione \> impostazioni**.
   
    ![Amministrazione](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Amministrazione")

9. Andare troppo**gestire Partner \> l'accesso Single Sign** su hello nel riquadro di sinistra.
   
    ![Gestione partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Gestione partner")

10. Fare clic su **+ Add Single Sign Ons**.
   
    ![Accessi Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Accessi Single Sign-On")

11. In hello **Single Sign-on** eseguire hello alla procedura seguente:
   
    ![Accessi Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Accessi Single Sign-On")

    a. In hello **nome** casella di testo, digitare un nome per la configurazione (ad esempio: *WAADSSOTest*).

    b. Selezionare **Enabled**.

    c. Selezionare **Use new SSO Certificate**.
             
    e. Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **Identity Provider Certificate** casella di testo.

    f. Hello Incolla **ID entità SAML** valore a cui è stato copiato dal portale di Azure in hello **Id entità** casella di testo.

    g. Hello Incolla **SAML Single Sign-On Service URL** valore a cui è stato copiato dal portale di Azure in hello **Identity Provider Login URL** casella di testo.

    h. Hello Incolla **Sign-Out URL** valore a cui è stato copiato dal portale di Azure in hello **Identity Provider Logout URL** casella di testo.
     
    i. In **SAML User ID Type** (Tipo ID utente SAML) selezionare **Assertion contains User”s sprinklr.com username** (L'asserzione contiene il nome utente sprinklr.com dell'utente).

    j. Come **SAML User ID Location**selezionare **è l'ID utente nell'elemento di nome identificatore hello dell'istruzione Subject hello**.

    k. Fare clic su **Salva**.
       
    ![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-sprinklr-test-user"></a>Creazione di un utente di test di Sprinklr

1. Accedi tooyour sito della società Sprinklr come amministratore.

2. Andare troppo**amministrazione \> impostazioni**.
   
    ![Amministrazione](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Amministrazione")

3. Andare troppo**gestire Client \> utenti** hello nel riquadro di sinistra.
   
    ![Impostazioni](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Impostazioni")

4. Fare clic su **Aggiungi utente**.
   
    ![Impostazioni](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Impostazioni")

5. In hello **modifica utente** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Modifica degli utenti](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Modifica degli utenti") 

    a. In hello **posta elettronica**, **nome** e **cognome** nelle caselle di testo, informazioni sul tipo di hello di un account utente di Azure AD desiderato tooprovision.

    b. Selezionare **Password disabled**.

    c. Selezionare **Language** (Lingua).

    d. Selezionare **User Type** (Tipo di utente).

    e. Fare clic su **Update**.
   
     >[!IMPORTANT]
     >**Password Disabled** deve essere selezionato tooenable toolog un utente in tramite un provider di identità. 
     
6. Andare troppo**ruolo**e quindi eseguire hello alla procedura seguente:
   
    ![Ruoli partner](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Ruoli partner")

    a. Da hello **globale** elenco, selezionare **tutti\_autorizzazioni**.  

    b. Fare clic su **Update**.

>[!NOTE]
>È possibile usare qualsiasi altro Sprinklr utente account strumento di creazione o le API fornite da Sprinklr tooprovision degli account utente di Azure AD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSprinklr.

![Assegna utente][200] 

**tooassign Britta Simon tooSprinklr, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Sprinklr**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Sprinklr hello in hello Pannello di accesso, deve ottenere tooyour automaticamente firmato in Sprinklr applicazione per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

