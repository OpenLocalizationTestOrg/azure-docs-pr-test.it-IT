---
title: 'Esercitazione: Integrazione di Azure Active Directory con Blackboard Learn | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Blackboard Learn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="d783a-103">Esercitazione: Integrazione di Azure Active Directory con Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="d783a-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="d783a-104">Questa esercitazione descrive come integrare Blackboard Learn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d783a-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d783a-105">L'integrazione di Blackboard Learn con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d783a-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d783a-106">È possibile controllare in Azure AD chi può accedere a Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="d783a-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="d783a-107">È possibile abilitare gli utenti per l'accesso automatico a Blackboard Learn (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d783a-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d783a-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d783a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d783a-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d783a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d783a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d783a-110">Prerequisites</span></span>

<span data-ttu-id="d783a-111">Per configurare l'integrazione di Azure AD con Blackboard Learn, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d783a-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="d783a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d783a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d783a-113">Sottoscrizione di Blackboard Learn abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d783a-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d783a-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d783a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d783a-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d783a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d783a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d783a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d783a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d783a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d783a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d783a-118">Scenario description</span></span>
<span data-ttu-id="d783a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d783a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d783a-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d783a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d783a-121">Aggiunta di Blackboard Learn dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d783a-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="d783a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d783a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="d783a-123">Aggiunta di Blackboard Learn dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d783a-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="d783a-124">Per configurare l'integrazione di Blackboard Learn in Azure AD, è necessario aggiungere Blackboard Learn dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d783a-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d783a-125">**Per aggiungere Blackboard Learn dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d783a-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d783a-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d783a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d783a-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d783a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d783a-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d783a-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d783a-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d783a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d783a-133">Nella casella di ricerca digitare **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="d783a-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="d783a-135">Nel pannello dei risultati selezionare **Blackboard Learn** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d783a-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d783a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d783a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d783a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Blackboard Learn usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d783a-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d783a-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Blackboard Learn che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d783a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="d783a-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="d783a-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="d783a-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (nome utente) in Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="d783a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="d783a-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Blackboard Learn, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d783a-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d783a-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d783a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d783a-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d783a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d783a-145">**[Creazione di un utente di test di Blackboard Learn](#creating-a-blackboard-learn-test-user)**: per avere una controparte di Britta Simon in Blackboard Learn collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d783a-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d783a-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d783a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d783a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d783a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d783a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d783a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d783a-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="d783a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="d783a-150">**Per configurare Single Sign-On di Azure AD con Blackboard Learn, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d783a-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="d783a-151">Nella pagina di integrazione dell'applicazione **Blackboard Learn** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d783a-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d783a-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d783a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="d783a-155">Nella sezione **URL e dominio Blackboard Learn** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d783a-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="d783a-157">a.</span><span class="sxs-lookup"><span data-stu-id="d783a-157">a.</span></span> <span data-ttu-id="d783a-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.blackboard.com/`.</span><span class="sxs-lookup"><span data-stu-id="d783a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="d783a-159">b.</span><span class="sxs-lookup"><span data-stu-id="d783a-159">b.</span></span> <span data-ttu-id="d783a-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="d783a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="d783a-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d783a-161">These values are not real.</span></span> <span data-ttu-id="d783a-162">è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="d783a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d783a-163">Per ottenere questi valori, contattare il [team di supporto clienti di Blackboard Learn](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="d783a-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="d783a-164">L'applicazione Blackboard Learn si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="d783a-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d783a-165">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="d783a-165">Configure the following claims for this application.</span></span> <span data-ttu-id="d783a-166">È possibile gestire i valori di questi attributi dalla sezione **Attributi utente** nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d783a-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="d783a-167">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="d783a-167">The following screenshot shows an example about it.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="d783a-169">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare gli attributi del token SAML come illustrato nell'immagine e seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="d783a-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="d783a-170">In questo caso è stato eseguito il mapping di Userprincipalname come attributo univoco dell'utente ma è possibile eseguirne il mapping al valore appropriato che distingue in modo univoco l'utente nell'organizzazione, a sua volta mappato al campo del nome utente di Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="d783a-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="d783a-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="d783a-171">Attribute Name</span></span> | <span data-ttu-id="d783a-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="d783a-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="d783a-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="d783a-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="d783a-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="d783a-174">user.userprincipalname</span></span> |

    <span data-ttu-id="d783a-175">a.</span><span class="sxs-lookup"><span data-stu-id="d783a-175">a.</span></span> <span data-ttu-id="d783a-176">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="d783a-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d783a-179">b.</span><span class="sxs-lookup"><span data-stu-id="d783a-179">b.</span></span> <span data-ttu-id="d783a-180">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="d783a-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="d783a-181">c.</span><span class="sxs-lookup"><span data-stu-id="d783a-181">c.</span></span> <span data-ttu-id="d783a-182">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="d783a-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d783a-183">d.</span><span class="sxs-lookup"><span data-stu-id="d783a-183">d.</span></span> <span data-ttu-id="d783a-184">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d783a-184">Click **Ok**.</span></span>

4. <span data-ttu-id="d783a-185">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="d783a-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="d783a-187">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d783a-187">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d783a-189">Nella sezione **Configurazione di Blackboard Learn** fare clic su **Configura Blackboard Learn** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="d783a-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d783a-190">Copiare l'**ID di entità SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="d783a-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="d783a-192">Per configurare l'accesso Single Sign-On sul lato **Blackboard Learn**, è necessario inviare il file **XML metadati** e l'**ID di entità SAML** al [team di supporto di Blackboard Learn](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="d783a-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="d783a-193">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d783a-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d783a-194">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d783a-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d783a-195">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d783a-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d783a-196">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d783a-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="d783a-197">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d783a-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d783a-199">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d783a-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d783a-200">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d783a-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d783a-202">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d783a-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d783a-204">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d783a-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d783a-206">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d783a-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d783a-208">a.</span><span class="sxs-lookup"><span data-stu-id="d783a-208">a.</span></span> <span data-ttu-id="d783a-209">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d783a-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d783a-210">b.</span><span class="sxs-lookup"><span data-stu-id="d783a-210">b.</span></span> <span data-ttu-id="d783a-211">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d783a-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="d783a-212">c.</span><span class="sxs-lookup"><span data-stu-id="d783a-212">c.</span></span> <span data-ttu-id="d783a-213">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d783a-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d783a-214">d.</span><span class="sxs-lookup"><span data-stu-id="d783a-214">d.</span></span> <span data-ttu-id="d783a-215">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d783a-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="d783a-216">Creazione di un utente di test di Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="d783a-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="d783a-217">In questa sezione viene creato un utente di nome Britta Simon in Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="d783a-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="d783a-218">L'applicazione Blackboard Learn supporta il provisioning degli utenti just-in-time.</span><span class="sxs-lookup"><span data-stu-id="d783a-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="d783a-219">Assicurarsi di aver configurato le attestazioni come descritto nella sezione **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="d783a-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d783a-220">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d783a-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d783a-221">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="d783a-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d783a-223">**Per assegnare Britta Simon a Blackboard Learn, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d783a-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="d783a-224">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d783a-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d783a-226">Nell'elenco delle applicazioni selezionare **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="d783a-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="d783a-228">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d783a-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d783a-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d783a-230">Click **Add** button.</span></span> <span data-ttu-id="d783a-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d783a-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d783a-233">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d783a-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d783a-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d783a-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d783a-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d783a-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d783a-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d783a-236">Testing single sign-on</span></span>

<span data-ttu-id="d783a-237">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d783a-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d783a-238">Quando si fa clic sul riquadro Blackboard Learn nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="d783a-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="d783a-239">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d783a-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d783a-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d783a-240">Additional resources</span></span>

* [<span data-ttu-id="d783a-241">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d783a-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d783a-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d783a-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

