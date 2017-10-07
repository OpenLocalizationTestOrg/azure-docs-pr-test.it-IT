---
title: 'Esercitazione: integrazione di Azure Active Directory con Five9 Plus Adapter (CTI, Contact Center Agents) | Microsoft Docs'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Five9 più Adapter (CTI, agenti di contatto Center)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a>Esercitazione: integrazione di Azure Active Directory con Five9 Plus Adapter (CTI, Contact Center Agents)

In questa esercitazione, è illustrato come toointegrate Five9 più Adapter (CTI, agenti Center contatti) con Azure Active Directory (Azure AD).

Integrazione Five9 più Adapter (CTI, agenti Center contatti) con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooFive9 più Adapter (CTI, agenti di contatto Center)
- È possibile abilitare le utenti tooautomatically get connesso tooFive9 Plus Adapter (CTI, contattare Center agenti) (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di tooconfigure Azure AD con Five9 più Adapter (CTI, agenti Center contatto), è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione abilitata all'accesso Single Sign-On per Five9 Plus Adapter (CTI, Contact Center Agents)

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Five9 più Adapter (CTI, gli agenti di centro di contatto) dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a>Aggiunta di Five9 più Adapter (CTI, gli agenti di centro di contatto) dalla raccolta hello
integrazione hello tooconfigure di Five9 più Adapter (CTI, gli agenti di centro di contatto) in Azure AD, è necessario tooadd Five9 più Adapter (CTI, gli agenti di centro di contatto) dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Five9 più Adapter (CTI, gli agenti di centro di contatto) dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Five9 più Adapter (CTI, gli agenti di centro di contatto)**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. Nel riquadro dei risultati hello, selezionare **Five9 più Adapter (CTI, gli agenti di centro di contatto)**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents) in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Five9 più Adapter (CTI, gli agenti di centro di contatto) è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlati hello Five9 più Adapter (CTI, contattare Center agenti) deve toobe stabilita.

In Five9 più Adapter (CTI, agenti Center Contact), assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure single sign-on AD Five9 più adapter (CTI, contattare Center agenti), è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Five9 più Adapter (CTI, gli agenti di centro di contatto)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave un equivalente di Britta Simon Five9 più adapter (CTI, gli agenti di centro di contatto) che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Five9 più Adapter (CTI, agenti di contatto Center).

**tooconfigure Azure single sign-on AD Five9 più adapter (CTI, agenti Center Contact), eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Five9 più Adapter (CTI, gli agenti di centro di contatto)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. In hello **dominio Five9 più Adapter (CTI, contattare Center agenti) e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    a. In hello **identificatore** , digitare un URL utilizzando hello seguenti modelli:

    |    Environment      |       URL      |
    | :-- | :-- |
    | Per "Five9 Plus Adapter for Microsoft Dynamics CRM" | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | Per "Five9 Plus Adapter for Zendesk" | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | Per "Five9 Plus Adapter for Agent Desktop Toolkit" | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:

    |      Environment     |      URL      |
    | :--                  | :--           |
    | Per "Five9 Plus Adapter for Microsoft Dynamics CRM" | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | Per "Five9 Plus Adapter for Zendesk" | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | Per "Five9 Plus Adapter for Agent Desktop Toolkit" | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. In hello **Five9 più Adapter (CTI, gli agenti di centro di contatto) configurazione** fare clic su **configurare Five9 più Adapter (CTI, gli agenti di centro di contatto)** tooopen **configurasign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. tooconfigure single sign-on sul **Five9 più Adapter (CTI, gli agenti di centro di contatto)** lato, è necessario hello toosend scaricato **Certificate(Base64), Sign-Out URL, ID entità SAML e SAML Single Sign-On Service URL** troppo[team di supporto Five9 più Adapter (CTI, gli agenti di centro di contatto)](https://www.five9.com/about/contact). Inoltre, inoltre, per la configurazione di SSO ulteriormente seguire hello in base adapter toohello passaggi seguenti:

    a. Guida dell'amministratore per "Five9 Plus Adapter per Agent Desktop Toolkit": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)
    
    b. Guida dell'amministratore per "Five9 Plus Adapter per Microsoft Dynamics CRM": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)
    
    c. Guida dell'amministratore per "Five9 Plus Adapter per Zendesk": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)


> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a>Creazione dell'utente test di Five9 Plus Adapter (CTI, Contact Center Agents)

In questa sezione si crea un utente chiamato Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents). Lavorare con [team di supporto Five9 più Adapter (CTI, gli agenti di centro di contatto)](https://www.five9.com/about/contact) per aggiungere gli utenti di hello nella piattaforma di hello Five9 più Adapter (CTI, agenti di contatto Center). Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooFive9 più Adapter (CTI, agenti di contatto Center).

![Assegna utente][200] 

**tooassign Britta Simon tooFive9 più Adapter (CTI, agenti Center Contact), eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Five9 più Adapter (CTI, gli agenti di centro di contatto)**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Five9 più Adapter (CTI, gli agenti di centro di contatto) hello in hello Pannello di accesso, è necessario ottenere applicazione Five9 più Adapter (CTI, agenti Center contattare) automaticamente firmato in tooyour.
Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

