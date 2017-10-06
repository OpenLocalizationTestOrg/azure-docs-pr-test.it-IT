---
title: aaaHow toodelegate registrazione e il prodotto sottoscrizione utente
description: Informazioni su come utente toodelegate registrazione e il prodotto tooa sottoscrizione di terze parti in Gestione API di Azure.
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
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="64c9c-103">La sottoscrizione di prodotto e la registrazione utente toodelegate</span><span class="sxs-lookup"><span data-stu-id="64c9c-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="64c9c-104">La delega consente toouse il sito Web esistente per la gestione tooproducts sign-in/iscrizione e sottoscrizione di sviluppatore come anziché funzionalità incorporate di hello toousing nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="64c9c-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="64c9c-105">Questo modo i dati degli utenti del sito Web tooown hello ed eseguire la convalida di hello di questi passaggi in modo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="64c9c-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="64c9c-106"><a name="delegate-signin-up"></a>Delega dell'accesso e dell'iscrizione degli sviluppatori</span><span class="sxs-lookup"><span data-stu-id="64c9c-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="64c9c-107">toodelegate developer tooyour Accedi ed effettuare l'iscrizione sito Web esistente che è necessario un endpoint speciale delega toocreate del sito che funge da punto di ingresso per tale richiesta avviata dal portale per sviluppatori di gestione API hello hello.</span><span class="sxs-lookup"><span data-stu-id="64c9c-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="64c9c-108">flusso di lavoro finale Hello verrà modificato come segue:</span><span class="sxs-lookup"><span data-stu-id="64c9c-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="64c9c-109">Developer fare clic sul collegamento di iscrizione o di accesso di hello in hello portale per sviluppatori di gestione API</span><span class="sxs-lookup"><span data-stu-id="64c9c-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="64c9c-110">Browser viene reindirizzato toohello delega endpoint</span><span class="sxs-lookup"><span data-stu-id="64c9c-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="64c9c-111">Endpoint di delega in cambio utente viene reindirizzato tooor presenta dell'interfaccia utente in cui viene chiesto toosign aggiuntivo o per l'abbonamento</span><span class="sxs-lookup"><span data-stu-id="64c9c-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="64c9c-112">Se l'operazione riesce, hello è reindirizzato toohello indietro gestione API per sviluppatori pagina del portale da che sono avviate</span><span class="sxs-lookup"><span data-stu-id="64c9c-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="64c9c-113">toobegin, si prima tooroute gestione API di configurazione richieste con l'endpoint di delega.</span><span class="sxs-lookup"><span data-stu-id="64c9c-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="64c9c-114">Nel portale di pubblicazione di gestione API hello, fare clic su **sicurezza** e quindi fare clic su hello **delega** scheda. Fare clic sulla casella di controllo di hello tooenable 'Delegate Accedi & iscrizione'.</span><span class="sxs-lookup"><span data-stu-id="64c9c-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Pagina Delega][api-management-delegation-signin-up]

