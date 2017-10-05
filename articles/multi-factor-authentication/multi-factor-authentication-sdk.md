---
title: Software Development Kit MFA per le app personalizzate | Microsoft Docs
description: In questo articolo viene spiegato come scaricare e usare l'SDK MFA di Azure per abilitare la verifica in due passaggi per le app personalizzate.
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
ms.openlocfilehash: 281f9c61a30a20027f69808600373aa272255ef6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="daf27-103">Compilazione di Multi-Factor Authentication in app personalizzate (SDK)</span><span class="sxs-lookup"><span data-stu-id="daf27-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="daf27-104">Il Software Development Kit (SDK) di Azure Multi-Factor Authentication consente di compilare la verifica in due passaggi direttamente nei processi di accesso o di transazione delle applicazioni nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="daf27-104">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="daf27-105">L'SDK di Multi-Factor Authentication è disponibile per C#, Visual Basic (.NET), Java, Perl, PHP e Ruby.</span><span class="sxs-lookup"><span data-stu-id="daf27-105">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="daf27-106">L'SDK fornisce un wrapper sottile per la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="daf27-106">The SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="daf27-107">Include tutto ciò che occorre per scrivere il codice, inclusi i file di codice sorgente commentati, i file di esempio e un file ReadMe dettagliato.</span><span class="sxs-lookup"><span data-stu-id="daf27-107">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="daf27-108">Ogni SDK include anche un certificato e una chiave privata univoci per il provider Multi-Factor Authentication per crittografare le transazioni.</span><span class="sxs-lookup"><span data-stu-id="daf27-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="daf27-109">Fino a quando si dispone di un provider, è possibile scaricare l'SDK in tutti i formati e le lingue necessari.</span><span class="sxs-lookup"><span data-stu-id="daf27-109">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="daf27-110">La struttura delle API nell'SDK di Multi-Factor Authentication è semplice.</span><span class="sxs-lookup"><span data-stu-id="daf27-110">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="daf27-111">Eseguire una sola funzione di chiamata a un'API con i parametri di opzione a più fattori (ad esempio la modalità di verifica) e dati utente (come il numero di telefono da chiamare o il numero PIN da convalidare).</span><span class="sxs-lookup"><span data-stu-id="daf27-111">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span></span> <span data-ttu-id="daf27-112">Le API convertono la chiamata di funzione in richieste di servizi web per il servizio Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="daf27-112">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="daf27-113">Tutte le chiamate devono includere un riferimento al certificato privato incluso in ogni SDK.</span><span class="sxs-lookup"><span data-stu-id="daf27-113">All calls must include a reference to the private certificate that is included in every SDK.</span></span>

<span data-ttu-id="daf27-114">Poiché le API non hanno accesso agli utenti registrati in Azure Active Directory, è necessario fornire le informazioni sull'utente in un file o database.</span><span class="sxs-lookup"><span data-stu-id="daf27-114">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="daf27-115">Inoltre, le API non forniscono funzionalità di gestione di registrazione o dell'utente, pertanto è necessario creare questi processi nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="daf27-115">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="daf27-116">Per scaricare l'SDK, è necessario creare un provider di Azure Multi-Factor Authentication, anche se si dispone di licenze di Azure MFA, AAD Premium o EMS.</span><span class="sxs-lookup"><span data-stu-id="daf27-116">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="daf27-117">Se si crea un provider di Azure Multi-Factor Authentication a tale scopo e si dispone già di licenze, creare il provider con il modello **Per utente abilitato**.</span><span class="sxs-lookup"><span data-stu-id="daf27-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="daf27-118">Collegare quindi il Provider alla directory contenente le licenze di Azure MFA, Azure AD Premium o EMS.</span><span class="sxs-lookup"><span data-stu-id="daf27-118">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="daf27-119">Con questa configurazione verranno eseguiti addebiti solo se il numero di utenti singoli che usano l'SDK è maggiore del numero di licenze possedute.</span><span class="sxs-lookup"><span data-stu-id="daf27-119">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span></span>


