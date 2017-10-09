---
titolo: aaa "PowerShell: cluster HDInsight di Azure con archivio Data Lake come spazio di archiviazione aggiuntivo | Servizi Microsoft Docs": lake-dell'archivio dati, hdinsight documentationcenter: ' autore: manager nitinme: jhubbard editor: cgronlun

ms. AssetID: ms. Service 164ada5a-222e-4be2-bd32-e51dbe993bc0: ms. DevLang archivio data lake: ms. topic na: articolo ms. tgt_pltfrm: Workload na: ms. date big data: author 08/06/2017: nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>Utilizzo di Azure PowerShell toocreate un cluster HDInsight con archivio Data Lake (come ulteriore spazio di archiviazione)
> [!div class="op_single_selector"]
> * [Uso del portale](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Uso di PowerShell (per l'archiviazione predefinita)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Uso di PowerShell (per l'archiviazione aggiuntiva)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Utilizzo di Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Informazioni su come toouse Azure PowerShell tooconfigure un HDInsight cluster con archivio Azure Data Lake **come spazio di archiviazione aggiuntivo**. Per istruzioni su come toocreate un HDInsight cluster con archivio Azure Data Lake come spazio di archiviazione predefinito, vedere [creare un cluster HDInsight con archivio Data Lake come spazio di archiviazione predefinito](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).

> [!NOTE]
> Se si intende archivio Azure Data Lake di toouse come spazio di archiviazione aggiuntivo per il cluster HDInsight, è consigliabile farlo durante la creazione di cluster hello come descritto in questo articolo. Aggiunta archivio Azure Data Lake come tooan ulteriore spazio di archiviazione cluster HDInsight esistente è una complessità del processo e soggetta a tooerrors.
>

Per i tipi di cluster supportati, Data Lake Store può essere usato come risorsa di archiviazione predefinita o come account di archiviazione aggiuntivo. Quando archivio Data Lake viene utilizzato come spazio di archiviazione aggiuntivo, account di archiviazione hello predefinito per i cluster hello saranno ancora BLOB di archiviazione di Azure (WASB) e i file correlati al cluster hello (ad esempio, i log e così via) vengono scritti ancora spazio di archiviazione predefinito di toohello, mentre quelli di hello che si desidera tooprocess possono essere archiviati in un account archivio Data Lake. Utilizzo archivio Data Lake come un account di archiviazione aggiuntive non influisce sulle prestazioni o hello possibilità tooread/scrittura toohello archiviazione dal hello cluster.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Udo di Data Lake Store per l'archiviazione di cluster HDInsight

Di seguito sono riportate alcune considerazioni importanti per l'uso di HDInsight con Data Lake Store:

* Cluster di HDInsight toocreate opzione con accesso tooData Lake archivio come spazio di archiviazione aggiuntivo è disponibile per le versioni 3.2, 3.4, 3.5 e 3.6 di HDInsight.

La configurazione di HDInsight toowork con archivio Data Lake tramite PowerShell include hello alla procedura seguente:

* Creare un Archivio Azure Data Lake
* Impostare per l'autenticazione basata su ruoli accedere tooData Lake archivio
* Creare cluster HDInsight con autenticazione tooData Lake archivio
* Eseguire un processo di test in cluster hello

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 o versioni successive**. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
* **Windows SDK**. Per installarlo, fare clic [qui](https://dev.windows.com/en-us/downloads). Utilizzare questo toocreate un certificato di sicurezza.
* **Entità servizio di Azure Active Directory**. Passaggi di questa esercitazione vengono fornite istruzioni su come toocreate un'entità servizio in Azure AD. Tuttavia, è necessario essere un toocreate di in grado di Azure AD amministratore toobe un'entità servizio. Se si è un amministratore di Azure AD, è possibile ignorare questo prerequisito e continuare l'esercitazione hello.

    **Se non si è un amministratore di Azure AD**, non sarà in grado di tooperform hello passaggi necessari toocreate un'entità servizio. In tal caso, l'amministratore di Azure AD deve creare un'entità servizio prima di creare un cluster HDInsight con l'archivio Data Lake Store. Inoltre, dell'entità servizio hello devono essere creati utilizzando un certificato, come descritto in [creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-azure-data-lake-store"></a>Creare un Archivio Azure Data Lake
Seguire questi toocreate passaggi un archivio Data Lake.

1. Dal desktop, aprire una nuova finestra di Azure PowerShell e immettere hello seguente frammento di codice. Quando richiesto toolog, assicurarsi che si accede con un proprietario o amministratore della sottoscrizione hello:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > Se si riceve un messaggio di errore simile troppo`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` quando si registra provider di risorse di archivio Data Lake hello, è possibile che la sottoscrizione non è abilitata per l'archivio Azure Data Lake. Assicurarsi di abilitare la sottoscrizione di Azure per l'anteprima pubblica di Archivio Data Lake seguendo queste [istruzioni](data-lake-store-get-started-portal.md).
   >
   >
2. Un account di Archivio Azure Data Lake è associato a un gruppo di risorse di Azure. Per iniziare, creare un gruppo di risorse di Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Verrà visualizzato un output simile al seguente:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Creare un account Archivio Azure Data Lake. account Hello nome specificato deve contenere solo lettere minuscole e numeri.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Verrà visualizzato un output simile hello seguente:

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. Caricare alcuni tooAzure di dati di esempio Data Lake. Si userà più avanti in questo articolo di tooverify che dati hello siano accessibili da un cluster HDInsight. Se si sta cercando alcuni tooupload di dati di esempio, è possibile ottenere hello **dati ambulanza** cartella hello [Git Repository di Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Impostare per l'autenticazione basata su ruoli accedere tooData Lake archivio
Ogni sottoscrizione di Azure è associata a una Azure Active Directory. Gli utenti e servizi che accedono a risorse di sottoscrizione hello utilizzando hello portale classico di Azure o API di gestione risorse di Azure devono prima autenticarsi con Azure Active Directory. Accesso tooAzure sottoscrizioni e dei servizi tramite l'assegnazione di ruolo appropriato di hello in una risorsa di Azure.  Per i servizi, un'entità servizio identifica il servizio di hello in hello Azure Active Directory (AAD). In questa sezione viene illustrato come servizio toogrant un'applicazione, ad esempio HDInsight, accesso tooan risorse di Azure (Buongiorno account archivio Azure Data Lake creato in precedenza), creare un'entità servizio per un'applicazione hello e assegnare ruoli toothat tramite Azure PowerShell.

tooset autenticazione di Active Directory per Azure Data Lake, è necessario eseguire hello seguenti attività.

* Creare un certificato autofirmato
* Creare un'applicazione in Azure Active Directory e un'entità servizio

### <a name="create-a-self-signed-certificate"></a>Creare un certificato autofirmato
Assicurarsi di avere [Windows SDK](https://dev.windows.com/en-us/downloads) installato prima di procedere con hello i passaggi in questa sezione. È necessario avere anche creato una directory, ad esempio **C:\mycertdir**, in cui verrà creato il certificato di hello.

1. Dalla finestra di PowerShell hello passare toohello percorso in cui è installato Windows SDK (in genere, `C:\Program Files (x86)\Windows Kits\10\bin\x86` e utilizzare hello [MakeCert] [ makecert] toocreate utilità un certificato autofirmato e un chiave privata. Utilizzare hello i comandi seguenti.

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Password della chiave privata hello tooenter richiesta sarà. Dopo il comando hello viene eseguito correttamente, verrà visualizzato un **CertFile.cer** e **myKey** nella directory di hello certificato specificato.
2. Hello utilizzare [Pvk2Pfx] [ pvk2pfx] utilità tooconvert hello PVK e con estensione cer file file con estensione pfx creato tooa MakeCert. Eseguire hello comando seguente.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Quando richiesto immettere hello password della chiave privata specificato in precedenza. valore specificato per hello Hello **- ordine di acquisto** parametro sia hello password associata al file con estensione pfx hello. Dopo che il comando hello completata correttamente, verrà inoltre visualizzato un CertFile.pfx nella directory di hello certificato specificato.

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>Creare un'applicazione Azure Active Directory e un'entità servizio
In questa sezione, eseguire i passaggi di hello toocreate un'entità servizio per un'applicazione Azure Active Directory, assegnare un'entità servizio di ruolo toohello e l'autenticazione come entità servizio hello fornendo un certificato. Eseguire hello toocreate i comandi seguenti di un'applicazione in Azure Active Directory.

1. Incollare i seguenti cmdlet nella finestra della console PowerShell hello hello. Verificare che un valore specificato per hello hello **- DisplayName** la proprietà è univoca. Hello, inoltre, i valori per **home page -** e **- IdentiferUris** sono i valori segnaposto e non vengono verificati.

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. Creare un'entità servizio utilizzando l'ID applicazione hello.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Concedere al file hello che saranno accessibili dal cluster HDInsight hello e cartella di archivio Data Lake toohello accesso dell'entità servizio hello. frammento di Hello seguente fornisce radice toohello accesso hello (in cui è stata copiata file di dati di esempio hello) dell'account archivio Data Lake e hello file stesso.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>Creare un cluster HDInsight Linux con Data Lake Store come risorsa di archiviazione aggiuntiva

In questa sezione viene creato un cluster HDInsight di Handoop Linux con Data Lake Store come risorsa di archiviazione aggiuntiva. Per questa versione, i cluster HDInsight hello e archivio Data Lake di hello devono trovarsi in hello nello stesso percorso.

1. Avviare durante il recupero degli ID di hello sottoscrizione tenant. che sarà necessario più avanti.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. Per questa versione, per un cluster Hadoop, archivio Data Lake sono utilizzabili solo come un'ulteriore spazio di archiviazione per cluster hello. spazio di archiviazione predefinito Hello saranno ancora BLOB hello in archiviazione di Azure (WASB). In tal caso, verrà innanzitutto creata hello contenitori di archiviazione e l'account di archiviazione necessari per il cluster hello.

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. Creare cluster HDInsight hello. Utilizzare hello cmdlet seguente.

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Al termine cmdlet hello è stata completata correttamente, verrà visualizzato un output elenca i dettagli del cluster hello.


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Eseguire i processi di prova in hello toouse di cluster HDInsight hello archivio Data Lake
Dopo aver configurato un cluster HDInsight, è possibile eseguire i processi di prova in hello cluster tootest tale hello HDInsight cluster può accedere l'archivio Data Lake. toodo in tal caso, si verrà eseguito un processo Hive di esempio che crea una tabella utilizzando i dati di esempio hello caricato archivio precedente tooyour Data Lake.

In questa sezione sarà possibile SSH in HDInsight Linux cluster creato e l'esecuzione di una query Hive esempio hello hello.

* Se si utilizza un tooSSH di client Windows in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se si utilizza un tooSSH client Linux in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. Una volta connessi, è possibile avviare hello Hive CLI utilizzando hello comando seguente:

        hive
2. Tramite hello CLI, immettere hello seguendo le istruzioni toocreate una nuova tabella denominata **veicoli** utilizzando dati di esempio hello in hello archivio Data Lake:

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    Verrà visualizzato un segue toohello simili di output:

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a>Accedere ad Archivio Data Lake tramite comandi HDFS
Dopo aver configurato archivio Data Lake toouse cluster HDInsight hello, è possibile utilizzare hello HDFS shell comandi tooaccess hello archivio.

In questa sezione sarà possibile SSH in HDInsight Linux cluster creato e di eseguire comandi HDFS hello hello.

* Se si utilizza un tooSSH di client Windows in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se si utilizza un tooSSH client Linux in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

Una volta connessi, utilizzare i seguenti file HDFS filesystem comando toolist hello in archivio Data Lake hello hello.

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

Vengono elencati i file hello caricato archivio precedente toohello Data Lake.

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

È inoltre possibile utilizzare hello `hdfs dfs -put` comando tooupload alcuni toohello file archivio Data Lake e quindi utilizzare `hdfs dfs -ls` tooverify file hello se caricati correttamente.

## <a name="see-also"></a>Vedere anche
* [Portale: Creare un toouse cluster HDInsight archivio Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
