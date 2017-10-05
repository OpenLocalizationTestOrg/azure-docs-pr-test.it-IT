---
title: 'Esercitazione: integrazione di Azure Active Directory con Five9 Plus Adapter (CTI, Contact Center Agents) | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Five9 Plus Adapter (CTI, Contact Center Agents).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: d75163ea5eb3fa811e07861f06e6c4d5c758b898
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="aa27f-103">Esercitazione: integrazione di Azure Active Directory con Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="aa27f-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="aa27f-104">Questa esercitazione descrive come integrare Five9 Plus Adapter (CTI, Contact Center Agents) con Azure Active Directory, ovvero Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa27f-104">In this tutorial, you learn how to integrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa27f-105">L'integrazione di Five9 Plus Adapter (CTI, Contact Center Agents) con Azure AD comporta i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa27f-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aa27f-106">È possibile controllare in Azure AD che ha accesso a Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="aa27f-106">You can control in Azure AD who has access to Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="aa27f-107">È possibile abilitare gli utenti per l'accesso automatico a Five9 Plus Adapter (CTI, Contact Center Agents), ovvero per l'accesso Single Sign-On, con i propri account di Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa27f-107">You can enable your users to automatically get signed-on to Five9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa27f-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa27f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="aa27f-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa27f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa27f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="aa27f-110">Prerequisites</span></span>

<span data-ttu-id="aa27f-111">Per configurare l'integrazione di Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents), sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa27f-111">To configure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need the following items:</span></span>

- <span data-ttu-id="aa27f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa27f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa27f-113">Sottoscrizione abilitata all'accesso Single Sign-On per Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="aa27f-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa27f-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="aa27f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa27f-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa27f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa27f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="aa27f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa27f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa27f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa27f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="aa27f-118">Scenario description</span></span>
<span data-ttu-id="aa27f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="aa27f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa27f-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa27f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa27f-121">Aggiunta di Five9 Plus Adapter (CTI, Contact Center Agents) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="aa27f-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
2. <span data-ttu-id="aa27f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa27f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-the-gallery"></a><span data-ttu-id="aa27f-123">Aggiunta di Five9 Plus Adapter (CTI, Contact Center Agents) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="aa27f-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
<span data-ttu-id="aa27f-124">Per configurare l'integrazione di Five9 Plus Adapter (CTI, Contact Center Agents) in Azure AD, è necessario aggiungere Five9 Plus Adapter (CTI, Contact Center Agents) dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="aa27f-124">To configure the integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need to add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aa27f-125">**Per aggiungere Five9 Plus Adapter (CTI, Contact Center Agents) dalla raccolta, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="aa27f-125">**To add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aa27f-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="aa27f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa27f-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aa27f-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="aa27f-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="aa27f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="aa27f-133">Nella casella di ricerca digitare **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-133">In the search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="aa27f-135">Nel pannello dei risultati selezionare **Five9 Plus Adapter (CTI, Contact Center Agents)**, quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aa27f-135">In the results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa27f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa27f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa27f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents) in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aa27f-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aa27f-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Five9 Plus Adapter (CTI, Contact Center Agents) che corrisponde all'utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa27f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is to a user in Azure AD.</span></span> <span data-ttu-id="aa27f-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato inFive9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="aa27f-140">In other words, a link relationship between an Azure AD user and the related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs to be established.</span></span>

