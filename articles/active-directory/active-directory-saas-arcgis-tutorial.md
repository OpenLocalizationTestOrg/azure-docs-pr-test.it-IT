---
title: 'Esercitazione: Integrazione di Azure Active Directory con ArcGIS Online | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ArcGIS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="d1c07-103">Esercitazione: Integrazione di Azure Active Directory con ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="d1c07-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="d1c07-104">Questa esercitazione descrive come integrare ArcGIS Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1c07-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1c07-105">L'integrazione di ArcGIS Online con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1c07-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d1c07-106">È possibile controllare in Azure AD chi può accedere ad ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="d1c07-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="d1c07-107">È possibile abilitare gli utenti per l'accesso automatico ad ArcGIS Online (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="d1c07-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d1c07-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c07-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d1c07-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1c07-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="d1c07-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d1c07-110">Prerequisites</span></span>

<span data-ttu-id="d1c07-111">Per configurare l'integrazione di Azure AD con ArcGIS Online, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1c07-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="d1c07-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1c07-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1c07-113">Sottoscrizione di ArcGIS Online abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d1c07-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1c07-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d1c07-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1c07-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1c07-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1c07-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d1c07-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d1c07-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1c07-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1c07-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d1c07-118">Scenario description</span></span>
<span data-ttu-id="d1c07-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d1c07-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1c07-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1c07-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1c07-121">Aggiunta di ArcGIS Online dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d1c07-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="d1c07-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c07-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="d1c07-123">Aggiunta di ArcGIS Online dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d1c07-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="d1c07-124">Per configurare l'integrazione di ArcGIS Online in Azure AD, è necessario aggiungere ArcGIS Online dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d1c07-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d1c07-125">**Per aggiungere ArcGIS Online dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d1c07-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d1c07-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d1c07-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d1c07-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d1c07-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d1c07-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d1c07-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d1c07-133">Nella casella di ricerca digitare **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-133">In the search box, type **ArcGIS Online**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="d1c07-135">Nel pannello dei risultati selezionare **ArcGIS Online** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d1c07-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d1c07-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c07-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d1c07-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ArcGIS Online usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d1c07-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d1c07-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di ArcGIS Online corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1c07-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="d1c07-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="d1c07-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="d1c07-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente) in ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="d1c07-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="d1c07-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con ArcGIS Online, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1c07-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d1c07-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d1c07-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d1c07-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d1c07-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1c07-145">**[Creazione di un utente di test di ArcGIS Online](#creating-an-arcgis-online-test-user)**: per avere una controparte di Britta Simon in ArcGIS Online collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1c07-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d1c07-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1c07-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1c07-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d1c07-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d1c07-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c07-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d1c07-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="d1c07-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="d1c07-150">**Per configurare l'accesso Single Sign-On di Azure AD con ArcGIS Online, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d1c07-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="d1c07-151">Nella pagina di integrazione dell'applicazione **ArcGIS Online** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d1c07-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d1c07-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="d1c07-155">Nella sezione **URL e dominio ArcGIS Online** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d1c07-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="d1c07-157">Nella casella di testo **URL di accesso** digitare il valore usando il modello seguente: `https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="d1c07-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d1c07-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="d1c07-158">This value is not the real.</span></span> <span data-ttu-id="d1c07-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="d1c07-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d1c07-160">Per ottenere questo valore, contattare il [team di supporto clienti di ArcGIS Online](http://support.esri.com/).</span><span class="sxs-lookup"><span data-stu-id="d1c07-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="d1c07-161">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="d1c07-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="d1c07-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d1c07-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d1c07-165">In un'altra finestra del Web browser accedere al sito aziendale di ArcGIS come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d1c07-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="d1c07-166">Fare clic su **EDIT SETTINGS** (Modifica impostazioni).</span><span class="sxs-lookup"><span data-stu-id="d1c07-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="d1c07-167">![Modificare le impostazioni](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Modificare le impostazioni")</span><span class="sxs-lookup"><span data-stu-id="d1c07-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="d1c07-168">Fare clic su **Security**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-168">Click **Security**.</span></span>

    <span data-ttu-id="d1c07-169">![Sicurezza](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="d1c07-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="d1c07-170">In **Enterprise Logins** (Accessi aziendali) fare clic su **SET IDENTITY PROVIDER** (Imposta provider di identità).</span><span class="sxs-lookup"><span data-stu-id="d1c07-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="d1c07-171">![Accessi aziendali](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Accessi aziendali")</span><span class="sxs-lookup"><span data-stu-id="d1c07-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="d1c07-172">Nella pagina di configurazione **Set Identity Provider** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d1c07-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="d1c07-173">![Impostare il provider di identità](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Impostare il provider di identità")</span><span class="sxs-lookup"><span data-stu-id="d1c07-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="d1c07-174">a.</span><span class="sxs-lookup"><span data-stu-id="d1c07-174">a.</span></span> <span data-ttu-id="d1c07-175">Nella casella di testo **Name** (Nome) digitare il nome della propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d1c07-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="d1c07-176">b.</span><span class="sxs-lookup"><span data-stu-id="d1c07-176">b.</span></span> <span data-ttu-id="d1c07-177">In **I metadati per il provider di identità dell'organizzazione verranno forniti mediante**, selezionare **Un File**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="d1c07-178">c.</span><span class="sxs-lookup"><span data-stu-id="d1c07-178">c.</span></span> <span data-ttu-id="d1c07-179">Per caricare il file di metadati scaricato, fare clic su **Seleziona file**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="d1c07-180">d.</span><span class="sxs-lookup"><span data-stu-id="d1c07-180">d.</span></span> <span data-ttu-id="d1c07-181">Fare clic su **SET IDENTITY PROVIDER** (Imposta provider di identità).</span><span class="sxs-lookup"><span data-stu-id="d1c07-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="d1c07-182">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d1c07-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d1c07-183">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d1c07-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d1c07-184">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1c07-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d1c07-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c07-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="d1c07-186">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c07-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d1c07-188">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d1c07-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d1c07-189">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d1c07-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d1c07-191">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d1c07-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d1c07-193">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d1c07-195">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d1c07-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d1c07-197">a.</span><span class="sxs-lookup"><span data-stu-id="d1c07-197">a.</span></span> <span data-ttu-id="d1c07-198">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1c07-199">b.</span><span class="sxs-lookup"><span data-stu-id="d1c07-199">b.</span></span> <span data-ttu-id="d1c07-200">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d1c07-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="d1c07-201">c.</span><span class="sxs-lookup"><span data-stu-id="d1c07-201">c.</span></span> <span data-ttu-id="d1c07-202">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d1c07-203">d.</span><span class="sxs-lookup"><span data-stu-id="d1c07-203">d.</span></span> <span data-ttu-id="d1c07-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="d1c07-205">Creazione di un utente di test di ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="d1c07-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="d1c07-206">Per consentire agli utenti di Azure AD di accedere ad ArcGIS Online, è necessario effettuarne il provisioning in ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="d1c07-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="d1c07-207">Nel caso di ArcGIS Online, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d1c07-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="d1c07-208">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d1c07-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d1c07-209">Accedere al tenant **ArcGIS** .</span><span class="sxs-lookup"><span data-stu-id="d1c07-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="d1c07-210">Fare clic su **INVITE MEMBERS** (Invita membri).</span><span class="sxs-lookup"><span data-stu-id="d1c07-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="d1c07-211">![Invitare i membri](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invitare i membri")</span><span class="sxs-lookup"><span data-stu-id="d1c07-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="d1c07-212">Selezionare **Add members automatically without sending an email** (Aggiungi membri automaticamente senza inviare un'e-mail) e quindi fare clic su **NEXT** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="d1c07-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="d1c07-213">![Aggiungere i membri automaticamente](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Aggiungere i membri automaticamente")</span><span class="sxs-lookup"><span data-stu-id="d1c07-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="d1c07-214">Nella finestra di dialogo **Membri** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d1c07-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="d1c07-215">![Aggiungere ed esaminare](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Aggiungere ed esaminare")</span><span class="sxs-lookup"><span data-stu-id="d1c07-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="d1c07-216">a.</span><span class="sxs-lookup"><span data-stu-id="d1c07-216">a.</span></span> <span data-ttu-id="d1c07-217">Nelle caselle di testo **Email** (Posta elettronica), **First name** (Nome) e **Last name** (Cognome) digitare rispettivamente l'indirizzo di posta elettronica, il nome e il cognome relativi a un account Azure AD valido di cui si vuole effettuare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="d1c07-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="d1c07-218">b.</span><span class="sxs-lookup"><span data-stu-id="d1c07-218">b.</span></span> <span data-ttu-id="d1c07-219">Fare clic su **ADD AND REVIEW** (Aggiungi e verifica).</span><span class="sxs-lookup"><span data-stu-id="d1c07-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="d1c07-220">Verificare i dati immessi e quindi fare clic su **ADD MEMBERS** (Aggiungi membri).</span><span class="sxs-lookup"><span data-stu-id="d1c07-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="d1c07-221">![Aggiungere un membro](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Aggiungere un membro")</span><span class="sxs-lookup"><span data-stu-id="d1c07-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="d1c07-222">Il titolare dell'account Azure Active Directory riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="d1c07-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d1c07-223">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1c07-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d1c07-224">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="d1c07-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d1c07-226">**Per assegnare Britta Simon ad ArcGIS Online, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d1c07-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="d1c07-227">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d1c07-229">Nell'elenco delle applicazioni selezionare **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="d1c07-231">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d1c07-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d1c07-233">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-233">Click **Add** button.</span></span> <span data-ttu-id="d1c07-234">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d1c07-236">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d1c07-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d1c07-237">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1c07-238">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d1c07-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d1c07-239">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d1c07-239">Testing single sign-on</span></span>

<span data-ttu-id="d1c07-240">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d1c07-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d1c07-241">Quando si fa clic sul riquadro ArcGIS Online nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="d1c07-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="d1c07-242">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1c07-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1c07-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d1c07-243">Additional resources</span></span>

* [<span data-ttu-id="d1c07-244">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1c07-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1c07-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1c07-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

