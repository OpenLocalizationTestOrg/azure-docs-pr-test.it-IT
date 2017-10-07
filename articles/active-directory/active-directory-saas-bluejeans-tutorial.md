---
title: 'Esercitazione: Integrazione di Azure Active Directory con BlueJeans | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e BlueJeans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a>Esercitazione: Integrazione di Azure Active Directory con BlueJeans

In questa esercitazione, è illustrato come toointegrate BlueJeans con Azure Active Directory (Azure AD).

Integrazione di BlueJeans con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooBlueJeans
- È possibile abilitare l'utenti tooautomatically get connesso tooBlueJeans (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con BlueJeans tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di BlueJeans abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di BlueJeans dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-bluejeans-from-hello-gallery"></a>Aggiunta di BlueJeans dalla raccolta hello
integrazione hello tooconfigure di BlueJeans in Azure AD, è necessario tooadd BlueJeans dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd BlueJeans dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **BlueJeans**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. Nel riquadro dei risultati hello, selezionare **BlueJeans**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BlueJeans usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in BlueJeans è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in BlueJeans deve toobe stabilita.

In BlueJeans, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure single sign-on AD con BlueJeans, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test BlueJeans](#creating-a-bluejeans-test-user)**  -toohave un equivalente di Britta Simon in BlueJeans che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione BlueJeans.

**Azure AD tooconfigure single sign-on con BlueJeans, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **BlueJeans** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. In hello **BlueJeans dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.BlueJeans.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.BlueJeans.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto Client di BlueJeans](https://support.bluejeans.com/contact) tooget questi valori. 
 
4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. In hello **BlueJeans configurazione** fare clic su **configurare BlueJeans** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, Modifica URL Password e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. In una finestra del web browser, accedere tooyour **BlueJeans** sito aziendale come amministratore.

8. Andare troppo**ADMIN \> impostazioni gruppo \> sicurezza**.
   
   ![Amministratore](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Amministratore")

9. In hello **sicurezza** seguire hello alla procedura seguente:
   
   ![Single Sign-On SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Single Sign-On SAML")   
   
   a. Selezionare **SAML Single Sign On**.
  
   b. Selezionare **Enable automatic provisioning**.

10. Passare con hello alla procedura seguente:

    ![Percorso certificato](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Percorso certificato")
    
    a. Fare clic su **Scegli File**e quindi caricare il certificato scaricato hello.
   
    b. Incolla **SAML Single Sign-On Service URL** in hello **URL di accesso** casella di testo.
   
    c. Incolla **Modifica URL Password** in hello **Change Password URL** casella di testo.
   
    d. Incolla **Sign-Out URL** in hello **Logout URL** casella di testo.

11. Passare con hello alla procedura seguente:
    
    ![Salvare le modifiche](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Salvare le modifiche")
    
    a. In hello **id utente** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    b. In hello **posta elettronica** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    c. Fare clic su **Salva modifiche**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-bluejeans-test-user"></a>Creazione di un utente di test di BlueJeans

toolog agli utenti di Azure AD tooenable in tooBlueJeans, è necessario eseguirne il provisioning in BlueJeans.  

Nel caso di BlueJeans, il provisioning è un'attività manuale.

**eseguire un account utente, tooprovision hello i passaggi seguenti:**

1. Accedi tooyour **BlueJeans** sito aziendale come amministratore.

2. Andare troppo**ADMIN \> Gestisci utenti \> Aggiungi utente**.
   
   ![Amministratore](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Amministratore")
   
   >[!IMPORTANT]
   >Hello **Aggiungi utente** scheda è disponibile solo se nell'hello **scheda sicurezza**, **abilitare il provisioning automatico** è deselezionata. 
   
3. In hello **Aggiungi utente** seguire hello alla procedura seguente:

    ![Aggiungere un utente](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Aggiungere un utente")
    
    a. Digitare un **nome utente BlueJeans**, un **indirizzo di posta elettronica**, **ID riunione BlueJeans**, **Passcode di moderatore**, un **nome completo** , hello **aziendale** di un account aAd di cui si desidera tooprovision in hello relative caselle di testo.
    
    b. Fare clic su **Aggiungi utente**.

>[!NOTE]
>È possibile usare qualsiasi altro BlueJeans utente account strumento di creazione o le API fornite da BlueJeans tooprovision account utente di AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBlueJeans.

![Assegna utente][200] 

**tooassign Britta Simon tooBlueJeans, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **BlueJeans**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello BlueJeans riquadro in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione BlueJeans.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

