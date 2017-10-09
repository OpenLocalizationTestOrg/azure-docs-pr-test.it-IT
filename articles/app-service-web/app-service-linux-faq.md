---
title: App del servizio Web App in domande frequenti su Linux aaaAzure | Documenti Microsoft
description: Domande frequenti su App Web del Servizio app di Azure su Linux.
keywords: Servizio app di Azure, app Web, domande frequenti, Linux, OSS
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a>Domande frequenti su App Web del Servizio app di Azure su Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Con la versione di hello dell'App Web in Linux, si sta lavorando aggiunta di funzionalità e apportando piattaforma tooour miglioramenti. Di seguito sono alcune domande frequenti (FAQ) che i clienti hanno richiesto ci su hello ultima mesi.
Se si dispone di una domanda, un commento per l'articolo hello ed è possibile rispondere appena possibile.

## <a name="built-in-images"></a>Immagini predefinite

**Q:** voglio toofork hello Docker contenitori predefiniti che hello piattaforma fornisce. Dove si trovano questi file?

**R:** È possibile trovare tutti i file Docker su [GitHub](https://github.com/azure-app-service). È possibile trovare tutti i contenitori Docker nell'[hub Docker](https://hub.docker.com/u/appsvc/).

**Q:** quali sono i valori previsti hello per hello sezione del File di avvio quando si configura stack di runtime hello?

**R:** per Node.Js, specificare il file di configurazione di hello PM2 o il file di script. Per .NET Core specificare il nome del file DLL compilato. Per Ruby, è possibile specificare hello Ruby script che si desidera tooinitialize dell'app con.

## <a name="management"></a>gestione

**Q:** cosa accade quando viene premuto il pulsante di riavvio hello nel portale di Azure hello?

**R:** questo è hello equivalente del riavvio di Docker.

**Q:** è possibile utilizzare Secure Shell (SSH) tooconnect toohello app contenitore macchina virtuale (VM)?

**R:** Sì, è possibile eseguire tramite il sito di Gestione controllo servizi hello, seguente hello controllo articolo per altre informazioni [supporto SSH per l'App Web in Linux](./app-service-linux-ssh-support.md)

**Q:** voglio toocreate un piano di Linux App Service tramite SDK o un modello ARM, come è possibile ottenere questo?

**R:** occorre hello tooset `reserved` campo di applicazione hello service troppo`true`.

## <a name="continuous-integrationdeployment"></a>Integrazione/distribuzione continua

**Q:** dell'applicazione web utilizza ancora un'immagine contenitore Docker precedente dopo che è già stato aggiornato immagine hello nell'Hub Docker. È supportata l'integrazione/distribuzione continua di contenitori personalizzati?

**R:** tooset integrazione/distribuzione continua per le immagini del Registro di sistema di Azure contenitore o DockerHub dal controllo hello articolo seguente [distribuzione continua con l'App Web di Azure in Linux](./app-service-linux-ci-cd.md). Per i registri privati, è possibile aggiornare il contenitore di hello arrestando e riavviando quindi l'app web. Oppure è possibile modificare o aggiungere un'applicazione fittizia impostazione tooforce un aggiornamento del contenitore.

**D:** Gli ambienti di gestione temporanea sono supportati?

**R:** Sì.

**Q:** è possibile utilizzare **distribuzione web** toodeploy dell'app web?

**R:** Sì, è necessario tooset un'app denominata `WEBSITE_WEBDEPLOY_USE_SCM` troppo`false`.

## <a name="language-support"></a>Supporto per le lingue

**D:** È presente il supporto per le app .NET Core non compilate?

**R:** Sì.

**R:** È previsto il supporto per lo strumento Composer come gestore delle dipendenze per le app PHP?

**R:** Sì. Durante una distribuzione Git, Kudu deve rilevare che si sta distribuendo un'applicazione PHP (grazie toohello presenza di un file composer.json) e verrà attivata un'installazione di creazione per l'utente.

## <a name="custom-containers"></a>Contenitori personalizzati

**D:** Uso un contenitore personalizzato. L'applicazione si trova in hello `\home\` directory, ma non è possibile trovare i file quando si naviga contenuto hello utilizzando hello [sito SCM](https://github.com/projectkudu/kudu) o un client FTP. Dove si trovano i file?

**R:** montaggio un toohello condivisione SMB `\home\` directory. In questo modo viene sostituito qualsiasi contenuto presente.

**D:** Uso un contenitore personalizzato. Non si desidera hello piattaforma toomount un toohello condivisione SMB `\home\`.

**R:** scopo è possibile che l'impostazione hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app impostazione troppo`false`.

**Q:** il contenitore personalizzato accetta un toostart molto tempo e contenitore di hello hello piattaforma riavvio prima che termina l'avvio.

**R:** è possibile configurare ora hello piattaforma hello attenderà prima di riavviare il contenitore. Questa operazione può essere eseguita dall'impostazione hello `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello impostazione app valore desiderato in secondi. valore predefinito di Hello è 230 secondi e hello max è 600 secondi.

**Q:** che cos'è il formato di hello per l'url del server del Registro di sistema privato?

**R:** occorre tooprovide hello del Registro di sistema completo url inclusi `http://` o `https://`.

**Q:** che cos'è il formato di hello per il nome dell'immagine hello nell'opzione del Registro di sistema privato?

**R:** occorre nome immagine completa di hello tooadd compresi url privato del Registro di sistema di hello (ad es. myacr.azurecr.io/dotnet:latest)

**Q:** desiderato tooexpose più di una porta in immagine contenitore personalizzato. È possibile?

**R:** Attualmente questa operazione non è supportata.

**D:** È possibile usare la propria archiviazione?

**R:** Attualmente questa operazione non è supportata.

**Q:** non è possibile accedere my del contenitore personalizzato file system o in esecuzione processi dal sito SCM hello. Perché?

**R:** sito SCM hello viene eseguito in un contenitore separato. Non è possibile controllare il sistema di file hello o in esecuzione processi di contenitore di app hello.

**Q:** il contenitore personalizzato è in ascolto porta tooa diversa dalla porta 80. Come è possibile configurare la porta toothat le richieste di app tooroute hello?

**R:** abbiamo il rilevamento automatico porta, è anche possibile specificare un'applicazione denominata **WEBSITES_PORT**e assegnare il valore di hello del numero di porta hello previsto. In precedenza si utilizzava piattaforma hello `PORT` app impostazione, si intende utilizzare hello toodeprecate questa impostazione di app e spostare toousing `WEBSITES_PORT` in modo esclusivo.

**Q:** necessario tooimplement HTTPS nel mio contenitore personalizzato.

**R:** No, piattaforma hello gestisce la terminazione HTTPS al server front-end hello condiviso.

## <a name="pricing-and-sla"></a>Prezzi e contratto di servizio

**Q:** che cos'è hello prezzi quando si usa l'anteprima pubblica di hello?

**R:** vengono addebitati metà hello quante ore che esegue l'app, con prezzi hello normale servizio App di Azure. Ciò significa che si ottiene uno sconto del 50% sul normale prezzo del Servizio app di Azure.

## <a name="other"></a>Altre

**Q:** quali sono i caratteri di hello è supportato nei nomi di impostazioni applicazione?

**R:** è solo possibile utilizzare A-Z, a-z, 0-9 e hello carattere di sottolineatura per le impostazioni dell'applicazione.

**D:** Dove è possibile richiedere nuove funzionalità?

**R:** è possibile inviare l'idea hello [forum sul feedback su applicazioni Web](https://aka.ms/webapps-uservoice). Aggiungere il titolo toohello "[Linux]" della propria idea.

## <a name="next-steps"></a>Passaggi successivi
* [Definizione di App Web di Azure in Linux](app-service-linux-intro.md)
* [SSH support for Azure Web App on Linux](./app-service-linux-ssh-support.md) (Supporto SSH per App Web di Azure in Linux)
* [Configurare gli ambienti di gestione temporanea nel Servizio app di Azure](./web-sites-staged-publishing.md)
* [Distribuzione continua con App Web di Azure in Linux](./app-service-linux-ci-cd.md)
