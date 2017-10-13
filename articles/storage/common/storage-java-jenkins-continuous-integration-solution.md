---
title: Uso di Archiviazione di Azure con una soluzione di Integrazione continuata Jenkins | Microsoft Docs
description: Questa esercitazione illustra come usare il servizio BLOB di Azure come archivio di elementi di compilazione creati da una soluzione di Integrazione continuata Jenkins.
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f4e5ca75-f6cb-4f74-981b-2aa06bb8de45
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 174ac449e803ed5327468a38ea7264cb9923a877
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-azure-storage-with-a-jenkins-continuous-integration-solution"></a>Uso di Archiviazione di Azure con una soluzione di Integrazione continuata Jenkins
## <a name="overview"></a>Overview
L'articolo seguente illustra come usare l'archiviazione BLOB come archivio di elementi di compilazione creati dalla soluzione di integrazione continua (CI) Jenkins o come origine di file scaricabili da usare in un processo di compilazione. Queste informazioni possono rivelarsi utili nel caso in cui si codifichi in un ambiente di sviluppo Agile (utilizzando Java o altri linguaggi), le compilazioni vengano eseguite in base all'integrazione continuata e sia necessario un archivio per gli elementi di compilazione, ad esempio per poterli condividere con altri membri dell'organizzazione o clienti oppure per gestire un archivio. Un altro scenario è quando il processo di compilazione stesso richiede altri file, ad esempio dipendenze da scaricare come parte dell'input di compilazione.

In questa esercitazione si utilizzerà il plug-in di Archiviazione di Azure per l'Integrazione continuata Jenkins reso disponibile da Microsoft.

## <a name="overview-of-jenkins"></a>Panoramica su Jenkins
Jenkins abilita l'integrazione continuata di un progetto software consentendo agli sviluppatori di integrare facilmente le modifiche apportate al codice e produrre compilazioni automaticamente e di frequente, aumentando così la produttività degli sviluppatori. Alle compilazioni è applicato il controllo delle versioni ed è possibile caricare gli elementi di compilazione in diversi archivi. In questo argomento viene illustrato come utilizzare l'archivio BLOB di Azure come archivio per gli elementi di compilazione. Verrà inoltre descritto come scaricare le dipendenze dall'archivio BLOB di Azure.

Per ulteriori informazioni su Jenkins, vedere [Meet Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins).

## <a name="benefits-of-using-the-blob-service"></a>Vantaggi dell'uso del servizio BLOB
Di seguito sono indicati i vantaggi dell'utilizzo del servizio BLOB per ospitare gli elementi di compilazione prodotti dallo sviluppo Agile:

* Disponibilità elevata degli elementi di compilazione e/o delle dipendenze scaricabili.
* Migliori prestazioni nel caricamento degli elementi di compilazione da parte della soluzione di Integrazione continuata Jenkins.
* Migliori prestazioni durante il download degli elementi di compilazione da parte di clienti e partner.
* Controllo dei criteri di accesso da parte dell'utente, che prevede la possibilità di scelta tra accesso anonimo, accesso condiviso con scadenza, accesso con firma, accesso privato e così via.

## <a name="prerequisites"></a>Prerequisiti
Per usare il servizio BLOB con la soluzione di Integrazione continuata Jenkins è necessario quanto segue:

* Una soluzione di Integrazione continuata Jenkins.
  
    Se si è sprovvisti di una soluzione di Integrazione continuata Jenkins è possibile eseguire una soluzione di Integrazione continuata Jenkins applicando la tecnica seguente:
  
  1. In un computer in cui è abilitato Java, scaricare il file jenkins.war dall'indirizzo <http://jenkins-ci.org>.
  2. Al prompt dei comandi aperto nella cartella che contiene jenkins.war eseguire:
     
      `java -jar jenkins.war`

  3. Nel browser aprire `http://localhost:8080/`. Verrà visualizzato il dashboard di Jenkins, che verrà usato per installare e configurare il plug-in di Archiviazione di Azure.
     
      Sebbene sia necessario configurare una tipica soluzione di Integrazione continuata Jenkins per eseguirla come servizio, ai fini di questa esercitazione sarà sufficiente eseguire il file WAR di Jenkins nella riga di comando.
