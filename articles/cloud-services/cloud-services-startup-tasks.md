---
title: "Attività di avvio di servizi Cloud di Azure aaaRun | Documenti Microsoft"
description: "Le attività di avvio consentono di preparare l'ambiente del servizio cloud per l'app. Spiega che l'attività di avvio del lavoro e la modalità toomake li"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>Modalità di avvio tooconfigure ed eseguire attività per un servizio cloud
È possibile utilizzare le operazioni di avvio attività tooperform prima dell'avvio di un ruolo. Le operazioni che è possibile tooperform includono l'installazione di un componente, la registrazione dei componenti COM, impostano le chiavi del Registro di sistema o l'avvio di un processo a esecuzione prolungata.

> [!NOTE]
> Attività di avvio non sono applicabili tooVirtual macchine, solo tooCloud servizio Web e ruoli di lavoro.
> 
> 

## <a name="how-startup-tasks-work"></a>Funzionamento delle attività di avvio
Attività di avvio sono azioni che vengono eseguite prima che i ruoli begin e definiti in hello [Servicedefinition] file utilizzando hello [attività] elemento all'interno di hello [avvio]elemento. Spesso le attività di avvio sono file batch, ma possono essere anche applicazioni console o file batch tramite i quali si avviano script di PowerShell.

Le variabili di ambiente passano informazioni all'interno di un'attività di avvio e archiviazione locale può essere utilizzato toopass informazioni da un'attività di avvio. Ad esempio, una variabile di ambiente può specificare programma tooa di hello percorso desiderato tooinstall e i file possono essere scritti archiviazione toolocal che può quindi essere letti successivamente dai ruoli.

L'attività di avvio è possibile registrare informazioni e directory di toohello errori specificata da hello **TEMP** variabile di ambiente. Durante l'attività di avvio, hello hello **TEMP** variabile di ambiente risolve toohello *c:\\risorse\\temp\\[guid]. [ roleName]\\RoleTemp* directory durante l'esecuzione nel cloud hello.

Le attività di avvio possono inoltre essere eseguite più volte tra un riavvio e l'altro. Ad esempio, verrà eseguita l'attività di avvio hello ogni volta che viene riciclato il ruolo di hello e ricicli dei ruoli non includono necessariamente un riavvio. Attività di avvio devono essere scritti in modo che consenta loro toorun più volte senza problemi.

Attività di avvio devono terminare con un **errorlevel** (o codice di uscita) pari a zero per hello avvio processo toocomplete. Se un'attività di avvio termina con un diverso da zero **errorlevel**, hello ruolo non verrà avviato.

## <a name="role-startup-order"></a>Sequenza di avvio di un ruolo
Hello procedura elenchi hello ruolo avvio in Azure:

1. istanza di Hello è contrassegnata come **iniziale** e non riceve traffico.
2. Tutte le attività di avvio vengono eseguite in base tootheir **taskType** attributo.
   
   * Hello **semplice** attività vengono eseguite in modo sincrono, uno alla volta.
   * Hello **background** e **in primo piano** attività sono attività di avvio toohello parallela e avviato in modo asincrono.  
     
     > [!WARNING]
     > IIS potrebbe non essere completamente configurato durante la fase di attività di avvio hello nel processo di avvio hello, pertanto potrebbero non essere disponibili dati specifici del ruolo. Per le attività di avvio che richiedono dati specifici per il ruolo è necessario usare [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).
     > 
     > 
3. processo host del ruolo Hello viene avviato e viene creato il sito di hello in IIS.
4. Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) metodo viene chiamato.
5. istanza di Hello è contrassegnata come **pronto** e il traffico indirizzato toohello istanza.
6. Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo viene chiamato.

## <a name="example-of-a-startup-task"></a>Esempio di attività di avvio
Attività di avvio vengono definite nel hello [Servicedefinition] file hello **attività** elemento. Hello **commandLine** attributo specifica il nome di hello e parametri del batch di avvio hello file o comando della console, hello **executionContext** attributo specifica il livello di privilegio hello dell'avvio di hello attività e hello **taskType** attributo specifica l'esecuzione delle attività hello.

In questo esempio, una variabile di ambiente **MyVersionNumber**, viene creato per attività di avvio hello e impostare il valore di toohello "**1.0.0.0**".

**ServiceDefinition.csdef**:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

Nell'esempio seguente di hello, hello **Startup.cmd** file batch scrive la riga hello "la versione corrente di hello is 1.0.0.0" toohello StartupLog.txt file nella directory hello specificata dalla variabile di ambiente TEMP hello. Hello `EXIT /B 0` riga assicura l'attività di avvio hello termina con un **errorlevel** pari a zero.

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> In Visual Studio, hello **copiare tooOutput Directory** proprietà per il file batch di avvio deve essere impostata troppo**Copia sempre** toobe assicurarsi che il file batch di avvio sia correttamente distribuito tooyour in Azure (**approot\\bin** per i ruoli Web, e **approot** per i ruoli di lavoro).
> 
> 

## <a name="description-of-task-attributes"></a>Descrizione degli attributi di Task
Hello seguito vengono descritti gli attributi di hello di hello **attività** elemento hello [Servicedefinition] file:

**riga di comando** -specifica la riga di comando hello per attività di avvio hello:

