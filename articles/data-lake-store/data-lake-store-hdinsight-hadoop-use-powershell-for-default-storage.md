---
title: HDInsight aaaCreate cluster con archivio Data Lake come spazio di archiviazione predefinito tramite PowerShell | Microsoft documenti
description: Utilizzare toocreate Azure PowerShell e usare il cluster HDInsight con archivio Azure Data Lake
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>Creare cluster HDInsight con Data Lake Store come risorsa di archiviazione predefinita usando PowerShell
> [!div class="op_single_selector"]
> * [Utilizzare hello portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Usare PowerShell (per l'archiviazione predefinita)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Usare PowerShell (per l'archiviazione aggiuntiva)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Usare Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Informazioni su come cluster di toouse tooconfigure di Azure PowerShell HDInsight di Azure con l'archivio Azure Data Lake, come spazio di archiviazione predefinito. Per istruzioni su come creare un cluster HDInsight con Data Lake Store come risorsa di archiviazione aggiuntiva, vedere [Usare Azure PowerShell per creare un cluster HDInsight con Data Lake Store (come risorsa di archiviazione predefinita)](data-lake-store-hdinsight-hadoop-use-powershell.md).

Di seguito sono riportate alcune considerazioni importanti per l'uso di HDInsight con Data Lake Store:

* cluster di HDInsight toocreate opzione Hello con accesso tooData Lake archivio come spazio di archiviazione predefinito è disponibile per HDInsight versione 3.5 e 3.6.

* toocreate opzione Hello cluster di HDInsight con accesso tooData Lake archivio come spazio di archiviazione predefinito *non disponibile* per il cluster HDInsight Premium.

tooconfigure toowork di HDInsight con archivio Data Lake tramite PowerShell, seguire le istruzioni hello hello accanto cinque sezioni.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, assicurarsi che siano soddisfatti i seguenti requisiti hello:

* **Una sottoscrizione di Azure**: andare troppo[versione di valutazione gratuita di Azure ottenere](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 o versione successiva**: vedere [come tooinstall e configurare PowerShell](/powershell/azure/overview).
* **Windows Software Development Kit (SDK)**: tooinstall Windows SDK, andare troppo[download e strumenti per Windows 10](https://dev.windows.com/en-us/downloads). Hello SDK è toocreate utilizzato un certificato di sicurezza.
* **Entità servizio di Azure Active Directory**: questa esercitazione viene descritto come toocreate un'entità servizio in Azure Active Directory (Azure AD). Tuttavia, toocreate un'entità servizio, è necessario essere un amministratore di Azure AD. Se si è un amministratore, è possibile ignorare questo prerequisito e continuare l'esercitazione hello.

    >[!NOTE]
    >È possibile creare un'entità servizio solo se si è un amministratore di Azure AD. Prima di poter creare un cluster HDInsight con Data Lake Store, un amministratore di Azure AD deve creare un'entità servizio. Hello dell'entità servizio deve essere creato con un certificato, come descritto in [creare un'entità servizio con certificato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Creare un account Archivio Data Lake
un account archivio Data Lake, toocreate hello seguenti:

1. Dal desktop, aprire una finestra di PowerShell e quindi immettere hello i frammenti di codice riportato di seguito. Quando si è richiesta toosign in, Accedi come uno degli amministratori di sottoscrizioni hello o proprietari. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Se si registra provider di risorse di archivio Data Lake hello e ricevere un messaggio di errore simile troppo`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, la sottoscrizione potrebbe non essere abilitata per l'archivio Data Lake. tooenable la sottoscrizione di Azure per l'anteprima pubblica di archivio Data Lake hello, seguire le istruzioni hello [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md).
    >

2. Un account Data Lake Store è associato a un gruppo di risorse di Azure. Iniziare creando un gruppo di risorse.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Verrà visualizzato un output simile al seguente:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Creare un account Data Lake Store. account Hello nome specificato deve contenere solo lettere minuscole e numeri.

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

4. L'uso di archivio Data Lake come spazio di archiviazione predefinito richiede toospecify che una radice percorso toowhich hello specifici per i cluster vengono copiati durante la creazione del cluster. toocreate un percorso, ovvero **/cluster/hdiadlcluster** nel frammento di codice hello, utilizzare hello seguente cmdlet:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Impostare per l'autenticazione basata su ruoli accedere tooData Lake archivio
Ogni sottoscrizione di Azure è associata a un'entità di Azure AD. Utenti e servizi di accedere alle risorse di sottoscrizione utilizzando hello portale Azure oppure hello API di gestione risorse di Azure devono prima autenticarsi con Azure AD. Accesso tooAzure sottoscrizioni e dei servizi tramite l'assegnazione di ruolo appropriato di hello in una risorsa di Azure. Per i servizi, un'entità servizio identifica il servizio di hello in Azure AD.

In questa sezione viene illustrato come servizio toogrant un'applicazione, ad esempio HDInsight, accesso tooan risorse di Azure (Buongiorno account archivio Data Lake creato in precedenza). Farlo, creare un servizio principale per un'applicazione hello e assegnare ruoli tooit tramite PowerShell.

tooset autenticazione di Active Directory per Azure Data Lake, eseguire attività di hello in hello nelle due sezioni che seguono.

### <a name="create-a-self-signed-certificate"></a>Creare un certificato autofirmato
Assicurarsi di avere [Windows SDK](https://dev.windows.com/en-us/downloads) installato prima di procedere con hello i passaggi in questa sezione. È necessario avere anche creato una directory, ad esempio *C:\mycertdir*, in cui creare il certificato di hello.

1. Finestra di PowerShell hello, passare toohello percorso in cui è installato Windows SDK (in genere, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) e utilizzare hello [MakeCert] [ makecert] toocreate utilità un certificato autofirmato e una chiave privata. Utilizzare hello seguenti comandi:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Password della chiave privata hello tooenter richiesta sarà. Dopo che il comando hello viene eseguito correttamente, si otterranno **CertFile.cer** e **myKey** nella directory di hello certificato specificato.
2. Hello utilizzare [Pvk2Pfx] [ pvk2pfx] utilità tooconvert hello PVK e con estensione cer file file con estensione pfx creato tooa MakeCert. Eseguire hello comando seguente:

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Quando richiesto, immettere hello password della chiave privata specificato in precedenza. valore specificato per hello Hello **- ordine di acquisto** parametro sia hello password associata a file con estensione pfx hello. Dopo il comando hello è stato completato, verrà visualizzato anche un **CertFile.pfx** nella directory di hello certificato specificato.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Creare un'applicazione Azure AD e un'entità servizio
In questa sezione, creare un'entità servizio per un'applicazione Azure AD, assegnare un'entità servizio di ruolo toohello e l'autenticazione come entità servizio hello fornendo un certificato. toocreate un'applicazione in Azure AD, eseguire hello seguenti comandi:

1. Incollare i seguenti cmdlet nella finestra della console PowerShell hello hello. Verificare che tale valore hello specificato per hello **- DisplayName** la proprietà è univoca. i valori per Hello **- home page** e **- IdentiferUris** sono i valori segnaposto e non vengono verificati.

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
3. Concedere radice dell'archivio Data Lake toohello accesso dell'entità servizio hello e tutte le cartelle di hello nel percorso radice hello specificato in precedenza. Utilizzare hello seguente cmdlet:

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Creare un cluster di HDInsight Linux con archivio Data Lake come spazio di archiviazione predefinito hello

In questa sezione, creare un cluster HDInsight Hadoop Linux con archivio Data Lake come spazio di archiviazione predefinito hello. Per questa versione, hello cluster HDInsight e archivio Data Lake deve trovarsi nella hello nello stesso percorso.

1. Recuperare l'ID tenant di sottoscrizione hello e archiviarlo toouse in un secondo momento.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Creare cluster HDInsight hello utilizzando hello seguente cmdlet:

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    Al termine hello cmdlet è stato completato correttamente, verrà visualizzato un output che elenca i dettagli del cluster hello.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Eseguire i processi di prova in hello HDInsight cluster toouse archivio Data Lake
Dopo aver configurato un cluster HDInsight, è possibile eseguire i processi di prova su di esso tooensure che possa accedere a archivio Data Lake. toodo in tal caso, eseguire una toocreate processo Hive di esempio una tabella che utilizza dati di esempio hello sono già disponibili in archivio Data Lake in  *<cluster root>/example/data/sample.log*.

In questa sezione, si stabilisce una connessione Secure Shell (SSH) in hello cluster HDInsight Linux creato e quindi si esegue una query Hive di esempio.

* Se si utilizza un toomake di client Windows una connessione SSH in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se si utilizza un toomake client Linux una connessione SSH in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. Dopo aver effettuato la connessione hello, avviare l'interfaccia della riga di comando di hello Hive (CLI) utilizzando hello comando seguente:

        hive
2. Utilizzare prova CLI tooenter prova seguendo le istruzioni toocreate una nuova tabella denominata **veicoli** utilizzando dati di esempio hello in archivio Data Lake:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Output della query hello dovrebbe nella console di hello SSH.

    >[!NOTE]
    >Hello percorso toohello dati di esempio in hello precedente comando CREATE TABLE sono `adl:///example/data/`, dove `adl:///` è hello cluster radice. Dopo l'esempio hello di directory principale del cluster hello specificato in questa esercitazione, il comando di hello è `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. È possibile utilizzare l'alternativa più breve hello o fornire principale del cluster toohello percorso completo di hello.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>Accedere a Data Lake Store tramite comandi HDFS
Dopo aver configurato l'archivio Data Lake toouse cluster HDInsight hello, è possibile utilizzare l'archivio di hello tooaccess di Hadoop Distributed File System (HDFS) shell dei comandi.

In questa sezione, si effettua una connessione SSH in hello cluster HDInsight Linux creato e quindi eseguire i comandi HDFS hello.

* Se si utilizza un toomake di client Windows una connessione SSH in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se si utilizza un toomake client Linux una connessione SSH in cluster hello, vedere [utilizzo di SSH con basati su Linux, Hadoop in HDInsight da Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

Dopo aver effettuato la connessione hello, elenco file hello in archivio Data Lake tramite hello HDFS file system comando seguente.

    hdfs dfs -ls adl:///

È inoltre possibile utilizzare hello `hdfs dfs -put` comando tooupload alcuni file tooData Lake archiviati e quindi utilizzare `hdfs dfs -ls` tooverify file hello se caricati correttamente.

## <a name="see-also"></a>Vedere anche
* [Portale di Azure: creare un toouse cluster HDInsight archivio Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
