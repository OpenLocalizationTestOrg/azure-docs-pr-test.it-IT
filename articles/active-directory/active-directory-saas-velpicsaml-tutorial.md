---
title: 'Esercitazione: Integrazione di Azure Active Directory con Velpic SAML| Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Velpic SAML.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="a6f04-103">Esercitazione: Integrazione di Azure Active Directory con Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="a6f04-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="a6f04-104">Questa esercitazione spiega come integrare Velpic SAML con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6f04-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6f04-105">L'integrazione di Velpic SAML con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6f04-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a6f04-106">È possibile controllare in Azure AD chi può accedere a Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="a6f04-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="a6f04-107">È possibile abilitare gli utenti per l'accesso automatico a Velpic SAML (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6f04-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6f04-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="a6f04-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="a6f04-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6f04-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6f04-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a6f04-110">Prerequisites</span></span>

<span data-ttu-id="a6f04-111">Per configurare l'integrazione di Azure AD con Velpic SAML, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6f04-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="a6f04-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6f04-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6f04-113">Sottoscrizione di Velpic SAML abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a6f04-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6f04-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a6f04-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6f04-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6f04-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6f04-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a6f04-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a6f04-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6f04-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6f04-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a6f04-118">Scenario description</span></span>
<span data-ttu-id="a6f04-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a6f04-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6f04-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6f04-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6f04-121">Aggiunta di Velpic SAML dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a6f04-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="a6f04-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6f04-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="a6f04-123">Aggiungere Velpic SAML dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a6f04-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="a6f04-124">Per configurare l'integrazione di Velpic SAML in Azure AD, è necessario aggiungere Velpic SAML dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a6f04-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a6f04-125">**Per aggiungere Velpic SAML dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a6f04-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a6f04-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a6f04-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a6f04-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a6f04-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a6f04-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a6f04-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a6f04-133">Nella casella di ricerca digitare **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-133">In the search box, type **Velpic SAML**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="a6f04-135">Nel pannello dei risultati selezionare **Velpic SAML** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6f04-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6f04-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6f04-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6f04-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Velpic SAML in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a6f04-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a6f04-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Velpic SAML che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6f04-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="a6f04-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="a6f04-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="a6f04-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** (Nome utente) in Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="a6f04-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="a6f04-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Velpic SAML, è necessario completare i seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="a6f04-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a6f04-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a6f04-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a6f04-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6f04-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6f04-145">**[Creazione di un utente test di Velpic SAML](#creating-a-velpic-saml-test-user)** : per avere una controparte di Britta Simon in Velpic SAML collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6f04-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a6f04-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6f04-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6f04-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a6f04-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6f04-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6f04-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6f04-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="a6f04-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="a6f04-150">**Per configurare Single Sign-On di Azure AD con Velpic SAML, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a6f04-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="a6f04-151">Nella pagina di integrazione dell'applicazione **Velpic SAML** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a6f04-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a6f04-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="a6f04-155">Immettere i dettagli nella sezione **URL e dominio Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="a6f04-157">a.</span><span class="sxs-lookup"><span data-stu-id="a6f04-157">a.</span></span> <span data-ttu-id="a6f04-158">Nella casella di testo **URL di accesso** digitare il valore come: `https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="a6f04-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="a6f04-159">b.</span><span class="sxs-lookup"><span data-stu-id="a6f04-159">b.</span></span> <span data-ttu-id="a6f04-160">Nella casella di testo **Identificatore** incollare il valore dell'**URL di Single Sign-On** `https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="a6f04-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a6f04-161">Si noti che l'URL di Single Sign-On verrà indicato dal team di Velpic SAML e il valore dell'identificatore sarà disponibile quando si configura il plug-in SSO sul lato Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="a6f04-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="a6f04-162">È necessario copiare tale valore dalla pagina dell'applicazione Velpic SAML e incollarlo qui.</span><span class="sxs-lookup"><span data-stu-id="a6f04-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="a6f04-163">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="a6f04-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="a6f04-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a6f04-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a6f04-167">Nella sezione Configurazione Velpic SAML scegliere Configura Velpic SAML per aprire la finestra di dialogo Configura accesso.</span><span class="sxs-lookup"><span data-stu-id="a6f04-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="a6f04-168">Copiare l'ID di entità SAML dalla sezione Riferimento rapido.</span><span class="sxs-lookup"><span data-stu-id="a6f04-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="a6f04-169">In un'altra finestra del Web browser accedere al sito aziendale di Velpic SAML come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a6f04-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="a6f04-170">Fare clic sulla scheda **Manage** (Gestisci), passare alla sezione **Integration** (Integrazione) e qui scegliere **Plugins** per creare un nuovo plug-in per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a6f04-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="a6f04-172">Fare clic sul pulsante **Add plugin** (Aggiungi plug-in).</span><span class="sxs-lookup"><span data-stu-id="a6f04-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="a6f04-174">Fare clic sul riquadro **SAML** nella pagina Add plugin (Aggiungi plug-in).</span><span class="sxs-lookup"><span data-stu-id="a6f04-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="a6f04-176">Immettere il nome del nuovo plug-in SAML e scegliere il pulsante **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="a6f04-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="a6f04-178">Immettere i dettagli seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6f04-178">Enter the details as follows:</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="a6f04-180">a.</span><span class="sxs-lookup"><span data-stu-id="a6f04-180">a.</span></span> <span data-ttu-id="a6f04-181">Nella casella di testo **Name** (Nome) digitare il nome del plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="a6f04-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="a6f04-182">b.</span><span class="sxs-lookup"><span data-stu-id="a6f04-182">b.</span></span> <span data-ttu-id="a6f04-183">Nella casella di testo **Issuer URL** (URL dell'autorità di certificazione) incollare l'**ID di entità SAML** copiato in precedenza dalla finestra **Configura accesso** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f04-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="a6f04-184">c.</span><span class="sxs-lookup"><span data-stu-id="a6f04-184">c.</span></span> <span data-ttu-id="a6f04-185">Nel riquadro della **configurazione dei metadati del provider** caricare il file XML dei metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f04-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="a6f04-186">d.</span><span class="sxs-lookup"><span data-stu-id="a6f04-186">d.</span></span> <span data-ttu-id="a6f04-187">È anche possibile scegliere di abilitare SAML al momento del provisioning selezionando la casella di controllo **Auto create new users** (Crea automaticamente nuovi utenti).</span><span class="sxs-lookup"><span data-stu-id="a6f04-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="a6f04-188">Se un utente non esiste in Velpic e questo flag non è abilitato, l'accesso da Azure avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a6f04-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="a6f04-189">Se il flag è abilitato, verrà automaticamente eseguito il provisioning dell'utente in Velpic al momento dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="a6f04-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="a6f04-190">e.</span><span class="sxs-lookup"><span data-stu-id="a6f04-190">e.</span></span> <span data-ttu-id="a6f04-191">Copiare l'**URL di Single Sign-On** dalla casella di testo e incollarlo nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f04-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="a6f04-192">f.</span><span class="sxs-lookup"><span data-stu-id="a6f04-192">f.</span></span> <span data-ttu-id="a6f04-193">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6f04-194">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6f04-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6f04-195">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f04-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a6f04-197">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a6f04-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a6f04-198">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a6f04-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6f04-200">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a6f04-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6f04-202">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6f04-204">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a6f04-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6f04-206">a.</span><span class="sxs-lookup"><span data-stu-id="a6f04-206">a.</span></span> <span data-ttu-id="a6f04-207">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6f04-208">b.</span><span class="sxs-lookup"><span data-stu-id="a6f04-208">b.</span></span> <span data-ttu-id="a6f04-209">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a6f04-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6f04-210">c.</span><span class="sxs-lookup"><span data-stu-id="a6f04-210">c.</span></span> <span data-ttu-id="a6f04-211">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a6f04-212">d.</span><span class="sxs-lookup"><span data-stu-id="a6f04-212">d.</span></span> <span data-ttu-id="a6f04-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="a6f04-214">Creare un utente test di Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="a6f04-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="a6f04-215">Questo passaggio in genere non è necessario poiché l'applicazione supporta il provisioning degli utenti just-in-time.</span><span class="sxs-lookup"><span data-stu-id="a6f04-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="a6f04-216">Se il provisioning automatico degli utenti non è abilitato, la creazione manuale dell'utente può essere eseguita come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="a6f04-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="a6f04-217">Accedere al sito aziendale di Velpic SAML come amministratore e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a6f04-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="a6f04-218">Fare clic sulla scheda Manage (Gestisci) e passare alla sezione Users (Utenti), quindi fare clic sul pulsante New (Nuovo) per aggiungere gli utenti.</span><span class="sxs-lookup"><span data-stu-id="a6f04-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![Aggiungi utente](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="a6f04-220">Nella finestra di dialogo **Create New User** (Crea nuovo utente) effettuare le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="a6f04-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="a6f04-222">a.</span><span class="sxs-lookup"><span data-stu-id="a6f04-222">a.</span></span> <span data-ttu-id="a6f04-223">Digitare il nome di Britta Simon nella casella di testo **First Name** (Nome).</span><span class="sxs-lookup"><span data-stu-id="a6f04-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="a6f04-224">b.</span><span class="sxs-lookup"><span data-stu-id="a6f04-224">b.</span></span> <span data-ttu-id="a6f04-225">Digitare il cognome di Britta Simon nella casella di testo **Last Name** (Cognome).</span><span class="sxs-lookup"><span data-stu-id="a6f04-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="a6f04-226">c.</span><span class="sxs-lookup"><span data-stu-id="a6f04-226">c.</span></span> <span data-ttu-id="a6f04-227">Digitare il nome utente di Britta Simon nella casella di testo **User Name** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="a6f04-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="a6f04-228">d.</span><span class="sxs-lookup"><span data-stu-id="a6f04-228">d.</span></span> <span data-ttu-id="a6f04-229">Nella casella di testo **Email** (Posta elettronica) digitare l'indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6f04-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="a6f04-230">e.</span><span class="sxs-lookup"><span data-stu-id="a6f04-230">e.</span></span> <span data-ttu-id="a6f04-231">Le informazioni rimanenti sono facoltative, se necessario si possono compilare.</span><span class="sxs-lookup"><span data-stu-id="a6f04-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="a6f04-232">f.</span><span class="sxs-lookup"><span data-stu-id="a6f04-232">f.</span></span> <span data-ttu-id="a6f04-233">Fare clic su **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a6f04-234">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6f04-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a6f04-235">In questa sezione si concede a Britta Simon l'accesso a Velpic SAML per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f04-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a6f04-237">**Per assegnare Britta Simon a Velpic SAML, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a6f04-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="a6f04-238">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a6f04-240">Nell'elenco di applicazioni selezionare **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="a6f04-242">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a6f04-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a6f04-244">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-244">Click **Add** button.</span></span> <span data-ttu-id="a6f04-245">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a6f04-247">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a6f04-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a6f04-248">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6f04-249">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a6f04-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6f04-250">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a6f04-250">Testing single sign-on</span></span>

<span data-ttu-id="a6f04-251">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a6f04-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="a6f04-252">Quando si fa clic sul riquadro Velpic SAML nel Pannello di accesso, viene visualizzata la pagina di accesso dell'applicazione Velpic SAML,</span><span class="sxs-lookup"><span data-stu-id="a6f04-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="a6f04-253">in cui dovrebbe apparire il pulsante **Log In With Azure AD** (Accedi con Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6f04-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="a6f04-255">Fare clic sul pulsante **Log In With Azure AD** (Accedi con Azure AD) per accedere a Velpic usando il proprio account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6f04-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a6f04-256">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a6f04-256">Additional resources</span></span>

* [<span data-ttu-id="a6f04-257">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6f04-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6f04-258">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6f04-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

