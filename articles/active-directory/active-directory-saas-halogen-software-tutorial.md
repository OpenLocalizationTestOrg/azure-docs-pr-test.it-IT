---
title: 'Esercitazione: Integrazione di Azure Active Directory con Halogen Software | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Halogen Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="c190f-103">Esercitazione: Integrazione di Azure Active Directory con Halogen Software</span><span class="sxs-lookup"><span data-stu-id="c190f-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="c190f-104">Questa esercitazione descrive come integrare Halogen Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c190f-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c190f-105">L'integrazione di Halogen Software con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c190f-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c190f-106">È possibile controllare in Azure AD chi può accedere a Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="c190f-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="c190f-107">È possibile abilitare gli utenti per l'accesso automatico a Halogen Software (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c190f-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c190f-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c190f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c190f-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c190f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c190f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c190f-110">Prerequisites</span></span>

<span data-ttu-id="c190f-111">Per configurare l'integrazione di Azure AD con Halogen Software, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c190f-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="c190f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c190f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c190f-113">Sottoscrizione di Halogen Software abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c190f-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c190f-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c190f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c190f-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c190f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c190f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c190f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c190f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c190f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c190f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c190f-118">Scenario description</span></span>

<span data-ttu-id="c190f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c190f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c190f-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c190f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c190f-121">Aggiunta di Halogen Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c190f-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="c190f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c190f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="c190f-123">Aggiunta di Halogen Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c190f-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="c190f-124">Per configurare l'integrazione di Halogen Software in Azure AD, è necessario aggiungere Halogen Software dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c190f-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c190f-125">**Per aggiungere Halogen Software dalla raccolta, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c190f-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c190f-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c190f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c190f-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c190f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c190f-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c190f-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c190f-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c190f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c190f-133">Nella casella di ricerca digitare **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="c190f-133">In the search box, type **Halogen Software**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="c190f-135">Nel pannello dei risultati selezionare **Halogen Software** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c190f-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c190f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c190f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c190f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Halogen Software mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c190f-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c190f-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Halogen Software corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c190f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="c190f-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="c190f-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="c190f-141">Per stabilire la relazione di collegamento, in Halogen Software assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c190f-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c190f-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Halogen Software, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c190f-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c190f-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c190f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c190f-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c190f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c190f-145">**[Creazione di un utente test di Halogen Software](#creating-a-halogen-software-test-user)**: per avere una controparte di Britta Simon in Halogen Software collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c190f-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c190f-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c190f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c190f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c190f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c190f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c190f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c190f-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="c190f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="c190f-150">**Per configurare Single Sign-On di Azure AD con Halogen Software, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c190f-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="c190f-151">Nella pagina di integrazione dell'applicazione **Halogen Software** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c190f-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c190f-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c190f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="c190f-155">Nella sezione **URL e dominio Halogen Software** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c190f-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="c190f-157">a.</span><span class="sxs-lookup"><span data-stu-id="c190f-157">a.</span></span> <span data-ttu-id="c190f-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://global.hgncloud.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="c190f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="c190f-159">b.</span><span class="sxs-lookup"><span data-stu-id="c190f-159">b.</span></span> <span data-ttu-id="c190f-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c190f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c190f-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c190f-161">These values are not real.</span></span> <span data-ttu-id="c190f-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="c190f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c190f-163">Per ottenere questi valori contattare il [team di supporto clienti di Halogen Software](https://support.halogensoftware.com/).</span><span class="sxs-lookup"><span data-stu-id="c190f-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="c190f-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="c190f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="c190f-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c190f-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c190f-168">In una finestra del browser diversa accedere all'applicazione **Software alogeno** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c190f-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="c190f-169">Scegliere la scheda **Options (Opzioni)** .</span><span class="sxs-lookup"><span data-stu-id="c190f-169">Click the **Options** tab.</span></span> 
   
    ![Cos'è Azure AD Connect][12]

8. <span data-ttu-id="c190f-171">Nel riquadro di spostamento a sinistra fare clic su **SAML Configuration**.</span><span class="sxs-lookup"><span data-stu-id="c190f-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Cos'è Azure AD Connect][13]

9. <span data-ttu-id="c190f-173">Nella pagina **Configurazione SAML** seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c190f-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![Cos'è Azure AD Connect][14]

     <span data-ttu-id="c190f-175">a.</span><span class="sxs-lookup"><span data-stu-id="c190f-175">a.</span></span> <span data-ttu-id="c190f-176">Come **Identificatore univoco**, selezionare **NameID**.</span><span class="sxs-lookup"><span data-stu-id="c190f-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="c190f-177">b.</span><span class="sxs-lookup"><span data-stu-id="c190f-177">b.</span></span> <span data-ttu-id="c190f-178">Come **Unique Identifier Maps To** (L'identificatore univoco mappa verso) selezionare **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c190f-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="c190f-179">c.</span><span class="sxs-lookup"><span data-stu-id="c190f-179">c.</span></span> <span data-ttu-id="c190f-180">Per caricare il file di metadati fare clic su **Browse** (Sfoglia) per selezionare il file e quindi fare clic su **Upload File** (Carica file).</span><span class="sxs-lookup"><span data-stu-id="c190f-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="c190f-181">d.</span><span class="sxs-lookup"><span data-stu-id="c190f-181">d.</span></span> <span data-ttu-id="c190f-182">Per testare la configurazione, fare clic su **Run Test**.</span><span class="sxs-lookup"><span data-stu-id="c190f-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="c190f-183">È necessario attendere la visualizzazione del messaggio"*The SAML test is complete. Please close this window*".</span><span class="sxs-lookup"><span data-stu-id="c190f-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="c190f-184">chiudere quindi la ginestra del browser aperta.</span><span class="sxs-lookup"><span data-stu-id="c190f-184">Then, close the opened browser window.</span></span> <span data-ttu-id="c190f-185">La casella di controllo **Enable SAML** (Abilita SAML) è selezionata solo se il test è stato completato.</span><span class="sxs-lookup"><span data-stu-id="c190f-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="c190f-186">e.</span><span class="sxs-lookup"><span data-stu-id="c190f-186">e.</span></span> <span data-ttu-id="c190f-187">Selezionare **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="c190f-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="c190f-188">f.</span><span class="sxs-lookup"><span data-stu-id="c190f-188">f.</span></span> <span data-ttu-id="c190f-189">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="c190f-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="c190f-190">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c190f-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c190f-191">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c190f-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c190f-192">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c190f-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c190f-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c190f-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="c190f-194">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c190f-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c190f-196">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c190f-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c190f-197">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c190f-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c190f-199">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="c190f-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c190f-201">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="c190f-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c190f-203">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c190f-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c190f-205">a.</span><span class="sxs-lookup"><span data-stu-id="c190f-205">a.</span></span> <span data-ttu-id="c190f-206">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c190f-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="c190f-207">b.</span><span class="sxs-lookup"><span data-stu-id="c190f-207">b.</span></span> <span data-ttu-id="c190f-208">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c190f-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c190f-209">c.</span><span class="sxs-lookup"><span data-stu-id="c190f-209">c.</span></span> <span data-ttu-id="c190f-210">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="c190f-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c190f-211">d.</span><span class="sxs-lookup"><span data-stu-id="c190f-211">d.</span></span> <span data-ttu-id="c190f-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c190f-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="c190f-213">Creazione di un utente test di Halogen Software</span><span class="sxs-lookup"><span data-stu-id="c190f-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="c190f-214">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="c190f-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="c190f-215">**Per creare un utente test denominato Britta Simon in Halogen Software, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c190f-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="c190f-216">Accedere all'applicazione **Halogen Software** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c190f-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="c190f-217">Fare clic sulla scheda **User Center** (Centro utenti) e quindi su **Create User** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="c190f-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![Cos'è Azure AD Connect][300]  

3. <span data-ttu-id="c190f-219">Nella pagina **Nuovo utente** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c190f-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![Cos'è Azure AD Connect][301]

    <span data-ttu-id="c190f-221">a.</span><span class="sxs-lookup"><span data-stu-id="c190f-221">a.</span></span> <span data-ttu-id="c190f-222">Digitare il nome dell'utente, ad esempio **Britta**, nella casella di testo **First Name** (Nome).</span><span class="sxs-lookup"><span data-stu-id="c190f-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="c190f-223">b.</span><span class="sxs-lookup"><span data-stu-id="c190f-223">b.</span></span> <span data-ttu-id="c190f-224">Digitare il cognome dell'utente, ad esempio **Simon**, nella casella di testo **Last Name** (Cognome).</span><span class="sxs-lookup"><span data-stu-id="c190f-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="c190f-225">c.</span><span class="sxs-lookup"><span data-stu-id="c190f-225">c.</span></span> <span data-ttu-id="c190f-226">Nella casella di testo **Username** (Nome utente) digitare **Britta Simon**, il nome utente che appare nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c190f-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="c190f-227">d.</span><span class="sxs-lookup"><span data-stu-id="c190f-227">d.</span></span> <span data-ttu-id="c190f-228">Nella casella di testo **Password** digitare una password per Britta.</span><span class="sxs-lookup"><span data-stu-id="c190f-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="c190f-229">e.</span><span class="sxs-lookup"><span data-stu-id="c190f-229">e.</span></span> <span data-ttu-id="c190f-230">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="c190f-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c190f-231">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c190f-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c190f-232">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="c190f-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c190f-234">**Per assegnare Britta Simon a Halogen Software, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c190f-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="c190f-235">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c190f-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c190f-237">Nell'elenco di applicazioni selezionare **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="c190f-237">In the applications list, select **Halogen Software**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="c190f-239">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c190f-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c190f-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c190f-241">Click **Add** button.</span></span> <span data-ttu-id="c190f-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c190f-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c190f-244">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c190f-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c190f-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c190f-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c190f-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c190f-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c190f-247">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c190f-247">Testing single sign-on</span></span>

<span data-ttu-id="c190f-248">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c190f-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c190f-249">Quando si fa clic sul riquadro Halogen Software nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="c190f-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c190f-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c190f-250">Additional resources</span></span>

* [<span data-ttu-id="c190f-251">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c190f-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c190f-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c190f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
