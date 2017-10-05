---
title: Personalizzazione dell'interfaccia utente - Azure AD B2C | Microsoft Docs
description: "Argomento che descrive le funzionalità di personalizzazione dell'interfaccia utente in Azure Active Directory B2C"
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
ms.openlocfilehash: 122fa997ea11b369aae3c59edf0043ab19d21aea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-customize-the-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="2b73c-103">Azure Active Directory B2C: personalizzare l'interfaccia utente di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2b73c-103">Azure Active Directory B2C: Customize the Azure AD B2C user interface (UI)</span></span>

<span data-ttu-id="2b73c-104">L'esperienza utente rappresenta l'aspetto più importante in un'applicazione rivolta ai clienti.</span><span class="sxs-lookup"><span data-stu-id="2b73c-104">User experience is paramount in a customer facing application.</span></span>  <span data-ttu-id="2b73c-105">L'utente può accrescere le dimensioni della sua base di clienti grazie alla creazione di esperienze utente con l'aspetto del marchio.</span><span class="sxs-lookup"><span data-stu-id="2b73c-105">Grow your customer base by crafting user experiences with the look and feel of your brand.</span></span> <span data-ttu-id="2b73c-106">Azure Active Directory B2C (Azure AD B2C) permette di personalizzare le pagine di iscrizione, accesso, modifica del profilo e reimpostazione della password con controllo Pixel Perfect.</span><span class="sxs-lookup"><span data-stu-id="2b73c-106">Azure Active Directory B2C (Azure AD B2C) lets you customize sign-up, sign-in, profile editing, and password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="2b73c-107">La funzionalità di personalizzazione dell'interfaccia utente delle pagine descritta in questo articolo non si applica al criterio di solo accesso, alla pagina di reimpostazione della password associata e ai messaggi di posta elettronica di verifica.</span><span class="sxs-lookup"><span data-stu-id="2b73c-107">The page UI customization feature described in this article does not apply to the sign-in only policy, its accompanying password reset page, and verification emails.</span></span>  <span data-ttu-id="2b73c-108">Queste funzionalità usano invece la [funzionalità di branding aziendale](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="2b73c-108">These features use the [company branding feature](../active-directory/active-directory-add-company-branding.md) instead.</span></span>
>

<span data-ttu-id="2b73c-109">Questo articolo include gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b73c-109">This article covers the following topics:</span></span>

* <span data-ttu-id="2b73c-110">Funzionalità di personalizzazione dell'interfaccia utente delle pagine.</span><span class="sxs-lookup"><span data-stu-id="2b73c-110">The page UI customization feature.</span></span>
* <span data-ttu-id="2b73c-111">Strumento per il caricamento di contenuti HTML nell'archivio BLOB di Azure per l'uso con la funzionalità di personalizzazione dell'interfaccia utente delle pagine.</span><span class="sxs-lookup"><span data-stu-id="2b73c-111">A tool for uploading HTML content to Azure Blob Storage for use with the page UI customization feature.</span></span>
* <span data-ttu-id="2b73c-112">Elementi dell'interfaccia utente usati da Azure AD B2C che è possibile personalizzare usando Cascading Style Sheets (CSS).</span><span class="sxs-lookup"><span data-stu-id="2b73c-112">The UI elements used by Azure AD B2C that you can customize using Cascading Style Sheets (CSS).</span></span>
* <span data-ttu-id="2b73c-113">Procedure consigliate per l'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2b73c-113">Best practices when exercising this feature.</span></span>

## <a name="the-page-ui-customization-feature"></a><span data-ttu-id="2b73c-114">Funzionalità di personalizzazione dell'interfaccia utente della pagina</span><span class="sxs-lookup"><span data-stu-id="2b73c-114">The page UI customization feature</span></span>

<span data-ttu-id="2b73c-115">È possibile personalizzare l'aspetto delle pagine di iscrizione, accesso, reimpostazione della password e modifica del profilo, tramite la configurazione di [criteri](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="2b73c-115">You can customize the look and feel of customer sign-up, sign-in, password reset, and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="2b73c-116">Gli utenti possono usufruire di un'esperienza fluida durante lo spostamento tra l'applicazione e le pagine gestite da Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2b73c-116">Your customers get a seamless experience when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="2b73c-117">A differenza di altri servizi con opzioni di interfaccia utente, Azure AD B2C usa un approccio moderno e semplice per la personalizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="2b73c-117">Unlike other services where UI options, Azure AD B2C uses a simple and modern approach to UI customization.</span></span>

<span data-ttu-id="2b73c-118">Ecco come funziona: Azure AD B2C esegue il codice nel browser del cliente e usa un approccio moderno denominato [Condivisione di risorse tra le origini (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="2b73c-118">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span>  <span data-ttu-id="2b73c-119">In fase di esecuzione, il contenuto viene caricato da un URL specificato in un criterio.</span><span class="sxs-lookup"><span data-stu-id="2b73c-119">At run-time, content is loaded from a URL that you specify in a policy.</span></span> <span data-ttu-id="2b73c-120">È possibile specificare URL diversi per pagine diverse.</span><span class="sxs-lookup"><span data-stu-id="2b73c-120">You can specify different URLs for different pages.</span></span> <span data-ttu-id="2b73c-121">Dopo che il contenuto caricato dall'URL viene unito con un frammento HTML inserito da Azure AD B2C, la pagina viene mostrata al cliente.</span><span class="sxs-lookup"><span data-stu-id="2b73c-121">After content loaded from your URL is merged with an HTML fragment inserted from Azure AD B2C, the page is displayed to your customer.</span></span> <span data-ttu-id="2b73c-122">Operazioni da eseguire:</span><span class="sxs-lookup"><span data-stu-id="2b73c-122">All you need to do is:</span></span>

1. <span data-ttu-id="2b73c-123">Creare contenuto HTML5 ben formato con un elemento `<div id="api"></div>` vuoto che si trova in un punto all'interno di `<body>`.</span><span class="sxs-lookup"><span data-stu-id="2b73c-123">Create well-formed HTML5 content with an empty `<div id="api"></div>` element located somewhere in the `<body>`.</span></span> <span data-ttu-id="2b73c-124">Questo elemento corrisponde al punto in cui viene inserito il contenuto di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2b73c-124">This element marks where the Azure AD B2C content is inserted.</span></span>
1. <span data-ttu-id="2b73c-125">Ospitare il contenuto in un endpoint HTTPS in cui è consentita la condivisione CORS.</span><span class="sxs-lookup"><span data-stu-id="2b73c-125">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="2b73c-126">Si noti che i metodi di richiesta GET e OPTIONS devono essere abilitati quando si configura CORS.</span><span class="sxs-lookup"><span data-stu-id="2b73c-126">Note both GET and OPTIONS request methods must be enabled when configuring CORS.</span></span>
1. <span data-ttu-id="2b73c-127">Usare CSS per applicare uno stile agli elementi dell'interfaccia utente inseriti da Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2b73c-127">Use CSS to style the UI elements that Azure AD B2C inserts.</span></span>

### <a name="a-basic-example-of-customized-html"></a><span data-ttu-id="2b73c-128">Esempio di codice HTML personalizzato di base</span><span class="sxs-lookup"><span data-stu-id="2b73c-128">A basic example of customized HTML</span></span>

<span data-ttu-id="2b73c-129">L'esempio seguente rappresenta il contenuto HTML di base che è possibile usare per testare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2b73c-129">The following example is the most basic HTML content that you can use to test this capability.</span></span> <span data-ttu-id="2b73c-130">Usare lo [strumento helper](active-directory-b2c-reference-ui-customization-helper-tool.md) per caricare e configurare il contenuto nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b73c-130">Use the [helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) to upload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="2b73c-131">È quindi possibile verificare che i pulsanti di base, senza stili e i campi del modulo in ogni pagina siano visualizzati e funzionali.</span><span class="sxs-lookup"><span data-stu-id="2b73c-131">You can then verify that the basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

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

## <a name="test-out-the-ui-customization-feature"></a><span data-ttu-id="2b73c-132">Provare la funzionalità di personalizzazione dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="2b73c-132">Test out the UI customization feature</span></span>

<span data-ttu-id="2b73c-133">Si desidera provare le funzionalità di personalizzazione dell'interfaccia utente usando il codice HTML e il contenuto CSS?</span><span class="sxs-lookup"><span data-stu-id="2b73c-133">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span>  <span data-ttu-id="2b73c-134">È stato fornito uno [strumento helper](active-directory-b2c-reference-ui-customization-helper-tool.md) che carica e configura il contenuto di esempio nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b73c-134">We've provided you [a helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="2b73c-135">È possibile ospitare il contenuto dell'interfaccia utente in qualsiasi punto: in server Web, reti CDN, AWS S3, sistemi di condivisione file e così via. A condizione che il contenuto sia ospitato in un endpoint HTTPS disponibile pubblicamente con CORS abilitato, è possibile iniziare.</span><span class="sxs-lookup"><span data-stu-id="2b73c-135">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as the content is hosted on a publicly available HTTPS endpoint with CORS enabled, you are good to go.</span></span> <span data-ttu-id="2b73c-136">L'archivio BLOB di Azure viene usato solo a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="2b73c-136">We are using Azure Blob storage for illustrative purposes only.</span></span>
>

## <a name="the-ui-fragments-embedded-by-azure-ad-b2c"></a><span data-ttu-id="2b73c-137">Frammenti dell'interfaccia utente incorporati da Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="2b73c-137">The UI fragments embedded by Azure AD B2C</span></span>

<span data-ttu-id="2b73c-138">Le sezioni seguenti riportano i frammenti HTML5 che Azure AD B2C unisce nell'elemento `<div id="api"></div>` all'interno del contenuto.</span><span class="sxs-lookup"><span data-stu-id="2b73c-138">The following sections list the HTML5 fragments that Azure AD B2C merges into the `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="2b73c-139">**Non inserire questi frammenti nel contenuto HTML5.**</span><span class="sxs-lookup"><span data-stu-id="2b73c-139">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="2b73c-140">Il servizio Azure AD B2C li inserisce in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2b73c-140">The Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="2b73c-141">Usare questi frammenti come riferimento quando si progettano i propri Cascading Style Sheets (CSS).</span><span class="sxs-lookup"><span data-stu-id="2b73c-141">Use these fragments as a reference when designing your own Cascading Style Sheets (CSS).</span></span>

### <a name="fragment-inserted-into-the-identity-provider-selection-page"></a><span data-ttu-id="2b73c-142">Frammento inserito nella "pagina di selezione del provider di identità"</span><span class="sxs-lookup"><span data-stu-id="2b73c-142">Fragment inserted into the "Identity provider selection page"</span></span>

<span data-ttu-id="2b73c-143">Questa pagina contiene un elenco dei provider di identità che l'utente può scegliere durante la procedura di iscrizione o di accesso.</span><span class="sxs-lookup"><span data-stu-id="2b73c-143">This page contains a list of identity providers that the user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="2b73c-144">Questi pulsanti includono i provider di identità basati su social network, ad esempio Facebook e Google+, o gli account locali (basati su indirizzo di posta elettronica o nome utente).</span><span class="sxs-lookup"><span data-stu-id="2b73c-144">These buttons include social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

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

### <a name="fragment-inserted-into-the-local-account-sign-up-page"></a><span data-ttu-id="2b73c-145">Frammento inserito nella "pagina di iscrizione dell'account locale"</span><span class="sxs-lookup"><span data-stu-id="2b73c-145">Fragment inserted into the "Local account sign-up page"</span></span>

<span data-ttu-id="2b73c-146">Questa pagina contiene un modulo per eseguire l'iscrizione dell'account locale in base a un indirizzo di posta elettronica o a un nome utente.</span><span class="sxs-lookup"><span data-stu-id="2b73c-146">This page contains a form for local account sign-up based on an email address or a user name.</span></span> <span data-ttu-id="2b73c-147">Il modulo può contenere diversi controlli di input, ad esempio caselle per l'immissione di testo, caselle per l'immissione della password, pulsanti di opzione, caselle a discesa a selezione singola e caselle di controllo con selezione multipla.</span><span class="sxs-lookup"><span data-stu-id="2b73c-147">The form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing the following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">The password entry fields do not match. Please enter the same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent to your inbox. Please copy it to the input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need to send new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used to contact you.');" class="tiny">What is this?</a>

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
                        <div class="helpText">8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
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
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('The postal code of your address.');" class="tiny">What is this?</a>
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

### <a name="fragment-inserted-into-the-social-account-sign-up-page"></a><span data-ttu-id="2b73c-148">Frammento inserito nella "pagina di iscrizione all'account di social network"</span><span class="sxs-lookup"><span data-stu-id="2b73c-148">Fragment inserted into the ""Social account sign-up page"</span></span>

<span data-ttu-id="2b73c-149">Questa pagina potrebbe essere visualizzata quando si effettua l'iscrizione usando un account esistente di un provider di identità basato su social network, ad esempio Facebook o Google+.</span><span class="sxs-lookup"><span data-stu-id="2b73c-149">This page may appear when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span>  <span data-ttu-id="2b73c-150">Viene usata quando è necessario raccogliere informazioni aggiuntive dall'utente finale attraverso un modulo di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="2b73c-150">It is used when additional information must be collected from the end user using a sign-up form.</span></span> <span data-ttu-id="2b73c-151">Questa pagina è simile alla pagina di iscrizione dell'account locale (mostrata nella sezione precedente), ad eccezione dei campi di immissione della password.</span><span class="sxs-lookup"><span data-stu-id="2b73c-151">This page is similar to the local account sign-up page (shown in the previous section) with the exception of the password entry fields.</span></span>

### <a name="fragment-inserted-into-the-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="2b73c-152">Frammento inserito nella "pagina unificata per l'iscrizione o l'accesso"</span><span class="sxs-lookup"><span data-stu-id="2b73c-152">Fragment inserted into the "Unified sign-up or sign-in page"</span></span>

<span data-ttu-id="2b73c-153">Questa pagina gestisce sia l'iscrizione che l'accesso dei clienti, che possono usare provider di identità basati su social network, come Facebook o Google+, o account locali.</span><span class="sxs-lookup"><span data-stu-id="2b73c-153">This page handles both sign-up & sign-in of customers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

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

### <a name="fragment-inserted-into-the-multi-factor-authentication-page"></a><span data-ttu-id="2b73c-154">Frammento inserito nella "pagina di autenticazione a più fattori"</span><span class="sxs-lookup"><span data-stu-id="2b73c-154">Fragment inserted into the "Multi-factor authentication page"</span></span>

<span data-ttu-id="2b73c-155">In questa pagina gli utenti possono verificare il proprio numero di telefono (tramite SMS o chiamata vocale) durante la procedura di iscrizione o di accesso.</span><span class="sxs-lookup"><span data-stu-id="2b73c-155">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone to authenticate you.</p>
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

### <a name="fragment-inserted-into-the-error-page"></a><span data-ttu-id="2b73c-156">Frammento inserito nella "pagina di errore"</span><span class="sxs-lookup"><span data-stu-id="2b73c-156">Fragment inserted into the ""Error page"</span></span>

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if the problem persists feel free to contact us. In the meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting the remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a><span data-ttu-id="2b73c-157">Localizzazione del contenuto HTML</span><span class="sxs-lookup"><span data-stu-id="2b73c-157">Localizing your HTML content</span></span>

<span data-ttu-id="2b73c-158">È possibile localizzare il contenuto HTML attivando la ["personalizzazione della lingua"](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="2b73c-158">You can localize your HTML content by turning on ['Language customization'](active-directory-b2c-reference-language-customization.md).</span></span>  <span data-ttu-id="2b73c-159">L'abilitazione di questa funzionalità consente ad Azure AD B2C di inoltrare il parametro Open ID Connect, `ui-locales`, all'endpoint.</span><span class="sxs-lookup"><span data-stu-id="2b73c-159">Enabling this feature allows Azure AD B2C to forward the Open ID Connect parameter, `ui-locales`, to your endpoint.</span></span>  <span data-ttu-id="2b73c-160">Il server di contenuti può usare questo parametro per fornire pagine HTML personalizzate specifiche della lingua.</span><span class="sxs-lookup"><span data-stu-id="2b73c-160">Your content server can use this parameter to provide customized HTML pages that are language-specific.</span></span>

## <a name="things-to-remember-when-building-your-own-content"></a><span data-ttu-id="2b73c-161">Aspetti da ricordare durante la fase di creazione del contenuto</span><span class="sxs-lookup"><span data-stu-id="2b73c-161">Things to remember when building your own content</span></span>

<span data-ttu-id="2b73c-162">Se si prevede di usare la funzionalità di personalizzazione dell'interfaccia utente della pagina, fare riferimento alle procedure consigliate seguenti:</span><span class="sxs-lookup"><span data-stu-id="2b73c-162">If you are planning to use the page UI customization feature, review the following best practices:</span></span>

* <span data-ttu-id="2b73c-163">Non copiare il contenuto predefinito di Azure AD B2C né provare a modificarlo.</span><span class="sxs-lookup"><span data-stu-id="2b73c-163">Don't copy the Azure AD B2C's default content and attempt to modify it.</span></span> <span data-ttu-id="2b73c-164">È preferibile creare il contenuto HTML5 da zero e usare il contenuto predefinito come riferimento.</span><span class="sxs-lookup"><span data-stu-id="2b73c-164">It is best to build your HTML5 content from scratch and to use default content as reference.</span></span>
* <span data-ttu-id="2b73c-165">Per motivi di sicurezza, non è consentito includere codice JavaScript nel contenuto.</span><span class="sxs-lookup"><span data-stu-id="2b73c-165">For security reasons, we don't allow you to include any JavaScript in your content.</span></span> <span data-ttu-id="2b73c-166">La maggior parte degli elementi necessari dovrebbe già essere disponibile.</span><span class="sxs-lookup"><span data-stu-id="2b73c-166">Most of what you need should be available out of the box.</span></span> <span data-ttu-id="2b73c-167">In caso contrario, usare [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) per richiedere nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2b73c-167">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) to request new functionality.</span></span>
* <span data-ttu-id="2b73c-168">Versioni di browser supportate:</span><span class="sxs-lookup"><span data-stu-id="2b73c-168">Supported browser versions:</span></span>
  * <span data-ttu-id="2b73c-169">Internet Explorer 11, 10, Edge</span><span class="sxs-lookup"><span data-stu-id="2b73c-169">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="2b73c-170">Supporto limitato per Internet Explorer 9, 8</span><span class="sxs-lookup"><span data-stu-id="2b73c-170">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="2b73c-171">Google Chrome 42.0 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="2b73c-171">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="2b73c-172">Mozilla Firefox 38.0 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="2b73c-172">Mozilla Firefox 38.0 and above</span></span>
