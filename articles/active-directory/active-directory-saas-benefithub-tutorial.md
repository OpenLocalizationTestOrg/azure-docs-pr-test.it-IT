---
title: 'Esercitazione: Integrazione di Azure Active Directory con BenefitHub | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e BenefitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 8df9c0d8443d6685253207ed1915c780275014fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="56c2e-103">Esercitazione: Integrazione di Azure Active Directory con BenefitHub</span><span class="sxs-lookup"><span data-stu-id="56c2e-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="56c2e-104">Questa esercitazione descrive come integrare BenefitHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56c2e-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56c2e-105">L'integrazione di BenefitHub con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="56c2e-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="56c2e-106">È possibile controllare in Azure AD chi può accedere a BenefitHub</span><span class="sxs-lookup"><span data-stu-id="56c2e-106">You can control in Azure AD who has access to BenefitHub</span></span>
- <span data-ttu-id="56c2e-107">È possibile abilitare gli utenti per l'accesso automatico a BenefitHub (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="56c2e-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56c2e-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56c2e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="56c2e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56c2e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56c2e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="56c2e-110">Prerequisites</span></span>

<span data-ttu-id="56c2e-111">Per configurare l'integrazione di Azure AD con BenefitHub, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="56c2e-111">To configure Azure AD integration with BenefitHub, you need the following items:</span></span>

- <span data-ttu-id="56c2e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56c2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56c2e-113">Sottoscrizione di BenefitHub abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="56c2e-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56c2e-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="56c2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56c2e-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="56c2e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56c2e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="56c2e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56c2e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56c2e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56c2e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="56c2e-118">Scenario description</span></span>
<span data-ttu-id="56c2e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="56c2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56c2e-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="56c2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56c2e-121">Aggiunta di BenefitHub dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="56c2e-121">Adding BenefitHub from the gallery</span></span>
2. <span data-ttu-id="56c2e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56c2e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-the-gallery"></a><span data-ttu-id="56c2e-123">Aggiunta di BenefitHub dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="56c2e-123">Adding BenefitHub from the gallery</span></span>
<span data-ttu-id="56c2e-124">Per configurare l'integrazione di BenefitHub in Azure AD, è necessario aggiungere BenefitHub dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="56c2e-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56c2e-125">**Per aggiungere BenefitHub dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="56c2e-125">**To add BenefitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56c2e-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="56c2e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="56c2e-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="56c2e-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="56c2e-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="56c2e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="56c2e-133">Nella casella di ricerca digitare **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-133">In the search box, type **BenefitHub**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="56c2e-135">Nel pannello dei risultati selezionare **BenefitHub** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="56c2e-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56c2e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56c2e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56c2e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BenefitHub usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="56c2e-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="56c2e-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di BenefitHub corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56c2e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span></span> <span data-ttu-id="56c2e-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="56c2e-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span></span>

