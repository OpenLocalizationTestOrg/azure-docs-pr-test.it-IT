---
title: 'Esercitazione: Integrazione di Azure Active Directory con GaggleAMP | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e GaggleAMP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: c591cf99aecc4153e378c42a530b80deeca63158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a>Esercitazione: Integrazione di Azure Active Directory con GaggleAMP

Questa esercitazione descrive come integrare GaggleAMP con Azure Active Directory (Azure AD).

L'integrazione di GaggleAMP con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a GaggleAMP
- È possibile abilitare gli utenti per l'accesso automatico a GaggleAMP (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con GaggleAMP, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD.
- Sottoscrizione di GaggleAMP abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:

1. Aggiunta di GaggleAMP dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-gaggleamp-from-the-gallery"></a>Aggiunta di GaggleAMP dalla raccolta
Per configurare l'integrazione di GaggleAMP in Azure AD, è necessario aggiungere GaggleAMP dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere GaggleAMP dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Applicazioni][2]
    
3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Applicazioni][3]

4. Nella casella di ricerca digitare **GaggleAMP**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. Nel pannello dei risultati selezionare **GaggleAMP** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con GaggleAMP mediante un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di GaggleAMP corrisponde a un determinato utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in GaggleAMP.

Per stabilire la relazione di collegamento, in GaggleAMP assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con GaggleAMP, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.
2. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creazione di un utente di test di GaggleAMP](#creating-a-gaggleamp-test-user)**: per avere una controparte di Britta Simon in GaggleAMP collegata alla rappresentazione dell'utente in Azure AD.
4. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione GaggleAMP.

**Per configurare Single Sign-On di Azure AD con GaggleAMP, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **GaggleAMP** del portale di Azure fare clic su **Single Sign-On**.

    ![Configura accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. Nella sezione **URL e dominio GaggleAMP** seguire questa procedura:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.gaggleamp.com`

    > [!NOTE] 
    > Poiché non è reale, Aggiornarlo con l'URL di accesso effettivo. Per ottenere il valore contattare il [team di supporto clienti di GaggleAMP](mailto:sales@gaggleamp.com). 
 
4. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. Nella sezione **Configurazione di GaggleAMP** fare clic su **Configura GaggleAMP** per aprire la finestra **Configura accesso**. Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. In un'altra istanza del browser passare alla pagina dell'accesso Single Sign-On SAML creata dal team di supporto di Gaggle, ad esempio *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*.

8. Nella pagina **SAML SSO** seguire questa procedura:  
   
    ![Accesso Single Sign-On di GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    a. Nella casella di testo **Autorità di certificazione del provider di identità** incollare il valore di **URL autorità di certificazione** copiato dal portale di Azure. 
 
    b. Nella casella di testo **URL di accesso Single Sign-On del provider di identità** incollare il valore di **URL servizio Single Sign-On** copiato dal portale di Azure. 

    c. Fare clic su **Save**      

    d. Inviare il **Certificato (Base64)** al [team di supporto di GaggleAMP](mailto:sales@gaggleamp.com).

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-a-gaggleamp-test-user"></a>Creazione di un utente di test di GaggleAMP

Questa sezione descrive come creare un utente chiamato Britta Simon in GaggleAMP. GaggleAMP supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Durante un tentativo di accesso a GaggleAMP viene creato un nuovo utente, se questo non esiste già. 

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a GaggleAMP.

![Assegna utente][200] 

**Per assegnare Britta Simon a GaggleAMP, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni selezionare **GaggleAMP**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro GaggleAMP nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione GaggleAMP.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

