---
title: Come abilitare l'accesso Single Sign-On tra app in iOS usando ADAL | Microsoft Docs
description: "Come utilizzare le funzionalità dell'SDK ADAL per abilitare il Single Sign-On tra le applicazioni. "
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
ms.openlocfilehash: 73b8ed7e6a153a0790f7eae9bd51bb2e554ae72e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="679e3-103">Come abilitare l'accesso Single Sign-On tra app in iOS usando ADAL</span><span class="sxs-lookup"><span data-stu-id="679e3-103">How to enable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="679e3-104">Ora i clienti si aspettano che l'accesso SSO (Single Sign-On) venga fornito in modo che gli utenti debbano inserire le loro credenziali una volta sola e che le credenziali funzionino automaticamente per le varie applicazioni.</span><span class="sxs-lookup"><span data-stu-id="679e3-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="679e3-105">La difficoltà di immissione di nome utente e password su uno schermo di piccole dimensioni, spesso abbinata a un fattore aggiuntivo (2FA) come una telefonata o un codice inviato tramite SMS, rende l'utente insoddisfatto se questa procedura va ripetuta più volte per il prodotto.</span><span class="sxs-lookup"><span data-stu-id="679e3-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="679e3-106">Inoltre, se si applica una piattaforma delle identità che può essere usata da altre applicazioni, ad esempio Microsoft Accounts o un account aziendale di Office365, i clienti si aspettano che le credenziali siano disponibili all'uso in tutte le applicazioni, indipendentemente dal fornitore.</span><span class="sxs-lookup"><span data-stu-id="679e3-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="679e3-107">La piattaforma Microsoft Identity, insieme agli altri SDK di Microsoft Identity, soddisfa queste aspettative e consente di offrire l'SSO ai clienti nella propria suite di applicazioni oppure, analogamente alla funzionalità broker e alle applicazioni di Authenticator, in tutto il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="679e3-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="679e3-108">Questa procedura illustrerà come configurare l'SDK all'interno dell'applicazione per offrire questo vantaggio ai clienti.</span><span class="sxs-lookup"><span data-stu-id="679e3-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="679e3-109">Questa procedura si applica a:</span><span class="sxs-lookup"><span data-stu-id="679e3-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="679e3-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="679e3-110">Azure Active Directory</span></span>
* <span data-ttu-id="679e3-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="679e3-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="679e3-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="679e3-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="679e3-113">Accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="679e3-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="679e3-114">Il documento precedente presuppone che si sappia come effettuare il [provisioning delle applicazioni nel portale legacy per Azure Active Directory](active-directory-how-to-integrate.md) e che l'applicazione sia stata integrata con [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="679e3-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="679e3-115">Concetti di SSO nella piattaforma Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="679e3-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="679e3-116">Broker di Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="679e3-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="679e3-117">Microsoft offre applicazioni per ogni piattaforma per dispositivi mobili che consentono il bridging delle credenziali tra le applicazioni di fornitori diversi e offre particolari funzionalità avanzate che richiedono un'unica posizione sicura da cui convalidare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="679e3-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="679e3-118">Queste applicazioni sono dette **broker**.</span><span class="sxs-lookup"><span data-stu-id="679e3-118">We call these **brokers**.</span></span> <span data-ttu-id="679e3-119">Nei sistemi iOS e Android i broker sono forniti tramite applicazioni scaricabili che i clienti possono installare in modo indipendente oppure possono essere inviati al dispositivo da una società che gestisce alcuni o tutti i dispositivi dei suoi dipendenti.</span><span class="sxs-lookup"><span data-stu-id="679e3-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="679e3-120">I broker supportano la gestione della sicurezza per alcune applicazioni soltanto o per tutto il dispositivo, a seconda di quanto stabilito dagli amministratori IT.</span><span class="sxs-lookup"><span data-stu-id="679e3-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="679e3-121">In Windows questa funzionalità è fornita da un sistema di selezione dell'account incorporato nel sistema operativo, il cui nome tecnico è Web Authentication Broker.</span><span class="sxs-lookup"><span data-stu-id="679e3-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="679e3-122">Per altre informazioni su come vengono usati questi broker e come vengono visualizzati dai clienti nel flusso di accesso per la piattaforma Microsoft Identity, continuare a leggere.</span><span class="sxs-lookup"><span data-stu-id="679e3-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="679e3-123">Modelli di accesso dai dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="679e3-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="679e3-124">Nella piattaforma Microsoft Identity l'accesso alle credenziali nei dispositivi avviene in base a due modelli:</span><span class="sxs-lookup"><span data-stu-id="679e3-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="679e3-125">Accessi non assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="679e3-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="679e3-126">Accessi assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="679e3-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="679e3-127">Accessi non assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="679e3-127">Non-broker assisted logins</span></span>
<span data-ttu-id="679e3-128">Gli accessi non assistiti da broker sono esperienze di accesso in linea con l'applicazione e utilizzano le risorse di archiviazione locali nel dispositivo per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="679e3-129">Le risorse di archiviazione possono essere condivise tra le applicazioni, ma le credenziali sono strettamente associate all'applicazione oppure a suite di applicazioni che usano le credenziali.</span><span class="sxs-lookup"><span data-stu-id="679e3-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="679e3-130">Questa è l'esperienza più frequente in molte applicazioni per dispositivi mobili in cui si immettono un nome utente e una password all'interno dell'applicazione stessa.</span><span class="sxs-lookup"><span data-stu-id="679e3-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="679e3-131">Questi tipi di accessi offrono i seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="679e3-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="679e3-132">L'esperienza utente si svolge interamente all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="679e3-133">Le credenziali possono essere condivise tra applicazioni firmate dallo stesso certificato, offrendo un'esperienza di Single Sign-On alla suite di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="679e3-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="679e3-134">Il controllo dell'esperienza di accesso viene fornito all'applicazione prima e dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="679e3-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="679e3-135">Questi tipi di accessi presentano i seguenti svantaggi:</span><span class="sxs-lookup"><span data-stu-id="679e3-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="679e3-136">L'utente non può eseguire il Single Sign-On per tutte le app che usano un'identità Microsoft, ma solo per le identità Microsoft configurate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="679e3-137">L'applicazione non può essere usata con funzionalità aziendali più avanzate, ad esempio l'Accesso condizionale o la suite di prodotti InTune.</span><span class="sxs-lookup"><span data-stu-id="679e3-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="679e3-138">L'applicazione non supporta l'autenticazione basata su certificati per gli utenti aziendali.</span><span class="sxs-lookup"><span data-stu-id="679e3-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="679e3-139">Di seguito viene illustrato il funzionamento degli SDK di Microsoft Identity con risorse di archiviazione condivise delle applicazioni per abilitare l'SSO:</span><span class="sxs-lookup"><span data-stu-id="679e3-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

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

