---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jitbit Helpdesk | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Jitbit Helpdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 6523ee3179dafd79528093b856b0ec10fafb4f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="40e58-103">Esercitazione: Integrazione di Azure Active Directory con Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="40e58-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="40e58-104">Questa esercitazione descrive come integrare Jitbit Helpdesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40e58-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40e58-105">L'integrazione di Jitbit Helpdesk con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="40e58-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="40e58-106">È possibile controllare in Azure AD chi può accedere a Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="40e58-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="40e58-107">È possibile abilitare gli utenti per l'accesso automatico a Jitbit Helpdesk (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="40e58-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40e58-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40e58-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="40e58-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40e58-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40e58-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="40e58-110">Prerequisites</span></span>

<span data-ttu-id="40e58-111">Per configurare l'integrazione di Azure AD con Jitbit Helpdesk, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="40e58-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="40e58-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40e58-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40e58-113">Sottoscrizione di Jitbit Helpdesk abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="40e58-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40e58-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="40e58-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40e58-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="40e58-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40e58-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="40e58-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40e58-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40e58-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40e58-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="40e58-118">Scenario description</span></span>
<span data-ttu-id="40e58-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="40e58-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40e58-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="40e58-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40e58-121">Aggiunta di Jitbit Helpdesk dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="40e58-121">Adding Jitbit Helpdesk from the gallery</span></span>
2. <span data-ttu-id="40e58-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="40e58-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="40e58-123">Aggiunta di Jitbit Helpdesk dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="40e58-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="40e58-124">Per configurare l'integrazione di Jitbit Helpdesk in Azure AD, è necessario aggiungere Jitbit Helpdesk dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="40e58-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="40e58-125">**Per aggiungere Jitbit Helpdesk dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="40e58-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="40e58-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="40e58-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40e58-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="40e58-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="40e58-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="40e58-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="40e58-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="40e58-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="40e58-133">Nella casella di ricerca digitare **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="40e58-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="40e58-135">Nel pannello dei risultati selezionare **Jitbit Helpdesk** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40e58-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40e58-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="40e58-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40e58-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Jitbit Helpdesk in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="40e58-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40e58-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Jitbit Helpdesk che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40e58-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="40e58-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="40e58-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="40e58-141">Per stabilire la relazione di collegamento, in Jitbit Helpdesk assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="40e58-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="40e58-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Jitbit Helpdesk, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="40e58-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="40e58-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="40e58-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="40e58-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40e58-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40e58-145">**[Creazione di un utente test di Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**: per avere una controparte di Britta Simon in Jitbit Helpdesk collegata alla rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="40e58-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="40e58-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40e58-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40e58-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="40e58-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40e58-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="40e58-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40e58-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="40e58-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="40e58-150">**Per configurare Single Sign-On di Azure AD con Jitbit Helpdesk, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="40e58-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="40e58-151">Nella pagina di integrazione dell'applicazione **Jitbit Helpdesk** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="40e58-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="40e58-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="40e58-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="40e58-155">Nella sezione **URL e dominio Jitbit Helpdesk** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="40e58-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="40e58-157">a.</span><span class="sxs-lookup"><span data-stu-id="40e58-157">a.</span></span> <span data-ttu-id="40e58-158">Nella casella di testo **URL di accesso** digitare l'URL adottando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="40e58-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="40e58-159">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="40e58-159">This value is not real.</span></span> <span data-ttu-id="40e58-160">aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="40e58-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="40e58-161">Per ottenere tale valore, contattare il [team di supporto clienti di Jitbit Helpdesk](https://www.jitbit.com/support/).</span><span class="sxs-lookup"><span data-stu-id="40e58-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="40e58-162">b.</span><span class="sxs-lookup"><span data-stu-id="40e58-162">b.</span></span>  <span data-ttu-id="40e58-163">Nella casella di testo **Identificatore** digitare un URL come di seguito: `https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="40e58-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="40e58-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="40e58-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="40e58-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="40e58-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40e58-168">Nella sezione **Configurazione di Jitbit Helpdesk** fare clic su **Configura Jitbit Helpdesk** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="40e58-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="40e58-169">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="40e58-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="40e58-171">In un'altra finestra del Web browser accedere al sito aziendale di Jitbit Helpdesk come amministratore.</span><span class="sxs-lookup"><span data-stu-id="40e58-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="40e58-172">Nel barra degli strumenti in alto fare clic su **Administration**.</span><span class="sxs-lookup"><span data-stu-id="40e58-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="40e58-173">![Amministrazione](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="40e58-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="40e58-174">Fare clic su **General settings**.</span><span class="sxs-lookup"><span data-stu-id="40e58-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="40e58-175">![Users, companies and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies and permissions")</span><span class="sxs-lookup"><span data-stu-id="40e58-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="40e58-176">Nella sezione di configurazione **Authentication settings** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="40e58-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="40e58-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span><span class="sxs-lookup"><span data-stu-id="40e58-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="40e58-178">a.</span><span class="sxs-lookup"><span data-stu-id="40e58-178">a.</span></span> <span data-ttu-id="40e58-179">Selezionare **Enable SAML 2.0 single sign on** (Abilita Single Sign-On SAML 2.0) per l'accesso Single Sign-On con **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="40e58-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="40e58-180">b.</span><span class="sxs-lookup"><span data-stu-id="40e58-180">b.</span></span> <span data-ttu-id="40e58-181">Nella casella di testo **Endpoint URL** incollare il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40e58-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="40e58-182">c.</span><span class="sxs-lookup"><span data-stu-id="40e58-182">c.</span></span> <span data-ttu-id="40e58-183">Aprire il certificato con codifica **base 64** nel blocco note, copiarne il contenuto negli appunti e incollarlo nella casella di testo **Certificato X.509**</span><span class="sxs-lookup"><span data-stu-id="40e58-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="40e58-184">d.</span><span class="sxs-lookup"><span data-stu-id="40e58-184">d.</span></span> <span data-ttu-id="40e58-185">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="40e58-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="40e58-186">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="40e58-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="40e58-187">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="40e58-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="40e58-188">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40e58-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40e58-189">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="40e58-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="40e58-190">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40e58-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="40e58-192">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="40e58-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="40e58-193">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="40e58-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40e58-195">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="40e58-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40e58-197">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="40e58-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40e58-199">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="40e58-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40e58-201">a.</span><span class="sxs-lookup"><span data-stu-id="40e58-201">a.</span></span> <span data-ttu-id="40e58-202">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40e58-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="40e58-203">b.</span><span class="sxs-lookup"><span data-stu-id="40e58-203">b.</span></span> <span data-ttu-id="40e58-204">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="40e58-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40e58-205">c.</span><span class="sxs-lookup"><span data-stu-id="40e58-205">c.</span></span> <span data-ttu-id="40e58-206">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="40e58-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="40e58-207">d.</span><span class="sxs-lookup"><span data-stu-id="40e58-207">d.</span></span> <span data-ttu-id="40e58-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="40e58-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="40e58-209">Creazione di un utente test di Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="40e58-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="40e58-210">Per consentire agli utenti di Azure AD di accedere a Jitbit Helpdesk, è necessario eseguirne il provisioning in Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="40e58-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="40e58-211">Nel caso di Jitbit Helpdesk, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="40e58-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="40e58-212">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="40e58-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="40e58-213">Accedere al tenant di **Jitbit Helpdesk** .</span><span class="sxs-lookup"><span data-stu-id="40e58-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="40e58-214">Scegliere **Amministrazione**dal menu disponibile nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="40e58-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="40e58-215">![Amministrazione](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="40e58-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="40e58-216">Fare clic su **Users, companies and permissions**.</span><span class="sxs-lookup"><span data-stu-id="40e58-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="40e58-217">![Users, companies and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies and permissions")</span><span class="sxs-lookup"><span data-stu-id="40e58-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="40e58-218">Fare clic su **Add User**.</span><span class="sxs-lookup"><span data-stu-id="40e58-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="40e58-219">![Aggiungere un utente](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="40e58-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="40e58-220">Nella sezione Create immettere i dati dell'account di Azure AD di cui si desidera eseguire il provisioning come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="40e58-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="40e58-221">![Creare](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="40e58-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="40e58-222">a.</span><span class="sxs-lookup"><span data-stu-id="40e58-222">a.</span></span> <span data-ttu-id="40e58-223">Nella casella di testo **Username** (Nome utente) digitare **Britta Simon**, il nome utente come nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40e58-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="40e58-224">b.</span><span class="sxs-lookup"><span data-stu-id="40e58-224">b.</span></span> <span data-ttu-id="40e58-225">Nella casella di testo **Email** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica dell'utente, ad esempio **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="40e58-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="40e58-226">c.</span><span class="sxs-lookup"><span data-stu-id="40e58-226">c.</span></span> <span data-ttu-id="40e58-227">Digitare il nome dell'utente, ad esempio **Britta**, nella casella di testo **First Name** (Nome).</span><span class="sxs-lookup"><span data-stu-id="40e58-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="40e58-228">d.</span><span class="sxs-lookup"><span data-stu-id="40e58-228">d.</span></span> <span data-ttu-id="40e58-229">Digitare il cognome dell'utente, ad esempio **Simon**, nella casella di testo **Last Name** (Cognome).</span><span class="sxs-lookup"><span data-stu-id="40e58-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="40e58-230">e.</span><span class="sxs-lookup"><span data-stu-id="40e58-230">e.</span></span> <span data-ttu-id="40e58-231">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="40e58-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="40e58-232">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Jitbit Helpdesk per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40e58-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="40e58-233">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="40e58-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="40e58-234">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="40e58-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![Assegna utente][200] 

<span data-ttu-id="40e58-236">**Per assegnare Britta Simon a Jitbit Helpdesk, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="40e58-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="40e58-237">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="40e58-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="40e58-239">Nell'elenco delle applicazioni selezionare **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="40e58-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="40e58-241">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="40e58-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="40e58-243">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="40e58-243">Click **Add** button.</span></span> <span data-ttu-id="40e58-244">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="40e58-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="40e58-246">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="40e58-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="40e58-247">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="40e58-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40e58-248">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="40e58-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="40e58-249">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="40e58-249">Testing single sign-on</span></span>

<span data-ttu-id="40e58-250">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="40e58-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="40e58-251">Quando si fa clic sul riquadro Jitbit Helpdesk nel Pannello di accesso, viene visualizzata la pagina di accesso dell'applicazione Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="40e58-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="40e58-252">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="40e58-252">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40e58-253">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="40e58-253">Additional resources</span></span>

* [<span data-ttu-id="40e58-254">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40e58-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40e58-255">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40e58-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

