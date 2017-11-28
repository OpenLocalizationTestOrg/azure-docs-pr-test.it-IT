---
title: Guida alla risoluzione dei problemi di Esplora archivi aaaAzure | Documenti Microsoft
description: "Panoramica della funzionalità di debug hello due di Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 5152f70418707d65c0a4bce9a916336829956219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="955c2-103">Guida alla risoluzione dei problemi di Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="955c2-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="955c2-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="955c2-104">Introduction</span></span>

<span data-ttu-id="955c2-105">Esplora archivi di Microsoft Azure (anteprima) è un'app autonoma che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="955c2-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="955c2-106">app Hello possono connettersi toStorage account ospitato in Azure, cloud statali e Stack di Azure.</span><span class="sxs-lookup"><span data-stu-id="955c2-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="955c2-107">In questa guida sono riepilogate le soluzioni per gli errori comuni riscontrati in Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="955c2-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="955c2-108">Problemi relativi all'accesso</span><span class="sxs-lookup"><span data-stu-id="955c2-108">Sign in issues</span></span>

<span data-ttu-id="955c2-109">Prima di continuare, provare a riavviare l'applicazione e verificare che i problemi di hello possono essere risolti.</span><span class="sxs-lookup"><span data-stu-id="955c2-109">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="955c2-110">Errore: certificato autofirmato nella catena di certificati</span><span class="sxs-lookup"><span data-stu-id="955c2-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="955c2-111">Esistono diversi motivi, perché questo errore può verificarsi, e due motivi più comuni hello sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="955c2-111">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="955c2-112">app Hello viene connesso tramite un "proxy trasparente", ovvero un server (ad esempio, il server aziendale) è intercetta il traffico HTTPS, la decrittografia e quindi crittografarlo utilizzando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="955c2-112">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="955c2-113">Si esegue un'applicazione, ad esempio software antivirus, che è inserendo messaggi hello HTTPS che si ricevano un certificato SSL autofirmato.</span><span class="sxs-lookup"><span data-stu-id="955c2-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="955c2-114">Quando Esplora archivi rileva uno dei problemi di hello, può non sapere se è stata manomessa messaggio HTTPS hello ricevuto.</span><span class="sxs-lookup"><span data-stu-id="955c2-114">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="955c2-115">Se si dispone di una copia del certificato autofirmato hello, è possibile utilizzare Esplora archivi di verificare l'attendibilità.</span><span class="sxs-lookup"><span data-stu-id="955c2-115">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="955c2-116">Se si è certi di chi esegue l'inserimento dei certificati di hello, seguire questi passaggi toofind è:</span><span class="sxs-lookup"><span data-stu-id="955c2-116">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="955c2-117">Installare Open SSL</span><span class="sxs-lookup"><span data-stu-id="955c2-117">Install Open SSL</span></span>

    - <span data-ttu-id="955c2-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (qualsiasi versione di hello chiaro dovrebbe essere sufficiente)</span><span class="sxs-lookup"><span data-stu-id="955c2-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="955c2-119">Mac e Linux: devono essere inclusi nel sistema operativo</span><span class="sxs-lookup"><span data-stu-id="955c2-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="955c2-120">Eseguire Open SSL</span><span class="sxs-lookup"><span data-stu-id="955c2-120">Run Open SSL</span></span>

    - <span data-ttu-id="955c2-121">Windows: aprire la directory di installazione di hello, fare clic su **/bin/**, quindi fare doppio clic su **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="955c2-121">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="955c2-122">Mac e Linux: eseguire **openssl** da un terminale.</span><span class="sxs-lookup"><span data-stu-id="955c2-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="955c2-123">Eseguire s_client -showcerts -connect microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="955c2-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="955c2-124">Cercare i certificati autofirmati.</span><span class="sxs-lookup"><span data-stu-id="955c2-124">Look for self-signed certificates.</span></span> <span data-ttu-id="955c2-125">Se si è certi che sono autofirmati, cercare in un punto qualsiasi oggetto hello ("s") e sono hello (ricerca per categorie ":") dell'autorità di certificazione stessa.</span><span class="sxs-lookup"><span data-stu-id="955c2-125">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="955c2-126">Dopo aver individuato i certificati autofirmati, ciascuno di essi, copiare e incollare tutto da **---BEGIN CERTIFICATE---** troppo**---END CERTIFICATE---** tooa nuovo file con estensione cer.</span><span class="sxs-lookup"><span data-stu-id="955c2-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="955c2-127">Aprire Esplora risorse di archiviazione, fare clic su **modifica** > **i certificati SSL** > **importazione certificati**e quindi utilizzare hello file selezione toofind, select, e aprire i file con estensione cer hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="955c2-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="955c2-128">Se non si trova alcun certificato autofirmato utilizzando hello sopra passaggi, contattare Microsoft tramite lo strumento di feedback hello per ulteriore assistenza.</span><span class="sxs-lookup"><span data-stu-id="955c2-128">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="955c2-129">Non è possibile tooretrieve sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="955c2-129">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="955c2-130">Se si è grado tooretrieve le sottoscrizioni dopo l'accesso, seguire questo problema tootroubleshoot questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="955c2-130">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="955c2-131">Verificare che l'account disponga di accesso toohello sottoscrizioni effettuando l'accesso al portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-131">Verify that your account has access toohello subscriptions by signing into hello Azure Portal.</span></span>

- <span data-ttu-id="955c2-132">Assicurarsi di aver effettuato utilizzando l'ambiente corretto di hello (Azure, Cina di Azure, Azure in Germania, Azure del governo o Stack ambiente/Azure personalizzato).</span><span class="sxs-lookup"><span data-stu-id="955c2-132">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="955c2-133">Se ci si trova dietro un proxy, assicurarsi che il proxy di Esplora archivi hello è stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="955c2-133">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="955c2-134">Provare a rimuovere e nuova aggiunta account hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-134">Try removing and readding hello account.</span></span>

- <span data-ttu-id="955c2-135">Provare a eliminare hello i seguenti file dalla directory radice (vale a dire C:\Users\ContosoUser) e quindi aggiungere nuovamente l'account hello:</span><span class="sxs-lookup"><span data-stu-id="955c2-135">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="955c2-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="955c2-136">.adalcache</span></span>

    - <span data-ttu-id="955c2-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="955c2-137">.devaccounts</span></span>

    - <span data-ttu-id="955c2-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="955c2-138">.extaccounts</span></span>

- <span data-ttu-id="955c2-139">Console di strumenti per sviluppatori hello espressioni di controllo (premendo F12) quando si esegue l'accesso per i messaggi di errore:</span><span class="sxs-lookup"><span data-stu-id="955c2-139">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![strumenti per sviluppatori](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="955c2-141">Pagina di autenticazione non è possibile toosee hello</span><span class="sxs-lookup"><span data-stu-id="955c2-141">Unable toosee hello authentication page</span></span>

<span data-ttu-id="955c2-142">Nel caso di pagina di autenticazione non è possibile toosee hello, seguire questo problema tootroubleshoot questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="955c2-142">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="955c2-143">A seconda della velocità di hello della connessione, potrebbe richiedere alcuni minuti per tooload nella pagina di accesso hello, attendere almeno un minuto prima di chiudere la finestra di dialogo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-143">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="955c2-144">Se ci si trova dietro un proxy, assicurarsi che il proxy di Esplora archivi hello è stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="955c2-144">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="955c2-145">Console per sviluppatori di hello visualizzazione premendo tasto F12 hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-145">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="955c2-146">Controllare le risposte hello dalla console per sviluppatori hello e vedere se è possibile trovare qualsiasi indicazione per questo motivo l'autenticazione non funziona.</span><span class="sxs-lookup"><span data-stu-id="955c2-146">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="955c2-147">Impossibile rimuovere l'account</span><span class="sxs-lookup"><span data-stu-id="955c2-147">Cannot remove account</span></span>

<span data-ttu-id="955c2-148">Se si è grado tooremove un account o hello Riesegui autenticazione collegamento non ha alcun effetto, seguire questo problema tootroubleshoot questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="955c2-148">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="955c2-149">Provare a eliminare hello i seguenti file dalla directory radice e quindi nuova aggiunta account hello:</span><span class="sxs-lookup"><span data-stu-id="955c2-149">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="955c2-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="955c2-150">.adalcache</span></span>

    - <span data-ttu-id="955c2-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="955c2-151">.devaccounts</span></span>

    - <span data-ttu-id="955c2-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="955c2-152">.extaccounts</span></span>

- <span data-ttu-id="955c2-153">Se si desidera tooremove SAS associata alle risorse di archiviazione, eliminare i seguenti file hello:</span><span class="sxs-lookup"><span data-stu-id="955c2-153">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="955c2-154">la cartella %AppData%/StorageExplorer per Windows</span><span class="sxs-lookup"><span data-stu-id="955c2-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="955c2-155">/Utenti/<your_name>/Library/Applicaiton SUpport/StorageExplorer per Mac</span><span class="sxs-lookup"><span data-stu-id="955c2-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="955c2-156">~/.config/StorageExplorer per Linux</span><span class="sxs-lookup"><span data-stu-id="955c2-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="955c2-157">Sarà necessario tooreenter tutte le credenziali se si eliminano questi file.</span><span class="sxs-lookup"><span data-stu-id="955c2-157">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="955c2-158">Problemi di proxy</span><span class="sxs-lookup"><span data-stu-id="955c2-158">Proxy issues</span></span>

<span data-ttu-id="955c2-159">Verificare innanzitutto che hello le seguenti informazioni immesse siano tutti corretti:</span><span class="sxs-lookup"><span data-stu-id="955c2-159">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="955c2-160">Hello URL del proxy e la porta numero</span><span class="sxs-lookup"><span data-stu-id="955c2-160">hello proxy URL and port number</span></span>

- <span data-ttu-id="955c2-161">Nome utente e password se richiesto dal proxy hello</span><span class="sxs-lookup"><span data-stu-id="955c2-161">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="955c2-162">soluzioni comuni</span><span class="sxs-lookup"><span data-stu-id="955c2-162">Common solutions</span></span>

<span data-ttu-id="955c2-163">Se si verificano ancora problemi, seguire questi passaggi tootroubleshoot loro:</span><span class="sxs-lookup"><span data-stu-id="955c2-163">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="955c2-164">Se è possibile connettersi toohello Internet senza utilizzare il proxy, verificare che funziona con Esplora archivi senza le impostazioni proxy abilitate.</span><span class="sxs-lookup"><span data-stu-id="955c2-164">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="955c2-165">In caso di hello, potrebbe esserci un problema con le impostazioni del proxy.</span><span class="sxs-lookup"><span data-stu-id="955c2-165">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="955c2-166">Funziona con i problemi di hello tooidentify amministratore proxy.</span><span class="sxs-lookup"><span data-stu-id="955c2-166">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="955c2-167">Verificare che altre applicazioni che utilizzano server proxy hello funzionino come previsto.</span><span class="sxs-lookup"><span data-stu-id="955c2-167">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="955c2-168">Verificare che sia possibile connettersi il portale di Microsoft Azure toohello tramite il web browser</span><span class="sxs-lookup"><span data-stu-id="955c2-168">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="955c2-169">Verificare di poter ricevere le risposte dagli endpoint del servizio.</span><span class="sxs-lookup"><span data-stu-id="955c2-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="955c2-170">Immettere uno degli URL dell'endpoint nel browser.</span><span class="sxs-lookup"><span data-stu-id="955c2-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="955c2-171">Se è possibile connettersi, si dovrebbe ricevere InvalidQueryParameterValue o una risposta XML simile.</span><span class="sxs-lookup"><span data-stu-id="955c2-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="955c2-172">Se anche altre persone usano Storage Explorer con il server proxy, accertarsi che riescano a connettersi.</span><span class="sxs-lookup"><span data-stu-id="955c2-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="955c2-173">Se è possibile connettersi, è possibile toocontact l'amministratore del server proxy.</span><span class="sxs-lookup"><span data-stu-id="955c2-173">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="955c2-174">Strumenti per la diagnosi dei problemi</span><span class="sxs-lookup"><span data-stu-id="955c2-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="955c2-175">Se si dispone di strumenti di rete, ad esempio Fiddler per Windows, i problemi di hello toodiagnose in grado di può essere come segue:</span><span class="sxs-lookup"><span data-stu-id="955c2-175">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="955c2-176">Se si dispone di toowork tramite il proxy, è possibile tooconfigure il tooconnect strumento rete tramite proxy hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-176">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="955c2-177">Controllare il numero di porta hello utilizzato per lo strumento di rete.</span><span class="sxs-lookup"><span data-stu-id="955c2-177">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="955c2-178">Immettere l'URL host locale hello e numero di porta dello strumento di rete come le impostazioni proxy in Esplora archivi hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-178">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="955c2-179">Se questo isdone correttamente, lo strumento rete inizia la registrazione delle richieste di rete dagli endpoint di servizio e toomanagement Esplora archivi.</span><span class="sxs-lookup"><span data-stu-id="955c2-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="955c2-180">Ad esempio, immettere https://cawablobgrs.blob.core.windows.net/ per l'endpoint blob in un browser e si riceverà una risposta è simile al seguente hello, che suggerisce risorsa hello è presente, anche se non è possibile accedere.</span><span class="sxs-lookup"><span data-stu-id="955c2-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![esempio di codice](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="955c2-182">Contattare l'amministratore del server proxy</span><span class="sxs-lookup"><span data-stu-id="955c2-182">Contact proxy server admin</span></span>

<span data-ttu-id="955c2-183">Se le impostazioni proxy siano corrette, è possibile toocontact l'amministratore del server proxy, e</span><span class="sxs-lookup"><span data-stu-id="955c2-183">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="955c2-184">Assicurarsi che il proxy non blocchi il traffico tooAzure management o risorsa gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="955c2-184">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="955c2-185">Verificare il protocollo di autenticazione hello del server proxy.</span><span class="sxs-lookup"><span data-stu-id="955c2-185">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="955c2-186">Storage Explorer attualmente non supporta i proxy NTLM.</span><span class="sxs-lookup"><span data-stu-id="955c2-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="955c2-187">Messaggio di errore "Impossibile tooRetrieve figli"</span><span class="sxs-lookup"><span data-stu-id="955c2-187">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="955c2-188">Se si è connessi tooAzure tramite un proxy, verificare che le impostazioni proxy siano corrette.</span><span class="sxs-lookup"><span data-stu-id="955c2-188">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="955c2-189">Se si sono state concesse accesso tooa risorsa dal proprietario hello di hello sottoscrizione o l'account, verificare di avere letto o elencare le autorizzazioni per tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="955c2-189">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="955c2-190">Problemi relativi all'URL SAS</span><span class="sxs-lookup"><span data-stu-id="955c2-190">Issues with SAS URL</span></span>
<span data-ttu-id="955c2-191">Se ci si connette tooa servizio tramite un URL SAS e verifica l'errore:</span><span class="sxs-lookup"><span data-stu-id="955c2-191">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="955c2-192">Verificare che l'URL di hello fornisca delle autorizzazioni necessarie hello tooread o un elenco di risorse.</span><span class="sxs-lookup"><span data-stu-id="955c2-192">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="955c2-193">Verificare che hello che URL non sia scaduto.</span><span class="sxs-lookup"><span data-stu-id="955c2-193">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="955c2-194">Se hello URL SAS è basata su criteri di accesso, verificare che i criteri di accesso hello non è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="955c2-194">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="955c2-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="955c2-195">Next steps</span></span>

<span data-ttu-id="955c2-196">Se nessuna delle soluzioni di hello risolvere il problema, inviare il problema tramite lo strumento di feedback hello con messaggio di posta elettronica e il numero di dettagli sul problema hello incluso come si può, in modo che possiamo contattarti per risolvere il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="955c2-196">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="955c2-197">toodo, fare clic su **Guida** menu e quindi fare clic su **Invia commenti e suggerimenti**.</span><span class="sxs-lookup"><span data-stu-id="955c2-197">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Commenti e suggerimenti](./media/storage-explorer-troubleshooting/4022503_en_1.png)
