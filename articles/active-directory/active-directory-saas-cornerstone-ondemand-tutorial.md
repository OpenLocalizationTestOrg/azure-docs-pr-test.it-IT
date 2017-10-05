---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cornerstone OnDemand | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Cornerstone OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 8bb32588579a0d40b9ae7e0f823c6daab21c856e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="c7f15-103">Esercitazione: Integrazione di Azure Active Directory con Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="c7f15-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="c7f15-104">Questa esercitazione descrive come integrare Cornerstone OnDemand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7f15-104">In this tutorial, you learn how to integrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7f15-105">L'integrazione di Cornerstone OnDemand con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7f15-105">Integrating Cornerstone OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7f15-106">È possibile controllare in Azure AD chi può accedere a Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="c7f15-106">You can control in Azure AD who has access to Cornerstone OnDemand</span></span>
- <span data-ttu-id="c7f15-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a Cornerstone OnDemand con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7f15-107">You can enable your users to automatically get signed-on to Cornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7f15-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7f15-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7f15-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7f15-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7f15-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c7f15-110">Prerequisites</span></span>

<span data-ttu-id="c7f15-111">Per configurare l'integrazione di Azure AD con Cornerstone OnDemand sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7f15-111">To configure Azure AD integration with Cornerstone OnDemand, you need the following items:</span></span>

- <span data-ttu-id="c7f15-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7f15-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7f15-113">Sottoscrizione di Cornerstone OnDemand abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c7f15-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7f15-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c7f15-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7f15-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7f15-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7f15-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c7f15-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7f15-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7f15-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7f15-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c7f15-118">Scenario description</span></span>
<span data-ttu-id="c7f15-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c7f15-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7f15-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7f15-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7f15-121">Aggiunta di Cornerstone OnDemand dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c7f15-121">Adding Cornerstone OnDemand from the gallery</span></span>
2. <span data-ttu-id="c7f15-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7f15-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-the-gallery"></a><span data-ttu-id="c7f15-123">Aggiunta di Cornerstone OnDemand dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c7f15-123">Adding Cornerstone OnDemand from the gallery</span></span>
<span data-ttu-id="c7f15-124">Per configurare l'integrazione di Cornerstone OnDemand in Azure AD è necessario aggiungere Cornerstone OnDemand dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c7f15-124">To configure the integration of Cornerstone OnDemand into Azure AD, you need to add Cornerstone OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7f15-125">**Per aggiungere Cornerstone OnDemand dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c7f15-125">**To add Cornerstone OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7f15-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c7f15-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7f15-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7f15-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c7f15-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7f15-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c7f15-133">Nella casella di ricerca digitare **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-133">In the search box, type **Cornerstone OnDemand**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="c7f15-135">Nel pannello dei risultati selezionare **Cornerstone OnDemand** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7f15-135">In the results panel, select **Cornerstone OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7f15-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7f15-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7f15-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cornerstone OnDemand mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c7f15-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7f15-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Cornerstone OnDemand corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7f15-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cornerstone OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="c7f15-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="c7f15-140">In other words, a link relationship between an Azure AD user and the related user in Cornerstone OnDemand needs to be established.</span></span>

<span data-ttu-id="c7f15-141">Per stabilire la relazione di collegamento, in Cornerstone OnDemand assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c7f15-141">In Cornerstone OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c7f15-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Cornerstone OnDemand è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7f15-142">To configure and test Azure AD single sign-on with Cornerstone OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7f15-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c7f15-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7f15-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7f15-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7f15-145">**[Creazione di un utente test di Cornerstone OnDemand](#creating-a-cornerstone-ondemand-test-user)**: per avere una controparte di Britta Simon in Cornerstone OnDemand collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7f15-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - to have a counterpart of Britta Simon in Cornerstone OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7f15-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7f15-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7f15-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c7f15-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7f15-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7f15-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7f15-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="c7f15-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="c7f15-150">**Per configurare l'accesso Single Sign-On di Azure AD con Cornerstone OnDemand, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c7f15-150">**To configure Azure AD single sign-on with Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="c7f15-151">Nella pagina di integrazione dell'applicazione **Cornerstone OnDemand** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-151">In the Azure portal, on the **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c7f15-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c7f15-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="c7f15-155">Nella sezione **URL e dominio Cornerstone OnDemand** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c7f15-155">On the **Cornerstone OnDemand Domain and URLs** section, perform the following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="c7f15-157">a.</span><span class="sxs-lookup"><span data-stu-id="c7f15-157">a.</span></span> <span data-ttu-id="c7f15-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company>.csod.com`.</span><span class="sxs-lookup"><span data-stu-id="c7f15-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="c7f15-159">b.</span><span class="sxs-lookup"><span data-stu-id="c7f15-159">b.</span></span> <span data-ttu-id="c7f15-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente: `https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="c7f15-160">In **Identifier** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7f15-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c7f15-161">These values are not real.</span></span> <span data-ttu-id="c7f15-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="c7f15-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c7f15-163">Per ottenere questi valori contattare il [team di supporto clienti di Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="c7f15-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) to get these values.</span></span> 
 
