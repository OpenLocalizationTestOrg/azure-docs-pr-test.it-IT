---
title: Autenticazione basata su intestazione con PingAccess per il proxy dell'applicazione di Azure AD | Microsoft Docs
description: Pubblicare le applicazioni con PingAccess e il proxy dell'applicazione per supportare l'autenticazione basata su intestazione.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 58034ab8830cf655199875b448948ea14dc04a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="ac349-103">Autenticazione basata su intestazione per l'accesso Single Sign-On con il proxy di applicazione e PingAccess</span><span class="sxs-lookup"><span data-stu-id="ac349-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="ac349-104">Il proxy dell'applicazione Azure Active Directory e PingAccess hanno collaborato per fornire ai clienti di Azure Active Directory l'accesso a un numero ancora maggiore di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ac349-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span></span> <span data-ttu-id="ac349-105">PingAccess espande le [offerte esistenti del proxy di applicazione](active-directory-application-proxy-get-started.md) in modo da includere l'accesso Single Sign-On alle applicazioni che usano intestazioni per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ac349-105">PingAccess expands the [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) to include single sign-on access to applications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="ac349-106">Che cos'è PingAccess per Azure AD?</span><span class="sxs-lookup"><span data-stu-id="ac349-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="ac349-107">PingAccess per Azure Active Directory è un'offerta di PingAccess che consente di mettere a disposizione degli utenti l'accesso e l'accesso Single Sign-On alle applicazioni che usano intestazioni per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ac349-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span></span> <span data-ttu-id="ac349-108">Il proxy dell'applicazione tratta queste app come qualsiasi altra, usando Azure AD per autenticare l'accesso e quindi passando il traffico attraverso il servizio del connettore.</span><span class="sxs-lookup"><span data-stu-id="ac349-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span></span> <span data-ttu-id="ac349-109">PingAccess sta davanti alle app e converte il token di accesso da Azure AD in un'intestazione, in modo che l'applicazione riceva l'autenticazione nel formato che è in grado di leggere.</span><span class="sxs-lookup"><span data-stu-id="ac349-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span></span>

<span data-ttu-id="ac349-110">Gli utenti non noteranno nulla di diverso quando eseguono l'accesso per usare le app aziendali.</span><span class="sxs-lookup"><span data-stu-id="ac349-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span></span> <span data-ttu-id="ac349-111">Possono comunque lavorare da qualsiasi luogo e dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac349-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="ac349-112">Poiché i connettori del proxy dell'applicazione indirizzano il traffico remoto a tutte le app indipendentemente dal loro tipo di autenticazione, continueranno a bilanciare il carico automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ac349-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="ac349-113">Come si ottiene l'accesso?</span><span class="sxs-lookup"><span data-stu-id="ac349-113">How do I get access?</span></span>

<span data-ttu-id="ac349-114">Poiché questo scenario è il risultato di una partnership fra Azure Active Directory e PingAccess, sono necessarie le licenze per entrambi i servizi.</span><span class="sxs-lookup"><span data-stu-id="ac349-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="ac349-115">Le sottoscrizioni Premium di Azure Active Directory, tuttavia, includono una licenza PingAccess di base che copre fino a 20 applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ac349-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span></span> <span data-ttu-id="ac349-116">Se è necessario pubblicare più di 20 applicazioni basate su intestazione, è possibile acquistare una licenza aggiuntiva da PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="ac349-117">Per altre informazioni, vedere [Edizioni di Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="ac349-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="ac349-118">Pubblicare l'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="ac349-118">Publish your application in Azure</span></span>

