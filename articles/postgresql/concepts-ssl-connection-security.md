---
title: "Configurare la connettività SSL nel Database di Azure per PostgreSQL | Microsoft Docs"
description: Indicazioni e informazioni per configurare il Database di Azure per PostgreSQL e delle applicazioni associate per usare correttamente le connessioni SSL.
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 685aa4c2f75b7c3260ca737f7c786157480b2d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="27f1e-103">Configurare la connettività SSL nel Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="27f1e-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="27f1e-104">Il Database di Azure per PostgreSQL preferisce connettere le applicazioni client al servizio di PostgreSQL usando la connettività SSL (Secure Sockets Layer).</span><span class="sxs-lookup"><span data-stu-id="27f1e-104">Azure Database for PostgreSQL prefers connecting your client applications to the PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="27f1e-105">L'applicazione delle connessioni SSL tra il server di database e le applicazioni client aiuta a proteggersi dagli attacchi "man in the middle" crittografando il flusso di dati tra il server e l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="27f1e-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

<span data-ttu-id="27f1e-106">Per impostazione predefinita, il servizio di database PostgreSQL è configurato per richiedere la connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="27f1e-106">By default, the PostgreSQL database service is configured to require SSL connection.</span></span> <span data-ttu-id="27f1e-107">Se l'applicazione client non supporta la connettività SSL, si è liberi di disabilitare l'opzione di richiesta SSL per la connessione al servizio di database.</span><span class="sxs-lookup"><span data-stu-id="27f1e-107">Optionally, you can disable requiring SSL for connecting to your database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="27f1e-108">Applicazione delle connessioni SSL</span><span class="sxs-lookup"><span data-stu-id="27f1e-108">Enforcing SSL connections</span></span>
<span data-ttu-id="27f1e-109">Per impostazione predefinita, l'opzione di applicazione delle connessioni SSL è attiva quando si esegue il provisioning di tutti i Database di Azure per i server PostgreSQL attraverso l'interfaccia della riga di comando e il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="27f1e-109">For all Azure Database for PostgreSQL servers provisioned through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="27f1e-110">Analogamente, le stringhe di connessione predefinite nelle impostazioni "Stringhe di connessione" per il server nel portale di Azure includono i parametri obbligatori per le lingue comuni per effettuare la connessione al server di database tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="27f1e-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="27f1e-111">Il parametro SSL varia in base al connettore, ad esempio "ssl=true", "sslmode=require" oppure "sslmode=required" e altre varianti.</span><span class="sxs-lookup"><span data-stu-id="27f1e-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="27f1e-112">Configurare l'applicazione di SSL</span><span class="sxs-lookup"><span data-stu-id="27f1e-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="27f1e-113">Facoltativamente, è possibile disabilitare l'applicazione della connettività SSL.</span><span class="sxs-lookup"><span data-stu-id="27f1e-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="27f1e-114">Microsoft Azure consiglia di abilitare sempre l'impostazione **Enforce SSL connection** (Applica connessione SSL) per una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="27f1e-114">Microsoft Azure recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="27f1e-115">Uso del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="27f1e-115">Using the Azure portal</span></span>
<span data-ttu-id="27f1e-116">Visitare il Database di Azure per il server PostgreSQL e fare clic su **Sicurezza connessione**.</span><span class="sxs-lookup"><span data-stu-id="27f1e-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="27f1e-117">Usare l'interruttore per abilitare o disabilitare l'impostazione **Applica connessione SSL**.</span><span class="sxs-lookup"><span data-stu-id="27f1e-117">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="27f1e-118">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="27f1e-118">Then click **Save**.</span></span> 

