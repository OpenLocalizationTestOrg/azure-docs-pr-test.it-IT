---
title: 'Esercitazione: Integrazione di Azure Active Directory con Thoughtworks Mingle | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Thoughtworks Mingle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a>Esercitazione: Integrazione di Azure Active Directory con Thoughtworks Mingle

In questa esercitazione, è illustrato come toointegrate Thoughtworks Mingle con Azure Active Directory (Azure AD).

Integrazione di Thoughtworks Mingle con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooThoughtworks Mingle
- È possibile abilitare l'utenti tooautomatically get connesso tooThoughtworks Mingle (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Thoughtworks Mingle tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Thoughtworks Mingle abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Thoughtworks Mingle dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a>Aggiunta di Thoughtworks Mingle dalla raccolta hello
integrazione hello tooconfigure di Thoughtworks Mingle in Azure AD, è necessario tooadd Thoughtworks Mingle dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Thoughtworks Mingle dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![pulsante di Hello Azure Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Nuovo pulsante dell'applicazione Hello][3]

4. Nella casella di ricerca hello, digitare **Thoughtworks Mingle**selezionare **Thoughtworks Mingle** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Thoughtworks Mingle nell'elenco risultati hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Thoughtworks Mingle usando un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Thoughtworks Mingle è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Thoughtworks Mingle deve toobe stabilita.

In Thoughtworks Mingle, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Thoughtworks Mingle, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creare un utente test Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave un equivalente di Britta Simon in Thoughtworks Mingle che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Thoughtworks Mingle.

**Azure AD tooconfigure single sign-on con Thoughtworks Mingle, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Thoughtworks Mingle** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. In hello **Thoughtworks Mingle dominio e gli URL** seguire hello alla procedura seguente:

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.mingle.thoughtworks.com`

    > [!NOTE] 
    > il valore di Hello non è di tipo real. Il valore di hello aggiornamento con hello URL effettivo Sign-On. Contatto [team di supporto Client di Thoughtworks Mingle](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) valore hello tooget. 
 
4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![collegamento al download del certificato Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. Accedi tooyour **Thoughtworks Mingle** sito aziendale come amministratore.

7. Fare clic su hello **Admin** scheda e quindi fare clic su **SSO Config**.
   
    ![Scheda Amministrazione](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Config SSO")

8. In hello **SSO Config** seguire hello alla procedura seguente:
   
    ![Configurazione dell'accesso SSO](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configurazione dell'accesso SSO")
    
    a. file di metadati hello tooupload, fare clic su **Choose file**. 

    b. Fare clic su **Salva modifiche**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente test di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-a-thoughtworks-mingle-test-user"></a>Creare un utente di test di Thoughtworks Mingle

Per Azure AD utenti toobe in grado di toosign in devono essere sottoposte a provisioning toohello applicazione Thoughtworks Mingle usando i rispettivi nomi utente di Azure Active Directory. Nel caso di hello di Thoughtworks Mingle, il provisioning è un'attività manuale.

**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**

1. Accedi tooyour del sito della società Thoughtworks Mingle come amministratore.

2. Fare clic su **Profilo**.
   
    ![Primo progetto](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Primo progetto")

3. Fare clic su hello **Admin** scheda e quindi fare clic su **utenti**.
   
    ![Utenti](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Utenti")

4. Fare clic su **Nuovo utente**.
   
    ![Nuovo utente](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Nuovo utente")

5. In hello **nuovo utente** finestra di dialogo eseguire hello alla procedura seguente:
   
    ![Finestra di dialogo Nuovo utente](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Nuovo utente")  
 
    a. Hello tipo **nome di accesso**, **nome visualizzato**, **scegliere password**, **Conferma password** di Azure un valido account di Active Directory, si desidera tooprovision in hello relative caselle di testo. 

    b. In **Tipo di utente** selezionare **Base**.

    c. Fare clic su **Crea questo profilo**.

>[!NOTE]
>È possibile usare qualsiasi altro Thoughtworks Mingle utente account strumento di creazione o le API fornite da Thoughtworks Mingle tooprovision account utente di AAD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Assegnare l'utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooThoughtworks Mingle.

![Assegnazione del ruolo utente hello][200] 

**tooassign tooThoughtworks Britta Simon Mingle, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Thoughtworks Mingle**.

    ![collegamento di Thoughtworks Mingle Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![riquadro assegnazione aggiungere Hello][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.

Quando si fa clic su riquadro Thoughtworks Mingle hello in hello Pannello di accesso, è necessario ottenere applicazione Thoughtworks Mingle tooyour automaticamente firmato-on.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