#### <a name="broker-assisted-logins"></a><span data-ttu-id="679e3-140">Accessi assistiti da broker</span><span class="sxs-lookup"><span data-stu-id="679e3-140">Broker assisted logins</span></span>
<span data-ttu-id="679e3-141">Gli accessi assistiti da broker sono esperienze di accesso che si svolgono all'interno dell'applicazione broker e usano le risorse di archiviazione e la sicurezza del broker per condividere le credenziali tra tutte le applicazioni sul dispositivo che applicano la piattaforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="679e3-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="679e3-142">Ciò significa che le applicazioni si affidano al broker per l'accesso degli utenti.</span><span class="sxs-lookup"><span data-stu-id="679e3-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="679e3-143">Nei sistemi iOS e Android i broker sono inseriti tramite applicazioni scaricabili che i clienti possono installare in modo indipendente oppure possono essere inviati al dispositivo da una società che gestisce il dispositivo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="679e3-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="679e3-144">Un esempio di questo tipo di applicazione è l'applicazione Microsoft Authenticator per iOS.</span><span class="sxs-lookup"><span data-stu-id="679e3-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="679e3-145">In Windows questa funzionalità è fornita da un sistema di selezione dell'account incorporato nel sistema operativo, il cui nome tecnico è Web Authentication Broker.</span><span class="sxs-lookup"><span data-stu-id="679e3-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="679e3-146">L'esperienza varia in base alla piattaforma e talvolta può essere un elemento di disturbo per gli utenti se non viene gestita correttamente.</span><span class="sxs-lookup"><span data-stu-id="679e3-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="679e3-147">Chi ha installato l'applicazione Facebook e usa la funzionalità di connessione di Facebook in un'altra applicazione avrà probabilmente maggiore dimestichezza con questo modello.</span><span class="sxs-lookup"><span data-stu-id="679e3-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="679e3-148">La piattaforma Microsoft Identity usa lo stesso modello.</span><span class="sxs-lookup"><span data-stu-id="679e3-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="679e3-149">Nel sistema operativo iOS questo genera un'animazione di "transizione" in cui l'applicazione viene inviata sullo sfondo mentre le applicazioni di Microsoft Authenticator vengono portate in primo piano in modo che l'utente possa scegliere con quale account accedere.</span><span class="sxs-lookup"><span data-stu-id="679e3-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="679e3-150">Nei sistemi Android e Windows la selezione degli account viene visualizzata in alto nell'applicazione, con un impatto meno fastidioso per l'utente.</span><span class="sxs-lookup"><span data-stu-id="679e3-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="679e3-151">Come viene richiamato il broker</span><span class="sxs-lookup"><span data-stu-id="679e3-151">How the broker gets invoked</span></span>
<span data-ttu-id="679e3-152">Se nel dispositivo è installato un broker compatibile, ad esempio l'applicazione Microsoft Authenticator, gli SDK di Microsoft Identity richiamano automaticamente il broker quando un utente indica che vuole accedere con un account della piattaforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="679e3-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="679e3-153">Potrebbe trattarsi di un account Microsoft personale, di un account aziendale o dell'istituto di istruzione o di un account dato e ospitato in Azure con i prodotti B2C e B2B.</span><span class="sxs-lookup"><span data-stu-id="679e3-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="679e3-154">Come si garantisce la validità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="679e3-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="679e3-155">La necessità di verificare l'identità di una chiamata di applicazione al broker è fondamentale per la sicurezza garantita con l'accesso assistito da broker.</span><span class="sxs-lookup"><span data-stu-id="679e3-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="679e3-156">Né IOS né Android applicano identificatori univoci che sono validi solo per una determinata applicazione, cosicché le applicazioni dannose possono effettuare lo "spoofing" di un identificatore dell'applicazione legittimo e ricevere i token per l'applicazione legittima.</span><span class="sxs-lookup"><span data-stu-id="679e3-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="679e3-157">Per garantire sempre la comunicazione con l'applicazione corretta in fase di esecuzione, chiediamo agli sviluppatori di assicurare un URI di reindirizzamento personalizzato al momento della registrazione dell'applicazione con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="679e3-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="679e3-158">**Le modalità di creazione dell'URI di reindirizzamento da parte degli sviluppatori vengono trattate in dettaglio di seguito.**</span><span class="sxs-lookup"><span data-stu-id="679e3-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="679e3-159">Questo URI di reindirizzamento personalizzato contiene l'ID bundle dell'applicazione e Apple App Store ne garantisce l'univocità per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-159">This custom redirectURI contains the Bundle ID of the application and is ensured to be unique to the application by the Apple App Store.</span></span> <span data-ttu-id="679e3-160">Quando un'applicazione chiama il broker, questo richiede al sistema operativo iOS per fornire l'ID bundle che ha chiamato il broker.</span><span class="sxs-lookup"><span data-stu-id="679e3-160">When an application calls the broker, the broker asks the iOS operating system to provide it with the Bundle ID that called the broker.</span></span> <span data-ttu-id="679e3-161">Il broker fornisce questo ID bundle a Microsoft nella chiamata al sistema di identità.</span><span class="sxs-lookup"><span data-stu-id="679e3-161">The broker provides this Bundle ID to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="679e3-162">Se l'ID bundle dell'applicazione non corrisponde all'ID bundle offerto dallo sviluppatore durante la registrazione, verrà negato l'accesso ai token per la risorsa richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-162">If the Bundle ID of the application does not match the Bundle ID provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="679e3-163">Questo controllo garantisce che solo l'applicazione registrata dallo sviluppatore riceva i token.</span><span class="sxs-lookup"><span data-stu-id="679e3-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="679e3-164">**Lo sviluppatore può scegliere se Microsoft Identity SDK deve chiamare il broker o usare il flusso non assistito dal broker.**</span><span class="sxs-lookup"><span data-stu-id="679e3-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="679e3-165">Se lo sviluppatore decide di non usare il flusso assistito dal broker, rinuncia al vantaggio dell'uso delle credenziali SSO che l'utente potrebbe avere già aggiunto nel dispositivo e impedisce di usare l'applicazione con le funzionalità aziendali offerte da Microsoft, ad esempio l'Accesso condizionale, le funzionalità di gestione di Intune e l'autenticazione basata su certificati.</span><span class="sxs-lookup"><span data-stu-id="679e3-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="679e3-166">Questi tipi di accessi offrono i seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="679e3-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="679e3-167">L'utente usufruisce del Single Sign-On per tutte le proprie applicazioni, indipendentemente dal fornitore.</span><span class="sxs-lookup"><span data-stu-id="679e3-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="679e3-168">L'applicazione può usare funzionalità aziendali più avanzate, ad esempio l'Accesso condizionale o la suite di prodotti InTune.</span><span class="sxs-lookup"><span data-stu-id="679e3-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="679e3-169">L'applicazione può supportare l'autenticazione basata su certificati per gli utenti aziendali.</span><span class="sxs-lookup"><span data-stu-id="679e3-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="679e3-170">Un'esperienza di accesso molto più sicura dato che l'identità dell'applicazione e l'utente vengono verificati dall'applicazione broker con algoritmi di sicurezza aggiuntivi e la crittografia.</span><span class="sxs-lookup"><span data-stu-id="679e3-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="679e3-171">Questi tipi di accessi presentano i seguenti svantaggi:</span><span class="sxs-lookup"><span data-stu-id="679e3-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="679e3-172">Nel sistema iOS l'utente viene trasferito dall'esperienza dell'applicazione durante la selezione delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="679e3-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="679e3-173">Perdita della possibilità di gestire l'esperienza di accesso per i clienti nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="679e3-174">Di seguito viene rappresentato il funzionamento degli SDK di Microsoft Identity con le applicazioni broker per abilitare l'SSO:</span><span class="sxs-lookup"><span data-stu-id="679e3-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

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

