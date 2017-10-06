---
title: 'Esercitazione: Integrazione di Azure Active Directory con &frankly | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e & Francamente.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 92677b6fcd8609ca31f82a30e85c7010b7bb3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a>Esercitazione: Integrazione di Azure Active Directory con &frankly

In questa esercitazione, è illustrato come toointegrate & Francamente con Azure Active Directory (Azure AD).

L'integrazione di & Francamente con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso troppo & Francamente
- È possibile abilitare gli utenti tooautomatically ottenere connesso troppo & Francamente (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD tooconfigure con & Francamente, necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di &frankly abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di & Francamente dalla raccolta di hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-frankly-from-hello-gallery"></a>Aggiunta di & Francamente dalla raccolta di hello
integrazione di hello tooconfigure di & Francamente in Azure AD, è necessario tooadd & Francamente dall'elenco di tooyour hello della raccolta di App SaaS gestite.

**tooadd & Francamente dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **& Francamente**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. Nel riquadro dei risultati hello, selezionare **& Francamente**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con &frankly in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow cosa hello utente corrispondente in & francamente è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e hello correlati in & utente Francamente toobe esigenze stabilita.

In & Francamente, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con & Francamente, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un & Francamente utente test](#creating-a-frankly-test-user)**  -toohave un equivalente di Britta Simon in & Francamente ovvero toohello collegato rappresentazione in forma di Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel & Francamente applicazioni.

**Azure AD tooconfigure singolo sign-on con & Francamente, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **& Francamente** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. In hello **& Francamente dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    a. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`

    b. In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`

4. Selezionare **Mostra impostazioni URL avanzate** Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`
    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello identificatore effettivo, Sign-on e URL di risposta. Contatto [team di supporto andfrankly](mailto:help@andfrankly.com) tooget questi valori.

5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. tooconfigure single sign-on sul **& Francamente** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto andfrankly](mailto:help@andfrankly.com). 

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-frankly-test-user"></a>Creazione di un utente test di &frankly

In questa sezione viene creato un utente chiamato Britta Simon in &frankly. Lavorare con [team di supporto andfrankly](mailto:help@andfrankly.com) gli utenti di hello tooadd hello & Francamente platform.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo l'accesso troppo & Francamente.

![Assegna utente][200] 

**tooassign Britta Simon & Francamente, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **& Francamente**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.

Quando fa clic su hello & si Francamente riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour & Francamente applicazioni

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