* Un account Azure. È possibile registrarsi per un account Azure all'indirizzo <http://www.azure.com>.
* Un account di archiviazione di Azure. Se non si dispone di un account di archiviazione, è possibile crearne uno attenendosi ai passaggi illustrati in [Creare un account di archiviazione](../common/storage-create-storage-account.md#create-a-storage-account).
* La conoscenza della soluzione di Integrazione continuata Jenkins è consigliata ma non richiesta, poiché nel contenuto seguente verrà usato un esempio semplice per illustrare i passaggi da seguire nell'uso del servizio BLOB come archivio per elementi di compilazione dell'Integrazione continuata Jenkins.

## <a name="how-to-use-the-blob-service-with-jenkins-ci"></a>Come usare il servizio BLOB con l'Integrazione continuata Jenkins
Per usare il servizio BLOB con Jenkins, è necessario installare il plug-in di Archiviazione di Azure, configurare il plug-in per usare l'account di archiviazione e creare un'operazione post-compilazione per il caricamento degli elementi di compilazione nell'account di archiviazione. Questi passaggi vengono descritti nelle sezioni seguenti.

## <a name="how-to-install-the-azure-storage-plugin"></a>Come installare il plug-in di Archiviazione di Azure
1. Nel dashboard di Jenkins fare clic su **Manage Jenkins**.
2. Nella pagina **Manage Jenkins** fare clic su **Manage Plugins**.
3. Fare clic sulla scheda **Available** .
4. Nella sezione **Artifact Uploaders** selezionare **Microsoft Azure Storage plugin**.
5. Fare clic su **Install without restart** oppure su **Download now and install after restart**.
6. Riavviare Jenkins.

## <a name="how-to-configure-the-azure-storage-plugin-to-use-your-storage-account"></a>Come configurare il plug-in di Archiviazione di Azure per usare l'account di archiviazione
1. Nel dashboard di Jenkins fare clic su **Manage Jenkins**.
2. Nella pagina **Manage Jenkins** fare clic su **Configure System**.
3. Nella sezione **Microsoft Azure Storage Account Configuration** :
   1. Immettere il nome dell'account di archiviazione che è possibile ottenere dal [portale di Azure](https://portal.azure.com).
   2. Immettere la chiave dell'account di archiviazione che è possibile ottenere dal [portale di Azure](https://portal.azure.com).
   3. Se si utilizza il servizio Cloud di Azure pubblico, immettere il valore predefinito in **Blob Service Endpoint URL** . Se si utilizza un servizio Cloud di Azure diverso, utilizzare l'endpoint specificato nel [portale di Azure](https://portal.azure.com) per l'account di archiviazione. 
   4. Fare clic su **Validate storage credentials** per convalidare l'account di archiviazione. 
   5. [Facoltativo] Se si dispone di account di archiviazione aggiuntivi che si desidera rendere disponibili all'Integrazione continuata Jenkins, fare clic su **Add more Storage Accounts**.
   6. Per salvare le impostazioni, fare clic su **Save** .

## <a name="how-to-create-a-post-build-action-that-uploads-your-build-artifacts-to-your-storage-account"></a>Creazione di un'operazione post-compilazione per il caricamento degli elementi di compilazione nell'account di archiviazione
Ai fini di questa esercitazione, è necessario innanzitutto creare un processo che crei più file e quindi aggiungere l'operazione post-compilazione per caricare i file nell'account di archiviazione.

1. Nel dashboard di Jenkins fare clic su **New Item**.
2. Denominare il processo **MyJob**, fare clic su **Build a free-style software project** e quindi fare clic su **OK**.
3. Nella sezione **Build** della configurazione del processo fare clic su **Add build step** e scegliere **Execute Windows batch command**.
4. Nella sezione **Command**usare i comandi seguenti:

    ```   
    md text
    cd text
    echo Hello Azure Storage from Jenkins > hello.txt
    date /t > date.txt
    time /t >> date.txt
    ```

5. Nella sezione **Post-build Actions** della configurazione del processo fare clic su **Add post-build action** e scegliere **Upload artifacts to Azure Blob storage**.
6. In **Storage Account Name**scegliere l'account di archiviazione da utilizzare.
7. In **Container Name**specificare il nome del contenitore. Il contenitore verrà creato se non esiste già al momento del caricamento degli elementi di compilazione. È possibile usare variabili di ambiente, pertanto in questo esempio immettere **${JOB_NAME}** come nome del contenitore.
   
    **Suggerimento**
   
    Sotto la sezione **Command** in cui è stato immesso uno script per **Execute Windows batch command** è presente un collegamento alle variabili di ambiente riconosciute da Jenkins. Fare clic sul collegamento per ottenere dettagli sui nomi e le descrizioni delle variabili di ambiente. Si noti che le variabili di ambiente che contengono caratteri speciali, ad esempio la variabile di ambiente **BUILD_URL** non sono ammesse come nome di contenitore o come percorso virtuale comune.
8. Ai fini di questo esempio, fare clic su **Make new container public by default** . Se si intende utilizzare un contenitore privato, è necessario creare una firma di accesso condiviso per consentire l'accesso. Questa operazione non rientra nell'ambito di questo argomento. Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](../storage-dotnet-shared-access-signature-part-1.md).
9. [Facoltativo] Fare clic su **Clean container before uploading** se si vuole cancellare i contenuti dal contenitore prima di caricare gli elementi di compilazione (lasciare questa casella deselezionata se non si vuole pulire i contenuti del contenitore).
10. In **List of Artifacts to upload** immettere **text/*.txt**.
11. In **Common virtual path for uploaded artifacts**, ai fini di questa esercitazione, immettere **${BUILD\_ID}/${BUILD\_NUMBER}**.
12. Per salvare le impostazioni, fare clic su **Save** .
13. Nel dashboard di Jenkins fare clic su **Build Now** per eseguire **MyJob**. Esaminare l'output di console per ottenere informazioni sullo stato. I messaggi di stato per il servizio di archiviazione di Azure verranno inclusi nell'output della console quando l'operazione post-compilazione avvierà il caricamento degli elementi di compilazione.
14. Dopo avere completato il processo, è possibile esaminare gli elementi di compilazione aprendo il BLOB pubblico.
    1. Eseguire l'accesso al [portale di Azure](https://portal.azure.com).
    2. Fare clic su **Storage**.
    3. Fare clic sul nome dell'account di archiviazione utilizzato per Jenkins.
    4. Fare clic su **Containers**.
    5. Fare clic sul contenitore denominato **myjob**, ossia la versione in lettere minuscole del nome processo assegnato al momento della creazione del processo Jenkins. In Archiviazione di Azure i nomi di contenitori e i nomi di BLOB sono riportati in lettere minuscole (e si applica la distinzione maiuscole/minuscole). Nell'elenco di BLOB per il contenitore denominato **myjob** dovrebbero essere inclusi **hello.txt** e **date.txt**. Copiare l'URL di uno di questi elementi e aprirlo nel browser. Verrà visualizzato il file di testo caricato come elemento di compilazione.

È possibile creare solo un'azione post-compilazione per il caricamento di elementi nell'archivio BLOB di Azure per ogni processo. Si noti che la singola azione post-compilazione per il caricamento di elementi nell'archivio BLOB di Azure può specificare file (inclusi caratteri jolly) e percorsi di file diversi in **List of Artifacts to upload** usando un punto e virgola come separatore. Ad esempio, se la compilazione Jenkins crea file JAR e TXT nella cartella **build** dell'area di lavoro dell'utente e si intende caricarli entrambi nell'archiviazione BLOB di Azure, usare quanto segue per il valore **List of Artifacts to upload**: **build/\*.jar;build/\*.txt**. Per specificare il percorso da usare nel nome del BLOB, è anche possibile usare la sintassi con i due punti. Ad esempio, se si vuole caricare i file JAR usando **binaries** nel percorso del BLOB e i file TXT usando **notices** nel percorso del BLOB, immettere quanto segue per il valore **List of Artifacts to upload**: **build/\*.jar::binaries;build/\*.txt::notices**.

## <a name="how-to-create-a-build-step-that-downloads-from-azure-blob-storage"></a>Come creare un passaggio di compilazione per il download di elementi dall'archivio BLOB di Azure
La procedura seguente illustra come configurare un passaggio di compilazione per il download di elementi dall'archivio BLOB di Azure. Questa operazione è utile per includere elementi nella compilazione, ad esempio file JAR conservati nell'archivio BLOB di Azure.

1. Nella sezione **Build** della configurazione del processo fare clic su **Add build step** e scegliere **Download from Azure Blob storage**.
2. In **Storage Account Name**scegliere l'account di archiviazione da utilizzare.
3. In **Container name**specificare il nome del contenitore in cui si trovano i BLOB da scaricare. A questo scopo, è possibile usare le variabili di ambiente.
4. In **Blob name**specificare il nome del BLOB. A questo scopo, è possibile usare le variabili di ambiente. È anche possibile usare un asterisco come carattere jolly dopo avere specificato le lettere iniziali del nome del BLOB. Ad esempio, digitando **project\*** si specificano tutti i BLOB i cui nomi iniziano per **project**.
5. [Facoltativo] In **Download path**specificare il percorso nel computer Jenkins in cui si vuole scaricare i file dall'archivio BLOB di Azure. A questo scopo, è anche possibile usare le variabili di ambiente. Se non si specifica un valore per **Download path**, i file dall'archivio BLOB di Azure verranno scaricati nell'area di lavoro del processo.

Per scaricare elementi aggiuntivi dall'archiviazione BLOB di Azure, è possibile creare altri passaggi di compilazione.

Dopo avere eseguito una build, è possibile verificare l'output della cronologia di compilazione della console o accedere al percorso di download per verificare che siano stati scaricati i BLOB previsti.  

## <a name="components-used-by-the-blob-service"></a>Componenti usati dal servizio BLOB
Di seguito è riportata una panoramica delle componenti del servizio BLOB.

* **Account di archiviazione:**tutti gli accessi ad Archiviazione di Azure vengono eseguiti tramite un account di archiviazione. Questo è il livello più alto dello spazio dei nomi per accedere ai BLOB. Un account può contenere un numero illimitato di contenitori, purché la dimensione totale di questi sia inferiore a 100 TB.
* **Contenitore:**un contenitore fornisce un raggruppamento di un set di BLOB. Tutti i BLOB devono trovarsi in un contenitore. In un account può esistere un numero illimitato di contenitori. In un contenitore può essere archiviato un numero illimitato di BLOB.
* **BLOB:**un file di qualsiasi tipo e dimensione. Vi sono due tipi di BLOB che possono essere archiviati in Archiviazione di Azure: BLOB di pagine e BLOB in blocchi. La maggior parte dei file sono BLOB in blocchi. Un singolo BLOB in blocchi può raggiungere fino a 200 GB di dimensione. In questa esercitazione vengono utilizzati BLOB in blocchi. I BLOB dell'altro tipo, di pagine, possono raggiungere dimensioni fino a 1 TB e risultano più efficienti quando vi sono intervalli di byte all'interno del file soggetti a modifiche frequenti. Per altre informazioni sui BLOB, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Formato dell'URL:**è possibile fare riferimento ai BLOB usando il formato di URL seguente:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    Il formato riportato sopra si riferisce al servizio Cloud Azure pubblico. Se si usa un servizio Cloud Azure diverso, usare l'endpoint specificato nel [portale di Azure](https://portal.azure.com) per determinare l'endpoint dell'URL.
  
    Nel formato riportato sopra, `storageaccount` rappresenta il nome dell'account di archiviazione, `container_name` rappresenta il nome del contenitore e `blob_name` rappresenta il nome del BLOB. Nel nome contenitore è possibile avere percorsi multipli, separati da una barra **/**. Poiché il nome del contenitore usato come esempio in questa esercitazione è **MyJob** e **${BUILD\_ID}/${BUILD\_NUMBER}** è stato usato per il percorso virtuale comune, l'URL del BLOB ha il formato seguente:
  
    `http://example.blob.core.windows.net/myjob/2014-04-14_23-57-00/1/hello.txt`

## <a name="next-steps"></a>Passaggi successivi
* [Meet Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins)
* [Azure Storage SDK per Java](https://github.com/azure/azure-storage-java)
* [Riferimento all'SDK del client di archiviazione di Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST dei servizi di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)

Per altre informazioni, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).