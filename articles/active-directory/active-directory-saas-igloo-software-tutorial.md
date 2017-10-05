---
title: 'Esercitazione: Integrazione di Azure Active Directory con Igloo Software | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Igloo Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="101d1-103">Esercitazione: Integrazione di Azure Active Directory con Igloo Software</span><span class="sxs-lookup"><span data-stu-id="101d1-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="101d1-104">Questa esercitazione descrive come integrare Igloo Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="101d1-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="101d1-105">L'integrazione di Igloo Software con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="101d1-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="101d1-106">È possibile controllare in Azure AD chi può accedere a Igloo Software</span><span class="sxs-lookup"><span data-stu-id="101d1-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="101d1-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a Igloo Software con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="101d1-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="101d1-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="101d1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="101d1-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="101d1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="101d1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="101d1-110">Prerequisites</span></span>

<span data-ttu-id="101d1-111">Per configurare l'integrazione di Azure AD con Igloo Software sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="101d1-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="101d1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="101d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="101d1-113">Sottoscrizione di Igloo Software abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="101d1-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="101d1-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="101d1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="101d1-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="101d1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="101d1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="101d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="101d1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="101d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="101d1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="101d1-118">Scenario description</span></span>
<span data-ttu-id="101d1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="101d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="101d1-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="101d1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="101d1-121">Aggiunta di Igloo Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="101d1-121">Adding Igloo Software from the gallery</span></span>
2. <span data-ttu-id="101d1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="101d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="101d1-123">Aggiunta di Igloo Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="101d1-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="101d1-124">Per configurare l'integrazione di Igloo Software in Azure AD è necessario aggiungere Igloo Software dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="101d1-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="101d1-125">**Per aggiungere Igloo Software dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="101d1-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="101d1-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="101d1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="101d1-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="101d1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="101d1-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="101d1-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="101d1-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="101d1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="101d1-133">Nella casella di ricerca digitare **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="101d1-133">In the search box, type **Igloo Software**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="101d1-135">Nel pannello dei risultati selezionare **Igloo Software** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="101d1-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="101d1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="101d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="101d1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Igloo Software mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="101d1-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="101d1-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Igloo Software corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="101d1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="101d1-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="101d1-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="101d1-141">Per stabilire la relazione di collegamento, in Igloo Software assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="101d1-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="101d1-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Igloo Software è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="101d1-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="101d1-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="101d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="101d1-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="101d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="101d1-145">**[Creazione di un utente test di Igloo Software](#creating-an-igloo-software-test-user)**: per avere una controparte di Britta Simon in Igloo Software collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="101d1-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="101d1-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="101d1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="101d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="101d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="101d1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="101d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="101d1-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="101d1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="101d1-150">**Per configurare l'accesso Single Sign-On di Azure AD con Igloo Software, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="101d1-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="101d1-151">Nella pagina di integrazione dell'applicazione **Igloo Software** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="101d1-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="101d1-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="101d1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="101d1-155">Nella sezione **URL e dominio Igloo Software** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="101d1-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="101d1-157">a.</span><span class="sxs-lookup"><span data-stu-id="101d1-157">a.</span></span> <span data-ttu-id="101d1-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.igloocommmunities.com`.</span><span class="sxs-lookup"><span data-stu-id="101d1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="101d1-159">b.</span><span class="sxs-lookup"><span data-stu-id="101d1-159">b.</span></span> <span data-ttu-id="101d1-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="101d1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="101d1-161">c.</span><span class="sxs-lookup"><span data-stu-id="101d1-161">c.</span></span> <span data-ttu-id="101d1-162">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="101d1-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="101d1-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="101d1-163">These values are not real.</span></span> <span data-ttu-id="101d1-164">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="101d1-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="101d1-165">Per ottenere questi valori contattare il [team di supporto clienti di Igloo Software](https://www.igloosoftware.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="101d1-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

