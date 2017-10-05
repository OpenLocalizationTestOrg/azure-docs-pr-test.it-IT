---
title: 'Esercitazione: Integrazione di Azure Active Directory con Optimizely | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Optimizely.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 4d6f6da6bace09fbd6ab105530a1162653675c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="b2dfa-103">Esercitazione: Integrazione di Azure Active Directory con Optimizely</span><span class="sxs-lookup"><span data-stu-id="b2dfa-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="b2dfa-104">Questa esercitazione descrive come integrare Optimizely con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b2dfa-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b2dfa-105">L'integrazione di Optimizely con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2dfa-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b2dfa-106">È possibile controllare in Azure AD chi può accedere a Optimizely</span><span class="sxs-lookup"><span data-stu-id="b2dfa-106">You can control in Azure AD who has access to Optimizely</span></span>
- <span data-ttu-id="b2dfa-107">È possibile abilitare gli utenti per l'accesso automatico a Optimizely (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2dfa-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b2dfa-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b2dfa-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b2dfa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2dfa-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b2dfa-110">Prerequisites</span></span>

<span data-ttu-id="b2dfa-111">Per configurare l'integrazione di Azure AD con Optimizely, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2dfa-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

- <span data-ttu-id="b2dfa-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b2dfa-113">Sottoscrizione di Optimizely abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b2dfa-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b2dfa-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b2dfa-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2dfa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b2dfa-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b2dfa-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b2dfa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b2dfa-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b2dfa-118">Scenario description</span></span>
<span data-ttu-id="b2dfa-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b2dfa-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2dfa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b2dfa-121">Aggiunta di Optimizely dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b2dfa-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="b2dfa-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2dfa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-the-gallery"></a><span data-ttu-id="b2dfa-123">Aggiunta di Optimizely dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b2dfa-123">Adding Optimizely from the gallery</span></span>
<span data-ttu-id="b2dfa-124">Per configurare l'integrazione di Optimizely in Azure AD, è necessario aggiungere Optimizely dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b2dfa-125">**Per aggiungere Optimizely dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b2dfa-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b2dfa-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b2dfa-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b2dfa-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b2dfa-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b2dfa-133">Nella casella di ricerca digitare **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-133">In the search box, type **Optimizely**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="b2dfa-135">Nel pannello dei risultati selezionare **Optimizely** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b2dfa-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2dfa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b2dfa-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Optimizely mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b2dfa-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b2dfa-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Optimizely che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="b2dfa-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Optimizely.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="b2dfa-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** in Optimizely.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="b2dfa-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Optimizely, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2dfa-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b2dfa-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b2dfa-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b2dfa-145">**[Creazione di un utente test di Optimizely](#creating-an-optimizely-test-user)**: per avere una controparte di Britta Simon in Optimizely collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b2dfa-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b2dfa-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b2dfa-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2dfa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b2dfa-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Optimizely.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="b2dfa-150">**Per configurare l'accesso Single Sign-On di Azure AD con Optimizely, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b2dfa-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="b2dfa-151">Nella pagina di integrazione dell'applicazione **Optimizely** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b2dfa-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="b2dfa-155">Nella sezione **URL e dominio Optimizely** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b2dfa-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="b2dfa-157">a.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-157">a.</span></span> <span data-ttu-id="b2dfa-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://app.optimizely.net/<instance name>`.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="b2dfa-159">b.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-159">b.</span></span> <span data-ttu-id="b2dfa-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente: `urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="b2dfa-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b2dfa-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b2dfa-161">These values are not the real.</span></span> <span data-ttu-id="b2dfa-162">è necessario aggiornarli con i valori reali di URL di accesso e Identificatore. La procedura è descritta più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="b2dfa-163">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="b2dfa-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b2dfa-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b2dfa-167">Nella sezione **Configurazione di Optimizely** fare clic su **Configura Optimizely** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-167">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b2dfa-168">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b2dfa-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="b2dfa-170">Per configurare l'accesso Single Sign-On sul lato **Optimizely** contattare l'account manager di Optimizely e trasmettere il **Certificato (Base64)** scaricato e il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML).</span><span class="sxs-lookup"><span data-stu-id="b2dfa-170">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="b2dfa-171">In risposta al messaggio di posta elettronica, Optimizely fornisce l'URL di accesso (SSO avviato da SP) e i valori di Identificatore (ID entità del provider di servizi).</span><span class="sxs-lookup"><span data-stu-id="b2dfa-171">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="b2dfa-172">a.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-172">a.</span></span> <span data-ttu-id="b2dfa-173">Copiare l'**URL SSO avviato da SP** specificato da Optimizely e incollarlo nella casella di testo **URL di accesso** nella sezione **URL e dominio Optimizely** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-173">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="b2dfa-174">b.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-174">b.</span></span> <span data-ttu-id="b2dfa-175">Copiare l'**ID entità del provider di servizi** specificato da Optimizely e incollarlo nella casella di testo **Identificatore** nella sezione **URL e dominio Optimizely** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-175">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="b2dfa-176">In una finestra del browser diversa accedere all'applicazione Optimizely.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-176">In a different browser window, sign-on to your Optimizely application.</span></span>