<span data-ttu-id="679e3-175">Sulla base di queste informazioni di base dovrebbe essere possibile comprendere meglio e implementare l'SSO all'interno dell'applicazione con la piattaforma e gli SDK di Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="679e3-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="679e3-176">Abilitazione di SSO tra app tramite ADAL</span><span class="sxs-lookup"><span data-stu-id="679e3-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="679e3-177">In questo esempio si userà ADAL iOS SDK per:</span><span class="sxs-lookup"><span data-stu-id="679e3-177">Here we use the ADAL iOS SDK to:</span></span>

* <span data-ttu-id="679e3-178">Attivare SSO non assistito da broker per la suite di app</span><span class="sxs-lookup"><span data-stu-id="679e3-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="679e3-179">Attivare il supporto per SSO assistito da broker</span><span class="sxs-lookup"><span data-stu-id="679e3-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="679e3-180">Attivazione dell'SSO per l'SSO non assistito da broker</span><span class="sxs-lookup"><span data-stu-id="679e3-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="679e3-181">Per l'SSO non assistito da broker tra applicazioni, gli SDK di Microsoft Identity risolvono automaticamente gran parte delle complessità dell'SSO,</span><span class="sxs-lookup"><span data-stu-id="679e3-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="679e3-182">tra cui la ricerca dell'utente corretto nella cache e la gestione di un elenco di utenti connessi di cui è possibile effettuare una query.</span><span class="sxs-lookup"><span data-stu-id="679e3-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="679e3-183">Per abilitare l'SSO tra le applicazioni di cui si è proprietari, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="679e3-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="679e3-184">Verificare che tutte le applicazioni usino lo stesso ID client o ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="679e3-185">Verificare che tutte le applicazioni condividano lo stesso certificato di firma di Apple per poter condividere i portachiavi.</span><span class="sxs-lookup"><span data-stu-id="679e3-185">Ensure that all of your applications share the same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="679e3-186">Richiedere lo stesso diritto per i portachiavi per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-186">Request the same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="679e3-187">Indicare agli SDK di Microsoft Identity il portachiavi condiviso da usare.</span><span class="sxs-lookup"><span data-stu-id="679e3-187">Tell the Microsoft Identity SDKs about the shared keychain you want us to use.</span></span>

