---
title: aaaDebug l'applicazione dell'infrastruttura del servizio di Azure in Eclipse | Documenti Microsoft
description: "Migliorare hello affidabilità e prestazioni dei servizi, sviluppo e il debug in Eclipse in un cluster di sviluppo locale."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a>Eseguire il debug dell'applicazione Service Fabric di Java con Eclipse
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
> 

1. Avviare un cluster di sviluppo locale seguendo i passaggi di hello in [impostazione dell'ambiente di sviluppo di Service Fabric](service-fabric-get-started-linux.md).

2. Aggiornare entryPoint.sh del servizio hello desiderato toodebug, in modo che inizi il processo di java hello con i parametri di eseguire il debug remoto. Questo file è reperibile in hello seguente posizione: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``. In questo esempio la porta 8001 è impostata per il debug.

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. Aggiornare il manifesto dell'applicazione hello impostando il numero di istanze di hello o hello conteggio di replica per il servizio di hello che è in corso il debug too1. Questa impostazione consente di evitare conflitti per la porta hello che viene utilizzato per il debug. Ad esempio, per i servizi senza stati, impostare ``InstanceCount="1"`` e per i servizi con stati replica di destinazione e min hello set too1 dimensioni nel seguente modo: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.

4. Distribuire un'applicazione hello.

5. Nell'IDE di Eclipse hello, selezionare **esecuzione -> Debug Configurations -> applicazione Java remota e le proprietà di connessione di input** e impostare le proprietà di hello come indicato di seguito:

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  Impostare punti di interruzione in punti desiderati ed eseguire il debug di un'applicazione hello.

Se un'applicazione hello è arrestato in modo anomalo, è inoltre possibile tooenable coredumps. Eseguire ``ulimit -c`` in una shell e, se viene restituito 0, gli elementi core dump non sono abilitati. tooenable coredumps illimitato, eseguire hello comando seguente: ``ulimit -c unlimited``. È inoltre possibile verificare lo stato di hello utilizzando il comando hello ``ulimit -a``.  Se si desidera percorso di generazione tooupdate hello coredump, eseguire ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``. 

### <a name="next-steps"></a>Passaggi successivi

* [Raccogliere log con Diagnostica di Azure](service-fabric-diagnostics-how-to-setup-lad.md).
* [Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).
