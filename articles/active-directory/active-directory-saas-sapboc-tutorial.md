---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Business Object Cloud | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAP Business oggetto Cloud.
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
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="97177-103">Esercitazione: Integrazione di Azure Active Directory con SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="97177-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="97177-104">In questa esercitazione, è illustrato come toointegrate SAP Business oggetto Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97177-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97177-105">Si otterrà hello seguenti vantaggi quando si integra SAP Business oggetto Cloud con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="97177-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="97177-106">In Azure AD, è possibile controllare chi ha accesso tooSAP Cloud oggetto Business.</span><span class="sxs-lookup"><span data-stu-id="97177-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="97177-107">È possibile accedere automaticamente il tooSAP utenti Business oggetto Cloud con accesso single sign-on e un account utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97177-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="97177-108">È possibile gestire gli account in una posizione centrale, hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="97177-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="97177-109">toolearn ulteriori informazioni su software come un servizio (SaaS) integrazione dell'applicazione con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97177-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97177-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="97177-110">Prerequisites</span></span>

<span data-ttu-id="97177-111">tooset l'integrazione di Azure AD con SAP Business oggetto Cloud, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="97177-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="97177-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97177-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97177-113">Sottoscrizione di SAP Business Object Cloud, con l'accesso Single Sign-On attivato</span><span class="sxs-lookup"><span data-stu-id="97177-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="97177-114">Se si passi hello in questa esercitazione, si consiglia di non testare loro in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="97177-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="97177-115">Indicazioni per il test passaggi hello in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="97177-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="97177-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="97177-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="97177-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97177-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97177-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="97177-118">Scenario description</span></span>
<span data-ttu-id="97177-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="97177-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="97177-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="97177-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97177-121">Aggiungere SAP Business oggetto Cloud dalla raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="97177-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="97177-122">Configurare e testare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97177-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="97177-123">Aggiungere SAP Business oggetto Cloud dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="97177-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="97177-124">tooset l'integrazione di hello di SAP Business oggetto Cloud con Azure AD, nella raccolta di hello, aggiungere l'elenco tooyour SAP Business oggetto Cloud di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="97177-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="97177-125">tooadd SAP Business oggetto Cloud dalla raccolta hello:</span><span class="sxs-lookup"><span data-stu-id="97177-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="97177-126">In hello [portale di Azure](https://portal.azure.com)in hello menu a sinistra, selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="97177-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="97177-128">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="97177-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![pagina applicazioni di Enterprise Hello][2]
    
