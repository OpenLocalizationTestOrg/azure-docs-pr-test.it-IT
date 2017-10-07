---
title: Archiviazione di Azure con una soluzione di integrazione continua Jenkins aaaUsing | Documenti Microsoft
description: In questa esercitazione viene illustrato come toouse hello Azure servizio blob come repository per gli elementi creati da una soluzione di integrazione continuata Jenkins di compilazione.
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
ms.openlocfilehash: 853c0c6c028596b3057bdc1dbbc59a9415c0fb77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-jenkins-continuous-integration-solution"></a>Uso di Archiviazione di Azure con una soluzione di Integrazione continuata Jenkins
## <a name="overview"></a>Panoramica
Hello informazioni riportate di seguito viene illustrato come archiviazione di Blob toouse come repository di artefatti di compilazione creata da una soluzione di integrazione continua Jenkins (CI) oppure come origine di toobe possibile scaricare i file in un processo di compilazione. Uno degli scenari di hello dove si trova questo utile è quando il codice sia scritto in un ambiente di sviluppo agile (tramite Java o in altri linguaggi) e le compilazioni in base alle integrazione continua, è necessario un repository per gli elementi di compilazione, in modo che è possibile , ad esempio, condividerle con altri membri dell'organizzazione, i clienti, o gestire un archivio. Un altro scenario è quando il processo di compilazione stesso richiede altri file, ad esempio, toodownload di dipendenze, come parte di hello input di compilazione.

In questa esercitazione si utilizzerà hello plug-in archiviazione di Azure per l'integrazione continua Jenkins resi disponibili da Microsoft.

## <a name="overview-of-jenkins"></a>Panoramica su Jenkins
Jenkins consente l'integrazione continua di un progetto software e consente agli sviluppatori tooeasily integrare le modifiche al codice e avere compilazioni prodotte automaticamente e spesso, con un conseguente incremento della produttività hello di sviluppatori hello. Le compilazioni vengono con controllo delle versioni e artefatti di compilazione possono essere caricato toovarious repository. Questo argomento viene illustrato come toouse Azure nell'archiviazione blob come repository di hello di artefatti di compilazione hello. Verrà visualizzata anche la modalità di archiviazione blob dipendenze toodownload da Azure.

Per ulteriori informazioni su Jenkins, vedere [Meet Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins).

## <a name="benefits-of-using-hello-blob-service"></a>Vantaggi dell'utilizzo del servizio Blob hello
Vantaggi dell'utilizzo di hello Blob servizio toohost includono gli elementi di compilazione di sviluppo agile:

* Disponibilità elevata degli elementi di compilazione e/o delle dipendenze scaricabili.
* Migliori prestazioni nel caricamento degli elementi di compilazione da parte della soluzione di Integrazione continuata Jenkins.
* Migliori prestazioni durante il download degli elementi di compilazione da parte di clienti e partner.
* Controllo dei criteri di accesso da parte dell'utente, che prevede la possibilità di scelta tra accesso anonimo, accesso condiviso con scadenza, accesso con firma, accesso privato e così via.

## <a name="prerequisites"></a>Prerequisiti
Si sarà necessario hello seguenti hello toouse servizio Blob con la soluzione di integrazione Continuata Jenkins:

* Una soluzione di Integrazione continuata Jenkins.
  
    Se attualmente non è una soluzione di integrazione Continuata Jenkins, è possibile eseguire una soluzione di integrazione Continuata Jenkins utilizzando hello tecnica seguente:
  
  1. In un computer in cui è abilitato Java, scaricare il file jenkins.war dall'indirizzo <http://jenkins-ci.org>.
  2. Al prompt dei comandi che è aperto toohello cartella che contiene jenkins.war, eseguire:
     
      `java -jar jenkins.war`

  3. Nel browser aprire `http://localhost:8080/`. Verrà aperta hello Jenkins dashboard in cui sarà possibile utilizzare tooinstall e configurare i plug-in archiviazione di Azure hello.
     
      Durante una tipica soluzione di integrazione Continuata Jenkins imposteranno toorun come servizio, l'esecuzione war Jenkins hello nella riga di comando hello sarà sufficiente per questa esercitazione.
