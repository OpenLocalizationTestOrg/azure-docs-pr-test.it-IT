---
title: 'Esercitazione: Integrazione di Azure Active Directory con New Relic | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e New Relic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 605e85c23a849f70fcc0237361d7a891f716ca3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="6261b-103">Esercitazione: Integrazione di Azure Active Directory con New Relic</span><span class="sxs-lookup"><span data-stu-id="6261b-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="6261b-104">Questa esercitazione descrive come integrare New Relic con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6261b-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6261b-105">L'integrazione di New Relic con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6261b-105">Integrating New Relic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6261b-106">È possibile controllare in Azure AD chi può accedere a New Relic</span><span class="sxs-lookup"><span data-stu-id="6261b-106">You can control in Azure AD who has access to New Relic</span></span>
- <span data-ttu-id="6261b-107">È possibile abilitare gli utenti per l'accesso automatico a New Relic (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="6261b-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6261b-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6261b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6261b-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6261b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6261b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6261b-110">Prerequisites</span></span>

<span data-ttu-id="6261b-111">Per configurare l'integrazione di Azure AD con New Relic, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6261b-111">To configure Azure AD integration with New Relic, you need the following items:</span></span>

- <span data-ttu-id="6261b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6261b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6261b-113">Sottoscrizione di New Relic abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6261b-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6261b-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6261b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6261b-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6261b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6261b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6261b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6261b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6261b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6261b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6261b-118">Scenario description</span></span>
<span data-ttu-id="6261b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6261b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6261b-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6261b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6261b-121">Aggiunta di New Relic dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6261b-121">Adding New Relic from the gallery</span></span>
2. <span data-ttu-id="6261b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6261b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-the-gallery"></a><span data-ttu-id="6261b-123">Aggiunta di New Relic dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6261b-123">Adding New Relic from the gallery</span></span>
<span data-ttu-id="6261b-124">Per configurare l'integrazione di New Relic in Azure AD, è necessario aggiungere New Relic dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6261b-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6261b-125">**Per aggiungere New Relic dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6261b-125">**To add New Relic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6261b-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6261b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6261b-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6261b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6261b-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6261b-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6261b-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="6261b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6261b-133">Nella casella di ricerca digitare **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="6261b-133">In the search box, type **New Relic**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="6261b-135">Nel pannello dei risultati selezionare **New Relic** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6261b-135">In the results panel, select **New Relic**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6261b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6261b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6261b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con New Relic usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6261b-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6261b-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di New Relic corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6261b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span></span> <span data-ttu-id="6261b-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in New Relic.</span><span class="sxs-lookup"><span data-stu-id="6261b-140">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span></span>

