---
title: 'Esercitazione: integrazione di Azure Active Directory con SAML SSO for Confluence di resolution GmbH | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SAML SSO for Confluence di resolution GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 70c01e2ee5d97ed5d09e9281c69f1110b5c220da
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a>Esercitazione: integrazione di Azure Active Directory con SAML SSO for Confluence di resolution GmbH

Questa esercitazione spiega come integrare SAML SSO for Confluence di resolution GmbH con Azure Active Directory, ovvero Azure AD.

L'integrazione di SAML SSO for Confluence di resolution GmbH con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi ha accesso a SAML SSO for Confluence di resolution GmbH
- È possibile abilitare gli utenti per l'accesso automatico a SAML SSO for Confluence di resolution GmbH, ovvero per il Single Sign-On, con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con SAML SSO for Confluence di resolution GmbH, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Una sottoscrizione attiva del Single Sign-On di SAML SSO for Confluence di resolution GmbH

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di SAML SSO for Confluence di resolution GmbH dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a>Aggiunta di SAML SSO for Confluence di resolution GmbH dalla raccolta

Per configurare l'integrazione di SAML SSO for Confluence di resolution GmbH in Azure AD, è necessario aggiungere SAML SSO for Confluence di resolution GmbH dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere SAML SSO for Confluence di resolution GmbH dalla raccolta, eseguire la procedura seguente:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

4. Nella casella di ricerca digitare **SAML SSO for Confluence di resolution GmbH**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. Nel pannello dei risultati selezionare **SAML SSO for Confluence by resolution GmbH** (SAML SSO for Confluence di resolution GmbH) e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAML SSO for Confluence di resolution GmbH con un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere il nome della controparte di SAML SSO for Confluence di resolution GmbH che corrisponde all'utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SAML SSO for Confluence di resolution GmbH.

Per stabilire la relazione di collegamento, in SAML SSO for Confluence di resolution GmbH assegnare il valore del **nome utente** in Azure AD come valore di **Username**.

Per configurare e testare l'accesso Single Sign-On di Azure AD con SAML SSO for Confluence di resolution GmbH, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
2. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creazione di un utente di test di SAML SSO for Confluence di resolution GmbH](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**: per avere una controparte di Britta Simon in SAML SSO for Confluence di resolution GmbH che sia collegata alla rappresentazione di Azure AD dell'utente.
4. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SAML SSO for Confluence di resolution GmbH.

**Per configurare l'accesso Single Sign-On di Azure AD con SAML SSO for Confluence di resolution GmbH, seguire la procedura illustrata di seguito:**

1. Nella pagina di integrazione dell'applicazione **SAML SSO for Confluence di resolution GmbH** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. Nella sezione **SAML SSO for Confluence by resolution GmbH Domain and URLs** (Dominio e URL di SAML SSO for Confluence di resolution GmbH) se si vuole configurare l'applicazione in modalità avviata da **IDP**:

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    a. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<server-base-url>/plugins/servlet/samlsso`

    b. Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<server-base-url>/plugins/servlet/samlsso`

4. Selezionare **Mostra impostazioni URL avanzate** se si desidera configurare l'applicazione in modalità avviata da **SP**:

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Poiché questi non sono i valori reali, è necessario aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi. Contattare il [team di supporto del client di SAML SSO for Confluence di resolution GmbH](https://www.resolution.de/go/support) per ottenere i valori. 

5. Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. In un'altra finestra del Web browser accedere al **portale di amministrazione di SAML SSO for Confluence di resolution GmbH** come amministratore.

8. Passare il puntatore del mouse sulla rotellina e scegliere **Add-ons** (Componenti aggiuntivi).
    
    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. Si verrà reindirizzati alla pagina di Administrator Access (Accesso come amministratore). Immettere la password e fare clic sul pulsante **Confirm** (Conferma).

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. Nella scheda **ATLASSIAN MARKETPLACE** (MARKETPLACE DI ATLASSIAN) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi). 

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. Cercare **SAML Single Sign On (SSO) for Confluence** e fare clic su **Install** (Installa) per installare il nuovo plug-in di SAML.

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. Viene avviata l'installazione del plug-in. Fare clic su **Close**.

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. Fare clic su **Manage**.

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. Fare clic su **Configure** (Configura) per configurare il nuovo plug-in.

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. Questo nuovo plug-in è disponibile anche nella scheda**USERS & SECURITY** (UTENTI E SICUREZZA).

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. Nella pagina **SAML SingleSignOn Plugin Configuration** (Configurazione del plug-in SAML SingleSignOn) fare clic sul pulsante **Add new IdP** (Aggiungi nuovo provider di identità) per configurare le impostazioni del provider di identità.

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. Nella pagina **Choose your SAML Identity Provider** (Scegliere il provider di identità SAML) eseguire la procedura seguente:

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon5a.png)
 
    a. Impostare **AD Azure** come tipo di provider di identità.
    
    b. Aggiungere il **nome** del provider di identità, ad esempio Azure AD.
    
    c. Aggiungere la **descrizione** del provider di identità, ad esempio Azure AD.
    
    d. Fare clic su **Avanti**.
    
