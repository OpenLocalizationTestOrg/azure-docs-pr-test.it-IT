---
title: ruoli aaaTroubleshoot che non soddisfano toostart | Documenti Microsoft
description: Ecco alcuni motivi comuni per cui un ruolo del servizio Cloud potrebbe non riuscire toostart. Sono inoltre disponibili soluzioni ai problemi di toothese.
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>Risolvere i problemi relativi a ruoli del servizio Cloud che non soddisfano toostart
Ecco alcuni problemi comuni e i ruoli di servizi Cloud correlati tooAzure soluzioni che non soddisfano toostart.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>File DLL o dipendenze mancanti
I problemi dovuti a ruoli che non rispondono e ruoli che passano in ciclo tra gli stati **Inizializzazione**, **Occupato** e **Arresto** possono essere provocati da file DLL o assembly mancanti.

I sintomi di file DLL o assembly mancati includono i seguenti:

* L'istanza del ruolo passa in ciclo tra gli stati **Inizializzazione**, **Occupato** e **Arresto**.
* L'istanza del ruolo è stato spostato troppo**pronto** ma se si passa l'applicazione web tooyour, non viene visualizzata la pagina di hello.

Sono disponibili diversi metodi consigliati per esaminare questi problemi.

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>Diagnosticare i problemi di DLL mancanti in un ruolo Web
Quando si passa tooa sito Web viene distribuito in un ruolo web e browser hello Visualizza server errore simili toohello di seguito, è possibile che una DLL è manca.

