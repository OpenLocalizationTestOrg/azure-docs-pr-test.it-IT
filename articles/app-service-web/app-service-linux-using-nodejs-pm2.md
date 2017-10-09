---
title: configurazione aaaUsing PM2 per Node.js in Azure Web App in Linux | Documenti Microsoft
description: Uso della configurazione PM2 per Node.js in App Web di Azure su Linux
keywords: Servizio app di Azure, app Web, nodejs, PM2, Linux, OSS
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>Usare la configurazione PM2 per Node.js in App Web di Azure su Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Se si imposta hello applicazione stack tooNode.js per l'App Web di Azure in Linux, viene visualizzato hello opzione tooset un file di avvio Node.js come illustrato nella seguente immagine hello:

![Impostare un file di avvio Node.js][1]

È possibile utilizzare questa opzione toodo uno di hello seguenti attività:

* Specificare uno script di avvio hello per l'app Node.js (ad esempio: /bin/server.js).
* Specificare toouse di file di configurazione di hello PM2 per l'app Node.js (ad esempio: /foo/process.json).
  
  > [!NOTE]
  > Se si desidera il toorestart processi Node.js automaticamente quando vengono modificate di determinati file, utilizzare configurazione PM2 hello. In caso contrario, l'applicazione non verrà riavviata quando riceve notifiche di modifica, ad esempio quando viene modificato il codice dell'applicazione.
  > 
  > 

È possibile controllare hello Node.js [elaborare documentazione file](http://pm2.keymetrics.io/docs/usage/application-declaration/) per tutte le opzioni di hello, ma di seguito è riportato un esempio di ciò che è possibile utilizzare come file di process.json:

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

Toonote aspetti importanti in questa configurazione sono:

* proprietà "script" Hello specifica script di avvio dell'applicazione.
* proprietà di "instances" Hello specifica il numero di istanze di hello nodo processo toolaunch. Se si esegue l'applicazione in macchine virtuali di dimensioni maggiori con più core, è una buona idea toomaximize delle risorse impostando un valore più alto qui.
* Hello "controllo" matrice specifica tutti i file che si desidera che toorestart hello nodo processo per quando vengono modificate.
* Per "watch_options" hello, è attualmente necessario toospecify "usePolling" come true a causa delle modalità di hello che è montato il contenuto dell'applicazione.

## <a name="next-steps"></a>Passaggi successivi
* [Definizione di App Web di Azure in Linux](app-service-linux-intro.md)
* [Domande frequenti su App Web del Servizio app di Azure su Linux](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
