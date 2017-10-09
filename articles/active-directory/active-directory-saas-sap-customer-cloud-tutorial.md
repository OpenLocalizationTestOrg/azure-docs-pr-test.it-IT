---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Cloud for Customer | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e il Cloud di SAP per cliente.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>Esercitazione: Integrazione di Azure Active Directory con SAP Cloud for Customer

In questa esercitazione, è illustrato come toointegrate SAP Cloud per il cliente con Azure Active Directory (Azure AD).

L'integrazione Cloud SAP per cliente con Azure AD fornisce hello seguenti vantaggi:

- È possibile controllare in Azure AD che ha accesso tooSAP Cloud per cliente
- È possibile abilitare l'utenti tooautomatically get connesso tooSAP Cloud per cliente (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure

Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

tooconfigure integrazione di Azure AD con SAP Cloud per cliente, è necessario hello seguenti elementi:

- Sottoscrizione di Azure AD.
- Sottoscrizione di SAP Cloud for Customer abilitata per l'accesso Single Sign-On

> [!NOTE]
> hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.

passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. scenario di Hello descritto in questa esercitazione è composto da due componenti principali:

1. Aggiunta di Cloud di SAP per cliente dalla raccolta hello
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>Aggiunta di Cloud di SAP per cliente dalla raccolta hello
integrazione hello tooconfigure di SAP Cloud per il cliente in Azure AD, è necessario tooadd Cloud SAP per cliente dall'elenco di tooyour hello raccolta di App SaaS gestite.

**tooadd Cloud SAP per cliente dalla raccolta di hello, eseguire hello alla procedura seguente:**

1. In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona. 

    ![Active Directory][1]

2. Passare troppo**applicazioni aziendali**. Quindi andare troppo**tutte le applicazioni**.

    ![Applicazioni][2]
    
3. tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.

    ![Applicazioni][3]

4. Nella casella di ricerca hello, digitare **Cloud SAP per cliente**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. Nel riquadro dei risultati hello, selezionare **Cloud SAP per cliente**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Cloud for Customer con un utente test di nome "Britta Simon".

Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nel Cloud di SAP per il cliente è tooa utente in Azure AD. In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nel Cloud di SAP per il cliente deve toobe stabilita.

Nel Cloud di SAP per cliente, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.

tooconfigure e test con SAP Cloud AD Azure single sign-on per cliente, è necessario hello toocomplete seguenti blocchi predefiniti:

1. **[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.
2. **[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.
3. **[Creazione di un Cloud di SAP per l'utente test cliente](#creating-a-sap-cloud-for-customer-test-user)**  -toohave un equivalente di Britta Simon nel Cloud di SAP per il cliente che è la rappresentazione toohello collegato Azure AD dell'utente.
4. **[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.
5. **[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nel Cloud per l'applicazione clienti SAP.

**tooconfigure AD Azure single sign-on con il Cloud di SAP per cliente, eseguire hello alla procedura seguente:**

1. Nel portale di Azure su hello hello **Cloud SAP per cliente** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.

    ![Configura accesso Single Sign-On][4]

2. In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. In hello **Cloud SAP per il dominio del cliente e gli URL** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    a. In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server name>.crm.ondemand.com`

    b. In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore. Contatto [Cloud SAP per il team di supporto clienti Client](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget questi valori. 

4. In hello **gli attributi utente** seguire hello alla procedura seguente:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    a. In **identificatore utente** elenco, seleziona hello **ExtractMailPrefix()** (funzione).

    b. Da hello **posta** elenco, l'attributo utente di selezionare hello da toouse per l'implementazione.
    Ad esempio, se si desidera toouse hello EmployeeID come identificatore utente univoco e archiviato il valore di attributo hello in hello ExtensionAttribute2, quindi selezionare user.extensionattribute2.  

5. In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. In hello **Cloud SAP per la configurazione personalizzata** fare clic su **configurare SAP Cloud per cliente** tooopen **Configura sign-on** finestra. Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget SSO configurato, eseguire hello alla procedura seguente:
   
    a. Accedere al portale di SAP Cloud for Customer con diritti di amministratore.
   
    b. Passare toohello **attività comuni di gestione utente e di applicazione** e fare clic su hello **Provider di identità** scheda.
   
    c. Fare clic su **nuovo Provider di identità** e hello selezionare file XML di metadati scaricato dal portale di Azure hello. Tramite l'importazione di metadati hello, sistema hello carica automaticamente il certificato di firma richiesta hello e certificato di crittografia.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Azure Active Directory richiede hello elemento URL del servizio Consumer di asserzione richiesta SAML hello, pertanto selezionare hello **URL del servizio Consumer di asserzione includono** casella di controllo.
   
    e. Fare clic su **Activate Single Sign-On**(Attiva Single Sign-On).
   
    f. Salvare le modifiche.
   
    g. Fare clic su hello **risorse del sistema** scheda.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. Nella casella di testo **URL di accesso di Azure AD** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    i. Specificare se il dipendente hello manualmente è possibile scegliere tra l'accesso con l'ID utente e password o SSO selezionando hello **selezione Provider di identità manuale**.
   
    j. In hello **URL SSO** sezione specificare URL hello che deve essere utilizzata da toosign i dipendenti nel sistema toohello. 
    In hello **tooEmployee URL inviato** elenco, è possibile scegliere tra hello le opzioni seguenti:
   
    **Non-SSO URL**
   
    sistema di Hello Invia solo hello normale sistema URL toohello dipendente. dipendente Hello non è possibile accedere utilizzando SSO e deve utilizzare password o invece del certificato.
   
    **SSO URL** 
   
    sistema di Hello Invia solo dipendente di toohello URL SSO hello. utilizzo di SSO dipendente Hello può accedere. Richiesta di autenticazione viene reindirizzato tramite hello IdP.
   
    **Automatic Selection**
   
    Se SSO non è attivo, il sistema di hello invia dipendente toohello URL normale sistema di hello. Se SSO è attiva, sistema di hello controlla se il dipendente hello dispone di una password. Se è disponibile una password, sia URL SSO e SSO di Non vengono inviati toohello dipendente. Tuttavia, se dipendente hello non dispone di password, solo hello URL SSO viene inviato toohello dipendente.
   
    k. Salvare le modifiche.

> [!TIP]
> È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!  Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello. È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.

![Creare un utente di Azure AD][100]

**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**

1. In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    a. In hello **nome** casella tipo **BrittaSimon**.

    b. In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Show Password** e annotare il valore di hello di hello **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>Creazione di un utente di test di SAP Cloud for Customer

In questa sezione viene creato un utente di nome Britta Simon in SAP Cloud for Customer. Rivolgersi [Cloud SAP per il team di supporto clienti](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) utenti hello tooadd hello Cloud SAP per la piattaforma di cliente. 

> [!NOTE]
> Assicurarsi che il valore NameID deve corrispondere con il campo username hello in hello Cloud SAP per la piattaforma di cliente.

### <a name="assigning-hello-azure-ad-test-user"></a>Assegnazione utente test hello Azure AD

In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAP Cloud per cliente.

![Assegna utente][200] 

**tooassign Britta Simon tooSAP Cloud per cliente, eseguire hello alla procedura seguente:**

1. Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni hello, selezionare **Cloud SAP per cliente**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.

Quando si fa clic hello SAP Cloud riquadro cliente in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato nel Cloud di SAP per l'applicazione del cliente.
Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

