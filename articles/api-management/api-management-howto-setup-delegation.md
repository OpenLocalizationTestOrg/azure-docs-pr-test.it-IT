---
title: Come delegare la registrazione utente e la sottoscrizione ai prodotti
description: Informazioni su come delegare la registrazione dell'utente e la sottoscrizione del prodotto a terze parti in Gestione API di Azure.
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="70748-103">Come delegare la registrazione utente e la sottoscrizione ai prodotti</span><span class="sxs-lookup"><span data-stu-id="70748-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="70748-104">La delega consente di usare il sito Web esistente per gestire l'accesso e l'iscrizione degli sviluppatori e la sottoscrizione ai prodotti invece di usare la funzionalità incorporata nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="70748-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="70748-105">Ciò consente al sito Web di avere la proprietà dei dati utente e di eseguire la convalida di questi passaggi in modo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="70748-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="70748-106"><a name="delegate-signin-up"> </a>Delega dell'accesso e dell'iscrizione degli sviluppatori</span><span class="sxs-lookup"><span data-stu-id="70748-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="70748-107">Per delegare l'accesso e l'iscrizione degli sviluppatori al sito Web esistente, è necessario creare un endpoint di delega speciale nel sito che funge da punto di ingresso per qualsiasi richiesta avviata dal portale per sviluppatori di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="70748-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="70748-108">Il flusso di lavoro finale sarà il seguente:</span><span class="sxs-lookup"><span data-stu-id="70748-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="70748-109">Lo sviluppatore fa clic sul collegamento per l'accesso o l'iscrizione nel portale per sviluppatori di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="70748-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="70748-110">Il browser viene reindirizzato all'endpoint di delega.</span><span class="sxs-lookup"><span data-stu-id="70748-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="70748-111">L'endpoint di delega visualizza o reindirizza a sua volta all'interfaccia utente in cui viene richiesto di effettuare l'accesso o l'iscrizione.</span><span class="sxs-lookup"><span data-stu-id="70748-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="70748-112">In caso di esito positivo, l'utente viene reindirizzato alla pagina del portale per sviluppatori di Gestione API da dove è partito.</span><span class="sxs-lookup"><span data-stu-id="70748-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="70748-113">Per iniziare, configurare innanzitutto Gestione API per indirizzare le richieste tramite l'endpoint di delega.</span><span class="sxs-lookup"><span data-stu-id="70748-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="70748-114">Nel portale di pubblicazione Gestione API fare clic su **Sicurezza** e selezionare la scheda **Delega**.</span><span class="sxs-lookup"><span data-stu-id="70748-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="70748-115">Fare clic sulla casella di controllo per abilitare "Delega accesso e iscrizione".</span><span class="sxs-lookup"><span data-stu-id="70748-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Pagina Delega][api-management-delegation-signin-up]

