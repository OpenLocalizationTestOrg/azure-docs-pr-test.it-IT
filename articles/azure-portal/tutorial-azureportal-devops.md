---
title: 'Esercitazione: DevOps con hello portale di Azure | Documenti Microsoft'
description: Informazioni su hello vari flussi di lavoro di DevOps in hello portale di Azure.
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>Esercitazione: DevOps con hello portale di Azure
piattaforma Azure Hello è piena di flussi di lavoro DevOps flessibile. In questa esercitazione illustrato come funzionalità hello tooleverage di hello Azure Portal toodevelop, testare, distribuire, risolvere i problemi, monitorare e gestire applicazioni in esecuzione. In questa esercitazione è incentrata sulla seguente hello:

1. Creazione di un'app Web e abilitazione della distribuzione continua
2. Sviluppare e testare un'app
3. Monitoraggio e risoluzione dei problemi di un'app
4. Attività di gestione di applicazioni generali

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>Creazione di un'app Web e abilitazione della distribuzione continua
Creare un'app Web con [Azure App Service](https://azure.microsoft.com/services/app-service/), che verranno usati nel resto di hello dell'esercitazione. All'inizio si abiliterà la distribuzione continua dal repository di codice sorgente all'ambiente di Azure in esecuzione.

1. Accedere al portale di Azure hello
2. Scegliere **servizi App** &gt; **sull'icona Aggiungi** e immettere un nome, scegliere la sottoscrizione e creare un nuovo tooserve gruppo di risorse come contenitore hello per servizio hello.
   
   Gruppi di risorse consentono di toomanage vari aspetti della soluzione di hello, ad esempio fatturazione, distribuzioni e il monitoraggio come un singolo gruppo tramite [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
   
   ![Immagine1][image1]
3. Dopo pochi secondi, verrà creato il servizio app. Richiedere hello di tooexplore pochi minuti diverse opzioni di menu per il servizio hello nel portale di hello.
   
   ![Immagine2][image2]    
4. Fare clic su URL hello. Si noti diversi hello scelte disponibili per gli strumenti e repository. È inoltre possibile utilizzare linguaggi hello e altri framework di propria scelta, tra cui .NET, Java e Ruby.
   
   ![Immagine3][image3]    
5. Hello portale di Azure effettua la distribuzione continua di un processo semplice che include solo pochi semplici passaggi. Nel portale di Azure hello, scegliere impostazioni dall'icona hello per il servizio app di hello che appena creato.
   
   ![Immagine4][image4]
   
   Dal pannello hello che verrà visualizzato a destra di hello, scorrere toohello la pubblicazione di sezione.
   
   ![Immagine5][image5]
6. A questo punto, configurare alcune impostazioni tooenable la distribuzione continua per app hello. Fare clic su Origine distribuzione e quindi su Scegliere l'origine. Si noti diversi hello opzioni che disponibili per le origini dei repository.
   
   ![Immagine6][image6]
7. Per questo esempio scegliere GitHub. Facoltativamente, scegliere repository hello scelto dall'utente e credenziali di autorizzazione hello del programma di installazione.
   
   ![Immagine7][image7]
8. Dopo aver repository tooyour di autorizzazione, è possibile scegliere un progetto e il ramo desiderato toodeploy. Sotto sono elencati diversi esempi fittizi.
   
   ![Immagine8][image8]
9. Dopo avere scelto il progetto e il ramo, fare clic su OK. È consigliabile iniziare toosee notifiche di una distribuzione.
   
   ![Immagine9][image9]
10. Spostarsi indietro tooGitHub toosee hello webhook che è stato creato un repository di controllo origine hello toointegrate con Azure. Hello portale di Azure consente l'integrazione con GitHub con solo pochi semplici passaggi.
    
    ![Immagine10][image10]
11. toodemonstrate la distribuzione continua, si aggiungere rapidamente alcuni repository toohello contenuto. Per un esempio semplice, aggiungere un repository GitHub di tooa file di testo di esempio. Si è gratuita toouse .NET, Ruby, Python o un altro tipo di applicazione con il servizio App. Ritiene tooadd disponibile un file di testo, repository di toohello applicazione MVC ASP.NET, Java o Ruby di propria scelta.
    
    ![Immagine11][image11]
12. Dopo il commit del repository tooyour modifiche, viene visualizzato un nuovo avviare la distribuzione nell'area di notifica del portale hello. Se non visualizzare rapidamente le modifiche apportate dopo il commit tooyour repository, fare clic su Sincronizza.
    
    ![Immagine12][image12]
13. A questo punto, se si tenta di carica la pagina hello per il servizio app di hello, si potrebbe ricevere un errore 403. In questo esempio, è perché non prevede alcuna installazione documento predefinita tipica per la pagina di hello, ad esempio un file htm o default. È possibile risolvere questo problema rapidamente con gli strumenti nel portale di Azure hello hello.  Nel portale di Azure hello scegliere impostazioni &gt; le impostazioni dell'applicazione.
    
     ![Immagine13][image13]
14. Viene aperto un pannello per le impostazioni dell'applicazione. Immettere il nome di hello della pagina di hello "SamplePage.html" e fare clic su Salva. Richiedere altre impostazioni di hello di tooexplore pochi minuti.
    
    ![Immagine14][image14]
15. Facoltativamente, aggiornare il tooensure URL browser vedrai modifiche hello previsto. In questo caso, è ora la compilazione di pagina hello testo semplice. Ogni repository toohello ulteriore modifica comporta una nuova distribuzione automatica.
    
    ![Immagine15][image15]
    
    Consente la distribuzione continua con hello portale di Azure è un'esperienza semplice. È anche possibile compilare pipeline di rilascio più complesse e utilizzare numerose altre tecniche di controllo del codice sorgente esistente e tooAzure toodeploy sistemi di integrazione continua, come l'uso di compilazione automatizzato e i sistemi di gestione di versione.

## <a name="develop-and-test-an-app"></a>Sviluppare e testare un'app
Successivamente, rendere il codice toohello alcune modifiche di base e distribuire rapidamente le modifiche. Installerà anche backup di alcuni test delle prestazioni per app Web hello.

1. Nel portale di Azure hello scegliere Servizi App dal riquadro di spostamento hello e individuare il servizio App.
   
   ![Immagine16][image16]
2. Fare clic su Strumenti.
   
   ![Immagine17][image17]
3. Si noti hello categoria in strumenti di sviluppo. Sono disponibili diversi strumenti utili qui che consentono di toowork con App senza uscire hello portale di Azure. Fare clic su Console.
   
   ![Immagine18][image18]
4. Nella finestra di console hello, è possibile eseguire comandi in tempo reale per l'app. Tipo hello dir comando e premere INVIO. Si noti che i comandi che richiedono privilegi elevati non funzionano.
   
   ![Immagine19][image19]
5. Spostare nuovamente toohello sviluppare categoria e scegliere Visual Studio Online. Nota: Visual Studio Online si chiama ora Visual Studio Team Services.
   
   ![Immagine20][image20]
6. Attivare l'esperienza di modifica nel browser hello per l'App.
   
   ![Immagine21][image21]
7. Viene installata un'estensione Web per l'app. Estensioni di aggiungono rapidamente e facilmente funzionalità tooapps in Azure. Si noti alcuni hello altri tipi di estensione disponibili nella schermata di hello riportata di seguito.
   
   ![Immagine22][image22]
8. Una volta installato hello estensione Visual Studio Online, fare clic su Vai.
   
   ![Immagine23][image23]
9. Verrà visualizzata la in cui si vedere sviluppo IDE direttamente nel browser hello di scheda di un browser. Esperienza di hello avviso riportato di seguito è in Chrome.
   
   ![Immagine24][image24]
10. È possibile eseguire diverse attività, ad esempio i file di modifica, aggiungere file e cartelle e scaricare contenuto dal sito in tempo reale di hello. Apporta una modifica rapida toohello SamplePage.html al file.
    
    ![Immagine25][image25]
11. Tra qualche minuto, hello modifiche vengono salvate automaticamente. Se si passa indietro toohello pagina, è possibile visualizzare le modifiche di hello. Tenere presente che modifiche di questo tipo non sono per lo più adatte agli ambienti di produzione. Tuttavia, gli strumenti di hello rendono toomake molto facilmente modifiche rapide per lo sviluppo e ambienti di test.
    
    ![Immagine26][image26]
    
    ![Immagine27][image27]
12. Spostare nuovamente pannello Strumenti toohello e nella categoria di sviluppare hello, fare clic sul Test delle prestazioni.
    
    ![Immagine28][image28]
13. È necessario un account di team services tooset. Per altri dettagli, vedere [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
14. Fare clic su Nuovo toocreate un test delle prestazioni.
    
    ![Immagine29][image29]
    
    Configurare hello diversi valori e fare clic su Esegui Test nella parte inferiore di hello della finestra di dialogo di hello tooinitiate un test delle prestazioni.
    
    ![Immagine30][image30]
    
    ![Immagine31][image31]
15. Una volta test hello viene avviata l'esecuzione, è possibile monitorare lo stato di hello.
    
    ![Immagine32][image32]
    
    Al termine del test di hello, facendo clic sul risultato di hello Mostra ulteriori dettagli.
    
    ![Immagine33][image33]
16. In questo esempio è stato creato un piccolo esecuzione dei test, pertanto è tooanalyze limitata dei dati, ma è possibile vedere diverse metriche, nonché eseguire nuovamente il test da questa visualizzazione. Hello portale di Azure semplifica la creazione, l'esecuzione e l'analisi di un processo semplice test delle prestazioni web. Hello schermate riportate di seguito visualizza i dati sulle prestazioni hello.
    
    ![Immagine34][image34]
    
    ![Immagine35][image35]
    
    ![Immagine36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>Monitoraggio e risoluzione dei problemi di un'app
Azure offre diverse funzionalità per il monitoraggio e la risoluzione dei problemi delle applicazioni in esecuzione.

1. Scegliere gli strumenti di hello portale di Azure per l'app Web.
   
   ![Immagine37][image37]
2. Nella categoria di risoluzione dei problemi di hello, si noti hello varie opzioni per l'utilizzo di potenziali problemi di strumenti tootroubleshoot con un'app in esecuzione. È possibile, ad esempio, monitorare il traffico HTTP in tempo reale, abilitare la riparazione automatica, visualizzare log e altro ancora.
   
   ![Immagine38][image38]
3. Scegliere le metriche del sito tooquickly get di una visualizzazione di alcuni codici HTTP.
   
   ![Immagine39][image39]
4. Scegliere Diagnostica distribuita come servizio. Scegliere il tipo di applicazione, quindi scegliere Esegui.
   
   ![Immagine40][image40]
   
   Inizia una raccolta.
   
   ![Immagine41][image41]
5. È possibile scegliere i potenziali problemi di hello log appropriato toodiagnose. È necessario tooenable registrazione toosee tutti i dati disponibili hello opzioni, ad esempio log HTTP.
   
   ![Immagine42][image42]
   
   Facendo clic sul file di Dump di memoria hello è possibile scaricare e analizzare un DebugDiag toohelp report di analisi trovare problemi potenziali.
   
   ![Immagine43][image43]
6. tooview più dati, è necessario tooenable ulteriori opzioni di registrazione. Nel portale di Azure hello, passare toohello Web app e scegliere le impostazioni.
   
   ![Immagine44][image44]
7. Scorrere verso il basso categoria funzionalità toohello e scegliere i log di diagnostica.
   
      ![Immagine45][image45]
8. Si noti hello varie opzioni per la registrazione. Attivare Registrazione server Web e fare clic su Salva.
   
   ![Immagine46][image46]
9. Spostare nuovamente toohello area di strumenti per app hello e scegliere diagnostica come servizio e fare clic su Esegui toorerun hello raccolta dei dati.
   
   ![Immagine47][image47]
10. Impostazione registrazione hello HTTP è abilitata, è ora possibile visualizzare i dati raccolti per i log di HTTP.
    
    ![Immagine48][image48]
11. Facendo clic sul file di log hello HTML, si produce un report di basate su browser completo per un'analisi più approfondita.
    
    ![Immagine49][image49]
12. Consente di tornare sezione Strumenti toohello hello portale di Azure per app hello. Scorrere sezione Strumenti toohello e scegliere Process Explorer.
    
    ![Immagine50][image50]
13. Scegliendo Esplora processi, è possibile visualizzare i dettagli sui processi in esecuzione. Di seguito è possibile analizza i processi e anche terminare i processi di tutti gli elementi dal portale di Azure hello.
    
    ![Immagine51][image51]
    
    ![Immagine52][image52]
14. Spostarsi all'indietro pannello impostazioni toohello di hello sinistra. Fare clic su Nuova richiesta di supporto.
    
    ![Immagine53][image53]
15. Dal pannello hello in hello destra, può inserire le informazioni sui problemi di hello, immettere le informazioni di contatto e caricare anche dati di diagnostica. Hello portale di Azure consente l'utilizzo di un'esperienza di supporto tecnico Microsoft.
    
    ![Immagine54][image54]
    
    ![Immagine55][image55]
    
    Hello portale di Azure consente di fornire potente e familiare tooling esperienze toohelp monitoraggio e risoluzione dei problemi delle applicazioni in esecuzione. Sono anche tootake in grado di azione rapidamente mediante l'esecuzione di attività, ad esempio riciclo dei processi, l'abilitazione e disabilitazione di varie raccolte di dati e anche l'integrazione con supporto tecnico Microsoft.

## <a name="general-application-management"></a>Gestione di applicazioni generale
Quando la gestione delle applicazioni, è spesso necessario tooperform una vasta gamma di attività quali la configurazione di strategie di backup, l'implementazione e gestione dei provider di identità e la configurazione di controllo di accesso basato sui ruoli. Come con hello altre esperienze DevOps, hello piattaforma Azure integra queste operazioni direttamente nel portale hello.

1. viene sincronizzato tooensure hello App Web protetta da perdita di dati è necessario tooconfigure backup. Passare toohello area di impostazioni per l'app Web.
   
   ![Immagine56][image56]
2. Nel Pannello di hello in hello destro, scorrere verso il basso toohello categoria di funzionalità.
   
    ![Immagine57][image57]
3. Scegliere di backup. a destra hello verrà visualizzato un pannello.
   
   ![Immagine58][image58]
4. Fare clic su Configura, scegliere un account di archiviazione dal pannello hello in hello destra.
   
   ![Immagine59][image59]
5. A questo punto, creare e scegliere un toohold contenitore di archiviazione dei backup. Fare clic su Crea nella parte inferiore di hello del pannello hello. Selezionare quindi il contenitore di hello.
   
   ![Immagine60][image60]
6. Una volta scelto il contenitore di hello, è possibile configurare le pianificazioni, nonché i backup di programma di installazione per i database. Per questo scenario, fare clic su hello Salva icona.
   
    ![Immagine61][image61]
7. Dopo il salvataggio, scorrere indietro toohello pannello a sinistra di hello per i backup. Fare clic su Esegui Backup ora un'applicazione hello tooback.
   
    ![Immagine62][image62]
8. Dopo alcuni istanti, viene creato un backup. Hello avviso Ripristina ora opzione hello cattura di schermata seguente.
   
    ![Immagine63][image63]
9. Fare clic su Ripristina ora ed esaminare pannello toohello opzioni di hello in hello destra. È possibile scegliere che un backup appropriati e facilmente tooan ripristino precedente lo stato in base alle esigenze. portale di Azure Hello ci ha consentito di abilitare facilmente una strategia di ripristino di emergenza semplice per l'applicazione hello.
   
    ![Immagine64][image64]
10. Spostare nuovamente pannello impostazioni toohello a sinistra di hello e in funzioni e scegliere l'autenticazione/autorizzazione.
    
     ![Immagine65][image65]
11. Nel pannello hello in hello destra scegliere l'autenticazione del servizio App. Si noti diverse hello opzioni che è possibile configurare con i provider più diffusi.
    
     ![Immagine66][image66]
12. Scegliere provider hello di propria scelta e notare le opzioni di hello per ambito hello. È possibile fornire un ID dell'App e il segreto dell'applicazione e abilitare rapidamente autenticazione Facebook per l'applicazione hello. Portale di Azure Hello Abilita l'autenticazione come una soluzione completa per le app.
    
     ![Immagine67][image67]
13. Spostare nuovamente pannello impostazioni toohello e selezionare gli utenti nella categoria Gestione delle risorse hello.
    
     ![Immagine68][image68]
14. Nel pannello hello in hello destro esaminare hello varie opzioni per l'aggiunta di ruoli e utenti. Hello portale di Azure consente di controllare facilmente RBAC (controllo di accesso basato sui ruoli) per un'applicazione hello.
    
     ![Immagine69][image69]

## <a name="summary"></a>Riepilogo
In questa esercitazione illustrati alcuni dei power hello con hello piattaforma Azure rapidamente consente la distribuzione continua per un'app web, l'esecuzione vari di sviluppo e le attività di test, il monitoraggio e risoluzione dei problemi di un'applicazione in tempo reale e infine Gestione chiave strategie, ad esempio il ripristino di emergenza, l'identità e controllo di accesso basato sui ruoli. Hello piattaforma Azure consente un'esperienza integrata per i flussi di lavoro di DevOps e possono lavorare in modo efficiente, rimanendo nel contesto per l'attività hello in questione.

## <a name="next-steps"></a>Passaggi successivi
* Gestione risorse di Azure è importante per l'abilitazione di DevOps su hello piattaforma Azure.  visitare più toolearn [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).
* informazioni sulla distribuzione di servizio App di Azure, visitare toolearn [distribuire il servizio App di tooAzure app](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
