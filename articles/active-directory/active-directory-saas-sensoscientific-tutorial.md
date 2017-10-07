---
title: 'Esercitazione: Integrazione di Azure Active Directory con SensoScientific Wireless Temperature Monitoring System | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e di sistema di monitoraggio della temperatura SensoScientific Wireless.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>Esercitazione: Integrazione di Azure Active Directory con SensoScientific Wireless Temperature Monitoring System

In questa esercitazione, è illustrato come toointegrate SensoScientific sistema di monitoraggio Wireless temperatura con Azure Active Directory (Azure AD).

Integrazione di sistema di monitoraggio della temperatura SensoScientific Wireless con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSensoScientific sistema di monitoraggio della temperatura Wireless
- È possibile abilitare l'utenti tooautomatically get connesso tooSensoScientific Wireless temperatura monitoraggio del sistema (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con sistema di monitoraggio della temperatura SensoScientific Wireless tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Una sottoscrizione abilitata per l'accesso Single Sign-On per SensoScientific Wireless Temperature Monitoring System

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di sistema di monitoraggio della temperatura Wireless SensoScientific dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a>Aggiunta di sistema di monitoraggio della temperatura Wireless SensoScientific dalla raccolta hello
integrazione hello tooconfigure di sistema di monitoraggio della temperatura SensoScientific Wireless in Azure AD, è necessario tooadd SensoScientific Wireless temperatura Monitoraggio sistema dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd SensoScientific Wireless temperatura Monitoraggio sistema dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **SensoScientific Wireless sistema di monitoraggio della temperatura**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. Nel riquadro dei risultati hello, selezionare **SensoScientific Wireless sistema di monitoraggio della temperatura**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SensoScientific Wireless Temperature Monitoring System con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nel sistema di monitoraggio della temperatura SensoScientific Wireless è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nel sistema di monitoraggio della temperatura SensoScientific Wireless deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nel sistema di monitoraggio della temperatura SensoScientific Wireless.

tooconfigure e prova AD Azure single sign-on con sistema di monitoraggio della temperatura SensoScientific Wireless, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente di test di sistema di monitoraggio della temperatura Wireless SensoScientific](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave un equivalente di Britta Simon SensoScientific Wireless temperatura Monitoraggio sistema che è collegato rappresentazione toohello Azure AD utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nell'applicazione di sistema di monitoraggio della temperatura SensoScientific Wireless.

**tooconfigure Azure single sign-on AD SensoScientific Wireless temperatura monitoraggio di sistema, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **SensoScientific Wireless sistema di monitoraggio della temperatura** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. In hello **SensoScientific Wireless temperatura Monitoraggio sistema dominio e gli URL** non sezione tooperform è necessario alcun passaggio come applicazione hello è già pre-integrata con Azure:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. In hello **SensoScientific configurazione sistema di monitoraggio della temperatura di Wireless** fare clic su **configurazione sistema di monitoraggio SensoScientific Wireless temperatura** tooopen  **Configurare l'accesso** finestra. Hello copia **Sign-Out URL, ID entità SAML** e **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. Accesso tooyour applicazione di sistema di monitoraggio della temperatura Wireless SensoScientific come amministratore.

8. Nel menu di navigazione hello in primo piano hello, fare clic su **configurazione** e goto **configura** in **Single Sign-On** tooopen hello Single Sign On Settings.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. In **Single Sign On Settings** form eseguire hello alla procedura seguente:
 
    a. Selezionare il **Nome autorità emittente** come Azure AD.
    
    b. Hello Incolla **ID entità SAML** che è stato copiato dal portale di Azure nella casella di testo URL autorità di certificazione.
    
    c. Hello Incolla **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure nella casella di testo URL servizio Single Sign-On.

    d. Hello Incolla **Sign-Out URL** che è stato copiato dal portale di Azure nella casella di testo URL del servizio Single Sign-Out.

    e. Sfoglia hello certificato è stato scaricato dal portale di Azure e caricare qui.
    
    f. Fare clic su **Salva**.
  
> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>Creazione di un utente test di SensoScientific Wireless Temperature Monitoring System

toolog agli utenti di Azure AD tooenable in tooSensoScientific sistema di monitoraggio della temperatura Wireless, è necessario eseguirne il provisioning nel sistema di monitoraggio della temperatura SensoScientific Wireless. Lavorare con [team di supporto di sistema di monitoraggio della temperatura Wireless SensoScientific](https://www.sensoscientific.com/contact-us/) per aggiungere gli utenti di hello nella piattaforma di sistema di monitoraggio della temperatura SensoScientific Wireless hello. Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSensoScientific sistema di monitoraggio della temperatura Wireless.

![Assegna utente][200] 

**tooassign Britta Simon tooSensoScientific sistema di monitoraggio della temperatura Wireless, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **SensoScientific Wireless sistema di monitoraggio della temperatura**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso. Fare clic sul riquadro di sistema di monitoraggio della temperatura SensoScientific Wireless hello in hello Pannello di accesso, sarà l'applicazione di sistema di monitoraggio SensoScientific Wireless temperatura tooyour automaticamente firmato-on. Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

