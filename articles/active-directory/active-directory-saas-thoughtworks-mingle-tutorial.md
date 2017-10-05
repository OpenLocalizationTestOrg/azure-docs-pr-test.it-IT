---
title: 'Esercitazione: Integrazione di Azure Active Directory con Thoughtworks Mingle | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Thoughtworks Mingle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 268ae5affb88a718f68c08daa94fe7aba4a99c11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="77ced-103">Esercitazione: Integrazione di Azure Active Directory con Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="77ced-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="77ced-104">Questa esercitazione descrive come integrare Thoughtworks Mingle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77ced-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77ced-105">L'integrazione di Thoughtworks Mingle con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="77ced-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="77ced-106">È possibile controllare in Azure AD chi può accedere a Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="77ced-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="77ced-107">È possibile abilitare gli utenti per l'accesso automatico a Thoughtworks Mingle (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="77ced-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77ced-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="77ced-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="77ced-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77ced-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77ced-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="77ced-110">Prerequisites</span></span>

<span data-ttu-id="77ced-111">Per configurare l'integrazione di Azure AD con Thoughtworks Mingle, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="77ced-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="77ced-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77ced-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77ced-113">Sottoscrizione di Thoughtworks Mingle abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="77ced-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77ced-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="77ced-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77ced-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="77ced-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77ced-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="77ced-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77ced-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77ced-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77ced-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="77ced-118">Scenario description</span></span>
<span data-ttu-id="77ced-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="77ced-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77ced-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="77ced-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77ced-121">Aggiunta di Thoughtworks Mingle dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="77ced-121">Adding Thoughtworks Mingle from the gallery</span></span>
2. <span data-ttu-id="77ced-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77ced-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="77ced-123">Aggiunta di Thoughtworks Mingle dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="77ced-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="77ced-124">Per configurare l'integrazione di Thoughtworks Mingle in Azure AD, è necessario aggiungere Thoughtworks Mingle dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="77ced-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="77ced-125">**Per aggiungere Thoughtworks Mingle dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="77ced-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="77ced-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="77ced-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="77ced-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="77ced-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="77ced-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="77ced-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="77ced-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="77ced-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="77ced-133">Nella casella di ricerca digitare **Thoughtworks Mingle**, selezionare **Thoughtworks Mingle** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="77ced-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![Thoughtworks Mingle nell'elenco dei risultati](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="77ced-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77ced-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="77ced-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Thoughtworks Mingle usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="77ced-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77ced-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Thoughtworks Mingle che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77ced-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="77ced-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="77ced-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="77ced-139">Per stabilire la relazione di collegamento, in Thoughtworks Mingle assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="77ced-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="77ced-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Thoughtworks Mingle, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="77ced-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="77ced-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="77ced-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="77ced-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77ced-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77ced-143">**[Creare un utente di test per Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**: per avere una controparte di Britta Simon in Thoughtworks Mingle collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77ced-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="77ced-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77ced-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77ced-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="77ced-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="77ced-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77ced-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="77ced-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="77ced-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="77ced-148">**Per configurare l'accesso Single Sign-On di Azure AD con Thoughtworks Mingle, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="77ced-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="77ced-149">Nella pagina di integrazione dell'applicazione **Thoughtworks Mingle** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="77ced-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="77ced-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="77ced-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="77ced-153">Nella sezione **URL e dominio Thoughtworks Mingle** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="77ced-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="77ced-155">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.mingle.thoughtworks.com`.</span><span class="sxs-lookup"><span data-stu-id="77ced-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="77ced-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="77ced-156">The value is not real.</span></span> <span data-ttu-id="77ced-157">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="77ced-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="77ced-158">Per ottenere il valore contattare il [team di supporto clienti di Thoughtworks Mingle](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support).</span><span class="sxs-lookup"><span data-stu-id="77ced-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
4. <span data-ttu-id="77ced-159">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="77ced-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="77ced-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="77ced-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77ced-163">Accedere al sito aziendale di **Thoughtworks Mingle** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="77ced-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="77ced-164">Fare clic sulla scheda **Admin**, quindi fare clic su **Config SSO**.</span><span class="sxs-lookup"><span data-stu-id="77ced-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="77ced-165">![Scheda Amministrazione](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Config SSO")</span><span class="sxs-lookup"><span data-stu-id="77ced-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="77ced-166">Nella sezione **Config SSO** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77ced-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="77ced-167">![Configurazione dell'accesso SSO](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configurazione dell'accesso SSO")</span><span class="sxs-lookup"><span data-stu-id="77ced-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="77ced-168">a.</span><span class="sxs-lookup"><span data-stu-id="77ced-168">a.</span></span> <span data-ttu-id="77ced-169">Per caricare il file di metadati, fare clic su **Scegli file**.</span><span class="sxs-lookup"><span data-stu-id="77ced-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="77ced-170">b.</span><span class="sxs-lookup"><span data-stu-id="77ced-170">b.</span></span> <span data-ttu-id="77ced-171">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="77ced-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="77ced-172">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="77ced-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="77ced-173">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="77ced-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="77ced-174">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77ced-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="77ced-175">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77ced-175">Create an Azure AD test user</span></span>
<span data-ttu-id="77ced-176">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="77ced-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="77ced-178">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77ced-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="77ced-179">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="77ced-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77ced-181">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="77ced-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77ced-183">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="77ced-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77ced-185">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="77ced-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77ced-187">a.</span><span class="sxs-lookup"><span data-stu-id="77ced-187">a.</span></span> <span data-ttu-id="77ced-188">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77ced-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77ced-189">b.</span><span class="sxs-lookup"><span data-stu-id="77ced-189">b.</span></span> <span data-ttu-id="77ced-190">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="77ced-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77ced-191">c.</span><span class="sxs-lookup"><span data-stu-id="77ced-191">c.</span></span> <span data-ttu-id="77ced-192">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="77ced-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="77ced-193">d.</span><span class="sxs-lookup"><span data-stu-id="77ced-193">d.</span></span> <span data-ttu-id="77ced-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="77ced-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="77ced-195">Creare un utente di test di Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="77ced-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="77ced-196">Per consentire agli utenti di Azure AD di accedere, è necessario eseguirne il privisioning nell'applicazione Thoughtworks Mingle utilizzando i relativi nomi utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="77ced-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="77ced-197">Nel caso di Thoughtworks Mingle, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="77ced-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="77ced-198">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="77ced-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="77ced-199">Accedere al sito aziendale di Thoughtworks Mingle come amministratore.</span><span class="sxs-lookup"><span data-stu-id="77ced-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="77ced-200">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="77ced-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="77ced-201">![Primo progetto](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Primo progetto")</span><span class="sxs-lookup"><span data-stu-id="77ced-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="77ced-202">Fare clic sulla scheda **Admin**, quindi fare clic su **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="77ced-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="77ced-203">![Utenti](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="77ced-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="77ced-204">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="77ced-204">Click **New User**.</span></span>
   
    <span data-ttu-id="77ced-205">![Nuovo utente](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="77ced-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="77ced-206">Nella pagina **Nuovo utente** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="77ced-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="77ced-207">![Finestra di dialogo Nuovo utente](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="77ced-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="77ced-208">a.</span><span class="sxs-lookup"><span data-stu-id="77ced-208">a.</span></span> <span data-ttu-id="77ced-209">Digitare nelle caselle di testo correlate **Nome accesso**, **Nome visualizzato**, **Scegli password**, **Conferma password** le informazioni relative a un account Azure AD valido di cui si desidera eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="77ced-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="77ced-210">b.</span><span class="sxs-lookup"><span data-stu-id="77ced-210">b.</span></span> <span data-ttu-id="77ced-211">In **Tipo di utente** selezionare **Base**.</span><span class="sxs-lookup"><span data-stu-id="77ced-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="77ced-212">c.</span><span class="sxs-lookup"><span data-stu-id="77ced-212">c.</span></span> <span data-ttu-id="77ced-213">Fare clic su **Crea questo profilo**.</span><span class="sxs-lookup"><span data-stu-id="77ced-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="77ced-214">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Thoughtworks Mingle per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="77ced-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="77ced-215">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77ced-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="77ced-216">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="77ced-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="77ced-218">**Per assegnare Britta Simon a Thoughtworks Mingle, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="77ced-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="77ced-219">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="77ced-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="77ced-221">Nell'elenco delle applicazioni selezionare **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="77ced-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![Il collegamento Thoughtworks Mingle nell'elenco delle applicazioni](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="77ced-223">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="77ced-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202] 

4. <span data-ttu-id="77ced-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="77ced-225">Click **Add** button.</span></span> <span data-ttu-id="77ced-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="77ced-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="77ced-228">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="77ced-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="77ced-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="77ced-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77ced-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="77ced-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="77ced-231">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="77ced-231">Test single sign-on</span></span>

<span data-ttu-id="77ced-232">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="77ced-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="77ced-233">Quando si fa clic sul riquadro Thoughtworks Mingle nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="77ced-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77ced-234">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="77ced-234">Additional resources</span></span>

* [<span data-ttu-id="77ced-235">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77ced-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77ced-236">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77ced-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

