---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="c4713-103">Esercitazione: Integrazione di Azure Active Directory con Salesforce</span><span class="sxs-lookup"><span data-stu-id="c4713-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="c4713-104">Questa esercitazione descrive come integrare Salesforce con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4713-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4713-105">L'integrazione di Salesforce con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4713-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c4713-106">È possibile controllare in Azure AD chi può accedere a Salesforce</span><span class="sxs-lookup"><span data-stu-id="c4713-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="c4713-107">È possibile abilitare gli utenti per l'accesso automatico a Salesforce (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4713-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4713-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4713-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c4713-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4713-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4713-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c4713-110">Prerequisites</span></span>

<span data-ttu-id="c4713-111">Per configurare l'integrazione di Azure AD con Salesforce, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4713-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="c4713-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4713-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4713-113">Sottoscrizione di Salesforce abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c4713-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4713-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c4713-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4713-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4713-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4713-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c4713-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4713-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4713-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4713-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c4713-118">Scenario description</span></span>
<span data-ttu-id="c4713-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c4713-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4713-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4713-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4713-121">Aggiunta di Salesforce dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c4713-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="c4713-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4713-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="c4713-123">Aggiunta di Salesforce dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c4713-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="c4713-124">Per configurare l'integrazione di Salesforce in Azure AD, è necessario aggiungere Salesforce dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c4713-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c4713-125">**Per aggiungere Salesforce dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c4713-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c4713-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c4713-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4713-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c4713-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c4713-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c4713-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c4713-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c4713-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c4713-133">Nella casella di ricerca digitare **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="c4713-133">In the search box, type **Salesforce**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="c4713-135">Nel pannello dei risultati selezionare **Salesforce** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c4713-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4713-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4713-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4713-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Salesforce in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c4713-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c4713-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Salesforce che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4713-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="c4713-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="c4713-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="c4713-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Salesforce, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4713-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c4713-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c4713-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c4713-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4713-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4713-145">**[Creazione di un utente test di Salesforce](#creating-a-salesforce-test-user)**: per avere una controparte di Britta Simon in Salesforce collegata alla rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c4713-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4713-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4713-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4713-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c4713-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4713-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4713-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4713-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="c4713-150">**Per configurare Single Sign-On di Azure AD con Salesforce, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c4713-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="c4713-151">Nella pagina di integrazione dell'applicazione **Salesforce** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c4713-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c4713-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c4713-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="c4713-155">Nella sezione **URL e dominio Salesforce** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c4713-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="c4713-157">Nella casella di testo **URL di accesso** digitare il valore usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="c4713-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="c4713-158">Account aziendale: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4713-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="c4713-159">Account sviluppatore: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4713-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4713-160">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c4713-160">These values are not the real.</span></span> <span data-ttu-id="c4713-161">è necessario aggiornarli con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="c4713-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="c4713-162">Per ottenere questi valori, contattare il [team di supporto clienti di Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="c4713-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="c4713-163">Nella sezione **Certificato di firma SAML** fare clic su **Certificato** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="c4713-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="c4713-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c4713-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4713-167">Nella sezione **Configurazione di Salesforce** fare clic su **Configura Salesforce** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="c4713-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c4713-168">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="c4713-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="c4713-169">![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="c4713-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="c4713-170">Aprire una nuova scheda del browser e accedere all'account di amministratore di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="c4713-171">Nel pannello di navigazione **Administrator** fare clic su **Security Controls** per espandere la sezione correlata.</span><span class="sxs-lookup"><span data-stu-id="c4713-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="c4713-172">Fare quindi clic su **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="c4713-172">Then click **Single Sign-On Settings**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="c4713-174">Nella pagina **Single Sign-On Settings** fare clic su **Edit**.</span><span class="sxs-lookup"><span data-stu-id="c4713-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="c4713-175">![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="c4713-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="c4713-176">Se non si è in grado di abilitare le impostazioni dell'accesso Single Sign-On per l'account Salesforce, potrebbe essere necessario contattare il [team di supporto clienti di Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="c4713-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="c4713-177">Selezionare **SAML Enabled**, quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="c4713-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="c4713-179">Per configurare le impostazioni dell'accesso Single Sign-On SAML, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="c4713-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="c4713-181">Nella pagina **SAML Single Sign-On Setting Edit** effettuare le configurazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4713-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="c4713-183">a.</span><span class="sxs-lookup"><span data-stu-id="c4713-183">a.</span></span> <span data-ttu-id="c4713-184">Nel campo **Name** specificare un nome descrittivo per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="c4713-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="c4713-185">Se si specifica un valore per **Name**, verrà popolata automaticamente la casella di testo **API Name**.</span><span class="sxs-lookup"><span data-stu-id="c4713-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="c4713-186">b.</span><span class="sxs-lookup"><span data-stu-id="c4713-186">b.</span></span> <span data-ttu-id="c4713-187">Incollare il valore **SMAL Entity ID** nel campo **Issuer** in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="c4713-188">c.</span><span class="sxs-lookup"><span data-stu-id="c4713-188">c.</span></span> <span data-ttu-id="c4713-189">Nella casella di testo **Entity Id**immettere il nome di dominio di Salesforce nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="c4713-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="c4713-190">Account aziendale: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4713-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="c4713-191">Account sviluppatore: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4713-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="c4713-192">d.</span><span class="sxs-lookup"><span data-stu-id="c4713-192">d.</span></span> <span data-ttu-id="c4713-193">Fare clic su **Browse** o **Choose File** per aprire la finestra di dialogo **Choose File to Upload**, selezionare il certificato Salesforce, quindi fare clic su **Open** per caricarlo.</span><span class="sxs-lookup"><span data-stu-id="c4713-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="c4713-194">e.</span><span class="sxs-lookup"><span data-stu-id="c4713-194">e.</span></span> <span data-ttu-id="c4713-195">In **SAML Identity Type** selezionare **Assertion contains User's salesforce.com username**.</span><span class="sxs-lookup"><span data-stu-id="c4713-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="c4713-196">f.</span><span class="sxs-lookup"><span data-stu-id="c4713-196">f.</span></span> <span data-ttu-id="c4713-197">In **SAML Identity Location** selezionare **Identity is in the NameIdentifier element of the Subject statement**</span><span class="sxs-lookup"><span data-stu-id="c4713-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="c4713-198">g.</span><span class="sxs-lookup"><span data-stu-id="c4713-198">g.</span></span> <span data-ttu-id="c4713-199">Incollare **URL servizio Single Sign-On** nel campo **URL di accesso provider di identità** in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="c4713-200">h.</span><span class="sxs-lookup"><span data-stu-id="c4713-200">h.</span></span> <span data-ttu-id="c4713-201">Per **Service Provider Initiated Request Binding** selezionare **HTTP Redirect**.</span><span class="sxs-lookup"><span data-stu-id="c4713-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="c4713-202">i.</span><span class="sxs-lookup"><span data-stu-id="c4713-202">i.</span></span> <span data-ttu-id="c4713-203">Fare infine clic su **Save** per applicare le impostazioni di SAML Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c4713-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="c4713-204">Nel pannello di navigazione sinistro in Salesforce fare clic su **Domain Management** per espandere la sezione correlata, quindi fare clic su **My Domain**.</span><span class="sxs-lookup"><span data-stu-id="c4713-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="c4713-206">Scorrere verso il basso fino alla sezione **Authentication Configuration**, quindi fare clic su **Edit**.</span><span class="sxs-lookup"><span data-stu-id="c4713-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="c4713-208">Nella sezione **Authentication Service** selezionare il nome descrittivo della configurazione SAML Single Sign-On, quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="c4713-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="c4713-210">Se vengono selezionati più servizi di autenticazione, agli utenti viene richiesta la selezione del servizio di autenticazione da usare per l'accesso quando si tenta di avviare l'accesso Single Sign-On all'ambiente di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="c4713-211">Se non si vuole visualizzare la richiesta, è consigliabile **lasciare deselezionati tutti gli altri servizi di autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="c4713-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="c4713-212">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c4713-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c4713-213">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c4713-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c4713-214">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD)</span><span class="sxs-lookup"><span data-stu-id="c4713-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4713-215">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4713-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4713-216">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4713-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c4713-218">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c4713-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c4713-219">Nel riquadro di spostamento sinistro del **portale di Azure** fare clic sull'icona di **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4713-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4713-221">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="c4713-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4713-223">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="c4713-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4713-225">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c4713-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4713-227">a.</span><span class="sxs-lookup"><span data-stu-id="c4713-227">a.</span></span> <span data-ttu-id="c4713-228">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4713-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4713-229">b.</span><span class="sxs-lookup"><span data-stu-id="c4713-229">b.</span></span> <span data-ttu-id="c4713-230">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c4713-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4713-231">c.</span><span class="sxs-lookup"><span data-stu-id="c4713-231">c.</span></span> <span data-ttu-id="c4713-232">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="c4713-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c4713-233">d.</span><span class="sxs-lookup"><span data-stu-id="c4713-233">d.</span></span> <span data-ttu-id="c4713-234">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c4713-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="c4713-235">Creazione di un utente test di Salesforce</span><span class="sxs-lookup"><span data-stu-id="c4713-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="c4713-236">In questa sezione si crea un utente di nome Britta Simon in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="c4713-237">Salesforce supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c4713-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="c4713-238">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="c4713-238">There is no action item for you in this section.</span></span> <span data-ttu-id="c4713-239">Se un utente non esiste in Salesforce, ne viene creato uno nuovo quando si tenta di accedere a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c4713-240">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4713-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c4713-241">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4713-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c4713-243">**Per assegnare Britta Simon a Salesforce, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c4713-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="c4713-244">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c4713-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c4713-246">Nell'elenco di applicazioni selezionare **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="c4713-246">In the applications list, select **Salesforce**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="c4713-248">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c4713-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c4713-250">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c4713-250">Click **Add** button.</span></span> <span data-ttu-id="c4713-251">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c4713-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c4713-253">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c4713-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c4713-254">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c4713-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4713-255">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c4713-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4713-256">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c4713-256">Testing single sign-on</span></span>

<span data-ttu-id="c4713-257">Per testare le impostazioni dell'accesso Single Sign-On, aprire il pannello di accesso all'indirizzo [https://myapps.microsoft.com](https://myapps.microsoft.com/), quindi accedere all'account di test e fare clic su **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="c4713-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4713-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c4713-258">Additional resources</span></span>

* [<span data-ttu-id="c4713-259">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4713-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4713-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4713-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c4713-261">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="c4713-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

