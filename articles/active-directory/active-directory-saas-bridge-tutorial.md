---
title: 'Esercitazione: Integrazione di Azure Active Directory con Bridge | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Bridge.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d2b7fd6f73f1b782cfe6337d13f9f22f9c70d389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="6f1b0-103">Esercitazione: Integrazione di Azure Active Directory con Bridge</span><span class="sxs-lookup"><span data-stu-id="6f1b0-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="6f1b0-104">Questa esercitazione descrive come integrare Bridge con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f1b0-104">In this tutorial, you learn how to integrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f1b0-105">L'integrazione di Bridge con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f1b0-105">Integrating Bridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6f1b0-106">È possibile controllare in Azure AD chi può accedere a Bridge</span><span class="sxs-lookup"><span data-stu-id="6f1b0-106">You can control in Azure AD who has access to Bridge</span></span>
- <span data-ttu-id="6f1b0-107">È possibile abilitare gli utenti per l'accesso automatico a Bridge (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f1b0-107">You can enable your users to automatically get signed-on to Bridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f1b0-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6f1b0-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f1b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f1b0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6f1b0-110">Prerequisites</span></span>

<span data-ttu-id="6f1b0-111">Per configurare l'integrazione di Azure AD con Bridge, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f1b0-111">To configure Azure AD integration with Bridge, you need the following items:</span></span>

- <span data-ttu-id="6f1b0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f1b0-113">Sottoscrizione di Bridge abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f1b0-113">A Bridge single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f1b0-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f1b0-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f1b0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f1b0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f1b0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f1b0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f1b0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6f1b0-118">Scenario description</span></span>
<span data-ttu-id="6f1b0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f1b0-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f1b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f1b0-121">Aggiunta di Bridge dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6f1b0-121">Adding Bridge from the gallery</span></span>
2. <span data-ttu-id="6f1b0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f1b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridge-from-the-gallery"></a><span data-ttu-id="6f1b0-123">Aggiunta di Bridge dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6f1b0-123">Adding Bridge from the gallery</span></span>
<span data-ttu-id="6f1b0-124">Per configurare l'integrazione di Bridge in Azure AD, è necessario aggiungere Bridge dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-124">To configure the integration of Bridge into Azure AD, you need to add Bridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6f1b0-125">**Per aggiungere Bridge dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f1b0-125">**To add Bridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6f1b0-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6f1b0-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6f1b0-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6f1b0-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6f1b0-133">Nella casella di ricerca digitare **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-133">In the search box, type **Bridge**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_search.png)

5. <span data-ttu-id="6f1b0-135">Nel pannello dei risultati selezionare **Bridge** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-135">In the results panel, select **Bridge**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f1b0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f1b0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f1b0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Bridge usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6f1b0-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6f1b0-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Bridge che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bridge is to a user in Azure AD.</span></span> <span data-ttu-id="6f1b0-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Bridge.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-140">In other words, a link relationship between an Azure AD user and the related user in Bridge needs to be established.</span></span>

