---
title: 'Esercitazione: Integrazione di Azure Active Directory con Atlassian Cloud | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Atlassian Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="22f6b-103">Esercitazione: Integrazione di Azure Active Directory con Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="22f6b-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="22f6b-104">Questa esercitazione descrive come integrare Atlassian Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="22f6b-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22f6b-105">L'integrazione di Atlassian Cloud con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f6b-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="22f6b-106">È possibile controllare in Azure AD chi può accedere ad Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="22f6b-106">You can control in Azure AD who has access to Atlassian Cloud</span></span>
- <span data-ttu-id="22f6b-107">È possibile abilitare gli utenti per l'accesso automatico ad Atlassian Cloud (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f6b-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="22f6b-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22f6b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="22f6b-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="22f6b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22f6b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="22f6b-110">Prerequisites</span></span>

<span data-ttu-id="22f6b-111">Per configurare l'integrazione di Azure AD con Atlassian Cloud, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f6b-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="22f6b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22f6b-113">Sottoscrizione di Atlassian Cloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="22f6b-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="22f6b-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="22f6b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="22f6b-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f6b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22f6b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="22f6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="22f6b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22f6b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22f6b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="22f6b-118">Scenario description</span></span>
<span data-ttu-id="22f6b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="22f6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22f6b-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f6b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22f6b-121">Aggiunta di Atlassian Cloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="22f6b-121">Adding Atlassian Cloud from the gallery</span></span>
2. <span data-ttu-id="22f6b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="22f6b-123">Aggiunta di Atlassian Cloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="22f6b-123">Adding Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="22f6b-124">Per configurare l'integrazione di Atlassian Cloud in Azure AD, è necessario aggiungere Atlassian Cloud dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="22f6b-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="22f6b-125">**Per aggiungere Atlassian Cloud dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="22f6b-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="22f6b-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="22f6b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="22f6b-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="22f6b-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="22f6b-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="22f6b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="22f6b-133">Nella casella di ricerca digitare **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-133">In the search box, type **Atlassian Cloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="22f6b-135">Nel pannello dei risultati selezionare **Atlassian Cloud** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22f6b-135">In the results panel, select **Atlassian Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="22f6b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="22f6b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Atlassian Cloud con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="22f6b-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="22f6b-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Atlassian Cloud che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f6b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="22f6b-140">In altre parole deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="22f6b-140">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span></span>

<span data-ttu-id="22f6b-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="22f6b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="22f6b-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Atlassian Cloud, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="22f6b-142">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="22f6b-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="22f6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="22f6b-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22f6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22f6b-145">**[Creazione di un utente di test di Atlassian Cloud](#creating-an-atlassian-cloud-test-user)**: per avere una controparte di Britta Simon in Atlassian Cloud collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f6b-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="22f6b-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f6b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22f6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="22f6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="22f6b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="22f6b-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="22f6b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="22f6b-150">**Per configurare l'accesso Single Sign-On di Azure AD con Atlassian Cloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="22f6b-150">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="22f6b-151">Nella pagina di integrazione dell'applicazione **Atlassian Cloud** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-151">In the Azure portal, on the **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="22f6b-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="22f6b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="22f6b-155">Nella sezione **URL e dominio Atlassian Cloud**, se si vuole configurare l'applicazione in modalità avviata da **IDP**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="22f6b-155">On the **Atlassian Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="22f6b-157">a.</span><span class="sxs-lookup"><span data-stu-id="22f6b-157">a.</span></span> <span data-ttu-id="22f6b-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="22f6b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="22f6b-159">b.</span><span class="sxs-lookup"><span data-stu-id="22f6b-159">b.</span></span> <span data-ttu-id="22f6b-160">Nella casella di testo **URL di risposta** digitare un URL come indicato di seguito: `https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="22f6b-160">In the **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="22f6b-161">Se si vuole configurare l'applicazione in modalità avviata da **SP**, selezionare **Mostra impostazioni URL avanzate** e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="22f6b-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="22f6b-163">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="22f6b-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="22f6b-164">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="22f6b-164">These values are not real.</span></span> <span data-ttu-id="22f6b-165">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="22f6b-165">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="22f6b-166">È possibile ottenere i valori esatti dalla schermata di configurazione SAML di Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="22f6b-166">You can get the exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="22f6b-167">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="22f6b-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="22f6b-169">Nella sezione **Configurazione di Atlassian Cloud** fare clic su **Configura Atlassian Cloud** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-169">On the **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="22f6b-170">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="22f6b-170">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="22f6b-172">Per ottenere l'accesso Single Sign-On configurato per l'applicazione, accedere al portale di Atlassian usando i diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="22f6b-172">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span></span>

