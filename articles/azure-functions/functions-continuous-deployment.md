---
title: distribuzione aaaContinuous per le funzioni di Azure | Documenti Microsoft
description: "Utilizzare le funzionalità di distribuzione continua del servizio App di Azure toopublish delle funzioni di Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a>Distribuzione continua per Funzioni di Azure
Funzioni di Azure rende facile toodeploy app funzione mediante l'integrazione continua di servizio App. Le funzioni si integrano con Dropbox, GitHub, BitBucket e Visual Studio Team Services, VSTS. In questo modo un flusso di lavoro in cui il codice di funzione viene aggiornato utilizzando uno di questi tooAzure di distribuzione di servizi integrati trigger. Nel caso di nuove funzioni tooAzure, iniziare con [panoramica delle funzioni di Azure](functions-overview.md).

La distribuzione continua è un'ottima opzione per i progetti in cui vengono integrati contributi numerosi e frequenti. Consente anche di mantenere il controllo dell'origine del codice funzione. Hello seguenti origini di distribuzione è attualmente supportata:

* [Bitbucket](https://bitbucket.org/)
* [Dropbox](https://www.dropbox.com/)
* Archivio esterno (Git o Mercurial)
* [Archivio locale GIT](../app-service-web/app-service-deploy-local-git.md)
* [GitHub](https://github.com)
* [OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

Le distribuzioni sono configurate in base alla singola app per le funzioni. Dopo aver abilitata la distribuzione continua, l'accesso di codice toofunction nel portale di hello è impostato troppo*sola lettura*.

## <a name="continuous-deployment-requirements"></a>Requisiti per la distribuzione continua

È necessario disporre dell'origine di distribuzione configurati e il codice funzioni nell'origine distribuzione hello prima di impostare la distribuzione continua. In una distribuzione di app di funzione specificata, ogni funzione si trova in una sottodirectory denominata, dove il nome di directory hello è il nome di hello della funzione hello.  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>Configurare la distribuzione continua
Utilizzare questa distribuzione continua tooconfigure di procedure per un'app di funzione esistente. Questa procedura illustra l'integrazione con un archivio di GitHub. Una procedura analoga si applica a Visual Studio Team Services o ad altri servizi di distribuzione.

1. Nell'app di funzione in hello [portale di Azure](https://portal.azure.com), fare clic su **funzionalità della piattaforma** e **opzioni di distribuzione**. 
   
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Quindi in hello **distribuzioni** fare clic su pannello **installazione**.
 
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. In hello **origine distribuzione** pannello, fare clic su **origine scegliere**, quindi immettere le informazioni di hello per l'origine di distribuzione scelto e fare clic su **OK**.
   
    ![Scegliere l'origine della distribuzione](./media/functions-continuous-deployment/choose-deployment-source.png)

Dopo aver configurata la distribuzione continua, tutte le modifiche ai file dell'origine di distribuzione vengono copiati toohello app di funzione e viene attivata una distribuzione completa del sito. sito Hello viene ridistribuito quando vengono aggiornati i file di origine hello.

## <a name="deployment-options"></a>Opzioni di distribuzione

di seguito Hello sono alcuni scenari di distribuzione tipiche:

- [Creare una distribuzione di staging](#staging)
- [Spostare una distribuzione esistente toocontinuous di funzioni](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>Creare una distribuzione di staging

Le app per le funzioni non supportano ancora slot di distribuzione. È comunque possibile gestire distribuzioni di staging e di produzione separate tramite l'integrazione continua.

processo tooconfigure Hello e di lavoro con una distribuzione di gestione temporanea è in genere simile al seguente:

1. Creare due applicazioni di funzione nella sottoscrizione, uno per il codice di produzione hello e uno per la gestione temporanea. 

2. Creare un'origine della distribuzione, se non è già presente. Questo esempio usa [GitHub].

3. Per l'app di funzione di produzione, hello completo precedente i passaggi **impostare la distribuzione continua** e set hello distribuzione ramo toohello ramo master del repository di GitHub.
   
    ![Scegliere il ramo della distribuzione](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. Ripetere questo passaggio per hello app di funzione di gestione temporanea, ma scegliere hello gestione temporanea invece di ramo nel repository di GitHub. Se l'origine della distribuzione non supporta le diramazioni, usare una cartella diversa.
    
5. Apportare aggiornamenti tooyour codice hello ramo o una cartella di gestione temporanea, quindi verificare che tali modifiche si rifletteranno in hello distribuzione di gestione temporanea.

6. Al termine del test, unire le modifiche dal ramo di gestione temporanea nel ramo master hello hello. Questo tipo di merge Attiva distribuzione toohello produzione funzione app. Se l'origine di distribuzione non supporta i rami, sovrascrivere i file nella cartella di produzione hello hello con file hello hello cartella di gestione temporanea.

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a>Spostare una distribuzione esistente toocontinuous di funzioni
Quando si dispongono di funzioni esistenti creati e gestiti nel portale di hello, è necessario toodownload esistente funzione tramite FTP o hello repository Git locale prima di impostare la distribuzione continua come descritto in precedenza i file di codice. È possibile farlo in hello le impostazioni di servizio App per l'app di funzione. Dopo che vengono scaricati i file, è possibile caricare le origine distribuzione continua tooyour scelto.

> [!NOTE]
> Dopo aver configurato l'integrazione continua, non sarà non è più in grado di tooedit l'origine dei file nel portale le funzioni hello.

- [Procedura: Configurare le credenziali di distribuzione](#credentials)
- [Procedura: Scaricare i file con FTP](#downftp)
- [Procedura: scaricare file utilizzando l'archivio Git locale hello](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>Procedura: Configurare le credenziali di distribuzione
Prima di poter scaricare i file dall'app di funzione con FTP o nell'archivio Git locale, è necessario configurare il sito di hello tooaccess credenziali. Le credenziali vengono impostate a livello di app di funzione hello. Utilizzare hello seguenti passaggi viene tooset le credenziali di distribuzione nel portale di Azure hello:

1. Nell'app di funzione in hello [portale di Azure](https://portal.azure.com), fare clic su **funzionalità della piattaforma** e **le credenziali di distribuzione**.
   
    ![Impostare le credenziali di distribuzione locali](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. Immettere un nome utente e una password, quindi fare clic su **Salva**. Ora è possibile utilizzare questi tooaccess credenziali app funzione dal repository Git predefinito hello o FTP.

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>Procedura: Scaricare i file tramite FTP

1. Nell'app di funzione in hello [portale di Azure](https://portal.azure.com), fare clic su **funzionalità della piattaforma** e **proprietà**, quindi copiare i valori hello per **utente FTP/distribuzione**, **Nome Host FTP**, e **nome Host FTPS**.  

    **Utente FTP/distribuzione** deve essere immesso come visualizzato nel portale di hello, incluso il nome dell'applicazione hello, tooprovide contesto appropriato per il server FTP hello.
   
    ![Ottenere le informazioni di distribuzione](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. Dal client FTP, utilizzare le informazioni di connessione hello raccolte tooconnect tooyour app e scaricare i file di origine hello per le funzioni.

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a>Procedura: scaricare file tramite l'archivio GIT locale

1. Nell'app di funzione in hello [portale di Azure](https://portal.azure.com), fare clic su **funzionalità della piattaforma** e **opzioni di distribuzione**. 
   
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Quindi in hello **distribuzioni** fare clic su pannello **installazione**.
 
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. In hello **origine distribuzione** pannello, fare clic su **repository Git locale** e quindi fare clic su **OK**.

3. In **funzionalità della piattaforma**, fare clic su **proprietà** e annotare il valore di hello dell'URL di Git. 
   
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. Clonare il repository hello sul computer locale utilizzando un prompt dei comandi basato su Git o lo strumento preferito di Git. comando di Git clone Hello è simile al seguente:
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. Recuperare i file dal clone toohello app di funzione nel computer locale, come in hello di esempio seguente:
   
        git pull origin master
   
    Se richiesto inserire le [credenziali di distribuzione configurate](#credentials).  

[GitHub]: https://github.com/
