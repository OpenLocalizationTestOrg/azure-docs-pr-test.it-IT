---
title: 'Esercitazione: Integrazione di Azure Active Directory con Coupa | Documentazione Microsoft'
description: Informazioni su come toouse Coupa con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="70d89-103">Esercitazione: Integrazione di Azure Active Directory con Coupa</span><span class="sxs-lookup"><span data-stu-id="70d89-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="70d89-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Coupa.</span><span class="sxs-lookup"><span data-stu-id="70d89-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="70d89-105">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="70d89-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="70d89-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="70d89-106">A valid Azure subscription</span></span>
* <span data-ttu-id="70d89-107">Sottoscrizione di Coupa abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="70d89-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="70d89-108">Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooCoupa saranno in grado di toosingle sign in un'applicazione hello utilizzando hello [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="70d89-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="70d89-109">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="70d89-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="70d89-110">Abilitazione di hello integrazione dell'applicazione Coupa</span><span class="sxs-lookup"><span data-stu-id="70d89-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="70d89-111">Configurazione dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="70d89-111">Configuring single sign-on</span></span>
* <span data-ttu-id="70d89-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="70d89-112">Configuring user provisioning</span></span>
* <span data-ttu-id="70d89-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="70d89-113">Assigning users</span></span>

<span data-ttu-id="70d89-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="70d89-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="70d89-115">Abilitare l'integrazione dell'applicazione hello per Coupa</span><span class="sxs-lookup"><span data-stu-id="70d89-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="70d89-116">obiettivo di Hello di questa sezione è toooutline come tooenable hello integrazione dell'applicazione Coupa.</span><span class="sxs-lookup"><span data-stu-id="70d89-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="70d89-117">**tooenable hello integrazione dell'applicazione Coupa, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70d89-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="70d89-118">Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70d89-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="70d89-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="70d89-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="70d89-120">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="70d89-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="70d89-121">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="70d89-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="70d89-122">![Applicazioni](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="70d89-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="70d89-123">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="70d89-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="70d89-124">![Aggiungere un'applicazione](./media/active-directory-saas-coupa-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="70d89-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="70d89-125">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="70d89-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="70d89-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-coupa-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="70d89-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="70d89-127">In hello **casella di ricerca**, tipo **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="70d89-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="70d89-128">![Raccolta di applicazioni](./media/active-directory-saas-coupa-tutorial/IC791898.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="70d89-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="70d89-129">Nel riquadro risultati hello selezionare **Coupa**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="70d89-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="70d89-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="70d89-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="70d89-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="70d89-131">Configure single sign-on</span></span>

<span data-ttu-id="70d89-132">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooCoupa con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="70d89-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="70d89-133">La configurazione di single sign-on per Coupa richiede tooretrieve un valore di identificazione personale da un certificato.</span><span class="sxs-lookup"><span data-stu-id="70d89-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="70d89-134">Se non si ha familiarità con questa procedura, vedere [come tooretrieve il valore di identificazione personale del certificato](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="70d89-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="70d89-135">**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70d89-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="70d89-136">Accesso tooyour sito della società Coupa come amministratore.</span><span class="sxs-lookup"><span data-stu-id="70d89-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="70d89-137">Andare troppo**installazione \> controllo di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="70d89-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="70d89-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="70d89-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="70d89-139">Fare clic su toodownload hello Coupa metadati file tooyour computer **scaricare e importare metadati SP**.</span><span class="sxs-lookup"><span data-stu-id="70d89-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="70d89-140">![Metadati Coupa SP](./media/active-directory-saas-coupa-tutorial/IC791901.png "Metadati Coupa SP")</span><span class="sxs-lookup"><span data-stu-id="70d89-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="70d89-141">In un'altra finestra del browser, accedere toohello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="70d89-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="70d89-142">In hello **Coupa** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="70d89-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="70d89-143">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="70d89-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="70d89-144">In hello **come si sarebbe ad esempio utenti toosign su tooCoupa** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="70d89-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="70d89-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="70d89-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="70d89-146">In hello **Configura URL App** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="70d89-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="70d89-147">![Configurare l'URL dell'app](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="70d89-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="70d89-148">In hello **URL di accesso** casella di testo, digitare l'URL usato per il toosign gli utenti in tooyour applicazione Coupa (ad esempio: "*http://company.Coupa.com*").</span><span class="sxs-lookup"><span data-stu-id="70d89-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="70d89-149">Aprire il file di metadati Coupa scaricato e quindi copiare hello **AssertionConsumerService index/URL**.</span><span class="sxs-lookup"><span data-stu-id="70d89-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="70d89-150">In hello **URL di risposta Coupa** casella di testo, incollare hello **AssertionConsumerService index/URL** valore.</span><span class="sxs-lookup"><span data-stu-id="70d89-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="70d89-151">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="70d89-151">Click **Next**.</span></span>
8. <span data-ttu-id="70d89-152">In hello **Configura accesso single sign-on in Coupa** pagina, toodownload il file di metadati, fare clic su **Scarica metadati**e quindi salvare il file hello in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="70d89-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="70d89-153">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="70d89-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="70d89-154">Nel sito della società Coupa hello passare troppo**installazione \> controllo di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="70d89-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="70d89-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="70d89-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="70d89-156">In hello **accedere con credenziali Coupa** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="70d89-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="70d89-157">![Accesso mediante le credenziali di Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Accesso mediante le credenziali di Coupa")</span><span class="sxs-lookup"><span data-stu-id="70d89-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="70d89-158">Selezionare **Accedere mediante SAML**.</span><span class="sxs-lookup"><span data-stu-id="70d89-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="70d89-159">Fare clic su **Sfoglia** tooupload il file di metadati scaricato Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="70d89-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="70d89-160">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="70d89-160">Click **Save**.</span></span>
11. <span data-ttu-id="70d89-161">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="70d89-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="70d89-162">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="70d89-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="70d89-163">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="70d89-163">Configure user provisioning</span></span>

<span data-ttu-id="70d89-164">In ordine tooenable Azure AD utenti toolog a Coupa, è necessario eseguirne il provisioning in Coupa.</span><span class="sxs-lookup"><span data-stu-id="70d89-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="70d89-165">Nel caso di hello di Coupa, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="70d89-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="70d89-166">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70d89-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="70d89-167">Accedi tooyour **Coupa** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="70d89-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="70d89-168">Scegliere dal menu hello in primo piano hello **installazione**e quindi fare clic su **utenti**.</span><span class="sxs-lookup"><span data-stu-id="70d89-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="70d89-169">![Utenti](./media/active-directory-saas-coupa-tutorial/IC791908.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="70d89-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="70d89-170">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="70d89-170">Click **Create**.</span></span>
   
   <span data-ttu-id="70d89-171">![Creare utenti](./media/active-directory-saas-coupa-tutorial/IC791909.png "Creare utenti")</span><span class="sxs-lookup"><span data-stu-id="70d89-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="70d89-172">In hello **utente creare** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="70d89-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="70d89-173">![Dettagli utente](./media/active-directory-saas-coupa-tutorial/IC791910.png "Dettagli utente")</span><span class="sxs-lookup"><span data-stu-id="70d89-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="70d89-174">Hello tipo **accesso**, **nome**, **Last Name**, **Single Sign-On ID**, **posta elettronica** gli attributi di un account di Azure Active Directory valido desiderate tooprovision hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="70d89-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="70d89-175">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="70d89-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="70d89-176">titolare dell'account di Azure Active Directory Hello verrà visualizzato un messaggio di posta elettronica con un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="70d89-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="70d89-177">È possibile usare qualsiasi altro Coupa utente account strumento di creazione o le API fornite da Coupa tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="70d89-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="70d89-178">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="70d89-178">Assign users</span></span>
<span data-ttu-id="70d89-179">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="70d89-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="70d89-180">**tooassign tooCoupa di utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70d89-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="70d89-181">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="70d89-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="70d89-182">In hello * * Coupa * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="70d89-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="70d89-183">![Assegnare utenti](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="70d89-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="70d89-184">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="70d89-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="70d89-185">![Sì](./media/active-directory-saas-coupa-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="70d89-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="70d89-186">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="70d89-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="70d89-187">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="70d89-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

