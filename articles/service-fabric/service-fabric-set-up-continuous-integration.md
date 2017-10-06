---
title: aaaSet l'integrazione continua per Azure microservizi | Documenti Microsoft
description: Ottenere una panoramica su come tooset di integrazione continua e distribuzione per un'applicazione di Service Fabric utilizzando Visual Studio Team Services (VSTS).
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>Configurare l'integrazione e la distribuzione continue di Service Fabric con Visual Studio Team Services
Questo articolo descrive hello tooset di passaggi di integrazione continua e distribuzione per un'applicazione Azure Service Fabric utilizzando Visual Studio Team Services (VSTS).

Questo documento riflette la routine corrente hello ed è previsto toochange nel tempo.

## <a name="prerequisites"></a>Prerequisiti
tooget avviato, seguire questi passaggi:

1. Assicurarsi di disporre di account di accesso tooa Team Services o [crearlo](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) manualmente.
2. Assicurarsi di disporre di progetto team di accesso tooa Team Services o [crearlo](https://www.visualstudio.com/docs/setup-admin/create-team-project) manualmente.
3. Assicurarsi di disporre di un toowhich di cluster di Service Fabric è possibile distribuire l'applicazione o crearne uno utilizzando hello [portale di Azure](service-fabric-cluster-creation-via-portal.md), un [modello di Azure Resource Manager](service-fabric-cluster-creation-via-arm.md), o [Visual Studio ](service-fabric-cluster-creation-via-visual-studio.md).
4. Verificare di aver già creato un progetto di applicazione di Service Fabric (.sfproj). È necessario disporre di un progetto che è stato creato o aggiornato con Service Fabric SDK 2.1 o versione successiva (file .sfproj hello deve contenere un valore di proprietà relative a ProjectVersion di 1.1 o versione successiva).

> [!NOTE]
> Non sono più necessari agenti di compilazione personalizzati. Gli agenti ospitati di Team Services sono ora preinstallati con il software di gestione dei cluster di Service Fabric, il che consente la distribuzione delle applicazioni direttamente dagli agenti.
> 
> 

## <a name="configure-and-share-your-source-files"></a>Configurare e condividere i file di origine
innanzitutto Hello che si desidera aggiungere toodo preparare un profilo di pubblicazione per l'uso dal processo di distribuzione hello eseguita all'interno di Team Services.  profilo di pubblicazione Hello deve essere configurato tootarget hello cluster è stata preparata in precedenza:

1. Scegliere un profilo di pubblicazione all'interno del progetto di applicazione che si desidera toouse del flusso di lavoro di integrazione continua. Seguire hello [pubblicare istruzioni](service-fabric-publish-app-remote-cluster.md) sulla toopublish un cluster remoto tooa delle applicazioni. Non è effettivamente necessario toopublish applicazione tuttavia. È possibile fare clic su hello **salvare** collegamento ipertestuale in hello finestra di dialogo di pubblicazione dopo aver configurato in modo appropriato le cose.
2. Se si desidera toobe l'applicazione aggiornati per ogni distribuzione che si verifica all'interno di Team Services, si desidera hello tooconfigure aggiornamento tooenable del profilo di pubblicazione. Nella finestra di dialogo utilizzata stessa pubblicazione nel passaggio 1 di hello, verificare che hello **hello aggiornamento applicazione** casella di controllo è selezionata.  Sono disponibili maggiori informazioni sulla [configurazione delle impostazioni di aggiornamento aggiuntive](service-fabric-visualstudio-configure-upgrade.md). Fare clic su hello **salvare** toohello di collegamento ipertestuale toosave hello impostazioni profilo di pubblicazione.
3. Assicurarsi di avere salvato le modifiche toohello pubblicare profilo e annullare hello finestra di dialogo pubblicazione.
4. Ora è troppo tempo[condividere i file di origine di progetto di applicazione](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) con Team Services. Una volta che i file di origine sono accessibili in Team Services, è possibile procedere con toohello il passaggio successivo della generazione di compilazioni. 

## <a name="create-a-build-definition"></a>Creare una definizione di compilazione
Una definizione di compilazione di Team Services descrive un flusso di lavoro costituito da un set di istruzioni di compilazione che vengono eseguite in sequenza. obiettivo di Hello della definizione di compilazione hello che si sta creando è un pacchetto di applicazione di Service Fabric tooproduce e altri elementi, che possono essere un'applicazione hello toodeploy utilizzato. Sono disponibili maggiori informazioni sulle [definizioni di compilazione](https://www.visualstudio.com/docs/build/define/create)di Team Services.

### <a name="create-a-definition-from-hello-build-template"></a>Creare una definizione di modello di compilazione hello
1. Aprire il progetto team in Visual Studio Team Services.
2. Seleziona hello **compilare** scheda.
3. Verde hello selezionare  **+**  firmare toocreate una nuova definizione di compilazione.
4. Nella finestra di dialogo hello visualizzata, selezionare **applicazione di Azure Service Fabric** all'interno di hello **compilare** categoria di modello.
5. Selezionare **Avanti**.
6. Selezionare il repository di hello e un ramo associato all'applicazione di Service Fabric.
7. Coda dell'agente selezionare hello desiderato toouse. Sono supportati agenti ospitati.
8. Selezionare **Crea**.
9. Salvare la definizione di compilazione hello e specificare un nome.
10. Hello paragrafo seguente è una descrizione dei passaggi di compilazione hello generato dal modello hello:

| Istruzione di compilazione | Descrizione |
| --- | --- |
| NuGet restore |Consente di ripristinare i pacchetti NuGet hello per la soluzione hello. |
| Compila la soluzione \*.sln |Compila l'intera soluzione hello. |
| Compila la soluzione \*.sfproj |Genera l'errore di pacchetto di applicazione di Service Fabric hello è un'applicazione hello toodeploy utilizzato. percorso del pacchetto dell'applicazione Hello è toobe specificato all'interno di directory dell'artefatto della compilazione hello. |
| Update Service Fabric App Versions |Aggiorna i valori di versione di hello in tooallow file manifesto del pacchetto di applicazione hello per supporto per l'aggiornamento. Vedere hello [pagina documentazione attività](https://go.microsoft.com/fwlink/?LinkId=820529) per ulteriori informazioni. |
| Copiare i file |Hello copie pubblicare toobe gli artefatti di compilazione di applicazione i parametri file toohello utilizzata per la distribuzione e del profilo. |
| Publish Artifact |Pubblica artefatti di compilazione hello. Consente a una definizione di versione degli elementi della build tooconsume hello. |

### <a name="verify-hello-default-set-of-tasks"></a>Verificare i set di attività predefinito hello
1. Verificare hello **soluzione** campo di input per hello **ripristino NuGet** e **Compila soluzione** istruzioni di compilazione.  Per impostazione predefinita, queste istruzioni di compilazione eseguire a seguito di tutti i file di soluzione sono contenuti nel repository di hello associata.  Se si desidera solo toooperate definizione di compilazione hello in uno di questi file di soluzione, è necessario il file toothat del percorso di tooexplicitly aggiornamento hello.
2. Verificare hello **soluzione** campo di input per hello **pacchetto applicazione** istruzione di compilazione.  Per impostazione predefinita, questa istruzione di compilazione si presuppone un solo progetto di applicazione di Service Fabric (.sfproj) esiste nel repository di hello.  Se si dispone di più di tali file nel repository e si desidera tootarget solo uno di essi per questa definizione di compilazione, è necessario il file toothat del percorso di tooexplicitly aggiornamento hello.  Se si desidera toopackage applicazione più progetti nel repository, è necessario toocreate aggiuntive **compilazione di Visual Studio** i passaggi nella definizione di compilazione hello che ogni destinazione di un progetto di applicazione.  È quindi necessario anche hello tooupdate **argomenti MSBuild** campo per ciascuna di queste istruzioni di compilazione in modo che il percorso di pacchetto hello è univoco per ognuno di essi.
3. Verificare il comportamento del controllo delle versioni hello definito in hello **versioni di App Fabric di aggiornamento servizio** istruzione di compilazione.  Per impostazione predefinita, questa istruzione di compilazione Accoda hello compilazione tooall versione valori numerici nei file manifesto del pacchetto di applicazione hello. Vedere hello [pagina documentazione attività](https://go.microsoft.com/fwlink/?LinkId=820529) per ulteriori informazioni. Ciò è utile per supportare l'aggiornamento dell'applicazione poiché la distribuzione di ogni aggiornamento richiede valori di versione diversi dalla distribuzione precedente hello. Se si sta prendendo in considerazione l'aggiornamento dell'applicazione toouse non nel flusso di lavoro, è possibile considerare la disabilitazione di questa istruzione di compilazione. Deve essere disabilitato se si intende tooproduce una compilazione che può essere utilizzati toooverwrite un'applicazione di Service Fabric esistente. distribuzione di Hello non riesce se versione hello di un'applicazione hello prodotta dalla compilazione hello corrisponde hello versione dell'applicazione hello cluster hello.
4. Se la soluzione contiene un progetto .NET Core, è necessario assicurarsi che la definizione di compilazione contiene un'istruzione di compilazione che consente di ripristinare le dipendenze di hello:
   1. Selezionare **Aggiungi istruzione di compilazione...**.
   2. Individuare hello **della riga di comando** attività all'interno della scheda utilità hello e fare clic sul pulsante Aggiungi.
   3. Per i campi di input dell'attività hello, utilizzare hello seguenti valori:
   4. Strumento: dotnet
   5. Argomenti: restore
   6. Trascinare l'attività hello in modo che sia immediatamente dopo hello **ripristino NuGet** passaggio.
5. Salvare le modifiche sono state apportate toohello definizione di compilazione.

### <a name="try-it"></a>Prova
Selezionare **Accoda compilazione** toomanually avviare una compilazione. Le compilazioni vengono attivate anche al momento del push o dell'archiviazione. Dopo aver verificato che la compilazione hello è in esecuzione correttamente, è possibile procedere con toodefining una definizione di versione che distribuisce il cluster tooa dell'applicazione.

## <a name="create-a-release-definition"></a>Creare una definizione di versione
Una definizione di versione di Team Services descrive un flusso di lavoro costituito da un set di attività che vengono eseguite in sequenza. obiettivo di Hello della definizione di versione di hello che si sta creando è tootake un pacchetto di applicazione e distribuirla tooa cluster. Se utilizzati insieme, hello definizione di compilazione e definizione di versione può eseguire l'intero flusso di lavoro hello da a partire da tooending i file di origine con un'applicazione in esecuzione nel cluster. Sono disponibili maggiori informazioni sulle [definizioni di versione](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)di Team Services.

### <a name="create-a-definition-from-hello-release-template"></a>Creare una definizione di modello di rilascio hello
1. Aprire il progetto in Visual Studio Team Services.
2. Seleziona hello **versione** scheda.
3. Selezionare hello verde  **+**  toocreate una nuova definizione di versione e selezionate **Crea definizione di versione** nel menu hello.
4. Nella finestra di dialogo hello visualizzata, selezionare **distribuzione dell'infrastruttura dei servizi Azure** all'interno di hello **distribuzione** categoria di modello.
5. Selezionare **Avanti**.
6. Selezionare una definizione di compilazione hello desiderato toouse come origine di hello questa definizione di versione.  definizione di compilazione Hello versione definizione riferimenti hello gli elementi che sono state prodotte da hello selezionato.
7. Controllare hello **distribuzione continua** casella di controllo se si desidera toohave Team Services crea una nuova versione e distribuire automaticamente un'applicazione hello Service Fabric ogni volta che viene completata una compilazione.
8. Coda dell'agente selezionare hello desiderato toouse. Sono supportati agenti ospitati.
9. Selezionare **Crea**.
10. Modificare il nome di definizione di hello facendo clic sull'icona di hello Matita nella parte superiore di hello della pagina hello.
11. Selezionare hello cluster toowhich deve essere distribuito l'applicazione hello **connessione Cluster** campo di input dell'attività hello. connessione cluster Hello fornisce le informazioni necessarie hello che consente a hello distribuzione attività tooconnect toohello cluster. Se si dispone ancora una connessione di cluster per il cluster, selezionare hello **Gestisci** collegamento ipertestuale Avanti toohello campo tooadd uno. Nella pagina hello visualizzata eseguire hello alla procedura seguente:
    1. Selezionare **nuovo Endpoint del servizio** e quindi selezionare **Azure Service Fabric** dal menu di hello.
    2. Selezionare il tipo di hello di autenticazione utilizzato dal cluster hello da questo endpoint di destinazione.
    3. Definire un nome per la connessione in hello **nome connessione** campo.  In genere, si utilizzerà il nome di hello del cluster.
    4. Definire l'URL dell'endpoint di connessione client hello in hello **Cluster Endpoint** campo.  Esempio: tcp://contoso.westus.cloudapp.azure.com:19000.
    5. Per le credenziali di Azure Active Directory, definire le credenziali di hello da toouse tooconnect toohello cluster in hello **Username** e **Password** campi.
    6. Per l'autenticazione basata su certificati, definire hello Base64 codifica del file del certificato client hello in hello **certificato Client** campo.  Vedere la finestra popup della Guida hello in tale campo per informazioni su come tooget tale valore.  Se il certificato è protetto da password, è possibile definire password hello in hello **Password** campo.
    7. Confermare le modifiche facendo clic su **OK**. Dopo lo spostamento indietro tooyour la definizione di versione, fare clic sull'icona di aggiornamento hello in hello **connessione Cluster** endpoint di hello toosee campo appena aggiunto.
12. Salvare la definizione di versione hello.

> [!NOTE]
> Gli account Microsoft, ad esempio @hotmail.com o @outlook.com, non sono supportati con l'autenticazione di Azure Active Directory.
> 
> 

definizione di Hello creato è costituita da un'attività di tipo **la distribuzione di applicazioni di servizio dell'infrastruttura**. Vedere hello [pagina documentazione attività](https://go.microsoft.com/fwlink/?LinkId=820528) per ulteriori informazioni su questa attività.

### <a name="verify-hello-template-defaults"></a>Verificare le impostazioni predefinite di hello modello
1. Verificare hello **profilo di pubblicazione** campo di input per hello **distribuire l'applicazione di Service Fabric** attività. Per impostazione predefinita, questo campo fa riferimento a un profilo di pubblicazione denominato Cloud.xml contenuti in elementi di compilazione hello. Se si desidera tooreference un profilo di pubblicazione diverso o se la generazione di hello contiene più i pacchetti di applicazioni ai relativi elementi, è necessario il percorso di hello tooupdate in modo appropriato.
2. Verificare hello **pacchetto di applicazione** campo di input per hello **distribuire l'applicazione di Service Fabric** attività. Per impostazione predefinita, questo campo fa riferimento a percorso del pacchetto dell'applicazione predefinito hello utilizzato nel modello di definizione di compilazione hello.  Se è stato modificato il percorso del pacchetto di hello predefinito dell'applicazione in hello definizione di compilazione, è necessario il percorso di hello tooupdate in modo appropriato qui anche.

### <a name="try-it"></a>Prova
Selezionare **creare rilasciare** da hello **versione** toomanually menu pulsante Crea una versione. Nella finestra di dialogo hello visualizzata, selezionare compilazione hello desiderato versione hello toobase su e quindi fare clic su **crea**. Se è abilitata la distribuzione continua, le versioni verranno create automaticamente quando la definizione di compilazione hello associata viene completata una compilazione.

## <a name="next-steps"></a>Passaggi successivi
altre informazioni sull'integrazione continua con le applicazioni di Service Fabric, leggere i seguenti articoli hello toolearn:

* [Documentazione di Team Services](https://www.visualstudio.com/docs/overview)
* [Gestione della compilazione in Team Services](https://www.visualstudio.com/docs/build/overview)
* [Gestione della versione in Team Services](https://www.visualstudio.com/docs/release/overview)

