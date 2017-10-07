---
title: aaaHow tooenable SSO tra app in iOS usando ADAL | Documenti Microsoft
description: "Come funzionalità hello toouse di hello tooenable SDK ADAL Single Sign-On tra le applicazioni. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="a6929-103">Come tooenable SSO tra app in iOS usando ADAL</span><span class="sxs-lookup"><span data-stu-id="a6929-103">How tooenable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="a6929-104">Fornendo Single Sign-On (SSO) in modo che gli utenti solo tooenter le proprie credenziali una sola volta e le credenziali di lavoro automaticamente tutte le applicazioni è previsto dai clienti.</span><span class="sxs-lookup"><span data-stu-id="a6929-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="a6929-105">immissione di nome utente e password su schermi di piccole dimensioni, spesso volte combinate con un fattore aggiuntivo (2FA), ad esempio una telefonata o un codice via SMS, la difficoltà di Hello risultati in rapida insoddisfazione dei clienti se un utente ha toodo più di una volta per il prodotto.</span><span class="sxs-lookup"><span data-stu-id="a6929-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="a6929-106">Inoltre, se si applica una piattaforma di identità che altre applicazioni possono utilizzare, ad esempio Accounts Microsoft o un account aziendale da Office 365, i clienti prevedere che toouse disponibili di toobe tali credenziali in tutte le proprie applicazioni indipendentemente dal fornitore hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="a6929-107">Hello piattaforma Microsoft Identity, con il SDK di identità di Microsoft, funziona disco rigido per l'utente e fornisce capacità toodelight hello i clienti con SSO sia nel proprio gruppo di applicazioni o, come con le funzionalità di Service broker e un autenticatore applicazioni, attraverso intero dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="a6929-108">Questa procedura dettagliata verrà specificato come tooconfigure Windows SDK all'interno di tooprovide l'applicazione ai clienti tooyour questo vantaggio.</span><span class="sxs-lookup"><span data-stu-id="a6929-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="a6929-109">Questa procedura si applica a:</span><span class="sxs-lookup"><span data-stu-id="a6929-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="a6929-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6929-110">Azure Active Directory</span></span>
* <span data-ttu-id="a6929-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="a6929-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="a6929-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="a6929-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="a6929-113">Accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6929-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="a6929-114">documento Hello precedente presuppone che si conosca come troppo[provisioning delle applicazioni nel portale di hello legacy per Azure Active Directory](active-directory-how-to-integrate.md) e l'applicazione integrata con hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="a6929-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="a6929-115">Concetti di SSO nella piattaforma delle identità Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="a6929-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="a6929-116">Broker di Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="a6929-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="a6929-117">Microsoft fornisce le applicazioni per ogni piattaforma per dispositivi mobili che consentono il bridging delle credenziali tra le applicazioni di fornitori diversi hello e consente a particolari funzionalità avanzate che richiedono un'unica posizione sicura da cui toovalidate credenziali.</span><span class="sxs-lookup"><span data-stu-id="a6929-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="a6929-118">Queste applicazioni sono dette **broker**.</span><span class="sxs-lookup"><span data-stu-id="a6929-118">We call these **brokers**.</span></span> <span data-ttu-id="a6929-119">In iOS e Android tali gestori vengono forniti tramite applicazioni scaricabile che i clienti installare in modo indipendente o possono essere inseriti toohello dispositivo da una società che gestisce alcuni o tutti i dispositivi hello per i relativi dipendenti.</span><span class="sxs-lookup"><span data-stu-id="a6929-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="a6929-120">Questi gestori supportano la sicurezza di gestione solo per alcune applicazioni o l'intero dispositivo hello in base a ciò che gli amministratori IT desiderano.</span><span class="sxs-lookup"><span data-stu-id="a6929-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="a6929-121">In Windows, questa funzionalità è fornita dalla selezione account incorporato nel sistema operativo toohello, tecnicamente detto hello Broker di autenticazione Web.</span><span class="sxs-lookup"><span data-stu-id="a6929-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="a6929-122">Per ulteriori informazioni su come vengono utilizzati questi intermediari e come i clienti potrebbero visualizzarli nel flusso di accesso per piattaforma di Microsoft Identity hello leggere.</span><span class="sxs-lookup"><span data-stu-id="a6929-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="a6929-123">Modelli di accesso dai dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="a6929-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="a6929-124">Accesso toocredentials nei dispositivi seguire due modelli di base per la piattaforma di Microsoft Identity hello:</span><span class="sxs-lookup"><span data-stu-id="a6929-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="a6929-125">Accessi non assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="a6929-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="a6929-126">Accessi assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="a6929-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="a6929-127">Accessi non assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="a6929-127">Non-broker assisted logins</span></span>
<span data-ttu-id="a6929-128">Account di accesso non broker assistito sono esperienze di accesso eseguite inline con un'applicazione hello e utilizzano l'archiviazione locale di hello sul dispositivo hello per tale applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="a6929-129">Questa risorsa di archiviazione può essere condivisi tra le applicazioni, ma le credenziali di hello sono strettamente associati toohello app o un gruppo di applicazioni utilizzando credenziali.</span><span class="sxs-lookup"><span data-stu-id="a6929-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="a6929-130">Molto probabile che hai verificato in molte applicazioni per dispositivi mobili quando si immette un nome utente e una password all'interno di un'applicazione hello stesso.</span><span class="sxs-lookup"><span data-stu-id="a6929-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="a6929-131">Questi account hanno hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="a6929-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="a6929-132">Esperienza utente esiste completamente all'interno di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="a6929-133">Le credenziali possono essere condivise tra le applicazioni firmate da hello stesso certificato, che fornisce una suite di tooyour esperienza single sign-on di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a6929-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="a6929-134">Controllo intorno esperienza hello della procedura di accesso viene fornito l'applicazione toohello prima e dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a6929-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="a6929-135">Questi account hanno hello seguenti svantaggi:</span><span class="sxs-lookup"><span data-stu-id="a6929-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="a6929-136">L'utente non può eseguire il Single Sign-On per tutte le app che usano un'identità Microsoft, ma solo per le identità Microsoft configurate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="a6929-137">L'applicazione non può essere utilizzata con funzionalità più avanzate di business, ad esempio l'accesso condizionale o utilizzare hello InTune famiglia di prodotti.</span><span class="sxs-lookup"><span data-stu-id="a6929-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="a6929-138">L'applicazione non supporta l'autenticazione basata su certificati per gli utenti aziendali.</span><span class="sxs-lookup"><span data-stu-id="a6929-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="a6929-139">Ecco una rappresentazione del funzionamento con archiviazione condivisa hello del tooenable applicazioni SSO hello identità SDK:</span><span class="sxs-lookup"><span data-stu-id="a6929-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="a6929-140">Accessi assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="a6929-140">Broker assisted logins</span></span>
<span data-ttu-id="a6929-141">Gli account di accesso assistita da Service Broker sono esperienze di accesso che si verificano all'interno di un'applicazione hello broker e utilizzare hello archiviazione e la protezione delle credenziali di hello broker tooshare a tutte le applicazioni sul dispositivo hello applicabili alla piattaforma di Microsoft Identity hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="a6929-142">Ciò significa che le applicazioni utilizzano hello broker toosign gli utenti.</span><span class="sxs-lookup"><span data-stu-id="a6929-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="a6929-143">In iOS e Android tali gestori vengono forniti tramite applicazioni scaricabile che i clienti installare in modo indipendente o possono essere inseriti toohello dispositivo da una società che gestisce il dispositivo di hello per utente.</span><span class="sxs-lookup"><span data-stu-id="a6929-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="a6929-144">Un esempio di questo tipo di applicazione è un'applicazione Microsoft Authenticator hello in iOS.</span><span class="sxs-lookup"><span data-stu-id="a6929-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="a6929-145">In Windows, questa funzionalità è fornita dalla selezione account incorporato nel sistema operativo toohello, tecnicamente detto hello Broker di autenticazione Web.</span><span class="sxs-lookup"><span data-stu-id="a6929-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="a6929-146">esperienza Hello varia in base alla piattaforma e a volte può risultare problematica toousers se non è gestita correttamente.</span><span class="sxs-lookup"><span data-stu-id="a6929-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="a6929-147">Si è probabilmente più familiarità con questo modello se è installata l'applicazione di Facebook hello e si usa Facebook Connect da un'altra applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="a6929-148">Hello utilizza piattaforma Microsoft Identity hello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="a6929-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="a6929-149">Per iOS in tal modo animazione "transizione" tooa in cui l'applicazione viene inviato background toohello mentre le applicazioni Microsoft Authenticator hello provengono in primo piano toohello per hello utente tooselect account con cui desiderano ricevere toosign con.</span><span class="sxs-lookup"><span data-stu-id="a6929-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="a6929-150">Per Android e Windows account hello selezione viene visualizzato all'interno dell'applicazione dell'utente toohello meno problematica.</span><span class="sxs-lookup"><span data-stu-id="a6929-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="a6929-151">La modalità in cui viene richiamato il broker hello</span><span class="sxs-lookup"><span data-stu-id="a6929-151">How hello broker gets invoked</span></span>
<span data-ttu-id="a6929-152">Se è installato un broker compatibile hello dispositivo come applicazione di Microsoft Authenticator, hello identità SDK hello verrà automaticamente hello lavoro richiamare broker hello automaticamente quando un utente indica che desiderano toolog con qualsiasi account da piattaforma di Microsoft Identity Hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="a6929-153">Potrebbe trattarsi di un account Microsoft personale, di un account aziendale o dell'istituto di istruzione o di un account dato e ospitato in Azure con i prodotti B2C e B2B.</span><span class="sxs-lookup"><span data-stu-id="a6929-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="a6929-154">Come è possibile garantire un'applicazione hello è valido</span><span class="sxs-lookup"><span data-stu-id="a6929-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="a6929-155">identità del Hello necessità tooensure hello di broker di hello chiamata di un'applicazione è fondamentale toohello sicurezza che forniamo nell'account di accesso di Service broker assistito.</span><span class="sxs-lookup"><span data-stu-id="a6929-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="a6929-156">IOS né Android applica gli identificatori univoci che sono validi solo per una determinata applicazione, in modo che applicazioni dannose potrebbero lo "spoofing" identificatore dell'applicazione legittimo e ricevere i token hello destinati a un'applicazione hello legittimi.</span><span class="sxs-lookup"><span data-stu-id="a6929-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="a6929-157">tooensure che Microsoft segnala sempre con un'applicazione hello corretto in fase di esecuzione, chiediamo hello developer tooprovide un redirectURI personalizzato quando si registra l'applicazione con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a6929-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="a6929-158">**Le modalità di creazione dell'URI di reindirizzamento da parte degli sviluppatori vengono trattate in dettaglio di seguito.**</span><span class="sxs-lookup"><span data-stu-id="a6929-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="a6929-159">Questo valore di redirectURI personalizzato contiene hello ID Bundle dell'applicazione hello ed è garantita l'applicazione univoco toohello toobe da hello Apple App Store.</span><span class="sxs-lookup"><span data-stu-id="a6929-159">This custom redirectURI contains hello Bundle ID of hello application and is ensured toobe unique toohello application by hello Apple App Store.</span></span> <span data-ttu-id="a6929-160">Quando un gestore di hello chiamate applicazione broker hello richiede iOS hello tooprovide sistema operativo hello con ID di pacchetto che ha chiamato broker hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-160">When an application calls hello broker, hello broker asks hello iOS operating system tooprovide it with hello Bundle ID that called hello broker.</span></span> <span data-ttu-id="a6929-161">broker Hello fornisce tooMicrosoft questo ID Bundle nel sistema di identità tooour chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-161">hello broker provides this Bundle ID tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="a6929-162">ID Bundle dell'applicazione hello hello non corrisponde a hello che ID Bundle fornito toous dallo sviluppatore hello durante la registrazione, si consentirà l'accesso toohello token per un'applicazione hello risorse hello richiede.</span><span class="sxs-lookup"><span data-stu-id="a6929-162">If hello Bundle ID of hello application does not match hello Bundle ID provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="a6929-163">Tale controllo garantisce che solo un'applicazione hello registrata dallo sviluppatore hello riceve i token.</span><span class="sxs-lookup"><span data-stu-id="a6929-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="a6929-164">**sviluppatore di Hello ha scelta hello del se hello Microsoft Identity SDK chiama broker hello o utilizza hello non broker assistito flusso.**</span><span class="sxs-lookup"><span data-stu-id="a6929-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="a6929-165">Tuttavia se hello scelto non toouse hello assistito broker flusso perdono hello vantaggio derivante dall'utilizzo delle credenziali SSO utente hello potrà avere già aggiunto al dispositivo hello e impedisce loro applicazione in uso con le funzionalità di business Microsoft Fornisce i clienti, ad esempio l'accesso condizionale, funzionalità di gestione di Intune e l'autenticazione basata su certificato.</span><span class="sxs-lookup"><span data-stu-id="a6929-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="a6929-166">Questi account hanno hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="a6929-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="a6929-167">Utente di cui si verifichi SSO per tutte le loro applicazioni indipendentemente dal fornitore hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="a6929-168">L'applicazione può utilizzare funzionalità più avanzate di business, ad esempio l'accesso condizionale o usare hello InTune suite di prodotti.</span><span class="sxs-lookup"><span data-stu-id="a6929-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="a6929-169">L'applicazione può supportare l'autenticazione basata su certificati per gli utenti aziendali.</span><span class="sxs-lookup"><span data-stu-id="a6929-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="a6929-170">Accedi molto più sicuro di riscontrare identità hello dell'applicazione hello e dell'utente hello vengono verificate dall'applicazione di Service broker hello con gli algoritmi di sicurezza aggiuntivo e la crittografia.</span><span class="sxs-lookup"><span data-stu-id="a6929-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="a6929-171">Questi account hanno hello seguenti svantaggi:</span><span class="sxs-lookup"><span data-stu-id="a6929-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="a6929-172">In iOS utente hello viene eseguita la transizione dall'esperienza dell'applicazione mentre si scelgono le credenziali.</span><span class="sxs-lookup"><span data-stu-id="a6929-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="a6929-173">Perdita di account di accesso di hello possibilità toomanage hello esperienza per i clienti all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="a6929-174">Ecco una rappresentazione di come utilizzare Microsoft Identity SDK hello hello broker tooenable applicazioni SSO:</span><span class="sxs-lookup"><span data-stu-id="a6929-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+
```

<span data-ttu-id="a6929-175">Grazie a queste informazioni di base deve essere toobetter in grado di comprendere e implementare SSO all'interno dell'applicazione utilizzando una piattaforma di Microsoft Identity hello e SDK.</span><span class="sxs-lookup"><span data-stu-id="a6929-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="a6929-176">Abilitazione di SSO tra app tramite ADAL</span><span class="sxs-lookup"><span data-stu-id="a6929-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="a6929-177">In questo caso si usa hello ADAL iOS SDK per:</span><span class="sxs-lookup"><span data-stu-id="a6929-177">Here we use hello ADAL iOS SDK to:</span></span>

* <span data-ttu-id="a6929-178">Attivare SSO non assistito da broker per la suite di app</span><span class="sxs-lookup"><span data-stu-id="a6929-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="a6929-179">Attivare il supporto per SSO assistito da broker</span><span class="sxs-lookup"><span data-stu-id="a6929-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="a6929-180">Attivazione dell'SSO per l'SSO non assistito da broker</span><span class="sxs-lookup"><span data-stu-id="a6929-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="a6929-181">Per tutte le applicazioni di accesso non broker SSO assistito hello identità SDK gestisce gran parte delle complessità hello di SSO.</span><span class="sxs-lookup"><span data-stu-id="a6929-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="a6929-182">Ciò include l'individuazione utente hello nella cache di hello e la gestione di un elenco di utenti ha effettuato l'accesso è tooquery.</span><span class="sxs-lookup"><span data-stu-id="a6929-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="a6929-183">tooenable SSO tutte le applicazioni che si è proprietari che è necessario hello toodo seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6929-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="a6929-184">Verificare che tutte le hello di utente le applicazioni stesso Client o applicazione ID.</span><span class="sxs-lookup"><span data-stu-id="a6929-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="a6929-185">Verificare che tutti i hello condivisione applicazioni la stessa firma del certificato di Apple in modo da poter condividere portachiavi</span><span class="sxs-lookup"><span data-stu-id="a6929-185">Ensure that all of your applications share hello same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="a6929-186">Richiesta hello stesso diritto keychain per ognuna delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a6929-186">Request hello same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="a6929-187">Informare hello identità SDK keychain condiviso hello che desideri toouse.</span><span class="sxs-lookup"><span data-stu-id="a6929-187">Tell hello Microsoft Identity SDKs about hello shared keychain you want us toouse.</span></span>

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="a6929-188">Utilizzando lo stesso ID Client di hello / applicazione ID per tutte le applicazioni nel gruppo di applicazioni di hello</span><span class="sxs-lookup"><span data-stu-id="a6929-188">Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="a6929-189">Per consentire tooknow piattaforma di Microsoft Identity hello che ne sia consentita tooshare token tra le applicazioni, ognuna delle applicazioni sarà necessario tooshare hello stesso Client o applicazione ID.</span><span class="sxs-lookup"><span data-stu-id="a6929-189">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="a6929-190">Questo è l'identificatore hello tooyou fornito al momento della prima applicazione è stato registrato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-190">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="a6929-191">Per comprendere come identificare diverse App toohello servizio Microsoft Identity se utilizza hello stesso ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-191">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="a6929-192">risposte Hello sono con hello **Redirect URIs**.</span><span class="sxs-lookup"><span data-stu-id="a6929-192">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="a6929-193">Ogni applicazione può avere più URI di reindirizzamento registrato nel portale di onboarding hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-193">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="a6929-194">Ogni app della suite avrà un URI di reindirizzamento diverso.</span><span class="sxs-lookup"><span data-stu-id="a6929-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="a6929-195">La situazione potrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="a6929-195">An example of how this looks is below:</span></span>

<span data-ttu-id="a6929-196">URI di reindirizzamento dell'app 1: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="a6929-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="a6929-197">URI di reindirizzamento dell'app 2: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="a6929-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="a6929-198">URI di reindirizzamento dell'app 3: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="a6929-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="a6929-199">....</span><span class="sxs-lookup"><span data-stu-id="a6929-199">....</span></span>

<span data-ttu-id="a6929-200">Questi vengono nidificati sotto lo stesso ID client hello / ID dell'applicazione e ricercata hello in base a URI è restituire toous nella configurazione del SDK di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="a6929-200">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="a6929-201">*Si noti che hello formato degli URI di reindirizzamento vengono spiegate di seguito. È possibile utilizzare qualsiasi URI di reindirizzamento a meno che non si desidera broker hello toosupport, nel qual caso è necessario simile hello precedente*</span><span class="sxs-lookup"><span data-stu-id="a6929-201">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="a6929-202">Creare la condivisione dei portachiavi tra le applicazioni</span><span class="sxs-lookup"><span data-stu-id="a6929-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="a6929-203">Abilitazione della condivisione di portachiavi esula hello in questo documento e coperto da Apple nel proprio documento [aggiunta di funzionalità](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span><span class="sxs-lookup"><span data-stu-id="a6929-203">Enabling keychain sharing is beyond hello scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="a6929-204">È importante soprattutto di stabilire il toobe portachiavi chiamato desiderato e aggiungere tale funzionalità in tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a6929-204">What is important is that you decide what you want your keychain toobe called and add that capability across all your applications.</span></span>

<span data-ttu-id="a6929-205">Quando si dispone dei diritti impostare correttamente la dovrebbe essere un file nella directory del progetto intitolata `entitlements.plist` che contiene un elemento che sembra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6929-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like hello following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="a6929-206">Dopo aver diritto portachiavi hello abilitato in ognuna delle applicazioni e si è pronti toouse SSO, informare hello Microsoft Identity SDK portachiavi utilizzando hello impostazione in seguito il `ADAuthenticationSettings` con hello seguente impostazione:</span><span class="sxs-lookup"><span data-stu-id="a6929-206">Once you have hello keychain entitlement enabled in each of your applications, and you are ready toouse SSO, tell hello Microsoft Identity SDK about your keychain by using hello following setting in your `ADAuthenticationSettings` with hello following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="a6929-207">Quando si condivide un portachiavi tra le applicazioni qualsiasi applicazione può eliminare utenti o peggio eliminare tutti i token hello in tutta l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-207">When you share a keychain across your applications any application can delete users or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="a6929-208">Questo è particolarmente disastroso se si hanno applicazioni che si basano su hello token toodo operazioni in background.</span><span class="sxs-lookup"><span data-stu-id="a6929-208">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="a6929-209">La condivisione a un portachiavi significa che è necessario prestare particolare attenzione in tutte le rimuove operazioni tramite hello identità SDK.</span><span class="sxs-lookup"><span data-stu-id="a6929-209">Sharing a keychain means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="a6929-210">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="a6929-210">That's it!</span></span> <span data-ttu-id="a6929-211">Hello Microsoft Identity SDK ora condividono le credenziali in tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a6929-211">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="a6929-212">elenco di utenti Hello verrà inoltre essere condivisi tra le istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-212">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="a6929-213">Attivazione di SSO per SSO assistito da broker</span><span class="sxs-lookup"><span data-stu-id="a6929-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="a6929-214">consente a un'applicazione di toouse qualsiasi broker da cui è installato nel dispositivo hello è Hello **disattivata per impostazione predefinita**.</span><span class="sxs-lookup"><span data-stu-id="a6929-214">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="a6929-215">Ordinare toouse l'applicazione con broker hello è necessario apportare alcune modifiche alla configurazione e aggiungere un'applicazione tooyour di codice.</span><span class="sxs-lookup"><span data-stu-id="a6929-215">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="a6929-216">Hello passaggi toofollow sono:</span><span class="sxs-lookup"><span data-stu-id="a6929-216">hello steps toofollow are:</span></span>

1. <span data-ttu-id="a6929-217">Abilitare la modalità di Service broker in toohello di chiamata del codice dell'applicazione SDK MS.</span><span class="sxs-lookup"><span data-stu-id="a6929-217">Enable broker mode in your application code's call toohello MS SDK.</span></span>
2. <span data-ttu-id="a6929-218">Stabilire un nuovo URI di reindirizzamento e fornire tooboth hello app e la registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a6929-218">Establish a new redirect URI and provide that tooboth hello app and your app registration.</span></span>
3. <span data-ttu-id="a6929-219">Registrazione di uno schema URL.</span><span class="sxs-lookup"><span data-stu-id="a6929-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="a6929-220">Supporto iOS9: aggiungere un file Info. plist tooyour di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-220">iOS9 Support: Add a permission tooyour info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="a6929-221">Passaggio 1: Abilitare la modalità broker nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a6929-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="a6929-222">possibilità di Hello per il broker di hello toouse applicazione è attivata quando si crea la configurazione iniziale dell'oggetto di autenticazione o contesto"hello".</span><span class="sxs-lookup"><span data-stu-id="a6929-222">hello ability for your application toouse hello broker is turned on when you create hello "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="a6929-223">A tal fine, impostare il tipo delle credenziali nel codice:</span><span class="sxs-lookup"><span data-stu-id="a6929-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="a6929-224">Hello `AD_CREDENTIALS_AUTO` impostazione consentirà hello Microsoft Identity SDK tootry toocall out broker toohello, `AD_CREDENTIALS_EMBEDDED` impedirà hello Microsoft Identity SDK dalla chiamata toohello broker.</span><span class="sxs-lookup"><span data-stu-id="a6929-224">hello `AD_CREDENTIALS_AUTO` setting will allow hello Microsoft Identity SDK tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` will prevent hello Microsoft Identity SDK from calling toohello broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="a6929-225">Passaggio 2: Registrazione di uno schema URL</span><span class="sxs-lookup"><span data-stu-id="a6929-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="a6929-226">piattaforma di Microsoft Identity Hello Usa broker hello tooinvoke di URL e dell'applicazione tooyour indietro quindi la restituzione di controllo.</span><span class="sxs-lookup"><span data-stu-id="a6929-226">hello Microsoft Identity platform uses URLs tooinvoke hello broker and then return control back tooyour application.</span></span> <span data-ttu-id="a6929-227">toofinish di andata e ritorno è necessario uno schema URL registrato per l'applicazione che hello Microsoft Identity conoscenza della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="a6929-227">toofinish that round trip you need a URL scheme registered for your application that hello Microsoft Identity platform will know about.</span></span> <span data-ttu-id="a6929-228">Questo può essere inoltre tooany altri schemi app potrebbe aver precedentemente registrato con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-228">This can be in addition tooany other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="a6929-229">È consigliabile apportare hello URL schema toominimize piuttosto univoco hello possibilità che un'altra app hello utilizzando lo stesso schema dell'URL.</span><span class="sxs-lookup"><span data-stu-id="a6929-229">We recommend making hello URL scheme fairly unique toominimize hello chances of another app using hello same URL scheme.</span></span> <span data-ttu-id="a6929-230">Apple non garantisce l'univocità hello degli schemi di URL registrati nell'archivio di app hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-230">Apple does not enforce hello uniqueness of URL schemes that are registered in hello app store.</span></span>
> 
> 

