---
title: 'Esercitazione: Integrazione di Azure Active Directory con Fidelity NetBenefits | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Fidelity NetBenefits.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 77dc8a98-c0e7-4129-ab88-28e7643e432a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2018
ms.author: jeedes
ms.openlocfilehash: 007d3c894731560423e2dde0572793a4282a4654
ms.sourcegitcommit: e19f6a1709b0fe0f898386118fbef858d430e19d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/13/2018
---
# <a name="tutorial-azure-active-directory-integration-with-fidelity-netbenefits"></a>Esercitazione: integrazione di Azure Active Directory con Fidelity NetBenefits

Questa esercitazione descrive come integrare Fidelity NetBenefits con Azure Active Directory (Azure AD).

L'integrazione di Fidelity NetBenefits con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Fidelity NetBenefits.
- È possibile abilitare gli utenti per l'accesso automatico a Fidelity NetBenefits (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Fidelity NetBenefits, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Fidelity NetBenefits abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Fidelity NetBenefits dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-fidelity-netbenefits-from-the-gallery"></a>Aggiunta di Fidelity NetBenefits dalla raccolta
Per configurare l'integrazione di Fidelity NetBenefits in Azure AD, è necessario aggiungere Fidelity NetBenefits dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Fidelity NetBenefits dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Pulsante Azure Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]
    
3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

4. Nella casella di ricerca digitare **Fidelity NetBenefits**, selezionare **Fidelity NetBenefits** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Fidelity NetBenefits nell'elenco dei risultati](./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Fidelity NetBenefits usando un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Fidelity NetBenefits che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Fidelity NetBenefits.

In Fidelity NetBenefits, il mapping dell'**utente** deve essere eseguito con **Utente di Azure AD** per stabilire la relazione di collegamento.

Per configurare e testare l'accesso Single Sign-On di Azure AD con Fidelity NetBenefits, è necessario completare i passaggi seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
2. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creare un utente di test di Fidelity NetBenefits](#create-a-fidelity-netbenefits-test-user)**: per avere una controparte di Britta Simon in Fidelity NetBenefits collegata alla rappresentazione dell'utente in Azure AD.
4. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Fidelity NetBenefits.

**Per configurare Single Sign-On di Azure AD con Fidelity NetBenefits, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Fidelity NetBenefits** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_samlbase.png)

3. Nella sezione **URL e dominio Fidelity NetBenefits** seguire questa procedura:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Fidelity NetBenefits](./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_url.png)

    a. Nella casella di testo **Identificatore** digitare un URL:

    Per ambiente di test: `urn:sp:fidelity:geninbndnbparts20:uat:xq1`

    Per ambiente di produzione: `urn:sp:fidelity:geninbndnbparts20`

    b. Nella casella di testo **URL di risposta** digitare un URL:

    Per ambiente di test: `https://loginxq1.fidelity.com/ftgw/Fas/NBExternal/NBPartSSO/InboundSSO/consumer/sp/ACS.saml2`

    Per ambiente di produzione: `https://login.fidelity.com/ftgw/Fas/NBExternal/NBPartSSO/InboundSSO/consumer/sp/ACS.saml2`
 
4. L'applicazione Fidelity NetBenefits prevede un formato specifico per le asserzioni SAML. È stato eseguito il mapping dell'**identificatore utente** con **user.userprincipalname**. È possibile eseguire il mapping con **employeeid** o altre attestazioni applicabili per l'organizzazione come **Identificatore utente**. La schermata seguente mostra un esempio relativo a questa operazione.

    ![Attributo Fidelity NetBenefits](./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_attribute.png)

    >[!Note]
    >Fidelity NetBenefits supporta la federazione statica e dinamica. In quella statica non viene usato il provisioning degli utenti Just-In-Time basato su SAML, mentre quella dinamica supporta il provisioning degli utenti Just-In-Time. Per l'uso di del provisioning basato su JIT, i clienti devono aggiungere altre attestazioni in Azure AD come la data di nascita dell'utente e così via. Tali dettagli vengono forniti dal [team di supporto di Fidelity NetBenefits](mailto:SSOMaintenance@fmr.com) e devono abilitare questa federazione dinamica per l'istanza.
    
4. Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.

    ![Collegamento di download del certificato](./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_400.png)

6. Nella sezione **Configurazione di Fidelity NetBenefits** fare clic su **Configura Fidelity NetBenefits** per aprire la finestra **Configura accesso**. Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**

    ![Configurazione di Fidelity NetBenefits](./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_configure.png) 

7. Per configurare l'accesso Single Sign-On sul lato **Fidelity NetBenefits** è necessario inviare il file **XML metadati** scaricato e i valori **ID entità SAML** e **URL del servizio Single Sign-On SAML** al [team di supporto di Fidelity NetBenefits](mailto:SSOMaintenance@fmr.com). La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/active-directory-saas-fidelitynetbenefits-tutorial/create_aaduser_01.png)

2. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-fidelitynetbenefits-tutorial/create_aaduser_02.png)

3. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/active-directory-saas-fidelitynetbenefits-tutorial/create_aaduser_03.png)

4. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/active-directory-saas-fidelitynetbenefits-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Crea**.
  
### <a name="create-a-fidelity-netbenefits-test-user"></a>Creare un utente di test di Fidelity NetBenefits

In questa sezione viene creato un utente di nome Britta Simon in Fidelity NetBenefits. Se si sta creando una federazione statica, collaborare con il [team di supporto di Fidelity NetBenefits](mailto:SSOMaintenance@fmr.com) per creare gli utenti nella piattaforma Fidelity NetBenefits. Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On. 

Per la federazione dinamica, gli utenti vengono creati utilizzando il provisioning degli utenti Just-In-Time. Per l'uso di del provisioning basato su JIT, i clienti devono aggiungere altre attestazioni in Azure AD come la data di nascita dell'utente e così via. Tali dettagli vengono forniti dal [team di supporto di Fidelity NetBenefits](mailto:SSOMaintenance@fmr.com) e devono abilitare questa federazione dinamica per l'istanza.

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Fidelity NetBenefits.

![Assegnare il ruolo utente][200] 

**Per assegnare Britta Simon a Fidelity NetBenefits, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco delle applicazioni, selezionare **Fidelity NetBenefits**.

    ![Collegamento di Fidelity NetBenefits nell'elenco delle applicazioni](./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_app.png)  

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Fidelity NetBenefits nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Fidelity NetBenefits.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fidelitynetbenefits-tutorial/tutorial_general_203.png

