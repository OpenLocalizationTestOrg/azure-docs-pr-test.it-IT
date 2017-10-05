---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Business Object Cloud | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SAP Business Object Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: 6d517c5e302ac36e5bba2053998c75f8f4d42683
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="39db8-103">Esercitazione: Integrazione di Azure Active Directory con SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="39db8-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="39db8-104">Questa esercitazione descrive come integrare SAP Business Object Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39db8-104">In this tutorial, you learn how to integrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39db8-105">L'integrazione di SAP Business Object Cloud con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="39db8-105">You get the following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="39db8-106">In Azure AD è possibile controllare chi può accedere a SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="39db8-106">In Azure AD, you can control who has access to SAP Business Object Cloud.</span></span>
- <span data-ttu-id="39db8-107">È possibile connettere automaticamente gli utenti a SAP Business Object Cloud usando Single Sign-On e l'account Azure AD di un utente.</span><span class="sxs-lookup"><span data-stu-id="39db8-107">You can automatically sign in your users to SAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="39db8-108">È possibile gestire gli account da una posizione centrale, il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="39db8-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="39db8-109">Per altre informazioni sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39db8-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39db8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="39db8-110">Prerequisites</span></span>

<span data-ttu-id="39db8-111">Per configurare l'integrazione di Azure AD con SAP Business Object Cloud, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="39db8-111">To set up Azure AD integration with SAP Business Object Cloud, you need the following items:</span></span>

- <span data-ttu-id="39db8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39db8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39db8-113">Sottoscrizione di SAP Business Object Cloud, con l'accesso Single Sign-On attivato</span><span class="sxs-lookup"><span data-stu-id="39db8-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="39db8-114">Se si testano i passaggi di questa esercitazione, è consigliabile non testarli in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="39db8-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="39db8-115">Raccomandazioni per il test dei passaggi di questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="39db8-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="39db8-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="39db8-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="39db8-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39db8-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39db8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="39db8-118">Scenario description</span></span>
<span data-ttu-id="39db8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="39db8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="39db8-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="39db8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39db8-121">Aggiungere SAP Business Object Cloud dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="39db8-121">Add SAP Business Object Cloud from the gallery.</span></span>
2. <span data-ttu-id="39db8-122">Configurare e testare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39db8-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-the-gallery"></a><span data-ttu-id="39db8-123">Aggiungere SAP Business Object Cloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="39db8-123">Add SAP Business Object Cloud from the gallery</span></span>
<span data-ttu-id="39db8-124">Per configurare l'integrazione di SAP Business Object Cloud con Azure AD, nella raccolta aggiungere SAP Business Object Cloud al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="39db8-124">To set up the integration of SAP Business Object Cloud with Azure AD, in the gallery, add SAP Business Object Cloud to your list of managed SaaS apps.</span></span>

<span data-ttu-id="39db8-125">Per aggiungere SAP Business Object Cloud dalla raccolta:</span><span class="sxs-lookup"><span data-stu-id="39db8-125">To add SAP Business Object Cloud from the gallery:</span></span>

