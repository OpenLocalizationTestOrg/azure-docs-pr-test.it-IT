---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zendesk | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Zendesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>Esercitazione: Integrazione di Azure Active Directory con Zendesk

In questa esercitazione, è illustrato come toointegrate Zendesk con Azure Active Directory (Azure AD).

Integrazione di Zendesk con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooZendesk
- È possibile abilitare l'utenti tooautomatically get connesso tooZendesk (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Zendesk tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Zendesk abilitata per l'accesso Single Sign-On


> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.


passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Zendesk dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD


## <a name="adding-zendesk-from-hello-gallery"></a>Aggiunta di Zendesk dalla raccolta hello
integrazione hello tooconfigure di Zendesk in Azure AD, è necessario tooadd Zendesk dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Zendesk dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Zendesk**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. Nel riquadro dei risultati hello, selezionare **Zendesk**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zendesk in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Zendesk è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Zendesk richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Zendesk.

tooconfigure e test Azure single sign-on AD con Zendesk, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Zendesk](#creating-a-zendesk-test-user)**  -toohave un equivalente di Britta Simon in Zendesk che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Zendesk.

**Azure AD tooconfigure single sign-on con Zendesk, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Zendesk** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. In hello **Zendesk dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    a. In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:`https://<subdomain>.zendesk.com`

    b. In hello **identificatore** casella di testo, valore di tipo hello utilizzando hello modello:`https://<subdomain>.zendesk.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con URL hello effettivo Sign-on e URL dell'identificatore. Contatto [team di supporto di Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget questi valori. 

4. Zendesk prevede asserzioni SAML hello in un formato specifico. Non sono presenti attributi SAML obbligatori ma facoltativamente è possibile aggiungere un attributo da **gli attributi utente** sezione hello seguente passaggi seguenti: 

     ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    a. Fare clic su hello **visualizzare e modificare tutti gli altri attributi di hello** casella di controllo.
     
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    b. Fare clic su hello **Aggiungi attributo** tooopen **Aggiungi attributo** finestra di dialogo.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    c. In hello **nome** casella di testo, nome dell'attributo di tipo hello (ad esempio **emailaddress**).
    
    d. Da hello **valore** elenco, il valore di attributo selezionare hello (come **user.mail**).
    
    e. Fare clic su **Ok**
 
    > [!NOTE] 
    > Utilizzare gli attributi tooadd gli attributi dell'estensione che non sono in Azure AD per impostazione predefinita. Fare clic su [gli attributi utente che possono essere impostati in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget elenco completo di hello di SAML attributi che **Zendesk** accetta. 

5. In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. In hello **Zendesk configurazione** fare clic su **configurare Zendesk** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. In un'altra finestra del Web browser accedere al sito aziendale di Zendesk come amministratore.

8. Fare clic su **Admin**.

9. Nel riquadro di spostamento a sinistra di hello, fare clic su **impostazioni**, quindi fare clic su **sicurezza**.

10. In hello **sicurezza** eseguire hello alla procedura seguente: 
   
     ![Sicurezza](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Sicurezza")

    ![Single Sign-On](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single Sign-On")

     a. Fare clic su hello **Admin & agenti** scheda.

     b. Selezionare **Single sign-on (SSO) e SAML** e quindi **SAML**.

     c. In **URL SSO SAML** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure. 

     d. In **URL disconnessione remota** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.
        
     e. In **Certificate Fingerprint** casella di testo, incollare hello **identificazione personale** valore del certificato che è stato copiato dal portale di Azure.
     
     f. Fare clic su **Save**.

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay utenti andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**. 

### <a name="creating-a-zendesk-test-user"></a>Creazione di un utente test Zendesk

Azure AD tooenable utenti toolog in **Zendesk**, è necessario eseguirne il provisioning in **Zendesk**.  
A seconda del ruolo di hello nelle App hello, hello è previsto il comportamento:

 1. All'accesso viene eseguito automaticamente il provisioning degli account dell'**utente finale**.
 2. **Agente** e **Admin** account necessitano toobe manualmente il provisioning **Zendesk** prima dell'accesso.
 
**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **Zendesk** tenant.

2. Seleziona hello **un elenco di clienti** scheda.

3. Seleziona hello **utente** scheda e fare clic su **Aggiungi**.
   
    ![Aggiungere un utente](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Aggiungere un utente")
4. Digitare l'indirizzo di posta elettronica hello di un account di Azure AD esistente si desidera tooprovision e quindi fare clic su **salvare**.
   
    ![Nuovo utente](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Nuovo utente")

> [!NOTE]
> È possibile usare qualsiasi altro Zendesk utente account strumento di creazione o qualsiasi API fornita da Zendesk tooprovision account utente di AAD.


### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooZendesk.

![Assegna utente][200] 

**tooassign Britta Simon tooZendesk, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Zendesk**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Zendesk hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Zendesk applicazione.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