8. <span data-ttu-id="22f6b-173">Nella sezione Authentication (Autenticazione) a sinistra fare clic su **Domains** (Domini).</span><span class="sxs-lookup"><span data-stu-id="22f6b-173">In the Authentication section of the left navigation click **Domains**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="22f6b-175">a.</span><span class="sxs-lookup"><span data-stu-id="22f6b-175">a.</span></span> <span data-ttu-id="22f6b-176">Nella casella di testo digitare il nome di dominio e quindi fare clic su **Add domain** (Aggiungi dominio).</span><span class="sxs-lookup"><span data-stu-id="22f6b-176">In the textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="22f6b-178">b.</span><span class="sxs-lookup"><span data-stu-id="22f6b-178">b.</span></span> <span data-ttu-id="22f6b-179">Per verificare il dominio, fare clic su **Verify** (Verifica).</span><span class="sxs-lookup"><span data-stu-id="22f6b-179">To verify the domain, click **Verify**.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="22f6b-181">c.</span><span class="sxs-lookup"><span data-stu-id="22f6b-181">c.</span></span> <span data-ttu-id="22f6b-182">Scaricare il file HTML di verifica del dominio, caricarlo nella cartella radice del sito Web del dominio, quindi fare clic su **Verify domain** (Verifica dominio).</span><span class="sxs-lookup"><span data-stu-id="22f6b-182">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="22f6b-184">d.</span><span class="sxs-lookup"><span data-stu-id="22f6b-184">d.</span></span> <span data-ttu-id="22f6b-185">Dopo la verifica del dominio, il valore del campo **Status** (Stato) è **Verified** (Verificato).</span><span class="sxs-lookup"><span data-stu-id="22f6b-185">Once the domain is verified, the value of the **Status** field is **Verified**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="22f6b-187">Nella barra di spostamento a sinistra fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-187">In the left navigation bar, click **SAML**.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="22f6b-189">Creare una configurazione SAML e aggiungere la configurazione del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="22f6b-189">Create a SAML Configuration and add the Identity provider configuration.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="22f6b-191">a.</span><span class="sxs-lookup"><span data-stu-id="22f6b-191">a.</span></span> <span data-ttu-id="22f6b-192">Nella casella di testo **Identity provider Entity ID** (ID entità provider di identità) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22f6b-192">In the **Identity provider Entity ID** text box, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="22f6b-193">b.</span><span class="sxs-lookup"><span data-stu-id="22f6b-193">b.</span></span> <span data-ttu-id="22f6b-194">Nella casella di testo **Identity provider SSO URL** (URL SSO provider di identità) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22f6b-194">In the **Identity provider SSO URL** text box, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="22f6b-195">c.</span><span class="sxs-lookup"><span data-stu-id="22f6b-195">c.</span></span> <span data-ttu-id="22f6b-196">Aprire il certificato scaricato dal portale di Azure e copiare i valori senza le righe di inizio e di fine, quindi incollarli nella casella **Public X509 certificate** (Certificato X509 pubblico).</span><span class="sxs-lookup"><span data-stu-id="22f6b-196">Open the downloaded certificate from Azure portal and copy the values without the Begin and End lines and paste it in the **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="22f6b-197">d.</span><span class="sxs-lookup"><span data-stu-id="22f6b-197">d.</span></span> <span data-ttu-id="22f6b-198">Per salvare le impostazioni, fare clic su **Save Configuration** (Salva configurazione).</span><span class="sxs-lookup"><span data-stu-id="22f6b-198">Click **Save Configuration**  to Save the settings.</span></span>
     
