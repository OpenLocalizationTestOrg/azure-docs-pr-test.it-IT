---
title: 'Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Dropbox for Business.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: jeedes
ms.openlocfilehash: 255cfcb777f88fd6c6ac62b3e7c216360ea11e54
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a>Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business

Questa esercitazione descrive come integrare Dropbox for Business con Azure Active Directory (Azure AD).

L'integrazione di Dropbox for Business con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD quali utenti possono accedere a Dropbox for Business.
- È possibile abilitare per gli utenti l'accesso automatico a Dropbox for Business (Single Sign-On) con i rispettivi account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Dropbox for Business, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Dropbox for Business abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Dropbox for Business dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-dropbox-for-business-from-the-gallery"></a>Aggiunta di Dropbox for Business dalla raccolta
Per configurare l'integrazione di Dropbox for Business in Azure AD, è necessario aggiungere Dropbox for Business dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Dropbox for Business dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Pulsante Azure Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]
    
3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

4. Nella casella di ricerca digitare **Dropbox for Business**, selezionare **Dropbox for Business** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Dropbox for Business nell'elenco dei risultati](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD a Dropbox for Business con l'utente di test "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente di Dropbox for Business che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Dropbox for Business.

Per stabilire la relazione di collegamento, in Dropbox for Business assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Dropbox for Business, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
2. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creare un utente di test di Dropbox for Business](#create-a-dropbox-for-business-test-user)**: per avere una controparte di Britta Simon in Dropbox for Business collegata alla relativa rappresentazione dell'utente in Azure AD.
4. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Dropbox for Business.

**Per configurare l'accesso Single Sign-On di Azure AD con Dropbox for Business, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Dropbox for Business** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. Nella sezione **URL e dominio Dropbox for Business** seguire questa procedura:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On in Dropbox for Business](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url1.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://www.dropbox.com/sso/<id>`

    b. Nella casella di testo **Identificatore** digitare un valore: `Dropbox`

    > [!NOTE] 
    > Il valore precedente non è un valore reale. È necessario aggiornarlo con l'URL di accesso effettivo, descritto più avanti nell'esercitazione. Per ottenere il valore, contattare il [team di assistenza per il client di Dropbox for Business](https://www.dropbox.com/business/contact). 
 

4. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Collegamento di download del certificato](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. Nella sezione **Configurazione di Dropbox for Business** fare clic su **Configura Dropbox for Business** per aprire la finestra **Configura accesso**. Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**

    ![Configurazione di Dropbox for Business](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. Per configurare l'accesso Single Sign-On sul lato **Dropbox for Business**, passare al tenant di Dropbox for Business.

    a. Accedere al tenant di Dropbox for Business. 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurare l'accesso Single Sign-On")
   
    b. Nel riquadro di spostamento a sinistra fare clic su **Admin Console**. 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurare l'accesso Single Sign-On")
   
    c. In **Console di amministrazione** fare clic su **Autenticazione** nel riquadro di spostamento a sinistra. 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurare l'accesso Single Sign-On")
   
    d. Nella sezione **Single sign-on** selezionare **Abilita Single Sign-On** e quindi fare clic su **More** (Altro) per espandere la sezione.  
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurare l'accesso Single Sign-On")
   
    e. Copiare l'URL accanto a **Users can sign in by entering their email address or they can go directly to** (Gli utenti possono accedere immettendo l'indirizzo di posta elettronica oppure possono passare direttamente a) e incollarlo nella casella di testo **URL di accesso** della sezione **URL e dominio Dropbox for Business** nel portale di Azure. 
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
8. Nella sezione **Single Sign-On** della pagina **Autenticazione** eseguire la procedura seguente: 
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurare l'accesso Single Sign-On")
   
    a. Fare clic su **Required**.
   
    b. Nella casella di testo **Sign-in URL** (URL di accesso) incollare il valore di **URL servizio Single Sign-On SAML** copiato dal portale di Azure.

    c. Fare clic su **Scegli certificato** e quindi selezionare il **file di certificato con codifica Base 64**.

    d. Fare clic su **Salva modifiche** per completare la configurazione del tenant DropBox for Business.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png)

2. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png)

3. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png)

4. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-a-dropbox-for-business-test-user"></a>Creare un utente di test di Dropbox for Business

In questa sezione viene creato un utente di nome Britta Simon in Dropbox for Business. Dropbox for Business supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Se un utente non esiste in Dropbox for Business, ne viene creato uno nuovo quando si tenta di accedere a Dropbox for Business.

>[!Note]
>Se è necessario creare un utente manualmente, contattare il [team di supporto clienti di Dropbox for Business](https://www.dropbox.com/business/contact) 

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Dropbox for Business.

![Assegnare il ruolo utente][200] 

**Per assegnare Britta Simon a Dropbox for Business, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco delle applicazioni selezionare **Dropbox for Business**.

    ![Collegamento di Dropbox for Business nell'elenco delle applicazioni](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png)  

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro di Dropbox for Business nel pannello di accesso dovrebbe essere visualizzata la pagina di accesso dell'applicazione Dropbox for Business.
 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

