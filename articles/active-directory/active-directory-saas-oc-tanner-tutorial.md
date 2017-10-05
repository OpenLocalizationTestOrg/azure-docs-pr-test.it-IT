---
title: 'Esercitazione: Integrazione di Azure Active Directory con O.C. Tanner - AppreciateHub | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e O.C. Tanner - AppreciateHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="9462b-105">Esercitazione: Integrazione di Azure Active Directory con O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="9462b-106">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="9462b-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="9462b-107">Questa esercitazione descrive come integrare O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="9462b-108">Tanner - AppreciateHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9462b-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9462b-109">L'integrazione di O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-109">Integrating O.C.</span></span> <span data-ttu-id="9462b-110">Tanner - AppreciateHub con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9462b-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9462b-111">È possibile controllare in Azure AD chi può accedere a O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="9462b-112">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="9462b-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="9462b-113">È possibile abilitare gli utenti ad accedere automaticamente a O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="9462b-114">Tanner - AppreciateHub (Single Sign-On) con i relativi account Azure AD</span><span class="sxs-lookup"><span data-stu-id="9462b-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9462b-115">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9462b-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9462b-116">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9462b-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9462b-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9462b-117">Prerequisites</span></span>

<span data-ttu-id="9462b-118">Per configurare l'integrazione di Azure Active Directory con O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="9462b-119">Tanner - AppreciateHub, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9462b-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="9462b-120">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9462b-120">An Azure AD subscription</span></span>
- <span data-ttu-id="9462b-121">Sottoscrizione di O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-121">A O.C.</span></span> <span data-ttu-id="9462b-122">Sottoscrizione di Tanner - AppreciateHub abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9462b-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9462b-123">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9462b-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9462b-124">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9462b-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9462b-125">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9462b-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9462b-126">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9462b-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9462b-127">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9462b-127">Scenario description</span></span>
<span data-ttu-id="9462b-128">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9462b-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9462b-129">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9462b-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9462b-130">Aggiunta di O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-130">Adding O.C.</span></span> <span data-ttu-id="9462b-131">Tanner - AppreciateHub dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9462b-131">Tanner - AppreciateHub from the gallery</span></span>
2. <span data-ttu-id="9462b-132">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9462b-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="9462b-133">Aggiunta di O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-133">Adding O.C.</span></span> <span data-ttu-id="9462b-134">Tanner - AppreciateHub dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9462b-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="9462b-135">Per configurare l'integrazione di O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-135">To configure the integration of O.C.</span></span> <span data-ttu-id="9462b-136">Tanner - AppreciateHub in Azure AD, è necessario aggiungere O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="9462b-137">Tanner - AppreciateHub dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9462b-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9462b-138">**Per aggiungere O.C. Tanner - AppreciateHub dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9462b-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9462b-139">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9462b-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9462b-141">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9462b-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9462b-142">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9462b-142">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="9462b-144">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="9462b-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="9462b-146">Nella casella di ricerca digitare **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="9462b-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="9462b-148">Nel riquadro dei risultati selezionare **O.C. Tanner - AppreciateHub** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9462b-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9462b-150">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9462b-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9462b-151">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="9462b-152">Tanner - AppreciateHub in base a un utente test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9462b-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9462b-153">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="9462b-154">Tanner - AppreciateHub che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9462b-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="9462b-155">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="9462b-156">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="9462b-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="9462b-157">In O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-157">In O.C.</span></span> <span data-ttu-id="9462b-158">Tanner - AppreciateHub per stabilire la relazione di collegamento, assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="9462b-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9462b-159">Per configurare e testare l'accesso Single Sign-On di Azure AD con O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="9462b-160">Tanner - AppreciateHub, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9462b-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9462b-161">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9462b-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9462b-162">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9462b-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9462b-163">**[Creazione di un utente test di O.C. Tanner - AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)** - per avere una controparte di Britta Simon in O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="9462b-164">Tanner - AppreciateHub collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9462b-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9462b-165">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9462b-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9462b-166">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="9462b-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9462b-167">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9462b-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9462b-168">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On con O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="9462b-169">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="9462b-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="9462b-170">**Per configurare l'accesso Single Sign-On di Azure AD con O.C. Tanner - AppreciateHub, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9462b-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="9462b-171">Nella pagina di integrazione dell'applicazione **O.C. Tanner - AppreciateHub** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9462b-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="9462b-173">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9462b-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="9462b-175">Nella sezione **Dominio e URL O.C. Tanner - AppreciateHub**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9462b-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="9462b-177">a.</span><span class="sxs-lookup"><span data-stu-id="9462b-177">a.</span></span> <span data-ttu-id="9462b-178">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="9462b-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9462b-179">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="9462b-179">This value is not real.</span></span> <span data-ttu-id="9462b-180">è necessario aggiornare questo valore con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="9462b-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="9462b-181">Contattare il [team. di supporto O.C. Tanner - AppreciateHub](mailto:sso@octanner.com) per ottenere questo valore.</span><span class="sxs-lookup"><span data-stu-id="9462b-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="9462b-182">b.</span><span class="sxs-lookup"><span data-stu-id="9462b-182">b.</span></span> <span data-ttu-id="9462b-183">Aprire il file dei metadati usando il collegamento seguente: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="9462b-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="9462b-184">c.</span><span class="sxs-lookup"><span data-stu-id="9462b-184">c.</span></span> <span data-ttu-id="9462b-185">Individuare il nodo **md:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="9462b-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="9462b-186">d.</span><span class="sxs-lookup"><span data-stu-id="9462b-186">d.</span></span> <span data-ttu-id="9462b-187">Copiare il valore dell'attributo **Location** .</span><span class="sxs-lookup"><span data-stu-id="9462b-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![Configurare le impostazioni dell'app][12]
   
    <span data-ttu-id="9462b-189">e.</span><span class="sxs-lookup"><span data-stu-id="9462b-189">e.</span></span> <span data-ttu-id="9462b-190">Nella casella di testo **Sign On URL** incollare il valore ottenuto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="9462b-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

