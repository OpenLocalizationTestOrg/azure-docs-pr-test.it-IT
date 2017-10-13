---
title: 'Esercitazione: Integrazione di Azure Active Directory con Lifesize Cloud | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Lifesize Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7542360f9c75786bf400553090ba0a891d9c2fcc
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a>Esercitazione: Integrazione di Azure Active Directory con Lifesize Cloud

Questa esercitazione descrive come integrare Lifesize Cloud con Azure Active Directory (Azure AD).

L'integrazione di Lifesize Cloud con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Lifesize Cloud
- È possibile abilitare gli utenti per l'accesso automatico a Lifesize Cloud (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Lifesize Cloud, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Lifesize Cloud abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:

1. Aggiunta di Lifesize Cloud dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-lifesize-cloud-from-the-gallery"></a>Aggiunta di Lifesize Cloud dalla raccolta
Per configurare l'integrazione di Lifesize Cloud in Azure AD, è necessario aggiungere Lifesize Cloud dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Lifesize Cloud dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Applicazioni][3]

4. Nella casella di ricerca digitare **Lifesize Cloud**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. Nel pannello dei risultati selezionare **Lifesize Cloud** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Lifesize Cloud con un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Lifesize Cloud che corrisponde a un utente di Azure AD. In altre parole deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Lifesize Cloud.

Per stabilire la relazione di collegamento, in Lifesize Cloud assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Lifesize Cloud, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.
2. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creazione di un utente di test di Lifesize Cloud](#creating-a-lifesize-cloud-test-user)**: per avere una controparte di Britta Simon in Lifesize Cloud collegata alla rappresentazione dell'utente in Azure AD.
4. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Lifesize Cloud.

**Per configurare l'accesso Single Sign-On di Azure AD con Lifesize Cloud, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Lifesize Cloud** del portale di Azure fare clic su **Single Sign-On**.

    ![Configura accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. Nella sezione **URL e dominio Lifesize Cloud** seguire questa procedura:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://login.lifesizecloud.com/ls/?acs`.

    b. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://login.lifesizecloud.com/<companyname>`

     
4. Selezionare **Mostra URL impostazioni avanzate** ed effettuare le seguenti operazioni:    
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    Nella casella di testo **Stato dell'inoltro** digitare un URL usando il criterio seguente: `https://webapp.lifesizecloud.com/?ent=<identifier>`
   
   > [!NOTE] 
   >Si noti che questi non sono i valori reali. è necessario aggiornare questi valori con l'URL di accesso, lo stato dell'inoltro e l'identificatore effettivi. Contattare il [team di supporto clienti di Lifesize Cloud](https://www.lifesize.com/support) per ottenere l'URL di accesso e l'identificatore e ricavare il valore dello stato dell'inoltro dalla configurazione SSO illustrata più avanti nell'esercitazione.

4. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. Nella sezione **Configurazione di Lifesize Cloud** fare clic su **Configura Lifesize Cloud** per aprire la finestra **Configura accesso**. Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. Al fine di configurare l'accesso Single Sign-On per l'applicazione, effettuare l'accesso all'applicazione Lifesize Cloud con privilegi di amministratore.

8. Nell'angolo superiore destro fare clic sul proprio nome e quindi su **Impostazioni avanzate**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. Nelle impostazioni avanzate fare clic sul collegamento **SSO Configuration** (Configurazione SSO). Verrà aperta la pagina della configurazione SSO per l'istanza.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. Ora configurare i valori seguenti nell'interfaccia utente di configurazione SSO.    
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    a. Nella casella di testo **Autorità di certificazione del provider di identità** incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.

    b.  Nella casella di testo **URL di accesso** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.

    c. Aprire nel Blocco note il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **Certificato X.509**.
  
    d. Nei mapping dell'attributo SAML per la casella di testo Nome inserire il valore **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**
    
    e. Nel mapping dell'attributo SAML per la casella di testo **Cognome** inserire il valore **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**
    
    f. Nel mapping dell'attributo SAML per la casella di testo **E-mail** inserire il valore **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**

11. Per verificare la configurazione è possibile fare clic sul pulsante **Prova**.
   
    >[!NOTE]
    >Perché la prova abbia esito positivo, è necessario completare la configurazione guidata di Azure AD e anche fornire l'accesso a utenti o gruppi che possano eseguire il test.

12. Abilitare l'accesso SSO con il pulsante **Enable SSO** (Abilita SSO).

13. Fare clic sul pulsante **Aggiorna** in modo che tutte le impostazioni vengano salvate. Verrà generato il valore RelayState. Copiare il valore RelayState, che viene generato nella casella di testo, incollarlo nella casella di testo **Stato dell'inoltro** della sezione **URL e dominio Lifesize Cloud**. 

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-lifesize-cloud-test-user"></a>Creazione di un utente di test di Lifesize Cloud

In questa sezione viene creato un utente chiamato Britta Simon in Lifesize Cloud. Lifesize Cloud supporta il provisioning utenti automatico. Dopo l'autenticazione in Azure AD sarà eseguito il provisioning automatico dell'utente nell'applicazione. 

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Lifesize Cloud.

![Assegna utente][200] 

**Per assegnare Britta Simon a Lifesize Cloud, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni selezionare **Lifesize Cloud**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Lifesize Cloud nel pannello di accesso, dovrebbe automaticamente apparire la pagina di accesso dell'applicazione Lifesize Cloud.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

