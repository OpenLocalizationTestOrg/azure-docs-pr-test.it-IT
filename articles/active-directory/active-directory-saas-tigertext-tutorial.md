---
title: 'Esercitazione: Integrazione di Azure Active Directory con TigerText Secure Messenger | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e TigerText Secure Messenger.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e101e5fc84b032b66dd0636bab8bff128791f77c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="5e9a5-103">Esercitazione: Integrazione di Azure Active Directory con TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="5e9a5-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="5e9a5-104">Questa esercitazione descrive come integrare TigerText Secure Messenger con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e9a5-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e9a5-105">L'integrazione di TigerText Secure Messenger con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e9a5-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5e9a5-106">È possibile controllare in Azure AD chi può accedere a TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="5e9a5-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="5e9a5-107">È possibile abilitare gli utenti per l'accesso automatico a TigerText Secure Messenger (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="5e9a5-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5e9a5-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5e9a5-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5e9a5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e9a5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5e9a5-110">Prerequisites</span></span>

<span data-ttu-id="5e9a5-111">Per configurare l'integrazione di Azure AD con TigerText Secure Messenger, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e9a5-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="5e9a5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5e9a5-113">Sottoscrizione di TigerText Secure Messenger abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5e9a5-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5e9a5-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5e9a5-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e9a5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5e9a5-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5e9a5-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e9a5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e9a5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5e9a5-118">Scenario description</span></span>
<span data-ttu-id="5e9a5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5e9a5-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e9a5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5e9a5-121">Aggiungere TigerText Secure Messenger dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="5e9a5-121">Add TigerText Secure Messenger from the gallery</span></span>
2. <span data-ttu-id="5e9a5-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e9a5-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="5e9a5-123">Aggiungere TigerText Secure Messenger dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="5e9a5-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="5e9a5-124">Per configurare l'integrazione di TigerText Secure Messenger in Azure AD, è necessario aggiungere TigerText Secure Messenger dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5e9a5-125">**Per aggiungere TigerText Secure Messenger dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5e9a5-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9a5-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5e9a5-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5e9a5-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5e9a5-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5e9a5-133">Nella casella di ricerca digitare **TigerText Secure Messenger**, selezionare **TigerText Secure Messenger** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![Aggiungere dalla raccolta](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5e9a5-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e9a5-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5e9a5-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TigerText Secure Messenger usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5e9a5-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5e9a5-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di TigerText Secure Messenger corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="5e9a5-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="5e9a5-139">Per stabilire la relazione di collegamento, in TigerText Secure Messenger assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="5e9a5-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5e9a5-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con TigerText Secure Messenger, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e9a5-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5e9a5-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5e9a5-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e9a5-143">**[Creare un utente di test di TigerText Secure Messenger](#create-a-tigertext-secure-messenger-test-user)**: per avere una controparte di Britta Simon in TigerText Secure Messenger collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5e9a5-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e9a5-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5e9a5-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e9a5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5e9a5-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="5e9a5-148">**Per configurare l'accesso Single Sign-On di Azure AD con TigerText Secure Messenger, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5e9a5-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9a5-149">Nella pagina di integrazione dell'applicazione **TigerText Secure Messenger** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5e9a5-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="5e9a5-153">Nella sezione **URL e dominio TigerText Secure Messenger** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5e9a5-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![Sezione URL e dominio TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="5e9a5-155">a.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-155">a.</span></span> <span data-ttu-id="5e9a5-156">Nella casella di testo **URL di accesso** digitare l'URL come: `https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="5e9a5-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="5e9a5-157">b.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-157">b.</span></span> <span data-ttu-id="5e9a5-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="5e9a5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5e9a5-159">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="5e9a5-159">This value is not real.</span></span> <span data-ttu-id="5e9a5-160">è necessario aggiornare questo valore con l'ID effettivo.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="5e9a5-161">Per ottenere questo valore, contattare il [team di supporto clienti di TigerText Secure Messenger](mailTo:prosupport@tigertext.com).</span><span class="sxs-lookup"><span data-stu-id="5e9a5-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
4. <span data-ttu-id="5e9a5-162">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="5e9a5-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5e9a5-164">Click **Save** button.</span></span>

    ![Pulsante per il salvataggio](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5e9a5-166">Per configurare l'accesso Single Sign-On per l'applicazione, contattare il [team di supporto di TigerText Secure Messenger](mailTo:prosupport@tigertext.com) e fornire i **metadati scaricati**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="5e9a5-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5e9a5-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5e9a5-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e9a5-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5e9a5-170">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e9a5-170">Create an Azure AD test user</span></span>
<span data-ttu-id="5e9a5-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5e9a5-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5e9a5-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9a5-174">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5e9a5-176">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Utenti e gruppi -> Tutti gli utenti](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5e9a5-178">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5e9a5-180">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5e9a5-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo utente](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5e9a5-182">a.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-182">a.</span></span> <span data-ttu-id="5e9a5-183">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5e9a5-184">b.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-184">b.</span></span> <span data-ttu-id="5e9a5-185">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5e9a5-186">c.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-186">c.</span></span> <span data-ttu-id="5e9a5-187">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5e9a5-188">d.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-188">d.</span></span> <span data-ttu-id="5e9a5-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="5e9a5-190">Creare un utente di test di TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="5e9a5-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="5e9a5-191">In questa sezione viene creato un utente di nome Britta Simon in TigerText.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="5e9a5-192">Collaborare con il [team di supporto clienti di TigerText Secure Messenger](mailTo:prosupport@tigertext.com) per aggiungere gli utenti nella piattaforma TigerText.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5e9a5-193">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e9a5-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="5e9a5-194">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5e9a5-196">**Per assegnare Britta Simon a TigerText Secure Messenger, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="5e9a5-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="5e9a5-197">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5e9a5-199">Nell'elenco delle applicazioni selezionare **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger nell'elenco delle app](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="5e9a5-201">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5e9a5-203">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-203">Click **Add** button.</span></span> <span data-ttu-id="5e9a5-204">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5e9a5-206">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5e9a5-207">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5e9a5-208">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5e9a5-209">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5e9a5-209">Test single sign-on</span></span>

<span data-ttu-id="5e9a5-210">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5e9a5-211">Quando si fa clic sul riquadro TigerText nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione TigerText.</span><span class="sxs-lookup"><span data-stu-id="5e9a5-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="5e9a5-212">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e9a5-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5e9a5-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5e9a5-213">Additional resources</span></span>

* [<span data-ttu-id="5e9a5-214">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e9a5-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5e9a5-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e9a5-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

