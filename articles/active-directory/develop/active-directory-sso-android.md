---
title: Come abilitare l'accesso Single Sign-On tra app su Android tramite ADAL | Documentazione Microsoft
description: "Come utilizzare le funzionalità dell'SDK ADAL per abilitare il Single Sign-On tra le applicazioni. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 9c7e959530a836fe5ddf74708363a636c39b3cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="2f8bd-103">Come abilitare l'accesso Single Sign-On tra app su Android tramite ADAL</span><span class="sxs-lookup"><span data-stu-id="2f8bd-103">How to enable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="2f8bd-104">Ora i clienti si aspettano che l'accesso SSO (Single Sign-On) venga fornito in modo che gli utenti debbano inserire le loro credenziali una volta sola e che le credenziali valgano automaticamente per le varie applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="2f8bd-105">La difficoltà di immissione di nome utente e password su uno schermo di piccole dimensioni, spesso abbinata a un fattore aggiuntivo (2FA) come una telefonata o un codice inviato tramite SMS, rende l'utente insoddisfatto se questa procedura va ripetuta più volte per il prodotto.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="2f8bd-106">Inoltre, se si applica una piattaforma delle identità che può essere usata da altre applicazioni, ad esempio Microsoft Accounts o un account aziendale di Office365, i clienti si aspettano che le credenziali siano disponibili all'uso in tutte le applicazioni, indipendentemente dal fornitore.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="2f8bd-107">La piattaforma Microsoft Identity, insieme agli altri SDK di Microsoft Identity, soddisfa queste aspettative e consente di offrire l'SSO ai clienti nella propria suite di applicazioni oppure, analogamente alla funzionalità broker e alle applicazioni di Authenticator, in tutto il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="2f8bd-108">Questa procedura illustrerà come configurare l'SDK all'interno dell'applicazione per offrire questo vantaggio ai clienti.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="2f8bd-109">Questa procedura si applica a:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="2f8bd-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f8bd-110">Azure Active Directory</span></span>
* <span data-ttu-id="2f8bd-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="2f8bd-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="2f8bd-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="2f8bd-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="2f8bd-113">Accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f8bd-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="2f8bd-114">Il documento precedente presuppone che si sappia come effettuare il [provisioning delle applicazioni nel portale legacy per Azure Active Directory](active-directory-how-to-integrate.md) e che l'applicazione sia stata integrata con [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="2f8bd-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="2f8bd-115">Concetti di SSO nella piattaforma Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="2f8bd-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="2f8bd-116">Broker di Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="2f8bd-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="2f8bd-117">Microsoft offre applicazioni per ogni piattaforma per dispositivi mobili che consentono il bridging delle credenziali tra le applicazioni di fornitori diversi e offre particolari funzionalità avanzate che richiedono un'unica posizione sicura da cui convalidare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="2f8bd-118">Queste applicazioni sono dette **broker**.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-118">We call these **brokers**.</span></span> <span data-ttu-id="2f8bd-119">Nei sistemi iOS e Android i broker sono forniti tramite applicazioni scaricabili che i clienti possono installare in modo indipendente oppure possono essere inviati al dispositivo da una società che gestisce alcuni o tutti i dispositivi dei suoi dipendenti.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="2f8bd-120">I broker supportano la gestione della sicurezza per alcune applicazioni soltanto o per tutto il dispositivo, a seconda di quanto stabilito dagli amministratori IT.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="2f8bd-121">In Windows questa funzionalità è fornita da un sistema di selezione dell'account incorporato nel sistema operativo, il cui nome tecnico è Web Authentication Broker.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="2f8bd-122">Per altre informazioni su come vengono usati questi broker e come vengono visualizzati dai clienti nel flusso di accesso per la piattaforma Microsoft Identity, continuare a leggere.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="2f8bd-123">Modelli di accesso dai dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="2f8bd-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="2f8bd-124">Nella piattaforma Microsoft Identity l'accesso alle credenziali nei dispositivi avviene in base a due modelli:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="2f8bd-125">Accessi non assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="2f8bd-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="2f8bd-126">Accessi assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="2f8bd-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="2f8bd-127">Accessi non assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="2f8bd-127">Non-broker assisted logins</span></span>
<span data-ttu-id="2f8bd-128">Gli accessi non assistiti da broker sono esperienze di accesso in linea con l'applicazione e utilizzano le risorse di archiviazione locali nel dispositivo per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="2f8bd-129">Le risorse di archiviazione possono essere condivise tra le applicazioni, ma le credenziali sono strettamente associate all'applicazione oppure a suite di applicazioni che usano le credenziali.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="2f8bd-130">Questa è l'esperienza più frequente in molte applicazioni per dispositivi mobili in cui si immettono un nome utente e una password all'interno dell'applicazione stessa.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="2f8bd-131">Questi tipi di accessi offrono i seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="2f8bd-132">L'esperienza utente si svolge interamente all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="2f8bd-133">Le credenziali possono essere condivise tra applicazioni firmate dallo stesso certificato, offrendo un'esperienza di Single Sign-On alla suite di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="2f8bd-134">Il controllo dell'esperienza di accesso viene fornito all'applicazione prima e dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="2f8bd-135">Questi tipi di accessi presentano i seguenti svantaggi:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="2f8bd-136">L'utente non può eseguire il Single Sign-On per tutte le app che usano un'identità Microsoft, ma solo per le identità Microsoft configurate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="2f8bd-137">L'applicazione non può essere usata con funzionalità aziendali più avanzate, ad esempio l'Accesso condizionale o la suite di prodotti InTune.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="2f8bd-138">L'applicazione non supporta l'autenticazione basata su certificati per gli utenti aziendali.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="2f8bd-139">Di seguito viene illustrato il funzionamento degli SDK di Microsoft Identity con risorse di archiviazione condivise delle applicazioni per abilitare l'SSO:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="2f8bd-140">Accessi assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="2f8bd-140">Broker assisted logins</span></span>
<span data-ttu-id="2f8bd-141">Gli accessi assistiti da broker sono esperienze di accesso che si svolgono all'interno dell'applicazione broker e usano le risorse di archiviazione e la sicurezza del broker per condividere le credenziali tra tutte le applicazioni sul dispositivo che applicano la piattaforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="2f8bd-142">Ciò significa che le applicazioni si affidano al broker per l'accesso degli utenti.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="2f8bd-143">Nei sistemi iOS e Android i broker sono inseriti tramite applicazioni scaricabili che i clienti possono installare in modo indipendente oppure possono essere inviati al dispositivo da una società che gestisce il dispositivo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="2f8bd-144">Un esempio di questo tipo di applicazione è l'applicazione Microsoft Authenticator per iOS.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="2f8bd-145">In Windows questa funzionalità è fornita da un sistema di selezione dell'account incorporato nel sistema operativo, il cui nome tecnico è Web Authentication Broker.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="2f8bd-146">L'esperienza varia in base alla piattaforma e talvolta può essere un elemento di disturbo per gli utenti se non viene gestita correttamente.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="2f8bd-147">Chi ha installato l'applicazione Facebook e usa la funzionalità di connessione di Facebook in un'altra applicazione avrà probabilmente maggiore dimestichezza con questo modello.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="2f8bd-148">La piattaforma Microsoft Identity usa lo stesso modello.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="2f8bd-149">Nel sistema operativo iOS questo genera un'animazione di "transizione" in cui l'applicazione viene inviata sullo sfondo mentre le applicazioni di Microsoft Authenticator vengono portate in primo piano in modo che l'utente possa scegliere con quale account accedere.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="2f8bd-150">Nei sistemi Android e Windows la selezione degli account viene visualizzata in alto nell'applicazione, con un impatto meno fastidioso per l'utente.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="2f8bd-151">Come viene richiamato il broker</span><span class="sxs-lookup"><span data-stu-id="2f8bd-151">How the broker gets invoked</span></span>
<span data-ttu-id="2f8bd-152">Se nel dispositivo è installato un broker compatibile, ad esempio l'applicazione Microsoft Authenticator, gli SDK di Microsoft Identity richiamano automaticamente il broker quando un utente indica che vuole accedere con un account della piattaforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="2f8bd-153">Potrebbe trattarsi di un account Microsoft personale, di un account aziendale o dell'istituto di istruzione o di un account dato e ospitato in Azure con i prodotti B2C e B2B.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="2f8bd-154">Come si garantisce la validità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="2f8bd-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="2f8bd-155">La necessità di verificare l'identità di una chiamata di applicazione al broker è fondamentale per la sicurezza garantita con l'accesso assistito da broker.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="2f8bd-156">Né IOS né Android applicano identificatori univoci che sono validi solo per una determinata applicazione, cosicché le applicazioni dannose possono effettuare lo "spoofing" di un identificatore dell'applicazione legittimo e ricevere i token per l'applicazione legittima.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="2f8bd-157">Per garantire sempre la comunicazione con l'applicazione corretta in fase di esecuzione, chiediamo agli sviluppatori di assicurare un URI di reindirizzamento personalizzato al momento della registrazione dell'applicazione con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="2f8bd-158">**Le modalità di creazione dell'URI di reindirizzamento da parte degli sviluppatori vengono trattate in dettaglio di seguito.**</span><span class="sxs-lookup"><span data-stu-id="2f8bd-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="2f8bd-159">Questo URI di reindirizzamento personalizzato contiene l'identificazione personale del certificato dell'applicazione e Google Play Store ne garantisce l'univocità per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span></span> <span data-ttu-id="2f8bd-160">Quando un'applicazione chiama il broker, questo richiede al sistema operativo Android per fornire l'identificazione personale del certificato che ha chiamato il broker.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span></span> <span data-ttu-id="2f8bd-161">Il broker offre questa identificazione personale del certificato a Microsoft nella chiamata al sistema di identità.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="2f8bd-162">Se l'identificazione personale del certificato dell'applicazione non corrisponde all'identificazione personale del certificato offerto dallo sviluppatore durante la registrazione, verrà negato l'accesso ai token per la risorsa richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="2f8bd-163">Tale controllo garantisce che solo l'applicazione registrata dallo sviluppatore riceva i token.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="2f8bd-164">**Lo sviluppatore può scegliere se Microsoft Identity SDK deve chiamare il broker o usare il flusso non assistito dal broker.**</span><span class="sxs-lookup"><span data-stu-id="2f8bd-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="2f8bd-165">Se lo sviluppatore decide di non usare il flusso assistito dal broker, rinuncia al vantaggio dell'uso delle credenziali SSO che l'utente potrebbe avere già aggiunto nel dispositivo e impedisce di usare l'applicazione con le funzionalità aziendali offerte da Microsoft, ad esempio l'Accesso condizionale, le funzionalità di gestione di Intune e l'autenticazione basata su certificati.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="2f8bd-166">Questi tipi di accessi offrono i seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="2f8bd-167">L'utente usufruisce del Single Sign-On per tutte le proprie applicazioni, indipendentemente dal fornitore.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="2f8bd-168">L'applicazione può usare funzionalità aziendali più avanzate, ad esempio l'Accesso condizionale o la suite di prodotti InTune.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="2f8bd-169">L'applicazione può supportare l'autenticazione basata su certificati per gli utenti aziendali.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="2f8bd-170">Un'esperienza di accesso molto più sicura dato che l'identità dell'applicazione e l'utente vengono verificati dall'applicazione broker con algoritmi di sicurezza aggiuntivi e la crittografia.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="2f8bd-171">Questi tipi di accessi presentano i seguenti svantaggi:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="2f8bd-172">Nel sistema iOS l'utente viene trasferito dall'esperienza dell'applicazione durante la selezione delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="2f8bd-173">Perdita della possibilità di gestire l'esperienza di accesso per i clienti nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="2f8bd-174">Di seguito viene rappresentato il funzionamento degli SDK di Microsoft Identity con le applicazioni broker per abilitare l'SSO:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
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