## <a name="download-the-sdk"></a><span data-ttu-id="daf27-120">Scaricare l'SDK</span><span class="sxs-lookup"><span data-stu-id="daf27-120">Download the SDK</span></span>
<span data-ttu-id="daf27-121">Per scaricare l'SDK Multi-Factor di Azure è necessario un [provider di Multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="daf27-121">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="daf27-122">Questo richiede una sottoscrizione di Azure completa, anche se si possiedono licenze di Azure MFA, Azure AD Premium o Enterprise Mobility Suite.</span><span class="sxs-lookup"><span data-stu-id="daf27-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="daf27-123">Per scaricare l'SDK, accedere al portale di gestione Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="daf27-123">To download the SDK, navigate to the Multi-Factor Management Portal.</span></span> <span data-ttu-id="daf27-124">È possibile accedere al portale gestendo direttamente il provider di Multi-Factor Authentication o facendo clic sul collegamento **Vai al portale** nella pagina delle impostazioni del servizio MFA.</span><span class="sxs-lookup"><span data-stu-id="daf27-124">You can reach the portal either by managing the Multi-Factor Auth Provider directly, or by clicking the **"Go to the portal"** link on the MFA service settings page.</span></span>

### <a name="download-from-the-azure-classic-portal"></a><span data-ttu-id="daf27-125">Download dal portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="daf27-125">Download from the Azure classic portal</span></span>
1. <span data-ttu-id="daf27-126">Accedere al [portale di Azure classico](https://manage.windowsazure.com) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="daf27-126">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="daf27-127">A sinistra, selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="daf27-127">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="daf27-128">Nella parte superiore della pagina Active Directory selezionare **Provider di Autenticazione a più fattori**</span><span class="sxs-lookup"><span data-stu-id="daf27-128">On the Active Directory page, at the top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="daf27-129">Nella parte inferiore selezionare **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="daf27-129">At the bottom select **Manage**.</span></span> <span data-ttu-id="daf27-130">Viene aperta una nuova pagina.</span><span class="sxs-lookup"><span data-stu-id="daf27-130">A new page opens.</span></span>
5. <span data-ttu-id="daf27-131">A sinistra, nella parte inferiore, fare clic su **SDK**.</span><span class="sxs-lookup"><span data-stu-id="daf27-131">On the left, at the bottom, click **SDK**.</span></span>
   <span data-ttu-id="daf27-132"><center>![Scaricare](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="daf27-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="daf27-133">Selezionare la lingua desiderata e fare clic su uno dei collegamenti di download associati.</span><span class="sxs-lookup"><span data-stu-id="daf27-133">Select the language you want and click one the associated download links.</span></span>
7. <span data-ttu-id="daf27-134">Salvare il download.</span><span class="sxs-lookup"><span data-stu-id="daf27-134">Save the download.</span></span>

### <a name="download-from-the-service-settings"></a><span data-ttu-id="daf27-135">Download dalle impostazioni del servizio</span><span class="sxs-lookup"><span data-stu-id="daf27-135">Download from the service settings</span></span>
1. <span data-ttu-id="daf27-136">Accedere al [portale di Azure classico](https://manage.windowsazure.com) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="daf27-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="daf27-137">A sinistra, selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="daf27-137">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="daf27-138">Fare doppio clic sull'istanza di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="daf27-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="daf27-139">Nella parte superiore fare clic su **Configura**</span><span class="sxs-lookup"><span data-stu-id="daf27-139">At the top click **Configure**</span></span>
5. <span data-ttu-id="daf27-140">In Multi-Factor Authentication selezionare **Gestisci impostazioni del servizio**
   ![Download](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="daf27-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="daf27-141">Nella parte inferiore della schermata della pagina Impostazioni servizio, fare clic su **Vai al portale**.</span><span class="sxs-lookup"><span data-stu-id="daf27-141">On the services settings page, at the bottom of the screen click **Go to the portal**.</span></span> <span data-ttu-id="daf27-142">Viene aperta una nuova pagina.</span><span class="sxs-lookup"><span data-stu-id="daf27-142">A new page opens.</span></span>
   <span data-ttu-id="daf27-143">![Scaricare](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="daf27-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="daf27-144">A sinistra, nella parte inferiore, fare clic su **SDK**.</span><span class="sxs-lookup"><span data-stu-id="daf27-144">On the left, at the bottom, click **SDK**.</span></span>
8. <span data-ttu-id="daf27-145">Selezionare la lingua desiderata e fare clic su uno dei collegamenti di download associati.</span><span class="sxs-lookup"><span data-stu-id="daf27-145">Select the language you want and click one the associated download links.</span></span>
9. <span data-ttu-id="daf27-146">Salvare il download.</span><span class="sxs-lookup"><span data-stu-id="daf27-146">Save the download.</span></span>

## <a name="whats-in-the-sdk"></a><span data-ttu-id="daf27-147">Contenuto dell'SDK</span><span class="sxs-lookup"><span data-stu-id="daf27-147">What's in the SDK</span></span>
<span data-ttu-id="daf27-148">L'SDK include gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="daf27-148">The SDK includes the following items:</span></span>

* <span data-ttu-id="daf27-149">**README**.</span><span class="sxs-lookup"><span data-stu-id="daf27-149">**README**.</span></span> <span data-ttu-id="daf27-150">Viene illustrato come usare le API di Multi-Factor Authentication in un'applicazione nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="daf27-150">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="daf27-151">**File di origine** per Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="daf27-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="daf27-152">**Certificato client** usato per comunicare con il servizio Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="daf27-152">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span></span>
* <span data-ttu-id="daf27-153">**Chiave privata** per il certificato</span><span class="sxs-lookup"><span data-stu-id="daf27-153">**Private key** for the certificate</span></span>
* <span data-ttu-id="daf27-154">**Risultati delle chiamate.**</span><span class="sxs-lookup"><span data-stu-id="daf27-154">**Call results.**</span></span> <span data-ttu-id="daf27-155">Un elenco di codici risultato chiamata.</span><span class="sxs-lookup"><span data-stu-id="daf27-155">A list of call result codes.</span></span> <span data-ttu-id="daf27-156">Per aprire questo file, usare un'applicazione con formattazione del testo, come ad esempio WordPad.</span><span class="sxs-lookup"><span data-stu-id="daf27-156">To open this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="daf27-157">Usare i codici risultato chiamata per verificare e risolvere l'implementazione di autenticazione Multi-Factor Authentication nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="daf27-157">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="daf27-158">Non sono codici di stato di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="daf27-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="daf27-159">**Esempi.**</span><span class="sxs-lookup"><span data-stu-id="daf27-159">**Examples.**</span></span> <span data-ttu-id="daf27-160">Codice di esempio per un'implementazione di base funzionante di Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="daf27-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="daf27-161">Il certificato client è un certificato privato univoco generato per un utente specifico.</span><span class="sxs-lookup"><span data-stu-id="daf27-161">The client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="daf27-162">Non condividere o perdere questo file.</span><span class="sxs-lookup"><span data-stu-id="daf27-162">Do not share or lose this file.</span></span> <span data-ttu-id="daf27-163">È la chiave per garantire la sicurezza delle comunicazioni con il servizio di autenticazione Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="daf27-163">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="daf27-164">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="daf27-164">Code sample</span></span>
<span data-ttu-id="daf27-165">Questo esempio di codice illustra come usare le API nell'SDK di Azure Multi-Factor Authentication per aggiungere all'applicazione una verifica tramite chiamata vocale in modalità standard.</span><span class="sxs-lookup"><span data-stu-id="daf27-165">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span></span> <span data-ttu-id="daf27-166">La modalità standard è una telefonata a cui l'utente risponde premendo il tasto #.</span><span class="sxs-lookup"><span data-stu-id="daf27-166">Standard mode is a telephone call that the user responds to by pressing the # key.</span></span>

<span data-ttu-id="daf27-167">In questo esempio viene usato l'SDK di Multi-Factor Authentication C# .NET 2.0 in un'applicazione ASP.NET con logica sul lato server C#, ma il processo è simile in altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="daf27-167">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span></span> <span data-ttu-id="daf27-168">Poiché l'SDK include file di origine, file non eseguibili, è possibile compilare i file e farvi riferimento o includerli direttamente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="daf27-168">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="daf27-169">Quando si implementa Multi-Factor Authentication, usare i metodi aggiuntivi (telefonata o SMS) come verifica secondaria o terziaria per integrare il metodo di autenticazione principale (nome utente e password).</span><span class="sxs-lookup"><span data-stu-id="daf27-169">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span></span> <span data-ttu-id="daf27-170">Questi metodi non sono progettati come metodi di autenticazione principale.</span><span class="sxs-lookup"><span data-stu-id="daf27-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="daf27-171">Panoramica dell'esempio di codice</span><span class="sxs-lookup"><span data-stu-id="daf27-171">Code Sample Overview</span></span>
<span data-ttu-id="daf27-172">Questo codice di esempio per un'applicazione demo Web semplice usa una chiamata con risposta mediante il tasto # per verificare l'autenticazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="daf27-172">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span></span> <span data-ttu-id="daf27-173">Questo fattore telefonata è noto in Multi-Factor Authentication come modalità standard.</span><span class="sxs-lookup"><span data-stu-id="daf27-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="daf27-174">Il codice sul lato client non include elementi specifici di autenticazione Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="daf27-174">The client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="daf27-175">Poiché i fattori di autenticazione aggiuntivi sono indipendenti dall'autenticazione principale, è possibile aggiungerli senza modificare l'interfaccia di accesso esistente.</span><span class="sxs-lookup"><span data-stu-id="daf27-175">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span></span> <span data-ttu-id="daf27-176">Le API negli SDK di Multi-Factor consentono di personalizzare l'esperienza dell'utente, ma potrebbe non essere necessario apportare alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="daf27-176">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span></span>

<span data-ttu-id="daf27-177">Il codice lato server aggiunge l'autenticazione in modalità standard nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="daf27-177">The server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="daf27-178">Crea un oggetto PfAuthParams con i parametri necessari per la verifica della modalità standard: nome utente, numero, modalità e il percorso verso il certificato del client (CertFilePath), che è necessario in ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="daf27-178">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="daf27-179">Per una dimostrazione di tutti i parametri in PfAuthParams, vedere il file di esempio nel SDK.</span><span class="sxs-lookup"><span data-stu-id="daf27-179">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span></span>

<span data-ttu-id="daf27-180">Successivamente, il codice passa l'oggetto PfAuthParams alla funzione pf_authenticate().</span><span class="sxs-lookup"><span data-stu-id="daf27-180">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span></span> <span data-ttu-id="daf27-181">Il valore restituito indica l'esito positivo o negativo dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="daf27-181">The return value indicates the success or failure of the authentication.</span></span> <span data-ttu-id="daf27-182">I parametri out, callStatus ed errorID, contengono informazioni aggiuntive sul risultato della chiamata.</span><span class="sxs-lookup"><span data-stu-id="daf27-182">The out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="daf27-183">I codici di risultato della chiamata sono documentati nel file dei risultati della chiamata nel SDK.</span><span class="sxs-lookup"><span data-stu-id="daf27-183">The call result codes are documented in the call results file in the SDK.</span></span>

<span data-ttu-id="daf27-184">Questa implementazione minima può essere scritta in poche righe.</span><span class="sxs-lookup"><span data-stu-id="daf27-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="daf27-185">Nel codice di produzione, tuttavia, è necessario includere la gestione degli errori più sofisticati, il codice di database aggiuntivo e un'esperienza utente avanzata.</span><span class="sxs-lookup"><span data-stu-id="daf27-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="daf27-186">Codice client web</span><span class="sxs-lookup"><span data-stu-id="daf27-186">Web Client Code</span></span>
<span data-ttu-id="daf27-187">Di seguito è riportato il codice di client web per una pagina demo.</span><span class="sxs-lookup"><span data-stu-id="daf27-187">The following is web client code for a demo page.</span></span>

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


### <a name="server-side-code"></a><span data-ttu-id="daf27-188">Codice lato server</span><span class="sxs-lookup"><span data-stu-id="daf27-188">Server-Side Code</span></span>
<span data-ttu-id="daf27-189">Nel seguente codice lato server, la Multi-Factor Authentication è configurata ed eseguita nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="daf27-189">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="daf27-190">La modalità standard (MODE_STANDARD) è una telefonata a cui l'utente risponde premendo il tasto #.</span><span class="sxs-lookup"><span data-stu-id="daf27-190">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span></span>

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
            // Step 1: Validate the username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from the user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains the private key for the client
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