1. <span data-ttu-id="39db8-126">Nel [portale di Azure](https://portal.azure.com) fare clic su **Azure Active Directory** nel menu sinistro.</span><span class="sxs-lookup"><span data-stu-id="39db8-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="39db8-128">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="39db8-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Pagina Applicazioni aziendali][2]
    
3. <span data-ttu-id="39db8-130">Per aggiungere una nuova applicazione, selezionare **Nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="39db8-130">To add a new application, select **New application**.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="39db8-132">Nella casella di ricerca immettere **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="39db8-132">In the search box, enter **SAP Business Object Cloud**.</span></span>

    ![Casella di ricerca](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="39db8-134">Nel pannello dei risultati selezionare **SAP Business Object Cloud** e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="39db8-134">In the results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business Object Cloud nell'elenco risultati](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="39db8-136">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39db8-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="39db8-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Business Object Cloud con un utente di test di nome *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="39db8-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="39db8-138">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente di Azure AD in SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="39db8-138">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="39db8-139">Deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="39db8-139">A link relationship between an Azure AD user and the related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="39db8-140">Per stabilire la relazione di collegamento, in SAP Business Object Cloud per **Username** (Nome utente) assegnare il valore del **nome utente** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39db8-140">To establish the link relationship, in SAP Business Object Cloud, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="39db8-141">Per configurare e testare l'accesso Single Sign-On di Azure AD con SAP Business Object Cloud, completare le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="39db8-141">To configure and test Azure AD single sign-on with SAP Business Object Cloud, complete the following tasks:</span></span>

1. <span data-ttu-id="39db8-142">[Configurare l'accesso Single Sign-On di Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="39db8-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="39db8-143">Configura un utente per l'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="39db8-143">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="39db8-144">[Creare un utente test di Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="39db8-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="39db8-145">Testa l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39db8-145">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="39db8-146">[Creare un utente di test di SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="39db8-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="39db8-147">Crea una controparte di Britta Simon in SAP Business Object Cloud collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39db8-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="39db8-148">[Assegnare l'utente di test di Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="39db8-148">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="39db8-149">Configura Britta Simon per usare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39db8-149">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39db8-150">[Testare l'accesso Single Sign-On](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="39db8-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="39db8-151">Verifica se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="39db8-151">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="39db8-152">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39db8-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="39db8-153">In questa sezione si attiva l'accesso Single Sign-On di Azure AD nel portale di Azure,</span><span class="sxs-lookup"><span data-stu-id="39db8-153">In this section, you turn on Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="39db8-154">quindi si configura Single Sign-On nell'applicazione SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="39db8-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="39db8-155">Per configurare Single Sign-On di Azure AD con SAP Business Object Cloud:</span><span class="sxs-lookup"><span data-stu-id="39db8-155">To set up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="39db8-156">Nella pagina di integrazione dell'applicazione **SAP Business Object Cloud** del portale di Azure selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="39db8-156">In the Azure portal, on the **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Selezionare Single Sign-On][4]

2. <span data-ttu-id="39db8-158">Nella pagina **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML**.</span><span class="sxs-lookup"><span data-stu-id="39db8-158">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Selezionare Accesso basato su SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="39db8-160">In **SAP Business Object Cloud Domain and URLs** (URL e dominio SAP Business Object Cloud) completare questa procedura:</span><span class="sxs-lookup"><span data-stu-id="39db8-160">Under **SAP Business Object Cloud Domain and URLs**, complete the following steps:</span></span>

    1. <span data-ttu-id="39db8-161">Nella casella **URL di accesso** immettere un URL con il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="39db8-161">In the **Sign-on URL** box, enter a URL that has the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="39db8-162">Nella casella **Identificatore** immettere un URL con il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="39db8-162">In the **Identifier** box, enter a URL that has the following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URL della pagina SAP Business Object Cloud Domain and URLs (URL e dominio SAP Business Object Cloud)](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="39db8-164">I valori in questi URL sono forniti solo a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="39db8-164">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="39db8-165">Aggiornare i valori con l'URL di accesso e l'URL dell'identificatore effettivi.</span><span class="sxs-lookup"><span data-stu-id="39db8-165">Update the values with the actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="39db8-166">Per ottenere l'URL di accesso, contattare il [team di supporto clienti di SAP Business Object Cloud](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="39db8-166">To get the sign-on URL, contact the [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="39db8-167">Per ottenere l'URL dell'identificatore, scaricare i metadati di SAP Business Object Cloud dalla console di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="39db8-167">You can get the identifier URL by downloading the SAP Business Object Cloud metadata from the admin console.</span></span> <span data-ttu-id="39db8-168">Questo concetto verrà spiegato più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="39db8-168">This is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="39db8-169">In **Certificato di firma SAML** selezionare **XML metadati**,</span><span class="sxs-lookup"><span data-stu-id="39db8-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="39db8-170">quindi salvare il file di metadati sul computer.</span><span class="sxs-lookup"><span data-stu-id="39db8-170">Then, save the metadata file on your computer.</span></span>

    ![Selezionare XML metadati](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="39db8-172">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="39db8-172">Select **Save**.</span></span>

    ![Selezionare Salva](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="39db8-174">In un'altra finestra del Web browser accedere al sito aziendale di SAP Business Object Cloud come amministratore.</span><span class="sxs-lookup"><span data-stu-id="39db8-174">In a different web browser window, sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="39db8-175">Selezionare **Menu** > **Sistema** > **Amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="39db8-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Selezionare Menu, quindi Sistema e infine Amministrazione](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="39db8-177">Selezionare l'icona **Modifica** (penna) nella scheda **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="39db8-177">On the **Security** tab, select the **Edit** (pen) icon.</span></span>
    
    ![Selezionare l'icona Modifica nella scheda Sicurezza](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="39db8-179">Per **Metodo di autenticazione** selezionare **SAML Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="39db8-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Selezionare SAML Single Sign-On per il metodo di autenticazione](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="39db8-181">Per scaricare i metadati del provider di servizi (passaggio 1), selezionare **Download**.</span><span class="sxs-lookup"><span data-stu-id="39db8-181">To download the service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="39db8-182">Nel file di metadati trovare e copiare il valore **entityID**.</span><span class="sxs-lookup"><span data-stu-id="39db8-182">In the metadata file, find and copy the **entityID** value.</span></span> <span data-ttu-id="39db8-183">Nel portale di Azure, in **SAP Business Object Cloud Domain and URLs** (URL e dominio SAP Business Object Cloud), incollare il valore nella casella **Identificatore**.</span><span class="sxs-lookup"><span data-stu-id="39db8-183">In the Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste the value in the **Identifier** box.</span></span>

    ![Copiare e incollare il valore di entityID](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="39db8-185">Per caricare i metadati del provider di servizi (passaggio 2) nel file scaricato nel portale di Azure, in **Upload Identity Provider metadata** (Caricare i metadati del provider di identità) selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="39db8-185">To upload the service provider metadata (Step 2) in the file that you downloaded from the Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![In Upload Identity Provider metadata (Caricare i metadati del provider di identità) selezionare Carica](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="39db8-187">Nell'elenco **Attributo utente** selezionare l'attributo utente (passaggio 3) da usare per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="39db8-187">In the **User Attribute** list, select the user attribute (Step 3) that you want to use for your implementation.</span></span> <span data-ttu-id="39db8-188">Questo attributo utente esegue il mapping al provider di identità.</span><span class="sxs-lookup"><span data-stu-id="39db8-188">This user attribute maps to the identity provider.</span></span> <span data-ttu-id="39db8-189">Per immettere un attributo personalizzato nella pagina dell'utente, usare l'opzione **Custom SAML Mapping** (Mapping SAML personalizzato).</span><span class="sxs-lookup"><span data-stu-id="39db8-189">To enter a custom attribute on the user's page, use the **Custom SAML Mapping** option.</span></span> <span data-ttu-id="39db8-190">oppure selezionare **Posta elettronica** o **ID UTENTE** come attributo utente.</span><span class="sxs-lookup"><span data-stu-id="39db8-190">Or, you can select either **Email** or **USER ID** as the user attribute.</span></span> <span data-ttu-id="39db8-191">Nell'esempio è stato selezionato **Posta elettronica** perché è stato eseguito il mapping dell'attestazione dell'ID utente con l'attributo **userprincipalname** nella sezione **Attributi utente** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="39db8-191">In our example, we selected **Email** because we mapped the user identifier claim with the **userprincipalname** attribute in the **User Attributes** section in the Azure portal.</span></span> <span data-ttu-id="39db8-192">Si ottiene così un indirizzo di posta elettronica dell'utente univoco, che viene inviato all'applicazione SAP Business Object Cloud in ogni risposta SAML con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="39db8-192">This provides a unique user email, which is sent to the SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Selezionare Attributo utente](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="39db8-194">Per verificare l'account con il provider di identità (passaggio 4), nella casella **Login Credential (Email)** (Credenziale di accesso - Posta elettronica) immettere l'indirizzo di posta elettronica dell'utente.</span><span class="sxs-lookup"><span data-stu-id="39db8-194">To verify the account with the identity provider (Step 4), in the **Login Credential (Email)** box, enter the user's email address.</span></span> <span data-ttu-id="39db8-195">Selezionare quindi **Verifica account**.</span><span class="sxs-lookup"><span data-stu-id="39db8-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="39db8-196">Il sistema aggiunge le credenziali di accesso all'account utente.</span><span class="sxs-lookup"><span data-stu-id="39db8-196">The system adds sign-in credentials to the user account.</span></span>

    ![Immettere l'indirizzo di posta elettronica e selezionare Verifica account](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="39db8-198">Selezionare l'icona **Salva**.</span><span class="sxs-lookup"><span data-stu-id="39db8-198">Select the **Save** icon.</span></span>

    ![Icona Salva](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="39db8-200">Un riepilogo delle istruzioni è disponibile nel [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="39db8-200">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="39db8-201">Dopo avere aggiunto l'app selezionando **Active Directory** > **Applicazioni aziendali**, selezionare la scheda **Single Sign-On**. È possibile accedere alla documentazione incorporata nella sezione **Configurazione** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="39db8-201">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="39db8-202">Per altre informazioni, vedere la [documentazione incorporata su Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="39db8-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="39db8-203">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39db8-203">Create an Azure AD test user</span></span>
<span data-ttu-id="39db8-204">In questa sezione viene creato un utente di test chiamato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="39db8-204">In this section, you create a test user named Britta Simon in the Azure portal.</span></span>

<span data-ttu-id="39db8-205">Per creare un utente di test in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="39db8-205">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="39db8-206">Nel portale di Azure fare clic su **Azure Active Directory** nel menu sinistro.</span><span class="sxs-lookup"><span data-stu-id="39db8-206">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39db8-208">Selezionare **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="39db8-208">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39db8-210">Per aprire la finestra di dialogo **Utente**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="39db8-210">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39db8-212">Nella finestra di dialogo **Utente** completare questa procedura:</span><span class="sxs-lookup"><span data-stu-id="39db8-212">In the **User** dialog box, complete the following steps:</span></span>
 
    1. <span data-ttu-id="39db8-213">Nella casella **Nome** immettere **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39db8-213">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="39db8-214">Nella casella **Nome utente** immettere l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39db8-214">In the **User name** box, enter the email address of the user Britta Simon.</span></span>

    3. <span data-ttu-id="39db8-215">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="39db8-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="39db8-216">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="39db8-216">Select **Create**.</span></span>

        ![Finestra di dialogo Utente](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Creare un utente di Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="39db8-219">Creare un utente di test di SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="39db8-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="39db8-220">È necessario effettuare il provisioning degli utenti di Azure AD in SAP Business Object Cloud perché possano accedere a SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="39db8-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in to SAP Business Object Cloud.</span></span> <span data-ttu-id="39db8-221">In SAP Business Object Cloud il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="39db8-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="39db8-222">Per effettuare il provisioning di un account utente:</span><span class="sxs-lookup"><span data-stu-id="39db8-222">To provision a user account:</span></span>

1. <span data-ttu-id="39db8-223">Accedere al sito aziendale di SAP Business Object Cloud come amministratore.</span><span class="sxs-lookup"><span data-stu-id="39db8-223">Sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="39db8-224">Selezionare **Menu** > **Security** (Sicurezza)  > **Users** (Utenti).</span><span class="sxs-lookup"><span data-stu-id="39db8-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="39db8-226">Nella pagina **Users** (Utenti) selezionare **+** per aggiungere i dettagli di un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="39db8-226">On the **Users** page, to add new user details, select **+**.</span></span> 

    ![Pagina Aggiungi utenti (Aggiungi utenti)](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="39db8-228">Completare quindi i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="39db8-228">Then, complete the following steps:</span></span>

    1. <span data-ttu-id="39db8-229">Nella casella **USER ID** (ID UTENTE) immettere l'ID dell'utente, ad esempio, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="39db8-229">In the **USER ID** box, enter the user ID of the user, like **Britta**.</span></span>

    2. <span data-ttu-id="39db8-230">Nella casella **FIRST NAME** (NOME) immettere il nome dell'utente, ad esempio **Britta**.</span><span class="sxs-lookup"><span data-stu-id="39db8-230">In the **FIRST NAME** box, enter the first name of the user, like **Britta**.</span></span>

    3. <span data-ttu-id="39db8-231">Nella casella **LAST NAME** (COGNOME) immettere il cognome dell'utente, ad esempio **Simon**.</span><span class="sxs-lookup"><span data-stu-id="39db8-231">In the **LAST NAME** box, enter the last name of the user, like **Simon**.</span></span>

    4. <span data-ttu-id="39db8-232">Nella casella **NOME VISUALIZZATO** immettere nome e cognome dell'utente, ad esempio **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="39db8-232">In the **DISPLAY NAME** box, enter the full name of the user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="39db8-233">Nella casella **E-MAIL** (POSTA ELETTRONICA) immettere l'indirizzo di posta elettronica dell'utente, ad esempio **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="39db8-233">In the **E-MAIL** box, enter the email address of the user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="39db8-234">Nella pagina **Select Roles** (Selezione ruoli) selezionare il ruolo appropriato per l'utente e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="39db8-234">On the **Select Roles** page, select the appropriate role for the user, and then select **OK**.</span></span>

      ![Selezionare il ruolo](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="39db8-236">Selezionare l'icona **Salva**.</span><span class="sxs-lookup"><span data-stu-id="39db8-236">Select the **Save** icon.</span></span>    


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="39db8-237">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="39db8-237">Assign the Azure AD test user</span></span>

<span data-ttu-id="39db8-238">In questa sezione si consente all'utente Britta Simon di usare l'accesso Single Sign-On di Azure AD concedendo all'account utente l'accesso a SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="39db8-238">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to SAP Business Object Cloud.</span></span>

<span data-ttu-id="39db8-239">Per assegnare Britta Simon a SAP Business Object Cloud:</span><span class="sxs-lookup"><span data-stu-id="39db8-239">To assign Britta Simon to SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="39db8-240">Nel portale di Azure aprire la visualizzazione applicazioni e quindi passare alla visualizzazione directory.</span><span class="sxs-lookup"><span data-stu-id="39db8-240">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="39db8-241">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="39db8-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="39db8-243">Nell'elenco delle applicazioni selezionare **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="39db8-243">In the applications list, select **SAP Business Object Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="39db8-245">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="39db8-245">In the left menu, select **Users and groups**.</span></span>

    ![Selezionare Utenti e gruppi][202] 

4. <span data-ttu-id="39db8-247">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="39db8-247">Select **Add**.</span></span> <span data-ttu-id="39db8-248">Quindi nella pagina **Aggiungi assegnazione** selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="39db8-248">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![Pagina Aggiungi assegnazione][203]

5. <span data-ttu-id="39db8-250">Nella pagina **Utenti e gruppi** selezionare **Britta Simon** nell'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="39db8-250">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="39db8-251">Nella pagina **Utenti e gruppi** selezionare **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="39db8-251">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="39db8-252">Nella pagina **Aggiungi assegnazione** selezionare **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="39db8-252">On the **Add Assignment** page, select **Assign**.</span></span>

![Assegnare il ruolo utente][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="39db8-254">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="39db8-254">Test single sign-on</span></span>

<span data-ttu-id="39db8-255">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="39db8-255">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="39db8-256">Quando si seleziona il riquadro SAP Business Object Cloud nel pannello di accesso, si accederà automaticamente all'applicazione SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="39db8-256">When you select the SAP Business Object Cloud tile in the access panel, you should be automatically signed in to your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="39db8-257">Per altre informazioni sul pannello di accesso, vedere [Introduzione al pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39db8-257">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39db8-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="39db8-258">Additional resources</span></span>

* [<span data-ttu-id="39db8-259">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39db8-259">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39db8-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39db8-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

