---
title: 'Esercitazione: Integrazione di Azure Active Directory con Freshservice | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Freshservice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d32775fa91d3a49da1ef55e57d1d38990fa09346
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="9fd41-103">Esercitazione: Integrazione di Azure Active Directory con Freshservice</span><span class="sxs-lookup"><span data-stu-id="9fd41-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="9fd41-104">Questa esercitazione descrive come integrare Freshservice con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9fd41-104">In this tutorial, you learn how to integrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9fd41-105">L'integrazione di Freshservice con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9fd41-105">Integrating Freshservice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9fd41-106">È possibile controllare in Azure AD chi può accedere a Freshservice</span><span class="sxs-lookup"><span data-stu-id="9fd41-106">You can control in Azure AD who has access to Freshservice</span></span>
- <span data-ttu-id="9fd41-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a Freshservice con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fd41-107">You can enable your users to automatically get signed-on to Freshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9fd41-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd41-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9fd41-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9fd41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fd41-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9fd41-110">Prerequisites</span></span>

<span data-ttu-id="9fd41-111">Per configurare l'integrazione di Azure AD con Freshservice sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9fd41-111">To configure Azure AD integration with Freshservice, you need the following items:</span></span>

- <span data-ttu-id="9fd41-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fd41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9fd41-113">Sottoscrizione di Freshservice abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9fd41-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9fd41-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9fd41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9fd41-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9fd41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9fd41-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9fd41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9fd41-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9fd41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9fd41-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9fd41-118">Scenario description</span></span>
<span data-ttu-id="9fd41-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9fd41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9fd41-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9fd41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9fd41-121">Aggiunta di Freshservice dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9fd41-121">Adding Freshservice from the gallery</span></span>
2. <span data-ttu-id="9fd41-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fd41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-the-gallery"></a><span data-ttu-id="9fd41-123">Aggiunta di Freshservice dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9fd41-123">Adding Freshservice from the gallery</span></span>
<span data-ttu-id="9fd41-124">Per configurare l'integrazione di Freshservice in Azure AD è necessario aggiungere Freshservice dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9fd41-124">To configure the integration of Freshservice into Azure AD, you need to add Freshservice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9fd41-125">**Per aggiungere Freshservice dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9fd41-125">**To add Freshservice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9fd41-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9fd41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9fd41-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9fd41-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="9fd41-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="9fd41-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="9fd41-133">Nella casella di ricerca digitare **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-133">In the search box, type **Freshservice**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="9fd41-135">Nel pannello dei risultati selezionare **Freshservice** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9fd41-135">In the results panel, select **Freshservice**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9fd41-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fd41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9fd41-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Freshservice mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9fd41-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9fd41-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Freshservice corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fd41-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Freshservice is to a user in Azure AD.</span></span> <span data-ttu-id="9fd41-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Freshservice.</span><span class="sxs-lookup"><span data-stu-id="9fd41-140">In other words, a link relationship between an Azure AD user and the related user in Freshservice needs to be established.</span></span>

