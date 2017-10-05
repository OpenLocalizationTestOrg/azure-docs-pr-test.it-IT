---
title: 'Esercitazione: integrazione di Azure Active Directory con Lynda.com | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Lynda.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="cd8a2-103">Esercitazione: Integrazione di Azure Active Directory con Lynda.com</span><span class="sxs-lookup"><span data-stu-id="cd8a2-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="cd8a2-104">Questa esercitazione descrive come integrare Lynda.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cd8a2-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd8a2-105">L'integrazione di Lynda.com con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd8a2-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cd8a2-106">È possibile controllare in Azure AD chi può accedere a Lynda.com</span><span class="sxs-lookup"><span data-stu-id="cd8a2-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="cd8a2-107">È possibile abilitare gli utenti per l'accesso automatico a Lynda.com (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd8a2-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd8a2-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cd8a2-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cd8a2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd8a2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cd8a2-110">Prerequisites</span></span>

<span data-ttu-id="cd8a2-111">Per configurare l'integrazione di Azure AD con Lynda.com, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd8a2-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="cd8a2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd8a2-113">Sottoscrizione di Lynda.com abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cd8a2-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd8a2-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd8a2-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd8a2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd8a2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd8a2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd8a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd8a2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cd8a2-118">Scenario description</span></span>
<span data-ttu-id="cd8a2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd8a2-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd8a2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd8a2-121">Aggiunta di Lynda.com dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="cd8a2-121">Adding Lynda.com from the gallery</span></span>
2. <span data-ttu-id="cd8a2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd8a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="cd8a2-123">Aggiunta di Lynda.com dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="cd8a2-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="cd8a2-124">Per configurare l'integrazione di Lynda.com in Azure AD, è necessario aggiungere Lynda.com dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cd8a2-125">**Per aggiungere Lynda.com dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cd8a2-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cd8a2-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cd8a2-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cd8a2-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="cd8a2-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="cd8a2-133">Nella casella di ricerca digitare **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-133">In the search box, type **Lynda.com**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="cd8a2-135">Nel pannello dei risultati selezionare **Lynda.com** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd8a2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd8a2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd8a2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Lynda.com usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cd8a2-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cd8a2-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di Lynda.com che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="cd8a2-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="cd8a2-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="cd8a2-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Lynda.com, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd8a2-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cd8a2-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cd8a2-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd8a2-145">**[Creazione di un utente test di Lynda.com](#creating-a-lyndacom-test-user)**: per avere una controparte di Britta Simon in Lynda.com collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd8a2-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd8a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd8a2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd8a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd8a2-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="cd8a2-150">**Per configurare l'accesso Single Sign-On di Azure AD con Lynda.com, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cd8a2-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="cd8a2-151">Nella pagina di integrazione dell'applicazione **Lynda.com** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="cd8a2-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="cd8a2-155">Nella sezione **URL e dominio Lynda.com** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cd8a2-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="cd8a2-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="cd8a2-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd8a2-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="cd8a2-158">This value is not real.</span></span> <span data-ttu-id="cd8a2-159">aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="cd8a2-160">Per ottenere questi valori, contattare il [team di supporto clienti di Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="cd8a2-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
4. <span data-ttu-id="cd8a2-161">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="cd8a2-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cd8a2-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cd8a2-165">Per configurare l'accesso Single Sign-On sul lato **Lynda.com**, è necessario inviare il file **XML dei metadati** scaricato al [supporto di Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="cd8a2-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd8a2-166">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd8a2-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd8a2-167">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="cd8a2-169">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cd8a2-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cd8a2-170">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd8a2-172">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd8a2-174">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd8a2-176">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cd8a2-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd8a2-178">a.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-178">a.</span></span> <span data-ttu-id="cd8a2-179">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd8a2-180">b.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-180">b.</span></span> <span data-ttu-id="cd8a2-181">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd8a2-182">c.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-182">c.</span></span> <span data-ttu-id="cd8a2-183">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cd8a2-184">d.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-184">d.</span></span> <span data-ttu-id="cd8a2-185">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="cd8a2-186">Creazione di un utente test di Lynda.com</span><span class="sxs-lookup"><span data-stu-id="cd8a2-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="cd8a2-187">Non è richiesta alcuna operazione per configurare il provisioning degli utenti in Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="cd8a2-188">Quando un utente assegnato prova ad accedere a Lynda.com usando il pannello di accesso, Lynda.com verifica se l'utente esiste.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="cd8a2-189">Se l’account utente non è ancora disponibile, viene creato automaticamente da Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="cd8a2-190">È possibile utilizzare qualsiasi altro strumento di creazione di account utente di Lynda.com o le API fornite da Lynda.com per effettuare il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cd8a2-191">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd8a2-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cd8a2-192">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![Assegna utente][200] 

<span data-ttu-id="cd8a2-194">**Per assegnare Britta Simon a Lynda.com, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cd8a2-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="cd8a2-195">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cd8a2-197">Nell'elenco delle applicazioni selezionare **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-197">In the applications list, select **Lynda.com**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="cd8a2-199">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="cd8a2-201">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-201">Click **Add** button.</span></span> <span data-ttu-id="cd8a2-202">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="cd8a2-204">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cd8a2-205">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd8a2-206">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cd8a2-207">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cd8a2-207">Testing single sign-on</span></span>

<span data-ttu-id="cd8a2-208">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cd8a2-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="cd8a2-209">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cd8a2-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cd8a2-210">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cd8a2-210">Additional resources</span></span>

* [<span data-ttu-id="cd8a2-211">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd8a2-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd8a2-212">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd8a2-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

