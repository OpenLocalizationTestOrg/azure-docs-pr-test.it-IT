---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cloud Management Portal for Microsoft Azure | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e il portale di gestione di Cloud di Microsoft Azure.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a>Esercitazione: Integrazione di Azure Active Directory con Cloud Management Portal for Microsoft Azure

In questa esercitazione, è illustrato come toointegrate portale di gestione di Cloud di Microsoft Azure con Azure Active Directory (Azure AD).

Integrazione di portale di gestione di Cloud di Microsoft Azure con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooCloud portale di gestione per Microsoft Azure
- È possibile abilitare l'utenti tooautomatically get connesso tooCloud portale di gestione per Microsoft Azure (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con il portale di gestione di Cloud di Microsoft Azure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione abilitata di Cloud Management Portal per Microsoft Azure Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiungere il portale di gestione di Cloud di Microsoft Azure dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a>Aggiungere il portale di gestione di Cloud di Microsoft Azure dalla raccolta hello
tooconfigure hello integrazione del portale di gestione di Cloud di Microsoft Azure AD Azure, è necessario tooadd il portale di gestione di Cloud di Microsoft Azure dall'elenco di tooyour hello raccolta di App SaaS gestite.

**Portale di gestione di Cloud di Microsoft Azure dalla raccolta di hello, tooadd eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **portale di gestione di Cloud di Microsoft Azure**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. Nel riquadro dei risultati hello, selezionare **portale di gestione di Cloud di Microsoft Azure**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cloud Management Portal for Microsoft Azure mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nel portale di gestione di Cloud per Microsoft Azure è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello nel portale di gestione di Cloud per Microsoft Azure deve toobe stabilita.

Nel portale di gestione di Cloud per Microsoft Azure, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test con il portale di gestione di Cloud AD Azure single sign-on a Microsoft Azure, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un portale di gestione di Cloud di Microsoft Azure test](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  -toohave un equivalente di Britta Simon nel portale di gestione di Cloud per Microsoft Azure che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nel portale di gestione del Cloud per l'applicazione di Microsoft Azure.

**tooconfigure AD Azure single sign-on con il portale di gestione di Cloud di Microsoft Azure, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **portale di gestione di Cloud di Microsoft Azure** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. In hello **portale di gestione di Cloud per dominio di Microsoft Azure e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    a. In hello **Sign-on URL** , digitare un URL utilizzando hello seguenti modelli: 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    b. In hello **identificatore** , digitare un URL utilizzando hello seguenti modelli: 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    c. In hello **URL di risposta** , digitare un URL utilizzando hello seguenti modelli: 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con URL di risposta, identificatore e Sign-On URL effettivo hello. Contatto [portale di gestione per il team di supporto Client di Microsoft Azure Cloud](mailto:jczernuszka@newsignature.com) tooget questi valori. 
 
4. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. In hello **portale di gestione di Cloud per la configurazione di Microsoft Azure** fare clic su **configurare portale di gestione Cloud per Microsoft Azure** tooopen **Configura sign-on**finestra. Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. tooconfigure single sign-on sul **portale di gestione di Cloud di Microsoft Azure** lato, è necessario hello toosend scaricato **certificato**, **Sign-Out URL**, **SAML Single Sign-On Service URL** e **ID entità SAML** troppo[portale di gestione per il team di supporto di Microsoft Azure Cloud](mailto:jczernuszka@newsignature.com). Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a>Creazione di un utente test di Cloud Management Portal for Microsoft Azure

obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon nel portale di gestione di Cloud di Microsoft Azure. Rivolgersi [portale di gestione per il team di supporto di Microsoft Azure Cloud](mailto:jczernuszka@newsignature.com) utenti hello tooadd hello portale di gestione di Cloud per l'account di Microsoft Azure.


### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCloud portale di gestione per Microsoft Azure.

![Assegna utente][200] 

**tooassign Britta Simon tooCloud portale di gestione per Microsoft Azure, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **portale di gestione di Cloud di Microsoft Azure**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.
Quando si fa clic hello portale di gestione di Cloud per il riquadro di Microsoft Azure in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato nel portale di gestione di Cloud per l'applicazione di Microsoft Azure.

Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

