---
title: Guida alla risoluzione dei problemi di Azure Storage Explorer | Microsoft Docs
description: "Panoramica delle due funzionalità di debug di Azure"
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
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: e9b833b07556378f17d9aaff0912c7d73dff44eb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="01baf-103">Guida alla risoluzione dei problemi di Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="01baf-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="01baf-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="01baf-104">Introduction</span></span>

<span data-ttu-id="01baf-105">Microsoft Azure Storage Explorer (anteprima) è un'app autonoma che consente di usare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="01baf-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="01baf-106">L'app può connettersi ad account di archiviazione ospitati in Azure, Sovereign Clouds e Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="01baf-106">The app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="01baf-107">In questa guida sono riepilogate le soluzioni per gli errori comuni riscontrati in Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="01baf-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="01baf-108">Problemi relativi all'accesso</span><span class="sxs-lookup"><span data-stu-id="01baf-108">Sign in issues</span></span>

<span data-ttu-id="01baf-109">Sono supportati solo account AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="01baf-109">Only Azure Active Directory (AAD) accounts are supported.</span></span> <span data-ttu-id="01baf-110">Se si usa un account ADFS, è probabile che l'accesso a Storage Explorer non funzioni.</span><span class="sxs-lookup"><span data-stu-id="01baf-110">If you use an ADFS account, it’s expected that signing in to Storage Explorer would not work.</span></span> <span data-ttu-id="01baf-111">Prima di continuare, provare a riavviare l'applicazione per vedere se i problemi si risolvono.</span><span class="sxs-lookup"><span data-stu-id="01baf-111">Before you continue, try restarting your application and see whether the problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="01baf-112">Errore: certificato autofirmato nella catena di certificati</span><span class="sxs-lookup"><span data-stu-id="01baf-112">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="01baf-113">Esistono diversi motivi per cui è possibile riscontrare questo errore. I due motivi più comuni sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="01baf-113">There are several reasons why you may encounter this error, and the most common two reasons are as follows:</span></span>

1. <span data-ttu-id="01baf-114">L'app è connessa tramite un "proxy trasparente", ovvero un server, ad esempio il server aziendale, che intercetta il traffico HTTPS, ne esegue la decrittografia e la crittografia con un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="01baf-114">The app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="01baf-115">Viene eseguita un'applicazione, ad esempio un software antivirus, che inserisce un certificato SSL autofirmato nei messaggi HTTPS ricevuti.</span><span class="sxs-lookup"><span data-stu-id="01baf-115">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into the HTTPS messages that you receive.</span></span>

<span data-ttu-id="01baf-116">Quando Storage Explorer rileva un problema, è possibile che l'informazione relativa alla possibile manomissione del messaggio HTTPS ricevuto non sia nota.</span><span class="sxs-lookup"><span data-stu-id="01baf-116">When Storage Explorer encounters one of the issues, it can no longer know whether the received HTTPS message is tampered.</span></span> <span data-ttu-id="01baf-117">Se si dispone di una copia del certificato autofirmato, è possibile fare in modo che Storage Explorer li consideri attendibili.</span><span class="sxs-lookup"><span data-stu-id="01baf-117">If you have a copy of the self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="01baf-118">Se non si conosce l'autore dell'inserimento del certificato, seguire questi passaggi per trovarlo:</span><span class="sxs-lookup"><span data-stu-id="01baf-118">If you are unsure of who is injecting the certificate, follow these steps to find it:</span></span>

