---
title: 'Esercitazione: Integrazione di Azure Active Directory con Proofpoint on Demand | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Proofpoint on Demand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="ffbcb-103">Esercitazione: Integrazione di Azure Active Directory con Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="ffbcb-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="ffbcb-104">Questa esercitazione descrive come integrare Proofpoint on Demand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ffbcb-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ffbcb-105">L'integrazione di Proofpoint on Demand con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ffbcb-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ffbcb-106">È possibile controllare in Azure AD chi può accedere a Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="ffbcb-106">You can control in Azure AD who has access to Proofpoint on Demand</span></span>
- <span data-ttu-id="ffbcb-107">È possibile abilitare gli utenti per l'accesso automatico a Proofpoint on Demand (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="ffbcb-107">You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ffbcb-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ffbcb-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ffbcb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffbcb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ffbcb-110">Prerequisites</span></span>

<span data-ttu-id="ffbcb-111">Per configurare l'integrazione di Azure AD con Proofpoint on Demand, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ffbcb-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

- <span data-ttu-id="ffbcb-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ffbcb-113">Sottoscrizione di Proofpoint on Demand abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ffbcb-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ffbcb-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ffbcb-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ffbcb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ffbcb-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ffbcb-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ffbcb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ffbcb-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ffbcb-118">Scenario description</span></span>
<span data-ttu-id="ffbcb-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ffbcb-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ffbcb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ffbcb-121">Aggiunta di Proofpoint on Demand dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ffbcb-121">Adding Proofpoint on Demand from the gallery</span></span>
2. <span data-ttu-id="ffbcb-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbcb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="ffbcb-123">Aggiunta di Proofpoint on Demand dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ffbcb-123">Adding Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="ffbcb-124">Per configurare l'integrazione di Proofpoint on Demand in Azure AD, è necessario aggiungere Proofpoint on Demand dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-124">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ffbcb-125">**Per aggiungere Proofpoint on Demand dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ffbcb-125">**To add Proofpoint on Demand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ffbcb-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ffbcb-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ffbcb-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ffbcb-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ffbcb-133">Nella casella di ricerca digitare **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-133">In the search box, type **Proofpoint on Demand**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="ffbcb-135">Nel pannello dei risultati selezionare **Proofpoint on Demand** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-135">In the results panel, select **Proofpoint on Demand**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ffbcb-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbcb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ffbcb-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Proofpoint on Demand usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ffbcb-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ffbcb-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Proofpoint on Demand che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="ffbcb-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-140">In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.</span></span>

<span data-ttu-id="ffbcb-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="ffbcb-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Proofpoint on Demand, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="ffbcb-142">To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ffbcb-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ffbcb-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ffbcb-145">**[Creazione di un utente di test di Proofpoint on Demand](#creating-a-proofpoint-on-demand-test-user)**: per avere una controparte di Britta Simon in Proofpoint on Demand collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ffbcb-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ffbcb-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ffbcb-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbcb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ffbcb-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="ffbcb-150">**Per configurare l'accesso Single Sign-On di Azure AD con Proofpoint on Demand, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ffbcb-150">**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="ffbcb-151">Nella pagina di integrazione dell'applicazione **Proofpoint on Demand** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-151">In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ffbcb-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
  
    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="ffbcb-155">Nella sezione **URL e dominio Proofpoint on Demand** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ffbcb-155">On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="ffbcb-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="ffbcb-157">a.In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="ffbcb-158">b.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-158">b.</span></span> <span data-ttu-id="ffbcb-159">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="ffbcb-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="ffbcb-160">c.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-160">c.</span></span>  <span data-ttu-id="ffbcb-161">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="ffbcb-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ffbcb-162">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ffbcb-162">These values are not the real.</span></span> <span data-ttu-id="ffbcb-163">è necessario aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-163">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="ffbcb-164">Per ottenere questi valori, contattare il [team di supporto di Proofpoint on Demand](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="ffbcb-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.</span></span> 

4. <span data-ttu-id="ffbcb-165">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="ffbcb-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ffbcb-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ffbcb-169">Nella sezione **Configurazione di Proofpoint on Demand** fare clic su **Configura Proofpoint on Demand** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-169">On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ffbcb-170">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-170">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="ffbcb-172">Per configurare l'accesso Single Sign-On sul lato **Proofpoint on Demand**, è necessario inviare il file **Certificato (Base 64)** scaricato, l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** al [team di supporto di Proofpoint on Demand](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="ffbcb-172">To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="ffbcb-173">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ffbcb-174">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ffbcb-175">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ffbcb-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ffbcb-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbcb-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="ffbcb-177">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ffbcb-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ffbcb-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ffbcb-180">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ffbcb-182">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ffbcb-182">These values are not the real.</span></span> <span data-ttu-id="ffbcb-183">è necessario aggiornarli con quelli effettivi.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-183">Update these values with the actual</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ffbcb-185">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ffbcb-187">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ffbcb-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ffbcb-189">a.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-189">a.</span></span> <span data-ttu-id="ffbcb-190">Nella casella di testo **Name** (Nome) digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-190">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="ffbcb-191">b.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-191">b.</span></span> <span data-ttu-id="ffbcb-192">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-192">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="ffbcb-193">c.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-193">c.</span></span> <span data-ttu-id="ffbcb-194">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ffbcb-195">d.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-195">d.</span></span> <span data-ttu-id="ffbcb-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="ffbcb-197">Creazione di un utente di test di Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="ffbcb-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="ffbcb-198">In questa sezione viene creato un utente di nome Britta Simon in Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="ffbcb-199">Collaborare con il [team di supporto di Proofpoint on Demand](https://www.proofpoint.com/us/support-services), per aggiungere gli utenti alla piattaforma Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ffbcb-200">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffbcb-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ffbcb-201">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ffbcb-203">**Per assegnare Britta Simon a Proofpoint on Demand, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ffbcb-203">**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="ffbcb-204">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ffbcb-206">Nell'elenco delle applicazioni selezionare **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-206">In the applications list, select **Proofpoint on Demand**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="ffbcb-208">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ffbcb-210">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-210">Click **Add** button.</span></span> <span data-ttu-id="ffbcb-211">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ffbcb-213">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ffbcb-214">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ffbcb-215">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ffbcb-216">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ffbcb-216">Testing single sign-on</span></span>

<span data-ttu-id="ffbcb-217">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ffbcb-218">Quando si fa clic sul riquadro **Proofpoint on Demand** nel pannello in accesso, verrà eseguito automaticamente l'accesso all'applicazione Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="ffbcb-218">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>
<span data-ttu-id="ffbcb-219">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ffbcb-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="ffbcb-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ffbcb-220">Additional resources</span></span>

* [<span data-ttu-id="ffbcb-221">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffbcb-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ffbcb-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffbcb-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