* <span data-ttu-id="64c9c-116">Decidere quali hello URL dell'endpoint speciali delega verrà e immetterlo nel hello **URL dell'endpoint delega** campo.</span><span class="sxs-lookup"><span data-stu-id="64c9c-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="64c9c-117">All'interno di hello **chiave di autenticazione delega** immettere una chiave privata che verrà utilizzato toocompute tooyou una firma fornito per la verifica tooensure che hello richiesta proviene effettivamente da Gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="64c9c-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="64c9c-118">È possibile fare clic su hello **generare** toohave pulsante Gestione API in modo casuale, generare una chiave per l'utente.</span><span class="sxs-lookup"><span data-stu-id="64c9c-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="64c9c-119">È possibile procedere hello toocreate **endpoint delega**.</span><span class="sxs-lookup"><span data-stu-id="64c9c-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="64c9c-120">Dispone di tooperform una serie di azioni:</span><span class="sxs-lookup"><span data-stu-id="64c9c-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="64c9c-121">Riceve una richiesta in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="64c9c-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="64c9c-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="64c9c-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="64c9c-123">Parametri di query per il caso di accesso / iscrizione hello:</span><span class="sxs-lookup"><span data-stu-id="64c9c-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="64c9c-124">**operation**: identifica il tipo di richiesta di delega; in questo caso può essere solo di tipo **SignIn**</span><span class="sxs-lookup"><span data-stu-id="64c9c-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="64c9c-125">**returnUrl**: hello URL della pagina hello in cui hello utente ha fatto clic su un collegamento di iscrizione o di accesso</span><span class="sxs-lookup"><span data-stu-id="64c9c-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="64c9c-126">**salt**: stringa salt speciale usata per il calcolo di un hash di sicurezza</span><span class="sxs-lookup"><span data-stu-id="64c9c-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="64c9c-127">**SIG**: hash calcolato un toobe hash sicurezza calcolata utilizzata per tooyour di confronto personalizzati</span><span class="sxs-lookup"><span data-stu-id="64c9c-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="64c9c-128">Verificare che la richiesta hello proviene da Gestione API di Azure (facoltativo ma consigliato per la sicurezza)</span><span class="sxs-lookup"><span data-stu-id="64c9c-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="64c9c-129">Calcolare un hash di HMAC-SHA512 di una stringa in base a hello **returnUrl** e **salt** parametri di query ([codice di esempio riportate di seguito]):</span><span class="sxs-lookup"><span data-stu-id="64c9c-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="64c9c-130">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="64c9c-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="64c9c-131">Confrontare hello hash calcolato in precedenza toohello valore hello **sig** parametro di query.</span><span class="sxs-lookup"><span data-stu-id="64c9c-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="64c9c-132">Se hello due hash corrispondono, spostare nel passaggio successivo toohello, in caso contrario negare hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="64c9c-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="64c9c-133">Verificare che si riceve una richiesta per l'accesso in/segno: hello **operazione** verrà impostato il parametro di query troppo "**SignIn**".</span><span class="sxs-lookup"><span data-stu-id="64c9c-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="64c9c-134">Utente hello presente con interfaccia utente toosign-in o iscrizione</span><span class="sxs-lookup"><span data-stu-id="64c9c-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="64c9c-135">Se l'utente di hello è iscrizione è toocreate un account corrispondente per tali in Gestione API.</span><span class="sxs-lookup"><span data-stu-id="64c9c-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="64c9c-136">[Creare un utente] con hello API REST gestione API.</span><span class="sxs-lookup"><span data-stu-id="64c9c-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="64c9c-137">In tal caso, assicurarsi di impostare toohello ID utente di hello stesso che si trovi nell'archivio utente o ID tooan che è possibile tenere traccia delle.</span><span class="sxs-lookup"><span data-stu-id="64c9c-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="64c9c-138">Quando hello viene correttamente autenticato:</span><span class="sxs-lookup"><span data-stu-id="64c9c-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="64c9c-139">[richiedere un token di single sign-on (SSO)] tramite hello API REST gestione API</span><span class="sxs-lookup"><span data-stu-id="64c9c-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="64c9c-140">aggiungere un toohello di parametro di query returnUrl URL SSO ricevuto dalla chiamata all'API hello precedente:</span><span class="sxs-lookup"><span data-stu-id="64c9c-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="64c9c-141">ad esempio, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="64c9c-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="64c9c-142">hello utente toohello sopra prodotti URL di reindirizzamento</span><span class="sxs-lookup"><span data-stu-id="64c9c-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="64c9c-143">In aggiunta toohello **SignIn** operazione, è anche possibile eseguire la gestione degli account seguendo i passaggi precedenti hello e utilizzando uno di hello seguenti operazioni.</span><span class="sxs-lookup"><span data-stu-id="64c9c-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="64c9c-144">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="64c9c-144">**ChangePassword**</span></span>
* <span data-ttu-id="64c9c-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="64c9c-145">**ChangeProfile**</span></span>
* <span data-ttu-id="64c9c-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="64c9c-146">**CloseAccount**</span></span>

