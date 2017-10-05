---
title: 'Esercitazione: Integrazione di Azure Active Directory con LogicMonitor | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e LogicMonitor.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e49960cac868f80af3e9165a9f75e49be87515f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="c1f4d-103">Esercitazione: Integrazione di Azure Active Directory con LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="c1f4d-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="c1f4d-104">Questa esercitazione descrive come integrare LogicMonitor con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1f4d-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1f4d-105">L'integrazione di LogicMonitor con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1f4d-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c1f4d-106">È possibile controllare in Azure AD chi può accedere a LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="c1f4d-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="c1f4d-107">È possibile abilitare gli utenti per l'accesso automatico a LogicMonitor (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1f4d-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1f4d-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c1f4d-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1f4d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1f4d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c1f4d-110">Prerequisites</span></span>

<span data-ttu-id="c1f4d-111">Per configurare l'integrazione di Azure AD con LogicMonitor, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1f4d-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="c1f4d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1f4d-113">Sottoscrizione di LogicMonitor abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c1f4d-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1f4d-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1f4d-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1f4d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1f4d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1f4d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1f4d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1f4d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c1f4d-118">Scenario description</span></span>
<span data-ttu-id="c1f4d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1f4d-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1f4d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1f4d-121">Aggiunta di LogicMonitor dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c1f4d-121">Adding LogicMonitor from the gallery</span></span>
2. <span data-ttu-id="c1f4d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1f4d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="c1f4d-123">Aggiunta di LogicMonitor dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c1f4d-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="c1f4d-124">Per configurare l'integrazione di LogicMonitor in Azure AD, è necessario aggiungere LogicMonitor dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c1f4d-125">**Per aggiungere LogicMonitor dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c1f4d-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c1f4d-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1f4d-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c1f4d-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c1f4d-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c1f4d-133">Nella casella di ricerca digitare **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-133">In the search box, type **LogicMonitor**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="c1f4d-135">Nel pannello dei risultati selezionare **LogicMonitor** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1f4d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1f4d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1f4d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LogicMonitor usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c1f4d-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1f4d-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di LogicMonitor che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="c1f4d-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="c1f4d-141">Per stabilire la relazione di collegamento, in LogicMonitor assegnare il valore di **nome utente** di Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c1f4d-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c1f4d-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con LogicMonitor, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1f4d-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c1f4d-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c1f4d-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1f4d-145">**[Creazione di un utente test di LogicMonitor](#creating-a-logicmonitor-test-user)**: per avere una controparte di Britta Simon in LogicMonitor collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1f4d-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1f4d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1f4d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1f4d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1f4d-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="c1f4d-150">**Per configurare l'accesso Single Sign-On di Azure AD con LogicMonitor, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c1f4d-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="c1f4d-151">Nella pagina di integrazione dell'applicazione **LogicMonitor** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c1f4d-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="c1f4d-155">Nella sezione **URL e dominio LogicMonitor** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c1f4d-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="c1f4d-157">a.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-157">a.</span></span> <span data-ttu-id="c1f4d-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.logicmonitor.com`.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="c1f4d-159">b.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-159">b.</span></span> <span data-ttu-id="c1f4d-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="c1f4d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c1f4d-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c1f4d-161">These values are not real.</span></span> <span data-ttu-id="c1f4d-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c1f4d-163">Per ottenere questi valori, contattare il [team di supporto clienti di LogicMonitor](https://www.logicmonitor.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="c1f4d-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="c1f4d-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="c1f4d-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c1f4d-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c1f4d-168">Accedere al sito aziendale di **LogicMonitor** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="c1f4d-169">Nel menu in alto fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-169">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="c1f4d-170">![Impostazioni](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="c1f4d-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="c1f4d-171">Nella barra di spostamento sul lato sinistro fare clic su **Single Sign-On**</span><span class="sxs-lookup"><span data-stu-id="c1f4d-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="c1f4d-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c1f4d-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="c1f4d-173">Nella sezione **Impostazioni Single Sign-on (SSO)** eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c1f4d-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="c1f4d-174">![Impostazioni di Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Impostazioni di Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c1f4d-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="c1f4d-175">a.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-175">a.</span></span> <span data-ttu-id="c1f4d-176">Selezionare **Attiva Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="c1f4d-177">b.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-177">b.</span></span> <span data-ttu-id="c1f4d-178">In **Default Role Assignment** (Assegnazione ruolo predefinito) selezionare **readonly**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="c1f4d-179">c.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-179">c.</span></span> <span data-ttu-id="c1f4d-180">Aprire il file di metadati scaricato in Blocco note, quindi incollare il contenuto del file nella casella di testo **Metadati del provider di identità** .</span><span class="sxs-lookup"><span data-stu-id="c1f4d-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="c1f4d-181">d.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-181">d.</span></span> <span data-ttu-id="c1f4d-182">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="c1f4d-183">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c1f4d-184">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c1f4d-185">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1f4d-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1f4d-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1f4d-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1f4d-187">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c1f4d-189">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c1f4d-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c1f4d-190">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1f4d-192">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1f4d-194">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1f4d-196">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c1f4d-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1f4d-198">a.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-198">a.</span></span> <span data-ttu-id="c1f4d-199">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1f4d-200">b.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-200">b.</span></span> <span data-ttu-id="c1f4d-201">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1f4d-202">c.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-202">c.</span></span> <span data-ttu-id="c1f4d-203">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c1f4d-204">d.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-204">d.</span></span> <span data-ttu-id="c1f4d-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="c1f4d-206">Creazione di un utente test di LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="c1f4d-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="c1f4d-207">Per consentire agli utenti di AAD di accedere, è necessario eseguirne il provisioning nell’applicazione LogicMonitor utilizzando i relativi nomi utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-207">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="c1f4d-208">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c1f4d-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="c1f4d-209">Accedere al sito aziendale di LogicMonitor come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-209">Log in to your LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="c1f4d-210">Nel menu in alto fare clic su **Settings** (Impostazioni) e quindi fare clic su **Roles and Users** (Ruoli e utenti).</span><span class="sxs-lookup"><span data-stu-id="c1f4d-210">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="c1f4d-211">![Ruoli e utenti](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Ruoli e utenti")</span><span class="sxs-lookup"><span data-stu-id="c1f4d-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="c1f4d-212">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-212">Click **Add**.</span></span>

4. <span data-ttu-id="c1f4d-213">Nella sezione **Aggiungi un account** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c1f4d-213">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="c1f4d-214">![Aggiungere un account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Aggiungere un account")</span><span class="sxs-lookup"><span data-stu-id="c1f4d-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="c1f4d-215">a.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-215">a.</span></span> <span data-ttu-id="c1f4d-216">Nelle caselle di testo **Username** (Nome utente), **Email** (Indirizzo di posta elettronica), **Password** e **Retype password** (Conferma password) digitare i valori dell'utente di Azure Active Directory di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-216">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="c1f4d-217">b.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-217">b.</span></span> <span data-ttu-id="c1f4d-218">Selezionare **Roles** (Ruoli), **View Permissions** (Visualizza autorizzazioni) e **Status** (Stato).</span><span class="sxs-lookup"><span data-stu-id="c1f4d-218">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
   <span data-ttu-id="c1f4d-219">c.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-219">c.</span></span> <span data-ttu-id="c1f4d-220">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="c1f4d-221">È possibile utilizzare qualsiasi altro strumento di creazione di account utente di LogicMonitor o le API fornite da LogicMonitor per eseguire il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c1f4d-222">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1f4d-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c1f4d-223">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c1f4d-225">**Per assegnare Britta Simon a LogicMonitor, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c1f4d-225">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="c1f4d-226">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c1f4d-228">Nell'elenco delle applicazioni selezionare **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-228">In the applications list, select **LogicMonitor**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="c1f4d-230">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c1f4d-232">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-232">Click **Add** button.</span></span> <span data-ttu-id="c1f4d-233">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c1f4d-235">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c1f4d-236">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1f4d-237">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1f4d-238">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c1f4d-238">Testing single sign-on</span></span>

<span data-ttu-id="c1f4d-239">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="c1f4d-240">Quando si fa clic sul riquadro LogicMonitor nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="c1f4d-240">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="c1f4d-241">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c1f4d-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c1f4d-242">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c1f4d-242">Additional resources</span></span>

* [<span data-ttu-id="c1f4d-243">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1f4d-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1f4d-244">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1f4d-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