<span data-ttu-id="9fd41-141">Per stabilire la relazione di collegamento, in Freshservice assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="9fd41-141">In Freshservice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9fd41-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Freshservice è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9fd41-142">To configure and test Azure AD single sign-on with Freshservice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9fd41-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9fd41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9fd41-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9fd41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9fd41-145">**[Creazione di un utente test di Freshservice](#creating-a-freshservice-test-user)**: per avere una controparte di Britta Simon in Freshservice collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fd41-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - to have a counterpart of Britta Simon in Freshservice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9fd41-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fd41-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9fd41-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="9fd41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9fd41-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fd41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9fd41-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Freshservice.</span><span class="sxs-lookup"><span data-stu-id="9fd41-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="9fd41-150">**Per configurare l'accesso Single Sign-On di Azure AD con Freshservice, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9fd41-150">**To configure Azure AD single sign-on with Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="9fd41-151">Nella pagina di integrazione dell'applicazione **Freshservice** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-151">In the Azure portal, on the **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="9fd41-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9fd41-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="9fd41-155">Nella sezione **URL e dominio Freshservice** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9fd41-155">On the **Freshservice Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="9fd41-157">a.</span><span class="sxs-lookup"><span data-stu-id="9fd41-157">a.</span></span> <span data-ttu-id="9fd41-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<democompany>.freshservice.com`.</span><span class="sxs-lookup"><span data-stu-id="9fd41-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="9fd41-159">b.</span><span class="sxs-lookup"><span data-stu-id="9fd41-159">b.</span></span> <span data-ttu-id="9fd41-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="9fd41-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9fd41-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="9fd41-161">These values are not real.</span></span> <span data-ttu-id="9fd41-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="9fd41-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9fd41-163">Per ottenere questi valori contattare il [team di supporto clienti di Freshservice](https://support.freshservice.com/).</span><span class="sxs-lookup"><span data-stu-id="9fd41-163">Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="9fd41-164">Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE** del certificato.</span><span class="sxs-lookup"><span data-stu-id="9fd41-164">On the **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="9fd41-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="9fd41-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9fd41-168">Nella sezione **Configurazione di Freshservice** fare clic su **Configura Freshservice** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-168">On the **Freshservice Configuration** section, click **Configure Freshservice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9fd41-169">Copiare i valori **Sign-Out URL (URL di disconnessione) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="9fd41-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="9fd41-171">In un'altra finestra del Web browser accedere al sito aziendale di Freshservice come amministratore.</span><span class="sxs-lookup"><span data-stu-id="9fd41-171">In a different web browser window, log in to your Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="9fd41-172">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="9fd41-173">![Amministratore](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="9fd41-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="9fd41-174">Nel **portale dei clienti** fare clic su **Security** (Sicurezza).</span><span class="sxs-lookup"><span data-stu-id="9fd41-174">In the **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="9fd41-175">![Sicurezza](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="9fd41-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="9fd41-176">Nella sezione **Security** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9fd41-176">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="9fd41-177">![Single Sign-On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="9fd41-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="9fd41-178">a.</span><span class="sxs-lookup"><span data-stu-id="9fd41-178">a.</span></span> <span data-ttu-id="9fd41-179">Passare a **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="9fd41-180">b.</span><span class="sxs-lookup"><span data-stu-id="9fd41-180">b.</span></span> <span data-ttu-id="9fd41-181">Selezionare **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="9fd41-182">c.</span><span class="sxs-lookup"><span data-stu-id="9fd41-182">c.</span></span> <span data-ttu-id="9fd41-183">Nella casella di testo **SAML Login URL** (URL di accesso SAML) incollare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd41-183">In the **SAML Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9fd41-184">d.</span><span class="sxs-lookup"><span data-stu-id="9fd41-184">d.</span></span> <span data-ttu-id="9fd41-185">Nella casella di testo **URL disconnessione** incollare il valore di **Sign-Out URL** (URL di disconnessione) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd41-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9fd41-186">e.</span><span class="sxs-lookup"><span data-stu-id="9fd41-186">e.</span></span> <span data-ttu-id="9fd41-187">Nella casella di testo **Security Certificate Fingerprint** (Impronta digitale certificato di protezione) incollare il valore **IDENTIFICAZIONE PERSONALE** del certificato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd41-187">In **Security Certificate Fingerprint** textbox, paste the **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9fd41-188">f.</span><span class="sxs-lookup"><span data-stu-id="9fd41-188">f.</span></span> <span data-ttu-id="9fd41-189">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="9fd41-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="9fd41-190">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="9fd41-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9fd41-191">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="9fd41-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9fd41-192">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9fd41-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9fd41-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fd41-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="9fd41-194">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd41-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="9fd41-196">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9fd41-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9fd41-197">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9fd41-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9fd41-199">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="9fd41-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9fd41-201">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9fd41-203">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9fd41-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9fd41-205">a.</span><span class="sxs-lookup"><span data-stu-id="9fd41-205">a.</span></span> <span data-ttu-id="9fd41-206">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9fd41-207">b.</span><span class="sxs-lookup"><span data-stu-id="9fd41-207">b.</span></span> <span data-ttu-id="9fd41-208">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9fd41-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9fd41-209">c.</span><span class="sxs-lookup"><span data-stu-id="9fd41-209">c.</span></span> <span data-ttu-id="9fd41-210">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9fd41-211">d.</span><span class="sxs-lookup"><span data-stu-id="9fd41-211">d.</span></span> <span data-ttu-id="9fd41-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="9fd41-213">Creazione di un utente test di Freshservice</span><span class="sxs-lookup"><span data-stu-id="9fd41-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="9fd41-214">Per consentire agli utenti di Azure AD di accedere a Freshservice, è necessario eseguire il provisioning degli utenti in Freshservice.</span><span class="sxs-lookup"><span data-stu-id="9fd41-214">To enable Azure AD users to log in to FreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="9fd41-215">Nel caso di FreshService, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="9fd41-215">In the case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="9fd41-216">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9fd41-216">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9fd41-217">Accedere al sito aziendale di **FreshService** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="9fd41-217">Log in to your **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="9fd41-218">Nel menu in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-218">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="9fd41-219">![Amministratore](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="9fd41-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="9fd41-220">Nella sezione **User Management** (Gestione utenti) fare clic su **Requesters** (Richiedenti).</span><span class="sxs-lookup"><span data-stu-id="9fd41-220">In the **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="9fd41-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span><span class="sxs-lookup"><span data-stu-id="9fd41-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="9fd41-222">Fare clic su **Nuovo Requester**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="9fd41-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span><span class="sxs-lookup"><span data-stu-id="9fd41-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="9fd41-224">Nella sezione **New Requester** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9fd41-224">In the **New Requester** section, perform the following steps:</span></span>
   
    <span data-ttu-id="9fd41-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span><span class="sxs-lookup"><span data-stu-id="9fd41-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="9fd41-226">a.</span><span class="sxs-lookup"><span data-stu-id="9fd41-226">a.</span></span> <span data-ttu-id="9fd41-227">Nelle caselle **First Name** e **Email** immettere il nome e l'indirizzo di posta elettronica di un account Azure Active Directory valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="9fd41-227">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="9fd41-228">b.</span><span class="sxs-lookup"><span data-stu-id="9fd41-228">b.</span></span> <span data-ttu-id="9fd41-229">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="9fd41-230">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="9fd41-230">The Azure Active Directory account holder gets an email including a link to confirm the account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="9fd41-231">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da FreshService per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="9fd41-231">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span></span>
>  

![Assegna utente][200] 

<span data-ttu-id="9fd41-233">**Per assegnare Britta Simon a Freshservice, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9fd41-233">**To assign Britta Simon to Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="9fd41-234">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9fd41-236">Nell'elenco delle applicazioni selezionare **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-236">In the applications list, select **Freshservice**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="9fd41-238">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="9fd41-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="9fd41-240">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-240">Click **Add** button.</span></span> <span data-ttu-id="9fd41-241">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="9fd41-243">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="9fd41-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9fd41-244">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9fd41-245">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9fd41-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9fd41-246">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9fd41-246">Testing single sign-on</span></span>

<span data-ttu-id="9fd41-247">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9fd41-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9fd41-248">Quando si fa clic sul riquadro Freshservice nel pannello di accesso si accede automaticamente all'applicazione Freshservice.</span><span class="sxs-lookup"><span data-stu-id="9fd41-248">When you click the Freshservice tile in the Access Panel, you should get automatically signed-on to your Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9fd41-249">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9fd41-249">Additional resources</span></span>

* [<span data-ttu-id="9fd41-250">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fd41-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9fd41-251">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fd41-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

