---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Workplace by Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: 4f34f6509d762cba6aba98a6eba010fd94656e67
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook

Questa esercitazione descrive come integrare Workplace by Facebook con Azure Active Directory, ovvero Azure AD.

L'integrazione di Workplace by Facebook con Azure AD offre i vantaggi seguenti:

- In Azure AD è possibile controllare chi può accedere a Workplace by Facebook.
- È possibile abilitare gli utenti per l'accesso automatico a Workplace by Facebook (Single Sign-On) con i loro account Azure AD.
- È possibile gestire gli account da una posizione centrale: il portale di Azure.

Per altri dettagli sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Workplace by Facebook, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Una sottoscrizione a Workplace by Facebook abilitata per l'accesso Single Sign-On (SSO)

A questo scopo, seguire queste indicazioni:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiungere Workplace by Facebook dalla raccolta.
2. Configurare e testare l'accesso Single Sign-On di Azure AD.

## <a name="add-workplace-by-facebook-from-the-gallery"></a>Aggiungere Workplace by Facebook dalla raccolta
Per configurare l'integrazione di Workplace by Facebook in Azure AD, aggiungere Workplace by Facebook dalla raccolta all'elenco di app SaaS gestite.

1. Nel [portale di Azure](https://portal.azure.com) fare clic su **Azure Active Directory** nel riquadro sinistro. 

    ![Pulsante Azure Active Directory][1]

2. Esplorare **Applicazioni aziendali** > **All applications** (Tutte le applicazioni).

    ![Pannello Applicazioni aziendali][2]
    
3. Per aggiungere una nuova applicazione, fare clic su **Nuova applicazione** nella parte superiore della finestra di dialogo.

    ![Pulsante Nuova applicazione][3]

4. Nella casella di ricerca digitare **Workplace by Facebook** e selezionare **Workplace by Facebook** dai risultati. Selezionare quindi **Aggiungi** per aggiungere l'applicazione.

    ![Workplace by Facebook nell'elenco risultati](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso SSO di Azure AD con Workplace by Facebook usando un utente di test di nome "Britta Simon".

Affinché l'accesso SSO funzioni correttamente, Azure AD deve conoscere il rapporto tra l'utente controparte di Workplace by Facebook e un utente di Azure AD. In altre parole, è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Workplace by Facebook.

Stabilire questa relazione assegnando il valore di **nome utente** in Azure AD al valore **Username** in Workplace by Facebook.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso SSO di Azure AD nel portale di Azure e viene configurato l'accesso SSO nell'applicazione Workplace by Facebook.

1. Nella pagina di integrazione dell'applicazione **Workplace by Facebook** del portale di Azure selezionare **Single Sign-On**.

    ![Configurare il collegamento Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso SSO.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Nella sezione **Workplace by Facebook Domain and URLs** (URL e dominio Workplace by Facebook) eseguire i passaggi riportati di seguito:

    a. Nella casella di testo **URL accesso** digitare un URL che usa il modello seguente: `https://<company subdomain>.facebook.com`

    b. Nella casella di testo **Identificatore** digitare l'URL che usa il modello seguente:`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > Questi valori sono solo un esempio. Aggiornare questi valori con URL di accesso e identificatore effettivi. Per ottenere questi valori, contattare il [team di supporto client Workplace by Facebook](https://workplace.fb.com/faq/). 

4. Nella sezione **Certificato di firma SAML** selezionare **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Collegamento di download del certificato](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Selezionare **Salva**.

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. Nella sezione **Workplace by Facebook Configuration** (Configurazione di Workplace by Facebook) selezionare **Configure Workplace by Facebook** (Configurare Workplace by Facebook) per aprire la finestra **Configura accesso**. Copiare l'**URL di disconnessione, l'ID entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.

    ![Configurazione di Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. In un'altra finestra del Web browser accedere al sito aziendale di Workplace by Facebook come amministratore.
  
   > [!NOTE] 
   > Nell'ambito del processo di autenticazione SAML, Workplace può usare stringhe di query di dimensioni massime di 2,5 kilobyte per passare i parametri ad Azure AD.

8. In **Company Dashboard** (Company Dashboard) passare alla scheda **Authentication** (Autenticazione).

9. In **SAML Authentication** (Autenticazione SAML) selezionare **SSO Only** (Solo SSO) dall'elenco a discesa.

10. Immettere i valori copiati dalla sezione **Workplace by Facebook Configuration** (Configurazione di Workplace by Facebook) del portale di Azure nei campi corrispondenti:

    *   Nella casella di testo **SAML URL** (URL SAML) incollare il valore di **URL servizio Single Sign-On** copiato dal portale di Azure.
    *   Nella casella di testo **SAML Issuer URL** (URL emittente SAML) incollare il valore dell'**ID entità SAML** copiato dal portale di Azure.
    *   In **SAML Logout Redirect (Optional)** (Reindirizzamento disconnessione SAML (facoltativo)) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.
    *   Aprire nel Blocco note il **certificato con codifica base 64** scaricato dal portale di Azure. Copiare il contenuto negli Appunti e quindi incollarlo nella casella di testo **Certificato SAML**.

11. Potrebbe essere necessario inserire l'URL dei partecipanti, l'URL del destinatario e l'URL ACS (servizio consumer di asserzione) elencati nella sezione **SAML Configuration** (Configurazione SAML).

12. Scorrere fino alla fine della sezione e selezionare **Test SSO** (Testa SSO). Viene visualizzata una finestra popup con la pagina di accesso di Azure AD. Per autenticarsi, immettere le credenziali come di consueto. Assicurarsi che l'indirizzo di posta elettronica restituito da Azure AD corrisponda a quello dell'account Workplace con cui si è connessi.

13. Se il test è stato completato, scorrere fino alla fine della pagina e selezionare **Salva**.

14. Chiunque usi Workplace visualizza ora la pagina di accesso ad Azure AD per l'autenticazione.

È possibile scegliere di configurare un URL di disconnessione SAML, che può essere usato per puntare alla pagina di disconnessione di Azure AD. Quando questa impostazione è abilitata e configurata, l'utente non viene più indirizzato alla pagina di disconnessione di Workplace. Invece che a questa pagina, l'utente viene reindirizzato all'URL aggiunto nell'impostazione di reindirizzamento di disconnessione SAML.


> [!TIP]
> Un riepilogo delle istruzioni è disponibile nel [portale di Azure](https://portal.azure.com) durante la configurazione dell'app. Dopo aver aggiunto l'app dalla sezione **Active Directory** > **Applicazioni aziendali** è sufficiente selezionare la scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).

### <a name="configure-reauthentication-frequency"></a>Configurare la frequenza di riautenticazione

È possibile configurare Workplace in modo che chieda una verifica SAML ogni giorno, ogni tre giorni, ogni settimana, ogni due settimane, ogni mese o mai.

> [!NOTE] 
>Il valore minimo per la verifica SAML nelle applicazioni per dispositivi mobili è impostato su una settimana.

È inoltre possibile forzare una reimpostazione SAML per tutti gli utenti. A tale scopo, usare il pulsante **Require SAML authentication for all users now** (Richiedi ora autenticazione SAML per tutti gli utenti).


### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

1. Nel **portale di Azure** fare clic su **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. Per visualizzare l'elenco di utenti, passare a **Users and groups** (Utenti e gruppi) e selezionare **Tutti gli utenti**.
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. Per aprire la finestra di dialogo **Utente**, fare clic su **Aggiungi**.
 
    ![Pulsante Aggiungi](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. Nella finestra di dialogo **Utente** seguire questa procedura:
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password**e annotare la password.

    d. Selezionare **Create**.
 
### <a name="create-a-workplace-by-facebook-test-user"></a>Creare un utente test di Workplace by Facebook

In questa sezione si crea un utente di nome Britta Simon in Workplace by Facebook. Workplace by Facebook supporta il provisioning JIT, abilitato per impostazione predefinita.

Non è necessaria alcuna azione dell'utente in questa sezione. Se un utente non esiste in Workplace by Facebook, si crea una nuova istanza quando si tenta di accedere a Workplace by Facebook.

>[!Note]
>Se è necessario creare un utente manualmente, contattare il [team di supporto al client di Workplace by Facebook](https://workplace.fb.com/faq/).

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata all'uso dell'accesso SSO di Azure concedendo l'accesso a Workplace by Facebook.

![Assegnare utenti][200] 

1. Nel portale di Azure aprire la visualizzazione applicazioni. Passare alla visualizzazione directory, accedere ad **Applicazioni aziendali** e quindi selezionare **All applications** (Tutte le applicazioni).

    ![Assegnare utenti][201] 

2. Nell'elenco di applicazioni selezionare **Workplace by Facebook**.

    ![Collegamento di Workplace by Facebook nell'elenco delle applicazioni](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202] 

4. Selezionare **Aggiungi**. Quindi nel riquadro **Aggiungi assegnazione** selezionare **Users and groups** (Utenti e gruppi).

    ![Riquadro Aggiungi assegnazione][203]

5. Nella finestra di dialogo **Users and groups** (Utenti e gruppi) selezionare **Britta Simon** nell'elenco di utenti.

6. Nella finestra di dialogo **Utenti e gruppi** fare clic su **Seleziona**.

7. Nella finestra di dialogo **Aggiungi assegnazione** selezionare **Assegna**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

Per testare le impostazioni di SSO, aprire il pannello di accesso.
Per altre informazioni, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).


## <a name="next-steps"></a>Passaggi successivi

* Vedere l'[elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md).
* Leggere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).
* Altre informazioni su come [configurare il provisioning utente](active-directory-saas-facebook-at-work-provisioning-tutorial.md).



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

