---
title: 'Esercitazione: Integrazione di Azure Active Directory con Samanage | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Samanage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c54dbe407145a29a712acc3c0fb549a38ac26bed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="56ef6-103">Esercitazione: Integrazione di Azure Active Directory con Samanage</span><span class="sxs-lookup"><span data-stu-id="56ef6-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="56ef6-104">Questa esercitazione descrive come integrare Samanage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56ef6-104">In this tutorial, you learn how to integrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56ef6-105">L'integrazione di Samanage con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="56ef6-105">Integrating Samanage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="56ef6-106">È possibile controllare in Azure AD chi può accedere a Samanage</span><span class="sxs-lookup"><span data-stu-id="56ef6-106">You can control in Azure AD who has access to Samanage</span></span>
- <span data-ttu-id="56ef6-107">È possibile abilitare gli utenti per l'accesso automatico a Samanage (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ef6-107">You can enable your users to automatically get signed-on to Samanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56ef6-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56ef6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="56ef6-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56ef6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56ef6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="56ef6-110">Prerequisites</span></span>

<span data-ttu-id="56ef6-111">Per configurare l'integrazione di Azure AD con Samanage, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="56ef6-111">To configure Azure AD integration with Samanage, you need the following items:</span></span>

- <span data-ttu-id="56ef6-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56ef6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56ef6-113">Sottoscrizione di Samanage abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="56ef6-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56ef6-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="56ef6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56ef6-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="56ef6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56ef6-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="56ef6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56ef6-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56ef6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56ef6-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="56ef6-118">Scenario description</span></span>
<span data-ttu-id="56ef6-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="56ef6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56ef6-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="56ef6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56ef6-121">Aggiunta di Samanage dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="56ef6-121">Adding Samanage from the gallery</span></span>
2. <span data-ttu-id="56ef6-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ef6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="56ef6-123">Aggiunta di Samanage dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="56ef6-123">Adding Samanage from the gallery</span></span>
<span data-ttu-id="56ef6-124">Per configurare l'integrazione di Samanage in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="56ef6-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56ef6-125">**Per aggiungere Samanage dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="56ef6-125">**To add Samanage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56ef6-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="56ef6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="56ef6-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="56ef6-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="56ef6-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="56ef6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="56ef6-133">Nella casella di ricerca digitare **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-133">In the search box, type **Samanage**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="56ef6-135">Nel pannello dei risultati selezionare **Samanage** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="56ef6-135">In the results panel, select **Samanage**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56ef6-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ef6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56ef6-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Samanage in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="56ef6-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56ef6-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Samanage che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56ef6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Samanage is to a user in Azure AD.</span></span> <span data-ttu-id="56ef6-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Samanage.</span><span class="sxs-lookup"><span data-stu-id="56ef6-140">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span></span>

