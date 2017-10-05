---
title: 'Esercitazione: Integrazione di Azure Active Directory con Hosted Graphite | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Hosted Graphite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f6ed02cc67be4090402a115c30819ff6cff99c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="e0717-103">Esercitazione: Integrazione di Azure Active Directory con Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="e0717-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="e0717-104">Questa esercitazione descrive come integrare Hosted Graphite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e0717-104">In this tutorial, you learn how to integrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e0717-105">L'integrazione di Hosted Graphite in Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e0717-105">Integrating Hosted Graphite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e0717-106">È possibile controllare in Azure AD gli utenti che possono accedere a Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="e0717-106">You can control in Azure AD who has access to Hosted Graphite</span></span>
- <span data-ttu-id="e0717-107">È possibile abilitare gli utenti per l'accesso automatico a Hosted Graphite (Single Sign-On) con il proprio account Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0717-107">You can enable your users to automatically get signed-on to Hosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e0717-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0717-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e0717-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e0717-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0717-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e0717-110">Prerequisites</span></span>

<span data-ttu-id="e0717-111">Per configurare l'integrazione di Azure AD in Hosted Graphite, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="e0717-111">To configure Azure AD integration with Hosted Graphite, you need the following items:</span></span>

- <span data-ttu-id="e0717-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0717-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e0717-113">Sottoscrizione di Hosted Graphite abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e0717-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e0717-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e0717-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e0717-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e0717-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e0717-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e0717-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e0717-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0717-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e0717-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e0717-118">Scenario description</span></span>
<span data-ttu-id="e0717-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e0717-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e0717-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e0717-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e0717-121">Aggiunta di Hosted Graphite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e0717-121">Adding Hosted Graphite from the gallery</span></span>
2. <span data-ttu-id="e0717-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0717-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-the-gallery"></a><span data-ttu-id="e0717-123">Aggiunta di Hosted Graphite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="e0717-123">Adding Hosted Graphite from the gallery</span></span>
<span data-ttu-id="e0717-124">Per configurare l'integrazione di Hosted Graphite in Azure AD, è necessario aggiungere Hosted Graphite dalla raccolta all'elenco delle app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e0717-124">To configure the integration of Hosted Graphite into Azure AD, you need to add Hosted Graphite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e0717-125">**Per aggiungere Hosted Graphite dalla raccolta, eseguire i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="e0717-125">**To add Hosted Graphite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e0717-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="e0717-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e0717-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e0717-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e0717-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e0717-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e0717-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="e0717-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e0717-133">Nella casella di ricerca digitare **Hosted Graphite**.</span><span class="sxs-lookup"><span data-stu-id="e0717-133">In the search box, type **Hosted Graphite**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="e0717-135">Nel pannello dei risultati selezionare **Hosted Graphite** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e0717-135">In the results panel, select **Hosted Graphite**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e0717-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0717-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e0717-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Hosted Graphite mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e0717-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e0717-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Hosted Graphite corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0717-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hosted Graphite is to a user in Azure AD.</span></span> <span data-ttu-id="e0717-140">In altre parole, è necessario stabilire una relazione di collegamento fra un utente di AD Azure e l'utente correlato di Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="e0717-140">In other words, a link relationship between an Azure AD user and the related user in Hosted Graphite needs to be established.</span></span>

<span data-ttu-id="e0717-141">Per stabilire la relazione di collegamento, in Hosted Graphite assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="e0717-141">In Hosted Graphite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e0717-142">Per configurare e testare l'accesso Single Sign-On in AD Azure con Hosted Graphite, è necessario completare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e0717-142">To configure and test Azure AD single sign-on with Hosted Graphite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e0717-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e0717-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e0717-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0717-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e0717-145">**[Creazione di un utente test di Hosted Graphite](#creating-a-hosted-graphite-test-user)**: per avere una controparte di Britta Simon in Hosted Graphite collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0717-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - to have a counterpart of Britta Simon in Hosted Graphite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e0717-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0717-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e0717-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="e0717-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e0717-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0717-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e0717-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="e0717-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="e0717-150">**Per configurare l'accesso Single Sign-On in Azure AD con Hosted Graphite, procedere come segue:**</span><span class="sxs-lookup"><span data-stu-id="e0717-150">**To configure Azure AD single sign-on with Hosted Graphite, perform the following steps:**</span></span>