<span data-ttu-id="6261b-141">Per stabilire la relazione di collegamento, in New Relic assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="6261b-141">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6261b-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con New Relic, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="6261b-142">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6261b-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6261b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6261b-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6261b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6261b-145">**[Creazione di un utente di test di New Relic](#creating-a-new-relic-test-user)**: per avere una controparte di Britta Simon in New Relic collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6261b-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6261b-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6261b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6261b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="6261b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6261b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6261b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6261b-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione New Relic.</span><span class="sxs-lookup"><span data-stu-id="6261b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="6261b-150">**Per configurare l'accesso Single Sign-On di Azure AD con New Relic, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6261b-150">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="6261b-151">Nella pagina di integrazione dell'applicazione **New Relic** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6261b-151">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6261b-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6261b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="6261b-155">Nella sezione **URL e dominio New Relic** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6261b-155">On the **New Relic Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="6261b-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="6261b-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6261b-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="6261b-158">The value is not real.</span></span> <span data-ttu-id="6261b-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="6261b-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="6261b-160">Per ottenere il valore contattare il [team di supporto di New Relic](https://support.newrelic.com/).</span><span class="sxs-lookup"><span data-stu-id="6261b-160">Contact [New Relic Client support team](https://support.newrelic.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="6261b-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="6261b-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="6261b-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6261b-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6261b-165">Nella sezione **Configurazione di New Relic** fare clic su **Configura New Relic** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="6261b-165">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6261b-166">Copiare l'**URL di disconnessione e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="6261b-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="6261b-168">In un'altra finestra del Web browser accedere al sito aziendale di **New Relic** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6261b-168">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="6261b-169">Nel menu in alto fare clic su **Impostazioni account**.</span><span class="sxs-lookup"><span data-stu-id="6261b-169">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="6261b-170">![Impostazioni account](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="6261b-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="6261b-171">Fare clic sulla scheda **Security and authentication** (Sicurezza e autenticazione), quindi fare clic sulla scheda **Single sign on**.</span><span class="sxs-lookup"><span data-stu-id="6261b-171">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
    <span data-ttu-id="6261b-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="6261b-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="6261b-173">Nella pagina della finestra di dialogo SAML eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6261b-173">On the SAML dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="6261b-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="6261b-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="6261b-175">a.</span><span class="sxs-lookup"><span data-stu-id="6261b-175">a.</span></span> <span data-ttu-id="6261b-176">Fare clic su **Choose File** per caricare il certificato di Azure Active Directory scaricato.</span><span class="sxs-lookup"><span data-stu-id="6261b-176">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="6261b-177">b.</span><span class="sxs-lookup"><span data-stu-id="6261b-177">b.</span></span> <span data-ttu-id="6261b-178">Nella casella di testo **Remote login URL** (URL di accesso remoto) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6261b-178">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="6261b-179">c.</span><span class="sxs-lookup"><span data-stu-id="6261b-179">c.</span></span> <span data-ttu-id="6261b-180">Nella casella di testo **Logout landing URL** (URL di destinazione di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6261b-180">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="6261b-181">d.</span><span class="sxs-lookup"><span data-stu-id="6261b-181">d.</span></span> <span data-ttu-id="6261b-182">Fare clic su **Save my changes**.</span><span class="sxs-lookup"><span data-stu-id="6261b-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="6261b-183">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6261b-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6261b-184">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="6261b-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6261b-185">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6261b-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6261b-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6261b-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="6261b-187">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6261b-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6261b-189">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6261b-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6261b-190">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6261b-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6261b-192">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="6261b-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6261b-194">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="6261b-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6261b-196">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6261b-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6261b-198">a.</span><span class="sxs-lookup"><span data-stu-id="6261b-198">a.</span></span> <span data-ttu-id="6261b-199">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6261b-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6261b-200">b.</span><span class="sxs-lookup"><span data-stu-id="6261b-200">b.</span></span> <span data-ttu-id="6261b-201">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6261b-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6261b-202">c.</span><span class="sxs-lookup"><span data-stu-id="6261b-202">c.</span></span> <span data-ttu-id="6261b-203">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="6261b-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6261b-204">d.</span><span class="sxs-lookup"><span data-stu-id="6261b-204">d.</span></span> <span data-ttu-id="6261b-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6261b-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="6261b-206">Creazione di un utente di test di New Relic</span><span class="sxs-lookup"><span data-stu-id="6261b-206">Creating a New Relic test user</span></span>

<span data-ttu-id="6261b-207">Per consentire agli utenti di Azure Active Directory di accedere a New Relic, è necessario eseguirne il provisioning in New Relic.</span><span class="sxs-lookup"><span data-stu-id="6261b-207">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="6261b-208">Nel caso di New Relic, il provisioning è un’attività manuale.</span><span class="sxs-lookup"><span data-stu-id="6261b-208">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="6261b-209">**Per effettuare il provisioning di un account utente in New Relic, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6261b-209">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="6261b-210">Accedere al sito aziendale di **New Relic** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6261b-210">Log in to your **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="6261b-211">Nel menu in alto fare clic su **Impostazioni account**.</span><span class="sxs-lookup"><span data-stu-id="6261b-211">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="6261b-212">![Impostazioni account](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="6261b-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="6261b-213">Nel riquadro **Account** a sinistra fare clic su **Summary** (Riepilogo), quindi su **Add user** (Aggiungi utente).</span><span class="sxs-lookup"><span data-stu-id="6261b-213">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="6261b-214">![Impostazioni account](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="6261b-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="6261b-215">Nella finestra di dialogo **Active users** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6261b-215">On the **Active users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="6261b-216">![Utenti attivi](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Utenti attivi")</span><span class="sxs-lookup"><span data-stu-id="6261b-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="6261b-217">a.</span><span class="sxs-lookup"><span data-stu-id="6261b-217">a.</span></span> <span data-ttu-id="6261b-218">Nella casella di testo **Posta elettronica** digitare l'indirizzo di posta elettronica di un utente valido di Azure Active Directory di cui si desidera eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="6261b-218">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>

    <span data-ttu-id="6261b-219">b.</span><span class="sxs-lookup"><span data-stu-id="6261b-219">b.</span></span> <span data-ttu-id="6261b-220">Come **Role** (Ruolo) selezionare **User** (Utente).</span><span class="sxs-lookup"><span data-stu-id="6261b-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="6261b-221">c.</span><span class="sxs-lookup"><span data-stu-id="6261b-221">c.</span></span> <span data-ttu-id="6261b-222">Fare clic su **Add this user**.</span><span class="sxs-lookup"><span data-stu-id="6261b-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="6261b-223">È possibile utilizzare qualsiasi altro strumento di creazione di account utente di New Relic o le API fornite da New Relic per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="6261b-223">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6261b-224">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6261b-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6261b-225">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a New Relic.</span><span class="sxs-lookup"><span data-stu-id="6261b-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6261b-227">**Per assegnare Britta Simon a New Relic, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6261b-227">**To assign Britta Simon to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="6261b-228">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6261b-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6261b-230">Nell'elenco delle applicazioni selezionare **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="6261b-230">In the applications list, select **New Relic**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="6261b-232">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6261b-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6261b-234">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6261b-234">Click **Add** button.</span></span> <span data-ttu-id="6261b-235">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6261b-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6261b-237">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="6261b-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6261b-238">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6261b-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6261b-239">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6261b-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6261b-240">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6261b-240">Testing single sign-on</span></span>

<span data-ttu-id="6261b-241">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6261b-241">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6261b-242">Quando si fa clic sul riquadro New Relic nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione New Relic.</span><span class="sxs-lookup"><span data-stu-id="6261b-242">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6261b-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6261b-243">Additional resources</span></span>

* [<span data-ttu-id="6261b-244">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6261b-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6261b-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6261b-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