<span data-ttu-id="ac349-119">Questo articolo è destinato a chi pubblica un'app con questo scenario per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="ac349-119">This article is intended for people who are publishing an app with this scenario for the first time.</span></span> <span data-ttu-id="ac349-120">Illustra come iniziare a usare sia l'applicazione sia PingAccess, oltre ai passaggi di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="ac349-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span></span> <span data-ttu-id="ac349-121">Se sono già stati configurati entrambi i servizi ma si vuole rivedere i passaggi di pubblicazione, è possibile ignorare l'installazione del connettore e passare a [Aggiungere l'app in Azure AD con il proxy dell'applicazione](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="ac349-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="ac349-122">Poiché questo scenario è il risultato di una partnership fra Azure AD e PingAccess, alcune delle istruzioni sono presenti sul sito di Ping Identity.</span><span class="sxs-lookup"><span data-stu-id="ac349-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="ac349-123">Installare un connettore proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="ac349-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="ac349-124">Se il proxy di applicazione è già attivato e si ha già un connettore installato, è possibile ignorare questa sezione e passare a [Aggiungere l'app in Azure AD con il proxy dell'applicazione](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="ac349-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="ac349-125">Il connettore del proxy di applicazione è un servizio di Windows Server che indirizza il traffico dai dipendenti remoti alle app pubblicate.</span><span class="sxs-lookup"><span data-stu-id="ac349-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span></span> <span data-ttu-id="ac349-126">Per istruzioni di installazione più dettagliate, vedere [Abilitare il proxy di applicazione nel portale di Azure](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="ac349-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="ac349-127">Accedere al [portale di Azure](https://portal.azure.com) come amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="ac349-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="ac349-128">Selezionare **Azure Active Directory** > **Proxy dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="ac349-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="ac349-129">Selezionare **Download Connector** (Scarica il connettore) per avviare il download del connettore del proxy di applicazione.</span><span class="sxs-lookup"><span data-stu-id="ac349-129">Select **Download Connector** to start the Application Proxy connector download.</span></span> <span data-ttu-id="ac349-130">Seguire le istruzioni di installazione.</span><span class="sxs-lookup"><span data-stu-id="ac349-130">Follow the installation instructions.</span></span>

   ![Abilitare il proxy dell'applicazione e scaricare il connettore](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="ac349-132">Scaricando il connettore si attiverà automaticamente il proxy di applicazione per la directory, ma se così non fosse, è possibile selezionare **Abilita proxy di applicazione**.</span><span class="sxs-lookup"><span data-stu-id="ac349-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-to-azure-ad-with-application-proxy"></a><span data-ttu-id="ac349-133">Aggiungere l'app ad Azure AD con il proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ac349-133">Add your app to Azure AD with Application Proxy</span></span>

<span data-ttu-id="ac349-134">Nel portale di Azure è necessario eseguire due azioni.</span><span class="sxs-lookup"><span data-stu-id="ac349-134">There are two actions you need to take in the Azure portal.</span></span> <span data-ttu-id="ac349-135">Per prima cosa, si pubblica l'applicazione con il proxy di applicazione,</span><span class="sxs-lookup"><span data-stu-id="ac349-135">First, you need to publish your application with Application Proxy.</span></span> <span data-ttu-id="ac349-136">quindi si raccolgono alcune informazioni sull'app che è possibile usare durante la procedura di PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span></span>

<span data-ttu-id="ac349-137">Seguire questi passaggi per pubblicare l'app.</span><span class="sxs-lookup"><span data-stu-id="ac349-137">Follow these steps to publish your app.</span></span> <span data-ttu-id="ac349-138">Per una descrizione più dettagliata dei passaggi 1-8, vedere [Pubblicare applicazioni mediante il proxy di applicazione AD Azure](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac349-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="ac349-139">Se non lo si è fatto nell'ultima sezione, accedere al [portale di Azure](https://portal.azure.com) come amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="ac349-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="ac349-140">Selezionare **Azure Active Directory** > **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ac349-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="ac349-141">Selezionare **Aggiungi** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="ac349-141">Select **Add** at the top of the blade.</span></span>
4. <span data-ttu-id="ac349-142">Selezionare **Applicazione locale**.</span><span class="sxs-lookup"><span data-stu-id="ac349-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="ac349-143">Compilare i campi obbligatori con le informazioni della nuova app.</span><span class="sxs-lookup"><span data-stu-id="ac349-143">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="ac349-144">Usare le seguenti linee guida per le impostazioni:</span><span class="sxs-lookup"><span data-stu-id="ac349-144">Use the following guidance for the settings:</span></span>
   - <span data-ttu-id="ac349-145">**URL interno**: normalmente si indica l'URL che porta alla pagina di accesso dell'app quando ci si trova nella rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="ac349-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span></span> <span data-ttu-id="ac349-146">Per questo scenario il connettore deve trattare il proxy PingAccess come prima pagina dell'app.</span><span class="sxs-lookup"><span data-stu-id="ac349-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span></span> <span data-ttu-id="ac349-147">Usare il formato seguente: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="ac349-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="ac349-148">La porta 3000 per impostazione predefinita, ma è possibile configurarla in PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-148">The port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="ac349-149">**Metodo di autenticazione preliminare**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac349-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="ac349-150">**Tradurre URL nelle intestazioni**: No</span><span class="sxs-lookup"><span data-stu-id="ac349-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="ac349-151">Se si tratta della prima applicazione, usare inizialmente la porta 3000 e aggiornare questa impostazione se viene modificata la configurazione di PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-151">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="ac349-152">Se si tratta almeno di una seconda app, è necessaria una corrispondenza con il listener configurato in PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-152">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="ac349-153">Altre informazioni sui [listener in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="ac349-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="ac349-154">Selezionare **Aggiungi** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="ac349-154">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="ac349-155">L'applicazione viene aggiunta e si apre il menu di avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="ac349-155">Your application is added, and the quick start menu opens.</span></span>
7. <span data-ttu-id="ac349-156">Nel menu di avvio rapido selezionare **Assegna utente per il test** e aggiungere almeno un utente all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ac349-156">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="ac349-157">Assicurarsi che questo account di test abbia accesso all'applicazione locale.</span><span class="sxs-lookup"><span data-stu-id="ac349-157">Make sure this test account has access to the on-premises application.</span></span>
8. <span data-ttu-id="ac349-158">Selezionare **Assegna** per salvare l'assegnazione dell'utente di test.</span><span class="sxs-lookup"><span data-stu-id="ac349-158">Select **Assign** to save the test user assignment.</span></span>
9. <span data-ttu-id="ac349-159">Nel pannello di gestione dell'app selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ac349-159">On the app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="ac349-160">Scegliere **Header-based sign-on** (Accesso basato su intestazione) dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="ac349-160">Choose **Header-based sign-on** from the drop-down menu.</span></span> <span data-ttu-id="ac349-161">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ac349-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="ac349-162">Se è la prima volta che si usa l'accesso Single Sign-On basato su intestazione, è necessario installare PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-162">If this is your first time using header-based single sign-on, you need to install PingAccess.</span></span> <span data-ttu-id="ac349-163">Per assicurarsi che la sottoscrizione di Azure venga associata automaticamente all'installazione di PingAccess, usare il collegamento presente nella pagina dell'accesso Single Sign-On per scaricare PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-163">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span></span> <span data-ttu-id="ac349-164">È possibile aprire il sito di download ora o in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ac349-164">You can open the download site now, or come back to this page later.</span></span> 

   ![Selezionare l'accesso basato su intestazione](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="ac349-166">Chiudere il pannello Applicazioni aziendali o scorrere completamente a sinistra per tornare al menu di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac349-166">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
12. <span data-ttu-id="ac349-167">Selezionare **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="ac349-167">Select **App registrations**.</span></span>

   ![Selezionare Registrazioni per l'app](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="ac349-169">Selezionare l'app appena aggiunta e quindi **URL di risposta**.</span><span class="sxs-lookup"><span data-stu-id="ac349-169">Select the app you just added, then **Reply URLs**.</span></span>

   ![Selezionare URL di risposta](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="ac349-171">Verificare se l'URL esterno assegnato all'app al passaggio 5 è incluso nell'elenco URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="ac349-171">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span></span> <span data-ttu-id="ac349-172">In caso contrario aggiungerlo ora.</span><span class="sxs-lookup"><span data-stu-id="ac349-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="ac349-173">Nel pannello delle impostazioni dell'app selezionare **Autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="ac349-173">On the app settings blade, select **Required permissions**.</span></span>

  ![Selezionare Autorizzazioni necessarie](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="ac349-175">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ac349-175">Select **Add**.</span></span> <span data-ttu-id="ac349-176">Per l'API scegliere **Windows Azure Active Directory** e quindi **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="ac349-176">For the API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="ac349-177">Per le autorizzazioni scegliere **Read and write all applications** (Leggi e scrivi in tutte le applicazioni) e **Accedi e leggi il profilo di un altro utente** e quindi **Seleziona** e **Fine**.</span><span class="sxs-lookup"><span data-stu-id="ac349-177">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Autorizzazioni SELECT](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-the-pingaccess-steps"></a><span data-ttu-id="ac349-179">Raccogliere informazioni per la procedura PingAccess</span><span class="sxs-lookup"><span data-stu-id="ac349-179">Collect information for the PingAccess steps</span></span>

1. <span data-ttu-id="ac349-180">Nel pannello delle impostazioni dell'app selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="ac349-180">On your app settings blade, select **Properties**.</span></span> 

  ![Selezionare Proprietà](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="ac349-182">Annotare il valore **ID applicazione**.</span><span class="sxs-lookup"><span data-stu-id="ac349-182">Save the **Application Id** value.</span></span> <span data-ttu-id="ac349-183">Sarà usato come ID client per la configurazione di PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-183">This is used for the client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="ac349-184">Nel pannello delle impostazioni dell'app selezionare **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="ac349-184">On the app settings blade, select **Keys**.</span></span>

  ![Selezionare Chiavi](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="ac349-186">Creare una chiave immettendo una descrizione della chiave e scegliendo una data di scadenza dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="ac349-186">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span></span>
5. <span data-ttu-id="ac349-187">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ac349-187">Select **Save**.</span></span> <span data-ttu-id="ac349-188">Viene visualizzato un GUID nel campo **Valore**.</span><span class="sxs-lookup"><span data-stu-id="ac349-188">A GUID appears in the **Value** field.</span></span>

  <span data-ttu-id="ac349-189">Annotare il valore adesso, in quanto non sarà più visibile dopo aver chiuso questa finestra.</span><span class="sxs-lookup"><span data-stu-id="ac349-189">Save this value now, as you won’t be able to see it again after you close this window.</span></span>

  ![Creare una nuova chiave](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="ac349-191">Chiudere il pannello Registrazioni per l'app o scorrere completamente a sinistra per tornare al menu di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac349-191">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
7. <span data-ttu-id="ac349-192">Selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="ac349-192">Select **Properties**.</span></span>
8. <span data-ttu-id="ac349-193">Salvare il GUID **ID directory**.</span><span class="sxs-lookup"><span data-stu-id="ac349-193">Save the **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-to-send-custom-fields"></a><span data-ttu-id="ac349-194">Facoltativo: aggiornare GraphAPI per inviare campi personalizzati</span><span class="sxs-lookup"><span data-stu-id="ac349-194">Optional - Update GraphAPI to send custom fields</span></span>

<span data-ttu-id="ac349-195">Per un elenco dei token di sicurezza che Azure AD invia per l'autenticazione, vedere [Riferimento al token di Azure AD](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="ac349-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="ac349-196">Se è necessaria un'attestazione personalizzata che invia altri token, usare GraphAPI per impostare il campo app *acceptMappedClaims* su **True**.</span><span class="sxs-lookup"><span data-stu-id="ac349-196">If you need a custom claim that sends other tokens, use GraphAPI to set the app field *acceptMappedClaims* to **True**.</span></span> <span data-ttu-id="ac349-197">Per eseguire questa configurazione è possibile usare Azure AD Graph Explorer o Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ac349-197">You can use either Azure AD Graph Explorer or MS Graph to make this configuration.</span></span> 

<span data-ttu-id="ac349-198">In questo esempio viene usato Graph Explorer:</span><span class="sxs-lookup"><span data-stu-id="ac349-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="ac349-199">Scaricare PingAccess e configurare l'app</span><span class="sxs-lookup"><span data-stu-id="ac349-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="ac349-200">Dopo aver completato la procedura di installazione di Azure Active Directory, è possibile ora passare alla configurazione di PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-200">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span></span> 

<span data-ttu-id="ac349-201">I passaggi dettagliati per la parte PingAccess di questo scenario continuano nella documentazione di Ping Identity, [Configurare PingAccess per Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="ac349-201">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="ac349-202">Questi passaggi consentono di ottenere un account PingAccess se non se ne possiede già uno, installare PingAccess Server e creare una connessione al Provider OIDC di Azure AD con l'ID directory copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac349-202">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span></span> <span data-ttu-id="ac349-203">È quindi possibile usare i valori dell'ID applicazione e della chiave per creare una sessione Web in PingAccess.</span><span class="sxs-lookup"><span data-stu-id="ac349-203">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span></span> <span data-ttu-id="ac349-204">Successivamente è possibile impostare i mapping delle identità e creare l'host virtuale, il sito e l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ac349-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="ac349-205">Test dell'app</span><span class="sxs-lookup"><span data-stu-id="ac349-205">Test your app</span></span>

<span data-ttu-id="ac349-206">Dopo aver completato tutti questi passaggi, l'app dovrebbe funzionare.</span><span class="sxs-lookup"><span data-stu-id="ac349-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="ac349-207">Per verificarlo aprire un browser e passare all'URL esterno creato quando è stata pubblicata l'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="ac349-207">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span></span> <span data-ttu-id="ac349-208">Accedere con l'account di test assegnato all'app.</span><span class="sxs-lookup"><span data-stu-id="ac349-208">Sign in with the test account that you assigned to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac349-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac349-209">Next steps</span></span>

- <span data-ttu-id="ac349-210">[Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html) (Configurare PingAccess per Azure AD)</span><span class="sxs-lookup"><span data-stu-id="ac349-210">[Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)</span></span>
- [<span data-ttu-id="ac349-211">Come viene offerto l'accesso Single Sign-On dal proxy di applicazione di Azure AD?</span><span class="sxs-lookup"><span data-stu-id="ac349-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="ac349-212">Risolvere i problemi del Proxy applicazione</span><span class="sxs-lookup"><span data-stu-id="ac349-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
