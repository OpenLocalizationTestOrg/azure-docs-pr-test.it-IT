---
title: Personalizzazione dell'interfaccia utente - Azure AD B2C | Microsoft Docs
description: "Un argomento nella funzionalità di personalizzazione dell'interfaccia utente hello in Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="f6db9-103">Azure Active B2C di Directory: Personalizzare l'interfaccia utente di Azure Active Directory B2C hello (UI)</span><span class="sxs-lookup"><span data-stu-id="f6db9-103">Azure Active Directory B2C: Customize hello Azure AD B2C user interface (UI)</span></span>

<span data-ttu-id="f6db9-104">L'esperienza utente rappresenta l'aspetto più importante in un'applicazione rivolta ai clienti.</span><span class="sxs-lookup"><span data-stu-id="f6db9-104">User experience is paramount in a customer facing application.</span></span>  <span data-ttu-id="f6db9-105">Aumento delle dimensioni del cliente base creando esperienze utente con hello aspetto del produttore.</span><span class="sxs-lookup"><span data-stu-id="f6db9-105">Grow your customer base by crafting user experiences with hello look and feel of your brand.</span></span> <span data-ttu-id="f6db9-106">Azure Active Directory B2C (Azure AD B2C) permette di personalizzare le pagine di iscrizione, accesso, modifica del profilo e reimpostazione della password con controllo Pixel Perfect.</span><span class="sxs-lookup"><span data-stu-id="f6db9-106">Azure Active Directory B2C (Azure AD B2C) lets you customize sign-up, sign-in, profile editing, and password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="f6db9-107">funzionalità personalizzazione dell'interfaccia utente pagina Hello descritta in questo articolo non si applica toohello Accedi solo criteri, la pagina di reimpostazione della password associata e messaggi di verifica.</span><span class="sxs-lookup"><span data-stu-id="f6db9-107">hello page UI customization feature described in this article does not apply toohello sign-in only policy, its accompanying password reset page, and verification emails.</span></span>  <span data-ttu-id="f6db9-108">Queste funzioni utilizzano hello [funzionalità di branding aziendale](../active-directory/active-directory-add-company-branding.md) invece.</span><span class="sxs-lookup"><span data-stu-id="f6db9-108">These features use hello [company branding feature](../active-directory/active-directory-add-company-branding.md) instead.</span></span>
>

<span data-ttu-id="f6db9-109">Questo articolo descrive hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="f6db9-109">This article covers hello following topics:</span></span>

* <span data-ttu-id="f6db9-110">funzionalità di personalizzazione dell'interfaccia utente di pagina Hello.</span><span class="sxs-lookup"><span data-stu-id="f6db9-110">hello page UI customization feature.</span></span>
* <span data-ttu-id="f6db9-111">Strumento per il caricamento tooAzure contenuto HTML nell'archiviazione Blob per l'utilizzo con funzionalità di personalizzazione dell'interfaccia utente di hello pagina.</span><span class="sxs-lookup"><span data-stu-id="f6db9-111">A tool for uploading HTML content tooAzure Blob Storage for use with hello page UI customization feature.</span></span>
* <span data-ttu-id="f6db9-112">elementi dell'interfaccia utente di Hello utilizzati da Azure AD B2C che è possibile personalizzare utilizzando fogli CSS (Cascading Style).</span><span class="sxs-lookup"><span data-stu-id="f6db9-112">hello UI elements used by Azure AD B2C that you can customize using Cascading Style Sheets (CSS).</span></span>
* <span data-ttu-id="f6db9-113">Procedure consigliate per l'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f6db9-113">Best practices when exercising this feature.</span></span>

## <a name="hello-page-ui-customization-feature"></a><span data-ttu-id="f6db9-114">funzionalità di personalizzazione dell'interfaccia utente di Hello pagina</span><span class="sxs-lookup"><span data-stu-id="f6db9-114">hello page UI customization feature</span></span>

<span data-ttu-id="f6db9-115">È possibile personalizzare hello aspetto della password di iscrizione, accedi, cliente reimpostazione e modifica del profilo di pagine (configurando [criteri](active-directory-b2c-reference-policies.md)).</span><span class="sxs-lookup"><span data-stu-id="f6db9-115">You can customize hello look and feel of customer sign-up, sign-in, password reset, and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="f6db9-116">Gli utenti possono usufruire di un'esperienza fluida durante lo spostamento tra l'applicazione e le pagine gestite da Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f6db9-116">Your customers get a seamless experience when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="f6db9-117">A differenza di altri servizi in cui le opzioni dell'interfaccia utente, Azure Active Directory B2C viene utilizzata una semplice e moderna approccio tooUI personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="f6db9-117">Unlike other services where UI options, Azure AD B2C uses a simple and modern approach tooUI customization.</span></span>

