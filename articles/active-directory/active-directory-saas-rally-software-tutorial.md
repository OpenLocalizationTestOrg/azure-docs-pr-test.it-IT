---
title: 'Esercitazione: Integrazione di Azure Active Directory con Rally Software | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Rally Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 6481c9ef0ca71419ccfa6f7956f4702985743df3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="657cd-103">Esercitazione: Integrazione di Azure Active Directory con Rally Software</span><span class="sxs-lookup"><span data-stu-id="657cd-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="657cd-104">Questa esercitazione descrive come integrare Rally Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="657cd-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="657cd-105">L'integrazione di Rally Software con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="657cd-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="657cd-106">È possibile controllare in Azure AD chi può accedere a Rally Software.</span><span class="sxs-lookup"><span data-stu-id="657cd-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="657cd-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a Rally Software con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="657cd-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="657cd-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="657cd-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="657cd-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="657cd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="657cd-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="657cd-110">Prerequisites</span></span>

<span data-ttu-id="657cd-111">Per configurare l'integrazione di Azure AD con Rally Software sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="657cd-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="657cd-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="657cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="657cd-113">Sottoscrizione di Rally Software abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="657cd-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="657cd-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="657cd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="657cd-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="657cd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="657cd-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="657cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="657cd-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="657cd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="657cd-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="657cd-118">Scenario description</span></span>
<span data-ttu-id="657cd-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="657cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="657cd-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="657cd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="657cd-121">Aggiunta di Rally Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="657cd-121">Adding Rally Software from the gallery</span></span>
2. <span data-ttu-id="657cd-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="657cd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="657cd-123">Aggiunta di Rally Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="657cd-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="657cd-124">Per configurare l'integrazione di Rally Software in Azure AD è necessario aggiungere Rally Software dalla raccolta al proprio elenco delle app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="657cd-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="657cd-125">**Per aggiungere Rally Software dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="657cd-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="657cd-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="657cd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="657cd-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="657cd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="657cd-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="657cd-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="657cd-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="657cd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="657cd-133">Nella casella di ricerca digitare **Rally Software**, selezionare **Rally Software** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="657cd-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![Rally Software nell'elenco risultati](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="657cd-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="657cd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="657cd-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Rally Software mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="657cd-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="657cd-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Rally Software corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="657cd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="657cd-138">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Rally Software.</span><span class="sxs-lookup"><span data-stu-id="657cd-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="657cd-139">Per stabilire la relazione di collegamento, in Rally Software assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="657cd-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="657cd-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Rally Software è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="657cd-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="657cd-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="657cd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="657cd-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="657cd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="657cd-143">**[Creare un utente test di Rally Software](#create-a-rally-software-test-user)**: per avere una controparte di Britta Simon in Rally Software collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="657cd-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="657cd-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="657cd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="657cd-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="657cd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="657cd-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="657cd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="657cd-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Rally Software.</span><span class="sxs-lookup"><span data-stu-id="657cd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="657cd-148">**Per configurare l'accesso Single Sign-On di Azure AD con Rally Software, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="657cd-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="657cd-149">Nella pagina di integrazione dell'applicazione **Rally Software** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="657cd-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="657cd-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="657cd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="657cd-153">Nella sezione **URL e dominio Rally Software** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="657cd-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="657cd-155">a.</span><span class="sxs-lookup"><span data-stu-id="657cd-155">a.</span></span> <span data-ttu-id="657cd-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant-name>.rally.com`.</span><span class="sxs-lookup"><span data-stu-id="657cd-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="657cd-157">b.</span><span class="sxs-lookup"><span data-stu-id="657cd-157">b.</span></span> <span data-ttu-id="657cd-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="657cd-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="657cd-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="657cd-159">These values are not real.</span></span> <span data-ttu-id="657cd-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="657cd-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="657cd-161">Per ottenere questi valori contattare il [team di supporto clienti di Rally Software](https://help.rallydev.com/).</span><span class="sxs-lookup"><span data-stu-id="657cd-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="657cd-162">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="657cd-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="657cd-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="657cd-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="657cd-166">Nella sezione **Configurazione di Rally Software** fare clic su **Configura Rally Software** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="657cd-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="657cd-167">Copiare l'**URL di disconnessione e l'ID di entità SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="657cd-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurazione di Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="657cd-169">Accedere al tenant **Rally Software** .</span><span class="sxs-lookup"><span data-stu-id="657cd-169">Log in to your **Rally Software** tenant.</span></span>

8. <span data-ttu-id="657cd-170">Nella barra degli strumenti in alto fare clic su **Setup** (Configurazione), quindi selezionare **Subscription** (Sottoscrizione).</span><span class="sxs-lookup"><span data-stu-id="657cd-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="657cd-171">![Sottoscrizione](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Sottoscrizione")</span><span class="sxs-lookup"><span data-stu-id="657cd-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="657cd-172">Fare clic sul pulsante **Action** (Azione).</span><span class="sxs-lookup"><span data-stu-id="657cd-172">Click the **Action** button.</span></span> <span data-ttu-id="657cd-173">Selezionare **Edit Subscription** (Modifica sottoscrizione) in alto a destra sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="657cd-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

10. <span data-ttu-id="657cd-174">Nella finestra di dialogo **Subscription** (Sottoscrizione) eseguire la procedura seguente, quindi fare clic su **Save & Close** (Salva e chiudi):</span><span class="sxs-lookup"><span data-stu-id="657cd-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="657cd-175">![Autenticazione](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Autenticazione")</span><span class="sxs-lookup"><span data-stu-id="657cd-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="657cd-176">a.</span><span class="sxs-lookup"><span data-stu-id="657cd-176">a.</span></span> <span data-ttu-id="657cd-177">Selezionare **Rally or SSO authentication** (Autenticazione Rally o SSO) dall'elenco a discesa Authentication (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="657cd-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="657cd-178">b.</span><span class="sxs-lookup"><span data-stu-id="657cd-178">b.</span></span> <span data-ttu-id="657cd-179">Nella casella di testo **Identity Provider URL** (URL provider di identità) incollare il valore di **SAML Entity ID** (ID entità SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="657cd-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="657cd-180">c.</span><span class="sxs-lookup"><span data-stu-id="657cd-180">c.</span></span> <span data-ttu-id="657cd-181">Nella casella di testo **SSO Logout** (Disconnessione SSO) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="657cd-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="657cd-182">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="657cd-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="657cd-183">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="657cd-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="657cd-184">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="657cd-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="657cd-185">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="657cd-185">Create an Azure AD test user</span></span>

<span data-ttu-id="657cd-186">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="657cd-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="657cd-188">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="657cd-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="657cd-189">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="657cd-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="657cd-191">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="657cd-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="657cd-193">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="657cd-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="657cd-195">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="657cd-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="657cd-197">a.</span><span class="sxs-lookup"><span data-stu-id="657cd-197">a.</span></span> <span data-ttu-id="657cd-198">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="657cd-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="657cd-199">b.</span><span class="sxs-lookup"><span data-stu-id="657cd-199">b.</span></span> <span data-ttu-id="657cd-200">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="657cd-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="657cd-201">c.</span><span class="sxs-lookup"><span data-stu-id="657cd-201">c.</span></span> <span data-ttu-id="657cd-202">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="657cd-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="657cd-203">d.</span><span class="sxs-lookup"><span data-stu-id="657cd-203">d.</span></span> <span data-ttu-id="657cd-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="657cd-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="657cd-205">Creare un utente test di Rally Software</span><span class="sxs-lookup"><span data-stu-id="657cd-205">Create a Rally Software test user</span></span>

<span data-ttu-id="657cd-206">Per consentire agli utenti di Azure AD di accedere, è necessario effettuarne il provisioning nell'applicazione Rally Software usando i relativi nomi utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="657cd-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="657cd-207">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="657cd-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="657cd-208">Accedere al tenant Rally Software.</span><span class="sxs-lookup"><span data-stu-id="657cd-208">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="657cd-209">Passare a **Impostazione \> UTENTI** e quindi fare clic su **+ Aggiungi nuovo**.</span><span class="sxs-lookup"><span data-stu-id="657cd-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="657cd-210">![Utenti](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="657cd-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="657cd-211">Digitare il nome nella casella di testo Nuovo utente, quindi fare clic su **Aggiungi con dettagli**.</span><span class="sxs-lookup"><span data-stu-id="657cd-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="657cd-212">Nella sezione **Crea utente** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="657cd-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="657cd-213">![Crea utente](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="657cd-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="657cd-214">a.</span><span class="sxs-lookup"><span data-stu-id="657cd-214">a.</span></span> <span data-ttu-id="657cd-215">Nella casella di testo **Name** (Nome) digitare il nome dell'utente, ad esempio **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="657cd-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="657cd-216">b.</span><span class="sxs-lookup"><span data-stu-id="657cd-216">b.</span></span> <span data-ttu-id="657cd-217">Nella casella di testo **Email address** (Indirizzo di posta elettronica) immettere l'indirizzo di posta elettronica dell'utente, ad esempio **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="657cd-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="657cd-218">c.</span><span class="sxs-lookup"><span data-stu-id="657cd-218">c.</span></span> <span data-ttu-id="657cd-219">Nella casella di testo **First Name** (Nome) immettere il nome dell'utente, ad esempio **Britta**.</span><span class="sxs-lookup"><span data-stu-id="657cd-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="657cd-220">d.</span><span class="sxs-lookup"><span data-stu-id="657cd-220">d.</span></span> <span data-ttu-id="657cd-221">Nella casella di testo **Last Name** (Nome) immettere il cognome dell'utente, ad esempio **Simon**.</span><span class="sxs-lookup"><span data-stu-id="657cd-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="657cd-222">e.</span><span class="sxs-lookup"><span data-stu-id="657cd-222">e.</span></span> <span data-ttu-id="657cd-223">Fare clic su **Salva e chiudi**.</span><span class="sxs-lookup"><span data-stu-id="657cd-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="657cd-224">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerti da Rally Software per effettuare il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="657cd-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="657cd-225">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="657cd-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="657cd-226">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure tramite la concessione dell'accesso a Rally Software.</span><span class="sxs-lookup"><span data-stu-id="657cd-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="657cd-228">**Per assegnare Britta Simon a Rally Software, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="657cd-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="657cd-229">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="657cd-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="657cd-231">Nell'elenco delle applicazioni selezionare **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="657cd-231">In the applications list, select **Rally Software**.</span></span>

    ![Collegamento di Rally Software nell'elenco delle applicazioni](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="657cd-233">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="657cd-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="657cd-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="657cd-235">Click **Add** button.</span></span> <span data-ttu-id="657cd-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="657cd-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="657cd-238">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="657cd-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="657cd-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="657cd-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="657cd-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="657cd-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="657cd-241">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="657cd-241">Test single sign-on</span></span>

<span data-ttu-id="657cd-242">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="657cd-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="657cd-243">Quando si fa clic sul riquadro Rally Software nel pannello di accesso si accede automaticamente all'applicazione Rally Software.</span><span class="sxs-lookup"><span data-stu-id="657cd-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="657cd-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="657cd-244">Additional resources</span></span>

* [<span data-ttu-id="657cd-245">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="657cd-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="657cd-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="657cd-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