4. <span data-ttu-id="101d1-166">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="101d1-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="101d1-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="101d1-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="101d1-170">Nella sezione **Configurazione di Igloo Software** fare clic su **Configura Igloo Software** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="101d1-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="101d1-171">Copiare l'**URL servizio Single Sign-On SAML e l'URL di disconnessione** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="101d1-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="101d1-173">In un'altra finestra del Web browser accedere al sito aziendale di Igloo Software come amministratore.</span><span class="sxs-lookup"><span data-stu-id="101d1-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="101d1-174">Passare a **Control panel**.</span><span class="sxs-lookup"><span data-stu-id="101d1-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="101d1-175">![Pannello di controllo](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Pannello di controllo")</span><span class="sxs-lookup"><span data-stu-id="101d1-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="101d1-176">Nella scheda **Appartenenza** fare clic su **Sign In Settings**.</span><span class="sxs-lookup"><span data-stu-id="101d1-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="101d1-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span><span class="sxs-lookup"><span data-stu-id="101d1-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="101d1-178">Nella sezione relativa alla configurazione SAML fare clic su **Configure SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="101d1-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="101d1-179">![Configurazione SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="101d1-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="101d1-180">Nella sezione **General Configuration** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="101d1-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="101d1-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span><span class="sxs-lookup"><span data-stu-id="101d1-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="101d1-182">a.</span><span class="sxs-lookup"><span data-stu-id="101d1-182">a.</span></span> <span data-ttu-id="101d1-183">Nella casella di testo **Connection Name** digitare un nome personalizzato per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="101d1-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="101d1-184">b.</span><span class="sxs-lookup"><span data-stu-id="101d1-184">b.</span></span> <span data-ttu-id="101d1-185">Nella casella di testo **IdP Login URL** (URL di accesso IdP) incollare il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="101d1-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="101d1-186">c.</span><span class="sxs-lookup"><span data-stu-id="101d1-186">c.</span></span> <span data-ttu-id="101d1-187">Nella casella di testo **IdP Logout URL** (URL di disconnessione IdP) incollare il valore di **Sign-Out URL** (URL di disconnessione) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="101d1-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="101d1-188">d.</span><span class="sxs-lookup"><span data-stu-id="101d1-188">d.</span></span> <span data-ttu-id="101d1-189">Selezionare **Logout Response and Request HTTP Type** (Risposta di disconnessione e tipo di richiesta HTTP) con l'impostazione **POST**.</span><span class="sxs-lookup"><span data-stu-id="101d1-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="101d1-190">e.</span><span class="sxs-lookup"><span data-stu-id="101d1-190">e.</span></span> <span data-ttu-id="101d1-191">Aprire nel Blocco note il certificato con codifica **Base 64** scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **Public Certificate** (Certificato pubblico).</span><span class="sxs-lookup"><span data-stu-id="101d1-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="101d1-192">In **Configurazione risposta e autenticazione**seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="101d1-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="101d1-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span><span class="sxs-lookup"><span data-stu-id="101d1-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="101d1-194">a.</span><span class="sxs-lookup"><span data-stu-id="101d1-194">a.</span></span> <span data-ttu-id="101d1-195">In **Provider di identità** selezionare **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="101d1-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="101d1-196">b.</span><span class="sxs-lookup"><span data-stu-id="101d1-196">b.</span></span> <span data-ttu-id="101d1-197">In **Tipo di identificatore** selezionare **Indirizzo e-mail**.</span><span class="sxs-lookup"><span data-stu-id="101d1-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="101d1-198">c.</span><span class="sxs-lookup"><span data-stu-id="101d1-198">c.</span></span> <span data-ttu-id="101d1-199">Nella casella di testo **Attributo posta elettronica** digitare **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="101d1-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="101d1-200">d.</span><span class="sxs-lookup"><span data-stu-id="101d1-200">d.</span></span> <span data-ttu-id="101d1-201">Nella casella di testo **Attributo nome** digitare **nomeproprio**.</span><span class="sxs-lookup"><span data-stu-id="101d1-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="101d1-202">e.</span><span class="sxs-lookup"><span data-stu-id="101d1-202">e.</span></span> <span data-ttu-id="101d1-203">Nella casella di testo **Attributo cognome** digitare **cognome**.</span><span class="sxs-lookup"><span data-stu-id="101d1-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="101d1-204">Per completare la configurazione seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="101d1-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="101d1-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span><span class="sxs-lookup"><span data-stu-id="101d1-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="101d1-206">a.</span><span class="sxs-lookup"><span data-stu-id="101d1-206">a.</span></span> <span data-ttu-id="101d1-207">In **User creation on Sign in** (Creazione utente all'accesso) selezionare **Create a new user in your site when they sign in** (Creare un nuovo utente all'accesso).</span><span class="sxs-lookup"><span data-stu-id="101d1-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="101d1-208">b.</span><span class="sxs-lookup"><span data-stu-id="101d1-208">b.</span></span> <span data-ttu-id="101d1-209">In **Impostazioni di accesso** selezionare **Usa pulsante SAML nella schermata di accesso**.</span><span class="sxs-lookup"><span data-stu-id="101d1-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="101d1-210">c.</span><span class="sxs-lookup"><span data-stu-id="101d1-210">c.</span></span> <span data-ttu-id="101d1-211">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="101d1-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="101d1-212">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="101d1-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="101d1-213">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="101d1-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="101d1-214">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="101d1-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="101d1-215">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="101d1-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="101d1-216">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="101d1-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="101d1-218">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="101d1-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="101d1-219">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="101d1-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="101d1-221">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="101d1-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="101d1-223">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="101d1-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="101d1-225">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="101d1-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="101d1-227">a.</span><span class="sxs-lookup"><span data-stu-id="101d1-227">a.</span></span> <span data-ttu-id="101d1-228">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="101d1-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="101d1-229">b.</span><span class="sxs-lookup"><span data-stu-id="101d1-229">b.</span></span> <span data-ttu-id="101d1-230">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="101d1-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="101d1-231">c.</span><span class="sxs-lookup"><span data-stu-id="101d1-231">c.</span></span> <span data-ttu-id="101d1-232">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="101d1-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="101d1-233">d.</span><span class="sxs-lookup"><span data-stu-id="101d1-233">d.</span></span> <span data-ttu-id="101d1-234">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="101d1-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="101d1-235">Creazione di un utente test di Igloo Software</span><span class="sxs-lookup"><span data-stu-id="101d1-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="101d1-236">Non è richiesto alcun intervento dell'utente per configurare il provisioning degli utenti in Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="101d1-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="101d1-237">Quando un utente assegnato prova ad accedere a Igloo Software usando il pannello di accesso, Igloo Software verifica se l'utente esiste.</span><span class="sxs-lookup"><span data-stu-id="101d1-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="101d1-238">Se l'account utente non è presente, Igloo Software lo crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="101d1-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="101d1-239">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="101d1-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="101d1-240">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="101d1-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![Assegna utente][200] 

<span data-ttu-id="101d1-242">**Per assegnare Britta Simon a Igloo Software, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="101d1-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="101d1-243">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="101d1-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="101d1-245">Nell'elenco delle applicazioni selezionare **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="101d1-245">In the applications list, select **Igloo Software**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="101d1-247">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="101d1-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="101d1-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="101d1-249">Click **Add** button.</span></span> <span data-ttu-id="101d1-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="101d1-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="101d1-252">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="101d1-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="101d1-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="101d1-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="101d1-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="101d1-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="101d1-255">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="101d1-255">Testing single sign-on</span></span>

<span data-ttu-id="101d1-256">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="101d1-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="101d1-257">Quando si fa clic sul riquadro Igloo Software nel pannello di accesso si accede automaticamente all'applicazione Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="101d1-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="101d1-258">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="101d1-258">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="101d1-259">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="101d1-259">Additional resources</span></span>

* [<span data-ttu-id="101d1-260">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="101d1-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="101d1-261">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="101d1-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

