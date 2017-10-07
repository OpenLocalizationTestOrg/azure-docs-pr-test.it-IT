---
title: recapito aaaContinuous per cloud services con Visual Studio Online | Documenti Microsoft
description: Informazioni su come App tooset le opzioni di distribuzione continua per Azure cloud senza salvare i file di configurazione del servizio di archiviazione chiave toohello di diagnostica
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely salvare servizi diagnostica chiave di archiviazione Cloud e di integrazione continua l'installazione e distribuzione tooAzure utilizzando Visual Studio Online
 Oggi è un progetto di origine tooopen pratica comune. Il salvataggio dei segreti dell'applicazione nei file di configurazione non è più considerato sicuro, perché comporta l'esposizione di vulnerabilità della sicurezza a causa della diffusione dei segreti dai controlli di origine pubblica. Risorse nell'ambiente Cloud hello archiviazione segreto come testo normale in un file in una pipeline di integrazione continua non è sicuro uno poiché il server di compilazione, potrebbero essere condivise. In questo articolo viene illustrato come Visual Studio e Visual Studio Online, è possibile ridurre i problemi di sicurezza hello durante lo sviluppo e il processo di integrazione continua.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Rimuovere il segreto della chiave di archiviazione di diagnostica dal file di configurazione del progetto
L'estensione di diagnostica dei Servizi cloud richiede l'Archiviazione di Azure per il salvataggio dei risultati di diagnostica. In precedenza stringa di connessione di archiviazione hello è specificata nei file di configurazione (. cscfg) di servizi Cloud hello e può essere selezionato nel controllo toosource. Nella versione più recente di Azure SDK hello archivio tooonly di comportamento hello una parziale stringa di connessione con la chiave di hello sostituito da un token è stato modificato. Hello alla procedura seguente viene descritto il funzionamento degli strumenti di servizi Cloud nuovo hello:

### <a name="1-open-hello-role-designer"></a>1. Aprire Progettazione ruoli hello
* Fare doppio clic oppure fare clic con il pulsante destro su una finestra di progettazione ruoli di tooopen ruolo di servizi Cloud

