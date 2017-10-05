---
title: 'Esercitazione: Integrazione di Azure Active Directory con Panopto | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Panopto.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 725fba1227cfc9c4850f9e2d6fd0b13e88eafa20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="a0407-103">Esercitazione: Integrazione di Azure Active Directory con Panopto</span><span class="sxs-lookup"><span data-stu-id="a0407-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="a0407-104">Questa esercitazione descrive come integrare Panopto con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0407-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0407-105">L'integrazione di Panopto con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0407-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a0407-106">È possibile controllare in Azure AD chi può accedere a Panopto</span><span class="sxs-lookup"><span data-stu-id="a0407-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="a0407-107">È possibile abilitare gli utenti per l'accesso automatico a Panopto (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="a0407-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0407-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0407-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a0407-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0407-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0407-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a0407-110">Prerequisites</span></span>

<span data-ttu-id="a0407-111">Per configurare l'integrazione di Azure AD con Panopto, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0407-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="a0407-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0407-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0407-113">Sottoscrizione di Panopto abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a0407-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0407-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a0407-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0407-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0407-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0407-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a0407-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0407-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0407-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0407-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a0407-118">Scenario description</span></span>
<span data-ttu-id="a0407-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a0407-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0407-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0407-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0407-121">Aggiunta di Panopto dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a0407-121">Adding Panopto from the gallery</span></span>
2. <span data-ttu-id="a0407-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0407-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="a0407-123">Aggiunta di Panopto dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a0407-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="a0407-124">Per configurare l'integrazione di Panopto in Azure AD, è necessario aggiungere Panopto dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a0407-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a0407-125">**Per aggiungere Panopto dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a0407-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a0407-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a0407-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0407-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a0407-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a0407-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a0407-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a0407-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0407-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a0407-133">Nella casella di ricerca digitare **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="a0407-133">In the search box, type **Panopto**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="a0407-135">Nel pannello dei risultati selezionare **Panopto** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0407-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0407-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0407-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a0407-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Panopto usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a0407-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a0407-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Panopto corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0407-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="a0407-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Panopto.</span><span class="sxs-lookup"><span data-stu-id="a0407-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="a0407-141">Per stabilire la relazione di collegamento, in Panopto assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="a0407-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a0407-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Panopto, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0407-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a0407-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a0407-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a0407-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0407-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0407-145">**[Creazione di un utente di test di Panopto](#creating-a-panopto-test-user)**: per avere una controparte di Britta Simon in Panopto collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0407-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0407-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0407-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0407-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a0407-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0407-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0407-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0407-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Panopto.</span><span class="sxs-lookup"><span data-stu-id="a0407-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="a0407-150">**Per configurare l'accesso Single Sign-On di Azure AD con Panopto, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a0407-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="a0407-151">Nella pagina di integrazione dell'applicazione **Panopto** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a0407-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a0407-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a0407-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="a0407-155">Nella sezione **URL e dominio Panopto** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a0407-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="a0407-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="a0407-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0407-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="a0407-158">This value is not real.</span></span> <span data-ttu-id="a0407-159">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="a0407-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a0407-160">Per ottenere questo valore, contattare il [team di supporto di Panopto](mailto:support@panopto.com‎).</span><span class="sxs-lookup"><span data-stu-id="a0407-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
4. <span data-ttu-id="a0407-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="a0407-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="a0407-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a0407-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0407-165">Nella sezione **Configurazione di Panopto** fare clic su **Configura Panopto** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="a0407-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a0407-166">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="a0407-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="a0407-168">In un'altra finestra del Web browser accedere al sito aziendale di Panopto come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a0407-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="a0407-169">Nella barra degli strumenti a sinistra, fare clic su **System** (Sistema) quindi fare clic su **Identity Providers** (Provider di identità).</span><span class="sxs-lookup"><span data-stu-id="a0407-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="a0407-170">![Sistema](./media/active-directory-saas-panopto-tutorial/ic777670.png "Sistema")</span><span class="sxs-lookup"><span data-stu-id="a0407-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="a0407-171">Fare clic su **Aggiungi provider**.</span><span class="sxs-lookup"><span data-stu-id="a0407-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="a0407-172">![Provider di identità](./media/active-directory-saas-panopto-tutorial/ic777671.png "Provider di identità")</span><span class="sxs-lookup"><span data-stu-id="a0407-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="a0407-173">Nella sezione del provider SAML, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a0407-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="a0407-174">![Configurazione SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "Configurazione SaaS")</span><span class="sxs-lookup"><span data-stu-id="a0407-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="a0407-175">a.</span><span class="sxs-lookup"><span data-stu-id="a0407-175">a.</span></span> <span data-ttu-id="a0407-176">Nell'elenco **Provider Type** (Tipo di provider) selezionare **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="a0407-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="a0407-177">b.</span><span class="sxs-lookup"><span data-stu-id="a0407-177">b.</span></span> <span data-ttu-id="a0407-178">Nella casella di testo **Nome istanza** , digitare un nome per l'istanza.</span><span class="sxs-lookup"><span data-stu-id="a0407-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="a0407-179">c.</span><span class="sxs-lookup"><span data-stu-id="a0407-179">c.</span></span> <span data-ttu-id="a0407-180">Nella casella di testo **Descrizione** , digitare una descrizione.</span><span class="sxs-lookup"><span data-stu-id="a0407-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="a0407-181">d.</span><span class="sxs-lookup"><span data-stu-id="a0407-181">d.</span></span> <span data-ttu-id="a0407-182">Nella casella di testo **Bounce Page Url** (URL pagina non recapitata) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0407-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a0407-183">e.</span><span class="sxs-lookup"><span data-stu-id="a0407-183">e.</span></span> <span data-ttu-id="a0407-184">Nella casella di testo **Issuer** (Autorità emittente) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0407-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a0407-185">f.</span><span class="sxs-lookup"><span data-stu-id="a0407-185">f.</span></span> <span data-ttu-id="a0407-186">Aprire nel Blocco note il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **Public Key** (Chiave pubblica).</span><span class="sxs-lookup"><span data-stu-id="a0407-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

