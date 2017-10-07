---
title: 'Esercitazione: Integrazione di Azure Active Directory con FreshDesk | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e FreshDesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>Esercitazione: Integrazione di Azure Active Directory con FreshDesk

In questa esercitazione, è illustrato come toointegrate FreshDesk con Azure Active Directory (Azure AD).

Integrazione di FreshDesk con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooFreshDesk
- È possibile abilitare l'utenti tooautomatically get connesso tooFreshDesk (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con FreshDesk tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di FreshDesk abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di FreshDesk dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-freshdesk-from-hello-gallery"></a>Aggiunta di FreshDesk dalla raccolta hello
integrazione hello tooconfigure di FreshDesk in Azure AD, è necessario tooadd FreshDesk dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd FreshDesk dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **FreshDesk**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. Nel riquadro dei risultati hello, selezionare **FreshDesk**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FreshDesk in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in FreshDesk è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in FreshDesk richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in FreshDesk.

tooconfigure e test Azure single sign-on AD con FreshDesk, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test FreshDesk](#creating-a-freshdesk-test-user)**  -toohave un equivalente di Britta Simon in FreshDesk toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on in freshservice.

**Azure AD tooconfigure single sign-on con FreshDesk, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello in hello **FreshDesk** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. In hello **FreshDesk dominio e gli URL** sezione, immettere hello **Sign-on URL** come: `https://<tenant-name>.freshdesk.com` o qualsiasi altro valore Freshdesk ha suggerito.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > Si noti che questo non è il valore reale. È necessario aggiornare questo valore con l'URL di accesso effettivo. Per ottenere tale valore, contattare il [team di supporto di FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg).  

4. In hello **certificato di firma SAML** fare clic su **certificato** e quindi salvare il certificato di hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. In hello **FreshDesk configurazione** fare clic su **FreshDesk configurare** finestra tooopen Configura sign-on. Copiare hello SAML Single Sign-On Service URL e Sign-Out URL da hello **riferimento rapido** sezione.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. In un'altra finestra del Web browser accedere al sito aziendale di Freshdesk come amministratore.

8. Scegliere dal menu hello in primo piano hello **Admin**.
   
   ![Amministratore](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Amministratore")

9. In hello **impostazioni generali** scheda, fare clic su **sicurezza**.
   
   ![Sicurezza](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Sicurezza")

10. In hello **sicurezza** seguire hello alla procedura seguente:
   
    ![Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign-On")
   
    a. Per **Single Sign On (SSO)** selezionare **On**.

    b. Selezionare **SAML SSO**.

    c. Hello tipo **SAML Single Sign-On Service URL** copiati dal portale Azure nel hello **SAML Login URL** casella di testo.

    d. Hello tipo **Sign-Out URL** copiati dal portale Azure nel hello **Logout URL** casella di testo.

    e. Hello copia **identificazione personale** valore dal certificato hello scaricato dal portale di Azure e incollarlo in hello **Security Certificate Fingerprint** casella di testo.  
 
    >[!TIP]
    >Per ulteriori informazioni, vedere [come tooretrieve il valore di identificazione personale del certificato](http://youtu.be/YKQF266SAxI). 
    
    f. Fare clic su **Save**.


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-freshdesk-test-user"></a>Creazione di un utente test di FreshDesk

In ordine tooenable Azure AD utenti toolog a FreshDesk, è necessario eseguirne il provisioning in FreshDesk.  
Nel caso di hello di FreshDesk, il provisioning è un'attività manuale.

**eseguire un account utente, tooprovision hello i passaggi seguenti:**

1. Accedi tooyour **Freshdesk** tenant.
2. Scegliere dal menu hello in primo piano hello **Admin**.
   
   ![Amministratore](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Amministratore")

3. In hello **impostazioni generali** scheda, fare clic su **agenti**.
   
   ![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")

4. Fare clic su **New Agent**.
   
    ![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")

5. Nella finestra di dialogo informazioni sull'agente hello eseguire hello alla procedura seguente:
   
   ![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")
   
   a. In hello **nome completo** casella di testo Nome hello del tipo di account di Azure AD hello si vuole tooprovision.

   b. In hello **posta elettronica** casella di testo, hello tipo AD Azure indirizzo di posta elettronica dell'account di Azure AD hello si desidera tooprovision.

   c. In hello **titolo** casella di testo, titolo hello tipo di account di Azure AD hello si vuole tooprovision.

   d. Selezionare **Agents role** e quindi fare clic su **Assign**.
       
   e. Fare clic su **Salva**.     
   
    >[!NOTE]
    >titolare dell'account di Azure AD di Hello riceverà un messaggio di posta elettronica che include un account di hello tooconfirm collegamento prima dell'effettiva attivazione. 
    > 
    
    >[!NOTE]
    >È possibile usare qualsiasi altro Freshdesk utente account strumento di creazione o le API fornite da Freshdesk tooprovision account utente di AAD. tooFreshDesk.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooBox proprio accesso.

![Assegna utente][200] 

**tooassign Britta Simon tooFreshDesk, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **FreshDesk**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro FreshDesk hello in hello Pannello di accesso, è necessario ottenere l'account di accesso pagina tooget connesso tooyour freshservice.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

