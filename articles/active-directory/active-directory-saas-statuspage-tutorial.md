---
title: 'Esercitazione: Integrazione di Azure Active Directory con StatusPage | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e StatusPage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a>Esercitazione Integrazione di Azure Active Directory con StatusPage

In questa esercitazione, è illustrato come toointegrate StatusPage con Azure Active Directory (Azure AD).

Integrazione StatusPage con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooStatusPage
- È possibile abilitare l'utenti tooautomatically get connesso tooStatusPage (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con StatusPage tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di StatusPage abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di StatusPage dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-statuspage-from-hello-gallery"></a>Aggiunta di StatusPage dalla raccolta hello
integrazione hello tooconfigure di StatusPage in Azure AD, è necessario tooadd StatusPage dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd StatusPage dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **StatusPage**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. Nel riquadro dei risultati hello, selezionare **StatusPage**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con StatusPage in base a un utente di test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in StatusPage è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in StatusPage deve toobe stabilita.

In StatusPage, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con StatusPage, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test StatusPage](#creating-a-statuspage-test-user)**  -toohave un equivalente di Britta Simon in StatusPage che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione StatusPage.

**Azure AD tooconfigure single sign-on con StatusPage, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **StatusPage** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. In hello **StatusPage dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello: 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > Contattare il team di supporto StatusPage hello in [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest i metadati necessari tooconfigure accesso single sign-on. 
    >
    >a. Dai metadati hello, copiare il valore di autorità di certificazione hello e quindi incollarlo hello **identificatore** casella di testo.
    >
    >b. Dai metadati hello, copiare l'URL di risposta hello e quindi incollarlo hello **URL di risposta** casella di testo.

4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. In hello **StatusPage configurazione** fare clic su **configurare StatusPage** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. In un'altra finestra del browser, accedere come amministratore nel sito della società di tooyour StatusPage.

8. Nella barra degli strumenti principale hello, fare clic su **Gestisci Account**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. Fare clic su hello **Single Sign-on** scheda. 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. Nella pagina di installazione SSO hello, eseguire hello alla procedura seguente:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    a. In hello **SSO Target URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.

    b. Aprire il certificato scaricato nel blocco note, hello copia il contenuto e quindi incollarlo hello **certificato** casella di testo. 

    c. Fare clic su **SALVA CONFIGURAZIONE**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-statuspage-test-user"></a>Creazione di un utente test per StatusPage

obiettivo di Hello di questa sezione è un utente denominato Britta Simon in StatusPage toocreate.

StatusPage supporta il provisioning JIT (just-in-time), È già stato abilitato in [Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on).

**un utente denominato Britta Simon in StatusPage, toocreate eseguire hello alla procedura seguente:**

1. Sito dell'azienda StatusPage tooyour accesso come amministratore.

2. Scegliere dal menu hello in primo piano hello **Gestisci Account**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. Fare clic su hello **i membri del Team** scheda. 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. Fare clic su **AGGIUNGI MEMBRO DEL TEAM**. 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. Hello tipo **indirizzo di posta elettronica**, **nome**, e **nome Sur** di un utente valido desiderate tooprovision hello relative caselle di testo. 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. Per **Ruolo** scegliere **Client Administrator** (Amministratore client).

7. Fare clic su **CREA ACCOUNT**.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooStatusPage.

![Assegna utente][200] 

**tooassign Britta Simon tooStatusPage, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **StatusPage**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.

Quando si fa clic su riquadro StatusPage hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour StatusPage applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

