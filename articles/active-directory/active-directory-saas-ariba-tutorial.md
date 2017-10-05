---
title: 'Esercitazione: Integrazione di Azure Active Directory con Ariba | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Ariba.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 214367847055ba38ee03a28d0afdcc58f68333cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="ab7b5-103">Esercitazione: Integrazione di Azure Active Directory con Ariba</span><span class="sxs-lookup"><span data-stu-id="ab7b5-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="ab7b5-104">Questa esercitazione descrive come integrare Ariba con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ab7b5-104">In this tutorial, you learn how to integrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab7b5-105">L'integrazione di Ariba con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab7b5-105">Integrating Ariba with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ab7b5-106">È possibile controllare in Azure AD chi può accedere ad Ariba</span><span class="sxs-lookup"><span data-stu-id="ab7b5-106">You can control in Azure AD who has access to Ariba</span></span>
- <span data-ttu-id="ab7b5-107">È possibile abilitare gli utenti per l'accesso automatico ad Ariba (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab7b5-107">You can enable your users to automatically get signed-on to Ariba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ab7b5-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ab7b5-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab7b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab7b5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ab7b5-110">Prerequisites</span></span>

<span data-ttu-id="ab7b5-111">Per configurare l'integrazione di Azure AD con Ariba, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab7b5-111">To configure Azure AD integration with Ariba, you need the following items:</span></span>

- <span data-ttu-id="ab7b5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab7b5-113">Sottoscrizione di Ariba abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ab7b5-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab7b5-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab7b5-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab7b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab7b5-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab7b5-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab7b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab7b5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ab7b5-118">Scenario description</span></span>
<span data-ttu-id="ab7b5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab7b5-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab7b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab7b5-121">Aggiunta di Ariba dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ab7b5-121">Adding Ariba from the gallery</span></span>
2. <span data-ttu-id="ab7b5-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab7b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-the-gallery"></a><span data-ttu-id="ab7b5-123">Aggiunta di Ariba dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ab7b5-123">Adding Ariba from the gallery</span></span>
<span data-ttu-id="ab7b5-124">Per configurare l'integrazione di Ariba in Azure AD, è necessario aggiungere Ariba dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ab7b5-125">**Per aggiungere Ariba dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ab7b5-125">**To add Ariba from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ab7b5-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ab7b5-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ab7b5-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ab7b5-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ab7b5-133">Nella casella di ricerca digitare **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-133">In the search box, type **Ariba**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="ab7b5-135">Nel pannello dei risultati selezionare **Ariba** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-135">In the results panel, select **Ariba**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ab7b5-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab7b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ab7b5-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Ariba in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ab7b5-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ab7b5-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Ariba che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Ariba is to a user in Azure AD.</span></span> <span data-ttu-id="ab7b5-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Ariba.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-140">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span></span>

<span data-ttu-id="ab7b5-141">Per stabilire la relazione di collegamento, in Ariba assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="ab7b5-141">In Ariba, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ab7b5-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Ariba, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab7b5-142">To configure and test Azure AD single sign-on with Ariba, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ab7b5-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ab7b5-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab7b5-145">**[Creazione di un utente test Ariba](#creating-an-ariba-test-user)** : per avere una controparte di Britta Simon in Ariba collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab7b5-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab7b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ab7b5-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab7b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ab7b5-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On all'applicazione Ariba.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="ab7b5-150">**Per configurare l'accesso Single Sign-On di Azure AD con Ariba, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ab7b5-150">**To configure Azure AD single sign-on with Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="ab7b5-151">Nella pagina di integrazione dell'applicazione **Ariba** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-151">In the Azure portal, on the **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ab7b5-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="ab7b5-155">Nella sezione **URL e dominio Ariba** eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="ab7b5-155">On the **Ariba Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="ab7b5-157">a.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-157">a.</span></span> <span data-ttu-id="ab7b5-158">Nella casella di testo **URL di accesso** digitare l'URL usando il criterio seguente: `https://<subdomain>.sourcing.ariba.com` o `https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="ab7b5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="ab7b5-159">b.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-159">b.</span></span> <span data-ttu-id="ab7b5-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="ab7b5-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ab7b5-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ab7b5-161">These values are not real.</span></span> <span data-ttu-id="ab7b5-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ab7b5-163">In questo caso è consigliabile usare in Identificatore il valore univoco della stringa.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="ab7b5-164">Per ottenere questi valori, contattare il team di supporto client di Ariba al numero **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-164">Contact Ariba Client support team at **1-866-218-2155** to get these values.</span></span> 
 

4. <span data-ttu-id="ab7b5-165">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate  file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="ab7b5-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ab7b5-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ab7b5-169">Per ottenere l'accesso SSO configurato per l'applicazione, contattare il team di supporto di Ariba al numero **1-866-218-2155** che fornirà anche le informazioni su come inviare il file **Certificato (Base64)** scaricato.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-169">To get SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how to provide them the downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="ab7b5-170">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ab7b5-171">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ab7b5-172">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ab7b5-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ab7b5-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab7b5-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="ab7b5-174">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ab7b5-176">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab7b5-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ab7b5-177">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ab7b5-179">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ab7b5-181">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ab7b5-183">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ab7b5-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ab7b5-185">a.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-185">a.</span></span> <span data-ttu-id="ab7b5-186">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab7b5-187">b.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-187">b.</span></span> <span data-ttu-id="ab7b5-188">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ab7b5-189">c.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-189">c.</span></span> <span data-ttu-id="ab7b5-190">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ab7b5-191">d.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-191">d.</span></span> <span data-ttu-id="ab7b5-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="ab7b5-193">Creazione di un utente test Ariba</span><span class="sxs-lookup"><span data-stu-id="ab7b5-193">Creating an Ariba test user</span></span>

<span data-ttu-id="ab7b5-194">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in Ariba.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-194">The objective of this section is to create a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="ab7b5-195">Collaborare contattando il team di supporto di Ariba al numero **1-866-218-2155** per aggiungere gli utenti nel sistema Ariba.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-195">Work with Ariba support team at **1-866-218-2155** to add the users in the Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="ab7b5-196">Per creare un utente manualmente, è necessario contattare il team di supporto di Ariba al numero **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-196">If you need to create a user manually, you need to contact the Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ab7b5-197">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab7b5-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ab7b5-198">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Ariba.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ariba.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ab7b5-200">**Per assegnare Britta Simon ad Ariba, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ab7b5-200">**To assign Britta Simon to Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="ab7b5-201">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ab7b5-203">Nell'elenco delle applicazioni selezionare **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-203">In the applications list, select **Ariba**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="ab7b5-205">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ab7b5-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-207">Click **Add** button.</span></span> <span data-ttu-id="ab7b5-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ab7b5-210">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ab7b5-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab7b5-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ab7b5-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ab7b5-213">Testing single sign-on</span></span>
<span data-ttu-id="ab7b5-214">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ab7b5-215">Quando si fa clic sul riquadro Ariba nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Ariba.</span><span class="sxs-lookup"><span data-stu-id="ab7b5-215">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ab7b5-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ab7b5-216">Additional resources</span></span>

* [<span data-ttu-id="ab7b5-217">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab7b5-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab7b5-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab7b5-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

