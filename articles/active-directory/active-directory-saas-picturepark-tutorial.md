---
title: 'Esercitazione: Integrazione di Azure Active Directory con Picturepark | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Picturepark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Esercitazione: Integrazione di Azure Active Directory con Picturepark

In questa esercitazione, è illustrato come toointegrate Picturepark con Azure Active Directory (Azure AD).

Integrazione Picturepark con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooPicturepark
- È possibile abilitare l'utenti tooautomatically get connesso tooPicturepark (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Picturepark tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Picturepark abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Picturepark dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-picturepark-from-hello-gallery"></a>Aggiunta di Picturepark dalla raccolta hello
integrazione hello tooconfigure di Picturepark in Azure AD, è necessario tooadd Picturepark dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Picturepark dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Picturepark**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. Nel riquadro dei risultati hello, selezionare **Picturepark**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Picturepark in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Picturepark è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Picturepark richiede toobe stabilita.

In Picturepark, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Picturepark, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Picturepark](#creating-a-picturepark-test-user)**  -toohave un equivalente di Britta Simon in Picturepark che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Picturepark.

**Azure AD tooconfigure single sign-on con Picturepark, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Picturepark** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. In hello **Picturepark dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.picturepark.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello: 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto Picturepark Client](https://picturepark.com/about/contact/) tooget questi valori. 
 
4. In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. In hello **Picturepark configurazione** fare clic su **configurare Picturepark** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. In un'altra finestra del Web browser accedere al sito aziendale di Picturepark come amministratore.

8. Nella barra degli strumenti hello in primo piano hello, fare clic su **strumenti di amministrazione**, quindi fare clic su **Console di gestione**.
   
    ![Console di gestione](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Console di gestione")

9. Fare clic su **Autenticazione**, quindi su **Provider di identità**.
   
    ![Autenticazione](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Autenticazione")

10. In hello **configurazione del provider di identità** seguire hello alla procedura seguente:
   
    ![Configurazione del provider di identità](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configurazione del provider di identità")
   
    a. Fare clic su **Aggiungi**.
  
    b. Digitare un nome per la configurazione.
   
    c. Selezionare **Imposta come predefinito**.
   
    d. In **Issuer URI** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.
   
    e. In **Trusted Issuer Thumb Print** casella di testo, hello Incolla valore **identificazione personale** che è stato copiato da **certificato di firma SAML** sezione. 

11. Fare clic su **JoinDefaultUsersGroup**.

12. hello tooset **Emailaddress** attributo hello **attestazione** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` e fare clic su **salvare**.

      ![Configurazione](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configurazione")

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-picturepark-test-user"></a>Creazione di un utente test di Picturepark

In ordine tooenable Azure AD utenti toolog a Picturepark, è necessario eseguirne il provisioning in Picturepark. Nel caso di hello di Picturepark, il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **Picturepark** tenant.

2. Nella barra degli strumenti hello in primo piano hello, fare clic su **strumenti di amministrazione**, quindi fare clic su **utenti**.
   
    ![Utenti](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Utenti")

3. In hello **Cenni preliminari sugli utenti** scheda, fare clic su **New**.
   
    ![Gestione degli utenti](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Gestione degli utenti")

4. In hello **Create User** finestra di dialogo, hello eseguire i passaggi di un utente valido delle Directory Azure Active seguenti si desidera tooprovision:
   
    ![Crea utente](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Crea utente")
   
    a. In hello **indirizzo di posta elettronica** casella di testo, hello tipo **indirizzo di posta elettronica** dell'utente hello  **BrittaSimon@contoso.com** .  
   
    b. In hello **Password** e **Conferma Password** nelle caselle di testo, hello tipo **password** di BrittaSimon. 
   
    c. In hello **nome** casella di testo, hello tipo **nome** dell'utente hello **Laura**. 
   
    d. In hello **cognome** casella di testo, hello tipo **cognome** dell'utente hello **Simon**.
   
    e. In hello **aziendale** casella di testo, hello tipo **nome società** dell'utente hello. 
   
    f. In hello **paese** casella di testo, seleziona hello **paese** dell'utente hello.
  
    g. In hello **ZIP** casella di testo, hello tipo **CAP** di città hello.
   
    h. In hello **Città** casella di testo, hello tipo **Città** dell'utente hello.

    i. Selezionare una **Language**.
   
    j. Fare clic su **Crea**.

>[!NOTE]
>È possibile usare qualsiasi altro Picturepark utente account strumento di creazione o le API fornite da Picturepark tooprovision degli account utente di Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPicturepark.

![Assegna utente][200] 

**tooassign Britta Simon tooPicturepark, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Picturepark**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Picturepark hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Picturepark applicazione. Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

