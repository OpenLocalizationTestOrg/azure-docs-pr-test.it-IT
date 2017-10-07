---
title: aaaUse tooget portale Azure introduttiva archivio Data Lake | Documenti Microsoft
description: Utilizzare hello toocreate portale Azure un account archivio Data Lake ed eseguire operazioni di base in hello archivio Data Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Introduzione a archivio Azure Data Lake tramite hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK per Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Interfaccia della riga di comando di Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Informazioni su come toouse hello Azure toocreate portale account archivio Azure Data Lake e come eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare file di dati, eliminare l'account, e così via. Per altre informazioni, vedere [Panoramica di Azure Data Lake Store](data-lake-store-overview.md).

Dopo due video Hello contenga hello stesse informazioni come descritto in questo articolo:

* [Creare un account Archivio Data Lake](https://mix.office.com/watch/1k1cycy4l4gen)
* [Gestire i dati in archivio Data Lake tramite hello Esplora dati](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Creare un account di Azure Data Lake Store

1. Accedere di nuovo toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **NUOVO**, selezionare **Data + Storage** (Dati + archiviazione), quindi fare clic su **Azure Data Lake Store**. Leggere le informazioni di hello in hello **archivio Azure Data Lake** blade e quindi fare clic su **crea** in hello inferiore sinistro del pannello hello.
3. In hello **archivio Data Lake di nuovo** pannello fornire valori hello, come illustrato nella seguente schermata hello:
   
    ![Creare un nuovo account Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Creare un nuovo account Azure Data Lake")
   
   * **Nome**. Immettere un nome univoco per hello account archivio Data Lake.
   * **Sottoscrizione**. Selezionare la sottoscrizione di hello in cui si desidera toocreate un nuovo account archivio Data Lake.
   * **Gruppo di risorse**. Selezionare un gruppo di risorse esistente oppure hello **Crea nuovo** toocreate opzione uno. Un gruppo di risorse è un contenitore che contiene risorse correlate per un'applicazione. Per altre informazioni, vedere [Gruppi di risorse in Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Percorso**: selezionare un percorso in cui si desidera account archivio Data Lake di hello toocreate.
   * **Impostazioni crittografia**. Sono disponibili tre opzioni:
     
     * **Non abilitare la crittografia**.
     * **Usare chiavi gestite da Azure Data Lake**,  Se si desidera toomanage archivio Azure Data Lake le chiavi di crittografia.
     * **Scegliere le chiavi da Azure Key Vault**. È possibile selezionare un'istanza di Azure Key Vault esistente oppure crearne una nuova. chiavi di hello toouse da un insieme di credenziali chiave, è necessario assegnare le autorizzazioni per hello account archivio Azure Data Lake tooaccess hello insieme credenziali chiavi Azure. Per istruzioni hello, vedere [assegnare autorizzazioni tooAzure insieme di credenziali chiave](#assign-permissions-to-azure-key-vault).
       
        ![Crittografia di Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Crittografia di Data Lake Store")
       
        Fare clic su **OK** in hello **le impostazioni di crittografia** blade.

        Per altre informazioni, vedere [Crittografia dei dati in Azure Data Lake Store](./data-lake-store-encryption.md).

4. Fare clic su **Crea**. Se si sceglie di dashboard toohello dell'account toopin hello, si passa nuovamente toohello dashboard ed è possibile visualizzare lo stato di avanzamento hello del provisioning dell'account archivio Data Lake. Una volta hello account archivio Data Lake viene eseguito il provisioning, pannello account hello viene visualizzato.

È anche possibile creare un account Data Lake Store usando modelli di Azure Resource Manager. Tali modelli sono accessibili dalla pagina [Modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/?term=data+lake+store).

- Senza crittografia dei dati: [Deploy Azure Data Lake Store account with no data encryption](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/) (Distribuire un account Azure Data Lake Store senza crittografia dei dati).
- Con crittografia dei dati con Data Lake Store: [Deploy Data Lake Store account with encryption(Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/) (Distribuire un account Data Lake Store con crittografia - Data Lake).
- Con crittografia dei dati con Azure Key Vault: [Deploy Data Lake Store account with encryption(Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/) (Distribuire un account Data Lake Store con crittografia - Key Vault).

### <a name="assign-permissions-to-azure-key-vault"></a>Assegnare autorizzazioni tooAzure insieme di credenziali chiave
Se si usa chiavi di crittografia di tooconfigure un insieme di credenziali chiave Azure su hello account archivio Data Lake, è necessario configurare l'accesso tra account archivio Data Lake di hello e hello insieme credenziali chiavi Azure. Eseguire hello seguendo i passaggi toodo così.

1. Se si utilizza le chiavi da hello insieme di credenziali chiave di Azure, pannello hello hello account archivio Data Lake viene visualizzato un avviso nella parte superiore di hello. Fare clic su hello di hello avviso tooopen **configurare le autorizzazioni di insieme di credenziali chiave** blade.
   
    ![Crittografia di Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Crittografia di Data Lake Store")
2. Pannello Hello Mostra due opzioni tooconfigure accesso.
   
   * Nella prima opzione hello, fare clic su **concedere l'autorizzazione** tooconfigure accesso. prima opzione Hello è abilitata solo quando l'utente di hello che ha creato l'account archivio Data Lake hello è anche un amministratore per hello insieme credenziali chiavi Azure.
   * Hello è visualizzato nel pannello hello cmdlet di PowerShell di toorun hello. Proprietario hello toobe di hello insieme credenziali chiavi Azure o si dispone delle autorizzazioni di hello possibilità toogrant su hello insieme credenziali chiavi Azure. Dopo aver eseguito i cmdlet di hello, tornare toohello pannello e fare clic su **abilitare** tooconfigure accesso.

## <a name="createfolder"></a>Creare delle cartelle in Azure Data Lake Store
È possibile creare cartelle sotto la toomanage account archivio Data Lake e archiviare i dati.

1. Aprire l'account archivio Data Lake hello creato. Nel riquadro di sinistra hello, fare clic su **Sfoglia**, fare clic su **archivio Data Lake**, dal Pannello di archivio Data Lake hello, quindi fare clic su nome dell'account hello in cui si desidera toocreate cartelle. Se è stato aggiunto schermata iniziale di hello account toohello, fare clic su riquadro account.
2. Nel pannello dell'account di Archivio Data Lake, fare clic su **Esplora dati**.
   
    ![Creare cartelle nell'account Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Creare cartelle nell'account Data Lake Store")
3. Nel pannello account archivio Data Lake, fare clic su **nuova cartella**, immettere un nome per la nuova cartella hello e quindi fare clic su **OK**.
   
    ![Creare cartelle nell'account Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Creare cartelle nell'account Data Lake Store")
   
    cartella Hello appena creata viene elencata in hello **Esplora dati** blade. È possibile creare cartelle nidificate fino a qualsiasi livello.
   
    ![Creare cartelle nell'account Data Lake](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Creare cartelle nell'account Data Lake")

## <a name="uploaddata"></a>Caricamento account archivio Data Lake tooAzure di dati
È possibile caricare il tooan dati account archivio Azure Data Lake direttamente in hello livello o tooa cartella radice che è stato creato all'interno di account hello. In hello seguente schermata, seguire tooupload passaggi hello una sottocartella tooa file da hello **Esplora dati** blade. In questa acquisizione dello schermo, file hello è caricato tooa sottocartella nel percorso di navigazione hello (contrassegnati in una casella rossa).

Se si sta cercando alcuni tooupload di dati di esempio, è possibile ottenere hello **dati ambulanza** cartella hello [Git Repository di Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Caricare dati](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Caricare dati")

## <a name="properties"></a>Le proprietà e le azioni disponibili in hello dati archiviati
Fare clic su hello tooopen di file appena aggiunto hello **proprietà** blade. sono disponibili in questo pannello Proprietà Hello associata a file hello e le azioni di hello che è possibile eseguire nel file hello. È inoltre possibile copiare hello percorso completo toofile nell'account archivio Azure Data Lake, evidenziato nella casella rossa hello hello seguente schermata:

![Le proprietà sui dati hello](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "proprietà sui dati hello")

* Fare clic su **anteprima** toosee un'anteprima del file hello, direttamente dal browser hello. È possibile specificare il formato di hello dell'anteprima di hello anche. Fare clic su **anteprima**, fare clic su **formato** in hello **anteprima File** pannello e hello **Anteprima formato** pannello specificare opzioni, ad esempio hello numero di righe toodisplay, codifica toouse toouse delimitatore, e così via.
  
  ![Formato di anteprima file](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "Formato di anteprima file")
* Fare clic su **scaricare** computer tooyour di toodownload hello file.
* Fare clic su **Rinomina file** file hello toorename.
* Fare clic su **Elimina file** file hello toodelete.

## <a name="secure-your-data"></a>Protezione dei dati
È possibile proteggere i dati di hello archiviati nell'account archivio Azure Data Lake tramite Azure Active Directory e il controllo di accesso (ACL). Per istruzioni su come toodo che, vedere [la protezione dei dati in archivio Azure Data Lake](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Eliminare l'account di Azure Data Lake Store
Fare clic su un account archivio Azure Data Lake, il pannello di archivio Data Lake, toodelete **eliminare**. azione di hello tooconfirm, sarà hello quale account toodelete nome hello tooenter richiesta. Immettere il nome di hello dell'account di hello e quindi fare clic su **eliminare**.

![Eliminare l'account Data Lake](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Eliminare l'account Data Lake")

## <a name="next-steps"></a>Passaggi successivi
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Accesso ai log di diagnostica per Azure Data Lake Store](data-lake-store-diagnostic-logs.md)

