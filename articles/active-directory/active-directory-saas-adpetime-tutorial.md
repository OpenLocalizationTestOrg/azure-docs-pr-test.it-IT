---
title: 'Esercitazione: Integrazione di Azure Active Directory con ADP eTime | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ADP eTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 31fed307a32e629d00aab7cc9d5167ee16d83936
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="7154e-103">Esercitazione: Integrazione di Azure Active Directory con ADP eTime</span><span class="sxs-lookup"><span data-stu-id="7154e-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="7154e-104">Questa esercitazione descrive come integrare ADP eTime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7154e-104">In this tutorial, you learn how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7154e-105">L'integrazione di ADP eTime con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7154e-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7154e-106">È possibile controllare in Azure AD chi può accedere ad ADP eTime</span><span class="sxs-lookup"><span data-stu-id="7154e-106">You can control in Azure AD who has access to ADP eTime</span></span>
- <span data-ttu-id="7154e-107">È possibile abilitare gli utenti per l'accesso automatico ad ADP eTime (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7154e-107">You can enable your users to automatically get signed-on to ADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7154e-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7154e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7154e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7154e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7154e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7154e-110">Prerequisites</span></span>

<span data-ttu-id="7154e-111">Per configurare l'integrazione di Azure AD con ADP eTime, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7154e-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

- <span data-ttu-id="7154e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7154e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7154e-113">Sottoscrizione di ADP eTime abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7154e-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7154e-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7154e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7154e-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7154e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7154e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7154e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7154e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7154e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7154e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7154e-118">Scenario description</span></span>
<span data-ttu-id="7154e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7154e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7154e-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7154e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7154e-121">Aggiunta di ADP eTime dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7154e-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="7154e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7154e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-the-gallery"></a><span data-ttu-id="7154e-123">Aggiunta di ADP eTime dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7154e-123">Adding ADP eTime from the gallery</span></span>
<span data-ttu-id="7154e-124">Per configurare l'integrazione di ADP eTime in Azure AD, è necessario aggiungere ADP eTime dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7154e-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7154e-125">**Per aggiungere ADP eTime dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7154e-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7154e-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7154e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7154e-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7154e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7154e-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7154e-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7154e-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="7154e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7154e-133">Nella casella di ricerca digitare **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="7154e-133">In the search box, type **ADP eTime**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="7154e-135">Nel pannello dei risultati selezionare **ADP eTime** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7154e-135">In the results panel, select **ADP eTime**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7154e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7154e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7154e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ADP eTime in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7154e-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7154e-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di ADP eTime che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7154e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP eTime is to a user in Azure AD.</span></span> <span data-ttu-id="7154e-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="7154e-140">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>

