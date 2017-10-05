---
title: 'Esercitazione: Integrazione di Azure Active Directory con CloudPassage | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e CloudPassage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 094740e20570665e975dec1a591989e411f90c16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="8f0f9-103">Esercitazione: Integrazione di Azure Active Directory con CloudPassage</span><span class="sxs-lookup"><span data-stu-id="8f0f9-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="8f0f9-104">Questa esercitazione descrive come integrare CloudPassage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f0f9-105">L'integrazione di CloudPassage con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8f0f9-106">È possibile controllare in Azure AD chi può accedere a CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="8f0f9-107">È possibile abilitare gli utenti per l'accesso automatico a CloudPassage (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f0f9-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8f0f9-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f0f9-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8f0f9-110">Prerequisites</span></span>

<span data-ttu-id="8f0f9-111">Per configurare l'integrazione di Azure AD con CloudPassage, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="8f0f9-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f0f9-113">Sottoscrizione di CloudPassage abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8f0f9-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f0f9-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f0f9-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f0f9-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f0f9-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f0f9-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8f0f9-118">Scenario description</span></span>
<span data-ttu-id="8f0f9-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f0f9-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f0f9-121">Aggiunta di CloudPassage dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8f0f9-121">Adding CloudPassage from the gallery</span></span>
2. <span data-ttu-id="8f0f9-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="8f0f9-123">Aggiunta di CloudPassage dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8f0f9-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="8f0f9-124">Per configurare l'integrazione di CloudPassage in Azure AD, è necessario aggiungere CloudPassage dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8f0f9-125">**Per aggiungere CloudPassage dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8f0f9-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8f0f9-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f0f9-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8f0f9-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8f0f9-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8f0f9-133">Nella casella di ricerca digitare **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-133">In the search box, type **CloudPassage**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="8f0f9-135">Nel pannello dei risultati selezionare **CloudPassage** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f0f9-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f0f9-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con CloudPassage mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8f0f9-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8f0f9-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di CloudPassage corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="8f0f9-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="8f0f9-141">Per stabilire la relazione di collegamento, in CloudPassage assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8f0f9-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con CloudPassage, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8f0f9-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8f0f9-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f0f9-145">**[Creazione di un utente test di CloudPassage](#creating-a-cloudpassage-test-user)**: per avere una controparte di Britta Simon in CloudPassage collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f0f9-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f0f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f0f9-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f0f9-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel nuovo portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="8f0f9-150">**Per configurare Single Sign-On di Azure AD con CloudPassage, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8f0f9-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="8f0f9-151">Nella pagina di integrazione dell'applicazione **CloudPassage** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8f0f9-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="8f0f9-155">Nella sezione **URL e dominio CloudPassage** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="8f0f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-157">a.</span></span> <span data-ttu-id="8f0f9-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://portal.cloudpassage.com/saml/init/accountid`.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="8f0f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-159">b.</span></span> <span data-ttu-id="8f0f9-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="8f0f9-161">È possibile ottenere il valore di questo attributo facendo clic su **SSO Setup documentation** (Documentazione della configurazione SSO) nella sezione **Single Sign-on Settings** (Impostazioni Single Sign-On) del portale di CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="8f0f9-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="8f0f9-163">These values are not real.</span></span> <span data-ttu-id="8f0f9-164">è necessario aggiornarli con l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="8f0f9-165">Per ottenere questi valori contattare il [team di supporto clienti di CloudPassage](https://www.cloudpassage.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="8f0f9-166">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="8f0f9-168">L'applicazione CloudPassage prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="8f0f9-169">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-169">The following screenshot shows an example for this.</span></span>
   
   ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="8f0f9-171">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="8f0f9-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="8f0f9-172">Attribute Name</span></span> | <span data-ttu-id="8f0f9-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="8f0f9-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="8f0f9-174">firstname</span><span class="sxs-lookup"><span data-stu-id="8f0f9-174">firstname</span></span> |<span data-ttu-id="8f0f9-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8f0f9-175">user.givenname</span></span> |
    | <span data-ttu-id="8f0f9-176">lastname</span><span class="sxs-lookup"><span data-stu-id="8f0f9-176">lastname</span></span> |<span data-ttu-id="8f0f9-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="8f0f9-177">user.surname</span></span> |
    | <span data-ttu-id="8f0f9-178">email</span><span class="sxs-lookup"><span data-stu-id="8f0f9-178">email</span></span> |<span data-ttu-id="8f0f9-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="8f0f9-179">user.mail</span></span> |
    
    <span data-ttu-id="8f0f9-180">a.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-180">a.</span></span> <span data-ttu-id="8f0f9-181">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="8f0f9-184">b.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-184">b.</span></span> <span data-ttu-id="8f0f9-185">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="8f0f9-186">c.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-186">c.</span></span> <span data-ttu-id="8f0f9-187">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8f0f9-188">d.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-188">d.</span></span> <span data-ttu-id="8f0f9-189">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-189">Click **Ok**.</span></span>

7. <span data-ttu-id="8f0f9-190">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8f0f9-190">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="8f0f9-192">Nella sezione **Configurazione di CloudPassage** fare clic su **Configura CloudPassage** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8f0f9-193">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="8f0f9-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="8f0f9-195">In un'altra finestra del Web browser accedere al sito aziendale di CloudPassage come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="8f0f9-196">Nel menu in alto fare clic su **Settings** (Impostazioni) e quindi su **Site Administration** (Amministrazione sito).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Configura accesso Single Sign-On][12]

11. <span data-ttu-id="8f0f9-198">Fare clic sulla scheda **Authentication Settings** (Impostazioni autenticazione).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![Configura accesso Single Sign-On][13]

12. <span data-ttu-id="8f0f9-200">Nella sezione **Single Sign-On Settings** (Impostazioni Single Sign-On) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Configura accesso Single Sign-On][14]

    <span data-ttu-id="8f0f9-202">a.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-202">a.</span></span> <span data-ttu-id="8f0f9-203">Selezionare la casella di controllo **Enable Single sign-on(SSO)(SSO Setup Documentation)** (Abilita Single Sign-On (SSO) (Documentazione di configurazione di SSO).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="8f0f9-204">b.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-204">b.</span></span> <span data-ttu-id="8f0f9-205">Incollare **SAML Entity ID** (ID entità SAML) nella casella di testo **SAML issuer URL** (URL autorità di certificazione SAML).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="8f0f9-206">c.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-206">c.</span></span> <span data-ttu-id="8f0f9-207">Incollare **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) nella casella di testo **SAML endpoint URL** (URL endpoint SAML).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="8f0f9-208">d.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-208">d.</span></span> <span data-ttu-id="8f0f9-209">Incollare **Sign-Out URL** (URL di disconnessione) nella casella di testo **Logout landing page** (Pagina di destinazione disconnessione).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="8f0f9-210">e.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-210">e.</span></span> <span data-ttu-id="8f0f9-211">Aprire il certificato scaricato nel Blocco note, copiare il contenuto del certificato negli Appunti e quindi incollarlo nella casella di testo **Certificato X.509**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="8f0f9-212">f.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-212">f.</span></span> <span data-ttu-id="8f0f9-213">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8f0f9-214">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8f0f9-215">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8f0f9-216">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f0f9-217">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0f9-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f0f9-218">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8f0f9-220">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8f0f9-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8f0f9-221">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f0f9-223">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f0f9-225">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f0f9-227">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f0f9-229">a.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-229">a.</span></span> <span data-ttu-id="8f0f9-230">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f0f9-231">b.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-231">b.</span></span> <span data-ttu-id="8f0f9-232">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f0f9-233">c.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-233">c.</span></span> <span data-ttu-id="8f0f9-234">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8f0f9-235">d.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-235">d.</span></span> <span data-ttu-id="8f0f9-236">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="8f0f9-237">Creazione di un utente test CloudPassage</span><span class="sxs-lookup"><span data-stu-id="8f0f9-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="8f0f9-238">Questa sezione descrive come creare un utente chiamato Britta Simon in CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="8f0f9-239">**Per creare un utente test denominato Britta Simon in CloudPassage, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8f0f9-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="8f0f9-240">Accedere al sito aziendale di **CloudPassage** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="8f0f9-241">Nella barra degli strumenti in alto fare clic su **Settings** (Impostazioni) e quindi su **Site Administration** (Amministrazione sito).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Creazione di un utente test CloudPassage][22] 