#### <a name="using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="679e3-188">Uso dello stesso ID client/ID applicazione per tutte le applicazioni della suite di applicazioni</span><span class="sxs-lookup"><span data-stu-id="679e3-188">Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="679e3-189">Per indicare alla piattaforma Microsoft Identity che è consentita la condivisione dei token tra le applicazioni, ogni applicazione dovrà condividere lo stesso ID client o ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-189">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="679e3-190">Si tratta dell'identificatore univoco fornito al momento della registrazione della prima applicazione nel portale.</span><span class="sxs-lookup"><span data-stu-id="679e3-190">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="679e3-191">Ci si potrebbe chiedere come si fa a identificare le varie applicazioni nel servizio di gestione delle identità Microsoft se tutte utilizzano lo stesso ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-191">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="679e3-192">La risposta sono gli **URI di reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="679e3-192">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="679e3-193">Ogni applicazione può avere più URI di reindirizzamento registrati nel portale di caricamento.</span><span class="sxs-lookup"><span data-stu-id="679e3-193">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="679e3-194">Ogni app della suite avrà un URI di reindirizzamento diverso.</span><span class="sxs-lookup"><span data-stu-id="679e3-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="679e3-195">La situazione potrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="679e3-195">An example of how this looks is below:</span></span>

<span data-ttu-id="679e3-196">URI di reindirizzamento dell'app 1: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="679e3-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="679e3-197">URI di reindirizzamento dell'app 2: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="679e3-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="679e3-198">URI di reindirizzamento dell'app 3: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="679e3-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="679e3-199">....</span><span class="sxs-lookup"><span data-stu-id="679e3-199">....</span></span>

