---
title: 'Esercitazione: Integrazione di Azure Active Directory con Direct | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Direct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 84582492592613320bd3ec2bdffe08519852d7c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="8dbcf-103">Esercitazione: Integrazione di Azure Active Directory con Direct</span><span class="sxs-lookup"><span data-stu-id="8dbcf-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="8dbcf-104">Questa esercitazione descrive come integrare Direct con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8dbcf-104">In this tutorial, you learn how to integrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8dbcf-105">L'integrazione di Direct con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-105">Integrating Direct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8dbcf-106">È possibile controllare in Azure AD chi può accedere a Direct</span><span class="sxs-lookup"><span data-stu-id="8dbcf-106">You can control in Azure AD who has access to Direct</span></span>
- <span data-ttu-id="8dbcf-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a Direct con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dbcf-107">You can enable your users to automatically get signed-on to Direct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8dbcf-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8dbcf-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8dbcf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8dbcf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8dbcf-110">Prerequisites</span></span>

<span data-ttu-id="8dbcf-111">Per configurare l'integrazione di Azure AD con Direct sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-111">To configure Azure AD integration with Direct, you need the following items:</span></span>

- <span data-ttu-id="8dbcf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8dbcf-113">Sottoscrizione di Direct abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8dbcf-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8dbcf-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8dbcf-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8dbcf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8dbcf-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8dbcf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8dbcf-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8dbcf-118">Scenario description</span></span>
<span data-ttu-id="8dbcf-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8dbcf-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8dbcf-121">Aggiunta di Direct dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8dbcf-121">Adding Direct from the gallery</span></span>
2. <span data-ttu-id="8dbcf-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dbcf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-the-gallery"></a><span data-ttu-id="8dbcf-123">Aggiunta di Direct dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8dbcf-123">Adding Direct from the gallery</span></span>
<span data-ttu-id="8dbcf-124">Per configurare l'integrazione di Direct in Azure AD è necessario aggiungere Direct dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-124">To configure the integration of Direct into Azure AD, you need to add Direct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8dbcf-125">**Per aggiungere Direct dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8dbcf-125">**To add Direct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8dbcf-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8dbcf-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8dbcf-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8dbcf-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8dbcf-133">Nella casella di ricerca digitare **Direct**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-133">In the search box, type **Direct**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="8dbcf-135">Nel pannello dei risultati selezionare **Direct** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-135">In the results panel, select **Direct**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8dbcf-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dbcf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8dbcf-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Direct mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8dbcf-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8dbcf-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Direct corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Direct is to a user in Azure AD.</span></span> <span data-ttu-id="8dbcf-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Direct.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-140">In other words, a link relationship between an Azure AD user and the related user in Direct needs to be established.</span></span>

