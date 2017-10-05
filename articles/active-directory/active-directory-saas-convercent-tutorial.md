---
title: 'Esercitazione: Integrazione di Azure Active Directory con Convercent | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Convercent.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 7af33cae7448a212734d327570b5082d0278fa0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="2467a-103">Esercitazione: Integrazione di Azure Active Directory con Convercent</span><span class="sxs-lookup"><span data-stu-id="2467a-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="2467a-104">Questa esercitazione descrive come integrare Convercent con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2467a-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2467a-105">L'integrazione di Convercent con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2467a-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2467a-106">È possibile controllare in Azure AD chi può accedere a Convercent</span><span class="sxs-lookup"><span data-stu-id="2467a-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="2467a-107">È possibile abilitare gli utenti per l'accesso automatico a Convercent (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2467a-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2467a-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2467a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2467a-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2467a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2467a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2467a-110">Prerequisites</span></span>

<span data-ttu-id="2467a-111">Per configurare l'integrazione di Azure AD con Convercent, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2467a-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="2467a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2467a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2467a-113">Sottoscrizione di Convercent abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2467a-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2467a-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2467a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2467a-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2467a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2467a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2467a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2467a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2467a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2467a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2467a-118">Scenario description</span></span>
<span data-ttu-id="2467a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2467a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2467a-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2467a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2467a-121">Aggiunta di Convercent dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2467a-121">Adding Convercent from the gallery</span></span>
2. <span data-ttu-id="2467a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2467a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-the-gallery"></a><span data-ttu-id="2467a-123">Aggiunta di Convercent dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2467a-123">Adding Convercent from the gallery</span></span>
<span data-ttu-id="2467a-124">Per configurare l'integrazione di Convercent in Azure AD, è necessario aggiungere Convercent dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2467a-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2467a-125">**Per aggiungere Convercent dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2467a-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2467a-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2467a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2467a-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2467a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2467a-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2467a-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2467a-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="2467a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2467a-133">Nella casella di ricerca digitare **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="2467a-133">In the search box, type **Convercent**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="2467a-135">Nel pannello dei risultati selezionare **Convercent** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2467a-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2467a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2467a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2467a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Convercent mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2467a-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2467a-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Convercent che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2467a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="2467a-140">In altre parole deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Convercent.</span><span class="sxs-lookup"><span data-stu-id="2467a-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="2467a-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Convercent.</span><span class="sxs-lookup"><span data-stu-id="2467a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="2467a-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Convercent, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2467a-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2467a-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2467a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2467a-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2467a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2467a-145">**[Creazione di un utente test di Convercent](#creating-a-convercent-test-user)**: per avere una controparte di Britta Simon in Convercent collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2467a-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2467a-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2467a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2467a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="2467a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2467a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2467a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2467a-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Convercent.</span><span class="sxs-lookup"><span data-stu-id="2467a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="2467a-150">**Per configurare l'accesso Single Sign-On di Azure AD con Convercent, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2467a-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="2467a-151">Nella pagina di integrazione dell'applicazione **Convercent** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2467a-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2467a-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2467a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="2467a-155">Nella sezione **URL e dominio Convercent**, se si vuole configurare l'applicazione in **modalità avviata da IDP** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2467a-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="2467a-157">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="2467a-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="2467a-158">Per configurare l'applicazione in **modalità avviata da SP**, nella sezione **URL e dominio Convercent** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2467a-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="2467a-160">a.</span><span class="sxs-lookup"><span data-stu-id="2467a-160">a.</span></span> <span data-ttu-id="2467a-161">Fare clic su **Mostra impostazioni URL avanzate**.</span><span class="sxs-lookup"><span data-stu-id="2467a-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="2467a-162">b.</span><span class="sxs-lookup"><span data-stu-id="2467a-162">b.</span></span> <span data-ttu-id="2467a-163">Nella casella di testo **URL di accesso** digitare il valore usando il criterio seguente: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="2467a-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="2467a-164">c.</span><span class="sxs-lookup"><span data-stu-id="2467a-164">c.</span></span> <span data-ttu-id="2467a-165">Nella casella di testo **Stato dell'inoltro** digitare il valore usando il criterio seguente: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="2467a-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2467a-166">Questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="2467a-166">These values are not the real values.</span></span> <span data-ttu-id="2467a-167">Aggiornare i valori con l'identificatore, l'URL di accesso e lo stato dell'inoltro effettivi.</span><span class="sxs-lookup"><span data-stu-id="2467a-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="2467a-168">Per ottenere questi valori contattare il [team di supporto clienti di Convercent](http://support.convercent.com).</span><span class="sxs-lookup"><span data-stu-id="2467a-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span></span>

5. <span data-ttu-id="2467a-169">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="2467a-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="2467a-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2467a-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="2467a-173">Per ottenere la configurazione dell'accesso Single Sign-On per l'applicazione, contattare il [team di supporto di Convercent](mailto:support@convercent.com) e trasmettere il file **XML metadati** scaricato.</span><span class="sxs-lookup"><span data-stu-id="2467a-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="2467a-174">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="2467a-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2467a-175">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="2467a-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2467a-176">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2467a-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2467a-177">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2467a-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="2467a-178">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2467a-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2467a-180">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2467a-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2467a-181">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2467a-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2467a-183">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="2467a-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2467a-185">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="2467a-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2467a-187">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2467a-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2467a-189">a.</span><span class="sxs-lookup"><span data-stu-id="2467a-189">a.</span></span> <span data-ttu-id="2467a-190">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2467a-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2467a-191">b.</span><span class="sxs-lookup"><span data-stu-id="2467a-191">b.</span></span> <span data-ttu-id="2467a-192">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2467a-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2467a-193">c.</span><span class="sxs-lookup"><span data-stu-id="2467a-193">c.</span></span> <span data-ttu-id="2467a-194">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="2467a-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2467a-195">d.</span><span class="sxs-lookup"><span data-stu-id="2467a-195">d.</span></span> <span data-ttu-id="2467a-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2467a-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="2467a-197">Creazione di un utente test di Convercent</span><span class="sxs-lookup"><span data-stu-id="2467a-197">Creating a Convercent test user</span></span>

<span data-ttu-id="2467a-198">Collaborare con il [team di supporto di Convercent](mailto:support@convercent.com) per aggiungere gli utenti nella piattaforma Convercent.</span><span class="sxs-lookup"><span data-stu-id="2467a-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2467a-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2467a-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2467a-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Convercent.</span><span class="sxs-lookup"><span data-stu-id="2467a-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2467a-202">**Per assegnare Britta Simon a Convercent, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2467a-202">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="2467a-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2467a-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2467a-205">Nell'elenco delle applicazioni selezionare **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="2467a-205">In the applications list, select **Convercent**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="2467a-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2467a-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2467a-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2467a-209">Click **Add** button.</span></span> <span data-ttu-id="2467a-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2467a-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2467a-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="2467a-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2467a-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2467a-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2467a-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2467a-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2467a-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2467a-215">Testing single sign-on</span></span>

<span data-ttu-id="2467a-216">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2467a-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2467a-217">Quando si fa clic sul riquadro Convercent nel pannello di accesso, si accederà automaticamente all'applicazione Convercent.</span><span class="sxs-lookup"><span data-stu-id="2467a-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>
<span data-ttu-id="2467a-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2467a-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2467a-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2467a-219">Additional resources</span></span>

* [<span data-ttu-id="2467a-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2467a-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2467a-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2467a-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

