---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kintone | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Kintone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: e5e847c12cba3611ce7ea2c3e956dbd55b1e0cac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="d8196-103">Esercitazione: Integrazione di Azure Active Directory con Kintone</span><span class="sxs-lookup"><span data-stu-id="d8196-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="d8196-104">Questa esercitazione descrive come integrare Kintone con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8196-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8196-105">L'integrazione di Kintone con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8196-105">Integrating Kintone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d8196-106">È possibile controllare in Azure AD chi può accedere a Kintone</span><span class="sxs-lookup"><span data-stu-id="d8196-106">You can control in Azure AD who has access to Kintone</span></span>
- <span data-ttu-id="d8196-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a Kintone con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8196-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8196-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8196-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d8196-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8196-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8196-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d8196-110">Prerequisites</span></span>

<span data-ttu-id="d8196-111">Per configurare l'integrazione di Azure AD con Kintone sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8196-111">To configure Azure AD integration with Kintone, you need the following items:</span></span>

- <span data-ttu-id="d8196-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8196-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8196-113">Sottoscrizione di Kintone abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d8196-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8196-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d8196-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d8196-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8196-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8196-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d8196-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d8196-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8196-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8196-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d8196-118">Scenario description</span></span>
<span data-ttu-id="d8196-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d8196-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8196-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8196-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8196-121">Aggiunta di Kintone dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d8196-121">Adding Kintone from the gallery</span></span>
2. <span data-ttu-id="d8196-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8196-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-the-gallery"></a><span data-ttu-id="d8196-123">Aggiunta di Kintone dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d8196-123">Adding Kintone from the gallery</span></span>
<span data-ttu-id="d8196-124">Per configurare l'integrazione di Kintone in Azure AD è necessario aggiungere Kintone dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d8196-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d8196-125">**Per aggiungere Kintone dalla raccolta seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d8196-125">**To add Kintone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d8196-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d8196-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d8196-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d8196-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d8196-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d8196-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d8196-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8196-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d8196-133">Nella casella di ricerca digitare **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="d8196-133">In the search box, type **Kintone**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="d8196-135">Nel pannello dei risultati selezionare **Kintone** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8196-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8196-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8196-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8196-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kintone mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d8196-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8196-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Kintone corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8196-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span></span> <span data-ttu-id="d8196-140">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Kintone.</span><span class="sxs-lookup"><span data-stu-id="d8196-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span></span>