<span data-ttu-id="679e3-200">Gli URI vengono nidificati sotto lo stesso ID client / ID applicazione e cercati in base all'URI di reindirizzamento restituito nella configurazione dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="679e3-200">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

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


<span data-ttu-id="679e3-201">*Il formato degli URI di reindirizzamento viene illustrato di seguito. È possibile usare qualsiasi URI di reindirizzamento a meno che non si voglia supportare il broker, nel qual caso deve essere simile ai precedenti*</span><span class="sxs-lookup"><span data-stu-id="679e3-201">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="679e3-202">Creare la condivisione dei portachiavi tra le applicazioni</span><span class="sxs-lookup"><span data-stu-id="679e3-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="679e3-203">L'abilitazione della condivisione dei portachiavi esula dall'ambito di questo documento ed è illustrata da Apple nel documento relativo all' [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html)(Aggiunta di funzionalità).</span><span class="sxs-lookup"><span data-stu-id="679e3-203">Enabling keychain sharing is beyond the scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="679e3-204">È importante decidere quale portachiavi deve essere chiamato e aggiungere tale funzionalità in tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="679e3-204">What is important is that you decide what you want your keychain to be called and add that capability across all your applications.</span></span>

<span data-ttu-id="679e3-205">Una volta configurati correttamente i diritti, nella directory del progetto verrà visualizzato un file denominato `entitlements.plist` il cui contenuto è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="679e3-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like the following:</span></span>

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

<span data-ttu-id="679e3-206">Una volta abilitato il diritto per i portachiavi in ogni applicazione e quando si è pronti a usare SSO, notificare il portachiavi a Microsoft Identity SDK usando l'impostazione seguente in `ADAuthenticationSettings` :</span><span class="sxs-lookup"><span data-stu-id="679e3-206">Once you have the keychain entitlement enabled in each of your applications, and you are ready to use SSO, tell the Microsoft Identity SDK about your keychain by using the following setting in your `ADAuthenticationSettings` with the following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="679e3-207">Quando si condivide un portachiavi tra le applicazioni, qualsiasi applicazione può eliminare utenti o peggio ancora eliminare tutti i token dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-207">When you share a keychain across your applications any application can delete users or worse delete all the tokens across your application.</span></span> <span data-ttu-id="679e3-208">Questo può essere un problema grave se sono presenti applicazioni che usano i token per svolgere operazioni in background.</span><span class="sxs-lookup"><span data-stu-id="679e3-208">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="679e3-209">La condivisione di un portachiavi implica che è necessario prestare grande attenzione durante tutte le operazioni di eliminazione con gli SDK di Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="679e3-209">Sharing a keychain means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="679e3-210">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="679e3-210">That's it!</span></span> <span data-ttu-id="679e3-211">L'SDK di Microsoft Identity condividerà le credenziali tra tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="679e3-211">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="679e3-212">Anche l'elenco degli utenti verrà condiviso tra le istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-212">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="679e3-213">Attivazione di SSO per SSO assistito da broker</span><span class="sxs-lookup"><span data-stu-id="679e3-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="679e3-214">La possibilità per un'applicazione di usare qualsiasi broker installato nel dispositivo è **disattivata per impostazione predefinita**.</span><span class="sxs-lookup"><span data-stu-id="679e3-214">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="679e3-215">Per usare l'applicazione con il broker è necessario apportare alcune modifiche alla configurazione e aggiungere una parte di codice all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-215">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="679e3-216">Ecco i passaggi da seguire:</span><span class="sxs-lookup"><span data-stu-id="679e3-216">The steps to follow are:</span></span>

