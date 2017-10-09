---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jitbit Helpdesk | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Jitbit Helpdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a>Esercitazione: Integrazione di Azure Active Directory con Jitbit Helpdesk

In questa esercitazione, è illustrato come toointegrate Jitbit Helpdesk con Azure Active Directory (Azure AD).

Integrazione di Jitbit Helpdesk con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooJitbit Helpdesk
- È possibile abilitare l'utenti tooautomatically get connesso tooJitbit Helpdesk (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con Jitbit Helpdesk, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Jitbit Helpdesk abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Jitbit Helpdesk dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a>Aggiunta di Jitbit Helpdesk dalla raccolta hello
integrazione hello tooconfigure di Jitbit Helpdesk in Azure AD, è necessario tooadd Jitbit Helpdesk dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Jitbit Helpdesk dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Jitbit Helpdesk**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. Nel riquadro dei risultati hello, selezionare **Jitbit Helpdesk**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Jitbit Helpdesk in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Jitbit Helpdesk è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Jitbit Helpdesk deve toobe stabilita.

In Jitbit Helpdesk, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test Azure single sign-on AD con Jitbit Helpdesk, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  -toohave un equivalente di Britta Simon in Jitbit Helpdesk che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Jitbit Helpdesk.

**Azure AD tooconfigure single sign-on con Jitbit Helpdesk, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Jitbit Helpdesk** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. In hello **Jitbit Helpdesk dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello: 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > Poiché non è reale, Aggiorna il valore con hello URL effettivo Sign-On. Contatto [team di supporto Client di Jitbit Helpdesk](https://www.jitbit.com/support/) tooget questo valore. 
    
    b.  In hello **identificatore** casella di testo, digitare un URL come riportato di seguito:`https://www.jitbit.com/web-helpdesk/`

    
 


4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. In hello **Jitbit Helpdesk configurazione** fare clic su **configurare Jitbit Helpdesk** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. In un'altra finestra del Web browser accedere al sito aziendale di Jitbit Helpdesk come amministratore.

8. Nella barra degli strumenti hello in primo piano hello, fare clic su **amministrazione**.
   
    ![Amministrazione](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Amministrazione")

9. Fare clic su **General settings**.
   
    ![Users, companies and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies and permissions")

10. In hello **le impostazioni di autenticazione** configurazione seguire hello alla procedura seguente:
   
    ![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")
    
    a. Selezionare **accesso Enable SAML 2.0 single**, toosign utilizzando Single Sign-On (SSO), con **OneLogin**.

    b. In hello **URL dell'EndPoint** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.

    c. Aprire il **base 64** codificato nel blocco note, hello copia del contenuto di esso negli Appunti, certificato e quindi incollarlo toohello **certificato x. 509** casella di testo

    d. Fare clic su **Salva modifiche**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella di testo, il nome di tipo come **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a>Creazione di un utente test di Jitbit Helpdesk

In ordine tooenable Azure AD utenti toolog in Jitbit Helpdesk, è necessario eseguirne il provisioning in Jitbit Helpdesk.  Nel caso di hello di Jitbit Helpdesk, il provisioning è un'attività manuale.

**tooprovision un account utente, eseguire hello alla procedura seguente:**

1. Accedi tooyour **Jitbit Helpdesk** tenant.

2. Scegliere dal menu hello in primo piano hello **amministrazione**.
   
    ![Amministrazione](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Amministrazione")

3. Fare clic su **Users, companies and permissions**.
   
    ![Users, companies and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies and permissions")

4. Fare clic su **Add User**.
   
    ![Aggiungere un utente](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Aggiungere un utente")
   
5. Nella sezione creare hello, digitare dati hello dell'account di Azure AD hello desiderato tooprovision come indicato di seguito:

    ![Creare](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Creare")
   
   a. In hello **Username** casella tipo **BrittaSimon**, nome utente hello come hello portale di Azure.

   b. In hello **posta elettronica** casella di testo, come di tipo messaggio di posta elettronica dell'utente hello  **BrittaSimon@contoso.com** .

   c. In hello **nome** casella di testo Nome tipo di utente hello come **Laura**.

   d. In hello **cognome** casella di testo, digitare cognome dell'utente hello come **Simon**.
   
   e. Fare clic su **Crea**.

>[!NOTE]
>È possibile usare qualsiasi altro Jitbit Helpdesk utente account strumento di creazione o qualsiasi API fornita da Jitbit Helpdesk tooprovision degli account utente di Azure AD.
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooJitbit supporto tecnico.

![Assegna utente][200] 

**tooassign Britta Simon tooJitbit Helpdesk, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Jitbit Helpdesk**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello Jitbit Helpdesk riquadro in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione di Jitbit Helpdesk.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