4. <span data-ttu-id="c7f15-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="c7f15-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="c7f15-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c7f15-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7f15-168">Nella sezione **Configurazione di Cornerstone OnDemand** fare clic su **Configura Cornerstone OnDemand** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-168">On the **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c7f15-169">Copiare l'**URL servizio Single Sign-On SAML e l'URL di disconnessione** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="c7f15-171">Per configurare l'accesso Single Sign-On sul lato **Cornerstone OnDemand** è necessario inviare il file **Certificato** scaricato e i valori **Sign-Out URL** (URL di disconnessione) e **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) al [team di supporto di Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="c7f15-171">To configure single sign-on on **Cornerstone OnDemand** side, you need to send the downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  to [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="c7f15-172">L'applicazione viene configurata in modo che la connessione SAML SSO sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="c7f15-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c7f15-173">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c7f15-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7f15-174">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c7f15-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7f15-175">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7f15-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7f15-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7f15-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7f15-177">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7f15-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c7f15-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c7f15-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7f15-180">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c7f15-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7f15-182">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="c7f15-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7f15-184">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7f15-186">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c7f15-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7f15-188">a.</span><span class="sxs-lookup"><span data-stu-id="c7f15-188">a.</span></span> <span data-ttu-id="c7f15-189">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7f15-190">b.</span><span class="sxs-lookup"><span data-stu-id="c7f15-190">b.</span></span> <span data-ttu-id="c7f15-191">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7f15-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7f15-192">c.</span><span class="sxs-lookup"><span data-stu-id="c7f15-192">c.</span></span> <span data-ttu-id="c7f15-193">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7f15-194">d.</span><span class="sxs-lookup"><span data-stu-id="c7f15-194">d.</span></span> <span data-ttu-id="c7f15-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="c7f15-196">Creazione di un utente test di Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="c7f15-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="c7f15-197">Per consentire agli utenti di Azure AD di accedere a Cornerstone OnDemand, è necessario eseguirne il provisioning in Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="c7f15-197">In order to enable Azure AD users to log into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="c7f15-198">Nel caso di Cornerstone OnDemand, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="c7f15-198">In the case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="c7f15-199">Per configurare il provisioning dell'utente inviare le informazioni, ad esempio nome e indirizzo di posta elettronica dell'utente di Azure AD, al [team di supporto di Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="c7f15-199">To configure user provisioning, send the information (e.g.: Name, Email) about the Azure AD user you want to provision to the [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="c7f15-200">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Cornerstone OnDemand per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="c7f15-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c7f15-201">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7f15-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c7f15-202">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="c7f15-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cornerstone OnDemand.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c7f15-204">**Per assegnare Britta Simon a Cornerstone OnDemand, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c7f15-204">**To assign Britta Simon to Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="c7f15-205">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c7f15-207">Nell'elenco delle applicazioni selezionare **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-207">In the applications list, select **Cornerstone OnDemand**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="c7f15-209">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c7f15-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c7f15-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-211">Click **Add** button.</span></span> <span data-ttu-id="c7f15-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c7f15-214">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c7f15-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7f15-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7f15-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c7f15-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7f15-217">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c7f15-217">Testing single sign-on</span></span>

<span data-ttu-id="c7f15-218">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c7f15-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c7f15-219">Quando si fa clic sul riquadro Cornerstone OnDemand nel pannello di accesso si accede automaticamente all'applicazione Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="c7f15-219">When you click the Cornerstone OnDemand tile in the Access Panel, you should get automatically signed-on to your Cornerstone OnDemand application.</span></span>
<span data-ttu-id="c7f15-220">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7f15-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c7f15-221">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c7f15-221">Additional resources</span></span>

* [<span data-ttu-id="c7f15-222">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7f15-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7f15-223">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7f15-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png

