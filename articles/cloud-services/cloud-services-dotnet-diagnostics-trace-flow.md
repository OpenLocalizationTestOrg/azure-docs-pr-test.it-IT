---
title: flusso di hello aaaTrace in un'applicazione di servizi Cloud con diagnostica di Azure | Documenti Microsoft
description: Aggiungere il debug di traccia messaggi tooan applicazione Azure toohelp, misurazione delle prestazioni, monitoraggio, analisi del traffico e altro ancora.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>Flusso di hello traccia di un'applicazione di servizi Cloud con diagnostica di Azure
La traccia è un modo per si toomonitor hello esecuzione dell'applicazione mentre è in esecuzione. È possibile utilizzare hello [Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), e [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classi toorecord informazioni sugli errori e esecuzione dell'applicazione in log, file di testo o altri dispositivi per l'analisi successiva. Per altre informazioni sulle funzionalità di traccia, vedere l'articolo sulle modalità per [tracciare e instrumentare applicazioni](https://msdn.microsoft.com/library/zs6s4h68.aspx).

## <a name="use-trace-statements-and-trace-switches"></a>Usare istruzioni e opzioni di traccia
Traccia di implementare nell'applicazione di servizi Cloud mediante l'aggiunta di hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello configurazione dell'applicazione e rendendo chiama tooSystem.Diagnostics.Trace o debug nel codice dell'applicazione. Utilizza il file di configurazione hello *app* per i ruoli di lavoro e hello *Web. config* per i ruoli web. Quando si crea un nuovo servizio ospitato con un modello di Visual Studio, diagnostica Azure viene aggiunto automaticamente il progetto toohello e hello DiagnosticMonitorTraceListener viene aggiunto il file di configurazione appropriato toohello per ruoli hello da aggiungere.

Per informazioni sull'inserimento delle istruzioni di traccia, vedere [procedura: aggiungere istruzioni di traccia tooApplication codice](https://msdn.microsoft.com/library/zd83saa2.aspx).

Inserendo [opzioni di traccia](https://msdn.microsoft.com/library/3at424ac.aspx) nel codice, è possibile controllare se la traccia viene eseguita e con quale copertura. Ciò consente di monitorare lo stato di hello dell'applicazione in un ambiente di produzione. Questo aspetto è particolarmente importante in un'applicazione aziendale che usa più componenti in esecuzione su più computer. Per altre informazioni, vedere la [procedura per configurare opzioni di traccia](https://msdn.microsoft.com/library/t06xyy08.aspx).

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>Configurare il listener di traccia di hello in un'applicazione Azure
Traccia, Debug e TraceSource, è necessario impostare "listener" toocollect e messaggi hello record che vengono inviati. I listener raccolgono, archiviano e indirizzano i messaggi di traccia, Indicano hello traccia output tooan destinazione appropriata, ad esempio un log, una finestra o un file di testo. Diagnostica di Azure Usa hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) classe.

Prima di completare la seguente procedura hello, è necessario inizializzare hello monitoraggio diagnostica Azure. toodo questa operazione, vedere [abilitazione di diagnostica Microsoft Azure](cloud-services-dotnet-diagnostics.md).

Si noti che se si utilizzano i modelli di hello forniti da Visual Studio, hello configurazione del listener hello viene aggiunta automaticamente per l'utente.

### <a name="add-a-trace-listener"></a>Aggiungere un listener di traccia
1. Aprire il file Web. config o App. config di hello per il ruolo.
2. Aggiungere i seguenti file di codice toohello hello. Modificare hello versione attributo toouse hello numero di versione dell'assembly hello che viene fatto riferimento. versione dell'assembly Hello non necessariamente modificato con ogni versione di Azure SDK a meno che non sono presenti aggiornamenti tooit.
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > Assicurarsi di avere un toohello di riferimento di progetto Microsoft.WindowsAzure.Diagnostics assembly. Numero di versione di aggiornamento hello in xml hello precedente versione di hello toomatch di hello riferimento Microsoft.WindowsAzure.Diagnostics assembly.
   > 
   > 
3. Salvare il file di configurazione di hello.

Per altre informazioni sui listener, vedere l'articolo sui [listener di traccia](https://msdn.microsoft.com/library/4y5y10s7.aspx).

Dopo aver completato i listener di hello passaggi tooadd hello, è possibile aggiungere codice tooyour istruzioni di traccia.

### <a name="tooadd-trace-statement-tooyour-code"></a>codice di tooyour tooadd traccia istruzione
1. Aprire un file di origine per l'applicazione, Ad esempio, hello <RoleName>file con estensione cs per il ruolo di lavoro hello o web.
2. Aggiungere il seguente hello utilizzando l'istruzione se non è già stata aggiunta:
    ```
        using System.Diagnostics;
    ```
3. Aggiungere istruzioni di traccia in cui si desiderano toocapture informazioni sullo stato di hello dell'applicazione. È possibile utilizzare un'ampia gamma di output di hello tooformat metodi di hello istruzione di traccia. Per ulteriori informazioni, vedere [procedura: aggiungere istruzioni di traccia tooApplication codice](https://msdn.microsoft.com/library/zd83saa2.aspx).
4. Salvare il file di origine hello.

