---
title: 'Esercitazione: Integrazione di Azure Active Directory con Sprinklr | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Sprinklr.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 6e1622cd55e3b0e8063604ac9dc0cb0673fa9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="08b55-103">Esercitazione: Integrazione di Azure Active Directory con Sprinklr</span><span class="sxs-lookup"><span data-stu-id="08b55-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="08b55-104">Questa esercitazione descrive come integrare Sprinklr con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="08b55-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08b55-105">L'integrazione di Sprinklr con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="08b55-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="08b55-106">È possibile controllare in Azure AD chi può accedere a Sprinklr</span><span class="sxs-lookup"><span data-stu-id="08b55-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="08b55-107">È possibile abilitare gli utenti per l'accesso automatico a Sprinklr (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="08b55-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="08b55-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="08b55-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="08b55-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08b55-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08b55-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="08b55-110">Prerequisites</span></span>

<span data-ttu-id="08b55-111">Per configurare l'integrazione di Azure AD con Sprinklr, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="08b55-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="08b55-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08b55-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08b55-113">Sottoscrizione di Sprinklr abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="08b55-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08b55-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="08b55-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08b55-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="08b55-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08b55-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="08b55-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08b55-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08b55-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08b55-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="08b55-118">Scenario description</span></span>
<span data-ttu-id="08b55-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="08b55-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08b55-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="08b55-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08b55-121">Aggiunta di Sprinklr dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="08b55-121">Adding Sprinklr from the gallery</span></span>
2. <span data-ttu-id="08b55-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b55-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="08b55-123">Aggiunta di Sprinklr dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="08b55-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="08b55-124">Per configurare l'integrazione di Sprinklr in Azure AD, è necessario aggiungere Sprinklr dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="08b55-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="08b55-125">**Per aggiungere Sprinklr dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="08b55-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="08b55-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="08b55-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="08b55-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="08b55-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="08b55-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="08b55-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="08b55-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="08b55-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="08b55-133">Nella casella di ricerca digitare **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="08b55-133">In the search box, type **Sprinklr**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="08b55-135">Nel pannello dei risultati selezionare **Sprinklr** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08b55-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="08b55-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b55-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="08b55-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Sprinklr usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="08b55-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="08b55-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Sprinklr corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08b55-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="08b55-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="08b55-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="08b55-141">Per stabilire la relazione di collegamento, in Sprinklr assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="08b55-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="08b55-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Sprinklr, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="08b55-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="08b55-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="08b55-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="08b55-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08b55-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08b55-145">**[Creazione di un utente di test di Sprinklr](#creating-a-sprinklr-test-user)**: per avere una controparte di Britta Simon in Sprinklr collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08b55-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="08b55-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08b55-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08b55-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="08b55-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="08b55-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b55-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="08b55-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="08b55-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="08b55-150">**Per configurare l'accesso Single Sign-On di Azure AD con Sprinklr, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="08b55-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="08b55-151">Nella pagina di integrazione dell'applicazione **Sprinklr** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="08b55-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="08b55-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="08b55-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="08b55-155">Nella sezione **URL e dominio Sprinklr** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="08b55-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="08b55-157">a.</span><span class="sxs-lookup"><span data-stu-id="08b55-157">a.</span></span> <span data-ttu-id="08b55-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.sprinklr.com`.</span><span class="sxs-lookup"><span data-stu-id="08b55-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="08b55-159">b.</span><span class="sxs-lookup"><span data-stu-id="08b55-159">b.</span></span> <span data-ttu-id="08b55-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="08b55-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08b55-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="08b55-161">These values are not real.</span></span> <span data-ttu-id="08b55-162">aggiornarli con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="08b55-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="08b55-163">Per ottenere questi valori, contattare il [team di supporto clienti di Sprinklr](https://www.sprinklr.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="08b55-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="08b55-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="08b55-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="08b55-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="08b55-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="08b55-168">Nella sezione **Configurazione di Sprinklr** fare clic su **Configura Sprinklr** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="08b55-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="08b55-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="08b55-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

7. <span data-ttu-id="08b55-170">In un'altra finestra del Web browser accedere al sito aziendale di Sprinklr come amministratore.</span><span class="sxs-lookup"><span data-stu-id="08b55-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="08b55-171">Passare ad **Administration (Amministrazione) \> Settings (Impostazioni)**.</span><span class="sxs-lookup"><span data-stu-id="08b55-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="08b55-172">![Amministrazione](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="08b55-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="08b55-173">Passare a **Manage Partner (Gestisci partner) \> Single Sign (Accesso singolo)** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="08b55-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="08b55-174">![Gestione partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Gestione partner")</span><span class="sxs-lookup"><span data-stu-id="08b55-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="08b55-175">Fare clic su **+ Add Single Sign Ons**.</span><span class="sxs-lookup"><span data-stu-id="08b55-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="08b55-176">![Accessi Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Accessi Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="08b55-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="08b55-177">Nella pagina **Single Sign On** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="08b55-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="08b55-178">![Accessi Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Accessi Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="08b55-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="08b55-179">a.</span><span class="sxs-lookup"><span data-stu-id="08b55-179">a.</span></span> <span data-ttu-id="08b55-180">Nella casella di testo **Name** (Nome) digitare un nome per la configurazione (ad esempio *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="08b55-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="08b55-181">b.</span><span class="sxs-lookup"><span data-stu-id="08b55-181">b.</span></span> <span data-ttu-id="08b55-182">Selezionare **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="08b55-182">Select **Enabled**.</span></span>

    <span data-ttu-id="08b55-183">c.</span><span class="sxs-lookup"><span data-stu-id="08b55-183">c.</span></span> <span data-ttu-id="08b55-184">Selezionare **Use new SSO Certificate**.</span><span class="sxs-lookup"><span data-stu-id="08b55-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="08b55-185">e.</span><span class="sxs-lookup"><span data-stu-id="08b55-185">e.</span></span> <span data-ttu-id="08b55-186">Aprire il certificato con codifica Base 64 nel Blocco note, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **Certificato provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="08b55-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="08b55-187">f.</span><span class="sxs-lookup"><span data-stu-id="08b55-187">f.</span></span> <span data-ttu-id="08b55-188">Incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure nella casella di testo **ID entità**.</span><span class="sxs-lookup"><span data-stu-id="08b55-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="08b55-189">g.</span><span class="sxs-lookup"><span data-stu-id="08b55-189">g.</span></span> <span data-ttu-id="08b55-190">Incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **URL di accesso provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="08b55-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="08b55-191">h.</span><span class="sxs-lookup"><span data-stu-id="08b55-191">h.</span></span> <span data-ttu-id="08b55-192">Incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure nella casella di testo **URL di disconnessione provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="08b55-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="08b55-193">i.</span><span class="sxs-lookup"><span data-stu-id="08b55-193">i.</span></span> <span data-ttu-id="08b55-194">In **SAML User ID Type** (Tipo ID utente SAML) selezionare **Assertion contains User”s sprinklr.com username** (L'asserzione contiene il nome utente sprinklr.com dell'utente).</span><span class="sxs-lookup"><span data-stu-id="08b55-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="08b55-195">j.</span><span class="sxs-lookup"><span data-stu-id="08b55-195">j.</span></span> <span data-ttu-id="08b55-196">In **SAML User ID Location** (Percorso ID utente SAML) selezionare **User ID is in the Name Identifier element of the Subject statement** (L'ID utente è nell'elemento identificatore nome dell'istruzione Subject).</span><span class="sxs-lookup"><span data-stu-id="08b55-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="08b55-197">k.</span><span class="sxs-lookup"><span data-stu-id="08b55-197">k.</span></span> <span data-ttu-id="08b55-198">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="08b55-198">Click **Save**.</span></span>
       
    <span data-ttu-id="08b55-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="08b55-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="08b55-200">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="08b55-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="08b55-201">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="08b55-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="08b55-202">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="08b55-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="08b55-203">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b55-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="08b55-204">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="08b55-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="08b55-206">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="08b55-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="08b55-207">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="08b55-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="08b55-209">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="08b55-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="08b55-211">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="08b55-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08b55-213">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="08b55-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08b55-215">a.</span><span class="sxs-lookup"><span data-stu-id="08b55-215">a.</span></span> <span data-ttu-id="08b55-216">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08b55-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08b55-217">b.</span><span class="sxs-lookup"><span data-stu-id="08b55-217">b.</span></span> <span data-ttu-id="08b55-218">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="08b55-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08b55-219">c.</span><span class="sxs-lookup"><span data-stu-id="08b55-219">c.</span></span> <span data-ttu-id="08b55-220">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="08b55-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="08b55-221">d.</span><span class="sxs-lookup"><span data-stu-id="08b55-221">d.</span></span> <span data-ttu-id="08b55-222">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="08b55-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="08b55-223">Creazione di un utente di test di Sprinklr</span><span class="sxs-lookup"><span data-stu-id="08b55-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="08b55-224">Accedere al sito aziendale di Sprinklr come amministratore.</span><span class="sxs-lookup"><span data-stu-id="08b55-224">Log in to your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="08b55-225">Passare ad **Administration (Amministrazione) \> Settings (Impostazioni)**.</span><span class="sxs-lookup"><span data-stu-id="08b55-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="08b55-226">![Amministrazione](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="08b55-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="08b55-227">Passare a **Manage Client (Gestisci client) \> Users (Utenti)** dal riquadro di sinistra.</span><span class="sxs-lookup"><span data-stu-id="08b55-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="08b55-228">![Impostazioni](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="08b55-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="08b55-229">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="08b55-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="08b55-230">![Impostazioni](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="08b55-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="08b55-231">Nella finestra di dialogo **Edit User** seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="08b55-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="08b55-232">![Modifica degli utenti](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Modifica degli utenti")</span><span class="sxs-lookup"><span data-stu-id="08b55-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="08b55-233">a.</span><span class="sxs-lookup"><span data-stu-id="08b55-233">a.</span></span> <span data-ttu-id="08b55-234">Nelle caselle di testo **Email** (E-mail), **First name** (Nome) e **Last name** (Cognome) digitare i dati di un account utente di Azure AD di cui eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="08b55-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="08b55-235">b.</span><span class="sxs-lookup"><span data-stu-id="08b55-235">b.</span></span> <span data-ttu-id="08b55-236">Selezionare **Password disabled**.</span><span class="sxs-lookup"><span data-stu-id="08b55-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="08b55-237">c.</span><span class="sxs-lookup"><span data-stu-id="08b55-237">c.</span></span> <span data-ttu-id="08b55-238">Selezionare **Language** (Lingua).</span><span class="sxs-lookup"><span data-stu-id="08b55-238">Select **Language**.</span></span>

    <span data-ttu-id="08b55-239">d.</span><span class="sxs-lookup"><span data-stu-id="08b55-239">d.</span></span> <span data-ttu-id="08b55-240">Selezionare **User Type** (Tipo di utente).</span><span class="sxs-lookup"><span data-stu-id="08b55-240">Select **User Type**.</span></span>

    <span data-ttu-id="08b55-241">e.</span><span class="sxs-lookup"><span data-stu-id="08b55-241">e.</span></span> <span data-ttu-id="08b55-242">Fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="08b55-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="08b55-243">**Password disabled** deve essere selezionata per consentire agli utenti di accedere tramite un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="08b55-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="08b55-244">Passare a **Role**ed eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="08b55-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="08b55-245">![Ruoli partner](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Ruoli partner")</span><span class="sxs-lookup"><span data-stu-id="08b55-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="08b55-246">a.</span><span class="sxs-lookup"><span data-stu-id="08b55-246">a.</span></span> <span data-ttu-id="08b55-247">Dall'elenco **Global** (Globale), selezionare **ALL\_Permissions** (Tutte le autorizzazioni).</span><span class="sxs-lookup"><span data-stu-id="08b55-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="08b55-248">b.</span><span class="sxs-lookup"><span data-stu-id="08b55-248">b.</span></span> <span data-ttu-id="08b55-249">Fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="08b55-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="08b55-250">È possibile usare qualsiasi altro strumento di creazione di account utente di Sprinklr o API fornita da Sprinklr per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08b55-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="08b55-251">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="08b55-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="08b55-252">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="08b55-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![Assegna utente][200] 

<span data-ttu-id="08b55-254">**Per assegnare Britta Simon a Sprinklr, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="08b55-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="08b55-255">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="08b55-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="08b55-257">Nell'elenco delle applicazioni selezionare **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="08b55-257">In the applications list, select **Sprinklr**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="08b55-259">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="08b55-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="08b55-261">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="08b55-261">Click **Add** button.</span></span> <span data-ttu-id="08b55-262">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="08b55-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="08b55-264">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="08b55-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="08b55-265">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="08b55-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08b55-266">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="08b55-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="08b55-267">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="08b55-267">Testing single sign-on</span></span>

<span data-ttu-id="08b55-268">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="08b55-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="08b55-269">Quando si fa clic sul riquadro Sprinklr nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Sprinklr. Per altre informazioni sul pannello di accesso, vedere [Introduzione al pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="08b55-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="08b55-270">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="08b55-270">Additional resources</span></span>

* [<span data-ttu-id="08b55-271">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08b55-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08b55-272">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08b55-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