3. <span data-ttu-id="97177-130">Selezionare una nuova applicazione, tooadd **nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="97177-130">tooadd a new application, select **New application**.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="97177-132">Nella casella di ricerca hello, immettere **SAP Business oggetto Cloud**.</span><span class="sxs-lookup"><span data-stu-id="97177-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![casella di ricerca Hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="97177-134">Nel riquadro dei risultati hello, selezionare **SAP Business oggetto Cloud**, quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="97177-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business oggetto Cloud nell'elenco risultati hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="97177-136">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="97177-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="97177-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Business Object Cloud con un utente di test di nome *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="97177-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="97177-138">Per toowork di accesso singolo, Azure AD deve tooknow hello Azure controparte utente di Active Directory nel Cloud di oggetto SAP Business.</span><span class="sxs-lookup"><span data-stu-id="97177-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="97177-139">È necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nel Cloud di oggetto SAP Business.</span><span class="sxs-lookup"><span data-stu-id="97177-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="97177-140">hello tooestablish collegamento relazione, nel Cloud di oggetto Business di SAP, per **Username**, assegnare il valore di hello di hello **nome utente** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97177-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="97177-141">tooconfigure e prova AD Azure single sign-on con SAP Business oggetto Cloud, hello completo seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="97177-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="97177-142">[Configurare l'accesso Single Sign-On di Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="97177-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="97177-143">Imposta un toouse utente questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="97177-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="97177-144">[Creare un utente test di Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="97177-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="97177-145">Test AD Azure single sign-on con utente hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97177-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="97177-146">[Creare un utente di test di SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="97177-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="97177-147">Crea un equivalente di Britta Simon in SAP Business oggetto Cloud toohello collegato rappresentazione in forma di Azure AD dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="97177-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="97177-148">[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="97177-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="97177-149">Imposta Britta Simon toouse AD Azure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="97177-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97177-150">[Testare l'accesso Single Sign-On](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="97177-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="97177-151">Verifica che la configurazione di hello funziona.</span><span class="sxs-lookup"><span data-stu-id="97177-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="97177-152">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="97177-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="97177-153">In questa sezione accendere singola AD Azure sign-on in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="97177-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="97177-154">quindi si configura Single Sign-On nell'applicazione SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="97177-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="97177-155">tooset di Azure AD single sign-on con SAP Business oggetto Cloud:</span><span class="sxs-lookup"><span data-stu-id="97177-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="97177-156">Nel portale di Azure su hello hello **SAP Business oggetto Cloud** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="97177-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Selezionare Single Sign-On][4]

2. <span data-ttu-id="97177-158">In hello **Single sign-on** pagina per **modalità**selezionare **basato su SAML Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="97177-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Selezionare Accesso basato su SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="97177-160">In **SAP Business oggetto Cloud dominio e gli URL**completa hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="97177-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="97177-161">In hello **Sign-on URL** , immettere un URL con hello seguente motivo:</span><span class="sxs-lookup"><span data-stu-id="97177-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="97177-162">In hello **identificatore** , immettere un URL con hello seguente motivo:</span><span class="sxs-lookup"><span data-stu-id="97177-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URL della pagina SAP Business Object Cloud Domain and URLs (URL e dominio SAP Business Object Cloud)](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="97177-164">i valori Hello in questi URL sono solo a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="97177-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="97177-165">Aggiornare i valori hello con hello effettivo sign-on URL URL e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="97177-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="97177-166">tooget hello URL sign-on, hello contatto [team di supporto SAP Business oggetto Cloud Client](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="97177-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="97177-167">È possibile ottenere l'URL dell'identificatore hello scaricando i metadati di SAP Business oggetto Cloud hello dalla console di amministrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="97177-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="97177-168">Ciò è illustrato più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="97177-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="97177-169">In **Certificato di firma SAML** selezionare **XML metadati**,</span><span class="sxs-lookup"><span data-stu-id="97177-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="97177-170">Quindi, salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="97177-170">Then, save hello metadata file on your computer.</span></span>

    ![Selezionare XML metadati](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="97177-172">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="97177-172">Select **Save**.</span></span>

    ![Selezionare Salva](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="97177-174">In una finestra del web browser, accedere come amministratore nel sito della società di SAP Business oggetto Cloud tooyour.</span><span class="sxs-lookup"><span data-stu-id="97177-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="97177-175">Selezionare **Menu** > **Sistema** > **Amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="97177-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Selezionare Menu, quindi Sistema e infine Amministrazione](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="97177-177">In hello **sicurezza** scheda, seleziona hello **modifica** icona (penna).</span><span class="sxs-lookup"><span data-stu-id="97177-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![Nella scheda sicurezza hello, selezionare l'icona di modifica di hello](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="97177-179">Per **Metodo di autenticazione** selezionare **SAML Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="97177-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Selezionare SAML Single Sign-On per il metodo di autenticazione hello](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="97177-181">toodownload hello provider i metadati del servizio (passaggio 1), selezionare **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="97177-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="97177-182">Nel file di metadati hello, trovare e copiare hello **entityID** valore.</span><span class="sxs-lookup"><span data-stu-id="97177-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="97177-183">In hello Azure portale, in **SAP Business oggetto Cloud dominio e gli URL**, incollare il valore di hello in hello **identificatore** casella.</span><span class="sxs-lookup"><span data-stu-id="97177-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![Copiare e incollare il valore di entityID hello](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="97177-185">tooupload hello metadati del servizio provider (passaggio 2) nel file hello scaricato da hello portale di Azure in **i metadati del Provider di identità caricare**selezionare **caricare**.</span><span class="sxs-lookup"><span data-stu-id="97177-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![In Upload Identity Provider metadata (Caricare i metadati del provider di identità) selezionare Carica](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="97177-187">In hello **attributo utente** elencare, attributo utente di selezionare hello (passaggio 3) che si desidera toouse per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="97177-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="97177-188">Questo attributo utente esegue il mapping toohello provider di identità.</span><span class="sxs-lookup"><span data-stu-id="97177-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="97177-189">un attributo personalizzato nella pagina dell'utente hello, utilizzare hello tooenter **Mapping SAML personalizzate** opzione.</span><span class="sxs-lookup"><span data-stu-id="97177-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="97177-190">In alternativa, è possibile selezionare **posta elettronica** o **ID utente** come attributo utente hello.</span><span class="sxs-lookup"><span data-stu-id="97177-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="97177-191">In questo esempio, è selezionato **posta elettronica** perché è stato eseguito il mapping di attestazione dell'identificatore utente hello con hello **userprincipalname** attributo hello **gli attributi utente** sezione hello Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="97177-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="97177-192">Ciò fornisce un messaggio di posta elettronica utente univoco, che viene inviata toohello applicazione SAP Business oggetto Cloud a ogni risposta SAML corretta.</span><span class="sxs-lookup"><span data-stu-id="97177-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Selezionare Attributo utente](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="97177-194">account di hello tooverify con il provider di identità hello (passaggio 4), in hello **credenziali di account di accesso (posta elettronica)** , immettere l'indirizzo di posta elettronica dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="97177-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="97177-195">Selezionare quindi **Verifica account**.</span><span class="sxs-lookup"><span data-stu-id="97177-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="97177-196">sistema Hello aggiunge l'account utente toohello di credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="97177-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![Immettere l'indirizzo di posta elettronica e selezionare Verifica account](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="97177-198">Seleziona hello **salvare** icona.</span><span class="sxs-lookup"><span data-stu-id="97177-198">Select hello **Save** icon.</span></span>

    ![Icona Salva](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="97177-200">È possibile leggere una versione di queste istruzioni in hello concisa [portale di Azure](https://portal.azure.com), mentre si configura l'app.</span><span class="sxs-lookup"><span data-stu-id="97177-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="97177-201">Dopo aver aggiunto l'applicazione hello selezionando **Active Directory** > **applicazioni aziendali**selezionare hello **Single Sign-On** scheda. È possibile accedere alla documentazione di hello incorporato in hello **configurazione** alla sezione, hello parte inferiore della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="97177-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="97177-202">Per altre informazioni, vedere la [documentazione incorporata su Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="97177-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="97177-203">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="97177-203">Create an Azure AD test user</span></span>
<span data-ttu-id="97177-204">In questa sezione si crea un utente di test denominato Britta Simon in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="97177-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="97177-205">toocreate un utente di prova in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="97177-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="97177-206">Nel portale di Azure, nel menu a sinistra di hello, hello selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="97177-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97177-208">elenco di hello toodisplay di utenti, selezionare **utenti e gruppi**, quindi selezionare **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="97177-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97177-210">hello tooopen **utente** nella finestra di dialogo **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="97177-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97177-212">In hello **utente** della finestra di dialogo hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="97177-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="97177-213">In hello **nome** immettere **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97177-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="97177-214">In hello **nome utente** , immettere l'indirizzo di posta elettronica hello dell'utente hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97177-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="97177-215">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="97177-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="97177-216">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="97177-216">Select **Create**.</span></span>

        ![finestra di dialogo utente Hello](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Creare un utente di Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="97177-219">Creare un utente di test di SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="97177-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="97177-220">Agli utenti di Azure AD devono essere eseguiti nel Cloud di oggetto SAP Business prima che possano accedere in tooSAP Cloud oggetto Business.</span><span class="sxs-lookup"><span data-stu-id="97177-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="97177-221">In SAP Business Object Cloud il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="97177-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="97177-222">tooprovision un account utente:</span><span class="sxs-lookup"><span data-stu-id="97177-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="97177-223">Accedi tooyour sito della società SAP Business oggetto Cloud come amministratore.</span><span class="sxs-lookup"><span data-stu-id="97177-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="97177-224">Selezionare **Menu** > **Security** (Sicurezza)  > **Users** (Utenti).</span><span class="sxs-lookup"><span data-stu-id="97177-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="97177-226">In hello **utenti** tooadd nuovi dettagli dell'utente, selezionare  **+** .</span><span class="sxs-lookup"><span data-stu-id="97177-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![Pagina Aggiungi utenti (Aggiungi utenti)](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="97177-228">Completare quindi hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="97177-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="97177-229">In hello **ID utente** immettere hello l'ID dell'utente di hello, ad esempio **Laura**.</span><span class="sxs-lookup"><span data-stu-id="97177-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="97177-230">In hello **nome** immettere come nome dell'utente di hello, hello **Laura**.</span><span class="sxs-lookup"><span data-stu-id="97177-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="97177-231">In hello **cognome** immettere hello cognome di hello utente, ad esempio **Simon**.</span><span class="sxs-lookup"><span data-stu-id="97177-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="97177-232">In hello **nome visualizzato** casella, immettere hello nome completo dell'utente di hello, ad esempio **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="97177-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="97177-233">In hello **posta elettronica** immettere indirizzo di posta elettronica hello dell'utente di hello, ad esempio  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="97177-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="97177-234">In hello **Selezione ruoli** pagina, selezionare hello ruolo appropriato per l'utente hello e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="97177-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![Selezionare il ruolo](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="97177-236">Seleziona hello **salvare** icona.</span><span class="sxs-lookup"><span data-stu-id="97177-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="97177-237">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="97177-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="97177-238">In questa sezione utente hello Britta Simon toouse AD Azure single sign-on tramite la concessione di hello utente account accesso tooSAP Cloud oggetto Business.</span><span class="sxs-lookup"><span data-stu-id="97177-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="97177-239">tooassign Britta Simon tooSAP Cloud oggetto Business:</span><span class="sxs-lookup"><span data-stu-id="97177-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="97177-240">Nel portale di Azure hello, aprire visualizzazione applicazioni hello e fare clic sulla visualizzazione directory toohello.</span><span class="sxs-lookup"><span data-stu-id="97177-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="97177-241">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="97177-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="97177-243">Nell'elenco di applicazioni hello, selezionare **SAP Business oggetto Cloud**.</span><span class="sxs-lookup"><span data-stu-id="97177-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="97177-245">Nel menu a sinistra di hello, selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="97177-245">In hello left menu, select **Users and groups**.</span></span>

    ![Selezionare Utenti e gruppi][202] 

4. <span data-ttu-id="97177-247">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="97177-247">Select **Add**.</span></span> <span data-ttu-id="97177-248">Quindi, nella hello **Aggiungi** selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="97177-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![pagina Aggiungi Hello][203]

5. <span data-ttu-id="97177-250">In hello **utenti e gruppi** hello elenco di utenti, selezionare pagina **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="97177-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="97177-251">In hello **utenti e gruppi** selezionare **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="97177-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="97177-252">In hello **Aggiungi** selezionare **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="97177-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![Assegnazione del ruolo utente hello][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="97177-254">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="97177-254">Test single sign-on</span></span>

<span data-ttu-id="97177-255">In questa sezione si test configurazione di Azure AD single sign-on utilizzando il pannello di accesso di hello.</span><span class="sxs-lookup"><span data-stu-id="97177-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="97177-256">Quando si seleziona il riquadro di SAP Business oggetto Cloud hello nel Pannello di accesso hello, è necessario essere connessi automaticamente tooyour applicazione SAP Business oggetto Cloud.</span><span class="sxs-lookup"><span data-stu-id="97177-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="97177-257">Per ulteriori informazioni sul pannello di accesso hello, vedere [Pannello di accesso di introduzione toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="97177-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="97177-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="97177-258">Additional resources</span></span>

* [<span data-ttu-id="97177-259">Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97177-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97177-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97177-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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

