---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zscaler Private Access (ZPA) | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e di accesso privata Zscaler (ZPA).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="f1490-103">Esercitazione: Integrazione di Azure Active Directory con Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="f1490-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="f1490-104">In questa esercitazione, è illustrato come toointegrate Zscaler privata accesso (ZPA) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1490-104">In this tutorial, you learn how toointegrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1490-105">Integrazione di accesso privata Zscaler (ZPA) con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f1490-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1490-106">È possibile controllare in Azure AD che ha accesso tooZscaler accesso privato (ZPA)</span><span class="sxs-lookup"><span data-stu-id="f1490-106">You can control in Azure AD who has access tooZscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="f1490-107">È possibile abilitare l'utenti tooautomatically get connesso tooZscaler privata accesso (ZPA) (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-107">You can enable your users tooautomatically get signed-on tooZscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1490-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="f1490-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="f1490-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1490-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1490-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f1490-110">Prerequisites</span></span>

<span data-ttu-id="f1490-111">integrazione di Azure AD con Zscaler privata accesso (ZPA) tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f1490-111">tooconfigure Azure AD integration with Zscaler Private Access (ZPA), you need hello following items:</span></span>

- <span data-ttu-id="f1490-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1490-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1490-113">Una sottoscrizione attiva con accesso Single Sign-on per Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="f1490-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="f1490-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f1490-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="f1490-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f1490-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1490-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f1490-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f1490-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1490-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f1490-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f1490-118">Scenario description</span></span>
<span data-ttu-id="f1490-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f1490-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1490-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f1490-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1490-121">Aggiunta di accesso privata Zscaler (ZPA) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f1490-121">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
2. <span data-ttu-id="f1490-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a><span data-ttu-id="f1490-123">Aggiunta di accesso privata Zscaler (ZPA) dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f1490-123">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
<span data-ttu-id="f1490-124">integrazione di hello di tooconfigure di Zscaler privata accesso (ZPA) in Azure AD, è necessario tooadd accesso privato Zscaler (ZPA) dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f1490-124">tooconfigure hello integration of Zscaler Private Access (ZPA) into Azure AD, you need tooadd Zscaler Private Access (ZPA) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1490-125">**tooadd Zscaler privata accesso (ZPA) dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f1490-125">**tooadd Zscaler Private Access (ZPA) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1490-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f1490-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1490-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f1490-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1490-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f1490-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f1490-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f1490-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f1490-133">Nella casella di ricerca hello, digitare **accesso privato Zscaler (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="f1490-133">In hello search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="f1490-135">Nel riquadro dei risultati hello, selezionare **accesso privato Zscaler (ZPA)**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f1490-135">In hello results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1490-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1490-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zscaler Private Access (ZPA) in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f1490-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1490-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Zscaler privata accesso (ZPA) è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1490-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Private Access (ZPA) is tooa user in Azure AD.</span></span> <span data-ttu-id="f1490-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello in Zscaler privata accesso (ZPA) richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f1490-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Private Access (ZPA) needs toobe established.</span></span>

<span data-ttu-id="f1490-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Zscaler privata accesso (ZPA).</span><span class="sxs-lookup"><span data-stu-id="f1490-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="f1490-142">tooconfigure e test Azure single sign-on AD con Zscaler privata accesso (ZPA), è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f1490-142">tooconfigure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1490-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f1490-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1490-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1490-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1490-145">**[Creazione di un utente di test di accesso privata Zscaler (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave un equivalente di Britta Simon in Zscaler privata accesso (ZPA) che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f1490-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - toohave a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f1490-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1490-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1490-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f1490-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1490-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1490-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione di accesso privata Zscaler (ZPA).</span><span class="sxs-lookup"><span data-stu-id="f1490-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="f1490-150">**tooconfigure Azure single sign-on AD con Zscaler privata di accesso (ZPA), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f1490-150">**tooconfigure Azure AD single sign-on with Zscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="f1490-151">Nel portale di gestione di Azure hello in hello **accesso privato Zscaler (ZPA)** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f1490-151">In hello Azure Management portal, on hello **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f1490-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1490-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="f1490-155">In hello **URL e il dominio di accesso privata Zscaler (ZPA)** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f1490-155">On hello **Zscaler Private Access (ZPA) Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="f1490-157">a.</span><span class="sxs-lookup"><span data-stu-id="f1490-157">a.</span></span> <span data-ttu-id="f1490-158">In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="f1490-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="f1490-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1490-159">b.</span></span> <span data-ttu-id="f1490-160">In hello **identificatore** casella di testo, tipo:`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="f1490-160">In hello **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1490-161">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="f1490-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="f1490-162">È necessario tooupdate questi valori con hello effettivo accesso URL e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="f1490-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="f1490-163">In questo caso, è consigliabile si toouse hello valore univoco dell'URL di identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="f1490-163">Here we suggest you toouse hello unique value of URL in hello Identifier.</span></span> <span data-ttu-id="f1490-164">Contatto [team di supporto di accesso privata Zscaler (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="f1490-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooget these values.</span></span>

4. <span data-ttu-id="f1490-165">In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="f1490-165">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="f1490-167">In hello **creare nuovo certificato** finestra di dialogo, fare clic sull'icona calendario hello e selezionare un **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="f1490-167">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="f1490-168">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f1490-168">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="f1490-170">In hello **certificato di firma SAML** selezionare **attivare di nuovo certificato** e fare clic su **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f1490-170">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="f1490-172">Nel menu a comparsa hello **il certificato di Rollover** finestra, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1490-172">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="f1490-174">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f1490-174">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="f1490-176">In un'altra finestra del Web browser accedere al sito aziendale di Zscaler Private Access (ZPA) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f1490-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="f1490-177">Passare troppo**amministratore** e quindi fare clic su **Idp configurazione**.</span><span class="sxs-lookup"><span data-stu-id="f1490-177">Navigate too**Administrator** and then click **Idp Configuration**.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="f1490-179">In hello **configurazione Idp** fare clic su **Aggiungi nuova configurazione IDP**.</span><span class="sxs-lookup"><span data-stu-id="f1490-179">In hello **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="f1490-181">In hello **nuova configurazione IDP** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f1490-181">In hello **New IDP Configuration** section, perform hello following steps:</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="f1490-183">a.</span><span class="sxs-lookup"><span data-stu-id="f1490-183">a.</span></span> <span data-ttu-id="f1490-184">Per caricare il file di metadati scaricato, fare clic su **Seleziona file**.</span><span class="sxs-lookup"><span data-stu-id="f1490-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="f1490-185">b.</span><span class="sxs-lookup"><span data-stu-id="f1490-185">b.</span></span> <span data-ttu-id="f1490-186">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f1490-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1490-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1490-188">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="f1490-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f1490-190">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f1490-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1490-191">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f1490-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1490-193">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="f1490-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1490-195">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f1490-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1490-197">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f1490-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1490-199">a.</span><span class="sxs-lookup"><span data-stu-id="f1490-199">a.</span></span> <span data-ttu-id="f1490-200">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1490-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1490-201">b.</span><span class="sxs-lookup"><span data-stu-id="f1490-201">b.</span></span> <span data-ttu-id="f1490-202">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1490-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1490-203">c.</span><span class="sxs-lookup"><span data-stu-id="f1490-203">c.</span></span> <span data-ttu-id="f1490-204">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f1490-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1490-205">d.</span><span class="sxs-lookup"><span data-stu-id="f1490-205">d.</span></span> <span data-ttu-id="f1490-206">Fare clic su **Create**(Crea).</span><span class="sxs-lookup"><span data-stu-id="f1490-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="f1490-207">Creazione di un utente di test Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="f1490-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="f1490-208">In questa sezione viene creato un utente di nome Britta Simon in a Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="f1490-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="f1490-209">Rivolgersi [team di supporto di accesso privata Zscaler (ZPA)](https://help.zscaler.com/zpa-submit-ticket) utenti hello tooadd nella piattaforma di accesso privata Zscaler (ZPA) hello.</span><span class="sxs-lookup"><span data-stu-id="f1490-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooadd hello users in hello Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1490-210">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1490-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1490-211">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooZscaler accesso accesso privato (ZPA).</span><span class="sxs-lookup"><span data-stu-id="f1490-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooZscaler Private Access (ZPA).</span></span>

![Assegna utente][200] 

<span data-ttu-id="f1490-213">**tooassign Britta Simon tooZscaler accesso privato (ZPA), eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f1490-213">**tooassign Britta Simon tooZscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="f1490-214">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f1490-214">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f1490-216">Nell'elenco di applicazioni hello, selezionare **accesso privato Zscaler (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="f1490-216">In hello applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="f1490-218">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f1490-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f1490-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f1490-220">Click **Add** button.</span></span> <span data-ttu-id="f1490-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f1490-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f1490-223">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f1490-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1490-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f1490-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1490-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f1490-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="f1490-226">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f1490-226">Testing single sign-on</span></span>

<span data-ttu-id="f1490-227">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f1490-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f1490-228">Quando si fa clic su riquadro di accesso privata Zscaler (ZPA) hello in hello Pannello di accesso, è necessario ottenere l'applicazione di accesso privata Zscaler (ZPA) tooyour automaticamente firmato in.</span><span class="sxs-lookup"><span data-stu-id="f1490-228">When you click hello Zscaler Private Access (ZPA) tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f1490-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f1490-229">Additional resources</span></span>

* [<span data-ttu-id="f1490-230">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1490-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1490-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1490-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png