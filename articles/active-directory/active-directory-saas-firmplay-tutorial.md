---
title: 'Esercitazione: Integrazione di Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e FirmPlay - Employee Advocacy for Recruiting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="88428-103">Esercitazione: Integrazione di Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="88428-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="88428-104">Questa esercitazione descrive come integrare FirmPlay - Employee Advocacy for Recruiting con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88428-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88428-105">L'integrazione di FirmPlay - Employee Advocacy for Recruiting con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="88428-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88428-106">È possibile controllare in Azure AD chi può accedere a FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="88428-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="88428-107">È possibile abilitare gli utenti per l'accesso automatico a FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="88428-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88428-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="88428-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="88428-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88428-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88428-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="88428-110">Prerequisites</span></span>

<span data-ttu-id="88428-111">Per configurare l'integrazione di Azure AD con FirmPlay - Employee Advocacy for Recruiting, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="88428-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="88428-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88428-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88428-113">Sottoscrizione di FirmPlay - Employee Advocacy for Recruiting abilitata per l'accesso Single-Sign On</span><span class="sxs-lookup"><span data-stu-id="88428-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="88428-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="88428-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="88428-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="88428-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88428-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="88428-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="88428-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88428-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="88428-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="88428-118">Scenario description</span></span>
<span data-ttu-id="88428-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="88428-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88428-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="88428-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88428-121">Aggiunta di FirmPlay - Employee Advocacy for Recruiting dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="88428-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="88428-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88428-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="88428-123">Aggiunta di FirmPlay - Employee Advocacy for Recruiting dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="88428-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="88428-124">Per configurare l'integrazione di FirmPlay - Employee Advocacy for Recruiting in Azure AD, è necessario aggiungere FirmPlay - Employee Advocacy for Recruiting dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="88428-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88428-125">**Per aggiungere FirmPlay - Employee Advocacy for Recruiting dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="88428-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88428-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="88428-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88428-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="88428-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88428-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="88428-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="88428-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="88428-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="88428-133">Nella casella di ricerca digitare **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="88428-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="88428-135">Nel pannello dei risultati selezionare **FirmPlay - Employee Advocacy for Recruiting** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="88428-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88428-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88428-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88428-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FirmPlay - Employee Advocacy for Recruiting con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="88428-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="88428-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di FirmPlay - Employee Advocacy for Recruiting che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88428-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="88428-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="88428-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="88428-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="88428-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="88428-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con FirmPlay - Employee Advocacy for Recruiting, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="88428-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88428-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="88428-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="88428-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88428-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88428-145">**[Creazione di un utente di test di FirmPlay - Employee Advocacy for Recruiting](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**: per avere una controparte di Britta Simon in FirmPlay - Employee Advocacy for Recruiting collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88428-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="88428-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88428-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88428-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="88428-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88428-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88428-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88428-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="88428-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="88428-150">**Per configurare l'accesso Single Sign-On di Azure AD con FirmPlay - Employee Advocacy for Recruiting, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="88428-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="88428-151">Nella pagina di integrazione dell'applicazione **FirmPlay - Employee Advocacy for Recruiting** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="88428-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="88428-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="88428-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="88428-155">Nella casella di testo **URL di accesso** della sezione **URL e dominio di FirmPlay - Employee Advocacy for Recruiting** digitare un URL usando il modello seguente: `https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="88428-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="88428-157">Si noti che questo non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="88428-157">Please note that this is not the real value.</span></span> <span data-ttu-id="88428-158">È necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="88428-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="88428-159">Per ottenere questo valore, contattare il [team di supporto di FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com).</span><span class="sxs-lookup"><span data-stu-id="88428-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="88428-160">Nella sezione **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="88428-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="88428-162">Nella finestra di dialogo **Crea nuovo certificato** fare clic sull'icona del calendario e selezionare una **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="88428-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="88428-163">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="88428-163">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="88428-165">Nella sezione **Certificato di firma SAML** selezionare **Make new certificate active** (Rendi attivo il nuovo certificato) e fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="88428-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="88428-167">Nella finestra popup **Rollover certificate** (Certificato di rollover) fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="88428-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="88428-169">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="88428-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="88428-171">Nella sezione **Configurazione di FirmPlay - Employee Advocacy for Recruiting** fare clic su **Configura FirmPlay - Employee Advocacy for Recruiting** per aprire la finestra di dialogo **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="88428-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="88428-174">Per configurare l'accesso SSO per l'applicazione, contattare il [team di supporto di FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) e fornire gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="88428-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="88428-175">•  **File del certificato** scaricato</span><span class="sxs-lookup"><span data-stu-id="88428-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="88428-176">•  **URL servizio Single Sign-On SAML**</span><span class="sxs-lookup"><span data-stu-id="88428-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="88428-177">•  **ID entità SAML**</span><span class="sxs-lookup"><span data-stu-id="88428-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="88428-178">•  **URL di disconnessione**</span><span class="sxs-lookup"><span data-stu-id="88428-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88428-179">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88428-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="88428-180">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="88428-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="88428-182">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="88428-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88428-183">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="88428-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88428-185">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="88428-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88428-187">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="88428-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88428-189">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="88428-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88428-191">a.</span><span class="sxs-lookup"><span data-stu-id="88428-191">a.</span></span> <span data-ttu-id="88428-192">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88428-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88428-193">b.</span><span class="sxs-lookup"><span data-stu-id="88428-193">b.</span></span> <span data-ttu-id="88428-194">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88428-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88428-195">c.</span><span class="sxs-lookup"><span data-stu-id="88428-195">c.</span></span> <span data-ttu-id="88428-196">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="88428-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="88428-197">d.</span><span class="sxs-lookup"><span data-stu-id="88428-197">d.</span></span> <span data-ttu-id="88428-198">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="88428-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="88428-199">Creazione di un utente di test di FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="88428-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="88428-200">In questa sezione si crea un utente di nome Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="88428-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="88428-201">Per aggiungere gli utenti nella piattaforma FirmPlay - Employee Advocacy for Recruiting, contattare il [team di supporto di FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com).</span><span class="sxs-lookup"><span data-stu-id="88428-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="88428-202">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="88428-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="88428-203">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="88428-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![Assegna utente][200] 

<span data-ttu-id="88428-205">**Per assegnare Britta Simon a FirmPlay - Employee Advocacy for Recruiting, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="88428-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="88428-206">Nel portale di gestione di Azure aprire la visualizzazione applicazioni, passare alla visualizzazione directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="88428-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="88428-208">Nell'elenco delle applicazioni selezionare **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="88428-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="88428-210">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="88428-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="88428-212">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="88428-212">Click **Add** button.</span></span> <span data-ttu-id="88428-213">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="88428-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="88428-215">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="88428-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="88428-216">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="88428-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88428-217">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="88428-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="88428-218">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="88428-218">Testing single sign-on</span></span>

<span data-ttu-id="88428-219">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="88428-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="88428-220">Quando si fa clic sul riquadro FirmPlay - Employee Advocacy for Recruiting nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="88428-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="88428-221">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="88428-221">Additional resources</span></span>

* [<span data-ttu-id="88428-222">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88428-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88428-223">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88428-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png