<span data-ttu-id="6f1b0-141">Per stabilire la relazione di collegamento, in Bridge assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="6f1b0-141">In Bridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6f1b0-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Bridge, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f1b0-142">To configure and test Azure AD single sign-on with Bridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6f1b0-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6f1b0-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f1b0-145">**[Creazione di un utente di test di Bridge](#creating-a-bridge-test-user)**: per avere una controparte di Britta Simon in Bridge collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - to have a counterpart of Britta Simon in Bridge that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f1b0-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f1b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f1b0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f1b0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f1b0-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Bridge.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bridge application.</span></span>

<span data-ttu-id="6f1b0-150">**Per configurare l'accesso Single Sign-On di Azure AD con Bridge, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f1b0-150">**To configure Azure AD single sign-on with Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="6f1b0-151">Nella pagina di integrazione dell'applicazione **Bridge** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-151">In the Azure portal, on the **Bridge** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6f1b0-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_samlbase.png)

3. <span data-ttu-id="6f1b0-155">Nella sezione **URL e dominio Bridge** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f1b0-155">On the **Bridge Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_url.png)

    <span data-ttu-id="6f1b0-157">a.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-157">a.</span></span> <span data-ttu-id="6f1b0-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.bridgeapp.com`.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    <span data-ttu-id="6f1b0-159">b.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-159">b.</span></span> <span data-ttu-id="6f1b0-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="6f1b0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f1b0-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="6f1b0-161">These values are not real.</span></span> <span data-ttu-id="6f1b0-162">è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6f1b0-163">Per ottenere questi valori, contattare il [team di supporto clienti di Bridge](https://community.bridgeapp.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="6f1b0-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="6f1b0-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (base)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_certificate.png) 

5. <span data-ttu-id="6f1b0-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6f1b0-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f1b0-168">Nella sezione **Configurazione di Bridge** fare clic su **Configura Bridge** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-168">On the **Bridge Configuration** section, click **Configure Bridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6f1b0-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="6f1b0-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_configure.png) 

7. <span data-ttu-id="6f1b0-171">Per configurare l'accesso Single Sign-On sul lato **Bridge**, è necessario inviare il file **Certificato (base)** scaricato e l'**ID di entità SAML, l'URL del servizio Single Sign-On SAML e l'URL di disconnessione** al [team di supporto di Bridge](https://community.bridgeapp.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="6f1b0-171">To configure single sign-on on **Bridge** side, you need to send the downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** to [Bridge support team](https://community.bridgeapp.com/community/help).</span></span> 

> [!TIP]
> <span data-ttu-id="6f1b0-172">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6f1b0-173">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6f1b0-174">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f1b0-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f1b0-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f1b0-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="6f1b0-176">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6f1b0-178">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6f1b0-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6f1b0-179">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f1b0-181">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f1b0-183">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f1b0-185">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6f1b0-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f1b0-187">a.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-187">a.</span></span> <span data-ttu-id="6f1b0-188">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f1b0-189">b.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-189">b.</span></span> <span data-ttu-id="6f1b0-190">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f1b0-191">c.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-191">c.</span></span> <span data-ttu-id="6f1b0-192">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6f1b0-193">d.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-193">d.</span></span> <span data-ttu-id="6f1b0-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-194">Click **Create**.</span></span>
 
### <a name="creating-a-bridge-test-user"></a><span data-ttu-id="6f1b0-195">Creazione di un utente test di Bridge</span><span class="sxs-lookup"><span data-stu-id="6f1b0-195">Creating a Bridge test user</span></span>

<span data-ttu-id="6f1b0-196">In questa sezione viene creato un utente di nome Britta Simon in Bridge.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-196">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="6f1b0-197">Collaborare con il [team di supporto clienti di Bridge](https://community.bridgeapp.com/community/help) per creare un utente nella piattaforma.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) to create a user in the platform.</span></span> <span data-ttu-id="6f1b0-198">Per aggiungere utenti alla piattaforma Bridge è possibile generare il ticket di supporto per Bridge da <a href="https://community.bridgeapp.com/community/help">qui</a>.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-198">You can raise the support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> to add the users in the Bridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6f1b0-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f1b0-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6f1b0-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Bridge.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bridge.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6f1b0-202">**Per assegnare Britta Simon a Bridge, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6f1b0-202">**To assign Britta Simon to Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="6f1b0-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6f1b0-205">Nell'elenco delle applicazioni selezionare **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-205">In the applications list, select **Bridge**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_app.png) 

3. <span data-ttu-id="6f1b0-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6f1b0-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-209">Click **Add** button.</span></span> <span data-ttu-id="6f1b0-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6f1b0-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6f1b0-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f1b0-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f1b0-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6f1b0-215">Testing single sign-on</span></span>

<span data-ttu-id="6f1b0-216">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-216">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6f1b0-217">Quando si fa clic sul riquadro Bridge nel pannello di accesso, si accederà automaticamente all'applicazione Bridge.</span><span class="sxs-lookup"><span data-stu-id="6f1b0-217">When you click the Bridge tile in the Access Panel, you should get automatically signed-on to your Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f1b0-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6f1b0-218">Additional resources</span></span>

* [<span data-ttu-id="6f1b0-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f1b0-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f1b0-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f1b0-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_203.png