![Aprire la finestra di progettazione dei ruoli][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. Nella sezione relativa alla diagnostica è stata aggiunta una nuova casella di controllo "Non rimuovere il segreto della chiave di archiviazione dal file di configurazione del progetto (.cscfg)"
* Se si utilizza l'emulatore di archiviazione locale di hello, questa casella di controllo è disabilitata perché non esiste alcun toomanage secret hello locale stringa di connessione, ovvero UseDevelopmentStorage = true.

![La stringa di connessione dell'emulatore di archiviazione locale non è segreta][1]

* Se si crea un nuovo progetto, questa casella di controllo è deselezionata per impostazione predefinita. Di conseguenza, nella sezione chiave hello di archiviazione della stringa di connessione di archiviazione hello selezionato verrà sostituito con un token. Hello valore del token hello verrà trovato nella cartella AppData Roaming dell'utente corrente hello, ad esempio: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Si noti cartella user\AppData hello è l'accesso controllato dall'account utente e viene considerato segreti di sviluppo toostore un posto sicuro.
> 
> 

![La chiave di archiviazione viene salvata nella cartella del profilo utente][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Selezionare un account di archiviazione di diagnostica
* Selezionare un account di archiviazione dalla finestra di dialogo hello avviata facendo hello "..." . Si noti come stringa di connessione di archiviazione hello generato avrà non chiave dell'account di archiviazione hello.
* Ad esempio: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.    Debug di hello progetto
* F5 toostart debug in Visual Studio. Tutto dovrebbe funzionare in hello stesso modo come prima.
  ![Avviare il debug localmente][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Pubblicare il progetto da Visual Studio
* Avvio hello finestra di dialogo pubblicazione e procedere con le istruzioni Accedi toopublish hello applicaion tooAzure.

### <a name="6-additional-information"></a>6. Informazioni aggiuntive
> Nota: il pannello impostazioni hello in Progettazione ruoli hello viene mantenuta come nel caso di ora. Se si desidera che la funzionalità di gestione di informazioni segrete hello toouse per la diagnostica, passare scheda configurazioni toohello.
> 
> 

![Aggiungere le impostazioni][4]

> Nota: Se abilitato, la chiave di Application Insights hello verrà archiviata come testo normale. chiave di Hello viene utilizzata solo per caricare contenuto in modo che non contiene dati sensibili sia a rischio di compromissione.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Compilare e pubblicare un progetto di Servizi cloud usando i modelli di attività di Visual Studio Online
* Hello alla procedura seguente viene illustrato come integrazione continua per i servizi Cloud toosetup progetto utilizzando l'attività di Visual Studio online:
  ### <a name="1----obtain-a-vso-account"></a>1.    Ottenere un account VSO
* [Creare account di Visual Studio Online] [ Create Visual Studio Online account] se non hai già
* [Creazione del progetto team] [ Create team project] nell'account Visual Studio online

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Configurare il controllo del codice sorgente in Visual Studio
* Connettere il progetto di team tooa

![Connettere il progetto tooteam][5]

![Selezionare tooconnect progetto team a][6]

* Aggiungere il controllo toosource progetto

![Aggiungere il controllo toosource progetto][7]

![Cartella del codice sorgente di mappa progetto tooa][8]

* Archiviare il progetto da Team Explorer

![Controllare nel controllo toosource progetto][9]

### <a name="3----configure-build-process"></a>3.    Configurare il processo di configurazione
* Progetto team tooyour di individuare e aggiungere un nuovo processo di compilazione di modelli

![Aggiungere una nuova compilazione][10]

* Selezionare un'attività di compilazione

![Aggiungere un'attività di compilazione][11]

![Selezionare il modello di attività di compilazione di Visual Studio][12]

* Modificare l'input dell'attività di compilazione. Personalizzare compilazione hello parametri in base tooyour

![Configurare l'attività di compilazione][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Configurare le variabili di compilazione

![Configurare le variabili di compilazione][14]

* Aggiungere una destinazione della compilazione tooupload di attività

![Scegliere l'attività di pubblicazione della destinazione finale della compilazione][15]

![Configurare l'attività di pubblicazione della destinazione finale della compilazione][16]

* Eseguire la compilazione hello

![Accodare la nuova compilazione][17]

![Visualizzare il riepilogo della compilazione][18]

* Se hello compilazione viene completata correttamente verrà visualizzato un toobelow simile risultato

![Risultato della compilazione][19]

### <a name="4----configure-release-process"></a>4.    Configurare il processo di rilascio
* Creare una nuova versione

![Creare una nuova versione][20]

* Selezionare l'attività di distribuzione di servizi Cloud di Azure hello

![Selezionare l'attività di distribuzione dei Servizi cloud di Azure][21]

* Come chiave dell'account di archiviazione hello non è selezionata nel controllo toosource, una chiave privata toospecify hello è necessario per l'impostazione delle estensioni di diagnostica. Espandere hello **opzioni avanzate per la creazione di un nuovo servizio** sezione e modificare hello **chiavi dell'Account di archiviazione diagnostica** input del parametro. Accetta l'input in più righe di una coppia chiave-valore nel formato hello **[RoleName]:$(StorageAccountKey)**

> Nota: se i dati di diagnostica in account di archiviazione hello stessa sottoscrizione in cui verrà pubblicata l'applicazione di servizi Cloud hello, non si dispone tooenter hello chiave nell'input di attività di distribuzione hello; distribuzione Hello a livello di codice ottiene informazioni sull'archiviazione hello dalla sottoscrizione
> 
> 

![Configurare l'attività di distribuzione dei Servizi cloud di Azure][22]

* Segreto utilizzare compilazione variabili toosave chiavi per l'archiviazione. una variabile come segreto fare clic sull'icona di blocco hello sul lato destro hello di hello toomask variabili di input

![Salvare le chiavi di archiviazione nelle variabili di compilazione del segreto][23]

* Creare una versione e distribuire il progetto tooAzure

![Creare una nuova versione][24]

## <a name="next-steps"></a>Passaggi successivi
toolearn più sull'impostazione di estensioni di diagnostica per i servizi Cloud di Azure, vedere [abilitare la diagnostica nei servizi Cloud di Azure tramite PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
