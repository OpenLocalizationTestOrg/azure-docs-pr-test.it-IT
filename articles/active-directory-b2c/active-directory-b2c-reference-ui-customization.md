---
title: Personalizzazione dell'interfaccia utente - Azure AD B2C | Microsoft Docs
description: "Argomento che descrive le funzionalità di personalizzazione dell'interfaccia utente in Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: mtillman
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: be3fe7199308606aaab002290319df9c82149433
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="azure-active-directory-b2c-customize-the-azure-ad-b2c-user-interface-ui"></a>Azure Active Directory B2C: personalizzare l'interfaccia utente di Azure AD B2C

L'esperienza utente rappresenta l'aspetto più importante in un'applicazione rivolta ai clienti.  L'utente può accrescere le dimensioni della sua base di clienti grazie alla creazione di esperienze utente con l'aspetto del marchio. Azure Active Directory B2C (Azure AD B2C) permette di personalizzare le pagine di iscrizione, accesso, modifica del profilo e reimpostazione della password con controllo Pixel Perfect.

> [!NOTE]
> La funzionalità di personalizzazione dell'interfaccia utente delle pagine descritta in questo articolo non si applica al criterio di solo accesso, alla pagina di reimpostazione della password associata e ai messaggi di posta elettronica di verifica.  Queste funzionalità usano invece la [funzionalità di branding aziendale](../active-directory/customize-branding.md).
>
> Analogamente, se un utente avvia un criterio di modifica del profilo *prima* dell'accesso, l'utente verrà reindirizzato a una pagina che può essere personalizzata tramite la [funzionalità di branding aziendale](../active-directory/customize-branding.md).

Questo articolo include gli argomenti seguenti:

* Funzionalità di personalizzazione dell'interfaccia utente della pagina.
* Strumento per il caricamento di contenuti HTML nell'archivio BLOB di Azure per l'uso con la funzionalità di personalizzazione dell'interfaccia utente delle pagine.
* Elementi dell'interfaccia utente utilizzati da Azure AD B2C che è possibile personalizzare utilizzando fogli CSS (Cascading Style Sheets).
* Procedure consigliate per l'utilizzo di questa funzionalità.

## <a name="the-page-ui-customization-feature"></a>Funzionalità di personalizzazione dell'interfaccia utente della pagina

È possibile personalizzare l'aspetto delle pagine di iscrizione, accesso, reimpostazione della password e modifica del profilo visualizzate dagli utenti, tramite la configurazione di [criteri](active-directory-b2c-reference-policies.md). Gli utenti possono usufruire di un'esperienza fluida durante lo spostamento tra l'applicazione e le pagine gestite da Azure AD B2C.

A differenza di altri servizi con opzioni dell'interfaccia utente, Azure AD B2C utilizza un approccio moderno e semplice per la personalizzazione dell'interfaccia utente.

Ecco come funziona: Azure AD B2C esegue il codice nel browser del cliente e usa un approccio moderno denominato [Condivisione di risorse tra le origini (CORS)](http://www.w3.org/TR/cors/).  In fase di esecuzione, il contenuto viene caricato da un URL specificato in un criterio. È possibile specificare URL diversi per pagine diverse. Dopo che il contenuto dell'URL viene unito con un frammento HTML inserito da Azure AD B2C, la pagina viene visualizzata al cliente. Operazioni da eseguire:

1. Creare contenuto HTML5 ben formato con un elemento `<div id="api"></div>` vuoto, inserito all'interno di `<body>`. Questo elemento corrisponde al punto in cui viene inserito il contenuto di Azure AD B2C.
1. Ospitare il contenuto in un endpoint HTTPS in cui è consentita la condivisione CORS. Notare che i metodi di richiesta GET e OPTIONS devono essere abilitati quando si configura CORS.
1. Usare CSS per applicare uno stile agli elementi dell'interfaccia utente inseriti da Azure AD B2C.

### <a name="a-basic-example-of-customized-html"></a>Esempio di base di codice HTML personalizzato

L'esempio seguente rappresenta il contenuto HTML di base che è possibile usare per testare questa funzionalità. Utilizzare lo [strumento di supporto](active-directory-b2c-reference-ui-customization-helper-tool.md) per caricare e configurare il contenuto nell'archivio di BLOB di Azure. È quindi possibile verificare che i pulsanti di base, senza stili e i campi del modulo in ogni pagina siano visualizzati e funzionali.

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

## <a name="test-out-the-ui-customization-feature"></a>Provare la funzionalità di personalizzazione dell'interfaccia utente

Si desidera provare le funzionalità di personalizzazione dell'interfaccia utente usando il codice HTML e il contenuto CSS?  È stato fornito uno [strumento di supporto](active-directory-b2c-reference-ui-customization-helper-tool.md) che carica e configura il contenuto di esempio nell'archiviazione BLOB di Azure.

> [!NOTE]
> È possibile ospitare il contenuto dell'interfaccia utente in qualsiasi punto: in server Web, reti CDN, AWS S3, sistemi di condivisione file e così via. A condizione di avere contenuto ospitato in un endpoint HTTPS disponibile pubblicamente con CORS abilitato, è possibile iniziare. L'archivio BLOB di Azure viene usato solo a scopo illustrativo.
>

## <a name="the-ui-fragments-embedded-by-azure-ad-b2c"></a>Frammenti dell'interfaccia utente incorporati da Azure AD B2C

Nelle sezioni seguenti sono riportati i frammenti HTML5 che Azure AD B2C unisce nell'elemento `<div id="api"></div>` che si trova nel contenuto. **Non inserire questi frammenti nel contenuto HTML5.** Il servizio Azure AD B2C li inserisce in fase di esecuzione. Usare i frammenti come riferimento quando si progettano fogli CSS (Cascading Style Sheet) personalizzati.

### <a name="fragment-inserted-into-the-identity-provider-selection-page"></a>Frammento inserito nella "Pagina di selezione del provider di identità"

Questa pagina contiene un elenco dei provider di identità che l'utente può scegliere durante la procedura di iscrizione o di accesso. Questi pulsanti includono provider di identità basati su social network, ad esempio Facebook e Google+, oppure account locali (basati sull'indirizzo di posta elettronica o sul nome utente).

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

