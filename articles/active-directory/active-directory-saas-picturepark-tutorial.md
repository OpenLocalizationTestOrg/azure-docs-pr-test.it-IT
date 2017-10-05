---
title: 'Esercitazione: Integrazione di Azure Active Directory con Picturepark | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Picturepark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 1c009aa1fdd3140a4466cf762b6c9687e74ce4c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="dd7da-103">Esercitazione: Integrazione di Azure Active Directory con Picturepark</span><span class="sxs-lookup"><span data-stu-id="dd7da-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="dd7da-104">Questa esercitazione descrive come integrare Picturepark con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd7da-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd7da-105">L'integrazione di Picturepark con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7da-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dd7da-106">È possibile controllare in Azure AD chi può accedere a Picturepark</span><span class="sxs-lookup"><span data-stu-id="dd7da-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="dd7da-107">È possibile abilitare gli utenti per l'accesso automatico a Picturepark (Single Sign-On) con gli account Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd7da-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd7da-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7da-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dd7da-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd7da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd7da-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dd7da-110">Prerequisites</span></span>

<span data-ttu-id="dd7da-111">Per configurare l'integrazione di Azure AD con Picturepark, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7da-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="dd7da-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd7da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd7da-113">Sottoscrizione di Picturepark abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dd7da-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd7da-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dd7da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd7da-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd7da-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="dd7da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd7da-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd7da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd7da-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="dd7da-118">Scenario description</span></span>
<span data-ttu-id="dd7da-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="dd7da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd7da-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd7da-121">Aggiunta di Picturepark dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dd7da-121">Adding Picturepark from the gallery</span></span>
2. <span data-ttu-id="dd7da-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd7da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="dd7da-123">Aggiunta di Picturepark dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dd7da-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="dd7da-124">Per configurare l'integrazione di Picturepark in Azure AD, è necessario aggiungere Picturepark dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="dd7da-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dd7da-125">**Per aggiungere Picturepark dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dd7da-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dd7da-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dd7da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd7da-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dd7da-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="dd7da-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="dd7da-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="dd7da-133">Nella casella di ricerca digitare **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-133">In the search box, type **Picturepark**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="dd7da-135">Nel pannello dei risultati selezionare **Picturepark** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dd7da-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd7da-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd7da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd7da-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Picturepark in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dd7da-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dd7da-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di Picturepark corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd7da-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="dd7da-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Picturepark.</span><span class="sxs-lookup"><span data-stu-id="dd7da-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="dd7da-141">Per stabilire la relazione di collegamento, in Picturepark assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="dd7da-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dd7da-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Picturepark, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7da-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dd7da-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dd7da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dd7da-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd7da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd7da-145">**[Creazione di un utente test di Picturepark](#creating-a-picturepark-test-user)**: per avere una controparte di Britta Simon in Picturepark collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dd7da-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd7da-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd7da-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd7da-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="dd7da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd7da-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd7da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd7da-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Picturepark.</span><span class="sxs-lookup"><span data-stu-id="dd7da-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="dd7da-150">**Per configurare l'accesso Single Sign-On di Azure AD con Picturepark, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dd7da-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="dd7da-151">Nella pagina di integrazione dell'applicazione **Picturepark** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="dd7da-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="dd7da-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="dd7da-155">Nella sezione **URL e dominio Picturepark** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dd7da-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="dd7da-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd7da-157">a.</span></span> <span data-ttu-id="dd7da-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.picturepark.com`.</span><span class="sxs-lookup"><span data-stu-id="dd7da-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="dd7da-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd7da-159">b.</span></span> <span data-ttu-id="dd7da-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="dd7da-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="dd7da-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="dd7da-161">These values are not real.</span></span> <span data-ttu-id="dd7da-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="dd7da-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dd7da-163">Per ottenere questi valori, contattare il [team di supporto clienti di Picturepark](https://picturepark.com/about/contact/).</span><span class="sxs-lookup"><span data-stu-id="dd7da-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="dd7da-164">Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE** del certificato.</span><span class="sxs-lookup"><span data-stu-id="dd7da-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="dd7da-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="dd7da-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd7da-168">Nella sezione **Configurazione di Picturepark** fare clic su **Configura Picturepark** per visualizzare la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dd7da-169">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="dd7da-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="dd7da-171">In un'altra finestra del Web browser accedere al sito aziendale di Picturepark come amministratore.</span><span class="sxs-lookup"><span data-stu-id="dd7da-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="dd7da-172">Nella barra degli strumenti in alto fare clic su **Strumenti di amministrazione**, quindi fare clic su **Console di gestione**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="dd7da-173">![Console di gestione](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Console di gestione")</span><span class="sxs-lookup"><span data-stu-id="dd7da-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="dd7da-174">Fare clic su **Autenticazione**, quindi su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="dd7da-175">![Autenticazione](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Autenticazione")</span><span class="sxs-lookup"><span data-stu-id="dd7da-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="dd7da-176">Nella sezione **Configurazione provider di identità** , eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dd7da-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="dd7da-177">![Configurazione del provider di identità](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configurazione del provider di identità")</span><span class="sxs-lookup"><span data-stu-id="dd7da-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="dd7da-178">a.</span><span class="sxs-lookup"><span data-stu-id="dd7da-178">a.</span></span> <span data-ttu-id="dd7da-179">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-179">Click **Add**.</span></span>
  
    <span data-ttu-id="dd7da-180">b.</span><span class="sxs-lookup"><span data-stu-id="dd7da-180">b.</span></span> <span data-ttu-id="dd7da-181">Digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="dd7da-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="dd7da-182">c.</span><span class="sxs-lookup"><span data-stu-id="dd7da-182">c.</span></span> <span data-ttu-id="dd7da-183">Selezionare **Imposta come predefinito**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="dd7da-184">d.</span><span class="sxs-lookup"><span data-stu-id="dd7da-184">d.</span></span> <span data-ttu-id="dd7da-185">Nella casella di testo **URI autorità emittente** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7da-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="dd7da-186">e.</span><span class="sxs-lookup"><span data-stu-id="dd7da-186">e.</span></span> <span data-ttu-id="dd7da-187">Nella casella di testo **Trusted Issuer Thumb Print** (Identificazione personale autorità emittente attendibile) incollare il valore di **Identificazione personale** copiato dalla sezione **Certificato di firma SAML**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="dd7da-188">Fare clic su **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="dd7da-189">Per impostare l'attributo **EmailAddress** nella casella di testo **Claim** (Attestazione), digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="dd7da-190">![Configurazione](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configurazione")</span><span class="sxs-lookup"><span data-stu-id="dd7da-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="dd7da-191">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="dd7da-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dd7da-192">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="dd7da-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dd7da-193">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd7da-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd7da-194">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd7da-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd7da-195">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7da-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="dd7da-197">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dd7da-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dd7da-198">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dd7da-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd7da-200">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="dd7da-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd7da-202">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd7da-204">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dd7da-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd7da-206">a.</span><span class="sxs-lookup"><span data-stu-id="dd7da-206">a.</span></span> <span data-ttu-id="dd7da-207">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd7da-208">b.</span><span class="sxs-lookup"><span data-stu-id="dd7da-208">b.</span></span> <span data-ttu-id="dd7da-209">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd7da-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd7da-210">c.</span><span class="sxs-lookup"><span data-stu-id="dd7da-210">c.</span></span> <span data-ttu-id="dd7da-211">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dd7da-212">d.</span><span class="sxs-lookup"><span data-stu-id="dd7da-212">d.</span></span> <span data-ttu-id="dd7da-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="dd7da-214">Creazione di un utente test di Picturepark</span><span class="sxs-lookup"><span data-stu-id="dd7da-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="dd7da-215">Per consentire agli utenti di Azure AD di accedere a Picturepark, è necessario eseguirne il provisioning in Picturepark.</span><span class="sxs-lookup"><span data-stu-id="dd7da-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="dd7da-216">Nel caso di Picturepark, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="dd7da-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="dd7da-217">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dd7da-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="dd7da-218">Accedere al tenant **Picturepark** .</span><span class="sxs-lookup"><span data-stu-id="dd7da-218">Log in to your **Picturepark** tenant.</span></span>