3. <span data-ttu-id="8f0f9-243">Fare clic sulla scheda **Users** (Utenti) e quindi fare clic su **Add New User** (Aggiungi nuovo utente).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Creazione di un utente test CloudPassage][23]

4. <span data-ttu-id="8f0f9-245">Nella sezione **Aggiungi nuovo utente** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8f0f9-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![Creazione di un utente test CloudPassage][24]
    
    <span data-ttu-id="8f0f9-247">a.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-247">a.</span></span> <span data-ttu-id="8f0f9-248">Nella casella di testo **Nome** digitare Britta.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="8f0f9-249">b.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-249">b.</span></span> <span data-ttu-id="8f0f9-250">Nella casella di testo **Cognome** digitare Simon.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="8f0f9-251">c.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-251">c.</span></span> <span data-ttu-id="8f0f9-252">Nelle caselle di testo **Username** (Nome utente), **Email** (Indirizzo di posta elettronica) e **Retype Email** (Digitare nuovamente l'indirizzo di posta elettronica) digitare il nome utente di Britta in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="8f0f9-253">d.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-253">d.</span></span> <span data-ttu-id="8f0f9-254">In **Access Type** (Tipo di accesso) selezionare **Enable Halo Portal Access** (Abilita accesso portale Halo).</span><span class="sxs-lookup"><span data-stu-id="8f0f9-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="8f0f9-255">e.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-255">e.</span></span> <span data-ttu-id="8f0f9-256">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8f0f9-257">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0f9-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8f0f9-258">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8f0f9-260">**Per assegnare Britta Simon ad Amazon Web Service (AWS), seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8f0f9-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="8f0f9-261">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8f0f9-263">Nell'elenco delle applicazioni selezionare **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-263">In the applications list, select **CloudPassage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="8f0f9-265">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8f0f9-267">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-267">Click **Add** button.</span></span> <span data-ttu-id="8f0f9-268">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8f0f9-270">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8f0f9-271">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f0f9-272">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f0f9-273">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8f0f9-273">Testing single sign-on</span></span>

<span data-ttu-id="8f0f9-274">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8f0f9-275">Quando si fa clic sul riquadro CloudPassage nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="8f0f9-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f0f9-276">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8f0f9-276">Additional resources</span></span>

* [<span data-ttu-id="8f0f9-277">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f0f9-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f0f9-278">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f0f9-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