* <span data-ttu-id="70748-117">Stabilire l'URL dell'endpoint di delega speciale e immetterlo nel campo **URL dell'endpoint delega** .</span><span class="sxs-lookup"><span data-stu-id="70748-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="70748-118">Nel campo **Chiave di autenticazione delega** immettere una chiave privata da usare per calcolare una firma fornita per verifica in modo da garantire che la richiesta provenga effettivamente da Gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="70748-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="70748-119">È quindi possibile fare clic sul pulsante **genera** in modo che Gestione API generi una chiave in modo casuale.</span><span class="sxs-lookup"><span data-stu-id="70748-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="70748-120">È ora necessario creare l'**endpoint di delega**,</span><span class="sxs-lookup"><span data-stu-id="70748-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="70748-121">che dovrà eseguire diverse operazioni:</span><span class="sxs-lookup"><span data-stu-id="70748-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="70748-122">Ricevere una richiesta nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="70748-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="70748-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="70748-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="70748-124">Parametri di query per l'accesso o l'iscrizione:</span><span class="sxs-lookup"><span data-stu-id="70748-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="70748-125">**operation**: identifica il tipo di richiesta di delega; in questo caso può essere solo di tipo **SignIn**</span><span class="sxs-lookup"><span data-stu-id="70748-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="70748-126">**returnUrl**: l'URL della pagina in cui l'utente ha selezionato il collegamento per l'accesso o l'iscrizione</span><span class="sxs-lookup"><span data-stu-id="70748-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="70748-127">**salt**: stringa salt speciale usata per il calcolo di un hash di sicurezza</span><span class="sxs-lookup"><span data-stu-id="70748-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="70748-128">**sig**: hash di sicurezza calcolato da usare per il confronto con il proprio hash calcolato</span><span class="sxs-lookup"><span data-stu-id="70748-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="70748-129">Verificare che la richiesta provenga da Gestione API di Azure. Questa operazione è facoltativa ma altamente consigliata per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="70748-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="70748-130">Calcolare un hash HMAC-SHA512 di una stringa in base ai parametri di query **returnUrl** e **salt** ([il codice di esempio è fornito di seguito]):</span><span class="sxs-lookup"><span data-stu-id="70748-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="70748-131">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="70748-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="70748-132">Confrontare l'hash sopra calcolato con il valore del parametro di query **sig** .</span><span class="sxs-lookup"><span data-stu-id="70748-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="70748-133">Se i due hash corrispondono, procedere con il passaggio successivo; in caso contrario, negare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="70748-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="70748-134">Verificare la ricezione di una richiesta di accesso o iscrizione: il parametro di query **operation** verrà impostato su "**SignIn**".</span><span class="sxs-lookup"><span data-stu-id="70748-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="70748-135">Visualizzare l'interfaccia utente per effettuare l'accesso o l'iscrizione.</span><span class="sxs-lookup"><span data-stu-id="70748-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="70748-136">Se l'utente sta effettuando un'iscrizione, è necessario creare un account corrispondente in Gestione API.</span><span class="sxs-lookup"><span data-stu-id="70748-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="70748-137">[Creare un utente] con l'API REST di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="70748-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="70748-138">Quando si esegue questa operazione, assicurarsi di impostare l'ID utente sullo stesso valore presente nell'archivio utenti o su un ID di cui è possibile tenere traccia.</span><span class="sxs-lookup"><span data-stu-id="70748-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="70748-139">Quando l'utente viene autenticato correttamente:</span><span class="sxs-lookup"><span data-stu-id="70748-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="70748-140">[Richiedere un token SSO (Single Sign-On)] tramite l'API REST di Gestione API</span><span class="sxs-lookup"><span data-stu-id="70748-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="70748-141">Aggiungere un parametro di query returnUrl all'URL SSO ricevuto dalla chiamata API precedente:</span><span class="sxs-lookup"><span data-stu-id="70748-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="70748-142">ad esempio, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="70748-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="70748-143">Reindirizzare l'utente all'URL generato in precedenza</span><span class="sxs-lookup"><span data-stu-id="70748-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="70748-144">Oltre all'operazione **SignIn** , è anche possibile eseguire la gestione degli account seguendo i passaggi precedenti e usando una delle operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="70748-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="70748-145">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="70748-145">**ChangePassword**</span></span>
* <span data-ttu-id="70748-146">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="70748-146">**ChangeProfile**</span></span>
* <span data-ttu-id="70748-147">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="70748-147">**CloseAccount**</span></span>

