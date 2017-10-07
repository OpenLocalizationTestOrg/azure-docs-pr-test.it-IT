---
title: 'Esercitazione: Integrazione di Azure Active Directory con TeamSeer | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TeamSeer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a>Esercitazione: Integrazione di Azure Active Directory con TeamSeer

In questa esercitazione, è illustrato come toointegrate TeamSeer con Azure Active Directory (Azure AD).

Integrazione TeamSeer con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooTeamSeer
- È possibile abilitare l'utenti tooautomatically get connesso tooTeamSeer (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con TeamSeer tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di TeamSeer abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di TeamSeer dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-teamseer-from-hello-gallery"></a>Aggiunta di TeamSeer dalla raccolta hello
integrazione hello tooconfigure di TeamSeer in tooAzure Active Directory, è necessario tooadd TeamSeer dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd TeamSeer dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **TeamSeer**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. Nel riquadro dei risultati hello, selezionare **TeamSeer**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TeamSeer usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in TeamSeer è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in TeamSeer deve toobe stabilita.

In TeamSeer, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con TeamSeer, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test TeamSeer](#creating-a-teamseer-test-user)**  -toohave un equivalente di Britta Simon in TeamSeer che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione TeamSeer.

**Azure AD tooconfigure single sign-on con TeamSeer, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **TeamSeer** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. In hello **TeamSeer dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.teamseer.com/<companyid>`

    > [!NOTE] 
    > il valore di Hello non è di tipo real. Il valore di hello aggiornamento con hello URL effettivo Sign-On. Contatto [team di supporto TeamSeer Client](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) valore hello tooget. 
 
4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. In hello **TeamSeer configurazione** fare clic su **configurare TeamSeer** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. In una finestra del web browser, accedere come amministratore nel sito della società TeamSeer di tooyour.

8. Andare troppo**HR Admin**.
   
    ![Amministratore risorse umane](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Amministratore risorse umane")

9. Fare clic su **Configura**.
   
    ![Installazione](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Installazione")

10. Fare clic su **Configura dettagli del provider SAML**.
   
    ![Impostazioni SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Impostazioni SAML")

11. Nella sezione dettagli di provider SAML hello, eseguire hello alla procedura seguente:
   
    ![Impostazioni SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Impostazioni SAML")   

    a. Hello Incolla **URL servizio Single Sign-On** valore toohello **URL** casella di testo.
          
    b. Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto negli Appunti tooyour e quindi incollarlo toohello **IdP Public Certificate** casella di testo.

12. hello toocomplete configurazione del provider SAML, eseguire hello alla procedura seguente:
    
    ![Impostazioni SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Impostazioni SAML") 

    a. In hello **indirizzi di posta elettronica di Test**, digitare l'indirizzo di posta elettronica dell'utente test hello. 
  
    b. In hello **dell'autorità di certificazione** casella di testo, hello tipo URL autorità di certificazione hello provider di servizi. 
  
    c. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-teamseer-test-user"></a>Creazione di un utente di test di TeamSeer

toolog agli utenti di Azure AD tooenable in tooTeamSeer, è necessario eseguirne il provisioning in tooShiftPlanning. Nel caso di hello di TeamSeer, il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **TeamSeer** sito aziendale come amministratore.

2. Eseguire hello alla procedura seguente:
   
    ![Amministratore risorse umane](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Amministratore risorse umane")  
 
    a. Andare troppo**HR Admin \> utenti**.
  
    b. Fare clic su **eseguire Creazione guidata nuovo utente hello**.

3. In hello **dettagli utente** seguire hello alla procedura seguente:
   
    ![Dettagli utente](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Dettagli utente")

    a. Hello tipo **nome**, **Surname**, **nome utente (indirizzo di posta elettronica)** di un account aAd di cui si desidera tooprovision in toohello relative caselle di testo.
  
    b. Fare clic su **Avanti**.

4. Seguire hello istruzioni per l'aggiunta di un nuovo utente e fare clic su **fine**.

>[!NOTE]
>È possibile usare qualsiasi altro TeamSeer utente account strumento di creazione o le API fornite da TeamSeer tooprovision degli account utente di Azure AD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTeamSeer.

![Assegna utente][200] 

**tooassign Britta Simon tooTeamSeer, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **TeamSeer**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello. Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

