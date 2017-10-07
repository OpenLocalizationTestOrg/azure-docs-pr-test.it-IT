---
title: 'Esercitazione: Integrazione di Azure Active Directory con Teamphoria| Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Teamphoria.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>Esercitazione: Integrazione di Azure Active Directory con Teamphoria

In questa esercitazione, è illustrato come toointegrate Teamphoria con Azure Active Directory (Azure AD).

Integrazione Teamphoria con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooTeamphoria
- È possibile abilitare l'utenti tooautomatically get connesso tooTeamphoria (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Teamphoria tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Teamphoria abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Teamphoria dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-teamphoria-from-hello-gallery"></a>Aggiunta di Teamphoria dalla raccolta hello
integrazione hello tooconfigure di Teamphoria in Azure AD, è necessario tooadd Teamphoria dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Teamphoria dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Teamphoria**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. Nel riquadro dei risultati hello, selezionare **Teamphoria**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Teamphoria usando un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Teamphoria è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Teamphoria deve toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Teamphoria.

tooconfigure e prova AD Azure single sign-on con Teamphoria, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Teamphoria](#creating-a-teamphoria-test-user)**  -toohave un equivalente di Britta Simon in Teamphoria toohello collegato AD Azure rappresentazione in seguito.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione Teamphoria.

**Azure AD tooconfigure single sign-on con Teamphoria, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello in hello **Teamphoria** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. In hello **Teamphoria dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare l'URL hello utilizzando hello seguente motivo:`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > Si noti che queste non sono valori reali hello. Hai tooupdate questi valori con hello URL effettivo Sign-On. Contatto [team di supporto Teamphoria Client](https://www.teamphoria.com/) tooget hello Sign-on URL. 

4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il certificato di hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. In hello **Teamphoria configurazione** fare clic su **configurare Teamphoria** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. tooconfigure single sign-on sul **Teamphoria** lato, applicazione Teamphoria tooyour di account di accesso come amministratore.

8. Andare troppo**le impostazioni di amministrazione** opzione nella barra degli strumenti a sinistra di hello e in hello hello scheda Configurazione fare clic su **SINGLE SIGN-ON** finestra di configurazione SSO tooopen hello.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. Fare clic su **Aggiungi nuovo PROVIDER di identità** opzione nel modulo di hello angolo superiore destro tooopen hello per l'aggiunta di impostazioni di hello per SSO.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. Immettere i dettagli di hello nei campi hello, come descritto di seguito

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    a. **NOME visualizzato** : immettere il nome visualizzato hello di plug-in hello nella pagina di amministrazione di hello.

    b. **Nome pulsante** : nome hello della scheda hello che verrà visualizzato nella pagina di accesso hello per l'accesso tramite SSO.

    c. **CERTIFICATO** : hello aprire certificato scaricato in precedenza dal portale di Azure nel blocco note, copia hello contenuto di hello hello stesso e incollarlo qui nella casella hello.

    d. **PUNTO di ingresso** : hello Incolla **SAML Single Sign-On Service URL** copiati precedenti hello modulo portale di Azure.

    e. Opzione troppo opzione hello**ON** e fare clic su **salvare**. 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-teamphoria-test-user"></a>Creare un utente test di Teamphoria

In ordine tooenable Azure AD utenti toolog in Teamphoria, è necessario eseguirne il provisioning in Teamphoria. Nel caso di hello di Teamphoria, il provisioning è un'attività manuale.

**eseguire un account utente, tooprovision hello i passaggi seguenti:**

1. Accedi tooyour sito della società Teamphoria come amministratore.

2. Fare clic su **ADMIN** impostazioni sulla barra degli strumenti a sinistra di hello e in hello **GESTISCI** fare clic su scheda **utenti** pagina di amministrazione di hello tooopen per gli utenti.

    ![Aggiungere un dipendente](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. Fare clic su hello **manuale INVITARE** opzione.

    ![Invita persone](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. In questa pagina effettuare l'operazione seguente. 
    
    ![Invita persone](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    a. In hello **indirizzo di posta elettronica** casella di testo, hello **indirizzo di posta elettronica** di BrittaSimon.

    b. In hello **nome** casella tipo **Laura**.

    c. In hello **cognome** casella tipo **Simon**.

    d. Fare clic su **INVITE 1 USER** (Invita 1 utente). L'utente deve tooaccept hello invito tooget creata nel sistema hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooTeamphoria proprio accesso.

![Assegna utente][200] 

**tooassign Britta Simon tooTeamphoria, eseguire hello alla procedura seguente:**

1. Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Teamphoria**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso. Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