<span data-ttu-id="64c9c-147">È necessario passare hello seguenti parametri di query per le operazioni di gestione di account.</span><span class="sxs-lookup"><span data-stu-id="64c9c-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="64c9c-148">**operation**: identifica il tipo di richiesta di delega (ChangePassword, ChangeProfile o CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="64c9c-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="64c9c-149">**userId**: id utente hello di hello account toomanage</span><span class="sxs-lookup"><span data-stu-id="64c9c-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="64c9c-150">**salt**: stringa salt speciale usata per il calcolo di un hash di sicurezza</span><span class="sxs-lookup"><span data-stu-id="64c9c-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="64c9c-151">**SIG**: hash calcolato un toobe hash sicurezza calcolata utilizzata per tooyour di confronto personalizzati</span><span class="sxs-lookup"><span data-stu-id="64c9c-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="64c9c-152"><a name="delegate-product-subscription"></a>Delega della sottoscrizione ai prodotti</span><span class="sxs-lookup"><span data-stu-id="64c9c-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="64c9c-153">La sottoscrizione al prodotto di delega funziona in modo analogo toodelegating utente Accedi/verticale.</span><span class="sxs-lookup"><span data-stu-id="64c9c-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="64c9c-154">flusso di lavoro Hello finale sarà come segue:</span><span class="sxs-lookup"><span data-stu-id="64c9c-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="64c9c-155">Sviluppatore seleziona un prodotto nel portale per sviluppatori di gestione API hello e fa clic sul pulsante Sottoscrivi hello</span><span class="sxs-lookup"><span data-stu-id="64c9c-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="64c9c-156">Browser viene reindirizzato toohello delega endpoint</span><span class="sxs-lookup"><span data-stu-id="64c9c-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="64c9c-157">Endpoint di delega esegue operazioni di sottoscrizione di prodotto obbligatorio: si tratta di tooyou e può comportare reindirizzamento toorequest di pagina tooanother informazioni di fatturazione, porre altre domande, o semplicemente l'archiviazione delle informazioni di hello e che non richiedono un'azione dell'utente</span><span class="sxs-lookup"><span data-stu-id="64c9c-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="64c9c-158">funzionalità di hello tooenable, su hello **delega** pagina fare clic su **delegare sottoscrizione al prodotto**.</span><span class="sxs-lookup"><span data-stu-id="64c9c-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="64c9c-159">Assicurarsi quindi di endpoint di delega hello esegue hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="64c9c-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="64c9c-160">Riceve una richiesta in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="64c9c-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="64c9c-161">*{operazione} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {toosubscribe prodotto per} & userId = {user richiesta} & salt = {stringa} & sig = {stringa}*</span><span class="sxs-lookup"><span data-stu-id="64c9c-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="64c9c-162">Parametri di query per il caso di sottoscrizione hello prodotto:</span><span class="sxs-lookup"><span data-stu-id="64c9c-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="64c9c-163">**operation**: identifica il tipo di richiesta di delega.</span><span class="sxs-lookup"><span data-stu-id="64c9c-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="64c9c-164">Per la sottoscrizione al prodotto richieste hello i valori validi sono:</span><span class="sxs-lookup"><span data-stu-id="64c9c-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="64c9c-165">"Sottoscrizione": fornito di un tooa di utente richiesta toosubscribe hello ha prodotto con ID (vedere sotto)</span><span class="sxs-lookup"><span data-stu-id="64c9c-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="64c9c-166">"Annullare la sottoscrizione": toounsubscribe una richiesta utente da un prodotto</span><span class="sxs-lookup"><span data-stu-id="64c9c-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="64c9c-167">"Rinnovare": un toorenew richiesta una sottoscrizione (ad esempio, che può scadere in)</span><span class="sxs-lookup"><span data-stu-id="64c9c-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="64c9c-168">**productId**: hello ID dell'utente di hello hello prodotto richiesto toosubscribe per</span><span class="sxs-lookup"><span data-stu-id="64c9c-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="64c9c-169">**userId**: hello ID dell'utente hello per il quale hello richiesta</span><span class="sxs-lookup"><span data-stu-id="64c9c-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="64c9c-170">**salt**: stringa salt speciale usata per il calcolo di un hash di sicurezza</span><span class="sxs-lookup"><span data-stu-id="64c9c-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="64c9c-171">**SIG**: hash calcolato un toobe hash sicurezza calcolata utilizzata per tooyour di confronto personalizzati</span><span class="sxs-lookup"><span data-stu-id="64c9c-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="64c9c-172">Verificare che la richiesta hello proviene da Gestione API di Azure (facoltativo ma consigliato per la sicurezza)</span><span class="sxs-lookup"><span data-stu-id="64c9c-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="64c9c-173">Calcolare un HMAC-SHA512 di una stringa in base a hello **productId**, **userId** e **salt** parametri di query:</span><span class="sxs-lookup"><span data-stu-id="64c9c-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="64c9c-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="64c9c-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="64c9c-175">Confrontare hello hash calcolato in precedenza toohello valore hello **sig** parametro di query.</span><span class="sxs-lookup"><span data-stu-id="64c9c-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="64c9c-176">Se hello due hash corrispondono, spostare nel passaggio successivo toohello, in caso contrario negare hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="64c9c-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="64c9c-177">Eseguire l'elaborazione della sottoscrizione qualsiasi prodotto in base al tipo di hello dell'operazione richiesta **operazione** -ad esempio fatturazione, ulteriori domande e così via.</span><span class="sxs-lookup"><span data-stu-id="64c9c-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="64c9c-178">Nella sottoscrizione correttamente hello utente toohello prodotto del lato, sottoscrizione prodotto di gestione API di hello utente toohello da [hello chiamata API REST per la sottoscrizione al prodotto].</span><span class="sxs-lookup"><span data-stu-id="64c9c-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="64c9c-179"><a name="delegate-example-code"></a> Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="64c9c-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="64c9c-180">Questi mostra esempi di codice come hello tootake *chiave di convalida di delega*, questo valore è impostato nella schermata di delega hello del portale di pubblicazione hello, toocreate un HMAC che viene quindi utilizzato firma hello toovalidate, dimostrando validità hello di hello returnUrl passato.</span><span class="sxs-lookup"><span data-stu-id="64c9c-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="64c9c-181">Hello stesso codice funziona per productId hello e ID utente con una lieve modifica.</span><span class="sxs-lookup"><span data-stu-id="64c9c-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="64c9c-182">**Hash toogenerate codice c# di returnUrl**</span><span class="sxs-lookup"><span data-stu-id="64c9c-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="64c9c-183">**NodeJS codice toogenerate hash returnUrl**</span><span class="sxs-lookup"><span data-stu-id="64c9c-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="64c9c-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64c9c-184">Next steps</span></span>
<span data-ttu-id="64c9c-185">Per ulteriori informazioni sulla delega, vedere hello video seguenti.</span><span class="sxs-lookup"><span data-stu-id="64c9c-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[richiedere un token di single sign-on (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[hello chiamata API REST per la sottoscrizione al prodotto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[codice di esempio riportate di seguito]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