11. <span data-ttu-id="22f6b-199">Aggiornare le impostazioni di Azure AD per assicurarsi di avere configurato l'URL corretto per l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="22f6b-199">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span></span>
  
    <span data-ttu-id="22f6b-200">a.</span><span class="sxs-lookup"><span data-stu-id="22f6b-200">a.</span></span> <span data-ttu-id="22f6b-201">Copiare l'**ID dell'identità SP** dalla schermata SAML e incollarlo in Azure AD come valore **Identificatore**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-201">Copy the **SP Identity ID** from the SAML screen and paste it in Azure AD as the **Identifier** value.</span></span>

    <span data-ttu-id="22f6b-202">b.</span><span class="sxs-lookup"><span data-stu-id="22f6b-202">b.</span></span> <span data-ttu-id="22f6b-203">L'URL di accesso corrisponde all'URL del tenant di Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="22f6b-203">Sign On URL is the tenant URL of your Atlassian Cloud.</span></span>   

     ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="22f6b-205">Nel portale di Azure fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-205">In the Azure portal, Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="22f6b-207">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="22f6b-207">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="22f6b-208">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="22f6b-208">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="22f6b-209">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="22f6b-209">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="22f6b-210">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f6b-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="22f6b-211">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="22f6b-211">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="22f6b-213">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="22f6b-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="22f6b-214">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="22f6b-214">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="22f6b-216">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="22f6b-216">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="22f6b-218">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-218">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="22f6b-220">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="22f6b-220">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="22f6b-222">a.</span><span class="sxs-lookup"><span data-stu-id="22f6b-222">a.</span></span> <span data-ttu-id="22f6b-223">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-223">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22f6b-224">b.</span><span class="sxs-lookup"><span data-stu-id="22f6b-224">b.</span></span> <span data-ttu-id="22f6b-225">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="22f6b-225">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="22f6b-226">c.</span><span class="sxs-lookup"><span data-stu-id="22f6b-226">c.</span></span> <span data-ttu-id="22f6b-227">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-227">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="22f6b-228">d.</span><span class="sxs-lookup"><span data-stu-id="22f6b-228">d.</span></span> <span data-ttu-id="22f6b-229">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="22f6b-230">Creazione di un utente di test di Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="22f6b-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="22f6b-231">Per consentire agli utenti di Azure AD di accedere ad Atlassian Cloud, è necessario effettuarne il provisioning in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="22f6b-231">To enable Azure AD users to log in to Atlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="22f6b-232">Nel caso di Atlassian Cloud il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="22f6b-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="22f6b-233">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="22f6b-233">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="22f6b-234">Nella sezione relativa all'amministrazione del sito fare clic sul pulsante **Users** (Utenti).</span><span class="sxs-lookup"><span data-stu-id="22f6b-234">In the Site administration section, click the **Users** button</span></span>

    ![Creare l'utente di Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="22f6b-236">Fare clic sul pulsante **Create User** (Crea utente) per creare un utente in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="22f6b-236">Click the **Create User** button to create a user in the Atlassian Cloud</span></span>

    ![Creare l'utente di Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="22f6b-238">Immettere **Email address** (Indirizzo di posta elettronica), **Username** (Nome utente) e **Full Name** (Nome completo) dell'utente e assegnare l'accesso all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="22f6b-238">Enter the user's **Email address**, **Username**, and **Full Name** and assign the application access.</span></span> 

    ![Creare l'utente di Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="22f6b-240">Fare clic sul pulsante **Create user** (Crea utente). L'invito tramite posta elettronica verrà inviato all'utente. Dopo l'accettazione dell'invito, l'utente sarà attivo nel sistema.</span><span class="sxs-lookup"><span data-stu-id="22f6b-240">Click **Create user** button, it will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span></span> 

>[!NOTE] 
><span data-ttu-id="22f6b-241">È anche possibile creare gli utenti in blocco facendo clic sul pulsante **Bulk Create** (Creazione in blocco) nella sezione Users (Utenti).</span><span class="sxs-lookup"><span data-stu-id="22f6b-241">You can also create the bulk users by clicking the **Bulk Create** button in the Users section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="22f6b-242">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="22f6b-242">Assigning the Azure AD test user</span></span>

<span data-ttu-id="22f6b-243">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="22f6b-243">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="22f6b-245">**Per assegnare Britta Simon ad Atlassian Cloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="22f6b-245">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="22f6b-246">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-246">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="22f6b-248">Nell'elenco di applicazioni selezionare **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-248">In the applications list, select **Atlassian Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="22f6b-250">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="22f6b-250">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="22f6b-252">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-252">Click **Add** button.</span></span> <span data-ttu-id="22f6b-253">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="22f6b-255">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="22f6b-255">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="22f6b-256">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22f6b-257">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="22f6b-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="22f6b-258">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="22f6b-258">Testing single sign-on</span></span>

<span data-ttu-id="22f6b-259">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="22f6b-259">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="22f6b-260">Quando si fa clic sul riquadro Atlassian Cloud nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="22f6b-260">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span></span> <span data-ttu-id="22f6b-261">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="22f6b-261">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="22f6b-262">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="22f6b-262">Additional resources</span></span>

* [<span data-ttu-id="22f6b-263">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22f6b-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22f6b-264">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22f6b-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