<span data-ttu-id="56c2e-141">Per stabilire la relazione di collegamento, in BenefitHub assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="56c2e-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="56c2e-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con BenefitHub, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="56c2e-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56c2e-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="56c2e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="56c2e-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56c2e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56c2e-145">**[Creazione di un utente di test di BenefitHub](#creating-a-benefithub-test-user)**: per avere una controparte di Britta Simon in BenefitHub collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56c2e-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="56c2e-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56c2e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56c2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="56c2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56c2e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56c2e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56c2e-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="56c2e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="56c2e-150">**Per configurare l'accesso Single Sign-On di Azure AD con BenefitHub, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="56c2e-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="56c2e-151">Nella pagina di integrazione dell'applicazione **BenefitHub** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="56c2e-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="56c2e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="56c2e-155">Nella sezione **URL e dominio BenefitHub** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="56c2e-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="56c2e-157">a.</span><span class="sxs-lookup"><span data-stu-id="56c2e-157">a.</span></span> <span data-ttu-id="56c2e-158">Nella casella di testo **Identificatore** digitare `urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="56c2e-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="56c2e-159">b.</span><span class="sxs-lookup"><span data-stu-id="56c2e-159">b.</span></span> <span data-ttu-id="56c2e-160">Nella casella di testo **URL di risposta** digitare: `https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="56c2e-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="56c2e-161">L'applicazione BenefitHub prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="56c2e-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="56c2e-162">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="56c2e-162">Configure the following claims for this application.</span></span> <span data-ttu-id="56c2e-163">È possibile gestire i valori di questi attributi dalla sezione "**Attributi utente**" nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="56c2e-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="56c2e-165">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente ed eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="56c2e-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="56c2e-166">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="56c2e-166">Attribute Name</span></span> | <span data-ttu-id="56c2e-167">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="56c2e-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="56c2e-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="56c2e-168">organizationid</span></span> | <span data-ttu-id="56c2e-169">< id organizzazione ></span><span class="sxs-lookup"><span data-stu-id="56c2e-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="56c2e-170">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="56c2e-170">This attribute value is not real.</span></span> <span data-ttu-id="56c2e-171">è necessario aggiornare questo valore con l'ID organizzazione effettivo.</span><span class="sxs-lookup"><span data-stu-id="56c2e-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="56c2e-172">Per ottenere l'ID organizzazione effettivo, contattare il [team di supporto di BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="56c2e-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span></span>
    
    <span data-ttu-id="56c2e-173">a.</span><span class="sxs-lookup"><span data-stu-id="56c2e-173">a.</span></span> <span data-ttu-id="56c2e-174">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="56c2e-177">b.</span><span class="sxs-lookup"><span data-stu-id="56c2e-177">b.</span></span> <span data-ttu-id="56c2e-178">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="56c2e-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="56c2e-179">c.</span><span class="sxs-lookup"><span data-stu-id="56c2e-179">c.</span></span> <span data-ttu-id="56c2e-180">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="56c2e-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="56c2e-181">d.</span><span class="sxs-lookup"><span data-stu-id="56c2e-181">d.</span></span> <span data-ttu-id="56c2e-182">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56c2e-183">Prima di configurare l'asserzione SAML, è necessario contattare il [team di supporto di BenefitHub](https://www.benefithub.com/Home/ContactUs) e richiedere il valore dell'attributo dell'identificatore univoco per il tenant.</span><span class="sxs-lookup"><span data-stu-id="56c2e-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="56c2e-184">Questo valore è necessario per configurare l'attestazione personalizzata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="56c2e-184">You need this value to configure the custom claim for your application.</span></span>

6. <span data-ttu-id="56c2e-185">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="56c2e-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="56c2e-187">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="56c2e-187">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="56c2e-189">Per configurare l'accesso Single Sign-On sul lato **BenefitHub**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="56c2e-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="56c2e-190">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="56c2e-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="56c2e-191">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="56c2e-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="56c2e-192">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="56c2e-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="56c2e-193">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56c2e-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56c2e-194">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56c2e-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="56c2e-195">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56c2e-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="56c2e-197">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="56c2e-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56c2e-198">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="56c2e-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56c2e-200">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="56c2e-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56c2e-202">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56c2e-204">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="56c2e-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56c2e-206">a.</span><span class="sxs-lookup"><span data-stu-id="56c2e-206">a.</span></span> <span data-ttu-id="56c2e-207">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56c2e-208">b.</span><span class="sxs-lookup"><span data-stu-id="56c2e-208">b.</span></span> <span data-ttu-id="56c2e-209">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56c2e-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56c2e-210">c.</span><span class="sxs-lookup"><span data-stu-id="56c2e-210">c.</span></span> <span data-ttu-id="56c2e-211">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="56c2e-212">d.</span><span class="sxs-lookup"><span data-stu-id="56c2e-212">d.</span></span> <span data-ttu-id="56c2e-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="56c2e-214">Creazione di un utente di test di BenefitHub</span><span class="sxs-lookup"><span data-stu-id="56c2e-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="56c2e-215">In questa sezione viene creato un utente di nome Britta Simon in BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="56c2e-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="56c2e-216">Collaborare con il [team di supporto di BenefitHub](https://www.benefithub.com/Home/ContactUs) per aggiungere gli utenti alla piattaforma BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="56c2e-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span></span> <span data-ttu-id="56c2e-217">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="56c2e-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="56c2e-218">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56c2e-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="56c2e-219">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="56c2e-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span></span>

![Assegna utente][200] 

<span data-ttu-id="56c2e-221">**Per assegnare Britta Simon a BenefitHub, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="56c2e-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="56c2e-222">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="56c2e-224">Nell'elenco delle applicazioni selezionare **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-224">In the applications list, select **BenefitHub**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="56c2e-226">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="56c2e-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="56c2e-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-228">Click **Add** button.</span></span> <span data-ttu-id="56c2e-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="56c2e-231">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="56c2e-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="56c2e-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56c2e-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="56c2e-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56c2e-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="56c2e-234">Testing single sign-on</span></span>

<span data-ttu-id="56c2e-235">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="56c2e-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="56c2e-236">Quando si fa clic sul riquadro BenefitHub nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="56c2e-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span></span>
<span data-ttu-id="56c2e-237">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="56c2e-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56c2e-238">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="56c2e-238">Additional resources</span></span>

* [<span data-ttu-id="56c2e-239">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56c2e-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56c2e-240">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56c2e-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

