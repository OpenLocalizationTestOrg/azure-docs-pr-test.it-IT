---
title: 'Esercitazione: Integrazione di Azure Active Directory con Springer Link | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Springer Link.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: b9aec6f8f293cdd31456a7f50e3efe792804c7c8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a>Esercitazione: Integrazione di Azure Active Directory con Springer Link

Questa esercitazione descrive come integrare Springer Link con Azure Active Directory (Azure AD).

L'integrazione di Springer Link con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Springer Link.
- È possibile abilitare gli utenti per l'accesso automatico a Springer Link (Single Sign-On) con gli account Azure AD.
- È possibile gestire gli account da una posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Springer Link, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Springer Link abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:

1. Aggiungere Springer Link dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-springer-link-from-the-gallery"></a>Aggiungere Springer Link dalla raccolta
Per configurare l'integrazione di Springer Link in Azure AD, è necessario aggiungere Springer Link dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere Springer Link dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Pulsante Azure Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]
    
3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

4. Nella casella di ricerca digitare **Springer Link**, selezionare **Springer Link** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Springer Link nell'elenco dei risultati](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Springer Link con un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di Springer Link corrispondente a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Springer Link.

Per stabilire la relazione di collegamento, in Springer Link assegnare il valore di **nome utente** di Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Springer Link, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
2. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
4. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Springer Link.

**Per configurare l'accesso Single Sign-On di Azure AD con Springer Link, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Springer Link** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. Nella sezione **URL e dominio Springer Link** se si vuole configurare l'applicazione in modalità avviata da **IDP**:

    ![Informazioni su URL e dominio Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    a. Nella casella di testo **Identificatore** digitare l'URL: `https://fsso.springer.com`

    b. Nella casella di testo **URL di risposta** digitare l'URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`    

4. Selezionare **Mostra impostazioni URL avanzate** se si desidera configurare l'applicazione in modalità avviata da **SP**:

    ![Informazioni su URL e dominio Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    Nella casella di testo **URL di accesso** digitare l'URL: `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`    

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. Per generare l'URL dei **metadati**, seguire questa procedura:

    a. Fare clic su **Registrazioni per l'app**.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    b. Fare clic su **Endpoint** per aprire la finestra di dialogo **Endpoint**.  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    c. Fare clic sul pulsante Copia per copiare l'URL del **DOCUMENTO METADATI FEDERAZIONE** e incollarlo nel Blocco note.
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    d. Passare ora alla pagina delle proprietà di **Springer Link** e copiare l'**ID applicazione** usando il pulsante **Copia** e incollarlo nel Blocco note.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    e. Generare l'**URL dei metadati** usando il modello seguente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`

7. Per configurare l'accesso Single Sign-On sul lato **Springer Link**, è necessario inviare l'**URL dei metadati** al [team di supporto di Springer Link](mailto:identity@springernature.com).

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).


### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Crea**.
 
### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Springer Link.

![Assegnare il ruolo utente][200] 

**Per assegnare Britta Simon a Springer Link, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni selezionare **Springer Link**.

    ![Collegamento Springer Link nell'elenco di applicazioni](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Springer Link nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Springer Link.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

