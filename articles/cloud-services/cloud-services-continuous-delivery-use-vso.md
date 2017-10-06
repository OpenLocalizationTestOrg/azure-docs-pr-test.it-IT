---
title: recapito aaaContinuous con Visual Studio Team Services in Azure | Documenti Microsoft
description: "Informazioni su come tooconfigure il Visual Studio Team Services i progetti team tooautomatically compilare e distribuire toohello funzionalità App Web di servizi cloud o di servizio App di Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>TooAzure il recapito continuo con Visual Studio Team Services
È possibile configurare la compilazione di Visual Studio Team Services team progetti tooautomatically e distribuire le app web tooAzure o servizi cloud.  (Per informazioni su come tooset fino a una compilazione continua e distribuzione del sistema utilizzando un *locale* Team Foundation Server, vedere [il recapito continuo per servizi Cloud in Azure](cloud-services-dotnet-continuous-delivery.md).)

In questa esercitazione si presuppone di Visual Studio 2013 e Azure SDK installata hello. Se si dispone già di Visual Studio 2013, scaricarlo scegliendo hello **possibile iniziare gratuitamente** collegamento [www.visualstudio.com](http://www.visualstudio.com). Installazione hello Azure SDK da [qui](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> È necessario un toocomplete di account di Visual Studio Team Services in questa esercitazione: È possibile [aprire un account di Visual Studio Team Services gratuito](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset backup un tooautomatically servizio cloud compilare e distribuire tooAzure utilizzando Visual Studio Team Services, seguire questi passaggi.

## <a name="1-create-a-team-project"></a>1: Creare un progetto team
Seguire le istruzioni di hello [qui](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate il team di progetto e crea un collegamento tooVisual Studio. In questa procedura dettagliata si presume che si usi Controllo della versione di Team Foundation (TFVC) come soluzione di controllo del codice sorgente. Se si desidera toouse Git per il controllo della versione, vedere [versione Git hello di questa procedura dettagliata](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-toosource-control"></a>2: controllare in un controllo toosource progetto
1. In Visual Studio, aprire Esplora hello toodeploy desiderato oppure crearne uno nuovo.
   È possibile distribuire un'app web o un servizio cloud (applicazione di Azure) da hello seguente passaggi in questa procedura dettagliata.
   Se si desidera toocreate una nuova soluzione, creare un nuovo progetto di servizio Cloud di Azure o un nuovo progetto ASP.NET MVC. Assicurarsi che hello progetto è destinato a .NET Framework 4 o 4.5 e se si sta creando un progetto di servizio cloud, aggiungere un ruolo web ASP.NET MVC e un ruolo di lavoro e scegliere l'applicazione Internet per il ruolo web hello. Quando richiesto, scegliere **Applicazione Internet**.
   Se si desidera toocreate un'app web, scegliere il modello di progetto applicazione Web ASP.NET di hello, quindi MVC. Vedere [Creare un'app Web ASP.NET in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > Al momento, Visual Studio Team Services supporta solo le distribuzioni CI di applicazioni Web di Visual Studio. I progetti di sito Web sono esterni all'ambito.
   > 
   > 
2. Aprire hello menu di scelta rapida Esplora hello e scegliere **tooSource Aggiungi soluzione controllo**.
   
    ![][5]
3. Accettare o modificare le impostazioni predefinite di hello e scegliere hello **OK** pulsante. Al termine del processo di hello, vengono visualizzate le icone di controllo di origine **Esplora**.
   
    ![][6]
4. Aprire il menu di scelta rapida hello per soluzione hello e scegliere **Archivia**.
   
    ![][7]
5. In hello **modifiche in sospeso** area di **Team Explorer**, digitare un commento per l'archiviazione hello e scegliere hello **Archivia** pulsante.
   
    ![][8]
   
    Si noti hello opzioni tooinclude o escludere modifiche specifiche quando si archivia. Se si desidera sono escluse le modifiche, scegliere hello **Includi tutto** collegamento.
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3: connettere hello progetto tooAzure
1. Dopo avere creato un progetto team di Visual Studio Team Services con un codice di origine in essa contenuti, si è pronti tooconnect tooAzure del progetto team.  In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), selezionare l'applicazione web o servizio cloud o crearne uno nuovo scegliendo hello  **+**  icona in basso a sinistra di hello e scegliendo **servizio Cloud** o **App Web** e quindi **creazione rapida**. Scegliere hello **impostare la pubblicazione con Visual Studio Team Services** collegamento.
   
    ![][10]
2. Nella procedura guidata hello, digitare il nome di hello dell'account di Visual Studio Team Services nella casella di testo hello e fare clic su hello **autorizzare ora** collegamento. Potrebbe essere necessario toosign in.
   
    ![][11]
3. In hello **richiesta di connessione** finestra di dialogo popup scegliere hello **Accept** pulsante tooauthorize tooconfigure Azure il progetto team in Visual Studio Team Services.
   
    ![][12]
4. Dopo aver concesso l'autorizzazione verrà visualizzato un elenco a discesa contenente un elenco dei progetti team di Visual Studio Team Services. Scegliere il nome di hello del progetto team creato nei passaggi precedenti hello e quindi sul pulsante della procedura guidata di hello segno di spunta.
   
    ![][13]
5. Dopo che il progetto è collegato, verrà visualizzato alcune istruzioni per l'archiviazione del progetto team di Visual Studio Team Services tooyour le modifiche.  Il successivo check-in, Visual Studio Team Services verrà compilato e distribuito tooAzure il progetto.  Provare a questo punto, fare clic su hello **Check-In da Visual Studio** il collegamento e quindi hello **avviare Visual Studio** collegamento (o equivalente hello **Visual Studio** pulsante nella parte inferiore di hello del portale schermata Ciao).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: Attivare una ricompilazione e ridistribuire il progetto
1. In Visual Studio **Team Explorer**, scegliere hello **Esplora controllo codice sorgente** collegamento.
   
    ![][15]
2. Selezionare il file di soluzione tooyour e aprirlo.
   
    ![][16]
3. In **Esplora soluzioni**aprire un file e modificarlo. Ad esempio, modificare il file hello `_Layout.cshtml` in visualizzazioni hello\\cartella condivisa in un ruolo web MVC.
   
    ![][17]
4. Modificare il logo hello per il sito hello e scegliere **Ctrl + S** file hello toosave.
   
    ![][18]
5. In **Team Explorer**, scegliere hello **modifiche in sospeso** collegamento.
   
    ![][19]
6. Immettere un commento e quindi scegliere hello **Archivia** pulsante.
   
    ![][20]
7. Scegliere hello **Home** pulsante tooreturn toohello **Team Explorer** pagina iniziale.
   
    ![][21]
8. Scegliere hello **compilazioni** hello tooview collegamento compilazioni in corso.
   
    ![][22]
   
    **Team Explorer** mostra che è stata attivata una compilazione per l'archiviazione.
   
    ![][23]
9. Fare doppio clic sul nome hello di compilazione hello in corso tooview un log dettagliato come compilazione hello.
   
    ![][24]
10. Durante la compilazione hello è in corso, esaminare una definizione di compilazione hello creata quando è stato collegato tooAzure TFS utilizzando la procedura guidata hello.  Aprire il menu di scelta rapida hello hello la definizione di compilazione e scegliere **Modifica definizione di compilazione**.
    
     ![][25]
    
     In hello **Trigger** scheda, si noterà che la definizione di compilazione hello è toobuild attivata ogni check-in per impostazione predefinita.
    
     ![][26]
    
     In hello **processo** scheda, è possibile vedere ambiente di distribuzione hello è impostato toohello nome dell'app web o servizio cloud. Se si lavora con le app web, proprietà hello che viene visualizzato è diversa da quelle indicate qui.
    
     ![][27]
11. Se si desiderano valori diversi da quelli predefiniti hello, specificare i valori per le proprietà di hello. salve le proprietà per la pubblicazione di Azure sono in hello **distribuzione** sezione.
    
     Hello nella tabella seguente mostra le proprietà disponibili hello in hello **distribuzione** sezione:
    
    | Proprietà | Valore predefinito |
    | --- | --- |
    | Consenti certificati non attendibili |Se è false, i certificati SSL devono essere firmati da un'autorità radice. |
    | Consenti aggiornamento |Consente di hello distribuzione tooupdate una distribuzione esistente anziché crearne uno nuovo. Consente di mantenere l'indirizzo IP hello. |
    | Non eliminare |Se è true, una distribuzione non correlata esistente non viene sovrascritta (l'aggiornamento è consentito). |
    | Percorso tooDeployment impostazioni |Hello percorso tooyour pubxml file per un'app web, toohello relativo di cartella radice del repository hello. Viene ignorato per i servizi cloud. |
    | Ambiente di distribuzione SharePoint |nome del servizio hello, Hello stesso. |
    | Ambiente di distribuzione Azure |Hello app o cloud nome del servizio web. |
12. Se si utilizza più configurazioni del servizio (file con estensione cscfg), è possibile specificare la configurazione del servizio desiderato hello in hello **argomenti di compilazione, avanzate, MSBuild** impostazione. Ad esempio, toouse ServiceConfiguration.Test.cscfg, impostare gli argomenti MSBuild opzione della riga `/p:TargetProfile=Test`.
    
     ![][38]
    
     A questo punto la compilazione sarà stata completata correttamente.
    
     ![][28]
13. Se si fa doppio clic sul nome di compilazione hello, Visual Studio visualizza un **Riepilogo compilazione**, compresi i risultati dei test da associati progetti di unit test.
    
     ![][29]
14. In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), è possibile visualizzare la distribuzione di hello associata nella hello **distribuzioni** scheda quando viene selezionato l'ambiente di gestione temporanea hello.
    
     ![][30]
15. Individuare l'URL del sito tooyour. Per un'app web, fare clic hello **Sfoglia** pulsante sulla barra dei comandi di hello. Per un servizio cloud, scegliere URL hello in hello **Quick Glance** sezione di hello **Dashboard** pagina che mostra l'ambiente di gestione temporanea hello per un servizio cloud. Le distribuzioni di integrazione continua per i servizi cloud sono pubblicati toohello ambiente di gestione temporanea per impostazione predefinita. È possibile modificare questa impostazione hello **ambiente del servizio Cloud alternativo** proprietà troppo**produzione**. Questa schermata mostra dove hello che URL del sito è nella pagina dashboard del servizio cloud hello.
    
    ![][31]
    
    Una nuova scheda del browser verrà aperto tooreveal del sito in esecuzione.
    
    ![][32]
    
    Per i servizi cloud, se si apporta altre progetto tooyour le modifiche, si trigger più compila e si accumuleranno più distribuzioni. Hello più recente contrassegnato come attivo.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: Ridistribuire una compilazione precedente
Questo passaggio si applica toocloud services ed è facoltativo. Nel portale di Azure classico hello, scegliere una distribuzione precedente quindi hello **ridistribuire** pulsante toorewind il sito tooan precedentemente check-in.  Si noti che verrà attivata una nuova compilazione in TFS e verrà creata una nuova voce nella cronologia della distribuzione.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: modificare la distribuzione di produzione hello
Questo passaggio si applica solo toocloud services, non le applicazioni web. Quando si è pronti, è possibile alzare di livello hello gestione temporanea toohello ambiente di produzione scegliendo hello **scambiare** pulsante hello portale di Azure classico. ambiente di gestione temporanea appena distribuito Hello è tooProduction innalzate di livello e ambiente di produzione hello precedente, se presente, diventa un ambiente di gestione temporanea. distribuzione attiva Hello potrebbe essere diverso per ambienti di gestione temporanea e produzione hello, ma la cronologia della distribuzione hello di compilazioni recenti è hello uguali indipendentemente dal fatto che dell'ambiente.

![][35]

## <a name="7-run-unit-tests"></a>7: Eseguire unit test
Questo passaggio si applica solo le app tooweb, non i servizi cloud. tooput controllo di qualità, alla distribuzione, è possibile eseguire unit test e in caso di errore, è possibile arrestare la distribuzione di hello.

1. In Visual Studio aggiungere un progetto di unit test.
   
   ![][39]
2. Aggiungere riferimenti toohello progetto desiderato tootest.
   
   ![][40]
3. Aggiungere alcuni unit test. tooget avviato, provare a un test fittizio che passa sempre.
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. Modificare la definizione di compilazione hello, scegliere hello **processo** scheda ed espandere hello **Test** nodo.
5. Set hello **Errore compilazione se test** tooTrue. Ciò significa che la distribuzione di hello non verrà eseguita a meno che non hello test vengono superati.
   
   ![][41]
6. Inserire in coda una nuova compilazione.
   
   ![][42]
   
   ![][43]
7. Mentre è in corso la compilazione hello, controllare lo stato di avanzamento.
   
    ![][44]
   
    ![][45]
8. Quando viene eseguita la compilazione hello, controllare i risultati dei test hello.
   
    ![][46]
   
    ![][47]
9. Provare a creare un test che non verrà superato. Aggiungere un nuovo test copiando hello prima, rinominarlo e impostare come commento la riga hello del codice che indica il che NotImplementedException è un'eccezione prevista.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Il controllo in hello modifica tooqueue una nuova compilazione.
    
     ![][48]
11. Visualizzare hello test risultati toosee i dettagli sull'errore hello.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'esecuzione di test delle unità in Visual Studio Team Services, vedere [Eseguire test delle unità nella compilazione](http://go.microsoft.com/fwlink/p/?LinkId=510474). Se si usa Git, vedere [condividere il codice in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) e [tooAzure distribuzione continua servizio App](../app-service-web/app-service-continuous-deployment.md).  Per altre informazioni su Visual Studio Team Services, vedere [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