11. <span data-ttu-id="a0407-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a0407-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a0407-188">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a0407-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a0407-189">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a0407-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a0407-190">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0407-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0407-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0407-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="a0407-192">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0407-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a0407-194">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a0407-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a0407-195">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a0407-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0407-197">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a0407-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0407-199">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a0407-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0407-201">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a0407-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0407-203">a.</span><span class="sxs-lookup"><span data-stu-id="a0407-203">a.</span></span> <span data-ttu-id="a0407-204">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0407-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0407-205">b.</span><span class="sxs-lookup"><span data-stu-id="a0407-205">b.</span></span> <span data-ttu-id="a0407-206">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0407-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0407-207">c.</span><span class="sxs-lookup"><span data-stu-id="a0407-207">c.</span></span> <span data-ttu-id="a0407-208">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a0407-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a0407-209">d.</span><span class="sxs-lookup"><span data-stu-id="a0407-209">d.</span></span> <span data-ttu-id="a0407-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a0407-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="a0407-211">Creazione di un utente di test di Panopto</span><span class="sxs-lookup"><span data-stu-id="a0407-211">Creating a Panopto test user</span></span>

<span data-ttu-id="a0407-212">Non è richiesto alcun intervento dell'utente per configurare il provisioning degli utenti in Panopto.</span><span class="sxs-lookup"><span data-stu-id="a0407-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="a0407-213">Quando un utente assegnato prova ad accedere a Panopto usando il pannello di accesso, Panopto verifica se l'utente esiste.</span><span class="sxs-lookup"><span data-stu-id="a0407-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="a0407-214">Se l’account utente non è disponibile, viene creato automaticamente da Panopto.</span><span class="sxs-lookup"><span data-stu-id="a0407-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="a0407-215">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerti da Panopto per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0407-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a0407-216">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0407-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a0407-217">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Panopto.</span><span class="sxs-lookup"><span data-stu-id="a0407-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a0407-219">**Per assegnare Britta Simon a Panopto, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a0407-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="a0407-220">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a0407-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a0407-222">Nell'elenco delle applicazioni selezionare **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="a0407-222">In the applications list, select **Panopto**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="a0407-224">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a0407-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a0407-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a0407-226">Click **Add** button.</span></span> <span data-ttu-id="a0407-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a0407-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a0407-229">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a0407-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a0407-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a0407-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0407-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a0407-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0407-232">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a0407-232">Testing single sign-on</span></span>

<span data-ttu-id="a0407-233">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a0407-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a0407-234">Quando si fa clic sul riquadro Panopto nel pannello di accesso, dovrebbe essere visualizzata la pagina di accesso dell'applicazione Panopto.</span><span class="sxs-lookup"><span data-stu-id="a0407-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="a0407-235">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a0407-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0407-236">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a0407-236">Additional resources</span></span>

* [<span data-ttu-id="a0407-237">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0407-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0407-238">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0407-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