<span data-ttu-id="d8196-141">Per stabilire la relazione di collegamento, in Kintone assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="d8196-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d8196-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Kintone è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8196-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d8196-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d8196-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d8196-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8196-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8196-145">**[Creazione di un utente test di Kintone](#creating-a-kintone-test-user)**: per avere una controparte di Britta Simon in Kintone collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8196-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d8196-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8196-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8196-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d8196-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8196-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8196-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8196-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Kintone.</span><span class="sxs-lookup"><span data-stu-id="d8196-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="d8196-150">**Per configurare l'accesso Single Sign-On di Azure AD con Kintone, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d8196-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="d8196-151">Nella pagina di integrazione dell'applicazione **Kintone** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d8196-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d8196-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d8196-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="d8196-155">Nella sezione **URL e dominio Kintone** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d8196-155">On the **Kintone Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="d8196-157">a.</span><span class="sxs-lookup"><span data-stu-id="d8196-157">a.</span></span> <span data-ttu-id="d8196-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.kintone.com`.</span><span class="sxs-lookup"><span data-stu-id="d8196-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="d8196-159">b.</span><span class="sxs-lookup"><span data-stu-id="d8196-159">b.</span></span> <span data-ttu-id="d8196-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="d8196-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="d8196-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d8196-161">These values are not real.</span></span> <span data-ttu-id="d8196-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="d8196-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d8196-163">Per ottenere questi valori contattare il [team di supporto clienti di Kintone](https://www.kintone.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="d8196-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="d8196-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="d8196-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="d8196-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d8196-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d8196-168">Nella sezione **Configurazione di Kintone** fare clic su **Configura Kintone** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="d8196-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d8196-169">Copiare i valori **Sign-Out URL (URL di disconnessione) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="d8196-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="d8196-171">In un'altra finestra del Web browser accedere al sito aziendale di **Kintone** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d8196-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="d8196-172">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d8196-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="d8196-173">![Impostazioni](./media/active-directory-saas-kintone-tutorial/ic785879.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="d8196-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="d8196-174">Fare clic su **Amministrazione utenti e di sistema**.</span><span class="sxs-lookup"><span data-stu-id="d8196-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="d8196-175">![Amministrazione utenti e di sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Amministrazione utenti e di sistema")</span><span class="sxs-lookup"><span data-stu-id="d8196-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="d8196-176">In **Amministrazione di sistema \> Sicurezza** fare clic su **Accesso**.</span><span class="sxs-lookup"><span data-stu-id="d8196-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="d8196-177">![Account di accesso](./media/active-directory-saas-kintone-tutorial/ic785881.png "Account di accesso")</span><span class="sxs-lookup"><span data-stu-id="d8196-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="d8196-178">Fare clic su **Abilita autenticazione SAML**.</span><span class="sxs-lookup"><span data-stu-id="d8196-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="d8196-179">![Autenticazione SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="d8196-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="d8196-180">Nella sezione SAML Authentication seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d8196-180">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="d8196-181">![Autenticazione SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="d8196-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="d8196-182">a.</span><span class="sxs-lookup"><span data-stu-id="d8196-182">a.</span></span> <span data-ttu-id="d8196-183">Nella casella di testo **URL di accesso** incollare il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8196-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d8196-184">b.</span><span class="sxs-lookup"><span data-stu-id="d8196-184">b.</span></span> <span data-ttu-id="d8196-185">Nella casella di testo **URL disconnessione** incollare il valore di **Sign-Out URL** (URL di disconnessione) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8196-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="d8196-186">c.</span><span class="sxs-lookup"><span data-stu-id="d8196-186">c.</span></span> <span data-ttu-id="d8196-187">Per caricare il certificato scaricato, fare clic su **Browse** .</span><span class="sxs-lookup"><span data-stu-id="d8196-187">Click **Browse** to upload your downloaded certificate.</span></span>
    
    <span data-ttu-id="d8196-188">d.</span><span class="sxs-lookup"><span data-stu-id="d8196-188">d.</span></span> <span data-ttu-id="d8196-189">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d8196-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d8196-190">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d8196-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d8196-191">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d8196-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d8196-192">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8196-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8196-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8196-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8196-194">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8196-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d8196-196">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d8196-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d8196-197">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d8196-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8196-199">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d8196-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8196-201">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d8196-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8196-203">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d8196-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8196-205">a.</span><span class="sxs-lookup"><span data-stu-id="d8196-205">a.</span></span> <span data-ttu-id="d8196-206">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8196-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8196-207">b.</span><span class="sxs-lookup"><span data-stu-id="d8196-207">b.</span></span> <span data-ttu-id="d8196-208">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d8196-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8196-209">c.</span><span class="sxs-lookup"><span data-stu-id="d8196-209">c.</span></span> <span data-ttu-id="d8196-210">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d8196-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d8196-211">d.</span><span class="sxs-lookup"><span data-stu-id="d8196-211">d.</span></span> <span data-ttu-id="d8196-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d8196-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="d8196-213">Creazione di un utente test di Kintone</span><span class="sxs-lookup"><span data-stu-id="d8196-213">Creating a Kintone test user</span></span>

<span data-ttu-id="d8196-214">Per consentire agli utenti di Azure AD di accedere a Kintone, è necessario eseguire il provisioning degli utenti in Kintone.</span><span class="sxs-lookup"><span data-stu-id="d8196-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="d8196-215">Nel caso di Kintone, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d8196-215">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="d8196-216">Per eseguire il provisioning di un account utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d8196-216">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="d8196-217">Accedere al sito aziendale di **Kintone** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d8196-217">Log in to your **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="d8196-218">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d8196-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="d8196-219">![Impostazioni](./media/active-directory-saas-kintone-tutorial/ic785879.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="d8196-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="d8196-220">Fare clic su **Amministrazione utenti e di sistema**.</span><span class="sxs-lookup"><span data-stu-id="d8196-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="d8196-221">![Amministrazione utenti e di sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Amministrazione utenti e di sistema")</span><span class="sxs-lookup"><span data-stu-id="d8196-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="d8196-222">In **Amministrazione Utente** fare clic su **Reparti e Utenti**.</span><span class="sxs-lookup"><span data-stu-id="d8196-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="d8196-223">![Reparto e utenti](./media/active-directory-saas-kintone-tutorial/ic785888.png "Reparto e utenti")</span><span class="sxs-lookup"><span data-stu-id="d8196-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="d8196-224">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="d8196-224">Click **New User**.</span></span>
   
    <span data-ttu-id="d8196-225">![Nuovi utenti](./media/active-directory-saas-kintone-tutorial/ic785889.png "Nuovi utenti")</span><span class="sxs-lookup"><span data-stu-id="d8196-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="d8196-226">Nella sezione **Nuovo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d8196-226">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d8196-227">![Nuovi utenti](./media/active-directory-saas-kintone-tutorial/ic785890.png "Nuovi utenti")</span><span class="sxs-lookup"><span data-stu-id="d8196-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="d8196-228">a.</span><span class="sxs-lookup"><span data-stu-id="d8196-228">a.</span></span> <span data-ttu-id="d8196-229">Nelle caselle di testo **Nome visualizzato**, **Nome di accesso**, **Nuova password**, **Conferma password** e **Indirizzo di posta elettronica** digitare i valori richiesti e gli altri dettagli di un account AAD valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="d8196-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span></span>
 
    <span data-ttu-id="d8196-230">b.</span><span class="sxs-lookup"><span data-stu-id="d8196-230">b.</span></span> <span data-ttu-id="d8196-231">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d8196-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d8196-232">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Kintone per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="d8196-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d8196-233">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8196-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d8196-234">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Kintone.</span><span class="sxs-lookup"><span data-stu-id="d8196-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d8196-236">**Per assegnare Britta Simon a Kintone, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d8196-236">**To assign Britta Simon to Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="d8196-237">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d8196-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d8196-239">Nell'elenco delle applicazioni selezionare **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="d8196-239">In the applications list, select **Kintone**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="d8196-241">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d8196-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d8196-243">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d8196-243">Click **Add** button.</span></span> <span data-ttu-id="d8196-244">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d8196-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d8196-246">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d8196-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d8196-247">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d8196-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8196-248">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d8196-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d8196-249">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d8196-249">Testing single sign-on</span></span>

<span data-ttu-id="d8196-250">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d8196-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d8196-251">Quando si fa clic sul riquadro Kintone nel pannello di accesso si accede automaticamente all'applicazione Kintone.</span><span class="sxs-lookup"><span data-stu-id="d8196-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8196-252">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d8196-252">Additional resources</span></span>

* [<span data-ttu-id="d8196-253">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8196-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8196-254">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8196-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

