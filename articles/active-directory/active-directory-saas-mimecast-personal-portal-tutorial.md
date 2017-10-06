---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mimecast Personal Portal | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Mimecast Personal Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a>Esercitazione: Integrazione di Azure Active Directory con Mimecast Personal Portal

In questa esercitazione, è illustrato come toointegrate Mimecast Personal Portal con Azure Active Directory (Azure AD).

Integrazione di Mimecast Personal Portal con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooMimecast Personal Portal
- È possibile abilitare l'utenti tooautomatically get connesso tooMimecast Personal Portal (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con Mimecast Personal Portal, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Mimecast Personal Portal abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Mimecast Personal Portal dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a>Aggiunta di Mimecast Personal Portal dalla raccolta hello
integrazione hello tooconfigure di Mimecast Personal Portal in Azure AD, è necessario tooadd Mimecast Personal Portal dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Mimecast Personal Portal dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Mimecast Personal Portal**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. Nel riquadro dei risultati hello, selezionare **Mimecast Personal Portal**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mimecast Personal Portal con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Mimecast Personal Portal è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Mimecast Personal Portal deve toobe stabilita.

In Mimecast Personal Portal, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Mimecast Personal Portal, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Mimecast Personal Portal](#creating-a-mimecast-personal-portal-test-user)**  -toohave un equivalente di Britta Simon in Mimecast Personal Portal che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Mimecast Personal Portal.

**tooconfigure AD Azure single sign-on con Mimecast Personal Portal, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Mimecast Personal Portal** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. In hello **Mimecast Personal Portal dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello: 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto Client di Mimecast Personal Portal](https://www.mimecast.com/customer-success/technical-support/) tooget questi valori. 
 


4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. In hello **Mimecast Personal Portal configurazione** fare clic su **configurare Mimecast Personal Portal** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. In un'altra finestra del Web browser accedere a Mimecast Personal Portal come amministratore.

8. Andare troppo**servizi \> applicazioni**.
   
    ![Applicazioni](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applicazioni")

9. Fare clic su **Authentication Profiles**.
   
    ![Profili di autenticazione](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Profili di autenticazione")

10. Fare clic su **New Authentication Profile**.
   
    ![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")

11. In hello **Authentication Profile** seguire hello alla procedura seguente:
   
    ![Profilo di autenticazione](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Profilo di autenticazione")
   
    a. In hello **descrizione** casella di testo, digitare un nome per la configurazione.
   
    b. Selezionare **Enforce SAML Authentication for Mimecast Personal Portal**.
   
    c. Come **Provider** selezionare **Azure Active Directory**.
   
    d. In **URL autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML** che è stato copiato dal portale di Azure.
   
    e. In **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.
   
    f. In **Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.

    g. Aprire il **base 64** codificato nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti, certificato e quindi incollarlo toohello **Identity Provider Certificate (Metadata)** casella di testo.

    h. Selezionare **Allow Single Sign On**.
   
    i. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a>Creazione di un utente test di Mimecast Personal Portal

In ordine tooenable Azure AD utenti toolog a Mimecast Personal Portal, è necessario eseguirne il provisioning in Mimecast Personal Portal. Nel caso di hello di Mimecast Personal Portal, il provisioning è un'attività manuale.

Prima di poter creare utenti, è necessario tooregister un dominio.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Accesso tooyour **Mimecast Personal Portal** come amministratore.

2. Andare troppo**directory \> interno**.
   
    ![Directory](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directory")

3. Fare clic su **Register New Domain**.
   
    ![Registra nuovo dominio](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Registra nuovo dominio")

4. Dopo aver creato il nuovo dominio, fare clic su **New Address**.
   
    ![Nuovo indirizzo](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "Nuovo indirizzo")

5. In hello indirizzo finestra di dialogo Nuovo, eseguire hello seguendo i passaggi di un valido di Azure si desidera tooprovision di account di Active Directory:
   
    ![Salvare](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Salvare")
   
    a. In hello **indirizzo di posta elettronica** casella tipo **indirizzo di posta elettronica** dell'utente hello come  **BrittaSimon@contoso.com** .
    
    b. In hello **nome globale** casella di testo, hello tipo **username** come **BrittaSimon**.

    c. In hello **Password**, e **Conferma Password** nelle caselle di testo, hello tipo **Password** dell'utente hello.
   
    b. Fare clic su **Salva**.

>[!NOTE]
>È possibile utilizzare qualsiasi altro strumento di creazione di account utente Mimecast Personal Portal o le API fornite da account utente di Azure AD tooprovision Mimecast Personal Portal. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMimecast Personal Portal.

![Assegna utente][200] 

**tooassign Britta Simon tooMimecast Personal Portal, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Mimecast Personal Portal**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On
In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro Mimecast Personal Portal hello in hello Pannello di accesso, è necessario ottenere applicazione Mimecast Personal Portal tooyour automaticamente firmato-on. Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