<span data-ttu-id="2f8bd-175">Sulla base di queste informazioni di base dovrebbe essere possibile comprendere meglio e implementare l'SSO all'interno dell'applicazione con la piattaforma e gli SDK di Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="2f8bd-176">Abilitazione di SSO tra app tramite ADAL</span><span class="sxs-lookup"><span data-stu-id="2f8bd-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="2f8bd-177">In questo esempio si usa l'SDK ADAL Android per:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-177">Here we use the ADAL Android SDK to:</span></span>

* <span data-ttu-id="2f8bd-178">Attivare SSO non assistito da broker per la suite di app</span><span class="sxs-lookup"><span data-stu-id="2f8bd-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="2f8bd-179">Attivare il supporto per SSO assistito da broker</span><span class="sxs-lookup"><span data-stu-id="2f8bd-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="2f8bd-180">Attivazione dell'SSO per l'SSO non assistito da broker</span><span class="sxs-lookup"><span data-stu-id="2f8bd-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="2f8bd-181">Per l'SSO non assistito da broker tra applicazioni, gli SDK di Microsoft Identity risolvono automaticamente gran parte delle complessità dell'SSO,</span><span class="sxs-lookup"><span data-stu-id="2f8bd-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="2f8bd-182">tra cui la ricerca dell'utente corretto nella cache e la gestione di un elenco di utenti connessi di cui è possibile effettuare una query.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="2f8bd-183">Per abilitare l'SSO tra le applicazioni di cui si è proprietari, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="2f8bd-184">Verificare che tutte le applicazioni usino lo stesso ID client o ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="2f8bd-185">Verificare che tutte le applicazioni abbiano lo stesso set di SharedUserID.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-185">Ensure all your applications have the same SharedUserID set.</span></span>
3. <span data-ttu-id="2f8bd-186">Verificare che tutte le applicazioni condividano lo stesso certificato di firma da Google Play Store per condividere l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="2f8bd-187">Passaggio 1: Utilizzo dello stesso ID client / ID applicazione per tutte le applicazioni della suite di applicazioni</span><span class="sxs-lookup"><span data-stu-id="2f8bd-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="2f8bd-188">Per comunicare alla piattaforma Microsoft Identity che è consentita la condivisione dei token tra le applicazioni, ciascuna delle applicazioni dovrà condividere lo stesso ID client o ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="2f8bd-189">Si tratta dell'identificatore univoco fornito al momento della registrazione della prima applicazione nel portale.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="2f8bd-190">Ci si potrebbe chiedere come si fa a identificare le varie applicazioni nel servizio di gestione delle identità Microsoft se tutte utilizzano lo stesso ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="2f8bd-191">La risposta sono gli **URI di reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-191">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="2f8bd-192">Ogni applicazione può avere più URI di reindirizzamento registrati nel portale di caricamento.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="2f8bd-193">Ogni app della suite avrà un URI di reindirizzamento diverso.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="2f8bd-194">La situazione potrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-194">An example of how this looks is below:</span></span>

