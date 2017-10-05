---
title: Distribuire un servizio di divisione e unione | Documentazione Microsoft
description: Suddivisione e unione con gli strumenti di database elastico
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6e2fea882c248fa095a9d450ed54a7b4e64b45e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="c8468-103">Distribuire un servizio di divisione e unione</span><span class="sxs-lookup"><span data-stu-id="c8468-103">Deploy a split-merge service</span></span>
<span data-ttu-id="c8468-104">Lo strumento di divisione e unione sposta i dati tra database partizionati.</span><span class="sxs-lookup"><span data-stu-id="c8468-104">The split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="c8468-105">Vedere [Spostamento di dati tra database cloud con numero maggiore di istanze](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="c8468-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-the-split-merge-packages"></a><span data-ttu-id="c8468-106">Scaricare i pacchetti di divisione e unione</span><span class="sxs-lookup"><span data-stu-id="c8468-106">Download the Split-Merge packages</span></span>
1. <span data-ttu-id="c8468-107">Scaricare la versione più recente di NuGet dal sito Web [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="c8468-107">Download the latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="c8468-108">Aprire un prompt dei comandi e passare alla directory in cui si è scaricato il file nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="c8468-108">Open a command prompt and navigate to the directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="c8468-109">Il download comprende comandi di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8468-109">The download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="c8468-110">Scaricare il pacchetto di divisione e unione più recente nella directory corrente usando il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="c8468-110">Download the latest Split-Merge package into the current directory with the below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="c8468-111">I file vengono inseriti in una directory denominata **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** dove *x.x.xxx.x* rappresenta il numero di versione.</span><span class="sxs-lookup"><span data-stu-id="c8468-111">The files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects the version number.</span></span> <span data-ttu-id="c8468-112">I file del servizio di divisione e unione si trovano nella sottodirectory **content\splitmerge\service** e gli script di PowerShell di divisione e unione (compresi i file DLL client necessari) si trovano nella sottodirectory **content\splitmerge\powershell**.</span><span class="sxs-lookup"><span data-stu-id="c8468-112">Find the split-merge Service files in the **content\splitmerge\service** sub-directory, and the Split-Merge PowerShell scripts (and required client .dlls) in the **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8468-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c8468-113">Prerequisites</span></span>
1. <span data-ttu-id="c8468-114">Creare un database SQL di Azure che verrà usato come database per lo stato di divisione e unione.</span><span class="sxs-lookup"><span data-stu-id="c8468-114">Create an Azure SQL DB database that will be used as the split-merge status database.</span></span> <span data-ttu-id="c8468-115">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c8468-115">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c8468-116">Creazione personalizzata di un nuovo **database SQL**.</span><span class="sxs-lookup"><span data-stu-id="c8468-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="c8468-117">Assegnare un nome al database e creare un nuovo amministratore e una password.</span><span class="sxs-lookup"><span data-stu-id="c8468-117">Give the database a name and create a new administrator and password.</span></span> <span data-ttu-id="c8468-118">Assicurarsi di prendere nota del nome e della password per l'uso successivo.</span><span class="sxs-lookup"><span data-stu-id="c8468-118">Be sure to record the name and password for later use.</span></span>
2. <span data-ttu-id="c8468-119">Assicurarsi che il server di database SQL di Azure consenta la connessione da parte dei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8468-119">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="c8468-120">Nel portale accedere a **Impostazioni firewall** e assicurarsi che l'impostazione **Consenti l'accesso a servizi di Azure** sia **attiva**.</span><span class="sxs-lookup"><span data-stu-id="c8468-120">In the portal, in the **Firewall Settings**, ensure that the **Allow access to Azure Services** setting is set to **On**.</span></span> <span data-ttu-id="c8468-121">Fare clic sull'icona "Salva".</span><span class="sxs-lookup"><span data-stu-id="c8468-121">Click the "save" icon.</span></span>
   
   ![Servizi consentiti][1]
3. <span data-ttu-id="c8468-123">Creare un account di archiviazione di Azure che verrà usato per l'output di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="c8468-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="c8468-124">Accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8468-124">Go to the Azure Portal.</span></span> <span data-ttu-id="c8468-125">Nella barra di sinistra fare clic su **Nuovo**, fare clic su **Dati e archiviazione** e quindi su **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="c8468-125">In the left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="c8468-126">Creare un servizio cloud di Azure che conterrà il servizio di divisione e unione.</span><span class="sxs-lookup"><span data-stu-id="c8468-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="c8468-127">Accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8468-127">Go to the Azure Portal.</span></span> <span data-ttu-id="c8468-128">Nella barra di sinistra fare clic su **Nuovo**, fare clic su **Calcolo**, **Servizio cloud** e quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c8468-128">In the left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="c8468-129">Configurare il servizio di divisione e unione</span><span class="sxs-lookup"><span data-stu-id="c8468-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="c8468-130">Configurazione del servizio di divisione e unione</span><span class="sxs-lookup"><span data-stu-id="c8468-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="c8468-131">Nella cartella in cui sono stati scaricati gli assembly necessari per la divisione e l'unione creare una copia del file **ServiceConfiguration.Template.cscfg** fornito con **SplitMergeService.cspkg** e rinominarlo **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="c8468-131">In the folder where you downloaded the Split-Merge assemblies, create a copy of the **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="c8468-132">Aprire **ServiceConfiguration.cscfg** in un editor di testo, ad esempio Visual Studio, che convalida input come il formato delle identificazioni personali del certificato.</span><span class="sxs-lookup"><span data-stu-id="c8468-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as the format of certificate thumbprints.</span></span>
3. <span data-ttu-id="c8468-133">Creare un nuovo database o scegliere un database esistente da usare come database per lo stato delle operazioni di divisione e unione, quindi recuperare la stringa di connessione del database.</span><span class="sxs-lookup"><span data-stu-id="c8468-133">Create a new database or choose an existing database to serve as the status database for Split-Merge operations and retrieve the connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="c8468-134">A questo punto, il database dello stato deve usare le regole di confronto Latin (SQL\_Latin1\_General\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="c8468-134">At this time, the status database must use the Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="c8468-135">Per ulteriori informazioni, vedere [Nome regole di confronto Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8468-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="c8468-136">Con il database SQL di Azure, la stringa di connessione presenta in genere un formato come il seguente:</span><span class="sxs-lookup"><span data-stu-id="c8468-136">With Azure SQL DB, the connection string typically is of the form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="c8468-137">Immettere la stringa di connessione nel file cscfg in entrambe le sezioni Role **SplitMergeWeb** e **SplitMergeWorker** dell'impostazione ElasticScaleMetadata.</span><span class="sxs-lookup"><span data-stu-id="c8468-137">Enter this connection string in the cscfg file in both the **SplitMergeWeb** and **SplitMergeWorker** role sections in the ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="c8468-138">Per il ruolo **SplitMergeWorker**, immettere una stringa di connessione valida nell'archiviazione di Azure per l'impostazione **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="c8468-138">For the **SplitMergeWorker** role, enter a valid connection string to Azure storage for the **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="c8468-139">Configurare la sicurezza</span><span class="sxs-lookup"><span data-stu-id="c8468-139">Configure security</span></span>
<span data-ttu-id="c8468-140">Per istruzioni dettagliate sulla configurazione della sicurezza del servizio, vedere l'articolo [Configurazione di sicurezza per suddivisione-unione](sql-database-elastic-scale-split-merge-security-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="c8468-140">For detailed instructions to configure the security of the service, refer to the [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="c8468-141">Ai fini di una semplice distribuzione di prova per questa esercitazione, verrà completata una serie minima di passaggi di configurazione per la messa in funzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="c8468-141">For the purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed to get the service up and running.</span></span> <span data-ttu-id="c8468-142">Questi passaggi abilitano unicamente il computer/l'account che li esegue alla comunicazione con il servizio.</span><span class="sxs-lookup"><span data-stu-id="c8468-142">These steps enable only the one machine/account executing them to communicate with the service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="c8468-143">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="c8468-143">Create a self-signed certificate</span></span>
<span data-ttu-id="c8468-144">Creare una nuova directory e, da questa, eseguire il seguente comando usando una finestra del [prompt dei comandi per gli sviluppatori per Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) :</span><span class="sxs-lookup"><span data-stu-id="c8468-144">Create a new directory and from this directory execute the following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="c8468-145">Verrà richiesta una password per proteggere la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="c8468-145">You are asked for a password to protect the private key.</span></span> <span data-ttu-id="c8468-146">Immettere una password complessa e confermarla.</span><span class="sxs-lookup"><span data-stu-id="c8468-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="c8468-147">Dopo questo passaggio, verrà richiesto di usare la password una volta ancora.</span><span class="sxs-lookup"><span data-stu-id="c8468-147">You are then prompted for the password to be used once more after that.</span></span> <span data-ttu-id="c8468-148">Fare clic su **Sì** alla fine per importarla nell'archivio delle Autorità di certificazione radice disponibili nell'elenco locale.</span><span class="sxs-lookup"><span data-stu-id="c8468-148">Click **Yes** at the end to import it to the Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="c8468-149">Creare un file PFX</span><span class="sxs-lookup"><span data-stu-id="c8468-149">Create a PFX file</span></span>
<span data-ttu-id="c8468-150">Eseguire il seguente comando dalla stessa finestra in cui è stato eseguito makecert. Servirsi della stessa password usata per la creazione del certificato:</span><span class="sxs-lookup"><span data-stu-id="c8468-150">Execute the following command from the same window where makecert was executed; use the same password that you used to create the certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-the-client-certificate-into-the-personal-store"></a><span data-ttu-id="c8468-151">Importare il certificato client nell'archivio personale</span><span class="sxs-lookup"><span data-stu-id="c8468-151">Import the client certificate into the personal store</span></span>
1. <span data-ttu-id="c8468-152">In Esplora risorse fare doppio clic su **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="c8468-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="c8468-153">Nell'**Importazione guidata certificati** selezionare **Utente corrente** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c8468-153">In the **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="c8468-154">Confermare il percorso del file e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c8468-154">Confirm the file path and click **Next**.</span></span>
4. <span data-ttu-id="c8468-155">Digitare la password, lasciare selezionata l'opzione **Includi tutte le proprietà estese** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c8468-155">Type the password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="c8468-156">Lasciare selezionata l'opzione **Seleziona automaticamente l'archivio certificati […]** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c8468-156">Leave **Automatically select the certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="c8468-157">Fare clic su **Fine**, quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8468-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-the-pfx-file-to-the-cloud-service"></a><span data-ttu-id="c8468-158">Caricare il file PFX nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="c8468-158">Upload the PFX file to the cloud service</span></span>
1. <span data-ttu-id="c8468-159">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c8468-159">Go to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c8468-160">Selezionare **Servizi cloud**.</span><span class="sxs-lookup"><span data-stu-id="c8468-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="c8468-161">Selezionare il servizio cloud creato precedentemente per il servizio di divisione e unione.</span><span class="sxs-lookup"><span data-stu-id="c8468-161">Select the cloud service you created above for the Split/Merge service.</span></span>
4. <span data-ttu-id="c8468-162">Scegliere **Certificati** dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="c8468-162">Click **Certificates** on the top menu.</span></span>
5. <span data-ttu-id="c8468-163">Fare clic su **Carica** nella barra inferiore.</span><span class="sxs-lookup"><span data-stu-id="c8468-163">Click **Upload** in the bottom bar.</span></span>
6. <span data-ttu-id="c8468-164">Selezionare il file PFX e immettere la stessa password usata sopra.</span><span class="sxs-lookup"><span data-stu-id="c8468-164">Select the PFX file and enter the same password as above.</span></span>
7. <span data-ttu-id="c8468-165">Una volta completata l'operazione, copiare l'identificazione personale del certificato dalla nuova voce nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="c8468-165">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

### <a name="update-the-service-configuration-file"></a><span data-ttu-id="c8468-166">Aggiornare il file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="c8468-166">Update the service configuration file</span></span>
<span data-ttu-id="c8468-167">Incollare l'identificazione personale del certificato copiata sopra nell'attributo identificazione personale/valore delle seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="c8468-167">Paste the certificate thumbprint copied above into the thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="c8468-168">Per il ruolo di lavoro:</span><span class="sxs-lookup"><span data-stu-id="c8468-168">For the worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="c8468-169">Per il ruolo Web:</span><span class="sxs-lookup"><span data-stu-id="c8468-169">For the web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="c8468-170">Si noti che per distribuzioni destinate alla produzione è necessario usare certificati separati per CA, crittografia, server e client.</span><span class="sxs-lookup"><span data-stu-id="c8468-170">Please note that for production deployments separate certificates should be used for the CA, for encryption, the Server certificate and client certificates.</span></span> <span data-ttu-id="c8468-171">Per istruzioni dettagliate, vedere l'articolo relativo alla [configurazione della sicurezza](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="c8468-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="c8468-172">Distribuire il servizio</span><span class="sxs-lookup"><span data-stu-id="c8468-172">Deploy your service</span></span>
1. <span data-ttu-id="c8468-173">Accedere al [portale di Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c8468-173">Go to the [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c8468-174">Fare clic sulla scheda **Servizi cloud** a sinistra, quindi selezionare il servizio cloud creato precedentemente.</span><span class="sxs-lookup"><span data-stu-id="c8468-174">Click the **Cloud Services** tab on the left, and select the cloud service that you created earlier.</span></span>
3. <span data-ttu-id="c8468-175">Fare clic su **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="c8468-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="c8468-176">Scegliere l'ambiente di gestione temporanea, quindi fare clic su **Carica una nuova distribuzione di gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="c8468-176">Choose the staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Staging][3]
5. <span data-ttu-id="c8468-178">Nella finestra di dialogo immettere un'etichetta per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c8468-178">In the dialog box, enter a deployment label.</span></span> <span data-ttu-id="c8468-179">Per "Pacchetto" e "Configurazione" fare clic su "Da locale", scegliere il file **SplitMergeService.cspkg** e il file con estensione cscfg configurato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8468-179">For both 'Package' and 'Configuration', click 'From Local' and choose the **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="c8468-180">Assicurarsi che la casella di controllo **Distribuire anche se uno o più ruoli contengono una singola istanza** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="c8468-180">Ensure that the checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="c8468-181">Fare clic sul pulsante con il segno di spunta in basso a destra per avviare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c8468-181">Hit the tick button in the bottom right to begin the deployment.</span></span> <span data-ttu-id="c8468-182">Per il completamento dell'operazione sarà necessario attendere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c8468-182">Expect it to take a few minutes to complete.</span></span>

   ![Carica][4]

## <a name="troubleshoot-the-deployment"></a><span data-ttu-id="c8468-184">Risolvere i problemi relativi alla distribuzione</span><span class="sxs-lookup"><span data-stu-id="c8468-184">Troubleshoot the deployment</span></span>
<span data-ttu-id="c8468-185">Se la messa in linea del proprio ruolo Web non riesce, è probabile che si tratti di un problema relativo alla configurazione della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c8468-185">If your web role fails to come online, it is likely a problem with the security configuration.</span></span> <span data-ttu-id="c8468-186">Verificare che SSL sia configurato come descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="c8468-186">Check that the SSL is configured as described above.</span></span>

<span data-ttu-id="c8468-187">Se la messa online del proprio ruolo di lavoro non riesce, ma riesce quella del ruolo Web, è probabile che si tratti di un problema con la connessione al database per lo stato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c8468-187">If your worker role fails to come online, but your web role succeeds, it is most likely a problem connecting to the status database that you created earlier.</span></span>

* <span data-ttu-id="c8468-188">Assicurarsi che la stringa di connessione nel file .cscfg sia corretta.</span><span class="sxs-lookup"><span data-stu-id="c8468-188">Make sure that the connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="c8468-189">Verificare che il server e il database esistano e che l'ID utente e la password siano corretti.</span><span class="sxs-lookup"><span data-stu-id="c8468-189">Check that the server and database exist, and that the user id and password are correct.</span></span>
* <span data-ttu-id="c8468-190">Per il database SQL di Azure, la stringa di connessione deve essere nel seguente formato:</span><span class="sxs-lookup"><span data-stu-id="c8468-190">For Azure SQL DB, the connection string should be of the form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="c8468-191">Assicurarsi che il nome del server non inizi con **https://**.</span><span class="sxs-lookup"><span data-stu-id="c8468-191">Ensure that the server name does not begin with **https://**.</span></span>
* <span data-ttu-id="c8468-192">Assicurarsi che il server di database SQL di Azure consenta la connessione da parte dei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8468-192">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="c8468-193">Per eseguire questa operazione, aprire https://manage.windowsazure.com, fare clic su "Database SQL" a sinistra, fare clic su "Server" in alto, quindi selezionare il proprio server.</span><span class="sxs-lookup"><span data-stu-id="c8468-193">To do this, open https://manage.windowsazure.com, click “SQL Databases” on the left, click “Servers” at the top, and select your server.</span></span> <span data-ttu-id="c8468-194">Fare clic su **Configura** nella parte superiore dello schermo e assicurarsi che l'impostazione **Servizi di Azure** sia impostata su "Sì"</span><span class="sxs-lookup"><span data-stu-id="c8468-194">Click **Configure** at the top and ensure that the **Azure Services** setting is set to “Yes”.</span></span> <span data-ttu-id="c8468-195">(vedere la sezione Prerequisiti all'inizio di questo articolo).</span><span class="sxs-lookup"><span data-stu-id="c8468-195">(See the Prerequisites section at the top of this article).</span></span>

## <a name="test-the-service-deployment"></a><span data-ttu-id="c8468-196">Testare la distribuzione del servizio</span><span class="sxs-lookup"><span data-stu-id="c8468-196">Test the service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="c8468-197">Connettersi con un Web browser</span><span class="sxs-lookup"><span data-stu-id="c8468-197">Connect with a web browser</span></span>
<span data-ttu-id="c8468-198">Determinare l'endpoint Web del servizio di divisione e unione.</span><span class="sxs-lookup"><span data-stu-id="c8468-198">Determine the web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="c8468-199">È possibile trovarlo nel portale di Azure classico accedendo al **Dashboard** del proprio servizio cloud e guardando in **URL sito** a destra.</span><span class="sxs-lookup"><span data-stu-id="c8468-199">You can find this in the Azure Classic Portal by going to the **Dashboard** of your cloud service and looking under **Site URL** on the right side.</span></span> <span data-ttu-id="c8468-200">Sostituire **http://** con **https://** poiché le impostazioni di sicurezza predefinite disabilitano l'endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8468-200">Replace **http://** with **https://** since the default security settings disable the HTTP endpoint.</span></span> <span data-ttu-id="c8468-201">Caricare la pagina per questo URL nel browser.</span><span class="sxs-lookup"><span data-stu-id="c8468-201">Load the page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="c8468-202">Eseguire i test con gli script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8468-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="c8468-203">È possibile testare la distribuzione e l'ambiente eseguendo gli script di PowerShell di esempio inclusi.</span><span class="sxs-lookup"><span data-stu-id="c8468-203">The deployment and your environment can be tested by running the included sample PowerShell scripts.</span></span>

<span data-ttu-id="c8468-204">I file di script inclusi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8468-204">The script files included are:</span></span>

1. <span data-ttu-id="c8468-205">**SetupSampleSplitMergeEnvironment.ps1** : consente di impostare un livello di dati di test per divisione e unione (per una descrizione dettagliata, vedere la tabella sottostante).</span><span class="sxs-lookup"><span data-stu-id="c8468-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="c8468-206">**ExecuteSampleSplitMerge.ps1** : consente di eseguire le operazioni di test sul livello di dati di test (per una descrizione dettagliata, vedere la tabella sottostante).</span><span class="sxs-lookup"><span data-stu-id="c8468-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on the test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="c8468-207">**GetMappings.ps1**: script di esempio di primo livello che visualizza lo stato corrente dei mapping di partizione.</span><span class="sxs-lookup"><span data-stu-id="c8468-207">**GetMappings.ps1** - top-level sample script that prints out the current state of the shard mappings.</span></span>
4. <span data-ttu-id="c8468-208">**ShardManagement.psm1**: script helper che include l'API ShardManagement</span><span class="sxs-lookup"><span data-stu-id="c8468-208">**ShardManagement.psm1**  - helper script that wraps the ShardManagement API</span></span>
5. <span data-ttu-id="c8468-209">**SqlDatabaseHelpers.psm1**: script helper per creare e gestire database SQL</span><span class="sxs-lookup"><span data-stu-id="c8468-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="c8468-210">File PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8468-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="c8468-211">Passi</span><span class="sxs-lookup"><span data-stu-id="c8468-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="c8468-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="c8468-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="c8468-213">Crea un database di gestione delle mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="c8468-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="c8468-214">Crea 2 database partizioni.</span><span class="sxs-lookup"><span data-stu-id="c8468-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="c8468-215">Crea una mappa partizioni per tali database (elimina eventuali mappe partizioni esistenti per i database).</span><span class="sxs-lookup"><span data-stu-id="c8468-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="c8468-216">Crea una tabella di esempio di piccole dimensioni in entrambe le partizioni e popola la tabella in una delle partizioni.</span><span class="sxs-lookup"><span data-stu-id="c8468-216">Creates a small sample table in both the shards, and populates the table in one of the shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="c8468-217">Dichiara l'elemento SchemaInfo per la tabella partizionata.</span><span class="sxs-lookup"><span data-stu-id="c8468-217">Declares the SchemaInfo for the sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="c8468-218">File PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8468-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="c8468-219">Passi</span><span class="sxs-lookup"><span data-stu-id="c8468-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="c8468-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="c8468-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="c8468-221">Invia una richiesta di divisione al front-end Web del servizio di divisione e unione, che sposta la metà dei dati dalla prima partizione alla seconda partizione.</span><span class="sxs-lookup"><span data-stu-id="c8468-221">Sends a split request to the Split-Merge Service web frontend, which splits half the data from the first shard to the second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="c8468-222">Esegue il polling del front-end Web per lo stato della richiesta di divisione e attende il completamento della richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8468-222">Polls the web frontend for the split request status and waits until the request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="c8468-223">Invia una richiesta di unione al front-end Web del servizio di divisione e unione, che sposta la metà dei dati dalla seconda partizione alla prima partizione.</span><span class="sxs-lookup"><span data-stu-id="c8468-223">Sends a merge request to the Split-Merge Service web frontend, which moves the data from the second shard back to the first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="c8468-224">Esegue il polling del front-end Web per lo stato della richiesta di unione e attende il completamento della richiesta.</span><span class="sxs-lookup"><span data-stu-id="c8468-224">Polls the web frontend for the merge request status and waits until the request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-to-verify-your-deployment"></a><span data-ttu-id="c8468-225">Usare PowerShell per la verifica della distribuzione</span><span class="sxs-lookup"><span data-stu-id="c8468-225">Use PowerShell to verify your deployment</span></span>
1. <span data-ttu-id="c8468-226">Aprire una nuova finestra di PowerShell e passare alla directory in cui si è scaricato il pacchetto di divisione e unione, quindi passare alla directory "powershell".</span><span class="sxs-lookup"><span data-stu-id="c8468-226">Open a new PowerShell window and navigate to the directory where you downloaded the Split-Merge package, and then navigate into the “powershell” directory.</span></span>
2. <span data-ttu-id="c8468-227">Creare un server di database SQL di Microsoft Azure (o sceglierne uno esistente) che conterrà il gestore dei mapping della partizione e le partizioni stesse.</span><span class="sxs-lookup"><span data-stu-id="c8468-227">Create an Azure SQL database server (or choose an existing server) where the shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c8468-228">Lo script SetupSampleSplitMergeEnvironment.ps1 crea tutti questi database sullo stesso server per impostazione predefinita, a scopo di semplificazione.</span><span class="sxs-lookup"><span data-stu-id="c8468-228">The SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on the same server by default to keep the script simple.</span></span> <span data-ttu-id="c8468-229">Non si tratta di una restrizione del servizio di divisione e unione in sé stesso.</span><span class="sxs-lookup"><span data-stu-id="c8468-229">This is not a restriction of the Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="c8468-230">Per spostare dati e aggiornare il mapping della partizione, sarà necessario un account di accesso di autenticazione SQL con accesso in lettura/scrittura ai database per il servizio di divisione e unione.</span><span class="sxs-lookup"><span data-stu-id="c8468-230">A SQL authentication login with read/write access to the DBs will be needed for the Split-Merge service to move data and update the shard map.</span></span> <span data-ttu-id="c8468-231">Poiché il servizio di divisione e unione viene eseguito nel cloud, non supporta attualmente l'autenticazione integrata.</span><span class="sxs-lookup"><span data-stu-id="c8468-231">Since the Split-Merge Service runs in the cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="c8468-232">Assicurarsi che il server SQL di Azure sia configurato per consentire l'accesso dall'indirizzo IP del computer che esegue questi script.</span><span class="sxs-lookup"><span data-stu-id="c8468-232">Make sure the Azure SQL server is configured to allow access from the IP address of the machine running these scripts.</span></span> <span data-ttu-id="c8468-233">È possibile trovare questa impostazione nel server SQL di Azure, in / configurazione / indirizzi IP consentiti.</span><span class="sxs-lookup"><span data-stu-id="c8468-233">You can find this setting under the Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="c8468-234">Eseguire lo script SetupSampleSplitMergeEnvironment.ps1 per creare l'ambiente di esempio.</span><span class="sxs-lookup"><span data-stu-id="c8468-234">Execute the SetupSampleSplitMergeEnvironment.ps1 script to create the sample environment.</span></span>
   
   <span data-ttu-id="c8468-235">L'esecuzione di questo script comporterà la cancellazione di tutte le strutture di dati di gestione dei mapping della partizione nel relativo database, nonché di tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="c8468-235">Running this script will wipe out any existing shard map management data structures on the shard map manager database and the shards.</span></span> <span data-ttu-id="c8468-236">Potrebbe risultare utile eseguire nuovamente lo script se si vuole inizializzare nuovamente il mapping della partizione o le partizioni stesse.</span><span class="sxs-lookup"><span data-stu-id="c8468-236">It may be useful to rerun the script if you wish to re-initialize the shard map or shards.</span></span>
   
   <span data-ttu-id="c8468-237">Riga di comando di esempio:</span><span class="sxs-lookup"><span data-stu-id="c8468-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="c8468-238">Eseguire lo script Getmappings.ps1 per visualizzare i mapping esistenti nell'ambiente di esempio.</span><span class="sxs-lookup"><span data-stu-id="c8468-238">Execute the Getmappings.ps1 script to view the mappings that currently exist in the sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="c8468-239">Eseguire lo script ExecuteSampleSplitMerge.ps1 per realizzare un'operazione di divisione (spostamento della metà dei dati dalla prima partizione alla seconda) e successivamente un'operazione di unione (spostando nuovamente i dati nella prima partizione).</span><span class="sxs-lookup"><span data-stu-id="c8468-239">Execute the ExecuteSampleSplitMerge.ps1 script to execute a split operation (moving half the data on the first shard to the second shard) and then a merge operation (moving the data back onto the first shard).</span></span> <span data-ttu-id="c8468-240">Se si è configurato SSL e si è lasciato l'endpoint http disabilitato, assicurarsi di usare l'endpoint https://.</span><span class="sxs-lookup"><span data-stu-id="c8468-240">If you configured SSL and left the http endpoint disabled, ensure that you use the https:// endpoint instead.</span></span>
   
   <span data-ttu-id="c8468-241">Riga di comando di esempio:</span><span class="sxs-lookup"><span data-stu-id="c8468-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="c8468-242">Se viene visualizzato il seguente errore, è probabile che di tratti di un problema con il certificato dell'endpoint Web.</span><span class="sxs-lookup"><span data-stu-id="c8468-242">If you receive the below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="c8468-243">Provare a connettersi all'endpoint con un Web browser e controllare se è presente un errore di certificato.</span><span class="sxs-lookup"><span data-stu-id="c8468-243">Try connecting to the Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="c8468-244">Se la connessione riesce, l'output dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c8468-244">If it succeeded, the output should look like the below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="c8468-245">Ora è possibile sperimentare il processo con altri tipi di dati.</span><span class="sxs-lookup"><span data-stu-id="c8468-245">Experiment with other data types!</span></span> <span data-ttu-id="c8468-246">Questi script accettano un parametro facoltativo, ShardKeyType, che consente di specificare il tipo di chiave.</span><span class="sxs-lookup"><span data-stu-id="c8468-246">All of these scripts take an optional -ShardKeyType parameter that allows you to specify the key type.</span></span> <span data-ttu-id="c8468-247">Il tipo predefinito è Int32, ma è anche possibile specificare Int64, Guid o Binary.</span><span class="sxs-lookup"><span data-stu-id="c8468-247">The default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="c8468-248">Creare richieste</span><span class="sxs-lookup"><span data-stu-id="c8468-248">Create requests</span></span>
<span data-ttu-id="c8468-249">Il servizio può essere usato tramite l'interfaccia utente Web o l'importazione nonché mediante il modulo PowerShell SplitMerge.psm1 che invierà le richieste tramite il ruolo web.</span><span class="sxs-lookup"><span data-stu-id="c8468-249">The service can be used either by using the web UI or by importing and using the SplitMerge.psm1 PowerShell module which will submit your requests through the web role.</span></span>

<span data-ttu-id="c8468-250">Il servizio può spostare i dati in tabelle partizionate e tabelle di riferimento.</span><span class="sxs-lookup"><span data-stu-id="c8468-250">The service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="c8468-251">Una tabella partizionata ha una colonna chiave di partizionamento e ospita dati di riga diversi per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="c8468-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="c8468-252">Una tabella di riferimento non è partizionata e può così contenere gli stessi dati di riga in ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="c8468-252">A reference table is not sharded so it contains the same row data on every shard.</span></span> <span data-ttu-id="c8468-253">Le tabelle di riferimento sono utili per i dati che non vengono modificati di frequente e vengono usate per il JOIN con tabelle partizionate nelle query.</span><span class="sxs-lookup"><span data-stu-id="c8468-253">Reference tables are useful for data that does not change often and is used to JOIN with sharded tables in queries.</span></span>

<span data-ttu-id="c8468-254">Per eseguire un'operazione di divisione e unione, è necessario dichiarare le tabelle partizionate e le tabelle di riferimento che si vogliono spostare.</span><span class="sxs-lookup"><span data-stu-id="c8468-254">In order to perform a split-merge operation, you must declare the sharded tables and reference tables that you want to have moved.</span></span> <span data-ttu-id="c8468-255">Questa operazione viene eseguita con l'API **SchemaInfo** .</span><span class="sxs-lookup"><span data-stu-id="c8468-255">This is accomplished with the **SchemaInfo** API.</span></span> <span data-ttu-id="c8468-256">Tale API si trova nello spazio dei nomi **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** .</span><span class="sxs-lookup"><span data-stu-id="c8468-256">This API is in the **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="c8468-257">Per ogni tabella partizionata, creare un oggetto **ShardedTableInfo** che descriva il nome dello schema padre della tabella (facoltativo, il valore predefinito è "dbo"), il nome della tabella e il nome della colonna della tabella che contiene la chiave di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="c8468-257">For each sharded table, create a **ShardedTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”), the table name, and the column name in that table that contains the sharding key.</span></span>
2. <span data-ttu-id="c8468-258">Per ogni tabella di riferimento, creare un oggetto **ReferenceTableInfo** che descriva il nome dello schema padre della tabella (facoltativo, il valore predefinito è "dbo") e il nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="c8468-258">For each reference table, create a **ReferenceTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”) and the table name.</span></span>
3. <span data-ttu-id="c8468-259">Aggiungere gli oggetti TableInfo precedenti a un nuovo oggetto **SchemaInfo** .</span><span class="sxs-lookup"><span data-stu-id="c8468-259">Add the above TableInfo objects to a new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="c8468-260">Ottenere un riferimento all'oggetto **ShardMapManager**, quindi chiamare **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="c8468-260">Get a reference to a **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="c8468-261">Aggiungere **SchemaInfo** a **SchemaInfoCollection**, fornendo il nome della mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="c8468-261">Add the **SchemaInfo** to the **SchemaInfoCollection**, providing the shard map name.</span></span>

<span data-ttu-id="c8468-262">È possibile consultare un esempio nello script SetupSampleSplitMergeEnvironment.ps1.</span><span class="sxs-lookup"><span data-stu-id="c8468-262">An example of this can be seen in the SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="c8468-263">Il servizio di divisione e unione non crea automaticamente il database di destinazione (o lo schema per tutte le tabelle nel database).</span><span class="sxs-lookup"><span data-stu-id="c8468-263">The Split-Merge service does not create the target database (or schema for any tables in the database) for you.</span></span> <span data-ttu-id="c8468-264">Questi devono essere creati precedentemente, prima di inviare richieste al servizio.</span><span class="sxs-lookup"><span data-stu-id="c8468-264">They must be pre-created before sending a request to the service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c8468-265">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="c8468-265">Troubleshooting</span></span>
<span data-ttu-id="c8468-266">Quando si eseguono gli script di PowerShell di esempio, è possibile che venga visualizzato un messaggio simile a quello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c8468-266">You may see the below message when running the sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.
   ```

<span data-ttu-id="c8468-267">Questo errore indica che il certificato SSL non è configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c8468-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="c8468-268">Seguire le istruzioni nella sezione "Connessione a un Web browser".</span><span class="sxs-lookup"><span data-stu-id="c8468-268">Please follow the instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="c8468-269">Se non è possibile inviare richieste, potrebbe essere visualizzato il seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="c8468-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="c8468-270">In questo caso, controllare il file di configurazione, in particolare l'impostazione per **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="c8468-270">In this case, check your configuration file, in particular the setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="c8468-271">In genere, questo errore indica che il ruolo di lavoro non è riuscito a inizializzare in modo corretto il database dei metadati al primo utilizzo.</span><span class="sxs-lookup"><span data-stu-id="c8468-271">This error typically indicates that the worker role could not successfully initialize the metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

