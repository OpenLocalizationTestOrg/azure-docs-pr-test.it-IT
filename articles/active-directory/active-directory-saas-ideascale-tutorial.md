---
title: 'Esercitazione: Integrazione di Azure Active Directory con IdeaScale | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e IdeaScale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a>Esercitazione: Integrazione di Azure Active Directory con IdeaScale

In questa esercitazione, è illustrato come toointegrate IdeaScale con Azure Active Directory (Azure AD).

Integrazione di IdeaScale con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooIdeaScale
- È possibile abilitare l'utenti tooautomatically get connesso tooIdeaScale (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con IdeaScale tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di IdeaScale abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di IdeaScale dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-ideascale-from-hello-gallery"></a>Aggiunta di IdeaScale dalla raccolta hello
integrazione hello tooconfigure di IdeaScale in Azure AD, è necessario tooadd IdeaScale dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd IdeaScale dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **IdeaScale**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. Nel riquadro dei risultati hello, selezionare **IdeaScale**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con IdeaScale mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in IdeaScale è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in IdeaScale richiede toobe stabilita.

In IdeaScale, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con IdeaScale, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test IdeaScale](#creating-an-ideascale-test-user)**  -toohave un equivalente di Britta Simon in IdeaScale che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione IdeaScale.

**Azure AD tooconfigure single sign-on con IdeaScale, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **IdeaScale** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. In hello **IdeaScale dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.ideascale.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto Client di IdeaScale](http://support.ideascale.com/) tooget questi valori. 
 
4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. In hello **IdeaScale configurazione** fare clic su **configurare IdeaScale** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e l'ID entità SAML** da hello **sezione di riferimento rapido**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. In una finestra del web browser, accedere come amministratore nel sito della società IdeaScale di tooyour.

8. Andare troppo**Community Settings**.
   
    ![Impostazioni Community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Impostazioni Community")

9. Andare troppo**sicurezza \> Single Sign-on Settings**.
   
    ![Impostazioni di Single Sign-On](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Impostazioni di Single Sign-On")

10. In **Single-Signon Type** (Tipo di accesso Single Sign-On) selezionare **SAML 2.0**.
   
    ![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")

11. In hello **Single Sign-on Settings** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Impostazioni di Single Sign-On](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Impostazioni di Single Sign-On")
   
    a. In **SAML IdP Entity ID** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.

    b. Copiare il contenuto di hello del file di metadati scaricato dal portale di Azure e incollarlo in hello **SAML IdP Metadata** casella di testo.

    c. In **Logout Success URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.

    d. Fare clic su **Salva modifiche**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-an-ideascale-test-user"></a>Creazione di un utente test di IdeaScale

toolog agli utenti di Azure AD tooenable a IdeaScale, è necessario eseguirne il provisioning in tooIdeaScale. Nel caso di hello di IdeaScale, il provisioning è un'attività manuale.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Accedi tooyour **IdeaScale** sito aziendale come amministratore.

2. Andare troppo**Community Settings**.
   
    ![Impostazioni Community](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Impostazioni Community")

3. Andare troppo**le impostazioni di base \> Gestione membri**.

4. Fare clic su **Aggiungi membro**.
   
    ![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")

5. Nella sezione Add New Member hello, eseguire hello alla procedura seguente:
   
    ![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")
   
    a. In hello **indirizzi di posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica di un account aAd di cui si desidera tooprovision.
   
    b. Fare clic su **Salva modifiche**. 
   
    >[!NOTE]
    >titolare dell'account di Azure Active Directory Hello Ottiene un messaggio di posta elettronica con un account di hello tooconfirm collegamento prima che diventi attivo.
      
>[!NOTE]
>È possibile usare qualsiasi altro IdeaScale utente account strumento di creazione o le API fornite da IdeaScale tooprovision account utente di AAD.
 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooIdeaScale.

![Assegna utente][200] 

**tooassign Britta Simon tooIdeaScale, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **IdeaScale**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On


obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.

Quando si fa clic su riquadro IdeaScale hello in hello Pannello di accesso, è necessario ottenere applicazione IdeaScale tooyour automaticamente firmato-on.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

