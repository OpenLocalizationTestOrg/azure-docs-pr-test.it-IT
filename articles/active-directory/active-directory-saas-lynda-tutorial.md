---
title: 'Esercitazione: integrazione di Azure Active Directory con Lynda.com | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Lynda.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: fb8d7824e5121da79e9248393b0cbcb0efaffec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a>Esercitazione: Integrazione di Azure Active Directory con Lynda.com

In questa esercitazione, è illustrato come toointegrate Lynda.com con Azure Active Directory (Azure AD).

Integrazione di Lynda.com con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooLynda.com
- È possibile abilitare l'utenti tooautomatically get connesso tooLynda.com (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Lynda.com tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Lynda.com abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Lynda.com dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-lyndacom-from-hello-gallery"></a>Aggiunta di Lynda.com dalla raccolta hello
integrazione hello tooconfigure di Lynda.com in Azure AD, è necessario tooadd Lynda.com dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Lynda.com dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Lynda.com**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. Nel riquadro dei risultati hello, selezionare **Lynda.com**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Lynda.com usando un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Lynda.com è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Lynda.com deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Lynda.com.

tooconfigure e test Azure single sign-on AD con Lynda.com, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Lynda.com](#creating-a-lyndacom-test-user)**  -toohave un equivalente di Britta Simon in Lynda.com che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Lynda.com.

**Azure AD tooconfigure single sign-on con Lynda.com, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Lynda.com** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. In hello **Lynda.com dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `

    > [!NOTE] 
    > Poiché non è reale, Aggiorna il valore con hello URL effettivo Sign-On. Contatto [team di supporto di Lynda.com Client](https://www.linkedin.com/help/lynda/ask) tooget questi valori. 
 
4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. tooconfigure single sign-on sul **Lynda.com** lato, è necessario hello toosend scaricato **Metadata XML** [il supporto di Lynda.com](https://www.linkedin.com/help/lynda/ask).

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-lyndacom-test-user"></a>Creazione di un utente test di Lynda.com

Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooLynda.com.  
Quando un utente assegnato tenta toolog in tooLynda.com mediante il pannello di accesso di hello, Lynda.com verifica se hello utente esiste.  

Se l’account utente non è ancora disponibile, viene creato automaticamente da Lynda.com.

>[!NOTE]
>È possibile usare qualsiasi altro Lynda.com utente account strumento di creazione o le API fornite da Lynda.com tooprovision account utente di AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLynda.com.

![Assegna utente][200] 

**tooassign Britta Simon tooLynda.com, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Lynda.com**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso. Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

