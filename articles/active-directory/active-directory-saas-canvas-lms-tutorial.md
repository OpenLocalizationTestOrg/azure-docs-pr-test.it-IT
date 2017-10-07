---
title: 'Esercitazione: Integrazione di Azure Active Directory con Canvas LMS | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Canvas LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a>Esercitazione: Integrazione di Azure Active Directory con Canvas LMS

In questa esercitazione, è illustrato come area di disegno toointegrate con Azure Active Directory (Azure AD).

Area di disegno di integrazione con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooCanvas
- È possibile abilitare l'utenti tooautomatically get connesso tooCanvas (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Canvas tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Canvas abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta area di disegno dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-canvas-from-hello-gallery"></a>Aggiunta area di disegno dalla raccolta hello
integrazione hello tooconfigure dell'area di disegno in Azure AD, è necessario tooadd area di disegno da elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Canvas dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **area di disegno**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. Nel riquadro dei risultati hello, selezionare **area di disegno**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Canvas usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nell'area di disegno è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello nell'area di disegno deve toobe stabilita.

Nell'area di disegno, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con area di disegno, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Canvas](#creating-a-canvas-test-user)**  -toohave un equivalente di Britta Simon nell'area di disegno che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione area di disegno.

**Azure AD tooconfigure single sign-on con area di disegno, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **area di disegno** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. In hello **URL e area di disegno dominio** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.instructure.com`

    b. In hello **identificatore** casella di testo, valore di tipo hello utilizzando hello modello:`https://<tenant-name>.instructure.com/saml2`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto Client di area di disegno](https://community.canvaslms.com/community/help) tooget questi valori. 
 
4. In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. In hello **configurazione Canvas** fare clic su **configurare Canvas** tooopen **Configura sign-on** finestra. Hello copia **Modifica URL Password, Sign-Out URL, ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. In una finestra del web browser, accedere come amministratore nel sito della società Canvas di tooyour.

8. Andare troppo**corsi \> gli account gestiti \> Microsoft**.
   
    ![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")

9. Nel riquadro di spostamento hello hello sinistra, selezionare **autenticazione**, quindi fare clic su **Aggiungi nuova configurazione SAML**.
   
    ![Autenticazione](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Autenticazione")

10. Nella pagina di integrazione corrente hello, eseguire hello alla procedura seguente:
   
    ![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")

    a. In **IdP Entity ID** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.

    b. In **Log On URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.

    c. In **Log Out URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.

    d. In **Change Password Link** casella di testo, hello Incolla valore **Modifica URL Password** che è stato copiato dal portale di Azure. 

    e. In **Certificate Fingerprint** casella di testo, incollare hello **identificazione personale** valore del certificato che è stato copiato dal portale di Azure.      
        
    f. Da hello **accesso attributo** elenco, selezionare **NameID**.

    g. Da hello **identificatore di formato** elenco, selezionare **emailAddress**.

    h. Fare clic su **Save authentication settings**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-canvas-test-user"></a>Creazione di un utente di test di Canvas

toolog agli utenti di Azure AD tooenable in tooCanvas, è necessario eseguirne il provisioning in Canvas.

Nel caso di Canvas, il provisioning degli utenti è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **area di disegno** tenant.

2. Andare troppo**corsi \> gli account gestiti \> Microsoft**.
   
   ![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")

3. Fare clic su **Users**.
   
   ![Utenti](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Utenti")

4. Fare clic su **Add new user**.
   
   ![Utenti](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Utenti")

5. In hello Aggiungi una pagina della finestra di dialogo Nuovo utente, eseguire hello alla procedura seguente:
   
   ![Aggiungere un utente](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Aggiungere un utente")
   
   a. In hello **nome completo** casella di testo, immettere il nome di hello dell'utente come **BrittaSimon**.

   b. In hello **posta elettronica** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .

   c. In hello **accesso** casella di testo, immettere l'indirizzo di posta elettronica dell'utente hello Azure AD come  **brittasimon@contoso.com** .

   d. Selezionare **la creazione dell'account utente di hello posta elettronica**.

   e. Fare clic su **Aggiungi utente**.

>[!NOTE]
>È possibile utilizzare qualsiasi altro area di disegno account strumento di creazione utente o le API fornite da Canvas tooprovision account utente di AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCanvas.

![Assegna utente][200] 

**tooassign Britta Simon tooCanvas, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **area di disegno**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro area di disegno hello in hello Pannello di accesso, è necessario ottenere applicazione Canvas tooyour automaticamente firmato-on.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

