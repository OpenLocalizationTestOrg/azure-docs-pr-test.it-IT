---
title: 'Esercitazione: Integrazione di Azure Active Directory con NetSuite | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>Esercitazione: Integrazione di Azure Active Directory con NetSuite

In questa esercitazione, è illustrato come toointegrate Netsuite con Azure Active Directory (Azure AD).

Integrazione Netsuite con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooNetsuite
- È possibile abilitare l'utenti tooautomatically get connesso tooNetsuite (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

integrazione di Azure AD con Netsuite tooconfigure, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Netsuite abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Netsuite dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-netsuite-from-hello-gallery"></a>Aggiunta di Netsuite dalla raccolta hello
integrazione hello tooconfigure di Netsuite in Azure AD, è necessario tooadd Netsuite dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Netsuite dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Netsuite**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. Nel riquadro dei risultati hello, selezionare **Netsuite**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Netsuite in base a un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Netsuite è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Netsuite richiede toobe stabilita.

Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Netsuite.

tooconfigure e prova AD Azure single sign-on con Netsuite, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un utente test Netsuite](#creating-a-netsuite-test-user)**  -toohave un equivalente di Britta Simon in Netsuite che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Netsuite.

**Azure AD tooconfigure single sign-on con Netsuite, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Netsuite** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. In hello **Netsuite dominio e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    In hello **URL di risposta** casella di testo, digitare un URL con modello di hello: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > Poiché il valore non è reale, Il valore di hello aggiornamento con hello URL di risposta effettivo. Contatto [team di supporto Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget questo valore.
 
4. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. In hello **Netsuite configurazione** fare clic su **configurare Netsuite** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. Aprire una nuova scheda nel browser e accedere al sito della società Netsuite come amministratore.

8. Nella barra degli strumenti di hello nella parte superiore di hello di hello pagina, fare clic su **installazione**, quindi fare clic su **Setup Manager**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. Da hello **le attività di configurazione** elenco, selezionare **integrazione**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. In hello **Manage Authentication** fare clic su **SAML Single Sign-on**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. In hello **SAML Setup** eseguire hello alla procedura seguente:
   
    a. Hello copia **SAML Single Sign-On Service URL** valore **riferimento rapido** sezione **Configura sign-on** e incollarlo in hello **Provider di identità Pagina di accesso** campo Netsuite.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b. In NetSuite selezionare **Primary Authentication Method** (Metodo di autenticazione primario).

    c. Per il campo hello etichettata **SAMLV2 Identity Provider Metadata**selezionare **caricare File di metadati IDP**. Quindi fare clic su **Sfoglia** file di metadati hello tooupload scaricato dal portale di Azure.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    d. Fare clic su **Submit**.

12. In Azure AD fare clic sulla casella di controllo **Visualizza e modifica tutti gli altri attributi utente** e aggiungere l'attributo.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Per hello **nome dell'attributo** digitare `account`. Per hello **valore dell'attributo** , digitare l'ID di account Netsuite. Questo valore è costante e modifica con l'account. Istruzioni su come toofind l'ID account sono incluse di seguito:

      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    a. In Netsuite, fare clic su **installazione** dal menu di navigazione superiore hello.

    b. Fare clic in hello **le attività di configurazione** sezione del menu di navigazione sinistro hello, seleziona hello **integrazione** sezione e fare clic su **preferenze di servizi Web**.

    c. Copiare l'ID Account Netsuite e incollarlo in hello **valore dell'attributo** campo in Azure AD.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. Prima che gli utenti possono eseguire single sign-on in Netsuite, si devono prima essere assegnate autorizzazioni appropriate di hello in Netsuite. Seguire le istruzioni di hello sotto tooassign queste autorizzazioni.

    a. Scegliere dal menu di spostamento superiore di hello **installazione**, quindi fare clic su **Setup Manager**.
      
      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. Scegliere dal menu di navigazione a sinistra di hello **Users/Roles**, quindi fare clic su **gestione ruoli**.
      
      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. Fare clic su **New Role**.

    d. Digitare un **nome** per il nuovo ruolo e seleziona hello **Single Sign-On solo** casella di controllo.
      
      ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    e. Fare clic su **Salva**.

    f. Scegliere dal menu hello in primo piano hello **autorizzazioni**. Fare quindi clic su **Setup**.
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. Selezionare **Set Up SAM Single Sign-on** (Configura Single Sign-on SAM), quindi fare clic su **Aggiungi**.

    h. Fare clic su **Salva**.

    i. Scegliere dal menu di spostamento superiore di hello **installazione**, quindi fare clic su **Setup Manager**.
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. Scegliere dal menu di navigazione a sinistra di hello **Users/Roles**, quindi fare clic su **Gestisci utenti**.
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. Selezionare un utente di test. Fare quindi clic su **Edit**.
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. Nella finestra di dialogo ruoli hello, selezionare il ruolo hello che è stato creato e fare clic su **Aggiungi**.
      
       ![Configura accesso Single Sign-On](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. Fare clic su **Salva**.
    
> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**. 

### <a name="creating-a-netsuite-test-user"></a>Creazione di un utente test di Netsuite

In questa sezione si crea un utente di nome Britta Simon in Netsuite. Netsuite supporta il provisioning JIT, abilitato per impostazione predefinita.
Non è necessario alcun intervento dell'utente in questa sezione. Se un utente non esiste già in Netsuite, quando si tenta di tooaccess Netsuite uno nuovo.


### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooNetsuite.

![Assegna utente][200] 

**tooassign Britta Simon tooNetsuite, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Netsuite**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

tootest le impostazioni single sign-on, aprire il pannello di accesso a hello [https://myapps.microsoft.com](https://myapps.microsoft.com/), accedere all'account di prova hello e fare clic su **Netsuite**.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Configura provisioning utenti](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

