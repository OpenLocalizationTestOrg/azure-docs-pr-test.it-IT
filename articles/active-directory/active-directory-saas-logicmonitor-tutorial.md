---
title: 'Esercitazione: Integrazione di Azure Active Directory con LogicMonitor | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e LogicMonitor.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: ea5cb8b574d763cb114286e3b2a5c94ab5546756
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a>Esercitazione: Integrazione di Azure Active Directory con LogicMonitor

In questa esercitazione, è illustrato come toointegrate LogicMonitor con Azure Active Directory (Azure AD).

Integrazione LogicMonitor con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooLogicMonitor
- È possibile abilitare l'utenti tooautomatically get connesso tooLogicMonitor (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con LogicMonitor tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di LogicMonitor abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di LogicMonitor dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-logicmonitor-from-hello-gallery"></a>Aggiunta di LogicMonitor dalla raccolta hello
integrazione hello tooconfigure di LogicMonitor in Azure AD, è necessario tooadd LogicMonitor dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd LogicMonitor dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **LogicMonitor**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. Nel riquadro dei risultati hello, selezionare **LogicMonitor**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LogicMonitor usando un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in LogicMonitor è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in LogicMonitor deve toobe stabilita.

In LogicMonitor, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con LogicMonitor, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test LogicMonitor](#creating-a-logicmonitor-test-user)**  -toohave un equivalente di Britta Simon in LogicMonitor che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione LogicMonitor.

**Azure AD tooconfigure single sign-on con LogicMonitor, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **LogicMonitor** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. In hello **LogicMonitor dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.logicmonitor.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.logicmonitor.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto LogicMonitor Client](https://www.logicmonitor.com/contact/) tooget questi valori. 
 


4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. Accedi tooyour **LogicMonitor** sito aziendale come amministratore.

7. Scegliere dal menu hello in primo piano hello **impostazioni**.
   
   ![Impostazioni](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Impostazioni")

8. Nella barra di spostamento hello sul lato sinistro di hello, fare clic su **Single Sign-On**
   
   ![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")

9. In hello **le impostazioni di Single Sign-on (SSO)** seguire hello alla procedura seguente:
   
   ![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")
   
   a. Selezionare **Attiva Single Sign-On**.

   b. In **Default Role Assignment** (Assegnazione ruolo predefinito) selezionare **readonly**.
   
   c. Aprire il file di metadati di hello scaricato nel blocco note e incollare il contenuto del file hello hello **i metadati del Provider di identità** casella di testo.
   
   d. Fare clic su **Salva modifiche**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-logicmonitor-test-user"></a>Creazione di un utente test di LogicMonitor

Per AAD utenti toobe in grado di toosign in devono essere sottoposte a provisioning toohello applicazione LogicMonitor usando i rispettivi nomi utente di Azure Active Directory.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Accedi tooyour sito della società LogicMonitor come amministratore.

2. Scegliere dal menu hello in primo piano hello **impostazioni**, quindi fare clic su **ruoli e utenti**.
   
   ![Ruoli e utenti](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Ruoli e utenti")

3. Fare clic su **Aggiungi**.

4. In hello **aggiungere un account** seguire hello alla procedura seguente:
   
   ![Aggiungere un account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Aggiungere un account")
   
   a. Hello tipo **Username**, **posta elettronica**, **Password**, e **password digitare di nuovo** i valori dell'utente di Azure Active Directory hello desiderato tooprovision in hello relative caselle di testo.
   
   b. Selezionare **ruoli**, **le autorizzazioni di visualizzazione**, hello e **stato**.
   
   c. Fare clic su **Submit**.

>[!NOTE]
>È possibile usare qualsiasi altro LogicMonitor utente account strumento di creazione o le API fornite da LogicMonitor tooprovision Azure Active Directory gli account utente. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLogicMonitor.

![Assegna utente][200] 

**tooassign Britta Simon tooLogicMonitor, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **LogicMonitor**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.
 
Quando si fa clic su riquadro LogicMonitor hello in hello Pannello di accesso, è necessario ottenere applicazione LogicMonitor tooyour automaticamente firmato-on.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

