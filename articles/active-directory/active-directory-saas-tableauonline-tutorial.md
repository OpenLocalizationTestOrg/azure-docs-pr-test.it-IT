---
title: 'Esercitazione: Integrazione di Azure Active Directory con Tableau Online | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Tableau Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 443fab1198a91a4d5749e6421f7b8603fc75a81e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="43949-103">Esercitazione: Integrazione di Azure Active Directory con Tableau Online</span><span class="sxs-lookup"><span data-stu-id="43949-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="43949-104">Questa esercitazione descrive come integrare Tableau Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43949-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43949-105">L'integrazione di Tableau Online con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="43949-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="43949-106">È possibile controllare in Azure AD chi può accedere a Tableau Online</span><span class="sxs-lookup"><span data-stu-id="43949-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="43949-107">È possibile abilitare gli utenti per l'accesso automatico a Tableau Online (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="43949-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43949-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="43949-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="43949-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="43949-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43949-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="43949-110">Prerequisites</span></span>

<span data-ttu-id="43949-111">Per configurare l'integrazione di Azure AD con Tableau Online, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="43949-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="43949-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43949-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43949-113">Sottoscrizione di Tableau Online abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="43949-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="43949-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="43949-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43949-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="43949-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43949-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="43949-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43949-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43949-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43949-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="43949-118">Scenario description</span></span>
<span data-ttu-id="43949-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="43949-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43949-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="43949-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43949-121">Aggiunta di Tableau Online dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="43949-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="43949-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43949-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="43949-123">Aggiunta di Tableau Online dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="43949-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="43949-124">Per configurare l'integrazione di Tableau Online in Azure AD, è necessario aggiungere Tableau Online dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="43949-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="43949-125">**Per aggiungere Tableau Online dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="43949-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="43949-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="43949-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="43949-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="43949-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="43949-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="43949-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="43949-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="43949-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="43949-133">Nella casella di ricerca digitare **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="43949-133">In the search box, type **Tableau Online**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="43949-135">Nel pannello dei risultati selezionare **Tableau Online** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="43949-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43949-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43949-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43949-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Tableau Online usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="43949-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="43949-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Tableau Online che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43949-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="43949-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="43949-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="43949-141">Per stabilire la relazione di collegamento, in Tableau Online assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="43949-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="43949-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Tableau Online, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="43949-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="43949-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="43949-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="43949-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43949-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43949-145">**[Creazione di un utente test di Tableau Online](#creating-a-tableau-online-test-user)** : per avere una controparte di Britta Simon in Tableau Online collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43949-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="43949-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43949-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="43949-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="43949-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43949-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43949-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43949-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="43949-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="43949-150">**Per configurare l'accesso Single Sign-On di Azure AD con Tableau Online, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="43949-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="43949-151">Nella pagina di integrazione dell'applicazione **Tableau Online** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="43949-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="43949-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="43949-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="43949-155">Nella sezione **URL e dominio Tableau Online** eseguire i seguenti passaggi:</span><span class="sxs-lookup"><span data-stu-id="43949-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="43949-157">a.</span><span class="sxs-lookup"><span data-stu-id="43949-157">a.</span></span> <span data-ttu-id="43949-158">Nella casella di testo **URL accesso** digitare l'URL: `https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="43949-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="43949-159">b.</span><span class="sxs-lookup"><span data-stu-id="43949-159">b.</span></span> <span data-ttu-id="43949-160">Nella casella di testo **Identificatore** digitare l'URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="43949-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="43949-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="43949-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="43949-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="43949-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="43949-165">In una finestra del browser diversa accedere all'applicazione Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="43949-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="43949-166">Fare clic su **Settings** (Impostazioni) e quindi su **Authentication** (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="43949-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="43949-168">Per abilitare SAML, nella sezione **Authentication Types** (Tipi di autenticazione).</span><span class="sxs-lookup"><span data-stu-id="43949-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="43949-169">Selezionare la casella di controllo **Single sign-on with SAML** (Accesso Single Sign-On con SAML).</span><span class="sxs-lookup"><span data-stu-id="43949-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="43949-171">Scorrere verso il basso fino alla sezione **Import metadata file into Tableau Online** (Importa file di metadati in Tableau Online).</span><span class="sxs-lookup"><span data-stu-id="43949-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="43949-172">Fare clic su Browse (Sfoglia) e importare il file di metadati scaricato da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43949-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="43949-173">Fare quindi clic su **Apply**(Applica).</span><span class="sxs-lookup"><span data-stu-id="43949-173">Then, click **Apply**.</span></span>
   
   ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="43949-175">Nella sezione **Match assertions** (Corrispondenza asserzioni) inserire il nome di asserzione del provider di identità corrispondente per l'**indirizzo e-mail**, il **nome** e il **cognome**.</span><span class="sxs-lookup"><span data-stu-id="43949-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="43949-176">Per ottenere queste informazioni da Azure AD:</span><span class="sxs-lookup"><span data-stu-id="43949-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="43949-177">a.</span><span class="sxs-lookup"><span data-stu-id="43949-177">a.</span></span> <span data-ttu-id="43949-178">Nel portale di Azure, aprire la pagina di integrazione dell'applicazione **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="43949-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="43949-179">b.</span><span class="sxs-lookup"><span data-stu-id="43949-179">b.</span></span> <span data-ttu-id="43949-180">Nella sezione degli attributi, selezionare la casella di controllo **"Visualizza e modifica tutti gli altri attributi utente"**.</span><span class="sxs-lookup"><span data-stu-id="43949-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="43949-182">c.</span><span class="sxs-lookup"><span data-stu-id="43949-182">c.</span></span> <span data-ttu-id="43949-183">Copiare il valore dello spazio dei nomi per i seguenti attributi: givenname, e-mail e cognome utilizzando la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="43949-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Single Sign-On di Microsoft Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="43949-185">d.</span><span class="sxs-lookup"><span data-stu-id="43949-185">d.</span></span> <span data-ttu-id="43949-186">Fare clic sul valore **user.givenname**</span><span class="sxs-lookup"><span data-stu-id="43949-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="43949-187">e.</span><span class="sxs-lookup"><span data-stu-id="43949-187">e.</span></span> <span data-ttu-id="43949-188">Copiare il valore dalla casella di testo **spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="43949-188">Copy the value from the **namespace** textbox.</span></span>

   ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="43949-190">f.</span><span class="sxs-lookup"><span data-stu-id="43949-190">f.</span></span> <span data-ttu-id="43949-191">Per copiare i valori dello spazio dei nomi per l'e-mail e il cognome, eseguire i passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="43949-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="43949-192">g.</span><span class="sxs-lookup"><span data-stu-id="43949-192">g.</span></span> <span data-ttu-id="43949-193">Tornare all'applicazione Tableau Online e configurare la sezione **Tableau Online Attributes** (Attributi di Tableau Online) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="43949-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="43949-194">Indirizzo di posta elettronica: **mail** o **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="43949-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="43949-195">Nome: **givenname**</span><span class="sxs-lookup"><span data-stu-id="43949-195">First name: **givenname**</span></span>
     * <span data-ttu-id="43949-196">Cognome: **surname**</span><span class="sxs-lookup"><span data-stu-id="43949-196">Last name: **surname**</span></span>
   
   ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="43949-198">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="43949-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="43949-199">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="43949-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="43949-200">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43949-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43949-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43949-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="43949-202">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="43949-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="43949-204">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="43949-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="43949-205">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="43949-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="43949-207">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="43949-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="43949-209">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="43949-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="43949-211">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="43949-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43949-213">a.</span><span class="sxs-lookup"><span data-stu-id="43949-213">a.</span></span> <span data-ttu-id="43949-214">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43949-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43949-215">b.</span><span class="sxs-lookup"><span data-stu-id="43949-215">b.</span></span> <span data-ttu-id="43949-216">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43949-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43949-217">c.</span><span class="sxs-lookup"><span data-stu-id="43949-217">c.</span></span> <span data-ttu-id="43949-218">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="43949-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="43949-219">d.</span><span class="sxs-lookup"><span data-stu-id="43949-219">d.</span></span> <span data-ttu-id="43949-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="43949-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="43949-221">Creazione di un utente test di Tableau Online</span><span class="sxs-lookup"><span data-stu-id="43949-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="43949-222">In questa sezione viene creato un utente chiamato Britta Simon in Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="43949-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="43949-223">In **Tableau Online** fare clic su **Settings** (Impostazioni) e quindi sulla sezione **Authentication** (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="43949-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="43949-224">Scorrere verso il basso fino alla sezione **Select Users** (Selezione utenti).</span><span class="sxs-lookup"><span data-stu-id="43949-224">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="43949-225">Fare clic su **Add Users** (Aggiungi utenti) e quindi su **Enter Email Addresses** (Immettere indirizzi di posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="43949-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="43949-227">Selezionare **Add users for single sign-on (SSO) authentication**(Aggiungi utenti per l'autenticazione Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="43949-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="43949-228">Nella casella di testo **Enter Email Addresses** (Immettere indirizzi di posta elettronica) aggiungere britta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="43949-228">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="43949-230">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="43949-230">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="43949-231">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="43949-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="43949-232">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="43949-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![Assegna utente][200] 

<span data-ttu-id="43949-234">**Per assegnare Britta Simon a Tableau Online, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="43949-234">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="43949-235">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="43949-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="43949-237">Nell'elenco delle applicazioni selezionare **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="43949-237">In the applications list, select **Tableau Online**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="43949-239">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="43949-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="43949-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="43949-241">Click **Add** button.</span></span> <span data-ttu-id="43949-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="43949-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="43949-244">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="43949-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="43949-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="43949-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43949-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="43949-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="43949-247">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="43949-247">Testing single sign-on</span></span>

<span data-ttu-id="43949-248">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="43949-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="43949-249">Quando si fa clic sul riquadro Tableau Online nel pannello di accesso, viene effettuato automaticamente l'accesso all'applicazione Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="43949-249">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43949-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="43949-250">Additional resources</span></span>

* [<span data-ttu-id="43949-251">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43949-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43949-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43949-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

