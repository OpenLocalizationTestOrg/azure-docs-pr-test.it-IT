---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zoom | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Zoom.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: aab491f162fd4d24c6ff4d8858f2edd96dda30d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="0e4c3-103">Esercitazione: Integrazione di Azure Active Directory con Zoom</span><span class="sxs-lookup"><span data-stu-id="0e4c3-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="0e4c3-104">Questa esercitazione descrive come integrare Zoom con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e4c3-104">In this tutorial, you learn how to integrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e4c3-105">L'integrazione di Zoom con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-105">Integrating Zoom with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0e4c3-106">È possibile controllare in Azure AD chi può accedere a Zoom.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-106">You can control in Azure AD who has access to Zoom.</span></span>
- <span data-ttu-id="0e4c3-107">È possibile abilitare gli utenti per l'accesso automatico a Zoom (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-107">You can enable your users to automatically get signed-on to Zoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0e4c3-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0e4c3-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e4c3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e4c3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0e4c3-110">Prerequisites</span></span>

<span data-ttu-id="0e4c3-111">Per configurare l'integrazione di Azure AD con Zoom, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-111">To configure Azure AD integration with Zoom, you need the following items:</span></span>

- <span data-ttu-id="0e4c3-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e4c3-113">Sottoscrizione di Zoom abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0e4c3-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e4c3-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e4c3-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e4c3-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e4c3-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e4c3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e4c3-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0e4c3-118">Scenario description</span></span>
<span data-ttu-id="0e4c3-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e4c3-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e4c3-121">Aggiunta di Zoom dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0e4c3-121">Adding Zoom from the gallery</span></span>
2. <span data-ttu-id="0e4c3-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e4c3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-the-gallery"></a><span data-ttu-id="0e4c3-123">Aggiunta di Zoom dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="0e4c3-123">Adding Zoom from the gallery</span></span>
<span data-ttu-id="0e4c3-124">Per configurare l'integrazione di Zoom in Azure AD, è necessario aggiungere Zoom dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-124">To configure the integration of Zoom into Azure AD, you need to add Zoom from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0e4c3-125">**Per aggiungere Zoom dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0e4c3-125">**To add Zoom from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0e4c3-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="0e4c3-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0e4c3-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="0e4c3-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="0e4c3-133">Nella casella di ricerca digitare **Zoom**, selezionare **Zoom** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-133">In the search box, type **Zoom**, select **Zoom** from result panel then click **Add** button to add the application.</span></span>

    ![Zoom nell'elenco risultati](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0e4c3-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e4c3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0e4c3-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zoom usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0e4c3-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e4c3-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Zoom corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoom is to a user in Azure AD.</span></span> <span data-ttu-id="0e4c3-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Zoom.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-138">In other words, a link relationship between an Azure AD user and the related user in Zoom needs to be established.</span></span>

<span data-ttu-id="0e4c3-139">Per stabilire la relazione di collegamento, in Zoom assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="0e4c3-139">In Zoom, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0e4c3-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Zoom, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-140">To configure and test Azure AD single sign-on with Zoom, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0e4c3-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0e4c3-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e4c3-143">**[Creare un utente di test di Zoom](#create-a-zoom-test-user)**: per avere una controparte di Britta Simon in Zoom collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - to have a counterpart of Britta Simon in Zoom that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e4c3-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e4c3-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0e4c3-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e4c3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0e4c3-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Zoom.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="0e4c3-148">**Per configurare l'accesso Single Sign-On di Azure AD con Zoom, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0e4c3-148">**To configure Azure AD single sign-on with Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="0e4c3-149">Nella pagina di integrazione dell'applicazione **Zoom** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-149">In the Azure portal, on the **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="0e4c3-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="0e4c3-153">Nella sezione **URL e dominio Zoom** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-153">On the **Zoom Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="0e4c3-155">a.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-155">a.</span></span> <span data-ttu-id="0e4c3-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.zoom.us`.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="0e4c3-157">b.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-157">b.</span></span> <span data-ttu-id="0e4c3-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="0e4c3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e4c3-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0e4c3-159">These values are not real.</span></span> <span data-ttu-id="0e4c3-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0e4c3-161">Per ottenere questi valori, contattare il [team di supporto clienti di Zoom](https://support.zoom.us/hc).</span><span class="sxs-lookup"><span data-stu-id="0e4c3-161">Contact [Zoom Client support team](https://support.zoom.us/hc) to get these values.</span></span> 
 
4. <span data-ttu-id="0e4c3-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="0e4c3-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0e4c3-164">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e4c3-166">Nella sezione **Configurazione di Zoom** fare clic su **Configura Zoom** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-166">On the **Zoom Configuration** section, click **Configure Zoom** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0e4c3-167">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="0e4c3-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="0e4c3-169">In un'altra finestra del Web browser accedere al sito aziendale di Zoom come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-169">In a different web browser window, log in to your Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="0e4c3-170">Fare clic sulla scheda **Single Sign-On** .</span><span class="sxs-lookup"><span data-stu-id="0e4c3-170">Click the **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="0e4c3-171">![Scheda Single Sign-On](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0e4c3-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="0e4c3-172">Fare clic sulla scheda **Security Control** (Controllo di sicurezza) e quindi passare alle impostazioni **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-172">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="0e4c3-173">Nella sezione Single Sign-On seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-173">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="0e4c3-174">![Sezione Single Sign-On](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0e4c3-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="0e4c3-175">a.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-175">a.</span></span> <span data-ttu-id="0e4c3-176">Nella casella di testo **Sign-in page URL** (URL pagina di accesso) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-176">In the **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="0e4c3-177">b.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-177">b.</span></span> <span data-ttu-id="0e4c3-178">Nella casella di testo **Sign-out page URL** (URL pagina di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-178">In the **Sign-out page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="0e4c3-179">c.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-179">c.</span></span> <span data-ttu-id="0e4c3-180">Aprire il certificato con codifica base 64 nel blocco note, copiarne il contenuto negli appunti e quindi incollarlo nella casella di testo **Identity provider certificate** .</span><span class="sxs-lookup"><span data-stu-id="0e4c3-180">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="0e4c3-181">d.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-181">d.</span></span> <span data-ttu-id="0e4c3-182">Nella casella di testo **Issuer** (Autorità emittente) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-182">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0e4c3-183">e.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-183">e.</span></span> <span data-ttu-id="0e4c3-184">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0e4c3-185">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0e4c3-186">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0e4c3-187">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e4c3-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0e4c3-188">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e4c3-188">Create an Azure AD test user</span></span>

<span data-ttu-id="0e4c3-189">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="0e4c3-191">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0e4c3-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0e4c3-192">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0e4c3-194">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0e4c3-196">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0e4c3-198">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-198">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0e4c3-200">a.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-200">a.</span></span> <span data-ttu-id="0e4c3-201">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e4c3-202">b.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-202">b.</span></span> <span data-ttu-id="0e4c3-203">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0e4c3-204">c.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-204">c.</span></span> <span data-ttu-id="0e4c3-205">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0e4c3-206">d.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-206">d.</span></span> <span data-ttu-id="0e4c3-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="0e4c3-208">Creare un utente di test di Zoom</span><span class="sxs-lookup"><span data-stu-id="0e4c3-208">Create a Zoom test user</span></span>

<span data-ttu-id="0e4c3-209">Per consentire agli utenti di Azure AD di accedere a Zoom, è necessario effettuarne il provisioning in Zoom.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-209">In order to enable Azure AD users to log in to Zoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="0e4c3-210">Nel caso di Zoom, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-210">In the case of Zoom, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="0e4c3-211">Per eseguire il provisioning di un account utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-211">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="0e4c3-212">Accedere al sito aziendale di **Zoom** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-212">Log in to your **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="0e4c3-213">Fare clic sulla scheda **Gestione account** e quindi su **Gestione utente**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-213">Click the **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="0e4c3-214">Nella sezione Gestione utente fare clic su **Aggiungi utenti**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-214">In the User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="0e4c3-215">![Gestione degli utenti](./media/active-directory-saas-zoom-tutorial/IC784703.png "Gestione degli utenti")</span><span class="sxs-lookup"><span data-stu-id="0e4c3-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="0e4c3-216">Nella pagina **Aggiungi utenti** seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0e4c3-216">On the **Add users** page, perform the following steps:</span></span>
   
    <span data-ttu-id="0e4c3-217">![Aggiungere utenti](./media/active-directory-saas-zoom-tutorial/IC784704.png "Aggiungere utenti")</span><span class="sxs-lookup"><span data-stu-id="0e4c3-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="0e4c3-218">a.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-218">a.</span></span> <span data-ttu-id="0e4c3-219">In **Tipo utente** selezionare **Basic**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="0e4c3-220">b.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-220">b.</span></span> <span data-ttu-id="0e4c3-221">Nella casella di testo **Emails** (Messaggi di posta elettronica) digitare l'indirizzo e-mail di un account Azure AD di cui si vuole effettuare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-221">In the **Emails** textbox, type the email address of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="0e4c3-222">c.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-222">c.</span></span> <span data-ttu-id="0e4c3-223">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="0e4c3-224">È possibile usare qualsiasi altro strumento o API di creazione di account utente di Zoom per effettuare il provisioning degli account utente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-224">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision Azure Active Directory user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0e4c3-225">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e4c3-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="0e4c3-226">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Zoom.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoom.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="0e4c3-228">**Per assegnare Britta Simon a Zoom, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0e4c3-228">**To assign Britta Simon to Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="0e4c3-229">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0e4c3-231">Nell'elenco delle applicazioni selezionare **Zoom**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-231">In the applications list, select **Zoom**.</span></span>

    ![Collegamento di Zoom nell'elenco delle applicazioni](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="0e4c3-233">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="0e4c3-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-235">Click **Add** button.</span></span> <span data-ttu-id="0e4c3-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="0e4c3-238">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0e4c3-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e4c3-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0e4c3-241">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0e4c3-241">Test single sign-on</span></span>

<span data-ttu-id="0e4c3-242">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0e4c3-243">Quando si fa clic sul riquadro Zoom nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Zoom.</span><span class="sxs-lookup"><span data-stu-id="0e4c3-243">When you click the Zoom tile in the Access Panel, you should get automatically signed-on to your Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e4c3-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0e4c3-244">Additional resources</span></span>

* [<span data-ttu-id="0e4c3-245">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e4c3-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e4c3-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e4c3-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

