---
title: 'Esercitazione: Integrazione di Azure Active Directory con HR2day by Merces | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e HR2day da Merces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Esercitazione: Integrazione di Azure Active Directory con HR2day by Merces

In questa esercitazione, è illustrato come toointegrate HR2day da Merces con Azure Active Directory (Azure AD).

Integrazione HR2day da Merces con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooHR2day da Merces.
- È possibile abilitare gli utenti tooautomatically ottenere l'accesso tooHR2day Merces con gli account di Azure AD.
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con HR2day da Merces tooconfigure, è necessario hello seguenti elementi:

- Una sottoscrizione di Azure AD.
- Sottoscrizione di HR2day by Merces abilitata per l'accesso Single Sign-On.

> [!NOTE]
> Non è consigliabile utilizzare un hello tootest ambiente di produzione i passaggi in questa esercitazione.

passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Ottenere una [versione di valutazione gratuita di un mese di Azure AD](https://azure.microsoft.com/pricing/free-trial/), se non la si ha già.  

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritta di seguito è composto da due componenti principali:

1. Aggiunta di HR2day da Merces dalla raccolta hello.
2. Configurazione e test dell'accesso Single Sign-On di Azure AD.

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>Aggiungere HR2day da Merces dalla raccolta di hello
integrazione di hello tooconfigure di HR2day da Merces in Azure AD, aggiungere HR2day da Merces hello raccolta tooyour elenco di App SaaS gestite.

**tooadd HR2day da Merces dalla raccolta di hello, richiedere hello alla procedura seguente:**

1. In hello [portale di Azure](https://portal.azure.com), nel riquadro di spostamento a sinistra di hello, selezionare hello **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Andare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd una nuova applicazione, seleziona hello **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **HR2day da Merces**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. Nel riquadro dei risultati hello, selezionare **HR2day da Merces**, quindi selezionare hello **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con HR2day by Merces usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow chi hello controparte utente in HR2day da Merces tooa utente in Azure AD. In altre parole, è necessario un collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in HR2day da Merces tooestablish.

In HR2day da Merces, assegnare hello **nome utente** in Azure AD troppo **Username** relazione hello tooestablish.

tooconfigure e prova AD Azure single sign-on con HR2day da Merces, è necessario hello toocomplete seguenti blocchi predefiniti:

1. [Configurare Azure AD single sign-on](#configuring-azure-ad-single-sign-on): abilitare il toouse agli utenti di questa funzionalità.
2. [Creare un utente di test di Azure AD](#creating-an-azure-ad-test-user): per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. [Creare un HR2day utente test Merces](#creating-an-hr2day-by-merces-test-user): creare un equivalente di Britta Simon in HR2day da Merces che è la rappresentazione toohello collegato Azure AD dell'utente.
4. [Assegnare l'utente test hello Azure AD](#assigning-the-azure-ad-test-user): abilitare Britta Simon toouse AD Azure single sign-on.
5. [Testare single sign-on](#testing-single-sign-on): verificare se funziona configurazione hello.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel HR2day dall'applicazione Merces.

**Azure AD tooconfigure single sign-on con HR2day da Merces, richiedere hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **HR2day da Merces** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. tooenable accesso single sign-on, in hello **Single sign-on** nella finestra di dialogo **modalità** come **basato su SAML Sign-on**.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. In hello **HR2day Merces dominio e gli URL** sezione, richiedere hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. In hello **Sign-on URL** casella, digitare un URL utilizzando hello seguente motivo: `https://<tenantname>.force.com/<instancename>`.

    b. In hello **identificatore** casella, digitare un URL utilizzando hello seguente motivo: `https://hr2day.force.com/<companyname>`.

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con URL hello effettivo sign-on e l'identificatore. Contatto hello [HR2day dal team di supporto client Merces](mailto:servicedesk@merces.nl) tooget questi valori. 
 


4. In hello **certificato di firma SAML** selezionare **Certificate(Base64)**e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. Questa sezione viene descritto come tooenable utenti tooauthenticate tooHR2day da Merces con il proprio account in Azure AD. Tale scopo, usando la federazione basata sul protocollo SAML hello.

    Il HR2day dall'applicazione Merces prevede asserzioni SAML hello in un formato specifico, che richiede il token SAML tooyour di tooadd attributo personalizzato mapping. Hello seguente schermata mostra un esempio di questo oggetto. 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Prima di poter configurare l'asserzione SAML hello, è necessario contattare hello [HR2day dal team di supporto Merces Client](mailto:servicedesk@merces.nl) e valore hello dell'attributo dell'identificatore univoco hello per le richieste per il tenant. È necessario passaggi di hello toocomplete questo valore nella sezione successiva hello. 

6. In hello **Single sign-on** della finestra di dialogo hello **gli attributi utente** sezione, configurare un attributo di token SAML hello, come illustrato nella seguente immagine hello. Richiedere quindi hello alla procedura seguente.
    
      | Nome attributo    |   Valore attributo |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | join([mail],"102938475Z","@" |
    
      a. hello tooopen **Aggiungi attributo** finestra di dialogo Seleziona **Aggiungi attributo**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. In hello **nome** digitare **ATTR_LOGINCLAIM**.

    c. Da hello **valore** elenco, selezionare **join**.

    d. Da hello **String1** elenco, selezionare **user.mail**.

    e. Per **String2**, digitare l'identificatore univoco di hello che viene fornito dal team HR2day.

    f. In hello **separatore** digitare  **@** .
    
    g. Selezionare **OK**.

7. Seleziona hello **salvare** pulsante.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. In hello **HR2day dalla configurazione Merces** selezionare **configurare HR2day da Merces** tooopen hello **Configura sign-on** finestra. Hello copia **Sign-Out URL**, **ID entità SAML**, e **SAML Single Sign-On Service URL** da hello **riferimento rapido** sezione.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. tooconfigure SSO per l'applicazione, contattare di hello [HR2day dal team di supporto client Merces](mailTo:servicedesk@merces.nl). Collegare hello scaricato **Certificate(Base64)** file tooyour messaggio di posta elettronica. Forniscono anche hello **Sign-Out URL**, **ID entità SAML**, e **SAML Single Sign-On Service URL** in modo che può essere configurati per l'integrazione di SSO.

    > [!NOTE]
    >Ricordare toohello Merces team necessarie per l'integrazione hello toobe ID entità impostata con il modello di hello **https://hr2day.force.com/INSTANCENAME**.

    > [!TIP]
    >È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo aver aggiunto questa app da hello **Active Directory** > **applicazioni aziendali** sezione, seleziona hello **Single Sign-On** scheda. Quindi hello accesso incorporati documentazione tramite hello **configurazione** sezione nella parte inferiore di hello. Altre informazioni sulla funzionalità di documentazione embedded hello in hello [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate richiedere hello alla procedura seguente:**

1. In hello **portale di Azure**, nel riquadro di spostamento a sinistra di hello, selezionare hello **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi selezionare **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** nella finestra di dialogo **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. In hello **utente** nella finestra di dialogo hello take alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    a. In hello **nome** digitare **BrittaSimon**.

    b. In hello **nome utente** casella, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password**e quindi annotare la password di hello.

    d. Selezionare **Crea**.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>Creare un utente di test di HR2day Merces

obiettivo di Hello di questa sezione è un utente chiamato Britta Simon in HR2day da Merces toocreate. gli utenti di hello tooadd nell'account hello HR2day, lavorare con hello [HR2day dal team di supporto client Merces](mailto:servicedesk@merces.nl). 

> [!NOTE]
> Se è necessario un utente toocreate manualmente, contattare hello [HR2day dal team di supporto client Merces](mailto:servicedesk@merces.nl).

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooHR2day proprio accesso da Merces.

![Assegnare utenti][200] 

**tooassign Britta Simon tooHR2day da Merces, richiedere hello alla procedura seguente:**

1. In hello Azure hello portale, aprire applicazioni consente di visualizzare, Vai a visualizzazione directory toohello e quindi andare troppo**applicazioni aziendali**. Selezionare quindi **Tutte le applicazioni**.

    ![Assegnare utenti][201] 

2. Nell'elenco di applicazioni hello, selezionare **HR2day da Merces**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. Dal menu hello hello sinistra, selezionare **utenti e gruppi**.

    ![Assegnare utenti][202] 

4. Seleziona hello **Aggiungi** pulsante. Quindi, nel hello **Aggiungi** nella finestra di dialogo **utenti e gruppi**.

    ![Assegnare utenti][203]

5. In hello **utenti e gruppi** della finestra di dialogo hello **utenti** elenco, selezionare **Britta Simon**.

6. Fare clic su hello **selezionare** pulsante.

7. In hello **Aggiungi** nella finestra di dialogo **assegnare**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

obiettivo di questa sezione Hello è tootest hello di configurazione di Azure AD single sign-on tramite Pannello di accesso.  

Quando si seleziona hello HR2day dal riquadro Merces in hello Pannello di accesso, l'utente automaticamente ottenere connesso tooyour HR2day dall'applicazione Merces.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

