---
title: 'Esercitazione: Integrazione di Azure Active Directory con SumoLogic| Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SumoLogic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e739106472ccf930b2942eb810dd844f2b1ade7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="90834-103">Esercitazione: Integrazione di Azure Active Directory con SumoLogic</span><span class="sxs-lookup"><span data-stu-id="90834-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="90834-104">Questa esercitazione descrive come integrare SumoLogic con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90834-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90834-105">L'integrazione di SumoLogic con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="90834-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="90834-106">È possibile controllare in Azure AD chi può accedere a SumoLogic</span><span class="sxs-lookup"><span data-stu-id="90834-106">You can control in Azure AD who has access to SumoLogic</span></span>
- <span data-ttu-id="90834-107">È possibile abilitare gli utenti per l'accesso automatico a SumoLogic (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="90834-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90834-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="90834-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="90834-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90834-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90834-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="90834-110">Prerequisites</span></span>

<span data-ttu-id="90834-111">Per configurare l'integrazione di Azure AD con SumoLogic, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="90834-111">To configure Azure AD integration with SumoLogic, you need the following items:</span></span>

- <span data-ttu-id="90834-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90834-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90834-113">Sottoscrizione di SumoLogic abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="90834-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90834-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="90834-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90834-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="90834-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90834-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="90834-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90834-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90834-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90834-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="90834-118">Scenario description</span></span>
<span data-ttu-id="90834-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="90834-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90834-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="90834-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90834-121">Aggiunta di SumoLogic dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="90834-121">Adding SumoLogic from the gallery</span></span>
2. <span data-ttu-id="90834-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90834-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-the-gallery"></a><span data-ttu-id="90834-123">Aggiunta di SumoLogic dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="90834-123">Adding SumoLogic from the gallery</span></span>
<span data-ttu-id="90834-124">Per configurare l'integrazione di SumoLogic in Azure AD, è necessario aggiungere SumoLogic dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="90834-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="90834-125">**Per aggiungere SumoLogic dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="90834-125">**To add SumoLogic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="90834-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="90834-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90834-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="90834-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="90834-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="90834-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="90834-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="90834-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="90834-133">Nella casella di ricerca digitare **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="90834-133">In the search box, type **SumoLogic**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="90834-135">Nel pannello dei risultati selezionare **SumoLogic** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="90834-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90834-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90834-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90834-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SumoLogic usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="90834-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="90834-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di SumoLogic corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90834-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span></span> <span data-ttu-id="90834-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="90834-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span></span>