### <a name="fragment-inserted-into-the-local-account-sign-up-page"></a>Frammento inserito nella "pagina di iscrizione dell'account locale"

Questa pagina contiene un modulo per eseguire l'iscrizione dell'account locale in base a un indirizzo e-mail o a un nome utente. Il modulo può contenere diversi controlli di input, ad esempio caselle per l'immissione di testo, caselle per l'immissione della password, pulsanti di opzione, caselle a discesa a selezione singola e caselle di controllo con selezione multipla.

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

### <a name="fragment-inserted-into-the-social-account-sign-up-page"></a>Frammento inserito nella "Pagina di iscrizione all'account di social networking"

Questa pagina potrebbe essere visualizzata quando si effettua l'iscrizione usando un account esistente di un provider di identità basato su social network, ad esempio Facebook o Google+.  Viene utilizzata quando è necessario raccogliere informazioni aggiuntive dall'utente finale con un modulo di iscrizione. Questa pagina è simile alla pagina di iscrizione dell'account locale (mostrata nella sezione precedente), ad eccezione dei campi di immissione della password.

### <a name="fragment-inserted-into-the-unified-sign-up-or-sign-in-page"></a>Frammento inserito nella "Pagina unificata per l'iscrizione o l'accesso"

Questa pagina gestisce sia l'iscrizione che l'accesso dei clienti, che possono usare provider di identità basati su social network, come Facebook o Google+, o account locali.

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

### <a name="fragment-inserted-into-the-multi-factor-authentication-page"></a>Frammento inserito nella "Pagina dell'autenticazione a più fattori"

In questa pagina gli utenti possono verificare il proprio numero di telefono (tramite SMS o chiamata vocale) durante la procedura di iscrizione o di accesso.

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

### <a name="fragment-inserted-into-the-error-page"></a>Frammento inserito nella "Pagina di errore"

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

## <a name="localizing-your-html-content"></a>Localizzazione del contenuto HTML

È possibile localizzare il contenuto HTML attivando la ["personalizzazione del linguaggio"](active-directory-b2c-reference-language-customization.md).  L'abilitazione di questa funzionalità consente ad Azure AD B2C di inoltrare il parametro Open ID Connect, `ui-locales`, all'endpoint.  Il server di contenuti può utilizzare questo parametro per fornire pagine HTML personalizzate specifiche del linguaggio.

## <a name="things-to-remember-when-building-your-own-content"></a>Aspetti da ricordare durante la fase di creazione del contenuto

Se si prevede di usare la funzionalità di personalizzazione dell'interfaccia utente della pagina, fare riferimento alle procedure consigliate seguenti:

* Non copiare il contenuto predefinito di Azure AD B2C né provare a modificarlo. È preferibile creare il contenuto HTML5 da zero e usare il contenuto predefinito come riferimento.
* Per motivi di sicurezza, non è consentito includere codice JavaScript nel contenuto. La maggior parte degli elementi necessari dovrebbe già essere disponibile. In caso contrario, usare [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) per richiedere nuove funzionalità.
* Versioni di browser supportate:
  * Internet Explorer 11, 10, Edge
  * Supporto limitato per Internet Explorer 9, 8
  * Google Chrome 42.0 e versioni successive
  * Mozilla Firefox 38.0 e versioni successive