<span data-ttu-id="56ef6-141">Per stabilire la relazione di collegamento, in Samanage assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="56ef6-141">In Samanage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="56ef6-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Samanage, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="56ef6-142">To configure and test Azure AD single sign-on with Samanage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56ef6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="56ef6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="56ef6-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56ef6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56ef6-145">**[Creazione di un utente di test di Samanage](#creating-a-samanage-test-user)** : per avere una controparte di Britta Simon in Samanage collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56ef6-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="56ef6-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56ef6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56ef6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="56ef6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56ef6-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ef6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56ef6-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Samanage.</span><span class="sxs-lookup"><span data-stu-id="56ef6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="56ef6-150">**Per configurare Single Sign-On di Azure AD con Samanage, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="56ef6-150">**To configure Azure AD single sign-on with Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="56ef6-151">Nella pagina di integrazione dell'applicazione **Samanage** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-151">In the Azure portal, on the **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="56ef6-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="56ef6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="56ef6-155">Nella sezione **URL e dominio Samanage** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="56ef6-155">On the **Samanage Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="56ef6-157">a.</span><span class="sxs-lookup"><span data-stu-id="56ef6-157">a.</span></span> <span data-ttu-id="56ef6-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<Company Name>.samanage.com/saml_login/<Company Name>`.</span><span class="sxs-lookup"><span data-stu-id="56ef6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="56ef6-159">b.</span><span class="sxs-lookup"><span data-stu-id="56ef6-159">b.</span></span> <span data-ttu-id="56ef6-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="56ef6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56ef6-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="56ef6-161">These values are not real.</span></span> <span data-ttu-id="56ef6-162">è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi. La procedura è descritta più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="56ef6-162">Update these values with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> <span data-ttu-id="56ef6-163">Per altri dettagli, contattare il [team di supporto clienti di Samanage](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="56ef6-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="56ef6-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="56ef6-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="56ef6-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="56ef6-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="56ef6-168">Nella sezione **Configurazione di Samanage** fare clic su **Configura Samanage** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-168">On the **Samanage Configuration** section, click **Configure Samanage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="56ef6-169">Copiare l'**URL di disconnessione e l'ID di entità SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="56ef6-171">In un'altra finestra del Web browser accedere al sito aziendale di Samanage come amministratore.</span><span class="sxs-lookup"><span data-stu-id="56ef6-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="56ef6-172">Fare clic su **Dashboard** e selezionare **Setup** (Configurazione) nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="56ef6-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="56ef6-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="56ef6-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="56ef6-174">Fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="56ef6-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="56ef6-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="56ef6-176">Nella sezione **Login using SAML** (Accesso tramite SAML) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="56ef6-176">Navigate to **Login using SAML** section, perform the following steps:</span></span>
   
    <span data-ttu-id="56ef6-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span><span class="sxs-lookup"><span data-stu-id="56ef6-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="56ef6-178">a.</span><span class="sxs-lookup"><span data-stu-id="56ef6-178">a.</span></span> <span data-ttu-id="56ef6-179">Fare clic su **Enable Single Sign-On with SAML**(Abilita Single Sign-On con SAML).</span><span class="sxs-lookup"><span data-stu-id="56ef6-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="56ef6-180">b.</span><span class="sxs-lookup"><span data-stu-id="56ef6-180">b.</span></span> <span data-ttu-id="56ef6-181">Nella casella di testo **Identity Provider URL** (URL provider di identità) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56ef6-181">In the **Identity Provider URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="56ef6-182">c.</span><span class="sxs-lookup"><span data-stu-id="56ef6-182">c.</span></span> <span data-ttu-id="56ef6-183">Verificare che **Login URL** (URL di accesso) corrisponda all'**URL di accesso** della sezione **URL e dominio Samanage** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56ef6-183">Confirm the **Login URL** matches the **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="56ef6-184">d.</span><span class="sxs-lookup"><span data-stu-id="56ef6-184">d.</span></span> <span data-ttu-id="56ef6-185">Nella casella di testo **Logout URL** (URL di disconnessione) immettere il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56ef6-185">In the **Logout URL** textbox, enter the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="56ef6-186">e.</span><span class="sxs-lookup"><span data-stu-id="56ef6-186">e.</span></span> <span data-ttu-id="56ef6-187">Nella casella di testo **SAML Issuer** (Autorità di certificazione SAML) digitare l'URI ID app impostato nel provider di identità.</span><span class="sxs-lookup"><span data-stu-id="56ef6-187">In the **SAML Issuer** textbox, type the app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="56ef6-188">f.</span><span class="sxs-lookup"><span data-stu-id="56ef6-188">f.</span></span> <span data-ttu-id="56ef6-189">Aprire il certificato con codifica Base 64 scaricato dal portale di Azure nel Blocco note, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **Paste your Identity Provider x.509 Certificate below** (Incollare il certificato X.509 del provider di identità di seguito).</span><span class="sxs-lookup"><span data-stu-id="56ef6-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="56ef6-190">g.</span><span class="sxs-lookup"><span data-stu-id="56ef6-190">g.</span></span> <span data-ttu-id="56ef6-191">Fare clic su **Create users if they do not exist in Samanage**(Crea utenti se non presenti in Samanage).</span><span class="sxs-lookup"><span data-stu-id="56ef6-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="56ef6-192">h.</span><span class="sxs-lookup"><span data-stu-id="56ef6-192">h.</span></span> <span data-ttu-id="56ef6-193">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="56ef6-194">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="56ef6-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="56ef6-195">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="56ef6-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="56ef6-196">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56ef6-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56ef6-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ef6-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="56ef6-198">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56ef6-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="56ef6-200">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="56ef6-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56ef6-201">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="56ef6-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56ef6-203">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="56ef6-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56ef6-205">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56ef6-207">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="56ef6-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56ef6-209">a.</span><span class="sxs-lookup"><span data-stu-id="56ef6-209">a.</span></span> <span data-ttu-id="56ef6-210">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56ef6-211">b.</span><span class="sxs-lookup"><span data-stu-id="56ef6-211">b.</span></span> <span data-ttu-id="56ef6-212">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56ef6-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56ef6-213">c.</span><span class="sxs-lookup"><span data-stu-id="56ef6-213">c.</span></span> <span data-ttu-id="56ef6-214">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="56ef6-215">d.</span><span class="sxs-lookup"><span data-stu-id="56ef6-215">d.</span></span> <span data-ttu-id="56ef6-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="56ef6-217">Creazione di un utente test per Samanage</span><span class="sxs-lookup"><span data-stu-id="56ef6-217">Creating a Samanage test user</span></span>

<span data-ttu-id="56ef6-218">Per consentire agli utenti di Azure AD di accedere a Samanage, è necessario effettuarne il provisioning in Samanage.</span><span class="sxs-lookup"><span data-stu-id="56ef6-218">To enable Azure AD users to log in to Samanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="56ef6-219">Nel caso di Samanage, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="56ef6-219">In the case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="56ef6-220">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="56ef6-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="56ef6-221">Accedere al sito aziendale di Samanage come amministratore.</span><span class="sxs-lookup"><span data-stu-id="56ef6-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="56ef6-222">Fare clic su **Dashboard** e selezionare **Setup** (Configurazione) nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="56ef6-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="56ef6-223">![Installazione](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="56ef6-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="56ef6-224">Fare clic sulla scheda **Users** .</span><span class="sxs-lookup"><span data-stu-id="56ef6-224">Click the **Users** tab</span></span>
   
    <span data-ttu-id="56ef6-225">![Utenti](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="56ef6-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="56ef6-226">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-226">Click **New User**.</span></span>
   
    <span data-ttu-id="56ef6-227">![Nuovo utente](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="56ef6-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="56ef6-228">In **Name** (Nome) e **Email Address** (Indirizzo di posta elettronica) digitare nome e indirizzo di posta elettronica di un account Azure Active Directory di cui si vuole effettuare il provisioning e fare clic su **Create user** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="56ef6-228">Type the **Name** and the **Email Address** of an Azure Active Directory account you want to provision and click **Create user**.</span></span>
   
    <span data-ttu-id="56ef6-229">![Crea utente](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="56ef6-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="56ef6-230">Il titolare dell'account Azure Active Directory riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="56ef6-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="56ef6-231">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerti da Samanage per eseguire il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="56ef6-231">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="56ef6-232">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="56ef6-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="56ef6-233">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Samanage.</span><span class="sxs-lookup"><span data-stu-id="56ef6-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Samanage.</span></span>

![Assegna utente][200] 

<span data-ttu-id="56ef6-235">**Per assegnare Britta Simon a Samanage, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="56ef6-235">**To assign Britta Simon to Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="56ef6-236">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="56ef6-238">Nell'elenco di applicazioni selezionare **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-238">In the applications list, select **Samanage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="56ef6-240">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="56ef6-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="56ef6-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-242">Click **Add** button.</span></span> <span data-ttu-id="56ef6-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="56ef6-245">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="56ef6-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="56ef6-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56ef6-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="56ef6-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56ef6-248">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="56ef6-248">Testing single sign-on</span></span>

<span data-ttu-id="56ef6-249">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="56ef6-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="56ef6-250">Quando si fa clic sul riquadro Samanage nel pannello di accesso, verrà eseguito automaticamente l'accesso all'applicazione Samanage.</span><span class="sxs-lookup"><span data-stu-id="56ef6-250">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span></span>
<span data-ttu-id="56ef6-251">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="56ef6-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56ef6-252">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="56ef6-252">Additional resources</span></span>

* [<span data-ttu-id="56ef6-253">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56ef6-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56ef6-254">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56ef6-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