1. <span data-ttu-id="e0717-151">Nella pagina di integrazione dell'applicazione **Hosted Graphite** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e0717-151">In the Azure portal, on the **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e0717-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e0717-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="e0717-155">Nella sezione **URL e dominio Hosted Graphite** seguire questa procedura per configurare l'applicazione in **modalità avviata da IDP**:</span><span class="sxs-lookup"><span data-stu-id="e0717-155">On the **Hosted Graphite Domain and URLs** section, if you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="e0717-157">a.</span><span class="sxs-lookup"><span data-stu-id="e0717-157">a.</span></span> <span data-ttu-id="e0717-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="e0717-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="e0717-159">b.</span><span class="sxs-lookup"><span data-stu-id="e0717-159">b.</span></span> <span data-ttu-id="e0717-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="e0717-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="e0717-161">Nella sezione **URL e dominio Hosted Graphite** seguire questa procedura per configurare l'applicazione in **modalità avviata da SP**:</span><span class="sxs-lookup"><span data-stu-id="e0717-161">On the **Hosted Graphite Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="e0717-163">a.</span><span class="sxs-lookup"><span data-stu-id="e0717-163">a.</span></span> <span data-ttu-id="e0717-164">Fare clic sull'opzione **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="e0717-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="e0717-165">b.</span><span class="sxs-lookup"><span data-stu-id="e0717-165">b.</span></span> <span data-ttu-id="e0717-166">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="e0717-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="e0717-167">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="e0717-167">Please note that these are not the real values.</span></span> <span data-ttu-id="e0717-168">È necessario aggiornare questi valori con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="e0717-168">You have to update these values with the actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="e0717-169">Per ottenere questi valori passare a Access->SAML setup (Accesso -> Configurazione SAML) nell'applicazione oppure contattare il [team di supporto di Hosted Graphite](mailto:help@hostedgraphite.com).</span><span class="sxs-lookup"><span data-stu-id="e0717-169">To get these values, you can go to Access->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="e0717-170">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="e0717-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="e0717-172">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e0717-172">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e0717-174">Nella sezione **Configurazione di Hosted Graphite** fare clic su **Configura Hosted Graphite** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="e0717-174">On the **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e0717-175">Copiare i valori **SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="e0717-175">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="e0717-177">Accedere al tenant di Hosted Graphite come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e0717-177">Sign-on to your Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="e0717-178">Accedere alla **pagina SAML Setup** (Configurazione SAML) dalla barra laterale, facendo clic su **Accesso -> SAML Setup (Configurazione SAML)**.</span><span class="sxs-lookup"><span data-stu-id="e0717-178">Go to the **SAML Setup page** in the sidebar (**Access -> SAML Setup**).</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="e0717-180">Verificare che gli URL corrispondano alla configurazione eseguita nella sezione **URL e Dominio Hosted Graphite** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0717-180">Confirm these URls match your configuration done on the **Hosted Graphite Domain and URLs** section of the Azure portal.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="e0717-182">Nelle caselle di testo **Entity or Issuer ID** (ID entità o emittente) e **SSO Login URL** (URL di accesso SSO) incollare i valori di **SAML Entity ID** (ID entità SAML) e **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiati dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0717-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste the value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="e0717-184">Selezionare "**Sola lettura**" come **ruolo utente predefinito**.</span><span class="sxs-lookup"><span data-stu-id="e0717-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="e0717-186">Aprire nel Blocco note il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **Certificato X.509**.</span><span class="sxs-lookup"><span data-stu-id="e0717-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="e0717-188">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e0717-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="e0717-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="e0717-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e0717-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="e0717-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e0717-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e0717-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e0717-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0717-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e0717-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0717-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e0717-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e0717-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e0717-196">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="e0717-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e0717-198">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="e0717-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e0717-200">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="e0717-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e0717-202">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e0717-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e0717-204">a.</span><span class="sxs-lookup"><span data-stu-id="e0717-204">a.</span></span> <span data-ttu-id="e0717-205">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e0717-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e0717-206">b.</span><span class="sxs-lookup"><span data-stu-id="e0717-206">b.</span></span> <span data-ttu-id="e0717-207">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e0717-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e0717-208">c.</span><span class="sxs-lookup"><span data-stu-id="e0717-208">c.</span></span> <span data-ttu-id="e0717-209">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="e0717-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e0717-210">d.</span><span class="sxs-lookup"><span data-stu-id="e0717-210">d.</span></span> <span data-ttu-id="e0717-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e0717-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="e0717-212">Creazione di un utente test di Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="e0717-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="e0717-213">Questa sezione descrive come creare un utente chiamato Britta Simon in Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="e0717-213">The objective of this section is to create a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="e0717-214">Hosted Graphite supporta il provisioning JIT, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e0717-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="e0717-215">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="e0717-215">There is no action item for you in this section.</span></span> <span data-ttu-id="e0717-216">Durante un tentativo di accesso a Hosted Graphite verrà creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="e0717-216">A new user will be created during an attempt to access Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="e0717-217">Per creare un utente manualmente, contattare il team di supporto di Hosted Graphite all'indirizzo <mailto:help@hostedgraphite.com>.</span><span class="sxs-lookup"><span data-stu-id="e0717-217">If you need to create a user manually, you need to contact the Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e0717-218">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0717-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e0717-219">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="e0717-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hosted Graphite.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e0717-221">**Per assegnare Britta Simon a Hosted Graphite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e0717-221">**To assign Britta Simon to Hosted Graphite, perform the following steps:**</span></span>

1. <span data-ttu-id="e0717-222">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e0717-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e0717-224">Nell'elenco delle applicazioni selezionare **Hosted Graphite**.</span><span class="sxs-lookup"><span data-stu-id="e0717-224">In the applications list, select **Hosted Graphite**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="e0717-226">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e0717-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e0717-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e0717-228">Click **Add** button.</span></span> <span data-ttu-id="e0717-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e0717-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e0717-231">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="e0717-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e0717-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e0717-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e0717-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e0717-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e0717-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e0717-234">Testing single sign-on</span></span>

<span data-ttu-id="e0717-235">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e0717-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e0717-236">Quando si fa clic sul riquadro Hosted Graphite nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="e0717-236">When you click the Hosted Graphite tile in the Access Panel, you should get automatically signed-on to your Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e0717-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e0717-237">Additional resources</span></span>

* [<span data-ttu-id="e0717-238">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0717-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e0717-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0717-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

