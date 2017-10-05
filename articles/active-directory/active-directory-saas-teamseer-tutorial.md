---
title: 'Esercitazione: Integrazione di Azure Active Directory con TeamSeer | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e TeamSeer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a5e8f6d1443681c43db95da5cef0b7f2ef92291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="f4246-103">Esercitazione: Integrazione di Azure Active Directory con TeamSeer</span><span class="sxs-lookup"><span data-stu-id="f4246-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="f4246-104">Questa esercitazione descrive come integrare TeamSeer con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4246-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4246-105">L'integrazione di TeamSeer con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4246-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f4246-106">È possibile controllare in Azure AD chi può accedere a TeamSeer</span><span class="sxs-lookup"><span data-stu-id="f4246-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="f4246-107">È possibile abilitare gli utenti per l'accesso automatico a TeamSeer (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="f4246-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f4246-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4246-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f4246-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4246-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4246-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f4246-110">Prerequisites</span></span>

<span data-ttu-id="f4246-111">Per configurare l'integrazione di Azure AD con TeamSeer, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4246-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="f4246-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4246-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4246-113">Sottoscrizione di TeamSeer abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f4246-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4246-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f4246-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4246-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4246-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4246-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f4246-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4246-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4246-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4246-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f4246-118">Scenario description</span></span>
<span data-ttu-id="f4246-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f4246-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4246-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4246-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4246-121">Aggiunta di TeamSeer dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f4246-121">Adding TeamSeer from the gallery</span></span>
2. <span data-ttu-id="f4246-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4246-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="f4246-123">Aggiunta di TeamSeer dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f4246-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="f4246-124">Per configurare l'integrazione di TeamSeer in Azure AD, è necessario aggiungere TeamSeer dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f4246-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f4246-125">**Per aggiungere TeamSeer dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f4246-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f4246-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f4246-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f4246-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f4246-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f4246-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f4246-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f4246-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4246-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f4246-133">Nella casella di ricerca digitare **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="f4246-133">In the search box, type **TeamSeer**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="f4246-135">Nel pannello dei risultati selezionare **TeamSeer** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f4246-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f4246-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4246-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f4246-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TeamSeer usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f4246-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f4246-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di TeamSeer corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4246-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="f4246-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="f4246-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="f4246-141">Per stabilire la relazione di collegamento, in TeamSeer assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="f4246-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f4246-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con TeamSeer, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4246-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f4246-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f4246-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f4246-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4246-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4246-145">**[Creazione di un utente di test di TeamSeer](#creating-a-teamseer-test-user)**: per avere una controparte di Britta Simon in TeamSeer collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4246-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4246-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4246-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4246-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f4246-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f4246-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4246-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f4246-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="f4246-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="f4246-150">**Per configurare l'accesso Single Sign-On di Azure AD con TeamSeer, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f4246-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="f4246-151">Nella pagina di integrazione dell'applicazione **TeamSeer** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f4246-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f4246-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f4246-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="f4246-155">Nella sezione **URL e dominio TeamSeer** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f4246-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="f4246-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="f4246-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f4246-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="f4246-158">The value is not real.</span></span> <span data-ttu-id="f4246-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="f4246-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="f4246-160">Per ottenere il valore, contattare il [team di supporto clienti di TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html).</span><span class="sxs-lookup"><span data-stu-id="f4246-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
4. <span data-ttu-id="f4246-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="f4246-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="f4246-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f4246-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f4246-165">Nella sezione **Configurazione di TeamSeer** fare clic su **Configura TeamSeer** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="f4246-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f4246-166">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f4246-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="f4246-168">In un'altra finestra del Web browser accedere al sito aziendale di TeamSeer come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f4246-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="f4246-169">Andare ad **Amministratore risorse umane**.</span><span class="sxs-lookup"><span data-stu-id="f4246-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="f4246-170">![Amministratore risorse umane](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Amministratore risorse umane")</span><span class="sxs-lookup"><span data-stu-id="f4246-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="f4246-171">Fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="f4246-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="f4246-172">![Installazione](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="f4246-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="f4246-173">Fare clic su **Configura dettagli del provider SAML**.</span><span class="sxs-lookup"><span data-stu-id="f4246-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="f4246-174">![Impostazioni SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="f4246-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="f4246-175">Nella sezione dei dettagli del provider SAML, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f4246-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="f4246-176">![Impostazioni SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="f4246-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="f4246-177">a.</span><span class="sxs-lookup"><span data-stu-id="f4246-177">a.</span></span> <span data-ttu-id="f4246-178">Incollare il valore dell'**URL del servizio Single Sign-On** nella casella di testo **URL**.</span><span class="sxs-lookup"><span data-stu-id="f4246-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="f4246-179">b.</span><span class="sxs-lookup"><span data-stu-id="f4246-179">b.</span></span> <span data-ttu-id="f4246-180">Aprire il certificato con codifica Base 64 in Blocco note, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **IdP Public Certificate** (Certificato pubblico IdP).</span><span class="sxs-lookup"><span data-stu-id="f4246-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="f4246-181">Per completare la configurazione del provider SAML eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f4246-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="f4246-182">![Impostazioni SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="f4246-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="f4246-183">a.</span><span class="sxs-lookup"><span data-stu-id="f4246-183">a.</span></span> <span data-ttu-id="f4246-184">In **Test indirizzi e-mail**, digitare l’indirizzo e-mail dell’utente test.</span><span class="sxs-lookup"><span data-stu-id="f4246-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="f4246-185">b.</span><span class="sxs-lookup"><span data-stu-id="f4246-185">b.</span></span> <span data-ttu-id="f4246-186">Nella casella di testo **Autorità di certificazione** digitare l'URL del provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="f4246-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="f4246-187">c.</span><span class="sxs-lookup"><span data-stu-id="f4246-187">c.</span></span> <span data-ttu-id="f4246-188">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f4246-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f4246-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f4246-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f4246-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f4246-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f4246-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4246-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f4246-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4246-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f4246-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4246-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f4246-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f4246-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f4246-196">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f4246-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f4246-198">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="f4246-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f4246-200">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="f4246-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f4246-202">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f4246-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f4246-204">a.</span><span class="sxs-lookup"><span data-stu-id="f4246-204">a.</span></span> <span data-ttu-id="f4246-205">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4246-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4246-206">b.</span><span class="sxs-lookup"><span data-stu-id="f4246-206">b.</span></span> <span data-ttu-id="f4246-207">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f4246-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f4246-208">c.</span><span class="sxs-lookup"><span data-stu-id="f4246-208">c.</span></span> <span data-ttu-id="f4246-209">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="f4246-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f4246-210">d.</span><span class="sxs-lookup"><span data-stu-id="f4246-210">d.</span></span> <span data-ttu-id="f4246-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f4246-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="f4246-212">Creazione di un utente di test di TeamSeer</span><span class="sxs-lookup"><span data-stu-id="f4246-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="f4246-213">Per consentire agli utenti di Azure AD di accedere a TeamSeer, è necessario effettuarne il provisioning in TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="f4246-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="f4246-214">Nel caso di TeamSeer, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f4246-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="f4246-215">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f4246-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f4246-216">Accedere al sito aziendale di **TeamSeer** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f4246-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="f4246-217">Eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f4246-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="f4246-218">![Amministratore risorse umane](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Amministratore risorse umane")</span><span class="sxs-lookup"><span data-stu-id="f4246-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="f4246-219">a.</span><span class="sxs-lookup"><span data-stu-id="f4246-219">a.</span></span> <span data-ttu-id="f4246-220">Accedere a **Amministratore risorse umane \> Utenti**.</span><span class="sxs-lookup"><span data-stu-id="f4246-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="f4246-221">b.</span><span class="sxs-lookup"><span data-stu-id="f4246-221">b.</span></span> <span data-ttu-id="f4246-222">Fare clic su **Esegui procedura guidata nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="f4246-222">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="f4246-223">Nella sezione **Dettagli utente** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f4246-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f4246-224">![Dettagli utente](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Dettagli utente")</span><span class="sxs-lookup"><span data-stu-id="f4246-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="f4246-225">a.</span><span class="sxs-lookup"><span data-stu-id="f4246-225">a.</span></span> <span data-ttu-id="f4246-226">Digitare **Nome**, **Cognome** e **Nome utente (indirizzo di posta elettronica)** di un account AAD valido di cui si vuole effettuare il provisioning nelle caselle di testo correlate.</span><span class="sxs-lookup"><span data-stu-id="f4246-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="f4246-227">b.</span><span class="sxs-lookup"><span data-stu-id="f4246-227">b.</span></span> <span data-ttu-id="f4246-228">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f4246-228">Click **Next**.</span></span>

4. <span data-ttu-id="f4246-229">Seguire le istruzioni visualizzate per l'aggiunta di un nuovo utente e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="f4246-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="f4246-230">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da TeamSeer per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4246-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f4246-231">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4246-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f4246-232">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="f4246-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f4246-234">**Per assegnare Britta Simon a TeamSeer, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f4246-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="f4246-235">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f4246-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f4246-237">Nell'elenco delle applicazioni selezionare **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="f4246-237">In the applications list, select **TeamSeer**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="f4246-239">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f4246-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f4246-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f4246-241">Click **Add** button.</span></span> <span data-ttu-id="f4246-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f4246-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f4246-244">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f4246-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f4246-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f4246-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4246-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f4246-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f4246-247">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f4246-247">Testing single sign-on</span></span>

<span data-ttu-id="f4246-248">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f4246-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f4246-249">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f4246-249">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f4246-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f4246-250">Additional resources</span></span>

* [<span data-ttu-id="f4246-251">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4246-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4246-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4246-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

