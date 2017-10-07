---
title: un servizio di suddivisione unione aaaDeploy | Documenti Microsoft
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
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="e44d0-103">Distribuire un servizio di divisione e unione</span><span class="sxs-lookup"><span data-stu-id="e44d0-103">Deploy a split-merge service</span></span>
<span data-ttu-id="e44d0-104">strumento di unione di menu combinato Hello consente di spostare i dati tra database partizionati.</span><span class="sxs-lookup"><span data-stu-id="e44d0-104">hello split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="e44d0-105">Vedere [Spostamento di dati tra database cloud con numero maggiore di istanze](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="e44d0-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-hello-split-merge-packages"></a><span data-ttu-id="e44d0-106">Scaricare i pacchetti hello unione di menu combinato</span><span class="sxs-lookup"><span data-stu-id="e44d0-106">Download hello Split-Merge packages</span></span>
1. <span data-ttu-id="e44d0-107">Scaricare hello NuGet più recente da [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="e44d0-107">Download hello latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="e44d0-108">Aprire un prompt dei comandi e passare toohello directory in cui è stato scaricato nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="e44d0-108">Open a command prompt and navigate toohello directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="e44d0-109">download di Hello include commmands di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e44d0-109">hello download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="e44d0-110">Scaricare il pacchetto suddivisione unione più recente di hello nella directory corrente di hello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e44d0-110">Download hello latest Split-Merge package into hello current directory with hello below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="e44d0-111">file Hello vengono inseriti in una directory denominata **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** in *x.x.xxx.x* riflette il numero di versione di hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-111">hello files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects hello version number.</span></span> <span data-ttu-id="e44d0-112">Trovare i file del servizio di suddivisione unione hello in hello **content\splitmerge\service** sottodirectory e hello gli script di PowerShell di unione di menu combinato (e client necessari file con estensione dll) in hello **content\splitmerge\powershell** sottodirectory.</span><span class="sxs-lookup"><span data-stu-id="e44d0-112">Find hello split-merge Service files in hello **content\splitmerge\service** sub-directory, and hello Split-Merge PowerShell scripts (and required client .dlls) in hello **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e44d0-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e44d0-113">Prerequisites</span></span>
1. <span data-ttu-id="e44d0-114">Creare un database di database SQL di Azure che verrà utilizzato come database di stato di unione di menu combinato hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-114">Create an Azure SQL DB database that will be used as hello split-merge status database.</span></span> <span data-ttu-id="e44d0-115">Passare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e44d0-115">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e44d0-116">Creazione personalizzata di un nuovo **database SQL**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="e44d0-117">Assegnare un nome di database hello e creare un nuovo amministratore e una password.</span><span class="sxs-lookup"><span data-stu-id="e44d0-117">Give hello database a name and create a new administrator and password.</span></span> <span data-ttu-id="e44d0-118">Impossibile verificare toorecord hello nome e la password per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="e44d0-118">Be sure toorecord hello name and password for later use.</span></span>
2. <span data-ttu-id="e44d0-119">Verificare che il server di database SQL di Azure consente tooit tooconnect servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e44d0-119">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="e44d0-120">Nel portale hello hello **le impostazioni del Firewall**, verificare che hello **Consenti l'accesso ai servizi tooAzure** impostazione troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-120">In hello portal, in hello **Firewall Settings**, ensure that hello **Allow access tooAzure Services** setting is set too**On**.</span></span> <span data-ttu-id="e44d0-121">Fare clic su hello "icona Salva".</span><span class="sxs-lookup"><span data-stu-id="e44d0-121">Click hello "save" icon.</span></span>
   
   ![Servizi consentiti][1]
3. <span data-ttu-id="e44d0-123">Creare un account di archiviazione di Azure che verrà usato per l'output di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="e44d0-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="e44d0-124">Passare toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e44d0-124">Go toohello Azure Portal.</span></span> <span data-ttu-id="e44d0-125">Nella barra sinistra hello, fare clic su **New**, fare clic su **dati e archiviazione**, quindi **archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-125">In hello left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="e44d0-126">Creare un servizio cloud di Azure che conterrà il servizio di divisione e unione.</span><span class="sxs-lookup"><span data-stu-id="e44d0-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="e44d0-127">Passare toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e44d0-127">Go toohello Azure Portal.</span></span> <span data-ttu-id="e44d0-128">Nella barra sinistra hello, fare clic su **New**, quindi **calcolo**, **servizio Cloud**, e **crea**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-128">In hello left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="e44d0-129">Configurare il servizio di divisione e unione</span><span class="sxs-lookup"><span data-stu-id="e44d0-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="e44d0-130">Configurazione del servizio di divisione e unione</span><span class="sxs-lookup"><span data-stu-id="e44d0-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="e44d0-131">Nella cartella hello in cui è stato scaricato assembly hello suddivisione unione, creare una copia di hello **ServiceConfiguration.Template.cscfg** file fornita insieme **SplitMergeService.cspkg** e rinominarlo **ServiceConfiguration. cscfg**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-131">In hello folder where you downloaded hello Split-Merge assemblies, create a copy of hello **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="e44d0-132">Aprire **ServiceConfiguration. cscfg** in un editor di testo, ad esempio Visual Studio che convalida l'input, ad esempio formato hello di identificazioni personali del certificato.</span><span class="sxs-lookup"><span data-stu-id="e44d0-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as hello format of certificate thumbprints.</span></span>
3. <span data-ttu-id="e44d0-133">Creare un nuovo database o scegliere un tooserve database esistente come database di stato hello per le operazioni di unione di menu combinato e recuperare la stringa di connessione hello di tale database.</span><span class="sxs-lookup"><span data-stu-id="e44d0-133">Create a new database or choose an existing database tooserve as hello status database for Split-Merge operations and retrieve hello connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="e44d0-134">In questo momento, database di stato hello deve utilizzare regole di confronto latino hello (SQL\_Latin1\_generale\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="e44d0-134">At this time, hello status database must use hello Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="e44d0-135">Per ulteriori informazioni, vedere [Nome regole di confronto Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="e44d0-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="e44d0-136">Con il database SQL di Azure, la stringa di connessione hello è in genere formato hello:</span><span class="sxs-lookup"><span data-stu-id="e44d0-136">With Azure SQL DB, hello connection string typically is of hello form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="e44d0-137">Immettere la stringa di connessione nel file cscfg hello in entrambi hello **SplitMergeWeb** e **SplitMergeWorker** sezioni ruolo nell'impostazione ElasticScaleMetadata hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-137">Enter this connection string in hello cscfg file in both hello **SplitMergeWeb** and **SplitMergeWorker** role sections in hello ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="e44d0-138">Per hello **SplitMergeWorker** ruolo, immettere un'archiviazione tooAzure stringa di connessione valida per hello **WorkerRoleSynchronizationStorageAccountConnectionString** impostazione.</span><span class="sxs-lookup"><span data-stu-id="e44d0-138">For hello **SplitMergeWorker** role, enter a valid connection string tooAzure storage for hello **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="e44d0-139">Configurare la sicurezza</span><span class="sxs-lookup"><span data-stu-id="e44d0-139">Configure security</span></span>
<span data-ttu-id="e44d0-140">Per istruzioni dettagliate tooconfigure hello sicurezza hello servizio, vedere toohello [configurazione della sicurezza suddivisione unione](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="e44d0-140">For detailed instructions tooconfigure hello security of hello service, refer toohello [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="e44d0-141">Ai fini di hello di una distribuzione di test semplice per questa esercitazione, un set minimo di passaggi di configurazione eseguita il servizio hello tooget attivo e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e44d0-141">For hello purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed tooget hello service up and running.</span></span> <span data-ttu-id="e44d0-142">Questi passaggi abilitano solo hello una macchina/account eseguirle toocommunicate con servizio hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-142">These steps enable only hello one machine/account executing them toocommunicate with hello service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="e44d0-143">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="e44d0-143">Create a self-signed certificate</span></span>
<span data-ttu-id="e44d0-144">Creare una nuova directory e da questo hello execute directory seguente comando utilizzando un [prompt dei comandi per sviluppatori per Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) finestra:</span><span class="sxs-lookup"><span data-stu-id="e44d0-144">Create a new directory and from this directory execute hello following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="e44d0-145">Richiesto per una chiave privata di tooprotect hello password.</span><span class="sxs-lookup"><span data-stu-id="e44d0-145">You are asked for a password tooprotect hello private key.</span></span> <span data-ttu-id="e44d0-146">Immettere una password complessa e confermarla.</span><span class="sxs-lookup"><span data-stu-id="e44d0-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="e44d0-147">Verrà chiesto di hello password toobe utilizzato più volte dopo che.</span><span class="sxs-lookup"><span data-stu-id="e44d0-147">You are then prompted for hello password toobe used once more after that.</span></span> <span data-ttu-id="e44d0-148">Fare clic su **Sì** in tooimport fine hello è archivio radice attendibile autorità di certificazione toohello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-148">Click **Yes** at hello end tooimport it toohello Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="e44d0-149">Creare un file PFX</span><span class="sxs-lookup"><span data-stu-id="e44d0-149">Create a PFX file</span></span>
<span data-ttu-id="e44d0-150">Eseguire hello comando seguente da hello stessa finestra in cui è stato eseguito makecert; Utilizzare hello stessa password che è usato toocreate hello certificato:</span><span class="sxs-lookup"><span data-stu-id="e44d0-150">Execute hello following command from hello same window where makecert was executed; use hello same password that you used toocreate hello certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a><span data-ttu-id="e44d0-151">Importare il certificato di client hello nell'archivio personale hello</span><span class="sxs-lookup"><span data-stu-id="e44d0-151">Import hello client certificate into hello personal store</span></span>
1. <span data-ttu-id="e44d0-152">In Esplora risorse fare doppio clic su **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="e44d0-153">In hello **importazione guidata certificati** selezionare **utente corrente** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-153">In hello **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="e44d0-154">Verificare il percorso di file hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-154">Confirm hello file path and click **Next**.</span></span>
4. <span data-ttu-id="e44d0-155">Digitare la password hello, lasciare **includono tutte le proprietà estese** selezionata e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-155">Type hello password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="e44d0-156">Lasciare **archivio certificati selezionare automaticamente hello […]**  selezionata e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-156">Leave **Automatically select hello certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="e44d0-157">Fare clic su **Fine**, quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a><span data-ttu-id="e44d0-158">Caricare il servizio cloud toohello di hello PFX file</span><span class="sxs-lookup"><span data-stu-id="e44d0-158">Upload hello PFX file toohello cloud service</span></span>
1. <span data-ttu-id="e44d0-159">Passare toohello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e44d0-159">Go toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e44d0-160">Selezionare **Servizi cloud**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="e44d0-161">Selezionare servizio cloud hello creato in precedenza per il servizio di suddivisione/unione hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-161">Select hello cloud service you created above for hello Split/Merge service.</span></span>
4. <span data-ttu-id="e44d0-162">Fare clic su **certificati** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-162">Click **Certificates** on hello top menu.</span></span>
5. <span data-ttu-id="e44d0-163">Fare clic su **caricare** barra inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-163">Click **Upload** in hello bottom bar.</span></span>
6. <span data-ttu-id="e44d0-164">Selezionare i file PFX hello e immettere hello uguale alla password precedente.</span><span class="sxs-lookup"><span data-stu-id="e44d0-164">Select hello PFX file and enter hello same password as above.</span></span>
7. <span data-ttu-id="e44d0-165">Al termine, copiare l'identificazione personale del certificato hello da hello nuova voce di elenco hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-165">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

### <a name="update-hello-service-configuration-file"></a><span data-ttu-id="e44d0-166">File di configurazione del servizio di aggiornamento hello</span><span class="sxs-lookup"><span data-stu-id="e44d0-166">Update hello service configuration file</span></span>
<span data-ttu-id="e44d0-167">Incollare l'identificazione personale del certificato hello copiato in precedenza nell'attributo/valore di identificazione personale hello di queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="e44d0-167">Paste hello certificate thumbprint copied above into hello thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="e44d0-168">Per il ruolo di lavoro hello:</span><span class="sxs-lookup"><span data-stu-id="e44d0-168">For hello worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="e44d0-169">Per il ruolo web hello:</span><span class="sxs-lookup"><span data-stu-id="e44d0-169">For hello web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="e44d0-170">Tenere presente che per le distribuzioni di produzione certificati separati devono essere utilizzati per hello autorità di certificazione, per la crittografia, hello certificato del Server e i certificati client.</span><span class="sxs-lookup"><span data-stu-id="e44d0-170">Please note that for production deployments separate certificates should be used for hello CA, for encryption, hello Server certificate and client certificates.</span></span> <span data-ttu-id="e44d0-171">Per istruzioni dettagliate, vedere l'articolo relativo alla [configurazione della sicurezza](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="e44d0-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="e44d0-172">Distribuire il servizio</span><span class="sxs-lookup"><span data-stu-id="e44d0-172">Deploy your service</span></span>
1. <span data-ttu-id="e44d0-173">Passare toohello [portale di Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e44d0-173">Go toohello [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e44d0-174">Fare clic su hello **servizi Cloud** scheda hello sinistra e selezionare il servizio cloud hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e44d0-174">Click hello **Cloud Services** tab on hello left, and select hello cloud service that you created earlier.</span></span>
3. <span data-ttu-id="e44d0-175">Fare clic su **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="e44d0-176">Scegliere l'ambiente di gestione temporanea hello, quindi fare clic su **carica una nuova distribuzione di gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-176">Choose hello staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Staging][3]
5. <span data-ttu-id="e44d0-178">Nella finestra di dialogo hello immettere un'etichetta di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e44d0-178">In hello dialog box, enter a deployment label.</span></span> <span data-ttu-id="e44d0-179">Per 'Package' e 'Configuration', fare clic su 'Da Local' e scegliere hello **SplitMergeService.cspkg** file e il file con estensione cscfg configurata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e44d0-179">For both 'Package' and 'Configuration', click 'From Local' and choose hello **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="e44d0-180">Verificare che tale casella hello **Distribuisci anche se uno o più ruoli contengono una singola istanza** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="e44d0-180">Ensure that hello checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="e44d0-181">Raggiunto il pulsante di segni di graduazione hello nella distribuzione di hello nella parte inferiore destra toobegin hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-181">Hit hello tick button in hello bottom right toobegin hello deployment.</span></span> <span data-ttu-id="e44d0-182">Previsto tootake toocomplete di pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e44d0-182">Expect it tootake a few minutes toocomplete.</span></span>

   ![Carica][4]

## <a name="troubleshoot-hello-deployment"></a><span data-ttu-id="e44d0-184">Risoluzione dei problemi di distribuzione hello</span><span class="sxs-lookup"><span data-stu-id="e44d0-184">Troubleshoot hello deployment</span></span>
<span data-ttu-id="e44d0-185">Se il ruolo web toocome online, è probabile che un problema di configurazione di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-185">If your web role fails toocome online, it is likely a problem with hello security configuration.</span></span> <span data-ttu-id="e44d0-186">Verificare che hello che SSL è configurato come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e44d0-186">Check that hello SSL is configured as described above.</span></span>

<span data-ttu-id="e44d0-187">Se il ruolo di lavoro ha esito negativo toocome online, ma il ruolo web ha esito positivo, è probabilmente un problema di connessione database stato toohello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e44d0-187">If your worker role fails toocome online, but your web role succeeds, it is most likely a problem connecting toohello status database that you created earlier.</span></span>

* <span data-ttu-id="e44d0-188">Assicurarsi che la stringa di connessione hello nel file con estensione cscfg è accurata.</span><span class="sxs-lookup"><span data-stu-id="e44d0-188">Make sure that hello connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="e44d0-189">Verificare che siano presenti database e server hello e che la password e l'id utente hello siano corretti.</span><span class="sxs-lookup"><span data-stu-id="e44d0-189">Check that hello server and database exist, and that hello user id and password are correct.</span></span>
* <span data-ttu-id="e44d0-190">Per il database di SQL Azure, la stringa di connessione hello deve essere formato hello:</span><span class="sxs-lookup"><span data-stu-id="e44d0-190">For Azure SQL DB, hello connection string should be of hello form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="e44d0-191">Verificare che non inizia con il nome del server hello **https://**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-191">Ensure that hello server name does not begin with **https://**.</span></span>
* <span data-ttu-id="e44d0-192">Verificare che il server di database SQL di Azure consente tooit tooconnect servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e44d0-192">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="e44d0-193">toodo, aprire https://manage.windowsazure.com, scegliere "Database di SQL" hello a sinistra, fare clic su "Server" nella parte superiore di hello e selezionare il server.</span><span class="sxs-lookup"><span data-stu-id="e44d0-193">toodo this, open https://manage.windowsazure.com, click “SQL Databases” on hello left, click “Servers” at hello top, and select your server.</span></span> <span data-ttu-id="e44d0-194">Fare clic su **configura** in hello in alto e verificare che hello **servizi Azure** impostazione troppo "Yes".</span><span class="sxs-lookup"><span data-stu-id="e44d0-194">Click **Configure** at hello top and ensure that hello **Azure Services** setting is set too“Yes”.</span></span> <span data-ttu-id="e44d0-195">(Vedere la sezione Prerequisiti hello sezione nella parte superiore di hello di questo articolo).</span><span class="sxs-lookup"><span data-stu-id="e44d0-195">(See hello Prerequisites section at hello top of this article).</span></span>

## <a name="test-hello-service-deployment"></a><span data-ttu-id="e44d0-196">Testare la distribuzione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="e44d0-196">Test hello service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="e44d0-197">Connettersi con un Web browser</span><span class="sxs-lookup"><span data-stu-id="e44d0-197">Connect with a web browser</span></span>
<span data-ttu-id="e44d0-198">Determinare l'endpoint web hello del servizio di suddivisione-unione.</span><span class="sxs-lookup"><span data-stu-id="e44d0-198">Determine hello web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="e44d0-199">È possibile trovare questo in hello portale classico di Azure da passare toohello **Dashboard** del servizio cloud e cercando nella **URL del sito** sul lato destro hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-199">You can find this in hello Azure Classic Portal by going toohello **Dashboard** of your cloud service and looking under **Site URL** on hello right side.</span></span> <span data-ttu-id="e44d0-200">Sostituire **http://** con **https://** poiché le impostazioni di sicurezza predefinite hello disabilitano endpoint hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="e44d0-200">Replace **http://** with **https://** since hello default security settings disable hello HTTP endpoint.</span></span> <span data-ttu-id="e44d0-201">Caricare la pagina hello per questo URL nel browser.</span><span class="sxs-lookup"><span data-stu-id="e44d0-201">Load hello page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="e44d0-202">Eseguire i test con gli script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="e44d0-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="e44d0-203">distribuzione di Hello e l'ambiente può essere testati eseguendo gli script di PowerShell di esempio hello incluso.</span><span class="sxs-lookup"><span data-stu-id="e44d0-203">hello deployment and your environment can be tested by running hello included sample PowerShell scripts.</span></span>

<span data-ttu-id="e44d0-204">file di script Hello forniti sono:</span><span class="sxs-lookup"><span data-stu-id="e44d0-204">hello script files included are:</span></span>

1. <span data-ttu-id="e44d0-205">**SetupSampleSplitMergeEnvironment.ps1** : consente di impostare un livello di dati di test per divisione e unione (per una descrizione dettagliata, vedere la tabella sottostante).</span><span class="sxs-lookup"><span data-stu-id="e44d0-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="e44d0-206">**ExecuteSampleSplitMerge.ps1** -esegue le operazioni di test nel test hello livello dati (vedere la tabella seguente per una descrizione dettagliata)</span><span class="sxs-lookup"><span data-stu-id="e44d0-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on hello test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="e44d0-207">**GetMappings.ps1** - principale script che visualizza lo stato corrente di hello di mapping delle partizioni hello di esempio.</span><span class="sxs-lookup"><span data-stu-id="e44d0-207">**GetMappings.ps1** - top-level sample script that prints out hello current state of hello shard mappings.</span></span>
4. <span data-ttu-id="e44d0-208">**ShardManagement.psm1** -script helper che esegue il wrapping hello ShardManagement API</span><span class="sxs-lookup"><span data-stu-id="e44d0-208">**ShardManagement.psm1**  - helper script that wraps hello ShardManagement API</span></span>
5. <span data-ttu-id="e44d0-209">**SqlDatabaseHelpers.psm1**: script helper per creare e gestire database SQL</span><span class="sxs-lookup"><span data-stu-id="e44d0-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="e44d0-210">File PowerShell</span><span class="sxs-lookup"><span data-stu-id="e44d0-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="e44d0-211">Passi</span><span class="sxs-lookup"><span data-stu-id="e44d0-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="e44d0-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="e44d0-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="e44d0-213">Crea un database di gestione delle mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="e44d0-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="e44d0-214">Crea 2 database partizioni.</span><span class="sxs-lookup"><span data-stu-id="e44d0-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="e44d0-215">Crea una mappa partizioni per tali database (elimina eventuali mappe partizioni esistenti per i database).</span><span class="sxs-lookup"><span data-stu-id="e44d0-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="e44d0-216">Crea una tabella di esempio di piccole dimensioni in entrambe le partizioni hello e popola la tabella hello in una delle partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-216">Creates a small sample table in both hello shards, and populates hello table in one of hello shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="e44d0-217">Dichiara hello SchemaInfo per la tabella partizionata hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-217">Declares hello SchemaInfo for hello sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="e44d0-218">File PowerShell</span><span class="sxs-lookup"><span data-stu-id="e44d0-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="e44d0-219">Passi</span><span class="sxs-lookup"><span data-stu-id="e44d0-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="e44d0-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="e44d0-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="e44d0-221">Invia un divisione richiesta toohello suddivisione unione servizio front-end web, che divide i dati hello metà dalla partizione secondo di hello prima partizione toohello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-221">Sends a split request toohello Split-Merge Service web frontend, which splits half hello data from hello first shard toohello second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="e44d0-222">Esegue il polling hello front-end web per suddividere lo stato di richiesta e attende fino al completamento di richiesta di hello hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-222">Polls hello web frontend for hello split request status and waits until hello request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="e44d0-223">Invia un merge richiesta toohello suddivisione unione servizio front-end web, che sposta i dati di hello dalla partizione prima di hello seconda partizione toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="e44d0-223">Sends a merge request toohello Split-Merge Service web frontend, which moves hello data from hello second shard back toohello first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="e44d0-224">Esegue il polling hello front-end web per lo stato richiesta di unione di hello e attende il completamento della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-224">Polls hello web frontend for hello merge request status and waits until hello request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a><span data-ttu-id="e44d0-225">Utilizzare PowerShell tooverify la distribuzione</span><span class="sxs-lookup"><span data-stu-id="e44d0-225">Use PowerShell tooverify your deployment</span></span>
1. <span data-ttu-id="e44d0-226">Aprire una nuova finestra di PowerShell passare toohello directory in cui è stato scaricato il pacchetto di suddivisione unione hello e quindi passare alla directory "powershell" hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-226">Open a new PowerShell window and navigate toohello directory where you downloaded hello Split-Merge package, and then navigate into hello “powershell” directory.</span></span>
2. <span data-ttu-id="e44d0-227">Creare un server di database SQL di Azure (o scegliere un server esistente) in cui verranno create gestore mappe partizioni di hello e partizioni.</span><span class="sxs-lookup"><span data-stu-id="e44d0-227">Create an Azure SQL database server (or choose an existing server) where hello shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e44d0-228">Hello SetupSampleSplitMergeEnvironment.ps1 script crea tutti questi database in hello stesso server da script hello tookeep predefinito semplice.</span><span class="sxs-lookup"><span data-stu-id="e44d0-228">hello SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on hello same server by default tookeep hello script simple.</span></span> <span data-ttu-id="e44d0-229">Non è una restrizione di hello suddivisione unione servizio stesso.</span><span class="sxs-lookup"><span data-stu-id="e44d0-229">This is not a restriction of hello Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="e44d0-230">Un accesso con autenticazione SQL con toohello di accesso in lettura/scrittura che database saranno necessaria per dati di unione di menu combinato servizio toomove hello e aggiornare la mappa partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-230">A SQL authentication login with read/write access toohello DBs will be needed for hello Split-Merge service toomove data and update hello shard map.</span></span> <span data-ttu-id="e44d0-231">Poiché hello servizio di suddivisione unione viene eseguito nel cloud hello, non supporta attualmente l'autenticazione integrata.</span><span class="sxs-lookup"><span data-stu-id="e44d0-231">Since hello Split-Merge Service runs in hello cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="e44d0-232">Verificare che sia configurato il server di SQL Azure hello tooallow accesso dall'indirizzo IP hello della macchina hello eseguire tali script.</span><span class="sxs-lookup"><span data-stu-id="e44d0-232">Make sure hello Azure SQL server is configured tooallow access from hello IP address of hello machine running these scripts.</span></span> <span data-ttu-id="e44d0-233">È possibile trovare questa impostazione nel server SQL Azure hello / configurazione / indirizzi IP consentiti.</span><span class="sxs-lookup"><span data-stu-id="e44d0-233">You can find this setting under hello Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="e44d0-234">Eseguire l'ambiente di esempio hello toocreate script SetupSampleSplitMergeEnvironment.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-234">Execute hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello sample environment.</span></span>
   
   <span data-ttu-id="e44d0-235">L'esecuzione dello script verrà cancellano i dati di gestione di mappa partizioni esistenti strutture di database di gestione della mappa partizioni hello e partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-235">Running this script will wipe out any existing shard map management data structures on hello shard map manager database and hello shards.</span></span> <span data-ttu-id="e44d0-236">Potrebbe essere script hello toorerun utile se si desidera mappa partizioni di hello toore inizializzare o partizioni.</span><span class="sxs-lookup"><span data-stu-id="e44d0-236">It may be useful toorerun hello script if you wish toore-initialize hello shard map or shards.</span></span>
   
   <span data-ttu-id="e44d0-237">Riga di comando di esempio:</span><span class="sxs-lookup"><span data-stu-id="e44d0-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="e44d0-238">Eseguire hello Getmappings.ps1 script tooview hello mapping attualmente presenti nell'ambiente di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-238">Execute hello Getmappings.ps1 script tooview hello mappings that currently exist in hello sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="e44d0-239">Eseguire hello ExecuteSampleSplitMerge.ps1 script tooexecute un'operazione di divisione (spostamento dei dati di hello metà nella partizione secondo di hello prima partizione toohello) e quindi un'operazione di unione (spostamento dati hello nella partizione prima di hello).</span><span class="sxs-lookup"><span data-stu-id="e44d0-239">Execute hello ExecuteSampleSplitMerge.ps1 script tooexecute a split operation (moving half hello data on hello first shard toohello second shard) and then a merge operation (moving hello data back onto hello first shard).</span></span> <span data-ttu-id="e44d0-240">Se è stato configurato SSL e l'endpoint http hello sinistro disabilitata, verificare di utilizzare endpoint https:// hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-240">If you configured SSL and left hello http endpoint disabled, ensure that you use hello https:// endpoint instead.</span></span>
   
   <span data-ttu-id="e44d0-241">Riga di comando di esempio:</span><span class="sxs-lookup"><span data-stu-id="e44d0-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="e44d0-242">Se si riceve hello di sotto di errore, è probabilmente un problema con il certificato dell'endpoint di Web.</span><span class="sxs-lookup"><span data-stu-id="e44d0-242">If you receive hello below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="e44d0-243">Ritentare la connessione degli endpoint Web toohello con un browser qualsiasi e controllare se è presente un errore di certificato.</span><span class="sxs-lookup"><span data-stu-id="e44d0-243">Try connecting toohello Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="e44d0-244">Se ha avuto esito positivo, output di hello dovrebbe essere simile hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e44d0-244">If it succeeded, hello output should look like hello below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="e44d0-245">Ora è possibile sperimentare il processo con altri tipi di dati.</span><span class="sxs-lookup"><span data-stu-id="e44d0-245">Experiment with other data types!</span></span> <span data-ttu-id="e44d0-246">Tutti questi script accettano un parametro di ShardKeyType - facoltativo che consente di tipo di chiave toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-246">All of these scripts take an optional -ShardKeyType parameter that allows you toospecify hello key type.</span></span> <span data-ttu-id="e44d0-247">valore predefinito di Hello è Int32, ma è anche possibile specificare Int64, Guid o Binary.</span><span class="sxs-lookup"><span data-stu-id="e44d0-247">hello default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="e44d0-248">Creare richieste</span><span class="sxs-lookup"><span data-stu-id="e44d0-248">Create requests</span></span>
<span data-ttu-id="e44d0-249">servizio Hello può essere utilizzato tramite l'interfaccia utente web hello o mediante l'importazione e uso di modulo di PowerShell SplitMerge.psm1 hello che verrà inviate le richieste tramite ruolo web hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-249">hello service can be used either by using hello web UI or by importing and using hello SplitMerge.psm1 PowerShell module which will submit your requests through hello web role.</span></span>

<span data-ttu-id="e44d0-250">servizio Hello può spostare i dati in tabelle partizionate sia tabelle di riferimento.</span><span class="sxs-lookup"><span data-stu-id="e44d0-250">hello service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="e44d0-251">Una tabella partizionata ha una colonna chiave di partizionamento e ospita dati di riga diversi per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="e44d0-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="e44d0-252">Una tabella di riferimento non è partizionata in modo che contenga hello stessa riga di dati in ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="e44d0-252">A reference table is not sharded so it contains hello same row data on every shard.</span></span> <span data-ttu-id="e44d0-253">Tabelle di riferimento sono utili per i dati non vengono modificati spesso e viene utilizzato tooJOIN con le tabelle partizionate nelle query.</span><span class="sxs-lookup"><span data-stu-id="e44d0-253">Reference tables are useful for data that does not change often and is used tooJOIN with sharded tables in queries.</span></span>

<span data-ttu-id="e44d0-254">In ordine tooperform un'operazione di unione di menu combinato, è necessario dichiarare tabelle partizionate hello e tabelle di riferimento che si desidera toohave spostato.</span><span class="sxs-lookup"><span data-stu-id="e44d0-254">In order tooperform a split-merge operation, you must declare hello sharded tables and reference tables that you want toohave moved.</span></span> <span data-ttu-id="e44d0-255">Questa operazione viene eseguita con hello **SchemaInfo** API.</span><span class="sxs-lookup"><span data-stu-id="e44d0-255">This is accomplished with hello **SchemaInfo** API.</span></span> <span data-ttu-id="e44d0-256">Questa API è hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="e44d0-256">This API is in hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="e44d0-257">Per ogni tabella partizionata, creare un **ShardedTableInfo** oggetto che descrive nome di schema della tabella hello padre (facoltativo, valore predefinito è troppo "dbo"), hello nome della tabella e il nome di colonna della tabella che contiene la chiave di partizionamento orizzontale hello hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-257">For each sharded table, create a **ShardedTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”), hello table name, and hello column name in that table that contains hello sharding key.</span></span>
2. <span data-ttu-id="e44d0-258">Per ogni tabella di riferimento, creare un **ReferenceTableInfo** oggetto che descrive nome di schema della tabella hello padre (facoltativo, valore predefinito è troppo "dbo") e il nome di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-258">For each reference table, create a **ReferenceTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”) and hello table name.</span></span>
3. <span data-ttu-id="e44d0-259">Aggiungere hello sopra TableInfo oggetti tooa nuova **SchemaInfo** oggetto.</span><span class="sxs-lookup"><span data-stu-id="e44d0-259">Add hello above TableInfo objects tooa new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="e44d0-260">Ottenere un riferimento tooa **ShardMapManager** oggetto e chiamare **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-260">Get a reference tooa **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="e44d0-261">Aggiungere hello **SchemaInfo** toohello **SchemaInfoCollection**, fornendo il nome della mappa partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="e44d0-261">Add hello **SchemaInfo** toohello **SchemaInfoCollection**, providing hello shard map name.</span></span>

<span data-ttu-id="e44d0-262">Un esempio di questo può essere visualizzato in hello SetupSampleSplitMergeEnvironment.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="e44d0-262">An example of this can be seen in hello SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="e44d0-263">Hello servizio di suddivisione unione non crea il database di destinazione hello (o dello schema per tutte le tabelle nel database di hello) per l'utente.</span><span class="sxs-lookup"><span data-stu-id="e44d0-263">hello Split-Merge service does not create hello target database (or schema for any tables in hello database) for you.</span></span> <span data-ttu-id="e44d0-264">Devono essere creati in precedenza prima di inviare un servizio toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="e44d0-264">They must be pre-created before sending a request toohello service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e44d0-265">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="e44d0-265">Troubleshooting</span></span>
<span data-ttu-id="e44d0-266">Si può vedere hello messaggio seguente durante l'esecuzione di script di powershell di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="e44d0-266">You may see hello below message when running hello sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

<span data-ttu-id="e44d0-267">Questo errore indica che il certificato SSL non è configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="e44d0-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="e44d0-268">Seguire le istruzioni di hello nella sezione 'Connessione con un web browser'.</span><span class="sxs-lookup"><span data-stu-id="e44d0-268">Please follow hello instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="e44d0-269">Se non è possibile inviare richieste, potrebbe essere visualizzato il seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="e44d0-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="e44d0-270">In questo caso, controllare il file di configurazione, in base alle impostazioni hello particolare per **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="e44d0-270">In this case, check your configuration file, in particular hello setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="e44d0-271">Questo errore indica in genere che il ruolo di lavoro hello Impossibile inizializzare correttamente il database dei metadati hello al primo utilizzo.</span><span class="sxs-lookup"><span data-stu-id="e44d0-271">This error typically indicates that hello worker role could not successfully initialize hello metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