1. <span data-ttu-id="679e3-217">Abilitare la modalità broker nella chiamata del codice dell'applicazione a MS SDK.</span><span class="sxs-lookup"><span data-stu-id="679e3-217">Enable broker mode in your application code's call to the MS SDK.</span></span>
2. <span data-ttu-id="679e3-218">Stabilire un nuovo URI di reindirizzamento e fornirlo sia all'app che alla registrazione dell'app</span><span class="sxs-lookup"><span data-stu-id="679e3-218">Establish a new redirect URI and provide that to both the app and your app registration.</span></span>
3. <span data-ttu-id="679e3-219">Registrazione di uno schema URL.</span><span class="sxs-lookup"><span data-stu-id="679e3-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="679e3-220">Supporto per iOS9: aggiungere un'autorizzazione al file info.plist.</span><span class="sxs-lookup"><span data-stu-id="679e3-220">iOS9 Support: Add a permission to your info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="679e3-221">Passaggio 1: Abilitare la modalità broker nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="679e3-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="679e3-222">La possibilità per l'applicazione di usare il broker viene attivata quando si crea il "contesto" o la configurazione iniziale dell'oggetto di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-222">The ability for your application to use the broker is turned on when you create the "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="679e3-223">A tal fine, impostare il tipo delle credenziali nel codice:</span><span class="sxs-lookup"><span data-stu-id="679e3-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See the ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="679e3-224">L'impostazione `AD_CREDENTIALS_AUTO` consentirà a Microsoft Identity SDK di provare a chiamare il broker, mentre `AD_CREDENTIALS_EMBEDDED` impedirà a Microsoft Identity SDK di chiamare il broker.</span><span class="sxs-lookup"><span data-stu-id="679e3-224">The `AD_CREDENTIALS_AUTO` setting will allow the Microsoft Identity SDK to try to call out to the broker, `AD_CREDENTIALS_EMBEDDED` will prevent the Microsoft Identity SDK from calling to the broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="679e3-225">Passaggio 2: Registrazione di uno schema URL</span><span class="sxs-lookup"><span data-stu-id="679e3-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="679e3-226">La piattaforma Microsoft Identity usa gli URL per richiamare il broker e quindi restituire il controllo all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-226">The Microsoft Identity platform uses URLs to invoke the broker and then return control back to your application.</span></span> <span data-ttu-id="679e3-227">Per completare tale round trip, è necessario uno schema URL registrato per l'applicazione, di cui la piattaforma Microsoft Identity verrà a conoscenza</span><span class="sxs-lookup"><span data-stu-id="679e3-227">To finish that round trip you need a URL scheme registered for your application that the Microsoft Identity platform will know about.</span></span> <span data-ttu-id="679e3-228">e che può andare ad aggiungersi a eventuali altri schemi app già registrati con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-228">This can be in addition to any other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="679e3-229">È consigliabile rendere il più possibile univoco lo schema URL per ridurre al minimo le possibilità che un'altra app usi lo stesso schema URL.</span><span class="sxs-lookup"><span data-stu-id="679e3-229">We recommend making the URL scheme fairly unique to minimize the chances of another app using the same URL scheme.</span></span> <span data-ttu-id="679e3-230">Apple non impone l'univocità degli schemi URL registrati nell'App Store.</span><span class="sxs-lookup"><span data-stu-id="679e3-230">Apple does not enforce the uniqueness of URL schemes that are registered in the app store.</span></span>
> 
> 

