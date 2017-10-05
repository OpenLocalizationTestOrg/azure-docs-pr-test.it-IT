---
title: 'Esercitazione: Integrazione di Azure Active Directory con Box | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Box.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 2cc2afe8ff3f0063224c94eb0b8135347051b0aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="6fe6a-103">Esercitazione: Integrazione di Azure Active Directory con Box</span><span class="sxs-lookup"><span data-stu-id="6fe6a-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="6fe6a-104">Questa esercitazione descrive come integrare Box con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6fe6a-104">In this tutorial, you learn how to integrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6fe6a-105">L'integrazione di Box con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6fe6a-105">Integrating Box with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6fe6a-106">È possibile controllare in Azure AD chi può accedere a Box</span><span class="sxs-lookup"><span data-stu-id="6fe6a-106">You can control in Azure AD who has access to Box</span></span>
- <span data-ttu-id="6fe6a-107">È possibile abilitare gli utenti per l'accesso automatico a Box (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe6a-107">You can enable your users to automatically get signed-on to Box (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6fe6a-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6fe6a-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6fe6a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fe6a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6fe6a-110">Prerequisites</span></span>

<span data-ttu-id="6fe6a-111">Per configurare l'integrazione di Azure AD con Box, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6fe6a-111">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="6fe6a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6fe6a-113">Sottoscrizione di Box abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6fe6a-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6fe6a-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6fe6a-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6fe6a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6fe6a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6fe6a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6fe6a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6fe6a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6fe6a-118">Scenario description</span></span>
<span data-ttu-id="6fe6a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6fe6a-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6fe6a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6fe6a-121">Aggiunta di Box dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6fe6a-121">Adding Box from the gallery</span></span>
2. <span data-ttu-id="6fe6a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe6a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-the-gallery"></a><span data-ttu-id="6fe6a-123">Aggiunta di Box dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6fe6a-123">Adding Box from the gallery</span></span>
<span data-ttu-id="6fe6a-124">Per configurare l'integrazione di Box in Azure AD è necessario aggiungere Box dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-124">To configure the integration of Box into Azure AD, you need to add Box from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6fe6a-125">**Per aggiungere Box dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6fe6a-125">**To add Box from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6fe6a-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6fe6a-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6fe6a-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6fe6a-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6fe6a-133">Nella casella di ricerca digitare **Box**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-133">In the search box, type **Box**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="6fe6a-135">Nel pannello dei risultati selezionare **Box** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-135">In the results panel, select **Box**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6fe6a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe6a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6fe6a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Box in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6fe6a-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6fe6a-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Box che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Box is to a user in Azure AD.</span></span> <span data-ttu-id="6fe6a-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Box.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-140">In other words, a link relationship between an Azure AD user and the related user in Box needs to be established.</span></span>

<span data-ttu-id="6fe6a-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Box.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Box.</span></span>

<span data-ttu-id="6fe6a-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Box, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="6fe6a-142">To configure and test Azure AD single sign-on with Box, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6fe6a-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6fe6a-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6fe6a-145">**[Creazione di un utente di test di Box](#creating-a-box-test-user)**: per avere una controparte di Britta Simon in Box collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-145">**[Creating a Box test user](#creating-a-box-test-user)** - to have a counterpart of Britta Simon in Box that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6fe6a-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6fe6a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6fe6a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe6a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6fe6a-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Box.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="6fe6a-150">**Per configurare l'accesso Single Sign-On di Azure AD con Box, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6fe6a-150">**To configure Azure AD single sign-on with Box, perform the following steps:**</span></span>

1. <span data-ttu-id="6fe6a-151">Nella pagina di integrazione dell'applicazione **Box** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-151">In the Azure portal, on the **Box** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6fe6a-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="6fe6a-155">Nella sezione **URL e dominio Box** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6fe6a-155">On the **Box Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="6fe6a-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="6fe6a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6fe6a-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="6fe6a-158">This value is not real.</span></span> <span data-ttu-id="6fe6a-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-159">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="6fe6a-160">Per ottenere questo valore, contattare il [team di supporto clienti di Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire).</span><span class="sxs-lookup"><span data-stu-id="6fe6a-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) to get this value.</span></span> 
 
4. <span data-ttu-id="6fe6a-161">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="6fe6a-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6fe6a-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6fe6a-165">Per ottenere la configurazione dell'accesso Single Sign-On per l'applicazione, contattare il [team di supporto di Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) e fornire il file XML scaricato.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-165">To get SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with the downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="6fe6a-166">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6fe6a-167">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6fe6a-168">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6fe6a-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6fe6a-169">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe6a-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="6fe6a-170">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6fe6a-172">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6fe6a-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6fe6a-173">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6fe6a-175">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6fe6a-177">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6fe6a-179">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6fe6a-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6fe6a-181">a.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-181">a.</span></span> <span data-ttu-id="6fe6a-182">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6fe6a-183">b.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-183">b.</span></span> <span data-ttu-id="6fe6a-184">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6fe6a-185">c.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-185">c.</span></span> <span data-ttu-id="6fe6a-186">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6fe6a-187">d.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-187">d.</span></span> <span data-ttu-id="6fe6a-188">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="6fe6a-189">Creazione di un utente test di Box</span><span class="sxs-lookup"><span data-stu-id="6fe6a-189">Creating a Box test user</span></span>

<span data-ttu-id="6fe6a-190">In questa sezione si crea un utente di nome Britta Simon in Box.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="6fe6a-191">Box supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="6fe6a-192">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-192">There is no action item for you in this section.</span></span> <span data-ttu-id="6fe6a-193">Se un utente non esiste in Box, ne viene creato uno nuovo quando si tenta di accedere a Box.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-193">If a user doesn't already exist in Box, a new one is created when you attempt to access Box.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6fe6a-194">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe6a-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6fe6a-195">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Box.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Box.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6fe6a-197">**Per assegnare Britta Simon a Box, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6fe6a-197">**To assign Britta Simon to Box, perform the following steps:**</span></span>

1. <span data-ttu-id="6fe6a-198">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6fe6a-200">Nell'elenco delle applicazioni selezionare **Box**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-200">In the applications list, select **Box**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="6fe6a-202">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6fe6a-204">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-204">Click **Add** button.</span></span> <span data-ttu-id="6fe6a-205">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6fe6a-207">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6fe6a-208">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6fe6a-209">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6fe6a-210">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6fe6a-210">Testing single sign-on</span></span>

<span data-ttu-id="6fe6a-211">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6fe6a-212">Quando si fa clic sul riquadro Box nel pannello di accesso, si apre la pagina per accedere all'applicazione Box.</span><span class="sxs-lookup"><span data-stu-id="6fe6a-212">When you click the Box tile in the Access Panel, you should get login page to get signed-on to your Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6fe6a-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6fe6a-213">Additional resources</span></span>

* [<span data-ttu-id="6fe6a-214">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fe6a-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6fe6a-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fe6a-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="6fe6a-216">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="6fe6a-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

