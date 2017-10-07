---
title: dimensioni della cartella TEMP aaaDefault sono troppo piccola per un ruolo | Documenti Microsoft
description: "Un ruolo del servizio cloud dispone di una quantità limitata di spazio per la cartella TEMP hello. In questo articolo vengono forniti alcuni suggerimenti su come tooavoid sta esaurendo lo spazio."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a>Dimensioni della cartella TEMP predefinita ridotte per un ruolo di lavoro/Web del servizio cloud
Per impostazione predefinita Hello directory temporanea di un ruolo web o di lavoro del servizio cloud ha una dimensione massima di 100 MB, che possono diventare completo a un certo punto. Questo articolo viene descritto come tooavoid sta esaurendo lo spazio per la directory temporanea di hello.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a>Perché ho esaurito lo spazio?
Hello standard Windows variabili di ambiente TEMP e TMP sono disponibili toocode che è in esecuzione nell'applicazione. Sia TEMP e TMP tooa punto singola directory con una dimensione massima di 100 MB. Tutti i dati vengono archiviati in questa directory non sono persistente nel ciclo di vita di hello del servizio cloud hello; Se le istanze del ruolo hello in un servizio cloud vengono riciclate, directory di hello viene pulita.

## <a name="suggestion-toofix-hello-problem"></a>Problema di hello toofix suggerimento
Implementare una delle seguenti alternative hello:

* Configurare una risorsa di archiviazione locale e accedervi direttamente invece che usando TEMP o TMP. una risorsa di archiviazione locale dal codice che è in esecuzione all'interno dell'applicazione, chiamata hello tooaccess [roleenvironment. Getlocalresource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) metodo.
* Configurare una risorsa di archiviazione locale e scegliere hello TEMP e TMP directory toopoint toohello percorso della risorsa di archiviazione locale di hello. Questa modifica deve essere eseguita all'interno di hello [Roleentrypoint](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) metodo.

Hello esempio di codice seguente viene illustrato come toomodify hello directory di destinazione per TEMP e TMP dal metodo OnStart hello:

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
Lettura di un blog che descrive [come tooincrease hello dimensioni della cartella temporanea ASP.NET ruolo Web Azure hello](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).

Altri [articoli sulla risoluzione dei problemi](/?tag=top-support-issue&product=cloud-services) per i servizi cloud.

toolearn come ruolo del servizio cloud tootroubleshoot problemi utilizzando i dati di diagnostica di Azure PaaS computer, visualizzare [serie di blog di Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
