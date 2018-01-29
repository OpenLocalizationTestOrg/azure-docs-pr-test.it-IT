---
title: 'Esercitazione: Integrazione di Azure Active Directory con Pluralsight | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Pluralsight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d148d78d9f98b6a3ddf1259177936b3976aeab
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a>Esercitazione: Integrazione di Azure Active Directory con Pluralsight

Questa esercitazione descrive come integrare Pluralsight con Azure Active Directory (Azure AD).

L'integrazione di Pluralsight con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD che ha accesso al Pluralsight.
- È possibile abilitare gli utenti per automaticamente ottenere firmato Pluralsight (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Pluralsight, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Pluralsight abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Pluralsight dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-pluralsight-from-the-gallery"></a>Aggiunta di Pluralsight dalla raccolta
Per configurare l'integrazione di Pluralsight in Azure AD, è necessario aggiungere Pluralsight dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Pluralsight dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Pulsante Azure Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]
    
3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

4. Nella casella di ricerca, digitare **Pluralsight**selezionare **Pluralsight** dal pannello risultati quindi fare clic su **Aggiungi** pulsante per aggiungere l'applicazione.

    ![Pluralsight nell'elenco dei risultati](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Pluralsight con un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Pluralsight che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Pluralsight.

Per stabilire la relazione di collegamento, in Pluralsight assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Pluralsight, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
2. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creare un utente test Pluralsight](#create-a-pluralsight-test-user)**  - disporre un equivalente di Britta Simon di Pluralsight collegato per la rappresentazione di Azure AD dell'utente.
4. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Pluralsight.

**Per configurare l'accesso Single Sign-On di Azure AD con Pluralsight, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Pluralsight** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. Nel **Pluralsight dominio e gli URL** sezione, eseguire la procedura seguente:

    ![Pluralsight informazioni domini e gli URL single sign-on](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<instancename>.pluralsight.com/sso/<companyname>`

    b. Nella casella di testo **Identificatore** digitare l'URL: `www.pluralsight.com`

    c. Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<instancename>.pluralsight.com/sp/ACS.saml2`
     
    > [!NOTE] 
    > Poiché questi non sono i valori reali, è necessario aggiornarli con l'URL di risposta e l'URL di accesso effettivi. Contatto [team di supporto Pluralsight Client](mailto:support@pluralsight.com) per ottenere questi valori. 

4. Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.

    ![Collegamento di download del certificato](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. Questa sezione descrive come abilitare l'accesso Single Sign-On di Azure AD nel portale di Azure e configurare l'accesso SSO nell'applicazione Pluralsight.

    L'applicazione Pluralsight prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML. La schermata seguente illustra un esempio relativo a questa operazione.

    ![Configure Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    >È anche possibile aggiungere l'attributo **ID univoco** con il valore appropriato come EmployeeID o un altro elemento adatto per l'organizzazione. Si noti anche che questo attributo non è obbligatorio, ma può essere aggiunto per identificare l'utente univoco. 

6. Per aggiungere gli **attributi token SAML**necessari, per ogni riga della tabella sotto, seguire questa procedura:
   
   | Nome attributo | Valore attributo |
   | ---| --- |
   | Nome |user.givenname |
   | Cognome |user.surname |
   | Email |user.mail |
   
   a. Fare clic su **add user attribute** to open the **Aggiungi attributo utente** .
    
     ![Configure Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   b. Nella casella di testo **Nome attributo** , digitare il nome dell'attributo indicato per quella riga.
  
   c. Nell’elenco **Valore attributo** selezionare il valore dell'attributo indicato per quella riga.
  
   d. Fare clic su **OK**.    

7. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. Per ottenere l'accesso Single Sign-On configurato per l'applicazione, contattare il team dei [servizi professionali](mailTo:professionalservices@pluralsight.com) di Pluralsight e comunicare il file di metadati scaricato.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png)

2. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png)

3. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png)

4. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-a-pluralsight-test-user"></a>Creare un utente test Pluralsight

Questa sezione descrive come creare un utente chiamato Britta Simon in Pluralsight. Collaborare con il [team di supporto clienti di Pluralsight](mailto:support@pluralsight.com) per aggiungere utenti all'account Pluralsight.

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Pluralsight.

![Assegnare il ruolo utente][200] 

**Per assegnare Britta Simon a Pluralsight, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco delle applicazioni selezionare **Pluralsight**.

    ![Il collegamento Pluralsight nell'elenco delle applicazioni](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png)  

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Pluralsight nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Pluralsight.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