<span data-ttu-id="2f8bd-195">URI di reindirizzamento dell'app 1: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="2f8bd-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="2f8bd-196">URI di reindirizzamento dell'app 2: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="2f8bd-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="2f8bd-197">URI di reindirizzamento dell'app 3: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="2f8bd-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="2f8bd-198">....</span><span class="sxs-lookup"><span data-stu-id="2f8bd-198">....</span></span>

<span data-ttu-id="2f8bd-199">Gli URI vengono nidificati sotto lo stesso ID client / ID applicazione e cercati in base all'URI di reindirizzamento restituito nella configurazione dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

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


<span data-ttu-id="2f8bd-200">*Il formato degli URI di reindirizzamento viene illustrato di seguito. È possibile utilizzare qualsiasi URI di reindirizzamento ad eccezione del caso in cui si desideri supportare il broker, nel qual caso gli URI di reindirizzamento devono essere simili ai precedenti*</span><span class="sxs-lookup"><span data-stu-id="2f8bd-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="2f8bd-201">Passaggio 2: Configurazione dell'archiviazione condivisa in Android</span><span class="sxs-lookup"><span data-stu-id="2f8bd-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="2f8bd-202">L'impostazione di `SharedUserID` esula dal contesto di questo documento, ma per maggiori informazioni si può leggere la documentazione di Google Android su [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="2f8bd-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="2f8bd-203">È importante decidere il nome di sharedUserID e usarlo in tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="2f8bd-204">Dopo aver creato l'attributo `SharedUserID` in tutte le applicazioni, si può usare SSO.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="2f8bd-205">Quando si condivide una risorsa di archiviazione tra le applicazioni, qualsiasi applicazione può eliminare utenti o peggio ancora eliminare tutti i token dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span></span> <span data-ttu-id="2f8bd-206">Questo può essere un problema grave se sono presenti applicazioni che usano i token per svolgere operazioni in background.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="2f8bd-207">La condivisione della risorsa di archiviazione implica che è necessario prestare grande attenzione durante tutte le operazioni di eliminazione tramite gli SDK di Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="2f8bd-208">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-208">That's it!</span></span> <span data-ttu-id="2f8bd-209">L'SDK di Microsoft Identity condividerà le credenziali tra tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-209">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="2f8bd-210">Anche l'elenco degli utenti verrà condiviso tra le istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-210">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="2f8bd-211">Attivazione di SSO per SSO assistito da broker</span><span class="sxs-lookup"><span data-stu-id="2f8bd-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="2f8bd-212">La possibilità per un'applicazione di usare qualsiasi broker installato nel dispositivo è **disattivata per impostazione predefinita**.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="2f8bd-213">Per usare l'applicazione con il broker è necessario apportare alcune modifiche alla configurazione e aggiungere una parte di codice all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="2f8bd-214">Ecco i passaggi da seguire:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-214">The steps to follow are:</span></span>

