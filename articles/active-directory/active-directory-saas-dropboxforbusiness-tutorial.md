---
title: 'Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Dropbox for Business.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a>Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business

In questa esercitazione, è illustrato come toointegrate Dropbox for Business con Azure Active Directory (Azure AD).

Integrazione di Dropbox for Business con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooDropbox for Business
- È possibile abilitare il get tooautomatically utenti connesso tooDropbox for Business (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con Dropbox for Business, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Dropbox for Business abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Dropbox for Business dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-dropbox-for-business-from-hello-gallery"></a>Aggiunta di Dropbox for Business dalla raccolta hello
integrazione di hello tooconfigure di Dropbox for Business in Azure AD, è necessario tooadd Dropbox for Business dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Dropbox for Business dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Dropbox for Business**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. Nel riquadro dei risultati hello, selezionare **Dropbox for Business**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Dropbox for Business con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Dropbox for Business è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Dropbox for Business deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Dropbox for Business.

tooconfigure e test Azure single sign-on AD con Dropbox for Business, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di una raccolta per l'utente test Business](#creating-a-dropbox-for-business-test-user)**  -toohave un equivalente di Britta Simon in Dropbox for Business che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in Dropbox per applicazioni aziendali.

**Azure AD tooconfigure single sign-on con Dropbox for Business, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Dropbox for Business** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. In hello **Dropbox per il dominio di Business e gli URL** seguire hello alla procedura seguente:

    a. Accesso tooyour Dropbox per il tenant di business. 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurare l'accesso Single Sign-On")
   
    b. Nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **Console di amministrazione**. 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurare l'accesso Single Sign-On")
   
    c. In hello **Console di amministrazione**, fare clic su **autenticazione** nel riquadro di spostamento sinistro hello. 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurare l'accesso Single Sign-On")
   
    d. In hello **Single sign-on** selezionare **abilitare single sign-on**, quindi fare clic su **più** tooexpand in questa sezione.  
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurare l'accesso Single Sign-On")
   
    e. Copia URL hello accanto troppo**gli utenti possono accedere immettendo l'indirizzo di posta elettronica oppure possono passare direttamente a**. 
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    f. Nel portale di Azure in hello hello **Sign-on URL** casella di testo, incollare hello URL.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.dropbox.com/sso/<id>`

    > [!NOTE] 
    > Poiché il valore non è reale, Aggiornare il valore di hello con hello Sign-on URL effettivo è ottenere dalla sezione Single sign-on. Contatto [Dropbox per il team di supporto Client di Business](https://www.dropbox.com/business/contact) tooget questo valore. 
 
4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. In hello **Dropbox for Business configurazione** fare clic su **configurare Dropbox for Business** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. tooconfigure single sign-on sul **Dropbox for Business** sul lato, andare il tenant Dropbox for Business, in hello **Single sign-on** sezione di hello **autenticazione** pagina eseguire hello alla procedura seguente: 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurare l'accesso Single Sign-On")
   
    a. Fare clic su **Required**.
   
    b. Nel portale di Azure su hello hello **Configura sign-on** finestra, hello copia **SAML Single Sign-On Service URL** valore e quindi incollarlo hello **URL di accesso** casella di testo.

    c. Fare clic su **Seleziona certificato**, quindi selezionare tooyour **file di certificato con codifica Base64**.

    d. Fare clic su **salvare modifiche** toocomplete configurazione hello del tenant DropBox for Business.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-dropbox-for-business-test-user"></a>Creazione di un utente test di Dropbox for Business

In questa sezione viene creato un utente di nome Britta Simon in Dropbox for Business. Dropbox for Business supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Se un utente non esiste già in Dropbox for Business, viene creato uno nuovo quando si tenta di tooaccess Dropbox for Business.

>[!Note]
>Se è necessario toocreate manualmente, contattare l'utente [Dropbox per il team di supporto Client di Business](https://www.dropbox.com/business/contact) 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooDropbox for Business.

![Assegna utente][200] 

**tooassign tooDropbox Britta Simon for Business, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Dropbox for Business**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello Dropbox per il riquadro di Business nel Pannello di accesso hello, è necessario ottenere la pagina di accesso di Dropbox per applicazioni aziendali.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configura provisioning utenti](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

