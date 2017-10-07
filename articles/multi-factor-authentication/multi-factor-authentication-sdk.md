---
title: aaaMFA software development kit per App personalizzate | Documenti Microsoft
description: "Questo articolo illustra come toodownload e utilizzare hello verifica in due passaggi tooenable di autenticazione a più fattori di Azure SDK per le app personalizzate."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="157c4-103">Compilazione di Multi-Factor Authentication in app personalizzate (SDK)</span><span class="sxs-lookup"><span data-stu-id="157c4-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="157c4-104">Consente di Azure multi-Factor Authentication Software Development Kit (SDK) di Hello in che compilare verifica in due passaggi direttamente hello Accedi o transazione processi delle applicazioni nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="157c4-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="157c4-105">Hello multi-Factor Authentication SDK è disponibile per c#, Visual Basic (.NET), Java, Perl, PHP e Ruby.</span><span class="sxs-lookup"><span data-stu-id="157c4-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="157c4-106">Hello SDK fornisce un wrapper di verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="157c4-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="157c4-107">Include tutto ciò che occorre toowrite del codice, inclusi i file di codice sorgente commentati, file di esempio e un file ReadMe dettagliato.</span><span class="sxs-lookup"><span data-stu-id="157c4-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="157c4-108">Ogni SDK include anche un certificato e chiave privata per crittografare le transazioni che sono univoci tooyour Provider multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="157c4-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="157c4-109">Se si dispone di un provider, è possibile scaricare hello SDK in tutti i linguaggi e formati in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="157c4-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="157c4-110">struttura Hello di hello API in hello multi-Factor Authentication SDK è semplice.</span><span class="sxs-lookup"><span data-stu-id="157c4-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="157c4-111">Effettuare una singola funzione di chiamata API tooan con i parametri di opzione di multi-factor hello (ad esempio, la modalità di verifica) e dati utente (ad esempio toocall numero di telefono hello o hello PIN numerico toovalidate).</span><span class="sxs-lookup"><span data-stu-id="157c4-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="157c4-112">API Hello convertono la chiamata di funzione hello in toohello le richieste di servizi web basati su cloud di servizio Azure multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="157c4-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="157c4-113">Tutte le chiamate devono includere un certificato privato di toohello di riferimento è incluso in ogni SDK.</span><span class="sxs-lookup"><span data-stu-id="157c4-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="157c4-114">Hello API non dispone di accesso toousers registrato in Azure Active Directory, è necessario fornire le informazioni utente in un file o database.</span><span class="sxs-lookup"><span data-stu-id="157c4-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="157c4-115">Hello API fornisce inoltre funzionalità di gestione di registrazione o l'utente, pertanto è necessario toobuild tali processi nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="157c4-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="157c4-116">toodownload hello SDK, è necessario un Provider di Azure multi-Factor Authentication toocreate anche se si dispone di licenze Azure MFA, Azure ad Premium o EMS.</span><span class="sxs-lookup"><span data-stu-id="157c4-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="157c4-117">Se si dispone già di licenze a tale scopo, creare un Provider di Azure multi-Factor Authentication, assicurarsi che toocreate hello Provider con hello **Per utente abilitato** modello.</span><span class="sxs-lookup"><span data-stu-id="157c4-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="157c4-118">Quindi, collegare directory che contiene le licenze di Azure MFA, Azure AD Premium o EMS hello toohello del Provider hello.</span><span class="sxs-lookup"><span data-stu-id="157c4-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="157c4-119">Questa configurazione assicura che verrà addebitato solo se si dispone di più utenti univoci utilizzando hello SDK numero hello di licenze possedute.</span><span class="sxs-lookup"><span data-stu-id="157c4-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="157c4-120">Scaricare il SDK di hello</span><span class="sxs-lookup"><span data-stu-id="157c4-120">Download hello SDK</span></span>
<span data-ttu-id="157c4-121">Download hello Azure multi-Factor SDK richiede una [Provider di Azure multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="157c4-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="157c4-122">Questo richiede una sottoscrizione di Azure completa, anche se si possiedono licenze di Azure MFA, Azure AD Premium o Enterprise Mobility Suite.</span><span class="sxs-lookup"><span data-stu-id="157c4-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="157c4-123">hello toodownload SDK, passare toohello portale di gestione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="157c4-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="157c4-124">È possibile raggiungere il portale di hello gestendo hello direttamente i Provider di autenticazione a più fattori, oppure facendo clic su hello **"Go toohello portale"** collegamento nella pagina Impostazioni servizio di autenticazione a più fattori hello.</span><span class="sxs-lookup"><span data-stu-id="157c4-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="157c4-125">Scaricare dal portale di Azure classico hello</span><span class="sxs-lookup"><span data-stu-id="157c4-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="157c4-126">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="157c4-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="157c4-127">A sinistra di hello, selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="157c4-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="157c4-128">Nella pagina Active Directory hello in select top hello **provider multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="157c4-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="157c4-129">Nella parte inferiore di hello selezionare **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="157c4-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="157c4-130">Viene aperta una nuova pagina.</span><span class="sxs-lookup"><span data-stu-id="157c4-130">A new page opens.</span></span>
5. <span data-ttu-id="157c4-131">Scegliere a sinistra, nella parte inferiore di hello, hello **SDK**.</span><span class="sxs-lookup"><span data-stu-id="157c4-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="157c4-132"><center>![Scaricare](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="157c4-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="157c4-133">Selezionare una lingua hello desiderata e fare clic sui collegamenti di download associati hello uno.</span><span class="sxs-lookup"><span data-stu-id="157c4-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="157c4-134">Salvare il download di hello.</span><span class="sxs-lookup"><span data-stu-id="157c4-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="157c4-135">Scaricare da impostazioni del servizio hello</span><span class="sxs-lookup"><span data-stu-id="157c4-135">Download from hello service settings</span></span>
1. <span data-ttu-id="157c4-136">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="157c4-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="157c4-137">A sinistra di hello, selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="157c4-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="157c4-138">Fare doppio clic sull'istanza di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="157c4-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="157c4-139">Al clic superiore hello **Configura**</span><span class="sxs-lookup"><span data-stu-id="157c4-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="157c4-140">In Multi-Factor Authentication selezionare **Gestisci impostazioni del servizio**
   ![Download](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="157c4-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="157c4-141">Nella pagina Impostazioni servizi hello in basso hello hello fare clic su **Go toohello portale**.</span><span class="sxs-lookup"><span data-stu-id="157c4-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="157c4-142">Viene aperta una nuova pagina.</span><span class="sxs-lookup"><span data-stu-id="157c4-142">A new page opens.</span></span>
   <span data-ttu-id="157c4-143">![Scaricare](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="157c4-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="157c4-144">Scegliere a sinistra, nella parte inferiore di hello, hello **SDK**.</span><span class="sxs-lookup"><span data-stu-id="157c4-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="157c4-145">Selezionare una lingua hello desiderata e fare clic sui collegamenti di download associati hello uno.</span><span class="sxs-lookup"><span data-stu-id="157c4-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="157c4-146">Salvare il download di hello.</span><span class="sxs-lookup"><span data-stu-id="157c4-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="157c4-147">Novità in hello SDK</span><span class="sxs-lookup"><span data-stu-id="157c4-147">What's in hello SDK</span></span>
<span data-ttu-id="157c4-148">Hello SDK include hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="157c4-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="157c4-149">**README**.</span><span class="sxs-lookup"><span data-stu-id="157c4-149">**README**.</span></span> <span data-ttu-id="157c4-150">Viene illustrato come toouse hello API di autenticazione a più fattori in un'applicazione nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="157c4-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="157c4-151">**File di origine** per Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="157c4-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="157c4-152">**Certificato client** utilizzare toocommunicate con hello servizio multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="157c4-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="157c4-153">**Chiave privata** certificato hello</span><span class="sxs-lookup"><span data-stu-id="157c4-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="157c4-154">**Risultati delle chiamate.**</span><span class="sxs-lookup"><span data-stu-id="157c4-154">**Call results.**</span></span> <span data-ttu-id="157c4-155">Un elenco di codici risultato chiamata.</span><span class="sxs-lookup"><span data-stu-id="157c4-155">A list of call result codes.</span></span> <span data-ttu-id="157c4-156">tooopen questo file, utilizzare un'applicazione con formattazione del testo, ad esempio WordPad.</span><span class="sxs-lookup"><span data-stu-id="157c4-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="157c4-157">Hello utilizzare tootest codici risultato chiamata e risoluzione dei problemi di implementazione di hello di multi-Factor Authentication nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="157c4-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="157c4-158">Non sono codici di stato di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="157c4-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="157c4-159">**Esempi.**</span><span class="sxs-lookup"><span data-stu-id="157c4-159">**Examples.**</span></span> <span data-ttu-id="157c4-160">Codice di esempio per un'implementazione di base funzionante di Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="157c4-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="157c4-161">certificato client hello è un certificato privato univoco generato per un utente.</span><span class="sxs-lookup"><span data-stu-id="157c4-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="157c4-162">Non condividere o perdere questo file.</span><span class="sxs-lookup"><span data-stu-id="157c4-162">Do not share or lose this file.</span></span> <span data-ttu-id="157c4-163">Se per la protezione di hello tooensuring chiave delle comunicazioni con il servizio multi-Factor Authentication hello.</span><span class="sxs-lookup"><span data-stu-id="157c4-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="157c4-164">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="157c4-164">Code sample</span></span>
<span data-ttu-id="157c4-165">In questo esempio di codice viene illustrato come toouse Ciao API hello vocale modalità standard di Azure multi-Factor Authentication SDK tooadd chiama applicazione tooyour di verifica.</span><span class="sxs-lookup"><span data-stu-id="157c4-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="157c4-166">Modalità standard è una chiamata telefonica che hello tooby risponde utente premendo il tasto di # hello.</span><span class="sxs-lookup"><span data-stu-id="157c4-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="157c4-167">In questo esempio utilizza hello c# .NET 2.0 multi-Factor Authentication SDK in un'applicazione ASP.NET di base con logica sul lato server c#, ma il processo di hello è simile in altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="157c4-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="157c4-168">Poiché hello SDK include file di origine, non eseguibili, è possibile compilare i file hello e farvi riferimento o includerli direttamente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="157c4-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="157c4-169">Quando si implementa multi-Factor Authentication, utilizzare metodi aggiuntivi di hello (telefonata o SMS) come toosupplement secondario e terziario verifica il metodo di autenticazione principale (nome utente e password).</span><span class="sxs-lookup"><span data-stu-id="157c4-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="157c4-170">Questi metodi non sono progettati come metodi di autenticazione principale.</span><span class="sxs-lookup"><span data-stu-id="157c4-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="157c4-171">Panoramica dell'esempio di codice</span><span class="sxs-lookup"><span data-stu-id="157c4-171">Code Sample Overview</span></span>
<span data-ttu-id="157c4-172">Questo codice di esempio per un'applicazione demo web semplice Usa una telefonata con un # risposta chiave tooverify hello autenticazione utente.</span><span class="sxs-lookup"><span data-stu-id="157c4-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="157c4-173">Questo fattore telefonata è noto in Multi-Factor Authentication come modalità standard.</span><span class="sxs-lookup"><span data-stu-id="157c4-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="157c4-174">codice sul lato client Hello non include tutti gli elementi specifici di multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="157c4-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="157c4-175">Fattori di autenticazione aggiuntivi hello sono indipendenti l'autenticazione principale hello, è possibile aggiungere senza modificare l'interfaccia hello esistente sign-on.</span><span class="sxs-lookup"><span data-stu-id="157c4-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="157c4-176">Ciao API hello multi-Factor SDK consentono di personalizzare l'esperienza utente hello, ma potrebbe non essere necessario toochange nulla affatto.</span><span class="sxs-lookup"><span data-stu-id="157c4-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="157c4-177">il codice lato server Hello aggiunge l'autenticazione in modalità standard nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="157c4-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="157c4-178">Crea un oggetto PfAuthParams con parametri hello che sono necessari per la verifica in modalità standard: nome utente, numero e la modalità di telefono e hello percorso toohello certificato client (CertFilePath), che è obbligatorio in ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="157c4-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="157c4-179">Per una dimostrazione di tutti i parametri PfAuthParams, vedere il file di esempio hello in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="157c4-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="157c4-180">Successivamente, il codice di hello passa hello PfAuthParams oggetto toohello pf_authenticate() una funzione.</span><span class="sxs-lookup"><span data-stu-id="157c4-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="157c4-181">valore restituito di Hello indica hello riuscita o meno dell'autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="157c4-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="157c4-182">Hello parametri, callStatus e errorID, contengono le informazioni sul risultato chiamata aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="157c4-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="157c4-183">i codici risultato chiamata Hello sono documentati nel file di risultati di chiamata hello in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="157c4-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="157c4-184">Questa implementazione minima può essere scritta in poche righe.</span><span class="sxs-lookup"><span data-stu-id="157c4-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="157c4-185">Nel codice di produzione, tuttavia, è necessario includere la gestione degli errori più sofisticati, il codice di database aggiuntivo e un'esperienza utente avanzata.</span><span class="sxs-lookup"><span data-stu-id="157c4-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="157c4-186">Codice client web</span><span class="sxs-lookup"><span data-stu-id="157c4-186">Web Client Code</span></span>
<span data-ttu-id="157c4-187">Hello seguito è riportato il codice client web per una pagina demo.</span><span class="sxs-lookup"><span data-stu-id="157c4-187">hello following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="157c4-188">Codice lato server</span><span class="sxs-lookup"><span data-stu-id="157c4-188">Server-Side Code</span></span>
<span data-ttu-id="157c4-189">Nel seguente codice lato server di hello, multi-Factor Authentication è configurato ed eseguire nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="157c4-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="157c4-190">Modalità standard (MODE_STANDARD) è che un utente di hello toowhich telefonata risponde premendo il tasto di # hello.</span><span class="sxs-lookup"><span data-stu-id="157c4-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