1. <span data-ttu-id="2f8bd-215">Abilitare la modalità broker nella chiamata del codice dell'applicazione dell'SDK MS</span><span class="sxs-lookup"><span data-stu-id="2f8bd-215">Enable broker mode in your application code's call to the MS SDK</span></span>
2. <span data-ttu-id="2f8bd-216">Definire un nuovo URI di reindirizzamento e indicarlo sia all'app che alla registrazione dell'app</span><span class="sxs-lookup"><span data-stu-id="2f8bd-216">Establish a new redirect URI and provide that to both the app and your app registration</span></span>
3. <span data-ttu-id="2f8bd-217">Impostazione delle autorizzazioni corrette nel manifesto Android</span><span class="sxs-lookup"><span data-stu-id="2f8bd-217">Setting up the correct permissions in the Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="2f8bd-218">Passaggio 1: Abilitare la modalità broker nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="2f8bd-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="2f8bd-219">La capacità dell'applicazione di usare il broker è attivata quando si creano le "impostazioni" o la configurazione iniziale dell'istanza di Authentication.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="2f8bd-220">A tal fine, impostare il tipo ApplicationSettings nel codice:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="2f8bd-221">Passaggio 2: Creare un nuovo URI di reindirizzamento con lo schema dell'URL</span><span class="sxs-lookup"><span data-stu-id="2f8bd-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="2f8bd-222">Per fare in modo che i token delle credenziali vengano sempre restituiti all'applicazione corretta, è necessario assicurarsi che il richiamo dell'applicazione avvenga in un modo verificabile dal sistema operativo Android.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span></span> <span data-ttu-id="2f8bd-223">Il sistema operativo Android utilizza in Google Play Store l'hash del certificato,</span><span class="sxs-lookup"><span data-stu-id="2f8bd-223">The Android operating system uses the hash of the certificate in the Google Play store.</span></span> <span data-ttu-id="2f8bd-224">che non può essere contraffatto da un'applicazione non autorizzata.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="2f8bd-225">Di conseguenza, l'hash del certificato viene usato insieme all'URI dell'applicazione broker per garantire che i token vengano restituiti all'applicazione corretta.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="2f8bd-226">È necessario definire questo URI di reindirizzamento univoco nell'applicazione e impostarlo come URI di reindirizzamento nel portale per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="2f8bd-227">L'URI di reindirizzamento deve essere nel formato corretto:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-227">Your redirect URI must be in the proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="2f8bd-228">Ad esempio: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="2f8bd-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="2f8bd-229">L'URI di reindirizzamento deve essere specificato nella registrazione dell'app tramite il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2f8bd-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="2f8bd-230">Per altre informazioni sulla registrazione di app Azure AD, vedere [Integrazione con Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="2f8bd-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-the-correct-permissions-in-your-application"></a><span data-ttu-id="2f8bd-231">Passaggio 3: Impostare le autorizzazioni corrette all'interno dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="2f8bd-231">Step 3: Set up the correct permissions in your application</span></span>
<span data-ttu-id="2f8bd-232">L'applicazione broker in Android usa la funzionalità AccountManager del sistema operativo Android per gestire le credenziali nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span></span> <span data-ttu-id="2f8bd-233">Per utilizzare il broker in Android, il manifesto dell'app deve disporre delle autorizzazioni per usare gli account di AccountManager.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span></span> <span data-ttu-id="2f8bd-234">Questo argomento viene discusso in modo dettagliato nella [documentazione di Google relativa ad AccountManager qui](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="2f8bd-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="2f8bd-235">In particolare, le autorizzazioni sono:</span><span class="sxs-lookup"><span data-stu-id="2f8bd-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="2f8bd-236">L'SSO è stato configurato!</span><span class="sxs-lookup"><span data-stu-id="2f8bd-236">You've configured SSO!</span></span>
<span data-ttu-id="2f8bd-237">Ora Microsoft Identity SDK condividerà automaticamente le credenziali tra le applicazioni e richiamerà il broker, se presente nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2f8bd-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