![Sicurezza connessione - Disabilitare l'applicazione di SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="27f1e-120">È possibile confermare l'impostazione aprendo la pagina **Panoramica** per visualizzare l'indicatore **SSL enforce status** (Stato di applicazione di SSL).</span><span class="sxs-lookup"><span data-stu-id="27f1e-120">You can confirm the setting by viewing the **Overview** page to see the **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="27f1e-121">Utilizzare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="27f1e-121">Using Azure CLI</span></span>
<span data-ttu-id="27f1e-122">È possibile abilitare o disabilitare il parametro **ssl-enforcement** usando rispettivamente i valori `Enabled` o `Disabled` nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="27f1e-122">You can enable or disable the **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="27f1e-123">Verificare che le connessioni SSL siano supportate dall'applicazione o dal framework</span><span class="sxs-lookup"><span data-stu-id="27f1e-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="27f1e-124">Per impostazione predefinita, molti framework di applicazione comuni che usano i servizi PostgreSQL per database, quali Drupal e Django, non abilitano SSL durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="27f1e-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="27f1e-125">L'abilitazione della connettività SSL deve essere eseguita dopo l'installazione o tramite i comandi dell'interfaccia della riga di comando specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="27f1e-125">Enabling SSL connectivity must be done after installation or through CLI commands specific to the application.</span></span> <span data-ttu-id="27f1e-126">Se il server PostgreSQL applica le connessioni SSL e l'applicazione associata non è configurata correttamente, l'applicazione potrebbe non riuscire a connettersi al server di database.</span><span class="sxs-lookup"><span data-stu-id="27f1e-126">If your PostgreSQL server is enforcing SSL connections and the associated application is not configured properly, the application may fail to connect to your database server.</span></span> <span data-ttu-id="27f1e-127">Consultare la documentazione dell'applicazione per le informazioni su come abilitare le connessioni SSL.</span><span class="sxs-lookup"><span data-stu-id="27f1e-127">Consult your application's documentation to learn how to enable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="27f1e-128">Applicazioni che richiedono la verifica del certificato per la connettività SSL</span><span class="sxs-lookup"><span data-stu-id="27f1e-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="27f1e-129">In alcuni casi, le applicazioni richiedono un file del certificato locale generato da un file di certificato (.cer) dell'autorità di certificazione (CA) attendibile per connettersi in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="27f1e-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) to connect securely.</span></span> <span data-ttu-id="27f1e-130">Vedere la procedura seguente per ottenere il file .cer, decodificare il certificato e associarlo all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="27f1e-130">See the following steps to obtain the .cer file, decode the certificate and bind it to your application.</span></span>

