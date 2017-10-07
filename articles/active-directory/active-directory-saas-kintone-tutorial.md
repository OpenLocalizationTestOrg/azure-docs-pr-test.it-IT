---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kintone | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kintone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a>Esercitazione: Integrazione di Azure Active Directory con Kintone

In questa esercitazione, è illustrato come toointegrate Kintone con Azure Active Directory (Azure AD).

Integrazione di Kintone con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooKintone
- È possibile abilitare l'utenti tooautomatically get connesso tooKintone (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Kintone tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Kintone abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Kintone dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-kintone-from-hello-gallery"></a>Aggiunta di Kintone dalla raccolta hello
integrazione hello tooconfigure di Kintone in Azure AD, è necessario tooadd Kintone dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Kintone dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Kintone**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. Nel riquadro dei risultati hello, selezionare **Kintone**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kintone mediante un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Kintone è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Kintone deve toobe stabilita.

In Kintone, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e prova AD Azure single sign-on con Kintone, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Kintone](#creating-a-kintone-test-user)**  -toohave un equivalente di Britta Simon in Kintone che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Kintone.

**Azure AD tooconfigure single sign-on con Kintone, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Kintone** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. In hello **Kintone dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.kintone.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [team di supporto Client di Kintone](https://www.kintone.com/contact/) tooget questi valori. 
 
4. In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. In hello **Kintone configurazione** fare clic su **configurare Kintone** tooopen **Configura sign-on** finestra. Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. In un'altra finestra del Web browser accedere al sito aziendale di **Kintone** come amministratore.

8. Fare clic su **Impostazioni**.
   
    ![Impostazioni](./media/active-directory-saas-kintone-tutorial/ic785879.png "Impostazioni")

9. Fare clic su **Amministrazione utenti e di sistema**.
   
    ![Amministrazione utenti e di sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Amministrazione utenti e di sistema")

10. In **Amministrazione di sistema \> Sicurezza** fare clic su **Accesso**.
   
    ![Account di accesso](./media/active-directory-saas-kintone-tutorial/ic785881.png "Account di accesso")

11. Fare clic su **Abilita autenticazione SAML**.
   
    ![Autenticazione SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Autenticazione SAML")

12. Nella sezione autenticazione SAML hello, eseguire hello alla procedura seguente:
    
    ![Autenticazione SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Autenticazione SAML")
    
    a. In hello **URL di accesso** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.
   
    b. In hello **Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.
    
    c. Fare clic su **Sfoglia** tooupload il certificato scaricato.
    
    d. Fare clic su **Salva**.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-kintone-test-user"></a>Creazione di un utente test di Kintone

toolog agli utenti di Azure AD tooenable in tooKintone, è necessario eseguirne il provisioning in Kintone.  
Nel caso di hello di Kintone, il provisioning è un'attività manuale.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision un account utente, eseguire hello alla procedura seguente:

1. Accedi tooyour **Kintone** sito aziendale come amministratore.

2. Fare clic su **Impostazioni**.
   
    ![Impostazioni](./media/active-directory-saas-kintone-tutorial/ic785879.png "Impostazioni")

3. Fare clic su **Amministrazione utenti e di sistema**.
   
    ![Amministrazione utenti e di sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Amministrazione utenti e di sistema")

4. In **Amministrazione Utente** fare clic su **Reparti e Utenti**.
   
    ![Reparto e utenti](./media/active-directory-saas-kintone-tutorial/ic785888.png "Reparto e utenti")

5. Fare clic su **Nuovo utente**.
   
    ![Nuovi utenti](./media/active-directory-saas-kintone-tutorial/ic785889.png "Nuovi utenti")

6. In hello **nuovo utente** seguire hello alla procedura seguente:
   
    ![Nuovi utenti](./media/active-directory-saas-kintone-tutorial/ic785890.png "Nuovi utenti")
   
    a. Digitare un **nome visualizzato**, **nome account di accesso**, **nuova Password**, **Conferma Password**, **indirizzo di posta elettronica**, e altri dettagli di un account aAd di cui che si desidera tooprovision in hello correlati nelle caselle di testo.
 
    b. Fare clic su **Salva**.

> [!NOTE]
> È possibile usare qualsiasi altro Kintone utente account strumento di creazione o le API fornite da Kintone tooprovision account utente di AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooKintone.

![Assegna utente][200] 

**tooassign Britta Simon tooKintone, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Kintone**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.

Quando si fa clic su riquadro Kintone hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Kintone applicazione.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