<span data-ttu-id="f6db9-118">Ecco come funziona: Azure AD B2C esegue il codice nel browser del cliente e usa un approccio moderno denominato [Condivisione di risorse tra le origini (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="f6db9-118">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span>  <span data-ttu-id="f6db9-119">In fase di esecuzione, il contenuto viene caricato da un URL specificato in un criterio.</span><span class="sxs-lookup"><span data-stu-id="f6db9-119">At run-time, content is loaded from a URL that you specify in a policy.</span></span> <span data-ttu-id="f6db9-120">È possibile specificare URL diversi per pagine diverse.</span><span class="sxs-lookup"><span data-stu-id="f6db9-120">You can specify different URLs for different pages.</span></span> <span data-ttu-id="f6db9-121">Dopo il contenuto caricato dall'URL viene unito con un frammento HTML inserito da Azure Active Directory B2C, pagina hello è visualizzato tooyour cliente.</span><span class="sxs-lookup"><span data-stu-id="f6db9-121">After content loaded from your URL is merged with an HTML fragment inserted from Azure AD B2C, hello page is displayed tooyour customer.</span></span> <span data-ttu-id="f6db9-122">È sufficiente toodo è:</span><span class="sxs-lookup"><span data-stu-id="f6db9-122">All you need toodo is:</span></span>

1. <span data-ttu-id="f6db9-123">Creare il contenuto con un oggetto vuoto ben formato HTML5 `<div id="api"></div>` elemento si trova in un punto qualsiasi nell'hello `<body>`.</span><span class="sxs-lookup"><span data-stu-id="f6db9-123">Create well-formed HTML5 content with an empty `<div id="api"></div>` element located somewhere in hello `<body>`.</span></span> <span data-ttu-id="f6db9-124">Segni di questo elemento in cui viene inserito il contenuto di Azure Active Directory B2C hello.</span><span class="sxs-lookup"><span data-stu-id="f6db9-124">This element marks where hello Azure AD B2C content is inserted.</span></span>
1. <span data-ttu-id="f6db9-125">Ospitare il contenuto in un endpoint HTTPS in cui è consentita la condivisione CORS.</span><span class="sxs-lookup"><span data-stu-id="f6db9-125">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="f6db9-126">Si noti che i metodi di richiesta GET e OPTIONS devono essere abilitati quando si configura CORS.</span><span class="sxs-lookup"><span data-stu-id="f6db9-126">Note both GET and OPTIONS request methods must be enabled when configuring CORS.</span></span>
1. <span data-ttu-id="f6db9-127">Utilizzare CSS toostyle hello elementi dell'interfaccia utente per l'inserimento di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="f6db9-127">Use CSS toostyle hello UI elements that Azure AD B2C inserts.</span></span>

### <a name="a-basic-example-of-customized-html"></a><span data-ttu-id="f6db9-128">Esempio di codice HTML personalizzato di base</span><span class="sxs-lookup"><span data-stu-id="f6db9-128">A basic example of customized HTML</span></span>

<span data-ttu-id="f6db9-129">Hello di esempio seguente è contenuto HTML di base hello che è possibile utilizzare tootest questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f6db9-129">hello following example is hello most basic HTML content that you can use tootest this capability.</span></span> <span data-ttu-id="f6db9-130">Hello utilizzare [dello strumento di supporto](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload e configurare il contenuto alla risorsa di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6db9-130">Use hello [helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="f6db9-131">È quindi possibile verificare che i pulsanti di base, non tema hello & i campi del form in ogni pagina sono visualizzati e funzionanti.</span><span class="sxs-lookup"><span data-stu-id="f6db9-131">You can then verify that hello basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a><span data-ttu-id="f6db9-132">Testare la funzionalità di personalizzazione dell'interfaccia utente di hello</span><span class="sxs-lookup"><span data-stu-id="f6db9-132">Test out hello UI customization feature</span></span>

<span data-ttu-id="f6db9-133">Desidera tootry le funzionalità di personalizzazione dell'interfaccia utente di hello utilizzando il contenuto HTML e CSS di esempio?</span><span class="sxs-lookup"><span data-stu-id="f6db9-133">Want tootry out hello UI customization feature by using our sample HTML and CSS content?</span></span>  <span data-ttu-id="f6db9-134">È stato fornito uno [strumento helper](active-directory-b2c-reference-ui-customization-helper-tool.md) che carica e configura il contenuto di esempio nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6db9-134">We've provided you [a helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="f6db9-135">È possibile ospitare il contenuto dell'interfaccia utente in qualsiasi punto: in server Web, reti CDN, AWS S3, sistemi di condivisione file e così via. Purché hello ospitato su un endpoint HTTPS disponibile pubblicamente con CORS abilitata, verrà toogo valido.</span><span class="sxs-lookup"><span data-stu-id="f6db9-135">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as hello content is hosted on a publicly available HTTPS endpoint with CORS enabled, you are good toogo.</span></span> <span data-ttu-id="f6db9-136">L'archivio BLOB di Azure viene usato solo a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="f6db9-136">We are using Azure Blob storage for illustrative purposes only.</span></span>
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a><span data-ttu-id="f6db9-137">frammenti di interfaccia utente di Hello incorporati da Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="f6db9-137">hello UI fragments embedded by Azure AD B2C</span></span>

<span data-ttu-id="f6db9-138">Nelle sezioni seguenti Hello elencano frammenti hello HTML5 che Azure Active Directory B2C unisce hello `<div id="api"></div>` elemento si trova nel contenuto.</span><span class="sxs-lookup"><span data-stu-id="f6db9-138">hello following sections list hello HTML5 fragments that Azure AD B2C merges into hello `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="f6db9-139">**Non inserire questi frammenti nel contenuto HTML5.**</span><span class="sxs-lookup"><span data-stu-id="f6db9-139">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="f6db9-140">Hello servizio Azure Active Directory B2C li inserisce in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f6db9-140">hello Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="f6db9-141">Usare questi frammenti come riferimento quando si progettano i propri Cascading Style Sheets (CSS).</span><span class="sxs-lookup"><span data-stu-id="f6db9-141">Use these fragments as a reference when designing your own Cascading Style Sheets (CSS).</span></span>

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a><span data-ttu-id="f6db9-142">Frammento inserito hello "Pagina di selezione del provider di identità"</span><span class="sxs-lookup"><span data-stu-id="f6db9-142">Fragment inserted into hello "Identity provider selection page"</span></span>

<span data-ttu-id="f6db9-143">Questa pagina contiene un elenco di identità, i provider che hello utente sono disponibili durante l'iscrizione o accesso.</span><span class="sxs-lookup"><span data-stu-id="f6db9-143">This page contains a list of identity providers that hello user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="f6db9-144">Questi pulsanti includono i provider di identità basati su social network, ad esempio Facebook e Google+, o gli account locali (basati su indirizzo di posta elettronica o nome utente).</span><span class="sxs-lookup"><span data-stu-id="f6db9-144">These buttons include social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a><span data-ttu-id="f6db9-145">Frammento inserito hello "pagina di iscrizione di un account locale"</span><span class="sxs-lookup"><span data-stu-id="f6db9-145">Fragment inserted into hello "Local account sign-up page"</span></span>

<span data-ttu-id="f6db9-146">Questa pagina contiene un modulo per eseguire l'iscrizione dell'account locale in base a un indirizzo di posta elettronica o a un nome utente.</span><span class="sxs-lookup"><span data-stu-id="f6db9-146">This page contains a form for local account sign-up based on an email address or a user name.</span></span> <span data-ttu-id="f6db9-147">modulo Hello può contenere diversi controlli di input, ad esempio una casella di input di testo, casella di immissione di password, pulsante di opzione, caselle di riepilogo a selezione singola e selezionare più caselle di controllo.</span><span class="sxs-lookup"><span data-stu-id="f6db9-147">hello form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a><span data-ttu-id="f6db9-148">Frammento inserito hello "" sociale account pagina di iscrizione"</span><span class="sxs-lookup"><span data-stu-id="f6db9-148">Fragment inserted into hello ""Social account sign-up page"</span></span>

<span data-ttu-id="f6db9-149">Questa pagina potrebbe essere visualizzata quando si effettua l'iscrizione usando un account esistente di un provider di identità basato su social network, ad esempio Facebook o Google+.</span><span class="sxs-lookup"><span data-stu-id="f6db9-149">This page may appear when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span>  <span data-ttu-id="f6db9-150">Viene utilizzato quando le informazioni aggiuntive devono essere raccolti dall'utente finale hello tramite un modulo di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="f6db9-150">It is used when additional information must be collected from hello end user using a sign-up form.</span></span> <span data-ttu-id="f6db9-151">Questa pagina è simile toohello account locale pagina di iscrizione (illustrato nella sezione precedente hello) con l'eccezione hello di campi di immissione di password hello.</span><span class="sxs-lookup"><span data-stu-id="f6db9-151">This page is similar toohello local account sign-up page (shown in hello previous section) with hello exception of hello password entry fields.</span></span>

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="f6db9-152">Frammento inserito hello "unificato iscrizione o accesso pagina"</span><span class="sxs-lookup"><span data-stu-id="f6db9-152">Fragment inserted into hello "Unified sign-up or sign-in page"</span></span>

<span data-ttu-id="f6db9-153">Questa pagina gestisce sia l'iscrizione che l'accesso dei clienti, che possono usare provider di identità basati su social network, come Facebook o Google+, o account locali.</span><span class="sxs-lookup"><span data-stu-id="f6db9-153">This page handles both sign-up & sign-in of customers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a><span data-ttu-id="f6db9-154">Frammento inserito hello "pagina di multi-factor authentication"</span><span class="sxs-lookup"><span data-stu-id="f6db9-154">Fragment inserted into hello "Multi-factor authentication page"</span></span>

<span data-ttu-id="f6db9-155">In questa pagina gli utenti possono verificare il proprio numero di telefono (tramite SMS o chiamata vocale) durante la procedura di iscrizione o di accesso.</span><span class="sxs-lookup"><span data-stu-id="f6db9-155">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a><span data-ttu-id="f6db9-156">Frammento inserito hello "[NULL]"Pagina di errore</span><span class="sxs-lookup"><span data-stu-id="f6db9-156">Fragment inserted into hello ""Error page"</span></span>

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a><span data-ttu-id="f6db9-157">Localizzazione del contenuto HTML</span><span class="sxs-lookup"><span data-stu-id="f6db9-157">Localizing your HTML content</span></span>

<span data-ttu-id="f6db9-158">È possibile localizzare il contenuto HTML attivando la ["personalizzazione della lingua"](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="f6db9-158">You can localize your HTML content by turning on ['Language customization'](active-directory-b2c-reference-language-customization.md).</span></span>  <span data-ttu-id="f6db9-159">Abilitazione di questa funzionalità consente di Azure Active Directory B2C tooforward hello aprire ID connettersi parametro, `ui-locales`, tooyour endpoint.</span><span class="sxs-lookup"><span data-stu-id="f6db9-159">Enabling this feature allows Azure AD B2C tooforward hello Open ID Connect parameter, `ui-locales`, tooyour endpoint.</span></span>  <span data-ttu-id="f6db9-160">Server di contenuti è possibile utilizzare questa pagine HTML del parametro tooprovide personalizzati che sono specifici del linguaggio.</span><span class="sxs-lookup"><span data-stu-id="f6db9-160">Your content server can use this parameter tooprovide customized HTML pages that are language-specific.</span></span>

## <a name="things-tooremember-when-building-your-own-content"></a><span data-ttu-id="f6db9-161">Operazioni tooremember durante la creazione di contenuti</span><span class="sxs-lookup"><span data-stu-id="f6db9-161">Things tooremember when building your own content</span></span>

<span data-ttu-id="f6db9-162">Se si prevede di funzionalità di personalizzazione dell'interfaccia utente di toouse hello pagina, esaminare hello procedure consigliate seguenti:</span><span class="sxs-lookup"><span data-stu-id="f6db9-162">If you are planning toouse hello page UI customization feature, review hello following best practices:</span></span>

* <span data-ttu-id="f6db9-163">Non copiare il contenuto dell'hello Azure Active Directory B2C impostazione predefinita e tentare toomodify è.</span><span class="sxs-lookup"><span data-stu-id="f6db9-163">Don't copy hello Azure AD B2C's default content and attempt toomodify it.</span></span> <span data-ttu-id="f6db9-164">Si è toobuild migliore del contenuto di HTML5 da zero e toouse contenuto predefinito come riferimento.</span><span class="sxs-lookup"><span data-stu-id="f6db9-164">It is best toobuild your HTML5 content from scratch and toouse default content as reference.</span></span>
* <span data-ttu-id="f6db9-165">Per motivi di sicurezza non è consentito è tooinclude codice JavaScript nel contenuto.</span><span class="sxs-lookup"><span data-stu-id="f6db9-165">For security reasons, we don't allow you tooinclude any JavaScript in your content.</span></span> <span data-ttu-id="f6db9-166">La maggior parte degli elementi devono essere disponibile predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="f6db9-166">Most of what you need should be available out of hello box.</span></span> <span data-ttu-id="f6db9-167">In caso contrario, utilizzare [Uservoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f6db9-167">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest new functionality.</span></span>
* <span data-ttu-id="f6db9-168">Versioni di browser supportate:</span><span class="sxs-lookup"><span data-stu-id="f6db9-168">Supported browser versions:</span></span>
  * <span data-ttu-id="f6db9-169">Internet Explorer 11, 10, Edge</span><span class="sxs-lookup"><span data-stu-id="f6db9-169">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="f6db9-170">Supporto limitato per Internet Explorer 9, 8</span><span class="sxs-lookup"><span data-stu-id="f6db9-170">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="f6db9-171">Google Chrome 42.0 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="f6db9-171">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="f6db9-172">Mozilla Firefox 38.0 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="f6db9-172">Mozilla Firefox 38.0 and above</span></span>