<span data-ttu-id="aa27f-141">Per stabilire la relazione di collegamento, in Five9 Plus Adapter (CTI, Contact Center Agents) assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="aa27f-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="aa27f-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents), è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa27f-142">To configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aa27f-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="aa27f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aa27f-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa27f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa27f-145">**[Creazione di un utente test di Five9 Plus Adapter (CTI, Contact Center Agents)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** : per avere una controparte di Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) collegata alla rappresentazione dell'utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa27f-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - to have a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa27f-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa27f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa27f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="aa27f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa27f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa27f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa27f-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="aa27f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="aa27f-150">**Per configurare il Single Sign-On di Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents) seguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="aa27f-150">**To configure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="aa27f-151">Nel portale di Azure, nella pagina di integrazione dell'applicazione **Five9 Plus Adapter (CTI, Contact Center Agents)** fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-151">In the Azure portal, on the **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="aa27f-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="aa27f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="aa27f-155">Nella sezione **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** (URL e dominio di Five9 Plus Adapter (CTI, Contact Center Agents)) eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="aa27f-155">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="aa27f-157">a.</span><span class="sxs-lookup"><span data-stu-id="aa27f-157">a.</span></span> <span data-ttu-id="aa27f-158">Nella casella di testo **Identificatore** digitare un URL usando i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa27f-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span>

    |    <span data-ttu-id="aa27f-159">Environment</span><span class="sxs-lookup"><span data-stu-id="aa27f-159">Environment</span></span>      |       <span data-ttu-id="aa27f-160">URL</span><span class="sxs-lookup"><span data-stu-id="aa27f-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="aa27f-161">Per "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="aa27f-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="aa27f-162">Per "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="aa27f-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="aa27f-163">Per "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="aa27f-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="aa27f-164">b.</span><span class="sxs-lookup"><span data-stu-id="aa27f-164">b.</span></span> <span data-ttu-id="aa27f-165">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="aa27f-165">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    |      <span data-ttu-id="aa27f-166">Environment</span><span class="sxs-lookup"><span data-stu-id="aa27f-166">Environment</span></span>     |      <span data-ttu-id="aa27f-167">URL</span><span class="sxs-lookup"><span data-stu-id="aa27f-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="aa27f-168">Per "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="aa27f-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="aa27f-169">Per "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="aa27f-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="aa27f-170">Per "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="aa27f-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="aa27f-171">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="aa27f-171">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="aa27f-173">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="aa27f-173">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aa27f-175">Nella sezione **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** (Configurazione di Five9 Plus Adapter (CTI, Contact Center Agents)) fare clic su **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** (Configura Five9 Plus Adapter (CTI, Contact Center Agents)) per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-175">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="aa27f-176">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="aa27f-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="aa27f-178">Per configurare l'accesso Single Sign-On sul lato **Five9 Plus Adapter (CTI, Contact Center Agents)**, è necessario inviare il file **Certificato (Base64) scaricato, l'URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di Five9 Plus Adapter (CTI, Contact Center Agents)](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="aa27f-178">To configure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="aa27f-179">In aggiunta, per proseguire la configurazione SSO seguire la procedura di seguito in base all'adattatore:</span><span class="sxs-lookup"><span data-stu-id="aa27f-179">Also additionally, for configuring SSO further please follow the below steps according to the adapter:</span></span>

    <span data-ttu-id="aa27f-180">a.</span><span class="sxs-lookup"><span data-stu-id="aa27f-180">a.</span></span> <span data-ttu-id="aa27f-181">Guida dell'amministratore per "Five9 Plus Adapter per Agent Desktop Toolkit": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="aa27f-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="aa27f-182">b.</span><span class="sxs-lookup"><span data-stu-id="aa27f-182">b.</span></span> <span data-ttu-id="aa27f-183">Guida dell'amministratore per "Five9 Plus Adapter per Microsoft Dynamics CRM": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="aa27f-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="aa27f-184">c.</span><span class="sxs-lookup"><span data-stu-id="aa27f-184">c.</span></span> <span data-ttu-id="aa27f-185">Guida dell'amministratore per "Five9 Plus Adapter per Zendesk": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="aa27f-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="aa27f-186">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="aa27f-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="aa27f-187">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="aa27f-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="aa27f-188">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa27f-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa27f-189">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa27f-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa27f-190">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="aa27f-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="aa27f-192">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="aa27f-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aa27f-193">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="aa27f-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa27f-195">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="aa27f-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa27f-197">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa27f-199">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="aa27f-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa27f-201">a.</span><span class="sxs-lookup"><span data-stu-id="aa27f-201">a.</span></span> <span data-ttu-id="aa27f-202">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa27f-203">b.</span><span class="sxs-lookup"><span data-stu-id="aa27f-203">b.</span></span> <span data-ttu-id="aa27f-204">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aa27f-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa27f-205">c.</span><span class="sxs-lookup"><span data-stu-id="aa27f-205">c.</span></span> <span data-ttu-id="aa27f-206">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aa27f-207">d.</span><span class="sxs-lookup"><span data-stu-id="aa27f-207">d.</span></span> <span data-ttu-id="aa27f-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="aa27f-209">Creazione dell'utente test di Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="aa27f-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="aa27f-210">In questa sezione si crea un utente chiamato Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="aa27f-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="aa27f-211">Contattare il [team di supporto di Five9 Plus Adapter (CTI, Contact Center Agents)](https://www.five9.com/about/contact) per aggiungere gli utenti nella piattaforma Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="aa27f-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add the users in the Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="aa27f-212">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="aa27f-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aa27f-213">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa27f-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="aa27f-214">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="aa27f-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Five9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Assegna utente][200] 

<span data-ttu-id="aa27f-216">**Per assegnare Britta Simon a Five9 Plus Adapter (CTI, Contact Center Agents), eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="aa27f-216">**To assign Britta Simon to Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="aa27f-217">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="aa27f-219">Nell'elenco delle applicazioni selezionare **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-219">In the applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="aa27f-221">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="aa27f-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="aa27f-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-223">Click **Add** button.</span></span> <span data-ttu-id="aa27f-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="aa27f-226">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="aa27f-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aa27f-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa27f-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="aa27f-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa27f-229">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="aa27f-229">Testing single sign-on</span></span>

<span data-ttu-id="aa27f-230">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="aa27f-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="aa27f-231">Quando si fa clic sul riquadro Five9 Plus Adapter (CTI, Contact Center Agents) nel Pannello di accesso, l'utente dovrebbe accedere automaticamente all'applicazione Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="aa27f-231">When you click the Five9 Plus Adapter (CTI, Contact Center Agents) tile in the Access Panel, you should get automatically signed-on to your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="aa27f-232">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aa27f-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa27f-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="aa27f-233">Additional resources</span></span>

* [<span data-ttu-id="aa27f-234">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa27f-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa27f-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa27f-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