18. Nella pagina **Identity provider configuration** (Configurazione provider di identità) fare clic sul pulsante **Next** (Avanti).

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon5b.png)

19. Nella pagina **Import SAML IdP Metadata** (Importa metadati provider di identità SAML) eseguire la procedura seguente:

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon5c.png)

    a. Fare clic sul pulsante **Load File** (Carica file) e selezionare il file XML di metadati scaricato al passaggio 5.

    b. Fare clic sul pulsante **Import** (Importa).
    
    c. Attendere il completamento dell'importazione.
    
    d. Fare clic qui sul pulsante **Next** (Avanti).
    
20. Nella pagina **User ID attribute and transformation** (Attributo e trasformazione ID utente) fare clic sul pulsante **Next** (Avanti).

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon5d.png)
    
21. Nella pagina **User creation and update** (Creazione e aggiornamento utente) fare clic su **Save & Next** (Salva e continua) per salvare le impostazioni.   
    
    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon6a.png)
    
22. Nella pagina **Test your settings** (Test impostazioni) fare clic su **Skip test & configure manually** (Ignora test e configura manualmente) per ignorare il test dell'utente. Il test verrà eseguito nella sezione successiva e richiede alcune impostazioni nel portale di Azure. 
    
    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon6b.png)
    
23. Nella finestra di dialogo visualizzata, contenente il messaggio **Skipping the test means...** (Significato della mancata esecuzione del test), fare clic su **OK**.
    
    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon6c.png)

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a>Creazione di un utente di test di SAML SSO for Confluence di resolution GmbH

Per consentire agli utenti di Azure AD di accedere a SAML SSO for Confluence di resolution GmbH, è necessario eseguire il provisioning in SAML SSO for Confluence di resolution GmbH.  
In SAML SSO for Confluence di resolution GmbH il provisioning è un'attività manuale.

**Per eseguire il provisioning di un account utente, seguire questa procedura:**

1. Accedere al sito aziendale di SAML SSO for Confluence di resolution GmbH come amministratore.

2. Passare il puntatore del mouse e fare clic su **User management** (Gestione utenti).

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. Nella sezione Users (Utenti) fare clic sula scheda **Add users** (Aggiungi utenti). Nella pagina della finestra di dialogo **"Add a User"** (Aggiungi un utente) eseguire la procedura seguente:

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    a. Nella casella di testo **Username** (Nome utente) digitare l'indirizzo di posta elettronica di un utente come Britta Simon.

    b. Nella casella di testo **Full Name** (Nome completo) digitare il nome completo dell'utente, ad esempio Britta Simon.

    c. Nella casella di testo **Email** digitare l'indirizzo di posta elettronica dell'utente, ad esempio Brittasimon@contoso.com.

    d. Nella casella di testo **Password** digitare la password di Britta Simon.

    e. Fare clic sul pulsante **Confirm** (Conferma) e immettere di nuovo la password.
    
    f. Fare clic sul pulsante **Aggiungi**.    

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SAML SSO for Confluence di resolution GmbH.

![Assegna utente][200] 

**Per aggiungere Britta Simon a SAML SSO for Confluence di resolution GmbH, eseguire la procedura seguente:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco delle applicazioni selezionare **SAML SSO for Confluence by resolution GmbH** (SAML SSO for Confluence di resolution GmbH).

    ![Configure Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro di SAML SSO for Confluence di resolution GmbH nel pannello di accesso, si effettua automaticamente l'accesso all'applicazione SAML SSO for Confluence di resolution GmbH.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