![Errore del server nell'applicazione '/'.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>Diagnosticare i problemi disabilitando gli errori personalizzati
Informazioni sugli errori più completi possono essere visualizzati mediante la configurazione Web. config hello per tooOff modalità hello web ruolo tooset hello errore personalizzato e ridistribuire il servizio di hello.

tooview completare più errori senza usare Desktop remoto:

1. Aprire la soluzione hello in Microsoft Visual Studio.
2. In hello **Esplora**, individuare il file Web. config hello e aprirlo.
3. Nel file Web. config hello, nella sezione System. Web hello e aggiungere hello seguente riga:

    ```xml
    <customErrors mode="Off" />
    ```
4. Salvare il file hello.
5. Ricreare il pacchetto e ridistribuire il servizio di hello.

Una volta che il servizio di hello viene ridistribuito, si verrà visualizzato un messaggio di errore con nome hello di hello mancante DLL o assembly.

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>Diagnosticare i problemi visualizzando errore hello in modalità remota
È possibile utilizzare Desktop remoto tooaccess hello ruolo e visualizzare informazioni sugli errori più completi in modalità remota. Utilizzare hello dopo errori di hello tooview passaggi tramite Desktop remoto:

1. Verificare che sia installato Azure SDK 1.3 o versione successiva.
2. Durante la distribuzione di hello della soluzione hello tramite Visual Studio, scegliere troppo "Configura connessioni Desktop remoto...". Per ulteriori informazioni sulla configurazione della connessione Desktop remoto hello, vedere [tramite Desktop remoto con i ruoli Azure](../vs-azure-tools-remote-desktop-roles.md).
3. In hello portale Microsoft Azure classico, una volta che viene visualizzato lo stato istanza hello **pronto**, fare clic su una delle istanze del ruolo hello.
4. Fare clic su hello **Connetti** icona in hello **accesso remoto** area della barra multifunzione hello.
5. Accedere utilizzando le credenziali specificate durante la configurazione di Desktop remoto hello hello macchina virtuale toohello.
6. Aprire una finestra di comando.
7. Digitare `IPconfig`.
8. Si noti il valore di indirizzo IPV4 hello.
9. Aprire Internet Explorer.
10. Digitare l'indirizzo hello e il nome di hello dell'applicazione web hello. ad esempio `http://<IPV4 Address>/default.aspx`.

Esplorazione toohello sito Web ora restituiscono i messaggi di errore più espliciti:

* Errore del server nell'applicazione '/'.
* Descrizione: Si è verificata un'eccezione non gestita durante l'esecuzione di hello della richiesta web corrente hello. Esaminare l'analisi dello stack per ulteriori informazioni sull'errore hello hello e dove proviene dal codice hello.
* Dettagli dell'eccezione: System.IO.FIleNotFoundException: Impossibile caricare il file o l'assembly 'Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35' o una delle relative dipendenze. Hello Impossibile trovare il file hello specificato.

ad esempio:

![Errore esplicito del server nell'applicazione '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>Diagnosticare i problemi usando l'emulatore di calcolo hello
È possibile utilizzare hello Microsoft Azure compute emulator toodiagnose e risolvere i problemi di dipendenze mancanti e gli errori di Web. config.

Per ottenere risultati ottimali con questo metodo di diagnosi, è consigliabile usare un computer o una macchina virtuale in cui è presente un'installazione pulita di Windows. toobest simulare hello ambiente Azure, utilizzare Windows Server 2008 R2 x64.

1. Installare una versione autonoma di hello di hello [Azure SDK](https://azure.microsoft.com/downloads/).
2. Nel computer di sviluppo hello, compilare il progetto di servizio cloud hello.
3. In Esplora risorse, passare toohello nella cartella bin\debug del progetto di servizio cloud di hello.
4. Copiare cartelle con estensione csx hello e computer di toohello file con estensione cscfg che si siano utilizzando problemi hello toodebug.
5. Nel computer pulito hello, aprire una finestra prompt dei comandi di Azure SDK e digitare `csrun.exe /devstore:start`.
6. Al prompt dei comandi di hello, digitare `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.
7. Quando viene avviato il ruolo di hello, si noterà informazioni dettagliate sull'errore in Internet Explorer. È inoltre possibile utilizzare gli strumenti di risoluzione dei problemi di Windows standard toofurther diagnosticare il problema di hello.

## <a name="diagnose-issues-by-using-intellitrace"></a>Diagnosticare i problemi usando IntelliTrace
Per i ruoli di lavoro e i ruoli Web che fanno uso di .NET Framework 4, è possibile usare [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), disponibile in Microsoft Visual Studio Enterprise.

Seguire questi servizio hello toodeploy di passaggi con IntelliTrace abilitato:

1. Verificare che sia installato Azure SDK 1.3 o versione successiva.
2. Distribuire la soluzione hello usando Visual Studio. Durante la distribuzione, controllare hello **Abilita IntelliTrace per ruoli .NET 4** casella di controllo.
3. Una volta avviata l'istanza di hello, aprire hello **Esplora Server**.
4. Espandere hello **Azure\\servizi Cloud** nodo e individuare hello distribuzione.
5. Espandere la distribuzione di hello fino a visualizzare le istanze del ruolo hello. Fare clic su una delle istanze di hello.
6. Scegliere **Visualizza log IntelliTrace**. Hello **Riepilogo IntelliTrace** verrà aperto.
7. Individuare la sezione relativa alle eccezioni hello di hello riepilogo. Se esistono eccezioni, sarà sezione hello **dati dell'eccezione**.
8. Espandere hello **dati dell'eccezione** e cercare **System.IO. FileNotFoundException** seguente toohello simili errori:

![Dati eccezione, assembly o file mancante](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>Risolvere DLL e assembly mancanti
tooaddress mancante errori DLL e assembly, seguire questi passaggi:

1. Aprire la soluzione hello in Visual Studio.
2. In **Esplora**aprire hello **riferimenti** cartella.
3. Fare clic su assembly hello identificato in errore hello.
4. In hello **proprietà** riquadro individuare **proprietà Copia localmente** e impostare il valore di hello troppo**True**.
5. Ridistribuire il servizio di cloud hello.

Dopo avere verificato che tutti gli errori sono stati corretti, è possibile distribuire il servizio di hello senza verificare hello **Abilita IntelliTrace per ruoli .NET 4** casella di controllo.

## <a name="next-steps"></a>Passaggi successivi
Altri [articoli sulla risoluzione dei problemi](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) per i servizi cloud.

toolearn come ruolo del servizio cloud tootroubleshoot problemi utilizzando i dati di diagnostica di Azure PaaS computer, vedere [serie di blog di Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
