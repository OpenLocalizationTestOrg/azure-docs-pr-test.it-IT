---
title: 'Esercitazione: Integrazione di Azure Active Directory con MOVEit Transfer - Azure AD integration | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e MOVEit Transfer - Azure AD integration.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: d35aceb9be2d0ff49f86a00cc84f5deb198d88f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="f27a9-103">Esercitazione: Integrazione di Azure Active Directory con MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="f27a9-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="f27a9-104">Questa esercitazione descrive come integrare MOVEit Transfer - Azure AD integration con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f27a9-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f27a9-105">L'integrazione di MOVEit Transfer - Azure AD integration con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f27a9-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f27a9-106">È possibile controllare in Azure AD chi può accedere a MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="f27a9-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="f27a9-107">È possibile abilitare gli utenti per l'accesso automatico a MOVEit Transfer - Azure AD integration (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="f27a9-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f27a9-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f27a9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f27a9-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f27a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f27a9-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f27a9-110">Prerequisites</span></span>

<span data-ttu-id="f27a9-111">Per configurare l'integrazione di Azure AD con MOVEit Transfer - Azure AD integration, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f27a9-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span></span>

- <span data-ttu-id="f27a9-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f27a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f27a9-113">Sottoscrizione di MOVEit Transfer - Azure AD integration abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f27a9-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f27a9-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f27a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f27a9-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f27a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f27a9-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f27a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f27a9-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f27a9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f27a9-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f27a9-118">Scenario description</span></span>
<span data-ttu-id="f27a9-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f27a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f27a9-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f27a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f27a9-121">Aggiunta di MOVEit Transfer - Azure AD integration dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f27a9-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
2. <span data-ttu-id="f27a9-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f27a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a><span data-ttu-id="f27a9-123">Aggiunta di MOVEit Transfer - Azure AD integration dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f27a9-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
<span data-ttu-id="f27a9-124">Per configurare l'integrazione di MOVEit Transfer - Azure AD integration in Azure AD, è necessario aggiungere MOVEit Transfer - Azure AD integration dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f27a9-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f27a9-125">**Per aggiungere MOVEit Transfer - Azure AD integration dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f27a9-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f27a9-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f27a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="f27a9-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f27a9-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="f27a9-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="f27a9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="f27a9-133">Nella casella di ricerca digitare **MOVEit Transfer - Azure AD integration**, selezionare **MOVEit Transfer - Azure AD integration** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f27a9-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span></span>

    ![MOVEit Transfer - Azure AD integration nell'elenco risultati](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f27a9-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f27a9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f27a9-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con MOVEit Transfer - Azure AD integration usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f27a9-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f27a9-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di MOVEit Transfer - Azure AD integration corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f27a9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span></span> <span data-ttu-id="f27a9-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="f27a9-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span></span>

<span data-ttu-id="f27a9-139">Per stabilire la relazione di collegamento, in MOVEit Transfer - Azure AD integration assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="f27a9-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f27a9-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con MOVEit Transfer - Azure AD integration, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="f27a9-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f27a9-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f27a9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f27a9-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f27a9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f27a9-143">**[Creare un utente di test di MOVEit Transfer - Azure AD integration](#create-a-moveit-transfer---azure-ad-integration-test-user)**: per avere una controparte di Britta Simon in MOVEit Transfer - Azure AD integration collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f27a9-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f27a9-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f27a9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f27a9-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f27a9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f27a9-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f27a9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f27a9-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="f27a9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="f27a9-148">**Per configurare l'accesso Single Sign-On di Azure AD con MOVEit Transfer - Azure AD integration, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f27a9-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="f27a9-149">Nella pagina di integrazione dell'applicazione **MOVEit Transfer - Azure AD integration** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f27a9-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f27a9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="f27a9-153">Nella sezione **URL e dominio MOVEit Transfer - Azure AD integration** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f27a9-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="f27a9-155">a.</span><span class="sxs-lookup"><span data-stu-id="f27a9-155">a.</span></span> <span data-ttu-id="f27a9-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="f27a9-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="f27a9-157">b.</span><span class="sxs-lookup"><span data-stu-id="f27a9-157">b.</span></span> <span data-ttu-id="f27a9-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="f27a9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="f27a9-159">c.</span><span class="sxs-lookup"><span data-stu-id="f27a9-159">c.</span></span> <span data-ttu-id="f27a9-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="f27a9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="f27a9-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="f27a9-161">These values are not real.</span></span> <span data-ttu-id="f27a9-162">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="f27a9-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f27a9-163">È possibile fare riferimento a questi valori più avanti nella sezione **URL dei metadati del provider di servizi** oppure contattare il [team di supporto clienti di MOVEit Transfer - Azure AD integration](https://community.ipswitch.com/s/support) per ottenere questi valori.</span><span class="sxs-lookup"><span data-stu-id="f27a9-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span></span>

4. <span data-ttu-id="f27a9-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="f27a9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="f27a9-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f27a9-166">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="f27a9-168">Accedere al tenant di MOVEit Transfer come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f27a9-168">Sign on to your MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="f27a9-169">Nella barra di spostamento a sinistra fare clic su **Settings**(Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="f27a9-169">On the left navigation pane, click **Settings**.</span></span>

    ![Sezione delle impostazioni sul lato dell'app](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="f27a9-171">Fare clic sul collegamento **Single Signon** (Single Sign-On) in **Security Policies -> User Auth** (Criteri di sicurezza -> Autenticazione utente).</span><span class="sxs-lookup"><span data-stu-id="f27a9-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Criteri di sicurezza sul lato dell'app](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="f27a9-173">Fare clic sul collegamento con l'URL dei metadati per scaricare il documento di metadati.</span><span class="sxs-lookup"><span data-stu-id="f27a9-173">Click the Metadata URL link to download the metadata document.</span></span>

    ![URL dei metadati del provider di servizi](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="f27a9-175">Verificare che il valore di **entityID** corrisponda a quello di **Identificatore** nella sezione **URL e dominio MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="f27a9-176">Verificare che l'URL della posizione **AssertionConsumerService** corrisponda all'**URL di risposta** nella sezione **URL e dominio MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="f27a9-178">Fare clic sul pulsante **Add Identity Provider** (Aggiungi provider di identità) per aggiungere un nuovo provider di identità federato.</span><span class="sxs-lookup"><span data-stu-id="f27a9-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>

    ![Aggiungi provider di identità](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="f27a9-180">Fare clic su **Browse** (Sfoglia) per selezionare il file di metadati scaricato dal portale di Azure e quindi fare clic su **Add Identity Provider** (Aggiungi provider di identità) per caricare il file scaricato.</span><span class="sxs-lookup"><span data-stu-id="f27a9-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span></span>

    ![Provider di identità SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="f27a9-182">Selezionare "**Yes**" (Sì) per **Enabled** (Abilitato) nella pagina **Edit Federated Identity Provider Settings** (Modifica impostazioni provider di identità federato) e fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="f27a9-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Impostazioni provider di identità federato](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="f27a9-184">Nella pagina **Edit Federated Identity Provider User Settings** (Modifica impostazioni utente del provider di identità federato) eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="f27a9-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span></span>
    
    ![Modifica delle impostazioni del provider di identità federato](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="f27a9-186">a.</span><span class="sxs-lookup"><span data-stu-id="f27a9-186">a.</span></span> <span data-ttu-id="f27a9-187">Selezionare **SAML NameID** (ID nome SAML) per **Login name** (Nome di accesso).</span><span class="sxs-lookup"><span data-stu-id="f27a9-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="f27a9-188">b.</span><span class="sxs-lookup"><span data-stu-id="f27a9-188">b.</span></span> <span data-ttu-id="f27a9-189">Selezionare **Other** (Altro) per **Full name** (Nome completo) e nella casella di testo **Attribute name** (Nome attributo) immettere il valore: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="f27a9-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="f27a9-190">c.</span><span class="sxs-lookup"><span data-stu-id="f27a9-190">c.</span></span> <span data-ttu-id="f27a9-191">Selezionare **Other** (Altro) per **Email** (Posta elettronica) e nella casella di testo **Attribute name** (Nome attributo) immettere il valore: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="f27a9-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="f27a9-192">d.</span><span class="sxs-lookup"><span data-stu-id="f27a9-192">d.</span></span> <span data-ttu-id="f27a9-193">Selezionare **Yes** (Sì) per **Auto-create account on signon** (Crea automaticamente account all'accesso).</span><span class="sxs-lookup"><span data-stu-id="f27a9-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="f27a9-194">e.</span><span class="sxs-lookup"><span data-stu-id="f27a9-194">e.</span></span> <span data-ttu-id="f27a9-195">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f27a9-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="f27a9-196">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f27a9-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f27a9-197">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f27a9-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f27a9-198">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f27a9-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f27a9-199">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f27a9-199">Create an Azure AD test user</span></span>

<span data-ttu-id="f27a9-200">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f27a9-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="f27a9-202">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f27a9-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f27a9-203">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="f27a9-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f27a9-205">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f27a9-207">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f27a9-209">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f27a9-209">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f27a9-211">a.</span><span class="sxs-lookup"><span data-stu-id="f27a9-211">a.</span></span> <span data-ttu-id="f27a9-212">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f27a9-213">b.</span><span class="sxs-lookup"><span data-stu-id="f27a9-213">b.</span></span> <span data-ttu-id="f27a9-214">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f27a9-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f27a9-215">c.</span><span class="sxs-lookup"><span data-stu-id="f27a9-215">c.</span></span> <span data-ttu-id="f27a9-216">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f27a9-217">d.</span><span class="sxs-lookup"><span data-stu-id="f27a9-217">d.</span></span> <span data-ttu-id="f27a9-218">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="f27a9-219">Creare un utente di test di MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="f27a9-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="f27a9-220">Questa sezione descrive come creare un utente di test di nome Britta Simon in MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="f27a9-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="f27a9-221">MOVEit Transfer - Azure AD integration supporta il provisioning JIT, che è stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="f27a9-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="f27a9-222">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="f27a9-222">There is no action item for you in this section.</span></span> <span data-ttu-id="f27a9-223">Durante il tentativo di accesso a MOVEit Transfer - Azure AD integration viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="f27a9-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="f27a9-224">Per creare un utente manualmente, contattare il [team di supporto clienti di MOVEit Transfer - Azure AD integration](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="f27a9-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f27a9-225">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f27a9-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="f27a9-226">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="f27a9-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="f27a9-228">**Per assegnare Britta Simon a MOVEit Transfer - Azure AD integration, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f27a9-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="f27a9-229">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f27a9-231">Nell'elenco delle applicazioni selezionare **MOVEit Transfer - Azure AD integration**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Collegamento di MOVEit Transfer - Azure AD integration nell'elenco delle applicazioni](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="f27a9-233">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f27a9-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="f27a9-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-235">Click **Add** button.</span></span> <span data-ttu-id="f27a9-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="f27a9-238">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f27a9-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f27a9-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f27a9-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f27a9-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f27a9-241">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f27a9-241">Test single sign-on</span></span>

<span data-ttu-id="f27a9-242">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f27a9-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f27a9-243">Quando si fa clic sul riquadro MOVEit Transfer - Azure AD integration nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione MOVEit Transfer - Azure AD integration.</span><span class="sxs-lookup"><span data-stu-id="f27a9-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f27a9-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f27a9-244">Additional resources</span></span>

* [<span data-ttu-id="f27a9-245">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f27a9-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f27a9-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f27a9-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