2. <span data-ttu-id="dd7da-219">Nella barra degli strumenti in alto fare clic su **Strumenti di amministrazione**, quindi su **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="dd7da-220">![Utenti](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="dd7da-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="dd7da-221">Nella scheda **Panoramica utenti** fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="dd7da-222">![Gestione degli utenti](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Gestione degli utenti")</span><span class="sxs-lookup"><span data-stu-id="dd7da-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="dd7da-223">Nella finestra di dialogo **Crea utente** eseguire i passaggi seguenti per un utente di Azure Active Directory valido di cui si vuole eseguire il provisioning:</span><span class="sxs-lookup"><span data-stu-id="dd7da-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="dd7da-224">![Crea utente](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="dd7da-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="dd7da-225">a.</span><span class="sxs-lookup"><span data-stu-id="dd7da-225">a.</span></span> <span data-ttu-id="dd7da-226">Nella casella di testo **Indirizzo di posta elettronica** digitare l'**indirizzo di posta elettronica** dell'utente **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="dd7da-227">b.</span><span class="sxs-lookup"><span data-stu-id="dd7da-227">b.</span></span> <span data-ttu-id="dd7da-228">Nelle caselle di testo **Password** e **Conferma password** digitare la **password** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd7da-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="dd7da-229">c.</span><span class="sxs-lookup"><span data-stu-id="dd7da-229">c.</span></span> <span data-ttu-id="dd7da-230">Nella casella di testo **Nome** digitare il **nome** dell'utente **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="dd7da-231">d.</span><span class="sxs-lookup"><span data-stu-id="dd7da-231">d.</span></span> <span data-ttu-id="dd7da-232">Nella casella di testo **Cognome** digitare il **cognome** dell'utente **Simon**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="dd7da-233">e.</span><span class="sxs-lookup"><span data-stu-id="dd7da-233">e.</span></span> <span data-ttu-id="dd7da-234">Nella casella di testo **Società** digitare il **nome della società** dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dd7da-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="dd7da-235">f.</span><span class="sxs-lookup"><span data-stu-id="dd7da-235">f.</span></span> <span data-ttu-id="dd7da-236">Nella casella di testo **Paese** selezionare il **paese** dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dd7da-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="dd7da-237">g.</span><span class="sxs-lookup"><span data-stu-id="dd7da-237">g.</span></span> <span data-ttu-id="dd7da-238">Nella casella **CAP** digitare il **CAP** della città.</span><span class="sxs-lookup"><span data-stu-id="dd7da-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="dd7da-239">h.</span><span class="sxs-lookup"><span data-stu-id="dd7da-239">h.</span></span> <span data-ttu-id="dd7da-240">Nella casella di testo **Città** digitare il **nome della città** dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dd7da-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="dd7da-241">i.</span><span class="sxs-lookup"><span data-stu-id="dd7da-241">i.</span></span> <span data-ttu-id="dd7da-242">Selezionare una **Language**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="dd7da-243">j.</span><span class="sxs-lookup"><span data-stu-id="dd7da-243">j.</span></span> <span data-ttu-id="dd7da-244">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="dd7da-245">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerta da Picturepark per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd7da-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dd7da-246">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd7da-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dd7da-247">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Picturepark.</span><span class="sxs-lookup"><span data-stu-id="dd7da-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![Assegna utente][200] 

<span data-ttu-id="dd7da-249">**Per assegnare Britta Simon a Picturepark, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dd7da-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="dd7da-250">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="dd7da-252">Nell'elenco di applicazioni selezionare **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-252">In the applications list, select **Picturepark**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="dd7da-254">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="dd7da-254">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="dd7da-256">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-256">Click **Add** button.</span></span> <span data-ttu-id="dd7da-257">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="dd7da-259">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="dd7da-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dd7da-260">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd7da-261">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dd7da-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd7da-262">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dd7da-262">Testing single sign-on</span></span>

<span data-ttu-id="dd7da-263">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="dd7da-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dd7da-264">Quando si fa clic sul riquadro Picturepark nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Picturepark.</span><span class="sxs-lookup"><span data-stu-id="dd7da-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="dd7da-265">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dd7da-265">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd7da-266">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="dd7da-266">Additional resources</span></span>

* [<span data-ttu-id="dd7da-267">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd7da-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd7da-268">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd7da-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

