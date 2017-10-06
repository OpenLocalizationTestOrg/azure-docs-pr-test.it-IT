---
title: gli eventi del ciclo di vita del servizio di Cloud aaaHandle | Documenti Microsoft
description: Informazioni su come hello del ciclo di vita di un ruolo del servizio Cloud possono essere utilizzati in .NET
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>Personalizzare hello del ciclo di vita di un ruolo Web o di lavoro in .NET
Quando si crea un ruolo di lavoro, si estende hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) classe che fornisce metodi per l'utente toooverride che consentono di rispondere a eventi toolifecycle. Per i ruoli web questa classe è facoltativa, è necessario utilizzare toorespond toolifecycle eventi.

## <a name="extend-hello-roleentrypoint-class"></a>Estendere una classe RoleEntryPoint hello
Hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) classe include metodi che vengono chiamati da Azure quando si **inizia**, **esegue**, o **Arresta** un ruolo web o di lavoro. Facoltativamente, è possibile ignorare questi metodi toomanage ruolo inizializzazione, sequenze di arresto di ruolo o thread di esecuzione hello del ruolo hello. 

Quando si estende **RoleEntryPoint**, è necessario essere consapevoli di hello seguenti comportamenti dei metodi di hello:

* Hello [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) e [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) metodi restituiscono un valore booleano, pertanto è possibile tooreturn **false** da questi metodi.
  
   Se il codice restituisce **false**, processo del ruolo hello viene terminato bruscamente, senza eseguire qualsiasi sequenza di arresto è possibile sul posto. In generale, è consigliabile evitare la restituzione **false** da hello **OnStart** metodo.
* Qualsiasi eccezione non rilevata all'interno di un overload di un metodo **RoleEntryPoint** viene considerato come un'eccezione non gestita.
  
   Se si verifica un'eccezione all'interno di uno dei metodi del ciclo di vita di hello, Azure genererà hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) evento, e quindi viene terminato il processo di hello. Quando il ruolo viene portato offline, viene riavviato da Azure. Quando un'eccezione non gestita si verifica, hello [arresto](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) evento non viene generato e hello **OnStop** non viene chiamato.

Se il ruolo non si avvia, oppure il riciclo tra hello durante l'inizializzazione, occupati e arresto di stati, il codice potrebbe generare un'eccezione non gestita all'interno di uno degli eventi del ciclo di vita hello che ogni ruolo di hello ora viene riavviato. In questo caso, utilizzare hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) toodetermine evento hello causa dell'eccezione hello e gestirlo in modo appropriato. Il ruolo potrebbe restituire anche da hello [eseguire](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (metodo), provocando toorestart ruolo hello. Per ulteriori informazioni sugli stati di distribuzione, vedere [tooRecycle comuni problemi che causa ruoli](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

> [!NOTE]
> Se si utilizza hello **strumenti di Azure per Microsoft Visual Studio** toodevelop l'applicazione, modelli di progetto di ruolo hello estendono automaticamente hello **RoleEntryPoint** classe, hello *WebRole.cs* e *WorkerRole.cs* file.
> 
> 

## <a name="onstart-method"></a>Metodo OnStart
Hello **OnStart** metodo viene chiamato quando l'istanza del ruolo viene portata online da Azure. Durante l'esecuzione di codice OnStart hello, l'istanza del ruolo hello è contrassegnato come **occupato** sia tooit diretto dal servizio di bilanciamento del carico hello alcun traffico esterno. È possibile eseguire l'override di questo operazioni di inizializzazione tooperform (metodo), ad esempio l'implementazione dei gestori eventi e l'avvio di [diagnostica Azure](cloud-services-how-to-monitor.md).

Se **OnStart** restituisce **true**, istanza hello è inizializzata correttamente e Azure chiama hello **Roleentrypoint** metodo. Se **OnStart** restituisce **false**, ruolo hello termina immediatamente, senza l'esecuzione di tutte le sequenze di arresto pianificato.

Hello seguente come esempio di codice hello toooverride **OnStart** metodo. Questo metodo configura e avvia un monitor di diagnostica quando l'istanza del ruolo hello viene avviato e impostato il trasferimento di account di archiviazione di dati tooa di registrazione:

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>Metodo OnStop
Hello **OnStop** metodo viene chiamato quando un'istanza del ruolo viene portata offline da Azure e prima dell'uscita dal processo hello. È possibile eseguire l'override di questo codice toocall metodo necessario per toocleanly di istanza del ruolo arrestato.

> [!IMPORTANT]
> Il codice in esecuzione in hello **OnStop** metodo ha un periodo di tempo limitato di toofinish quando viene chiamato per motivi diversi da un arresto avviato dall'utente. Trascorso tale tempo, hello processo viene terminato, pertanto è necessario assicurarsi che il codice in hello **OnStop** metodo possa essere eseguito rapidamente o tollerata toocompletion non è in esecuzione. Hello **OnStop** metodo viene chiamato dopo hello **arresto** viene generato l'evento.
> 
> 

## <a name="run-method"></a>Metodo Run
È possibile eseguire l'override di hello **eseguire** metodo tooimplement un thread di lunga durata per l'istanza del ruolo.

Si esegue l'override di hello **eseguire** metodo non è obbligatorio; l'implementazione predefinita di hello avvia un thread in costante stato di sospensione. Se si esegue l'override di hello **eseguire** (metodo), il codice dovrebbe bloccarsi per un periodo illimitato. Se hello **eseguire** metodo viene restituito, hello ruolo automaticamente normalmente riciclato; in altre parole, Azure hello **arresto** eventi e chiamate hello **OnStop** metodo in modo che è possibile eseguire le sequenze di arresto prima hello ruolo venga portato offline.

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>Implementazione dei metodi del ciclo di vita ASP.NET hello per un ruolo web
È possibile utilizzare metodi del ciclo di vita ASP.NET hello, inoltre toothose fornito da hello **RoleEntryPoint** classe toomanage sequenze di inizializzazione e di arresto per un ruolo web. Potrebbe essere utile per motivi di compatibilità se si trasferisce un tooAzure di applicazioni ASP.NET esistenti. metodi del ciclo di vita ASP.NET Hello vengano chiamati dall'interno di hello **RoleEntryPoint** metodi. Hello **applicazione\_avviare** metodo viene chiamato dopo hello **Roleentrypoint** al termine di metodo. Hello **applicazione\_fine** metodo viene chiamato prima hello **Roleentrypoint** metodo viene chiamato.

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come troppo[creare un pacchetto del servizio cloud](cloud-services-model-and-package.md).