* Un account Azure. È possibile registrarsi per un account Azure all'indirizzo <http://www.azure.com>.
* Un account di archiviazione di Azure. Se si dispone già di un account di archiviazione, è possibile crearne uno attenendosi alla procedura hello in [creare un Account di archiviazione](../common/storage-create-storage-account.md#create-a-storage-account).
* Familiarità con la soluzione di integrazione Continuata Jenkins hello è consigliata ma non obbligatorio, come hello contenuto seguente utilizzerà tooshow un esempio di base hello passaggi necessari quando si utilizza il servizio Blob di hello come repository per l'integrazione continua Jenkins gli elementi di compilazione.

## <a name="how-toouse-hello-blob-service-with-jenkins-ci"></a>Come toouse hello servizio Blob con integrazione Continuata Jenkins
servizio Blob di hello toouse con Jenkins, sarà necessario tooinstall hello plug-in archiviazione di Azure, configurare l'account di archiviazione di toouse plug-in di hello e quindi creare un'azione post-compilazione che consente di caricare l'account di archiviazione tooyour artefatti di compilazione. Questi passaggi sono descritti nelle seguenti sezioni hello.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Come tooinstall hello plug-in archiviazione di Azure
1. Nel dashboard di Jenkins hello, fare clic su **gestire Jenkins**.
2. In hello **gestire Jenkins** pagina, fare clic su **gestire plug-in**.
3. Fare clic su hello **disponibile** scheda.
4. In hello **artefatto Uploaders** sezione controllo **plug-in archiviazione di Microsoft Azure**.
5. Fare clic su **Install without restart** oppure su **Download now and install after restart**.
6. Riavviare Jenkins.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Come tooconfigure hello toouse plug-in archiviazione di Azure all'account di archiviazione
1. Nel dashboard di Jenkins hello, fare clic su **gestire Jenkins**.
2. In hello **gestire Jenkins** pagina, fare clic su **Configura sistema**.
3. In hello **configurazione di Account di archiviazione di Microsoft Azure** sezione:
   1. Immettere il nome di account di archiviazione, è possibile ottenere da hello [portale Azure](https://portal.azure.com).
   2. Immettere la chiave di account di archiviazione, anche ottenuta dal hello [portale Azure](https://portal.azure.com).
   3. Utilizzare il valore predefinito hello per **URL Endpoint del servizio Blob** se si utilizza cloud pubblico di Azure hello. Se si utilizza un altro cloud di Azure, è possibile utilizzare endpoint hello come specificato in hello [portale Azure](https://portal.azure.com) dell'account di archiviazione. 
   4. Fare clic su **convalidare le credenziali di archiviazione** toovalidate account di archiviazione. 
   5. [Facoltativo] Se si dispone di account di archiviazione aggiuntivi che si desidera tooyour disponibili effettuata integrazione Continuata Jenkins, fare clic su **aggiungere altri account di archiviazione**.
   6. Fare clic su **salvare** toosave le impostazioni.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Come toocreate un'azione post-compilazione che consente di caricare l'account di archiviazione tooyour artefatti di compilazione
Ai fini delle istruzioni, prima è necessario un processo che creare più file, quindi aggiungere nell'account di archiviazione di hello azione post-compilazione tooupload hello file tooyour toocreate.

1. Nel dashboard di Jenkins hello, fare clic su **nuovo elemento**.
2. Nome del processo hello **MyJob**, fare clic su **compila un progetto software stile liberare**, quindi fare clic su **OK**.
3. In hello **compilare** sezione di configurazione del processo di hello, fare clic su **istruzione di compilazione Aggiungi** e scegliere **comando batch di Windows eseguire**.
4. In **comando**, utilizzare hello seguenti comandi:

    ```   
    md text
    cd text
    echo Hello Azure Storage from Jenkins > hello.txt
    date /t > date.txt
    time /t >> date.txt
    ```

5. In hello **azioni post-compilazione** sezione di configurazione del processo di hello, fare clic su **aggiungere azioni post-compilazione** e scegliere **caricare nell'archiviazione Blob tooAzure elementi**.
6. Per **nome account di archiviazione**, selezionare hello toouse account di archiviazione.
7. Per **nome contenitore**, specificare il nome di contenitore hello. (verrà creato il contenitore di hello se non esiste quando vengono caricati gli artefatti di compilazione hello.) È possibile utilizzare le variabili di ambiente, pertanto in questo esempio immettere **${JOB_NAME}** come nome del contenitore hello.
   
    **Suggerimento**
   
    Di sotto di hello **comando** sezione in cui è stato immesso uno script per **comando batch di Windows eseguire** è un collegamento di variabili di ambiente toohello riconosciute da Jenkins. Fare clic su tale collegamento, i nomi delle variabili di ambiente hello toolearn e descrizioni. Tenere presente che ambiente variabili che contengono caratteri speciali, ad esempio hello **BUILD_URL** variabile di ambiente, non sono consentiti come un nome di contenitore o un percorso virtuale comune.
8. Ai fini di questo esempio, fare clic su **Make new container public by default** . (Se si desidera toouse un contenitore privato, è necessario toocreate un accesso tooallow firma di accesso condiviso. Ovvero esula hello in questo argomento. Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](../storage-dotnet-shared-access-signature-part-1.md).
9. [Facoltativo] Fare clic su **contenitore pulito prima di caricare** se si desidera hello contenitore toobe cancellato il contenuto prima di artefatti di compilazione vengono caricati (lasciarla deselezionata se non si desidera contenuto hello tooclean del contenitore hello).
10. Per **tooupload elenco di elementi**, immettere  **testo /*. txt**.
11. In **Common virtual path for uploaded artifacts**, ai fini di questa esercitazione, immettere **${BUILD\_ID}/${BUILD\_NUMBER}**.
12. Fare clic su **salvare** toosave le impostazioni.
13. Nel dashboard di Jenkins hello, fare clic su **compilare ora** toorun **MyJob**. Esaminare l'output di console hello per lo stato. Messaggi di stato per l'archiviazione di Azure verranno inclusi nell'output di console hello all'avvio di azione di post-compilazione hello artefatti di compilazione tooupload.
14. Al completamento del processo di hello, è possibile esaminare gli elementi di compilazione hello aprendo blob pubblici hello.
    1. Account di accesso toohello [portale Azure](https://portal.azure.com).
    2. Fare clic su **Storage**.
    3. Fare clic su nome account di archiviazione hello utilizzata per Jenkins.
    4. Fare clic su **Containers**.
    5. Fare clic sul contenitore hello denominato **myjob**, hello versione minuscola del nome di processo hello assegnato al momento della creazione processo Jenkins hello. In Archiviazione di Azure i nomi di contenitori e i nomi di BLOB sono riportati in lettere minuscole (e si applica la distinzione maiuscole/minuscole). Nell'elenco di hello di BLOB per il contenitore di hello denominato **myjob** dovrebbe **hello.txt** e **date.txt**. Copia URL hello per uno di questi elementi e aprirlo nel browser. File di testo hello caricato verrà visualizzato come un elemento di compilazione.

È possibile creare solo un'azione post-compilazione che carica nell'archiviazione blob tooAzure elementi per ogni processo. Si noti che l'archiviazione blob di hello singola azione di post-compilazione tooupload elementi tooAzure possa specificare diversi file (inclusi i caratteri jolly) e toofiles percorsi all'interno di **tooupload elenco di elementi** usando un punto e virgola come separatore. Ad esempio, se il Jenkins compila produce file JAR e i file con estensione TXT dell'area di lavoro **compilare** cartella e si desidera tooupload entrambi tooAzure nell'archiviazione blob, usare hello seguenti per hello **tooupload elenco di elementi** valore: **compilare /\*JAR; compilazione /\*. txt**. Inoltre, è possibile utilizzare la sintassi di due punti doppio toospecify toouse un percorso all'interno di nome blob hello. Ad esempio, se si desidera hello JAR tooget caricati utilizzando **file binari** nel percorso blob hello e tooget file TXT di hello caricati utilizzando **avvisi** nel percorso blob hello, utilizzare la seguente hello per hello  **Elenco di tooupload elementi** valore: **compilare /\*. jar::binaries; compilazione /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Come toocreate un'istruzione di compilazione che esegue il download da archiviazione blob di Azure
Hello alla procedura seguente viene illustrato come una compilazione tooconfigure passaggio elementi toodownload dall'archiviazione blob di Azure. Questo potrebbe essere utile se si desidera che gli elementi tooinclude la compilazione, ad esempio, JAR presenti in Azure nell'archiviazione blob.

1. In hello **compilare** sezione di configurazione del processo di hello, fare clic su **istruzione di compilazione Aggiungi** e scegliere **scaricare dall'archiviazione Blob di Azure**.
2. Per **nome account di archiviazione**, selezionare hello toouse account di archiviazione.
3. Per **nome contenitore**, specificare il nome di hello del contenitore di hello che contiene il BLOB hello desiderato toodownload. A questo scopo, è possibile usare le variabili di ambiente.
4. Per **nome Blob**, specificare il nome di blob hello. A questo scopo, è possibile usare le variabili di ambiente. Inoltre, è possibile utilizzare un asterisco come carattere jolly dopo aver specificato hello lettere iniziali del nome blob hello. Ad esempio, digitando **project\*** si specificano tutti i BLOB i cui nomi iniziano per **project**.
5. [Facoltativo] Per **percorso di Download**, specificare il percorso di hello hello Jenkins computer in cui si desidera file toodownload dall'archiviazione blob di Azure. A questo scopo, è anche possibile usare le variabili di ambiente. (Se non si specifica un valore per **percorso di Download**, file hello dall'archiviazione blob di Azure sarà dell'area di lavoro del processo scaricato toohello.)

Se si dispone di altri elementi desiderati toodownload dall'archiviazione blob di Azure, è possibile creare istruzioni di compilazione aggiuntive.

Dopo aver eseguito una compilazione, è possibile controllare hello output di console di cronologia di compilazione o esaminare il percorso di download, toosee hello se BLOB previsti sono stati scaricati correttamente.  

## <a name="components-used-by-hello-blob-service"></a>Componenti utilizzati dal servizio Blob hello
esempio Hello viene fornita una panoramica dei componenti del servizio Blob hello.

* **Account di archiviazione**: tutti gli accessi tooAzure archiviazione viene eseguita tramite un account di archiviazione. Si tratta hello di livello più elevato dello spazio dei nomi di hello per accedere agli oggetti BLOB. Un account può contenere un numero illimitato di contenitori, purché la dimensione totale di questi sia inferiore a 100 TB.
* **Contenitore:**un contenitore fornisce un raggruppamento di un set di BLOB. Tutti i BLOB devono trovarsi in un contenitore. In un account può esistere un numero illimitato di contenitori. In un contenitore può essere archiviato un numero illimitato di BLOB.
* **BLOB:**un file di qualsiasi tipo e dimensione. Vi sono due tipi di BLOB che possono essere archiviati in Archiviazione di Azure: BLOB di pagine e BLOB in blocchi. La maggior parte dei file sono BLOB in blocchi. Un blob in blocchi singolo può essere backup too200GB nella dimensione. In questa esercitazione vengono utilizzati BLOB in blocchi. BLOB di pagine, un altro tipo di blob, è possibile backup too1TB, le dimensioni e sono più efficiente quando gli intervalli di byte in un file vengono modificati spesso. Per altre informazioni sui BLOB, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Formato URL**: i BLOB sono indirizzabili utilizzando hello seguendo il formato di URL:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (cloud pubblico di Azure toohello formato hello sopra si applica. Se si utilizza un altro cloud di Azure, utilizzare endpoint hello all'interno di hello [portale Azure](https://portal.azure.com) toodetermine l'endpoint dell'URL.)
  
    In formato hello precedente, `storageaccount` rappresenta hello nome dell'account di archiviazione, `container_name` rappresenta hello nome del contenitore, e `blob_name` rappresenta hello nome del blob di, rispettivamente. All'interno di nome contenitore hello, è possibile avere più percorsi, separati da un barra rovesciata,  **/** . nome del contenitore di esempio Hello in questa esercitazione è stata **MyJob**, e **${compilare\_ID} / ${compilare\_numero}** è stata utilizzata per hello comuni percorso virtuale risultanti in hello blob con un URL di hello seguente formato:
  
    `http://example.blob.core.windows.net/myjob/2014-04-14_23-57-00/1/hello.txt`

## <a name="next-steps"></a>Passaggi successivi
* [Meet Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins)
* [Azure Storage SDK per Java](https://github.com/azure/azure-storage-java)
* [Riferimento all'SDK del client di archiviazione di Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST dei servizi di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)

Per altre informazioni, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).