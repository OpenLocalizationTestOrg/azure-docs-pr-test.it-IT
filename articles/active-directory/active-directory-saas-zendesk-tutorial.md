---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zendesk | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Zendesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="a634f-103">Esercitazione: Integrazione di Azure Active Directory con Zendesk</span><span class="sxs-lookup"><span data-stu-id="a634f-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="a634f-104">Questa esercitazione descrive come integrare Zendesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a634f-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a634f-105">L'integrazione di Zendesk con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a634f-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a634f-106">È possibile controllare in Azure AD chi può accedere a Zendesk</span><span class="sxs-lookup"><span data-stu-id="a634f-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="a634f-107">È possibile abilitare gli utenti per l'accesso automatico a Zendesk (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a634f-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a634f-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a634f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a634f-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a634f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a634f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a634f-110">Prerequisites</span></span>

<span data-ttu-id="a634f-111">Per configurare l'integrazione di Azure AD con Zendesk, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a634f-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="a634f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a634f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a634f-113">Zendesk abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a634f-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="a634f-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a634f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="a634f-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a634f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a634f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a634f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a634f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a634f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="a634f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a634f-118">Scenario description</span></span>
<span data-ttu-id="a634f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a634f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a634f-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a634f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a634f-121">Aggiunta di Zendesk dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a634f-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="a634f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a634f-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="a634f-123">Aggiunta di Zendesk dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a634f-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="a634f-124">Per configurare l'integrazione di Zendesk in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a634f-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a634f-125">**Per aggiungere Zendesk dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a634f-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a634f-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a634f-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a634f-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a634f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a634f-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a634f-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a634f-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a634f-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a634f-133">Nella casella di ricerca digitare **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="a634f-133">In the search box, type **Zendesk**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="a634f-135">Nel pannello dei risultati selezionare **Zendesk** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a634f-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a634f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a634f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a634f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zendesk in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a634f-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a634f-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Zendesk che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a634f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="a634f-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Zendesk.</span><span class="sxs-lookup"><span data-stu-id="a634f-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="a634f-141">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in Zendesk.</span><span class="sxs-lookup"><span data-stu-id="a634f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="a634f-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Zendesk, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a634f-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a634f-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a634f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a634f-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a634f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a634f-145">**[Creazione di un utente di test di Zendesk](#creating-a-zendesk-test-user)**: per avere una controparte di Britta Simon in Zendesk collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a634f-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a634f-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a634f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a634f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a634f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a634f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a634f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a634f-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Zendesk.</span><span class="sxs-lookup"><span data-stu-id="a634f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="a634f-150">**Per configurare Single Sign-On di Azure AD con Zendesk, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a634f-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="a634f-151">Nella pagina di integrazione dell'applicazione **Zendesk** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a634f-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a634f-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a634f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="a634f-155">Nella sezione **Zendesk Domain and URLs** (URL e dominio Zendesk) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a634f-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="a634f-157">a.</span><span class="sxs-lookup"><span data-stu-id="a634f-157">a.</span></span> <span data-ttu-id="a634f-158">Nella casella di testo **URL di accesso** digitare il valore usando il modello seguente: `https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="a634f-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="a634f-159">b.</span><span class="sxs-lookup"><span data-stu-id="a634f-159">b.</span></span> <span data-ttu-id="a634f-160">Nella casella di testo **Identificatore** digitare il valore adottando il modello seguente: `https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="a634f-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a634f-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="a634f-161">These values are not real.</span></span> <span data-ttu-id="a634f-162">è necessario aggiornarli con l'URL identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="a634f-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="a634f-163">Per ottenere questi valori, contattare il [team di supporto di Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise).</span><span class="sxs-lookup"><span data-stu-id="a634f-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="a634f-164">Zendesk prevede che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="a634f-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a634f-165">Non sono presenti attributi SAML obbligatori ma facoltativamente è possibile aggiungere un attributo dalla sezione **Attributi utente** sezione seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a634f-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="a634f-167">a.</span><span class="sxs-lookup"><span data-stu-id="a634f-167">a.</span></span> <span data-ttu-id="a634f-168">Fare clic sulla casella di controllo **View and edit all the other attributes** (Visualizza e modifica tutti gli altri attributi).</span><span class="sxs-lookup"><span data-stu-id="a634f-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="a634f-170">b.</span><span class="sxs-lookup"><span data-stu-id="a634f-170">b.</span></span> <span data-ttu-id="a634f-171">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="a634f-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a634f-173">c.</span><span class="sxs-lookup"><span data-stu-id="a634f-173">c.</span></span> <span data-ttu-id="a634f-174">Nella casella di testo **Nome** digitare il nome dell'attributo (ad esempio **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="a634f-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="a634f-175">d.</span><span class="sxs-lookup"><span data-stu-id="a634f-175">d.</span></span> <span data-ttu-id="a634f-176">Nell'elenco **Valore** selezionare il valore dell'attributo (ad esempio **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="a634f-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="a634f-177">e.</span><span class="sxs-lookup"><span data-stu-id="a634f-177">e.</span></span> <span data-ttu-id="a634f-178">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="a634f-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="a634f-179">Usare gli attributi dell'estensione per aggiungere attributi che non sono in Azure AD per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a634f-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="a634f-180">Fare clic su [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) (Attributi utente che possono essere impostati in SAML) per ottenere l'elenco completo degli attributi accettati da **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="a634f-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="a634f-181">Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE** del certificato.</span><span class="sxs-lookup"><span data-stu-id="a634f-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="a634f-183">Nella sezione **Zendesk Configuration** (Configurazione di Zendesk) fare clic su **Configure Zendesk** (Configura Zendesk) per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="a634f-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a634f-184">Copiare l'**URL servizio Single Sign-On SAML e l'URL di disconnessione** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="a634f-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="a634f-186">In un'altra finestra del Web browser accedere al sito aziendale di Zendesk come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a634f-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="a634f-187">Fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="a634f-187">Click **Admin**.</span></span>

9. <span data-ttu-id="a634f-188">Nel riquadro di spostamento sinistro fare clic su **Impostazioni** e quindi su **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="a634f-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="a634f-189">Nella pagina **Sicurezza** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a634f-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="a634f-190">![Sicurezza](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="a634f-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="a634f-191">![Single Sign-On](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a634f-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="a634f-192">a.</span><span class="sxs-lookup"><span data-stu-id="a634f-192">a.</span></span> <span data-ttu-id="a634f-193">Fare clic sulla scheda **Amministratore e agenti**.</span><span class="sxs-lookup"><span data-stu-id="a634f-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="a634f-194">b.</span><span class="sxs-lookup"><span data-stu-id="a634f-194">b.</span></span> <span data-ttu-id="a634f-195">Selezionare **Single sign-on (SSO) e SAML** e quindi **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a634f-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="a634f-196">c.</span><span class="sxs-lookup"><span data-stu-id="a634f-196">c.</span></span> <span data-ttu-id="a634f-197">Nella casella di testo **SAML SSO URL** (URL SSO SAML) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a634f-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="a634f-198">d.</span><span class="sxs-lookup"><span data-stu-id="a634f-198">d.</span></span> <span data-ttu-id="a634f-199">Nella casella di testo **Remote Log Out URL** (URL di disconnessione remota) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a634f-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="a634f-200">e.</span><span class="sxs-lookup"><span data-stu-id="a634f-200">e.</span></span> <span data-ttu-id="a634f-201">Nella casella di testo **Certificate Fingerprint** (Impronta digitale certificato) incollare il valore **Identificazione personale** del certificato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a634f-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="a634f-202">f.</span><span class="sxs-lookup"><span data-stu-id="a634f-202">f.</span></span> <span data-ttu-id="a634f-203">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="a634f-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a634f-204">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a634f-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="a634f-205">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a634f-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a634f-207">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a634f-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a634f-208">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a634f-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a634f-210">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a634f-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a634f-212">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a634f-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a634f-214">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a634f-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a634f-216">a.</span><span class="sxs-lookup"><span data-stu-id="a634f-216">a.</span></span> <span data-ttu-id="a634f-217">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a634f-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a634f-218">b.</span><span class="sxs-lookup"><span data-stu-id="a634f-218">b.</span></span> <span data-ttu-id="a634f-219">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a634f-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a634f-220">c.</span><span class="sxs-lookup"><span data-stu-id="a634f-220">c.</span></span> <span data-ttu-id="a634f-221">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a634f-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a634f-222">d.</span><span class="sxs-lookup"><span data-stu-id="a634f-222">d.</span></span> <span data-ttu-id="a634f-223">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a634f-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="a634f-224">Creazione di un utente test Zendesk</span><span class="sxs-lookup"><span data-stu-id="a634f-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="a634f-225">Per consentire agli utenti di Azure AD di accedere a **Zendesk**, è necessario eseguirne il provisioning in **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="a634f-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="a634f-226">Il comportamento si basa sul ruolo assegnato nelle applicazioni:</span><span class="sxs-lookup"><span data-stu-id="a634f-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="a634f-227">All'accesso viene eseguito automaticamente il provisioning degli account dell'**utente finale**.</span><span class="sxs-lookup"><span data-stu-id="a634f-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="a634f-228">Il provisioning degli account **Agente** e **Amministratore** devono essere eseguiti manualmente in **Zendesk** prima dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="a634f-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="a634f-229">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a634f-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a634f-230">Accedere al tenant di **Zendesk** .</span><span class="sxs-lookup"><span data-stu-id="a634f-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="a634f-231">Selezionare la scheda **Customer List** .</span><span class="sxs-lookup"><span data-stu-id="a634f-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="a634f-232">Selezionare la scheda **User** e fare clic su **Add**.</span><span class="sxs-lookup"><span data-stu-id="a634f-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="a634f-233">![Aggiungere un utente](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="a634f-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="a634f-234">Digitare l'indirizzo di posta elettronica di un account Azure AD esistente di cui si vuole eseguire il provisioning e quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="a634f-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="a634f-235">![Nuovo utente](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="a634f-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="a634f-236">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Zendesk per eseguire il provisioning degli account utente Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a634f-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a634f-237">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a634f-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a634f-238">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Zendesk.</span><span class="sxs-lookup"><span data-stu-id="a634f-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a634f-240">**Per assegnare Britta Simon a Zendesk, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a634f-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="a634f-241">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a634f-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a634f-243">Nell'elenco di applicazioni selezionare **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="a634f-243">In the applications list, select **Zendesk**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="a634f-245">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a634f-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a634f-247">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a634f-247">Click **Add** button.</span></span> <span data-ttu-id="a634f-248">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a634f-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a634f-250">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a634f-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a634f-251">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a634f-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a634f-252">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a634f-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a634f-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a634f-253">Testing single sign-on</span></span>

<span data-ttu-id="a634f-254">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a634f-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a634f-255">Quando si fa clic sul riquadro di Zendesk nel riquadro di accesso, si dovrebbe accedere automaticamente all'applicazione Zendesk.</span><span class="sxs-lookup"><span data-stu-id="a634f-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="a634f-256">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a634f-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a634f-257">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a634f-257">Additional resources</span></span>

* [<span data-ttu-id="a634f-258">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a634f-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a634f-259">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a634f-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