* Hello comando, con i parametri della riga di comando facoltativi, che inizia l'attività di avvio hello.
* Questo è spesso hello filename di un file con estensione cmd o bat di batch.
* attività Hello è relativo toohello AppRoot\\cartella Bin per la distribuzione di hello. Le variabili di ambiente non vengono espanse per determinare il percorso di hello e dell'attività hello. Se è necessaria l'espansione dell'ambiente, è possibile creare un piccolo script con estensione cmd con il quale richiamare l'attività di avvio.
* Può essere un'applicazione console o un file batch che avvia uno [script di PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).

**executionContext** -specifica il livello di privilegio hello per attività di avvio hello. livello di privilegio Hello può essere limitata o con privilegi elevato:

* **limitato**  
  attività di avvio Hello viene eseguito con hello stessi privilegi del ruolo hello. Quando hello **executionContext** attributo per hello [Runtime] elemento è **limitato**, quindi vengono utilizzati i privilegi di utente.
* **elevato**  
  attività di avvio Hello viene eseguito con privilegi di amministratore. In questo modo le attività di avvio programmi tooinstall, apportare modifiche alla configurazione di IIS, eseguire le modifiche del Registro di sistema e altre attività a livello di amministratore senza aumentare il livello di privilegio hello del ruolo hello stesso.  

> [!NOTE]
> Hello il livello di privilegio dell'attività di avvio non è necessario toobe hello stesso come ruolo hello stesso.
> 
> 

**taskType** -specifica hello modo un'attività di avvio viene eseguito.

* **simple**  
  Le attività vengono eseguite in modo sincrono, uno alla volta, nell'ordine di hello specificato in hello [Servicedefinition] file. Quando uno **semplice** attività di avvio termina con un **errorlevel** pari a zero, hello successivamente **semplice** viene eseguita l'attività di avvio. Se non sono più **semplice** tooexecute, le attività di avvio, quindi verrà avviato il ruolo hello stesso.   
  
  > [!NOTE]
  > Se hello **semplice** attività termina con un diverso da zero **errorlevel**, hello istanza viene bloccata. Le successive **semplice** attività di avvio e ruolo hello stesso, non verrà avviato.
  > 
  > 
  
    tooensure che il file batch termina con un **errorlevel** pari a zero, eseguire il comando hello `EXIT /B 0` alla fine di hello del processo del file batch.
* **background**  
  Le attività vengono eseguite in modo asincrono, in parallelo con avvio hello del ruolo hello.
* **foreground**  
  Le attività vengono eseguite in modo asincrono, in parallelo con avvio hello del ruolo hello. Hello differenza fondamentale tra un **in primo piano** e **background** attività è che un **in primo piano** attività impedisce ruolo hello dal riciclo o arresto fino a quando non dispone di attività hello è terminata. Hello **background** attività non dispone di questa restrizione.

## <a name="environment-variables"></a>Variabili di ambiente
Le variabili di ambiente sono un'attività di avvio tooa modo toopass informazioni. Ad esempio, è possibile inserire hello percorso tooa blob che contiene tooinstall un programma, o numeri di porta che verrà utilizzato il ruolo o funzionalità toocontrol le impostazioni dell'attività di avvio.

Esistono due tipi di variabili di ambiente per attività di avvio. variabili di ambiente statiche e variabili di ambiente basano sui membri di hello [ RoleEnvironment] classe. Sono entrambi hello [ambiente] sezione di hello [Servicedefinition] file ed entrambi hello utilizzare [variabile] elemento e **nome** attributo.

Hello utilizza le variabili di ambiente statiche **valore** attributo di hello [variabile] elemento. esempio Hello precedente crea la variabile di ambiente hello **MyVersionNumber** che ha un valore statico di "**1.0.0.0**". Un altro esempio sarebbe toocreate un **StagingOrProduction** variabile di ambiente che è possibile impostare manualmente toovalues di "**di gestione temporanea**"o"**produzione**" tooperform azioni di avvio diverse in base al valore di hello di hello **StagingOrProduction** variabile di ambiente.

Le variabili di ambiente basate sui membri della classe RoleEnvironment hello non utilizzano hello **valore** attributo di hello [variabile] elemento. In alternativa, hello [RoleInstanceValue] elemento figlio, con hello appropriato **XPath** valore dell'attributo, viene utilizzati toocreate una variabile di ambiente in base a un membro specifico di hello [ RoleEnvironment] classe. I valori per hello **XPath** attributo tooaccess vari [ RoleEnvironment] sono disponibili valori [qui](cloud-services-role-config-xpath.md).

Ad esempio, toocreate una variabile di ambiente che è "**true**" quando l'istanza di hello è in esecuzione nell'emulatore di calcolo, hello e "**false**" durante l'esecuzione nel cloud hello, utilizzare l'esempio hello [variabile] e [RoleInstanceValue] elementi:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come tooperform alcuni [comuni attività di avvio](cloud-services-startup-tasks-common.md) con il servizio Cloud.

[Creare il pacchetto](cloud-services-model-and-package.md) del servizio cloud.  

[Servicedefinition]: cloud-services-model-and-package.md#csdef
[attività]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[avvio]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[ambiente]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[variabile]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