4. <span data-ttu-id="9462b-191">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="9462b-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="9462b-193">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="9462b-193">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9462b-195">Per configurare l’accesso Single Sign-On sul lato **O.C. Tanner - AppreciateHub**, è necessario inviare il file di **XML metadati** scaricato al team di supporto di [O.C. Tanner - AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="9462b-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="9462b-196">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="9462b-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9462b-197">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="9462b-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9462b-198">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9462b-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9462b-199">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9462b-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="9462b-200">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9462b-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="9462b-202">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9462b-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9462b-203">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9462b-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9462b-205">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="9462b-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9462b-207">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="9462b-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9462b-209">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9462b-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9462b-211">a.</span><span class="sxs-lookup"><span data-stu-id="9462b-211">a.</span></span> <span data-ttu-id="9462b-212">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9462b-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9462b-213">b.</span><span class="sxs-lookup"><span data-stu-id="9462b-213">b.</span></span> <span data-ttu-id="9462b-214">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9462b-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9462b-215">c.</span><span class="sxs-lookup"><span data-stu-id="9462b-215">c.</span></span> <span data-ttu-id="9462b-216">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="9462b-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9462b-217">d.</span><span class="sxs-lookup"><span data-stu-id="9462b-217">d.</span></span> <span data-ttu-id="9462b-218">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9462b-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="9462b-219">Creazione di un utente test di O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-219">Creating a O.C.</span></span> <span data-ttu-id="9462b-220">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="9462b-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="9462b-221">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="9462b-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="9462b-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="9462b-223">**Per creare un utente denominato Britta Simon in O.C. Tanner - AppreciateHub, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9462b-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="9462b-224">Chiedere al [team. di supporto di O.C. Tanner - AppreciateHub](mailto:sso@octanner.com) di creare un utente con un valore per l'attributo nameID equivalente al nome utente di Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9462b-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9462b-225">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9462b-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9462b-226">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="9462b-227">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="9462b-227">Tanner - AppreciateHub.</span></span>

![Assegna utente][200] 

<span data-ttu-id="9462b-229">**Per assegnare Britta Simon a O.C. Tanner - AppreciateHub, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9462b-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="9462b-230">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9462b-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9462b-232">Nell'elenco delle applicazioni selezionare **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="9462b-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="9462b-234">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="9462b-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="9462b-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9462b-236">Click **Add** button.</span></span> <span data-ttu-id="9462b-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9462b-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="9462b-239">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="9462b-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9462b-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9462b-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9462b-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9462b-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9462b-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9462b-242">Testing single sign-on</span></span>

<span data-ttu-id="9462b-243">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9462b-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="9462b-244">Quando si fa clic sul riquadro O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-244">When you click the O.C.</span></span> <span data-ttu-id="9462b-245">Tanner - AppreciateHub nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione O.C.</span><span class="sxs-lookup"><span data-stu-id="9462b-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="9462b-246">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="9462b-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9462b-247">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9462b-247">Additional resources</span></span>

* [<span data-ttu-id="9462b-248">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9462b-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9462b-249">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9462b-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