<span data-ttu-id="a6929-231">Ecco un esempio di come appare nella configurazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="a6929-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="a6929-232">È anche possibile usare XCode:</span><span class="sxs-lookup"><span data-stu-id="a6929-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="a6929-233">Passaggio 3: Stabilire un nuovo URI di reindirizzamento con lo schema URL</span><span class="sxs-lookup"><span data-stu-id="a6929-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="a6929-234">In ordine tooensure che è sempre restituire credenziali hello token toohello corretta applicazione, è necessario toomake che è richiamata tooyour applicazione in modo da hello del sistema operativo iOS è possibile verificare.</span><span class="sxs-lookup"><span data-stu-id="a6929-234">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello iOS operating system can verify.</span></span> <span data-ttu-id="a6929-235">applicazioni di Service broker di Hello iOS del sistema operativo report toohello Microsoft hello ID Bundle dell'applicazione hello chiamata.</span><span class="sxs-lookup"><span data-stu-id="a6929-235">hello iOS operating system reports toohello Microsoft broker applications hello Bundle ID of hello application calling it.</span></span> <span data-ttu-id="a6929-236">di cui un'applicazione non autorizzata non può effettuare lo spoofing.</span><span class="sxs-lookup"><span data-stu-id="a6929-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="a6929-237">Pertanto, è usato insieme a hello URI del nostro tooensure applicazione Service broker token hello vengono restituiti toohello corretta applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-237">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="a6929-238">È necessario è tooestablish questo reindirizzamento univoco sia nell'applicazione e set URI come URI di reindirizzamento nel nostro portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="a6929-238">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="a6929-239">L'URI di reindirizzamento deve essere nel formato corretto di hello di:</span><span class="sxs-lookup"><span data-stu-id="a6929-239">Your redirect URI must be in hello proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="a6929-240">Ad esempio: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="a6929-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="a6929-241">Questo URI di reindirizzamento deve toobe specificato con la registrazione di app utilizzando hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a6929-241">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="a6929-242">Per altre informazioni sulla registrazione di app Azure AD, vedere [Integrazione con Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="a6929-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a><span data-ttu-id="a6929-243">Passaggio 3a: aggiungere un URI di reindirizzamento nell'autenticazione basata su certificati di portale toosupport app e sviluppo</span><span class="sxs-lookup"><span data-stu-id="a6929-243">Step 3a: Add a redirect URI in your app and dev portal toosupport certificate based authentication</span></span>
<span data-ttu-id="a6929-244">autenticazione basata sul certificato toosupport secondo "msauth" deve toobe registrato nell'applicazione e hello [portale di Azure](https://portal.azure.com/) toohandle l'autenticazione del certificato se lo si desidera tooadd che supportano l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6929-244">toosupport cert based authentication a second "msauth"  needs toobe registered in your application and hello [Azure portal](https://portal.azure.com/) toohandle certificate authentication if you wish tooadd that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="a6929-245">Ad esempio: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="a6929-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a><span data-ttu-id="a6929-246">Passaggio 4: iOS9: aggiungere un'app tooyour parametro di configurazione</span><span class="sxs-lookup"><span data-stu-id="a6929-246">Step 4: iOS9: Add a configuration parameter tooyour app</span></span>
<span data-ttu-id="a6929-247">Libreria ADAL Usa – canOpenURL: toocheck se broker hello è installato nel dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a6929-247">ADAL uses –canOpenURL: toocheck if hello broker is installed on hello device.</span></span> <span data-ttu-id="a6929-248">In iOS 9 Apple ha bloccato gli schemi di cui un'applicazione può effettuare una query.</span><span class="sxs-lookup"><span data-stu-id="a6929-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="a6929-249">Sarà necessario tooadd "msauth" toohello LSApplicationQueriesSchemes sezione il `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="a6929-249">You will need tooadd “msauth” toohello LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="a6929-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="a6929-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="a6929-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="a6929-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="a6929-252">L'SSO è stato configurato!</span><span class="sxs-lookup"><span data-stu-id="a6929-252">You've configured SSO!</span></span>
<span data-ttu-id="a6929-253">Ora hello SDK identità Microsoft verrà automaticamente sia condivide le credenziali tra le applicazioni e richiamare broker hello se è presente sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a6929-253">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