### <a name="download-the-certificate-file-from-the-certificate-authority-ca"></a><span data-ttu-id="27f1e-131">Scaricare il file del certificato dall'autorità di certificazione (CA)</span><span class="sxs-lookup"><span data-stu-id="27f1e-131">Download the certificate file from the Certificate Authority (CA)</span></span> 
<span data-ttu-id="27f1e-132">Il certificato richiesto per comunicare con il Database di Azure per il server PostgreSQL tramite SSL si trova [qui](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="27f1e-132">The certificate needed to communicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="27f1e-133">Scaricare il file del certificato e salvarlo in locale.</span><span class="sxs-lookup"><span data-stu-id="27f1e-133">Download the certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="27f1e-134">Scaricare e installare OpenSSL sul computer</span><span class="sxs-lookup"><span data-stu-id="27f1e-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="27f1e-135">Per decodificare il file del certificato richiesto dall'applicazione per connettersi al server di database in modo sicuro, è necessario installare OpenSSL sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="27f1e-135">To decode the certificate file needed for your application to connect securely to your database server, you need to install OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="27f1e-136">Per Linux, OS X o Unix</span><span class="sxs-lookup"><span data-stu-id="27f1e-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="27f1e-137">Le librerie OpenSSL vengono distribuite nel codice sorgente direttamente da [OpenSSL Software Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="27f1e-137">The OpenSSL libraries are provided in source code directly from the [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="27f1e-138">Le istruzioni seguenti consentono di eseguire i passaggi necessari per installare OpenSSL nel computer Linux.</span><span class="sxs-lookup"><span data-stu-id="27f1e-138">The following instructions guide you through the steps necessary to install OpenSSL on your Linux PC.</span></span> <span data-ttu-id="27f1e-139">In questo articolo vengono usati i comandi noti per lavorare su Ubuntu 12.04 (e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="27f1e-139">This article uses commands known to work on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="27f1e-140">Aprire una sessione terminal e installare OpenSSL</span><span class="sxs-lookup"><span data-stu-id="27f1e-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="27f1e-141">Estrarre i file dal pacchetto di download</span><span class="sxs-lookup"><span data-stu-id="27f1e-141">Extract the files from the download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="27f1e-142">Specificare la directory in cui sono stati estratti i file.</span><span class="sxs-lookup"><span data-stu-id="27f1e-142">Enter the directory where the files were extracted.</span></span> <span data-ttu-id="27f1e-143">Per impostazione predefinita, deve essere come segue.</span><span class="sxs-lookup"><span data-stu-id="27f1e-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="27f1e-144">Configurare OpenSSL eseguendo il comando indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="27f1e-144">Configure OpenSSL by executing the following command.</span></span> <span data-ttu-id="27f1e-145">Se si desidera collocare i file in una cartella diversa da /usr/local/openssl, assicurarsi di modificare quanto segue in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="27f1e-145">If you want the files in a folder different than /usr/local/openssl, make sure to change the following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="27f1e-146">Ora che OpenSSL è stato configurato correttamente, è necessario compilarlo per convertire il certificato.</span><span class="sxs-lookup"><span data-stu-id="27f1e-146">Now that OpenSSL is configured properly, you need to compile it to convert your certificate.</span></span> <span data-ttu-id="27f1e-147">A tale scopo, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="27f1e-147">To compile, run the following command:</span></span>

```bash
make
```
<span data-ttu-id="27f1e-148">Al termine della compilazione è possibile installare OpenSSL come eseguibile con questo comando:</span><span class="sxs-lookup"><span data-stu-id="27f1e-148">Once compiling is complete, you're ready to install OpenSSL as an executable by running the following command:</span></span>
```bash
make install
```
<span data-ttu-id="27f1e-149">Per confermare di aver installato correttamente OpenSSL nel sistema, eseguire il comando seguente e assicurarsi di ottenere lo stesso output.</span><span class="sxs-lookup"><span data-stu-id="27f1e-149">To confirm that you've successfully installed OpenSSL on your system, run the following command and check to make sure you get the same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="27f1e-150">In caso affermativo, si dovrebbe vedere il messaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="27f1e-150">If successful you should see the following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="27f1e-151">Per Windows</span><span class="sxs-lookup"><span data-stu-id="27f1e-151">For Windows</span></span>
<span data-ttu-id="27f1e-152">L'installazione di OpenSSL in un PC Windows può essere eseguita nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="27f1e-152">Installing OpenSSL on a Windows PC can be done in the following ways:</span></span>
1. <span data-ttu-id="27f1e-153">**(Scelta consigliata)** Usando la funzionalità Bash per Windows disponibile in Windows 10 e versioni successive, OpenSSL viene installato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="27f1e-153">**(Recommended)** Using the built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="27f1e-154">Le istruzioni su come abilitare la funzionalità Bash per Windows in Windows 10 sono disponibili [qui](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="27f1e-154">Instructions on how to enable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="27f1e-155">Tramite il download di un'applicazione Win32/64 bit fornita dalla community.</span><span class="sxs-lookup"><span data-stu-id="27f1e-155">Through downloading a Win32/64 application provided by the community.</span></span> <span data-ttu-id="27f1e-156">Pur non offrendo o avallando eventuali programmi di installazione di Windows specifici, OpenSSL Software Foundation offre un elenco dei programmi di installazione disponibili [qui](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="27f1e-156">While the OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="27f1e-157">Decodificare il file del certificato</span><span class="sxs-lookup"><span data-stu-id="27f1e-157">Decode your certificate file</span></span>
<span data-ttu-id="27f1e-158">Il file CA radice scaricato è in formato crittografato.</span><span class="sxs-lookup"><span data-stu-id="27f1e-158">The downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="27f1e-159">Usare OpenSSL per decodificare il file del certificato.</span><span class="sxs-lookup"><span data-stu-id="27f1e-159">Use OpenSSL to decode the certificate file.</span></span> <span data-ttu-id="27f1e-160">Per farlo, eseguire questo comando OpenSSL:</span><span class="sxs-lookup"><span data-stu-id="27f1e-160">To do so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-to-azure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="27f1e-161">Connessione al Database di Azure per PostgreSQL con autenticazione del certificato SSL</span><span class="sxs-lookup"><span data-stu-id="27f1e-161">Connecting to Azure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="27f1e-162">Ora che il certificato è stato decodificato correttamente, è possibile connettersi al server di database in modo protetto tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="27f1e-162">Now that you have successfully decoded your certificate, you can now connect to your database server securely over SSL.</span></span> <span data-ttu-id="27f1e-163">Per consentire la verifica dei certificati server, il certificato deve essere posizionato nel file ~/.postgresql/root.crt nella directory home dell'utente.</span><span class="sxs-lookup"><span data-stu-id="27f1e-163">To allow server certificate verification, the certificate must be placed in the file ~/.postgresql/root.crt in the user's home directory.</span></span> <span data-ttu-id="27f1e-164">Su Microsoft Windows il file è denominato % APPDATA%\postgresql\root.crt.</span><span class="sxs-lookup"><span data-stu-id="27f1e-164">(On Microsoft Windows the file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="27f1e-165">Di seguito vengono fornite le istruzioni per connettersi al Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="27f1e-165">The following provides instructions for connecting to Azure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="27f1e-166">Attualmente si verifica un problema noto se si usa "sslmode = verify-full" nella connessione al servizio, ovvero la connessione avrà esito negativo con un errore indicante che il _certificato del server per "&lt;area&gt;.control.database.windows.net" (e 7 altri nomi) non corrisponde al nome host "&lt;servername&gt;.postgres.database.azure.com"._</span><span class="sxs-lookup"><span data-stu-id="27f1e-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection to the service, the connection will fail with the following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="27f1e-167">Se è obbligatorio usare la modalità "sslmode=verify-full", usare la convenzione di denominazione server  **&lt;nomeserver&gt;.database.windows.net** come nome host della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="27f1e-167">If "sslmode=verify-full" is required, please use the server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="27f1e-168">In futuro questa limitazione verrà rimossa.</span><span class="sxs-lookup"><span data-stu-id="27f1e-168">We plan to remove this limitation in the future.</span></span> <span data-ttu-id="27f1e-169">Le connessioni che usano altre [modalità SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) devono continuare a usare la convenzione di denominazione host preferita  **&lt;nomeserver&gt;.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="27f1e-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue to use the preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="27f1e-170">Uso dell'utilità della riga di comando PSQL</span><span class="sxs-lookup"><span data-stu-id="27f1e-170">Using psql command-line utility</span></span>
<span data-ttu-id="27f1e-171">L'esempio seguente illustra come connettersi al server PostgreSQL tramite l'utilità della riga di comando PSQL.</span><span class="sxs-lookup"><span data-stu-id="27f1e-171">The following example shows you how to successfully connect to your PostgreSQL server using the psql command-line utility.</span></span> <span data-ttu-id="27f1e-172">Usare il file `root.crt` creato e `sslmode=verify-ca` o l'opzione `sslmode=verify-full`.</span><span class="sxs-lookup"><span data-stu-id="27f1e-172">Use the `root.crt` file created and the `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="27f1e-173">Usando l'interfaccia della riga di comando di PostgreSQL, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="27f1e-173">Using the PostgreSQL command-line interface, execute the following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="27f1e-174">Se l'operazione va a buon fine, si dovrebbe ottenere l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="27f1e-174">If successful, you receive the following output:</span></span>
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="27f1e-175">Uso dello strumento GUI pgAdmin</span><span class="sxs-lookup"><span data-stu-id="27f1e-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="27f1e-176">La configurazione di pgAdmin 4 per connettersi in modo sicuro tramite SSL richiede l'impostazione di `SSL mode = Verify-CA` o `SSL mode = Verify-Full` nel modo indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="27f1e-176">Configuring pgAdmin 4 to connect securely over SSL requires you to set the `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Schermata di pgAdmin - connessione - modalità SSL richiesta](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="27f1e-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27f1e-178">Next steps</span></span>
<span data-ttu-id="27f1e-179">Esaminare varie opzioni di connettività dell'applicazione secondo [Raccolte connessioni per il Database di Azure per PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="27f1e-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
