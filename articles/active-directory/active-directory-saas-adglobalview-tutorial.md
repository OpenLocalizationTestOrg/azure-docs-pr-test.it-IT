---
title: 'Esercitazione: Integrazione di Azure Active Directory con ADP Globalview | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ADP Globalview.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: e9a5e65c484dfb98d1a7bc63d55f6ef92039554b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="21454-103">Esercitazione: Integrazione di Azure Active Directory con ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="21454-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="21454-104">Questa esercitazione descrive come integrare ADP Globalview con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="21454-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21454-105">L'integrazione di ADP Globalview con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="21454-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="21454-106">È possibile controllare in Azure AD chi può accedere ad ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="21454-106">You can control in Azure AD who has access to ADP Globalview</span></span>
- <span data-ttu-id="21454-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On ad ADP Globalview con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="21454-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="21454-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="21454-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="21454-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="21454-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21454-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="21454-110">Prerequisites</span></span>

<span data-ttu-id="21454-111">Per configurare l'integrazione di Azure AD con ADP Globalview sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="21454-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span></span>

- <span data-ttu-id="21454-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21454-112">An Azure AD subscription</span></span>
- <span data-ttu-id="21454-113">Sottoscrizione di ADP Globalview abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="21454-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="21454-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="21454-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="21454-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="21454-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="21454-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="21454-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="21454-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="21454-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21454-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="21454-118">Scenario description</span></span>
<span data-ttu-id="21454-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="21454-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="21454-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="21454-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="21454-121">Aggiunta di ADP Globalview dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="21454-121">Adding ADP Globalview from the gallery</span></span>
2. <span data-ttu-id="21454-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="21454-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-the-gallery"></a><span data-ttu-id="21454-123">Aggiunta di ADP Globalview dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="21454-123">Adding ADP Globalview from the gallery</span></span>
<span data-ttu-id="21454-124">Per configurare l'integrazione di ADP Globalview in Azure AD è necessario aggiungere ADP Globalview dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="21454-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="21454-125">**Per aggiungere ADP Globalview dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="21454-125">**To add ADP Globalview from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="21454-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="21454-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="21454-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="21454-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="21454-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="21454-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="21454-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="21454-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="21454-133">Nella casella di ricerca digitare **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="21454-133">In the search box, type **ADP Globalview**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="21454-135">Nel pannello dei risultati selezionare **ADP Globalview** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="21454-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="21454-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="21454-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="21454-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ADP Globalview mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="21454-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="21454-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di ADP Globalview corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21454-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span></span> <span data-ttu-id="21454-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="21454-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span></span>

<span data-ttu-id="21454-141">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="21454-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span></span>