<span data-ttu-id="8dbcf-141">Per stabilire la relazione di collegamento, in Direct assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="8dbcf-141">In Direct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8dbcf-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Direct è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-142">To configure and test Azure AD single sign-on with Direct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8dbcf-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8dbcf-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8dbcf-145">**[Creazione di un utente test di Direct](#creating-a-direct-test-user)**: per avere una controparte di Britta Simon in Direct collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - to have a counterpart of Britta Simon in Direct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8dbcf-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8dbcf-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8dbcf-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dbcf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8dbcf-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel nuovo portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Direct.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="8dbcf-150">**Per configurare l'accesso Single Sign-On di Azure AD con Direct, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8dbcf-150">**To configure Azure AD single sign-on with Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="8dbcf-151">Nella pagina di integrazione dell'applicazione **Direct** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-151">In the Azure portal, on the **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8dbcf-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="8dbcf-155">Nella sezione **URL e dominio Direct** per configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-155">On the **Direct Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="8dbcf-157">Nella casella di testo **Identificatore** digitare l'URL: `https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="8dbcf-157">In the **Identifier** textbox, type the URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="8dbcf-158">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="8dbcf-160">Nella casella di testo **URL accesso** digitare l'URL: `https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="8dbcf-160">In the **Sign-on URL** textbox, type the URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="8dbcf-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="8dbcf-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8dbcf-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8dbcf-165">Per configurare l'accesso Single Sign-On sul lato **Direct** è necessario inviare il file **XML metadati** scaricato al [team di supporto di Direct](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="8dbcf-165">To configure single sign-on on **Direct** side, you need to send the downloaded **Metadata XML** to [Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="8dbcf-166">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8dbcf-167">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8dbcf-168">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8dbcf-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8dbcf-169">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dbcf-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="8dbcf-170">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8dbcf-172">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8dbcf-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8dbcf-173">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8dbcf-175">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8dbcf-177">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8dbcf-179">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8dbcf-181">a.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-181">a.</span></span> <span data-ttu-id="8dbcf-182">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8dbcf-183">b.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-183">b.</span></span> <span data-ttu-id="8dbcf-184">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8dbcf-185">c.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-185">c.</span></span> <span data-ttu-id="8dbcf-186">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8dbcf-187">d.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-187">d.</span></span> <span data-ttu-id="8dbcf-188">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="8dbcf-189">Creazione di un utente test di Direct</span><span class="sxs-lookup"><span data-stu-id="8dbcf-189">Creating a Direct test user</span></span>

<span data-ttu-id="8dbcf-190">In questa sezione si crea un utente con nome Britta Simon in Direct.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="8dbcf-191">Collaborare con il [team di supporto di Direct](https://direct4b.com/ja/support.html#inquiry) per aggiungere gli utenti nella piattaforma Direct.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add the users in the Direct platform.</span></span> <span data-ttu-id="8dbcf-192">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8dbcf-193">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dbcf-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8dbcf-194">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Direct.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Direct.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8dbcf-196">**Per assegnare Britta Simon a Direct, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8dbcf-196">**To assign Britta Simon to Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="8dbcf-197">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8dbcf-199">Nell'elenco delle applicazioni selezionare **Direct**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-199">In the applications list, select **Direct**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="8dbcf-201">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8dbcf-203">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-203">Click **Add** button.</span></span> <span data-ttu-id="8dbcf-204">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8dbcf-206">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8dbcf-207">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8dbcf-208">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8dbcf-209">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8dbcf-209">Testing single sign-on</span></span>

<span data-ttu-id="8dbcf-210">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="8dbcf-211">Se si vuole testare in **modalità avviata da IDP**:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-211">If you wish to test in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="8dbcf-212">Quando si fa clic sul riquadro **Direct** nel pannello di accesso si accede automaticamente all'applicazione **Direct**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-212">When you click the **Direct** tile in the Access Panel, you should get automatically signed-on to your **Direct** application.</span></span>

2. <span data-ttu-id="8dbcf-213">Se si vuole testare in **modalità avviata da SP**:</span><span class="sxs-lookup"><span data-stu-id="8dbcf-213">If you wish to test in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="8dbcf-214">a.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-214">a.</span></span> <span data-ttu-id="8dbcf-215">Fare clic sulla scheda **Direct** nel pannello di accesso. Verrà aperta la pagina per l'accesso all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-215">Click on the **Direct** tile in the Access Panel and you will be redirected to the application sign-on page.</span></span>

    <span data-ttu-id="8dbcf-216">b.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-216">b.</span></span> <span data-ttu-id="8dbcf-217">Digitare il valore di `subdomain` nella casella di testo e premere 次へ (Avanti). Viene eseguito l'accesso automatico all'applicazione **Direct**.</span><span class="sxs-lookup"><span data-stu-id="8dbcf-217">Input your `subdomain` in the textbox displayed and press '次へ (Next)' and you should get automatically signed-on to your **Direct** application .</span></span>
    
<span data-ttu-id="8dbcf-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8dbcf-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8dbcf-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8dbcf-219">Additional resources</span></span>

* [<span data-ttu-id="8dbcf-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dbcf-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8dbcf-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dbcf-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