<span data-ttu-id="70748-148">È necessario passare i parametri di query seguenti per le operazioni di gestione di account.</span><span class="sxs-lookup"><span data-stu-id="70748-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="70748-149">**operation**: identifica il tipo di richiesta di delega (ChangePassword, ChangeProfile o CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="70748-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="70748-150">**userId**: ID utente dell'account da gestire</span><span class="sxs-lookup"><span data-stu-id="70748-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="70748-151">**salt**: stringa salt speciale usata per il calcolo di un hash di sicurezza</span><span class="sxs-lookup"><span data-stu-id="70748-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="70748-152">**sig**: hash di sicurezza calcolato da usare per il confronto con il proprio hash calcolato</span><span class="sxs-lookup"><span data-stu-id="70748-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="70748-153"><a name="delegate-product-subscription"> </a>Delega della sottoscrizione ai prodotti</span><span class="sxs-lookup"><span data-stu-id="70748-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="70748-154">La delega della sottoscrizione ai prodotti funziona in modo analogo alla delega dell'accesso o dell'iscrizione.</span><span class="sxs-lookup"><span data-stu-id="70748-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="70748-155">Il flusso di lavoro finale sarà il seguente:</span><span class="sxs-lookup"><span data-stu-id="70748-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="70748-156">Lo sviluppatore seleziona un prodotto nel portale per sviluppatori di Gestione API e fa clic sul pulsante Sottoscrivi.</span><span class="sxs-lookup"><span data-stu-id="70748-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="70748-157">Il browser viene reindirizzato all'endpoint di delega.</span><span class="sxs-lookup"><span data-stu-id="70748-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="70748-158">L'endpoint di delega esegue i passaggi necessari per la sottoscrizione ai prodotti. È possibile scegliere i passaggi da eseguire, ad esempio se reindirizzare a un'altra pagina per richiedere le informazioni di fatturazione, se porre altre domande o semplicemente se archiviare le informazioni senza richiedere alcun intervento da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="70748-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="70748-159">Per abilitare la funzionalità, nella pagina **Delega** fare clic su **Delega sottoscrizione ai prodotti**.</span><span class="sxs-lookup"><span data-stu-id="70748-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="70748-160">Assicurarsi quindi che l'endpoint di delega esegua le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="70748-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="70748-161">Ricevere una richiesta nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="70748-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="70748-162">*http://www.yourwebsite.com/apimdelegation?operation={operazione}&productId={prodotto per il quale effettuare la sottoscrizione}&userId={utente che esegue la richiesta}&salt={stringa}&sid={stringa}*</span><span class="sxs-lookup"><span data-stu-id="70748-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="70748-163">Parametri di query per la sottoscrizione ai prodotti:</span><span class="sxs-lookup"><span data-stu-id="70748-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="70748-164">**operation**: identifica il tipo di richiesta di delega.</span><span class="sxs-lookup"><span data-stu-id="70748-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="70748-165">Per le richieste di sottoscrizione ai prodotti le opzioni valide sono:</span><span class="sxs-lookup"><span data-stu-id="70748-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="70748-166">"Subscribe": richiesta di sottoscrizione a un prodotto specifico con l'ID fornito (vedere sotto)</span><span class="sxs-lookup"><span data-stu-id="70748-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="70748-167">"Unsubscribe": richiesta di annullamento della sottoscrizione a un prodotto</span><span class="sxs-lookup"><span data-stu-id="70748-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="70748-168">"Renew": richiesta di rinnovo di una sottoscrizione, ad esempio perché è scaduta</span><span class="sxs-lookup"><span data-stu-id="70748-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="70748-169">**productId**: ID del prodotto a cui effettuare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="70748-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="70748-170">**userId**: ID dell'utente per il quale viene eseguita la richiesta</span><span class="sxs-lookup"><span data-stu-id="70748-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="70748-171">**salt**: stringa salt speciale usata per il calcolo di un hash di sicurezza</span><span class="sxs-lookup"><span data-stu-id="70748-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="70748-172">**sig**: hash di sicurezza calcolato da usare per il confronto con il proprio hash calcolato</span><span class="sxs-lookup"><span data-stu-id="70748-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="70748-173">Verificare che la richiesta provenga da Gestione API di Azure. Questa operazione è facoltativa ma altamente consigliata per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="70748-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="70748-174">Calcolare un hash HMAC-SHA512 di una stringa in base ai parametri di query **productId**, **userId** e **salt**:</span><span class="sxs-lookup"><span data-stu-id="70748-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="70748-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="70748-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="70748-176">Confrontare l'hash sopra calcolato con il valore del parametro di query **sig** .</span><span class="sxs-lookup"><span data-stu-id="70748-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="70748-177">Se i due hash corrispondono, procedere con il passaggio successivo; in caso contrario, negare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="70748-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="70748-178">Eseguire una qualsiasi elaborazione della sottoscrizione al prodotto in base al tipo di operazione richiesta in **operation** , ad esempio fatturazione, altre domande e così via.</span><span class="sxs-lookup"><span data-stu-id="70748-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="70748-179">Dopo la corretta sottoscrizione al prodotto in locale, effettuare la sottoscrizione al prodotto in Gestione API [chiamando l'API REST per la sottoscrizione al prodotto].</span><span class="sxs-lookup"><span data-stu-id="70748-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="70748-180"><a name="delegate-example-code"> </a> Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="70748-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="70748-181">I codici di esempio seguenti illustrano come usare la *chiave di convalida della delega*, impostata nella schermata Delega del portale di pubblicazione, per creare un HMAC che viene quindi usato per convalidare la firma, dimostrando la validità del returnUrl passato.</span><span class="sxs-lookup"><span data-stu-id="70748-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="70748-182">Lo stesso codice funziona per productId e userId con leggeri modifiche.</span><span class="sxs-lookup"><span data-stu-id="70748-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="70748-183">**Codice C# per generare l'hash di returnUrl**</span><span class="sxs-lookup"><span data-stu-id="70748-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="70748-184">**Codice NodeJS per generare l'hash di returnUrl**</span><span class="sxs-lookup"><span data-stu-id="70748-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="70748-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70748-185">Next steps</span></span>
<span data-ttu-id="70748-186">Per altre informazioni sulla delega, vedere il video seguente.</span><span class="sxs-lookup"><span data-stu-id="70748-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="70748-187">[Richiedere un token SSO (Single Sign-On)]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="70748-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="70748-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="70748-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="70748-189">[chiamando l'API REST per la sottoscrizione al prodotto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="70748-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="70748-190">[il codice di esempio è fornito di seguito]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="70748-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