<span data-ttu-id="21454-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con ADP Globalview è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="21454-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="21454-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="21454-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="21454-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21454-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21454-145">**[Creazione di un utente test di ADP Globalview](#creating-an-adp-globalview-test-user)**: per avere una controparte di Britta Simon in ADP Globalview collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21454-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="21454-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21454-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21454-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="21454-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="21454-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="21454-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="21454-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="21454-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="21454-150">**Per configurare l'accesso Single Sign-On di Azure AD con ADP Globalview, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="21454-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="21454-151">Nella pagina di integrazione dell'applicazione **ADP Globalview** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="21454-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="21454-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="21454-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="21454-155">Nella sezione **URL e dominio ADP Globalview** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="21454-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="21454-157">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente: `https://<subdomain>.globalview.adp.com/federate` o `https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="21454-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="21454-158">Il valore non è reale.</span><span class="sxs-lookup"><span data-stu-id="21454-158">The value is not real.</span></span> <span data-ttu-id="21454-159">È necessario aggiornare questo valore con l'ID effettivo.</span><span class="sxs-lookup"><span data-stu-id="21454-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="21454-160">Per ottenere il valore contattare il [supporto ADP Globalview](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="21454-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span></span>
 
4. <span data-ttu-id="21454-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="21454-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="21454-163">Dato che l'applicazione ADP Globalview prevede un formato specifico per le asserzioni SAML, è necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="21454-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="21454-164">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="21454-164">The following screenshot shows an example for it.</span></span> <span data-ttu-id="21454-165">Il nome dell'attestazione sarà sempre **"PersonImmutableID"** e il valore di cui è stato eseguito il mapping a ExtensionAttribute2, che contiene il valore EmployeeID dell'utente.</span><span class="sxs-lookup"><span data-stu-id="21454-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="21454-166">In questo caso il mapping degli utenti da Azure AD ad ADP Globalview viene eseguito su EmployeeID, ma è possibile eseguirlo su un valore diverso anche in base alle impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="21454-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="21454-167">È possibile collaborare prima di tutto con il team di ADP GlobalView per usare l'identificatore corretto di un utente ed eseguire il mapping di tale valore all'attestazione **"PersonImmutableID"**.</span><span class="sxs-lookup"><span data-stu-id="21454-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="21454-168">È anche possibile mappare l'attestazione di posta elettronica e ID utente come illustrato nell'immagine.</span><span class="sxs-lookup"><span data-stu-id="21454-168">You can also map the Email and UserID claim as shown in the picture.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="21454-170">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come illustrato nell'immagine e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="21454-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="21454-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="21454-171">Attribute Name</span></span> | <span data-ttu-id="21454-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="21454-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="21454-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="21454-173">personalimmutableid</span></span> | <span data-ttu-id="21454-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="21454-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="21454-175">email</span><span class="sxs-lookup"><span data-stu-id="21454-175">email</span></span>               | <span data-ttu-id="21454-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="21454-176">user.mail</span></span> |
    | <span data-ttu-id="21454-177">userid</span><span class="sxs-lookup"><span data-stu-id="21454-177">userid</span></span>              | <span data-ttu-id="21454-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="21454-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="21454-179">a.</span><span class="sxs-lookup"><span data-stu-id="21454-179">a.</span></span> <span data-ttu-id="21454-180">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="21454-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="21454-183">b.</span><span class="sxs-lookup"><span data-stu-id="21454-183">b.</span></span> <span data-ttu-id="21454-184">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="21454-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="21454-185">c.</span><span class="sxs-lookup"><span data-stu-id="21454-185">c.</span></span> <span data-ttu-id="21454-186">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="21454-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="21454-187">d.</span><span class="sxs-lookup"><span data-stu-id="21454-187">d.</span></span> <span data-ttu-id="21454-188">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="21454-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="21454-189">Prima di poter configurare l'asserzione SAML è necessario contattare il [team di supporto di ADP Globalview](https://www.adp.com/contact-us/overview.aspx) e richiedere il valore dell'attributo dell'identificatore univoco per il tenant.</span><span class="sxs-lookup"><span data-stu-id="21454-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="21454-190">Questo valore è necessario per configurare l'attestazione personalizzata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="21454-190">You need this value to configure the custom claim for your application.</span></span> 

8. <span data-ttu-id="21454-191">Nella sezione **Configurazione di ADP Globalview** fare clic su **Configura ADP Globalview** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="21454-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span></span> <span data-ttu-id="21454-192">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="21454-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="21454-194">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="21454-194">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="21454-196">Per configurare l'accesso Single Sign-On sul lato **ADP Globalview** è necessario inviare il file **Certificato (Base64)** scaricato e i valori **Sign-Out URL (URL di disconnessione), SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** al [supporto ADP Globalview](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="21454-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="21454-197">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="21454-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="21454-198">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="21454-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="21454-199">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="21454-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="21454-200">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="21454-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="21454-201">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="21454-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="21454-203">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="21454-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="21454-204">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="21454-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="21454-206">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="21454-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="21454-208">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="21454-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="21454-210">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="21454-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="21454-212">a.</span><span class="sxs-lookup"><span data-stu-id="21454-212">a.</span></span> <span data-ttu-id="21454-213">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="21454-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="21454-214">b.</span><span class="sxs-lookup"><span data-stu-id="21454-214">b.</span></span> <span data-ttu-id="21454-215">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="21454-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="21454-216">c.</span><span class="sxs-lookup"><span data-stu-id="21454-216">c.</span></span> <span data-ttu-id="21454-217">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="21454-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="21454-218">d.</span><span class="sxs-lookup"><span data-stu-id="21454-218">d.</span></span> <span data-ttu-id="21454-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="21454-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="21454-220">Creazione di un utente test di ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="21454-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="21454-221">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="21454-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="21454-222">Collaborare con il [team di supporto di ADP Globalview](https://www.adp.com/contact-us/overview.aspx) per aggiungere gli utenti nell'account ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="21454-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="21454-223">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="21454-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="21454-224">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="21454-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span></span>

![Assegna utente][200] 

<span data-ttu-id="21454-226">**Per assegnare Britta Simon ad ADP Globalview, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="21454-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="21454-227">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="21454-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="21454-229">Nell'elenco delle applicazioni selezionare **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="21454-229">In the applications list, select **ADP Globalview**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="21454-231">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="21454-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="21454-233">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="21454-233">Click **Add** button.</span></span> <span data-ttu-id="21454-234">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="21454-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="21454-236">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="21454-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="21454-237">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="21454-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21454-238">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="21454-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="21454-239">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="21454-239">Testing single sign-on</span></span>

<span data-ttu-id="21454-240">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="21454-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="21454-241">Quando si fa clic sul riquadro ADP GlobalView nel pannello di accesso, si accede automaticamente all'applicazione ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="21454-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="21454-242">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="21454-242">Additional resources</span></span>

* [<span data-ttu-id="21454-243">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21454-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21454-244">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21454-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