<span data-ttu-id="679e3-231">Ecco un esempio di come appare nella configurazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="679e3-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="679e3-232">È anche possibile usare XCode:</span><span class="sxs-lookup"><span data-stu-id="679e3-232">You may also do this in XCode as well:</span></span>

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

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="679e3-233">Passaggio 3: Stabilire un nuovo URI di reindirizzamento con lo schema URL</span><span class="sxs-lookup"><span data-stu-id="679e3-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="679e3-234">Per assicurarsi che i token delle credenziali vengano sempre restituiti all'applicazione corretta, è necessario verificare che l'applicazione venga richiamata in un modo controllabile dal sistema operativo iOS.</span><span class="sxs-lookup"><span data-stu-id="679e3-234">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the iOS operating system can verify.</span></span> <span data-ttu-id="679e3-235">Il sistema operativo iOS segnala alle applicazioni broker Microsoft l'ID bundle dell'applicazione chiamante,</span><span class="sxs-lookup"><span data-stu-id="679e3-235">The iOS operating system reports to the Microsoft broker applications the Bundle ID of the application calling it.</span></span> <span data-ttu-id="679e3-236">di cui un'applicazione non autorizzata non può effettuare lo spoofing.</span><span class="sxs-lookup"><span data-stu-id="679e3-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="679e3-237">Di conseguenza, l'hash del certificato viene usato insieme all'URI dell'applicazione broker per garantire che i token vengano restituiti all'applicazione corretta.</span><span class="sxs-lookup"><span data-stu-id="679e3-237">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="679e3-238">È necessario definire questo URI di reindirizzamento univoco nell'applicazione e impostarlo come URI di reindirizzamento nel portale per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="679e3-238">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="679e3-239">L'URI di reindirizzamento deve essere nel formato corretto:</span><span class="sxs-lookup"><span data-stu-id="679e3-239">Your redirect URI must be in the proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="679e3-240">Ad esempio: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="679e3-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="679e3-241">L'URI di reindirizzamento deve essere specificato nella registrazione dell'app tramite il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="679e3-241">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="679e3-242">Per altre informazioni sulla registrazione di app Azure AD, vedere [Integrazione con Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="679e3-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-to-support-certificate-based-authentication"></a><span data-ttu-id="679e3-243">Passaggio 3a: Aggiungere un URI di reindirizzamento nell'app e nel portale per sviluppatori per supportare l'autenticazione basata su certificati</span><span class="sxs-lookup"><span data-stu-id="679e3-243">Step 3a: Add a redirect URI in your app and dev portal to support certificate based authentication</span></span>
<span data-ttu-id="679e3-244">Per supportare l'autenticazione basata su certificati è necessario registrare un secondo "msauth" nell'applicazione e nel [portale di Azure](https://portal.azure.com/) per gestire l'autenticazione del certificato, se si vuole aggiungere tale supporto nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="679e3-244">To support cert based authentication a second "msauth"  needs to be registered in your application and the [Azure portal](https://portal.azure.com/) to handle certificate authentication if you wish to add that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="679e3-245">Ad esempio: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="679e3-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-to-your-app"></a><span data-ttu-id="679e3-246">Passaggio 4: iOS9: Aggiungere un parametro di configurazione all'app</span><span class="sxs-lookup"><span data-stu-id="679e3-246">Step 4: iOS9: Add a configuration parameter to your app</span></span>
<span data-ttu-id="679e3-247">ADAL usa –canOpenURL: per controllare se il broker è installato nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="679e3-247">ADAL uses –canOpenURL: to check if the broker is installed on the device.</span></span> <span data-ttu-id="679e3-248">In iOS 9 Apple ha bloccato gli schemi di cui un'applicazione può effettuare una query.</span><span class="sxs-lookup"><span data-stu-id="679e3-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="679e3-249">Sarà necessario aggiungere "msauth" alla sezione LSApplicationQueriesSchemes di `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="679e3-249">You will need to add “msauth” to the LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="679e3-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="679e3-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="679e3-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="679e3-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="679e3-252">L'SSO è stato configurato!</span><span class="sxs-lookup"><span data-stu-id="679e3-252">You've configured SSO!</span></span>
<span data-ttu-id="679e3-253">Ora Microsoft Identity SDK condividerà automaticamente le credenziali tra le applicazioni e richiamerà il broker, se presente nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="679e3-253">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

