---
title: 'Esercitazione: Integrazione di Azure Active Directory con IQNavigator VMS | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e IQNavigator VMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a>Esercitazione: Integrazione di Azure Active Directory con IQNavigator VMS

In questa esercitazione, è illustrato come toointegrate IQNavigator VMS con Azure Active Directory (Azure AD).

Integrazione IQNavigator VMS con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooIQNavigator macchine Virtuali
- È possibile abilitare l'utenti tooautomatically get connesso tooIQNavigator macchine Virtuali (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con VMS IQNavigator tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di IQNavigator VMS abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di IQNavigator VMS dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a>Aggiunta di IQNavigator VMS dalla raccolta hello
integrazione hello tooconfigure di IQNavigator VMS in Azure AD, è necessario tooadd IQNavigator VMS dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd IQNavigator VMS dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **IQNavigator VMS**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. Nel riquadro dei risultati hello, selezionare **IQNavigator VMS**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con IQNavigator VMS con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello VMS IQNavigator è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello IQNavigator VMS deve toobe stabilita.

VMS IQNavigator, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con IQNavigator VMS, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test VMS IQNavigator](#creating-a-iqnavigator-vms-test-user)**  -toohave un equivalente di Britta Simon VMS IQNavigator che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione IQNavigator VMS.

**Azure AD tooconfigure single sign-on con IQNavigator VMS, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **IQNavigator VMS** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. In hello **IQNavigator macchine Virtuali di dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    a. In hello **identificatore** casella di testo, digitare l'URL hello:`iqn.com`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`

4. Controllare **Mostra URL impostazioni avanzate**, eseguire hello seguente passaggio:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    In hello **inoltro stato** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.iqnavigator.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con stato di URL di risposta e inoltro effettivo hello. Contatto [team di supporto Client di macchine Virtuali IQNavigator](https://www.beeline.com/iqn-product-support/) tooget questi valori. 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. hello toogenerate **metadati** url, eseguire hello alla procedura seguente:

    a. Fare clic su **Registrazioni per l'app**.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    b. Fare clic su **endpoint** tooopen **endpoint** la finestra di dialogo.  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    c. Fare clic su hello copia pulsante toocopy **documento metadati federazione** url e incollarlo nel blocco note.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    d. Ora passare toohello pagina delle proprietà di **IQNavigator VMS** e hello copia **Id applicazione** utilizzando **copia** pulsante e incollarlo nel blocco note.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    e. Generare hello **URL dei metadati** utilizzando hello seguente motivo:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`

7. Applicazione IQNavigator previsto valore dell'identificatore utente univoco hello in attestazioni nome identificatore hello. Cliente può eseguire il mapping hello di valore corretto per l'attestazione dell'identificatore di nome hello. In questo caso è stato eseguito il mapping utente hello. UserPrincipalName a scopo dimostrativo hello. Ma in base a tooyour impostazioni dell'organizzazione è necessario mappare valore corretto hello relativo.   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. In hello **configurazione di macchine Virtuali IQNavigator** fare clic su **configurare macchine Virtuali IQNavigator** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. tooconfigure single sign-on sul **IQNavigator VMS** lato, è necessario hello toosend **URL dei metadati**, **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo [Team di supporto IQNavigator VMS](https://www.beeline.com/iqn-product-support/). Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-iqnavigator-vms-test-user"></a>Creazione di un utente test di IQNavigator VMS

obiettivo di Hello di questa sezione è un utente denominato Britta Simon IQNavigator VMS toocreate. Lavorare con [team di supporto IQNavigator VMS](https://www.beeline.com/iqn-product-support/) utenti hello tooadd hello account IQNavigator VMS.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooIQNavigator macchine Virtuali.

![Assegna utente][200] 

**tooassign Britta Simon tooIQNavigator le macchine Virtuali, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **IQNavigator VMS**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello riquadro IQNavigator VMS in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione IQNavigator VMS.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

