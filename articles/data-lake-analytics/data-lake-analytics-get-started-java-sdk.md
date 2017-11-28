---
title: applicazioni di toodevelop aaaUse Data Lake Analitica Java SDK | Documenti Microsoft
description: Usare le applicazioni Azure Data Lake Analitica Java SDK toodevelop
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 07830b36-2fe3-4809-a846-129cf67b6a9e
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0d975812fe659ed34ee9befd37ee7c0bf50d3414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-java-sdk"></a><span data-ttu-id="61b8d-103">Introduzione ad Azure Data Lake Analytics con Java SDK</span><span class="sxs-lookup"><span data-stu-id="61b8d-103">Get started with Azure Data Lake Analytics using Java SDK</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="61b8d-104">Informazioni su come toouse hello Azure Data Lake Analitica Java SDK toocreate un account di Azure Data Lake ed eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare i file di dati, eliminare l'account e con i processi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="61b8d-104">Learn how toouse hello Azure Data Lake Analytics Java SDK toocreate an Azure Data Lake account and perform basic operations such as create folders, upload and download data files, delete your account, and work with jobs.</span></span> <span data-ttu-id="61b8d-105">Per altre informazioni su Data Lake, vedere [Panoramica di Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61b8d-105">For more information about Data Lake, see [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="61b8d-106">In questa esercitazione verrà sviluppata un'applicazione console Java che include esempi di attività amministrative comuni, inoltre saranno creati dati di test e sarà inviato un processo.</span><span class="sxs-lookup"><span data-stu-id="61b8d-106">In this tutorial, you will develop a Java console application which contains samples of common administrative tasks as well as creating test data and submitting a job.</span></span>  <span data-ttu-id="61b8d-107">toogo tramite hello supportato stesso esercitazione usare altri strumenti, fare clic sulle schede di hello in primo piano hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="61b8d-107">toogo through hello same tutorial using other supported tools, click hello tabs on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61b8d-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="61b8d-108">Prerequisites</span></span>
* <span data-ttu-id="61b8d-109">Java Development Kit (JDK) 8 con Java versione 1.8.</span><span class="sxs-lookup"><span data-stu-id="61b8d-109">Java Development Kit (JDK) 8 (using Java version 1.8).</span></span>
* <span data-ttu-id="61b8d-110">IntelliJ o un altro ambiente di sviluppo Java adatto.</span><span class="sxs-lookup"><span data-stu-id="61b8d-110">IntelliJ or another suitable Java development environment.</span></span> <span data-ttu-id="61b8d-111">Questo prerequisito è facoltativo ma consigliato.</span><span class="sxs-lookup"><span data-stu-id="61b8d-111">This is optional but recommended.</span></span> <span data-ttu-id="61b8d-112">istruzioni di Hello seguenti utilizzano IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="61b8d-112">hello instructions below use IntelliJ.</span></span>
* <span data-ttu-id="61b8d-113">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-113">**An Azure subscription**.</span></span> <span data-ttu-id="61b8d-114">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61b8d-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="61b8d-115">Creare un'applicazione Azure Active Directory (AAD) e recuperarne **ID client**, **ID tenant** e **chiave**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-115">Create an Azure Active Directory (AAD) application and retrieve its **Client ID**, **Tenant ID**, and **Key**.</span></span> <span data-ttu-id="61b8d-116">Per ulteriori informazioni sulle applicazioni di Azure ad e istruzioni su come tooget un ID client, vedere [applicazione creare Active Directory e l'entità servizio utilizzando portale](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61b8d-116">For more information about AAD applications and instructions on how tooget a client ID, see [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="61b8d-117">URI di Reply Hello e la chiave sarà disponibile anche dal portale hello dopo aver creato un'applicazione hello e chiave generata.</span><span class="sxs-lookup"><span data-stu-id="61b8d-117">hello Reply URI and Key will also be available from hello portal once you have hello application created and key generated.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="61b8d-118">Come si esegue l'autenticazione tramite Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61b8d-118">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="61b8d-119">frammento di codice Hello seguente fornisce il codice per **interattivo** l'autenticazione, in cui un'applicazione hello fornisce le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="61b8d-119">hello code snippet below provides code for **non-interactive** authentication, where hello application provides its own credentials.</span></span>

<span data-ttu-id="61b8d-120">Sarà necessario toogive risorse toocreate di autorizzazione dell'applicazione in Azure per questa esercitazione toowork.</span><span class="sxs-lookup"><span data-stu-id="61b8d-120">You will need toogive your application permission toocreate resources in Azure for this tutorial toowork.</span></span> <span data-ttu-id="61b8d-121">È **consigliabile** consentire solo applicazione collaboratore autorizzazioni tooa nuovo inutilizzati e vuoto il gruppo di risorse nella sottoscrizione di Azure per scopi di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="61b8d-121">It is **highly recommended** that you only give this application Contributor permissions tooa new, unused, and empty resource group in your Azure subscription for hello purposes of this tutorial.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="61b8d-122">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="61b8d-122">Create a Java application</span></span>
1. <span data-ttu-id="61b8d-123">Aprire IntelliJ e creare un nuovo progetto di Java con hello **riga di comando App** modello.</span><span class="sxs-lookup"><span data-stu-id="61b8d-123">Open IntelliJ and create a new Java project using hello **Command Line App** template.</span></span>
2. <span data-ttu-id="61b8d-124">Fare clic sul progetto hello sul lato sinistro di hello dello schermo e fare clic su **aggiungere supporto per Framework**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-124">Right-click on hello project on hello left-hand side of your screen and click **Add Framework Support**.</span></span> <span data-ttu-id="61b8d-125">Scegliere **Maven** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-125">Choose **Maven** and click **OK**.</span></span>
3. <span data-ttu-id="61b8d-126">Aprire hello appena creato **"pom.xml"** file e aggiungere hello seguente frammento di testo tra hello  **\</version >** tag e hello  **\< /progetto >** tag:</span><span class="sxs-lookup"><span data-stu-id="61b8d-126">Open hello newly created **"pom.xml"** file and add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>

    >[!NOTE]
    ><span data-ttu-id="61b8d-127">Questo passaggio è temporaneo fino a quando non è disponibile in Maven hello Azure Data Lake Analitica SDK.</span><span class="sxs-lookup"><span data-stu-id="61b8d-127">This step is temporary until hello Azure Data Lake Analytics SDK is available in Maven.</span></span> <span data-ttu-id="61b8d-128">Questo articolo verrà aggiornato una volta hello SDK è disponibile in Maven.</span><span class="sxs-lookup"><span data-stu-id="61b8d-128">This article will be updated once hello SDK is available in Maven.</span></span> <span data-ttu-id="61b8d-129">Tutti gli aggiornamenti futuri toothis SDK sarà disponibile tramite Maven.</span><span class="sxs-lookup"><span data-stu-id="61b8d-129">All future updates toothis SDK will be availble through Maven.</span></span>
    >

        <repositories>
            <repository>
                <id>adx-snapshots</id>
                <name>Azure ADX Snapshots</name>
                <url>http://adxsnapshots.azurewebsites.net/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
            <repository>
                <id>oss-snapshots</id>
                <name>Open Source Snapshots</name>
                <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                    <updatePolicy>always</updatePolicy>
                </snapshots>
            </repository>
        </repositories>
        <dependencies>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-authentication</artifactId>
                <version>1.0.0-20160513.000802-24</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-runtime</artifactId>
                <version>1.0.0-20160513.000812-28</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.rest</groupId>
                <artifactId>client-runtime</artifactId>
                <version>1.0.0-20160513.000825-29</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-store</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-analytics</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
        </dependencies>
4. <span data-ttu-id="61b8d-130">Andare troppo**File**, quindi **impostazioni**, quindi **compilare**, **esecuzione**, **distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-130">Go too**File**, then **Settings**, then **Build**, **Execution**, **Deployment**.</span></span> <span data-ttu-id="61b8d-131">Selezionare **Build Tools** (Strumenti di compilazione), **Maven** e quindi **Importing** (Importazione).</span><span class="sxs-lookup"><span data-stu-id="61b8d-131">Select **Build Tools**, **Maven**, **Importing**.</span></span> <span data-ttu-id="61b8d-132">Selezionare **Import Maven projects automatically**(Importa automaticamente progetti Maven).</span><span class="sxs-lookup"><span data-stu-id="61b8d-132">Then check **Import Maven projects automatically**.</span></span>
5. <span data-ttu-id="61b8d-133">Aprire **Main.java** e sostituire hello blocco di codice esistente con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="61b8d-133">Open **Main.java** and replace hello existing code block with hello following code.</span></span> <span data-ttu-id="61b8d-134">Inoltre, specificare i valori hello per i parametri indicati nel frammento di codice hello, ad esempio **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_ resourceGroupName** e sostituire i segnaposto per **ID CLIENT**, **segreto CLIENT**, **ID TENANT**, e  **ID SOTTOSCRIZIONE**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-134">Also, provide hello values for parameters called out in hello code snippet, such as **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName** and replace placeholders for **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID**, and **SUBSCRIPTION-ID**.</span></span>

    <span data-ttu-id="61b8d-135">Questo codice passa attraverso il processo di hello di creazione di account archivio Data Lake e Data Lake Analitica, la creazione di file nell'archivio di hello, in esecuzione un processo, lo stato del processo di recupero, output del processo di download e infine l'eliminazione di account di hello.</span><span class="sxs-lookup"><span data-stu-id="61b8d-135">This code goes through hello process of creating Data Lake Store and Data Lake Analytics accounts, creating files in hello store, running a job, getting job status, downloading job output, and finally deleting hello account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="61b8d-136">È attualmente un problema noto con hello servizio di Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="61b8d-136">There is currently a known issue with hello Azure Data Lake Service.</span></span>  <span data-ttu-id="61b8d-137">Se l'app di esempio hello viene interrotta o si verifica un errore, potrebbe essere toomanually delete hello archivio Data Lake & Data Lake Analitica gli account creati script hello.</span><span class="sxs-lookup"><span data-stu-id="61b8d-137">If hello sample app is interrupted or encounters an error, you may need toomanually delete hello Data Lake Store & Data Lake Analytics accounts that hello script creates.</span></span>  <span data-ttu-id="61b8d-138">Se non si ha familiarità con hello portale, hello [gestire dei Analitica delle Lake Azure dati tramite il portale di Azure](data-lake-analytics-manage-use-portal.md) Guida iniziare.</span><span class="sxs-lookup"><span data-stu-id="61b8d-138">If you're not familiar with hello Portal, hello [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span></span>
   >
   >

        package com.company;

        import com.microsoft.azure.CloudException;
        import com.microsoft.azure.credentials.ApplicationTokenCredentials;
        import com.microsoft.azure.management.datalake.store.*;
        import com.microsoft.azure.management.datalake.store.models.*;
        import com.microsoft.azure.management.datalake.analytics.*;
        import com.microsoft.azure.management.datalake.analytics.models.*;
        import com.microsoft.rest.credentials.ServiceClientCredentials;
        import java.io.*;
        import java.nio.charset.Charset;
        import java.nio.file.Files;
        import java.nio.file.Paths;
        import java.util.ArrayList;
        import java.util.UUID;
        import java.util.List;

        public class Main {
            private static String _adlsAccountName;
            private static String _adlaAccountName;
            private static String _resourceGroupName;
            private static String _location;

            private static String _tenantId;
            private static String _subId;
            private static String _clientId;
            private static String _clientSecret;

            private static DataLakeStoreAccountManagementClient _adlsClient;
            private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;
            private static DataLakeAnalyticsAccountManagementClient _adlaClient;
            private static DataLakeAnalyticsJobManagementClient _adlaJobClient;
            private static DataLakeAnalyticsCatalogManagementClient _adlaCatalogClient;

            public static void main(String[] args) throws Exception {
                _adlsAccountName = "<DATA-LAKE-STORE-NAME>";
                _adlaAccountName = "<DATA-LAKE-ANALYTICS-NAME>";
                _resourceGroupName = "<RESOURCE-GROUP-NAME>";
                _location = "East US 2";

                _tenantId = "<TENANT-ID>";
                _subId =  "<SUBSCRIPTION-ID>";
                _clientId = "<CLIENT-ID>";

                _clientSecret = "<CLIENT-SECRET>"; // TODO: For production scenarios, we recommend that you replace this line with a more secure way of acquiring hello application client secret, rather than hard-coding it in hello source code.

                String localFolderPath = "C:\\local_path\\"; // TODO: Change this tooany unused, new, empty folder on your local machine.

                // Authenticate
                ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
                SetupClients(creds);

                // Create Data Lake Store and Analytics accounts
                WaitForNewline("Authenticated.", "Creating NEW accounts.");
                CreateAccounts();
                WaitForNewline("Accounts created.", "Displaying accounts.");

                // List Data Lake Store and Analytics accounts that this app can access
                System.out.println(String.format("All ADL Store accounts that this app can access in subscription %s:", _subId));
                List<DataLakeStoreAccount> adlsListResult = _adlsClient.getAccountOperations().list().getBody();
                for (DataLakeStoreAccount acct : adlsListResult) {
                    System.out.println(acct.getName());
                }
                System.out.println(String.format("All ADL Analytics accounts that this app can access in subscription %s:", _subId));
                List<DataLakeAnalyticsAccount> adlaListResult = _adlaClient.getAccountOperations().list().getBody();
                for (DataLakeAnalyticsAccount acct : adlaListResult) {
                    System.out.println(acct.getName());
                }
                WaitForNewline("Accounts displayed.", "Creating files.");

                // Create a file in Data Lake Store: input1.csv
                // TODO: these change order in hello next patch
                byte[] bytesContents = "123,abc".getBytes();
                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, "/input1.csv", bytesContents, true);

                WaitForNewline("File created.", "Submitting a job.");

                // Submit a job tooData Lake Analytics
                UUID jobId = SubmitJobByScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input too@\"/output1.csv\" USING Outputters.Csv();", "testJob");
                WaitForNewline("Job submitted.", "Getting job status.");

                // Wait for job completion and output job status
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                System.out.println("Waiting for job completion.");
                WaitForJob(jobId);
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                WaitForNewline("Job completed.", "Downloading job output.");

                // Download job output from Data Lake Store
                DownloadFile("/output1.csv", localFolderPath + "output1.csv");
                WaitForNewline("Job output downloaded.", "Deleting file.");

                // Delete file from Data Lake Store
                DeleteFile("/output1.csv");
                WaitForNewline("File deleted.", "Deleting account.");

                // Delete account
                _adlsClient.getAccountOperations().delete(_resourceGroupName, _adlsAccountName);
                _adlaClient.getAccountOperations().delete(_resourceGroupName, _adlaAccountName);
                WaitForNewline("Account deleted.", "DONE.");
            }

            //Set up clients
            public static void SetupClients(ServiceClientCredentials creds)
            {
                _adlsClient = new DataLakeStoreAccountManagementClientImpl(creds);
                _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClientImpl(creds);
                _adlaClient = new DataLakeAnalyticsAccountManagementClientImpl(creds);
                _adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);
                _adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClientImpl(creds);
                _adlsClient.setSubscriptionId(_subId);
                _adlaClient.setSubscriptionId(_subId);
            }

            // Helper function tooshow status and wait for user input
            public static void WaitForNewline(String reason, String nextAction)
            {
                if (nextAction == null)
                    nextAction = "";

                System.out.println(reason + "\r\nPress ENTER toocontinue...");
                try{System.in.read();}
                catch(Exception e){}

                if (!nextAction.isEmpty())
                {
                    System.out.println(nextAction);
                }
            }

            // Create Data Lake Store and Analytics accounts
            public static void CreateAccounts() throws InterruptedException, CloudException, IOException {
                // Create ADLS account
                DataLakeStoreAccount adlsParameters = new DataLakeStoreAccount();
                adlsParameters.setLocation(_location);

                _adlsClient.getAccountOperations().create(_resourceGroupName, _adlsAccountName, adlsParameters);

                // Create ADLA account
                DataLakeStoreAccountInfo adlsInfo = new DataLakeStoreAccountInfo();
                adlsInfo.setName(_adlsAccountName);

                DataLakeStoreAccountInfoProperties adlsInfoProperties = new DataLakeStoreAccountInfoProperties();
                adlsInfo.setProperties(adlsInfoProperties);

                List<DataLakeStoreAccountInfo> adlsInfoList = new ArrayList<DataLakeStoreAccountInfo>();
                adlsInfoList.add(adlsInfo);

                DataLakeAnalyticsAccountProperties adlaProperties = new DataLakeAnalyticsAccountProperties();
                adlaProperties.setDataLakeStoreAccounts(adlsInfoList);
                adlaProperties.setDefaultDataLakeStoreAccount(_adlsAccountName);

                DataLakeAnalyticsAccount adlaParameters = new DataLakeAnalyticsAccount();
                adlaParameters.setLocation(_location);
                adlaParameters.setName(_adlaAccountName);
                adlaParameters.setProperties(adlaProperties);

                    /* If this line generates an error message like "hello deep update for property 'DataLakeStoreAccounts' is not supported", please delete hello ADLS and ADLA accounts via hello portal and re-run your script. */

                _adlaClient.getAccountOperations().create(_resourceGroupName, _adlaAccountName, adlaParameters);
            }

            //todo: this changes in hello next version of hello API
            public static void CreateFile(String path, String contents, boolean force) throws IOException, CloudException {
                byte[] bytesContents = contents.getBytes();

                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, path, bytesContents, force);
            }

            public static void DeleteFile(String filePath) throws IOException, CloudException {
                _adlsFileSystemClient.getFileSystemOperations().delete(filePath, _adlsAccountName);
            }

            // Download file
            public static void DownloadFile(String srcPath, String destPath) throws IOException, CloudException {
                InputStream stream = _adlsFileSystemClient.getFileSystemOperations().open(srcPath, _adlsAccountName).getBody();

                PrintWriter pWriter = new PrintWriter(destPath, Charset.defaultCharset().name());

                String fileContents = "";
                if (stream != null) {
                    Writer writer = new StringWriter();

                    char[] buffer = new char[1024];
                    try {
                        Reader reader = new BufferedReader(
                                new InputStreamReader(stream, "UTF-8"));
                        int n;
                        while ((n = reader.read(buffer)) != -1) {
                            writer.write(buffer, 0, n);
                        }
                    } finally {
                        stream.close();
                    }
                    fileContents =  writer.toString();
                }

                pWriter.println(fileContents);
                pWriter.close();
            }

            // Submit a U-SQL job by providing script contents.
            // Returns hello job ID
            public static UUID SubmitJobByScript(String script, String jobName) throws IOException, CloudException {
                UUID jobId = java.util.UUID.randomUUID();
                USqlJobProperties properties = new USqlJobProperties();
                properties.setScript(script);
                JobInformation parameters = new JobInformation();
                parameters.setName(jobName);
                parameters.setJobId(jobId);
                parameters.setType(JobType.USQL);
                parameters.setProperties(properties);

                JobInformation jobInfo = _adlaJobClient.getJobOperations().create(_adlaAccountName, jobId, parameters).getBody();

                return jobId;
            }

            // Wait for job completion
            public static JobResult WaitForJob(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                while (jobInfo.getState() != JobState.ENDED)
                {
                    jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName,jobId).getBody();
                }
                return jobInfo.getResult();
            }

            // Get job status
            public static String GetJobStatus(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                return jobInfo.getState().toValue();
            }
        }

1. <span data-ttu-id="61b8d-139">Seguire toorun prompt hello e un'applicazione hello completo.</span><span class="sxs-lookup"><span data-stu-id="61b8d-139">Follow hello prompts toorun and complete hello application.</span></span>

## <a name="see-also"></a><span data-ttu-id="61b8d-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="61b8d-140">See also</span></span>
* <span data-ttu-id="61b8d-141">toosee hello stesso esercitazione con altri strumenti, fare clic sui selettori di hello scheda nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="61b8d-141">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="61b8d-142">toosee una query più complessa, vedere [sito Web di analizzare i log di Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="61b8d-142">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="61b8d-143">tooget iniziare a sviluppare applicazioni U-SQL, vedere [script U-SQL sviluppare utilizzando Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="61b8d-143">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="61b8d-144">toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md), e [riferimenti al linguaggio U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="61b8d-144">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="61b8d-145">Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics con il portale di Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61b8d-145">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="61b8d-146">tooget una panoramica del Data Lake Analitica, vedere [Panoramica di Azure Data Lake Analitica](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61b8d-146">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