<span data-ttu-id="90834-141">Per stabilire la relazione di collegamento, in SumoLogic assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="90834-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="90834-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SumoLogic, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="90834-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="90834-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="90834-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="90834-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90834-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90834-145">**[Creazione di un utente di test di SumoLogic](#creating-a-sumologic-test-user)**: per avere una controparte di Britta Simon in SumoLogic collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90834-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="90834-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90834-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90834-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="90834-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90834-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90834-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90834-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="90834-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="90834-150">**Per configurare l'accesso Single Sign-On di Azure AD con SumoLogic, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="90834-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="90834-151">Nella pagina di integrazione dell'applicazione **SumoLogic** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="90834-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="90834-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="90834-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="90834-155">Nella sezione **URL e dominio SumoLogic** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="90834-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="90834-157">a.</span><span class="sxs-lookup"><span data-stu-id="90834-157">a.</span></span> <span data-ttu-id="90834-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenantname>.SumoLogic.com`.</span><span class="sxs-lookup"><span data-stu-id="90834-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="90834-159">b.</span><span class="sxs-lookup"><span data-stu-id="90834-159">b.</span></span> <span data-ttu-id="90834-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="90834-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="90834-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="90834-161">These values are not real.</span></span> <span data-ttu-id="90834-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="90834-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="90834-163">Per ottenere questi valori, contattare il [team di supporto clienti di SumoLogic](https://www.sumologic.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="90834-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="90834-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="90834-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="90834-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="90834-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="90834-168">Nella sezione **Configurazione di SumoLogic** fare clic su **Configura SumoLogic** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="90834-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="90834-169">Copiare i valori **SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="90834-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="90834-171">In un'altra finestra del Web browser accedere al sito aziendale di SumoLogic come amministratore.</span><span class="sxs-lookup"><span data-stu-id="90834-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="90834-172">Passare a **Manage (Gestisci) \> Security (Sicurezza)**.</span><span class="sxs-lookup"><span data-stu-id="90834-172">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="90834-173">![Gestione](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Gestione")</span><span class="sxs-lookup"><span data-stu-id="90834-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="90834-174">Fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="90834-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="90834-175">![Impostazioni di sicurezza globale](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Impostazioni di sicurezza globale")</span><span class="sxs-lookup"><span data-stu-id="90834-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="90834-176">Dall'elenco **Select a configuration or create a new one** (Selezionare o creare una configurazione) selezionare **Azure AD**, quindi fare clic su **Configure** (Configura).</span><span class="sxs-lookup"><span data-stu-id="90834-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="90834-177">![Configurare SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configurare SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="90834-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="90834-178">Nella finestra di dialogo **Configura SAML 2.0** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="90834-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="90834-179">![Configurare SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configurare SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="90834-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="90834-180">a.</span><span class="sxs-lookup"><span data-stu-id="90834-180">a.</span></span> <span data-ttu-id="90834-181">Nella casella di testo **Configuration Name** (Nome configurazione) digitare **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="90834-181">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="90834-182">b.</span><span class="sxs-lookup"><span data-stu-id="90834-182">b.</span></span> <span data-ttu-id="90834-183">Selezionare **Debug Mode**.</span><span class="sxs-lookup"><span data-stu-id="90834-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="90834-184">c.</span><span class="sxs-lookup"><span data-stu-id="90834-184">c.</span></span> <span data-ttu-id="90834-185">Nella casella di testo **Issuer** (Autorità emittente) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="90834-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="90834-186">d.</span><span class="sxs-lookup"><span data-stu-id="90834-186">d.</span></span> <span data-ttu-id="90834-187">Nella casella di testo **Authn Request URL** (URL richiesta di autenticazione) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="90834-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="90834-188">e.</span><span class="sxs-lookup"><span data-stu-id="90834-188">e.</span></span> <span data-ttu-id="90834-189">Aprire il certificato con codifica Base 64 nel Blocco note, copiarne il contenuto negli Appunti e incollare l’intero certificato nella casella di testo **Certificate X.509** .</span><span class="sxs-lookup"><span data-stu-id="90834-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="90834-190">f.</span><span class="sxs-lookup"><span data-stu-id="90834-190">f.</span></span> <span data-ttu-id="90834-191">Per **Email Attribute** (Attributo e-mail), selezionare **Use SAML subject** (Usa oggetto SAML).</span><span class="sxs-lookup"><span data-stu-id="90834-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="90834-192">g.</span><span class="sxs-lookup"><span data-stu-id="90834-192">g.</span></span> <span data-ttu-id="90834-193">Selezionare **SP initiated Login Configuration**.</span><span class="sxs-lookup"><span data-stu-id="90834-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="90834-194">h.</span><span class="sxs-lookup"><span data-stu-id="90834-194">h.</span></span> <span data-ttu-id="90834-195">Nella casella di testo **Login Path** (Percorso di accesso) digitare **Azure** e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90834-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="90834-196">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="90834-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="90834-197">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="90834-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="90834-198">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90834-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90834-199">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90834-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="90834-200">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="90834-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="90834-202">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="90834-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="90834-203">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="90834-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90834-205">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="90834-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90834-207">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="90834-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90834-209">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="90834-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90834-211">a.</span><span class="sxs-lookup"><span data-stu-id="90834-211">a.</span></span> <span data-ttu-id="90834-212">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90834-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90834-213">b.</span><span class="sxs-lookup"><span data-stu-id="90834-213">b.</span></span> <span data-ttu-id="90834-214">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90834-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90834-215">c.</span><span class="sxs-lookup"><span data-stu-id="90834-215">c.</span></span> <span data-ttu-id="90834-216">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="90834-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="90834-217">d.</span><span class="sxs-lookup"><span data-stu-id="90834-217">d.</span></span> <span data-ttu-id="90834-218">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="90834-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="90834-219">Creazione di un utente di test di SumoLogic</span><span class="sxs-lookup"><span data-stu-id="90834-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="90834-220">Per consentire agli utenti di Azure AD di accedere a SumoLogic, è necessario effettuarne il provisioning in SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="90834-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="90834-221">Nel caso di SumoLogic, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="90834-221">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="90834-222">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="90834-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="90834-223">Accedere al tenant **SumoLogic** .</span><span class="sxs-lookup"><span data-stu-id="90834-223">Log in to your **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="90834-224">Passare a **Manage (Gestisci) \> Users (Utenti)**.</span><span class="sxs-lookup"><span data-stu-id="90834-224">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="90834-225">![Utenti](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="90834-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="90834-226">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="90834-226">Click **Add**.</span></span>
   
    <span data-ttu-id="90834-227">![Utenti](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="90834-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="90834-228">Nella finestra di dialogo **New User** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="90834-228">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="90834-229">![Nuovo utente](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="90834-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="90834-230">a.</span><span class="sxs-lookup"><span data-stu-id="90834-230">a.</span></span> <span data-ttu-id="90834-231">Digitare le informazioni correlate dell'account Azure AD di cui si vuole effettuare il provisioning nelle caselle di testo **First Name** (Nome), **Last Name** (Cognome) e **Email** (Posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="90834-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="90834-232">b.</span><span class="sxs-lookup"><span data-stu-id="90834-232">b.</span></span> <span data-ttu-id="90834-233">Selezionare un ruolo.</span><span class="sxs-lookup"><span data-stu-id="90834-233">Select a role.</span></span>
  
    <span data-ttu-id="90834-234">c.</span><span class="sxs-lookup"><span data-stu-id="90834-234">c.</span></span> <span data-ttu-id="90834-235">Per **Status** (Stato) selezionare **Active** (Attivo).</span><span class="sxs-lookup"><span data-stu-id="90834-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="90834-236">d.</span><span class="sxs-lookup"><span data-stu-id="90834-236">d.</span></span> <span data-ttu-id="90834-237">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="90834-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="90834-238">È possibile usare qualsiasi altro strumento di creazione di account utente SumoLogic o qualsiasi API fornita da SumoLogic per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90834-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="90834-239">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90834-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="90834-240">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="90834-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span></span>

![Assegna utente][200] 

<span data-ttu-id="90834-242">**Per assegnare Britta Simon a SumoLogic, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="90834-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="90834-243">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="90834-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="90834-245">Nell'elenco delle applicazioni selezionare **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="90834-245">In the applications list, select **SumoLogic**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="90834-247">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="90834-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="90834-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="90834-249">Click **Add** button.</span></span> <span data-ttu-id="90834-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="90834-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="90834-252">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="90834-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="90834-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="90834-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90834-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="90834-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90834-255">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="90834-255">Testing single sign-on</span></span>

<span data-ttu-id="90834-256">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="90834-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="90834-257">Quando si fa clic sul riquadro SumoLogic nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="90834-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90834-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="90834-258">Additional resources</span></span>

* [<span data-ttu-id="90834-259">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90834-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90834-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90834-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