<span data-ttu-id="7154e-141">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="7154e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="7154e-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con ADP eTime, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7154e-142">To configure and test Azure AD single sign-on with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7154e-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7154e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7154e-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7154e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7154e-145">**[Creazione di un utente di test di ADP eTime](#creating-an-adp-etime-test-user)** : per avere una controparte di Britta Simon in ADP eTime collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7154e-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7154e-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7154e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7154e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="7154e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7154e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7154e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7154e-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="7154e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="7154e-150">**Per configurare Single Sign-On di Azure AD con ADP eTime, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7154e-150">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="7154e-151">Nella pagina di integrazione dell'applicazione **ADP eTime** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7154e-151">In the Azure portal, on the **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7154e-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7154e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="7154e-155">Nella sezione **URL e dominio ADP eTime** eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="7154e-155">On the **ADP eTime Domain and URLs** section, perform the following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="7154e-157">a.</span><span class="sxs-lookup"><span data-stu-id="7154e-157">a.</span></span> <span data-ttu-id="7154e-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="7154e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="7154e-159">b.</span><span class="sxs-lookup"><span data-stu-id="7154e-159">b.</span></span> <span data-ttu-id="7154e-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="7154e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="7154e-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="7154e-161">These values are not the real.</span></span> <span data-ttu-id="7154e-162">è necessario aggiornarli con l'URL di risposta e l'identificatore effettivi.</span><span class="sxs-lookup"><span data-stu-id="7154e-162">Update these values with the actual Reply URL and Identifier.</span></span> <span data-ttu-id="7154e-163">Per ottenere questi valori, contattare il [team di supporto di ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="7154e-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to get these values.</span></span>

4. <span data-ttu-id="7154e-164">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="7154e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="7154e-166">L'applicazione ADP eTime prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="7154e-166">The ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="7154e-167">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="7154e-167">The following screenshot shows an example for this.</span></span> <span data-ttu-id="7154e-168">Il nome dell'attestazione sarà sempre **"PersonImmutableID"** e il valore di cui è stato eseguito il mapping a ExtensionAttribute2, che contiene il valore EmployeeID dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7154e-168">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

    <span data-ttu-id="7154e-169">Il mapping degli utenti da Azure AD ad ADP eTime verrà eseguito in EmployeeID, ma è possibile eseguire il mapping a un valore diverso, anche in base alle impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7154e-169">Here the user mapping from Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="7154e-170">Collaborare quindi prima di tutto con il [team di supporto di ADP eTime](https://www.adp.com/contact-us/overview.aspx) per usare l'identificatore corretto di un utente ed eseguire il mapping di tale valore all'attestazione **"PersonImmutableID"**.</span><span class="sxs-lookup"><span data-stu-id="7154e-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="7154e-172">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come illustrato nell'immagine e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7154e-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="7154e-173">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="7154e-173">Attribute Name</span></span> | <span data-ttu-id="7154e-174">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="7154e-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="7154e-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="7154e-175">PersonImmutableID</span></span> | <span data-ttu-id="7154e-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="7154e-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="7154e-177">a.</span><span class="sxs-lookup"><span data-stu-id="7154e-177">a.</span></span> <span data-ttu-id="7154e-178">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="7154e-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7154e-181">b.</span><span class="sxs-lookup"><span data-stu-id="7154e-181">b.</span></span> <span data-ttu-id="7154e-182">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="7154e-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="7154e-183">c.</span><span class="sxs-lookup"><span data-stu-id="7154e-183">c.</span></span> <span data-ttu-id="7154e-184">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="7154e-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7154e-185">d.</span><span class="sxs-lookup"><span data-stu-id="7154e-185">d.</span></span> <span data-ttu-id="7154e-186">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7154e-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7154e-187">Prima di poter configurare l'asserzione SAML, è necessario contattare il [team di supporto di ADP eTime](https://www.adp.com/contact-us/overview.aspx) e richiedere il valore dell'attributo dell'identificatore univoco per il tenant.</span><span class="sxs-lookup"><span data-stu-id="7154e-187">Before you can configure the SAML assertion, you need to contact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="7154e-188">Questo valore è necessario per configurare l'attestazione personalizzata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7154e-188">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="7154e-189">Nella sezione **Configurazione di ADP eTime** fare clic su **Configura ADP eTime** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="7154e-189">On the **ADP eTime Configuration** section, click **Configure ADP eTime** to open **Configure sign-on** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="7154e-191">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7154e-191">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="7154e-193">Per configurare l'accesso Single Sign-On sul lato **ADP eTime**, è necessario inviare il file di **XML metadati** scaricato al [team di supporto di ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="7154e-193">To configure single sign-on on **ADP eTime** side, you need to send the downloaded **Metadata XML** to [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="7154e-194">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="7154e-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7154e-195">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="7154e-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7154e-196">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7154e-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7154e-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7154e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="7154e-198">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7154e-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7154e-200">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7154e-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7154e-201">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7154e-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7154e-203">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="7154e-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7154e-205">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="7154e-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7154e-207">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7154e-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7154e-209">a.</span><span class="sxs-lookup"><span data-stu-id="7154e-209">a.</span></span> <span data-ttu-id="7154e-210">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7154e-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7154e-211">b.</span><span class="sxs-lookup"><span data-stu-id="7154e-211">b.</span></span> <span data-ttu-id="7154e-212">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7154e-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7154e-213">c.</span><span class="sxs-lookup"><span data-stu-id="7154e-213">c.</span></span> <span data-ttu-id="7154e-214">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="7154e-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7154e-215">d.</span><span class="sxs-lookup"><span data-stu-id="7154e-215">d.</span></span> <span data-ttu-id="7154e-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7154e-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="7154e-217">Creazione di un utente di test di ADP eTime</span><span class="sxs-lookup"><span data-stu-id="7154e-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="7154e-218">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="7154e-218">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="7154e-219">Collaborare con il [team di supporto di ADP eTime](https://www.adp.com/contact-us/overview.aspx) per aggiungere gli utenti nell'account ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="7154e-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP eTime account.</span></span> 
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7154e-220">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7154e-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7154e-221">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="7154e-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP eTime.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7154e-223">**Per assegnare Britta Simon ad ADP eTime, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7154e-223">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="7154e-224">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7154e-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7154e-226">Nell'elenco di applicazioni selezionare **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="7154e-226">In the applications list, select **ADP eTime**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="7154e-228">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7154e-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7154e-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7154e-230">Click **Add** button.</span></span> <span data-ttu-id="7154e-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7154e-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7154e-233">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="7154e-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7154e-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7154e-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7154e-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7154e-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7154e-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7154e-236">Testing single sign-on</span></span>

<span data-ttu-id="7154e-237">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7154e-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7154e-238">Quando si fa clic sul riquadro ADP eTime nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="7154e-238">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>
<span data-ttu-id="7154e-239">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7154e-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7154e-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7154e-240">Additional resources</span></span>

* [<span data-ttu-id="7154e-241">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7154e-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7154e-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7154e-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