1. <span data-ttu-id="01baf-119">Installare Open SSL</span><span class="sxs-lookup"><span data-stu-id="01baf-119">Install Open SSL</span></span>

    - <span data-ttu-id="01baf-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html), una delle versioni light dovrebbe essere sufficiente</span><span class="sxs-lookup"><span data-stu-id="01baf-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions should be sufficient)</span></span>

    - <span data-ttu-id="01baf-121">Mac e Linux: devono essere inclusi nel sistema operativo</span><span class="sxs-lookup"><span data-stu-id="01baf-121">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="01baf-122">Eseguire Open SSL</span><span class="sxs-lookup"><span data-stu-id="01baf-122">Run Open SSL</span></span>

    - <span data-ttu-id="01baf-123">Windows: aprire la directory di installazione, fare clic su **/bin/**, quindi fare doppio clic su **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="01baf-123">Windows: open the installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="01baf-124">Mac e Linux: eseguire **openssl** da un terminale.</span><span class="sxs-lookup"><span data-stu-id="01baf-124">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="01baf-125">Eseguire s_client -showcerts -connect microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="01baf-125">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="01baf-126">Cercare i certificati autofirmati.</span><span class="sxs-lookup"><span data-stu-id="01baf-126">Look for self-signed certificates.</span></span> <span data-ttu-id="01baf-127">Se si è certi di quali certificati sono autofirmati, verificare ovunque che l'oggetto ("s") e l'autorità emittente ("i:") siano uguali.</span><span class="sxs-lookup"><span data-stu-id="01baf-127">If you are unsure which are self-signed, look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>

5. <span data-ttu-id="01baf-128">Dopo aver trovato i certificati autofirmati, per ognuno di essi, copiare e incollare tutto da e includendo **-----BEGIN CERTIFICATE-----** a **-----END CERTIFICATE-----** in un nuovo file con estensione CER.</span><span class="sxs-lookup"><span data-stu-id="01baf-128">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file.</span></span>

6. <span data-ttu-id="01baf-129">Aprire Storage Explorer, fare clic su **Modifica** > **Certificati SSL** > **Importa certificati**, quindi usare la selezione file per trovare, selezionare e aprire i file con estensione CER creati.</span><span class="sxs-lookup"><span data-stu-id="01baf-129">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use the file picker to find, select, and open the .cer files that you created.</span></span>

<span data-ttu-id="01baf-130">Se non è possibile trovare alcun certificato autofirmato seguendo i passaggi precedenti, contattare Microsoft tramite lo strumento di feedback per ricevere assistenza.</span><span class="sxs-lookup"><span data-stu-id="01baf-130">If you cannot find any self-signed certificates using the above steps, contact us through the feedback tool for more help.</span></span>

### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="01baf-131">Impossibile recuperare le sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="01baf-131">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="01baf-132">Se non è possibile recuperare le sottoscrizioni dopo aver eseguito correttamente l'accesso, seguire questi passaggi per risolvere questo problema:</span><span class="sxs-lookup"><span data-stu-id="01baf-132">If you are unable to retrieve your subscriptions after you successfully sign in, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="01baf-133">Verificare che l'account abbia accesso alle sottoscrizioni effettuando l'accesso al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="01baf-133">Verify that your account has access to the subscriptions by signing into the Azure portal.</span></span>

- <span data-ttu-id="01baf-134">Assicurarsi di aver effettuato l'accesso usando l'ambiente corretto, ad esempio Azure, Azure Cina, Azure Germania, Azure Governo degli Stati Uniti o Ambiente personalizzato/Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="01baf-134">Make sure that you have signed in using the correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="01baf-135">Se si è protetti da un proxy, assicurarsi che il proxy Storage Explorer sia stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="01baf-135">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="01baf-136">Provare a rimuovere e a aggiungere nuovamente l'account.</span><span class="sxs-lookup"><span data-stu-id="01baf-136">Try removing and readding the account.</span></span>

- <span data-ttu-id="01baf-137">Provare a eliminare i file seguenti dalla directory radice, ovvero, C:\Utenti\ContosoUser, e quindi aggiungere nuovamente l'account:</span><span class="sxs-lookup"><span data-stu-id="01baf-137">Try deleting the following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding the account:</span></span>

    - <span data-ttu-id="01baf-138">.adalcache</span><span class="sxs-lookup"><span data-stu-id="01baf-138">.adalcache</span></span>

    - <span data-ttu-id="01baf-139">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="01baf-139">.devaccounts</span></span>

    - <span data-ttu-id="01baf-140">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="01baf-140">.extaccounts</span></span>

- <span data-ttu-id="01baf-141">Controllare la console degli strumenti per sviluppatori premendo F12 quando si esegue l'accesso per i messaggi di errore:</span><span class="sxs-lookup"><span data-stu-id="01baf-141">Watch the developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![strumenti per sviluppatori](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="01baf-143">Impossibile visualizzare la pagina di autenticazione</span><span class="sxs-lookup"><span data-stu-id="01baf-143">Unable to see the authentication page</span></span>

<span data-ttu-id="01baf-144">Se non si riesce a visualizzare la pagina di autenticazione, seguire questi passaggi per risolvere questo problema:</span><span class="sxs-lookup"><span data-stu-id="01baf-144">If you are unable to see the authentication page, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="01baf-145">A seconda della velocità della connessione, il caricamento della pagina di accesso potrebbe richiedere un po' di tempo, attendere almeno un minuto prima di chiudere la finestra di dialogo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="01baf-145">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog box.</span></span>

- <span data-ttu-id="01baf-146">Se si è protetti da un proxy, assicurarsi che il proxy Storage Explorer sia stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="01baf-146">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="01baf-147">Visualizzare la console per sviluppatori premendo il tasto F12.</span><span class="sxs-lookup"><span data-stu-id="01baf-147">View the developer console by pressing the F12 key.</span></span> <span data-ttu-id="01baf-148">Controllare le risposte nella console per sviluppatori per trovare informazioni sul mancato funzionamento dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="01baf-148">Watch the responses from the developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="01baf-149">Impossibile rimuovere l'account</span><span class="sxs-lookup"><span data-stu-id="01baf-149">Cannot remove account</span></span>

<span data-ttu-id="01baf-150">Se non è possibile rimuovere un account o se il collegamento per eseguire nuovamente l'autenticazione non esegue alcuna operazione, attenersi alla seguente procedura per risolvere questo problema:</span><span class="sxs-lookup"><span data-stu-id="01baf-150">If you are unable to remove an account, or if the reauthenticate link does not do anything, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="01baf-151">Provare a eliminare i file seguenti dalla directory radice e quindi aggiungere nuovamente l'account:</span><span class="sxs-lookup"><span data-stu-id="01baf-151">Try deleting the following files from your root directory, and then readding the account:</span></span>

    - <span data-ttu-id="01baf-152">.adalcache</span><span class="sxs-lookup"><span data-stu-id="01baf-152">.adalcache</span></span>

    - <span data-ttu-id="01baf-153">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="01baf-153">.devaccounts</span></span>

    - <span data-ttu-id="01baf-154">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="01baf-154">.extaccounts</span></span>

- <span data-ttu-id="01baf-155">Se si desidera rimuovere le risorse di archiviazione collegate al SAS, eliminare i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="01baf-155">If you want to remove SAS attached Storage resources, delete the following files:</span></span>

    - <span data-ttu-id="01baf-156">la cartella %AppData%/StorageExplorer per Windows</span><span class="sxs-lookup"><span data-stu-id="01baf-156">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="01baf-157">/Utenti/<your_name>/Library/Applicaiton SUpport/StorageExplorer per Mac</span><span class="sxs-lookup"><span data-stu-id="01baf-157">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="01baf-158">~/.config/StorageExplorer per Linux</span><span class="sxs-lookup"><span data-stu-id="01baf-158">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="01baf-159">Se si eliminano questi file è necessario immettere nuovamente tutte le credenziali.</span><span class="sxs-lookup"><span data-stu-id="01baf-159">You will have to reenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="01baf-160">Problemi di proxy</span><span class="sxs-lookup"><span data-stu-id="01baf-160">Proxy issues</span></span>

<span data-ttu-id="01baf-161">In primo luogo, assicurarsi che le informazioni seguenti immesse siano corrette:</span><span class="sxs-lookup"><span data-stu-id="01baf-161">First, make sure that the following information you entered are all correct:</span></span>

- <span data-ttu-id="01baf-162">l'URL del proxy e il numero di porta</span><span class="sxs-lookup"><span data-stu-id="01baf-162">The proxy URL and port number</span></span>

- <span data-ttu-id="01baf-163">nome utente e password se richiesto dal proxy</span><span class="sxs-lookup"><span data-stu-id="01baf-163">Username and password if required by the proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="01baf-164">soluzioni comuni</span><span class="sxs-lookup"><span data-stu-id="01baf-164">Common solutions</span></span>

<span data-ttu-id="01baf-165">Se si verificano ancora problemi, attenersi alla procedura seguente per risolverli:</span><span class="sxs-lookup"><span data-stu-id="01baf-165">If you are still experiencing issues, follow these steps to troubleshoot them:</span></span>

- <span data-ttu-id="01baf-166">Se è possibile connettersi a Internet senza usare il proxy, verificare che Storage Explorer funzioni senza le impostazioni del proxy abilitate.</span><span class="sxs-lookup"><span data-stu-id="01baf-166">If you can connect to the Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="01baf-167">In questo caso, potrebbe esserci un problema con le impostazioni del proxy.</span><span class="sxs-lookup"><span data-stu-id="01baf-167">If this is the case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="01baf-168">Rivolgersi all'amministratore del proxy per identificare i problemi.</span><span class="sxs-lookup"><span data-stu-id="01baf-168">Work with your proxy administrator to identify the problems.</span></span>

- <span data-ttu-id="01baf-169">Verificare che altre applicazioni che usano il server proxy funzionino come previsto.</span><span class="sxs-lookup"><span data-stu-id="01baf-169">Verify that other applications using the proxy server work as expected.</span></span>

- <span data-ttu-id="01baf-170">Verificare che sia possibile connettersi al portale di Microsoft Azure usando il Web browser</span><span class="sxs-lookup"><span data-stu-id="01baf-170">Verify that you can connect to the Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="01baf-171">Verificare di poter ricevere le risposte dagli endpoint del servizio.</span><span class="sxs-lookup"><span data-stu-id="01baf-171">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="01baf-172">Immettere uno degli URL dell'endpoint nel browser.</span><span class="sxs-lookup"><span data-stu-id="01baf-172">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="01baf-173">Se è possibile connettersi, si dovrebbe ricevere InvalidQueryParameterValue o una risposta XML simile.</span><span class="sxs-lookup"><span data-stu-id="01baf-173">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="01baf-174">Se anche altre persone usano Storage Explorer con il server proxy, accertarsi che riescano a connettersi.</span><span class="sxs-lookup"><span data-stu-id="01baf-174">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="01baf-175">Se questo non avviene, potrebbe essere necessario contattare l'amministratore del server proxy.</span><span class="sxs-lookup"><span data-stu-id="01baf-175">If they can connect, you may have to contact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="01baf-176">Strumenti per la diagnosi dei problemi</span><span class="sxs-lookup"><span data-stu-id="01baf-176">Tools for diagnosing issues</span></span>

<span data-ttu-id="01baf-177">Se si dispone di strumenti di rete, ad esempio Fiddler per Windows, è possibile diagnosticare i problemi come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="01baf-177">If you have networking tools, such as Fiddler for Windows, you may be able to diagnose the problems as follows:</span></span>

- <span data-ttu-id="01baf-178">Se si deve usare il proxy, è necessario configurare lo strumento di rete per connettersi tramite il proxy.</span><span class="sxs-lookup"><span data-stu-id="01baf-178">If you have to work through your proxy, you may have to configure your networking tool to connect through the proxy.</span></span>

- <span data-ttu-id="01baf-179">Controllare il numero della porta usato dallo strumento di rete.</span><span class="sxs-lookup"><span data-stu-id="01baf-179">Check the port number used by your networking tool.</span></span>

- <span data-ttu-id="01baf-180">Immettere l'URL dell'host locale e il numero della porta dello strumento di rete come impostazioni proxy in Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="01baf-180">Enter the local host URL and the networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="01baf-181">Se questa operazione viene eseguita correttamente, lo strumento di rete inizia la registrazione delle richieste di rete effettuate da Storage Explorer agli endpoint di gestione e del servizio.</span><span class="sxs-lookup"><span data-stu-id="01baf-181">If this is done correctly, your networking tool starts logging network requests made by Storage Explorer to management and service endpoints.</span></span> <span data-ttu-id="01baf-182">Ad esempio, immettere https://cawablobgrs.blob.core.windows.net/ per l'endpoint BLOB in un browser. Si riceverà una risposta simile alla seguente, che suggerisce che la risorsa è disponibile, anche se non è possibile accedervi.</span><span class="sxs-lookup"><span data-stu-id="01baf-182">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles the following, which suggests the resource exists, although you cannot access it.</span></span>

![esempio di codice](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="01baf-184">Contattare l'amministratore del server proxy</span><span class="sxs-lookup"><span data-stu-id="01baf-184">Contact proxy server admin</span></span>

<span data-ttu-id="01baf-185">Se le impostazioni del proxy sono corrette, è necessario contattare l'amministratore del server proxy e</span><span class="sxs-lookup"><span data-stu-id="01baf-185">If your proxy settings are correct, you may have to contact your proxy server admin, and</span></span>

- <span data-ttu-id="01baf-186">Assicurarsi che il proxy non blocchi il traffico agli endpoint di gestione o risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="01baf-186">Make sure that your proxy does not block traffic to Azure management or resource endpoints.</span></span>

- <span data-ttu-id="01baf-187">Verificare il protocollo di autenticazione usato dal server proxy.</span><span class="sxs-lookup"><span data-stu-id="01baf-187">Verify the authentication protocol used by your proxy server.</span></span> <span data-ttu-id="01baf-188">Storage Explorer attualmente non supporta i proxy NTLM.</span><span class="sxs-lookup"><span data-stu-id="01baf-188">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-to-retrieve-children-error-message"></a><span data-ttu-id="01baf-189">Messaggio di errore "Unable to Retrieve Children" (Impossibile recuperare gli elementi figlio)</span><span class="sxs-lookup"><span data-stu-id="01baf-189">"Unable to Retrieve Children" error message</span></span>

<span data-ttu-id="01baf-190">Se si è connessi ad Azure tramite un proxy, verificare che le impostazioni del proxy siano corrette.</span><span class="sxs-lookup"><span data-stu-id="01baf-190">If you are connected to Azure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="01baf-191">Se è stato concesso l'accesso a una risorsa dal proprietario della sottoscrizione o dell'account, verificare di avere letto o elencare le autorizzazioni per tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="01baf-191">If you were granted access to a resource from the owner of the subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="01baf-192">Problemi relativi all'URL SAS</span><span class="sxs-lookup"><span data-stu-id="01baf-192">Issues with SAS URL</span></span>
<span data-ttu-id="01baf-193">Se ci si connette a un servizio tramite un URL SAS e si verifica questo errore:</span><span class="sxs-lookup"><span data-stu-id="01baf-193">If you are connecting to a service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="01baf-194">Verificare che l'URL abbia le autorizzazioni necessarie per la lettura o l'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="01baf-194">Verify that the URL provides the necessary permissions to read or list resources.</span></span>

- <span data-ttu-id="01baf-195">Verificare che l'URL non sia scaduto.</span><span class="sxs-lookup"><span data-stu-id="01baf-195">Verify that the URL has not expired.</span></span>

- <span data-ttu-id="01baf-196">Se l'URL SAS si basa su un criterio di accesso, verificare che i criteri di accesso non siano stati revocati.</span><span class="sxs-lookup"><span data-stu-id="01baf-196">If the SAS URL is based on an access policy, verify that the access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01baf-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01baf-197">Next steps</span></span>

<span data-ttu-id="01baf-198">Se nessuna delle soluzioni funziona, comunicare il problema tramite lo strumento di feedback inserendo l'indirizzo di posta elettronica e il maggior numero di informazioni possibili, in modo che Microsoft possa contattare l'utente per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="01baf-198">If none of the solutions work for you, submit your issue through the feedback tool with your email and as many details about the issue included as you can, so that we can contact you for fixing the issue.</span></span>

<span data-ttu-id="01baf-199">A tale scopo, fare clic sul menu **Guida** e quindi fare clic su **Commenti e suggerimenti**.</span><span class="sxs-lookup"><span data-stu-id="01baf-199">To do this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Commenti e suggerimenti](./media/storage-explorer-troubleshooting/4022503_en_1.png)