10. <span data-ttu-id="b2dfa-177">Fare clic sul nome del proprio account in alto a destra e quindi su **Account Settings**(Impostazioni account).</span><span class="sxs-lookup"><span data-stu-id="b2dfa-177">Click you account name in the top right corner and then **Account Settings**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="b2dfa-179">Nella scheda Account, selezionare la casella **Enable SSO** (Abilita SSO) nella sezione **Overview** (Panoramica) di Single Sign On.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-179">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="b2dfa-181">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="b2dfa-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="b2dfa-182">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b2dfa-183">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b2dfa-184">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b2dfa-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b2dfa-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2dfa-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="b2dfa-186">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b2dfa-188">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b2dfa-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b2dfa-189">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b2dfa-191">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b2dfa-193">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b2dfa-195">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b2dfa-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b2dfa-197">a.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-197">a.</span></span> <span data-ttu-id="b2dfa-198">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b2dfa-199">b.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-199">b.</span></span> <span data-ttu-id="b2dfa-200">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b2dfa-201">c.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-201">c.</span></span> <span data-ttu-id="b2dfa-202">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b2dfa-203">d.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-203">d.</span></span> <span data-ttu-id="b2dfa-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="b2dfa-205">Creazione di un utente test di Optimizely</span><span class="sxs-lookup"><span data-stu-id="b2dfa-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="b2dfa-206">In questa sezione viene creato un utente di nome Britta Simon in Optimizely.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="b2dfa-207">Nella home page selezionare la scheda **Collaborators** (Collaboratori).</span><span class="sxs-lookup"><span data-stu-id="b2dfa-207">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="b2dfa-208">Per aggiungere un nuovo collaboratore al progetto fare clic su **New Collaborator** (Nuovo collaboratore).</span><span class="sxs-lookup"><span data-stu-id="b2dfa-208">To add new collaborator to the project, click **New Collaborator**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="b2dfa-210">Immettere l'indirizzo di posta elettronica e assegnare un ruolo ai nuovi collaboratori.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-210">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="b2dfa-211">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-211">Click **Invite**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="b2dfa-213">L'utente riceve un invito tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="b2dfa-213">They receive an email invite.</span></span> <span data-ttu-id="b2dfa-214">e deve eseguire l'accesso a Optimizely usando l'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-214">Using the email address, they have to log in to Optimizely.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b2dfa-215">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2dfa-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b2dfa-216">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Optimizely.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b2dfa-218">**Per assegnare Britta Simon a Optimizely, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b2dfa-218">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="b2dfa-219">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b2dfa-221">Nell'elenco di applicazioni selezionare **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-221">In the applications list, select **Optimizely**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="b2dfa-223">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b2dfa-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-225">Click **Add** button.</span></span> <span data-ttu-id="b2dfa-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b2dfa-228">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b2dfa-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b2dfa-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b2dfa-231">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b2dfa-231">Testing single sign-on</span></span>

<span data-ttu-id="b2dfa-232">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b2dfa-233">Quando si fa clic sul riquadro Optimizely nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Optimizely.</span><span class="sxs-lookup"><span data-stu-id="b2dfa-233">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b2dfa-234">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b2dfa-234">Additional resources</span></span>

* [<span data-ttu-id="b2dfa-235">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2dfa-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b2dfa-236">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2dfa-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

