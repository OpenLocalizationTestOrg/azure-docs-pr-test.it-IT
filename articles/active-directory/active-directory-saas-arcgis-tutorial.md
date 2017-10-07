---
title: 'Esercitazione: Integrazione di Azure Active Directory con ArcGIS Online | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ArcGIS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a>Esercitazione: Integrazione di Azure Active Directory con ArcGIS Online

In questa esercitazione, è illustrato come toointegrate ArcGIS Online con Azure Active Directory (Azure AD).

Integrazione ArcGIS Online con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooArcGIS Online
- È possibile abilitare l'utenti tooautomatically get connesso tooArcGIS Online (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con ArcGIS Online, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di ArcGIS Online abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di ArcGIS Online dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-arcgis-online-from-hello-gallery"></a>Aggiunta di ArcGIS Online dalla raccolta hello
integrazione hello tooconfigure di ArcGIS Online in Azure AD, è necessario tooadd ArcGIS Online dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd ArcGIS Online dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **nuova applicazione** pulsante nella parte superiore di hello di hello finestra di dialogo tooadd nuova applicazione.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **ArcGIS Online**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. Nel riquadro dei risultati hello, selezionare **ArcGIS Online**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ArcGIS Online usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ArcGIS Online è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ArcGIS Online richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in ArcGIS Online.

tooconfigure e prova AD Azure single sign-on con ArcGIS Online, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Online ArcGIS](#creating-an-arcgis-online-test-user)**  -toohave un equivalente di Britta Simon in ArcGIS Online è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione ArcGIS Online.

**Azure AD tooconfigure single sign-on con ArcGIS Online, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **ArcGIS Online** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. In hello **ArcGIS Online dominio e gli URL** seguire hello seguente passaggio:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://<company>.maps.arcgis.com`

    > [!NOTE] 
    > Questo valore non è hello reale. Aggiorna il valore con hello URL effettivo Sign-On. Contatto [team di supporto di Client Online ArcGIS](http://support.esri.com/) tooget questo valore. 

4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. In un'altra finestra del Web browser accedere al sito aziendale di ArcGIS come amministratore.

7. Fare clic su **EDIT SETTINGS** (Modifica impostazioni).

    ![Modificare le impostazioni](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Modificare le impostazioni")

8. Fare clic su **Security**.

    ![Sicurezza](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Sicurezza")

9. In **Enterprise Logins** (Accessi aziendali) fare clic su **SET IDENTITY PROVIDER** (Imposta provider di identità).

    ![Accessi aziendali](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Accessi aziendali")

10. In hello **Set Identity Provider** configurazione eseguire hello alla procedura seguente:
   
    ![Impostare il provider di identità](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Impostare il provider di identità")
   
    a. In hello **nome** casella di testo, digitare il nome dell'organizzazione.

    b. Per **verranno specificati i metadati per il Provider di identità Enterprise hello utilizzando**selezionare **A File**.

    c. tooupload file di metadati scaricato, fare clic su **Choose file**.

    d. Fare clic su **SET IDENTITY PROVIDER** (Imposta provider di identità).

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di Britta Simon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-an-arcgis-online-test-user"></a>Creazione di un utente di test di ArcGIS Online

In ordine tooenable Azure AD utenti toolog in ArcGIS Online, è necessario eseguirne il provisioning in ArcGIS Online.  
Nel caso di hello di ArcGIS Online, il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **ArcGIS** tenant.

2. Fare clic su **INVITE MEMBERS** (Invita membri).
   
    ![Invitare i membri](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invitare i membri")

3. Selezionare **Add members automatically without sending an email** (Aggiungi membri automaticamente senza inviare un'e-mail) e quindi fare clic su **NEXT** (Avanti).
   
    ![Aggiungere i membri automaticamente](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Aggiungere i membri automaticamente")

4. In hello **membri** finestra di dialogo eseguire hello alla procedura seguente:
   
     ![Aggiungere ed esaminare](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Aggiungere ed esaminare")
    
     a. Immettere hello **posta elettronica**, **nome**, e **cognome** di un account aAd di cui si desidera tooprovision.
  
     b. Fare clic su **ADD AND REVIEW** (Aggiungi e verifica).
5. Esaminare i dati di hello immesse e quindi fare clic su **Aggiungi membri**.
   
    ![Aggiungere un membro](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Aggiungere un membro")
        
    > [!NOTE]
    > titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooArcGIS Online.

![Assegna utente][200] 

**tooassign Britta Simon tooArcGIS Online, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **ArcGIS Online**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro di ArcGIS Online hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in ArcGIS Online delle applicazioni.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

