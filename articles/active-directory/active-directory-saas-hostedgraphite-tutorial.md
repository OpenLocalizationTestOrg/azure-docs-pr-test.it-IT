---
title: 'Esercitazione: Integrazione di Azure Active Directory con Hosted Graphite | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e grafite ospitato.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a>Esercitazione: Integrazione di Azure Active Directory con Hosted Graphite

In questa esercitazione, è illustrato come toointegrate grafite Hosted con Azure Active Directory (Azure AD).

Integrazione grafite ospitato con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooHosted grafite
- È possibile abilitare l'utenti tooautomatically get connesso tooHosted grafite (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con ospitato grafite tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Hosted Graphite abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di grafite ospitato dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-hosted-graphite-from-hello-gallery"></a>Aggiunta di grafite ospitato dalla raccolta hello
integrazione hello tooconfigure di grafite ospitato in Azure AD, è necessario tooadd grafite ospitato dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd grafite ospitato dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **ospitato grafite**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. Nel riquadro dei risultati hello, selezionare **ospitato grafite**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Hosted Graphite mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in grafite ospitato è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in grafite ospitato richiede toobe stabilita.

In grafite ospitato, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con grafite ospitato, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente di test ospitati grafite](#creating-a-hosted-graphite-test-user)**  -toohave un equivalente di Britta Simon in grafite ospitato che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione grafite ospitato.

**Azure AD tooconfigure single sign-on con grafite ospitato, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **ospitato grafite** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. In hello **ospitato grafite dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità avviata da IDP**, eseguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.hostedgraphite.com/metadata/<user id>`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.hostedgraphite.com/complete/saml/<user id>`

4. In hello **ospitato grafite dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **modalità iniziata da SP**, eseguire hello alla procedura seguente:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    a. Fare clic su hello **Mostra URL impostazioni avanzate** opzione

    b. In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.hostedgraphite.com/login/saml/<user id>/`   

    > [!NOTE] 
    > Si noti che queste non sono valori reali hello. Hai tooupdate questi valori con hello effettivo identificatore, un URL di risposta e un URL di accesso. tooget questi valori, è possibile passare tooAccess -> configurazione SAML sul lato applicazione o contatto [team di supporto ospitato grafite](mailto:help@hostedgraphite.com).
    >
 
5. In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. In hello **ospitato configurazione grafite** fare clic su **configurare grafite ospitato** tooopen **Configura sign-on** finestra. Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. Tenant di grafite ospitato tooyour accesso come amministratore.

9. Passare toohello **pagina SAML Setup** nell'intestazione laterale hello (**accesso -> configurazione SAML**).
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. Verificare gli URL corrispondano alla configurazione eseguita su hello **ospitato grafite dominio e gli URL** sezione di hello portale di Azure.
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. In **entità o ID autorità di certificazione** e **URL di accesso SSO** nelle caselle di testo, incollare il valore di hello di **ID entità SAML** e **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure. 
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. Selezionare "**Sola lettura**" come **ruolo utente predefinito**.
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. Aprire il certificato con codifica base 64 nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509** casella di testo.
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. Fare clic sul pulsante **Salva** .

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-hosted-graphite-test-user"></a>Creazione di un utente test di Hosted Graphite

obiettivo di Hello di questa sezione è toocreate un utente denominato Britta Simon in grafite ospitato. Hosted Graphite supporta il provisioning JIT, che è abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Verrà creato un nuovo utente durante una tooaccess tentativo grafite ospitato se non esiste ancora.

>[!NOTE]
>Se è necessario un utente toocreate manualmente, è necessario team di supporto toocontact hello grafite ospitato tramite < mailto:help@hostedgraphite.com >. 

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHosted grafite.

![Assegna utente][200] 

**tooassign Britta Simon tooHosted grafite, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **ospitato grafite**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.

Quando si fa clic su riquadro ospitato grafite hello in hello Pannello di accesso, è necessario ottenere l'applicazione ospitata grafite tooyour automaticamente firmato in.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

