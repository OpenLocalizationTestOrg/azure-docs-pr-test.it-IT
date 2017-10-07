---
title: Argomenti di eseguire l'aggiornamento dell'applicazione aaaAdvanced | Documenti Microsoft
description: Questo articolo descrive alcuni argomenti avanzati relativi tooupgrading un'applicazione di Service Fabric.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>Aggiornamento di un'applicazione di Service Fabric: argomenti avanzati
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>Aggiungere o rimuovere servizi durante l'aggiornamento di un'applicazione
Se un nuovo servizio viene aggiunto tooan applicazione già distribuita, viene pubblicato come un aggiornamento, nuovo servizio hello è applicazione aggiunta toohello distribuito.  Di un aggiornamento non influisce sugli servizi hello che erano già parte di un'applicazione hello. Tuttavia, è necessario avviare un'istanza del servizio hello che è stato aggiunto per hello nuovo servizio toobe active (utilizzando hello `New-ServiceFabricService` cmdlet).

Un aggiornamento può anche prevedere la rimozione di determinati servizi da un'applicazione. Tuttavia, è necessario arrestare tutte le istanze correnti del servizio di hello-eliminato prima di procedere con l'aggiornamento di hello (utilizzando hello `Remove-ServiceFabricService` cmdlet).

## <a name="manual-upgrade-mode"></a>Modalità di aggiornamento manuale
> [!NOTE]
> modalità manuale di Hello non monitorato deve essere considerata solo per un aggiornamento non riuscito o sospeso. modalità monitorato Hello è hello consigliata la modalità di aggiornamento per le applicazioni di Service Fabric.
>
>

Azure Service Fabric fornisce più modalità di aggiornamento dei cluster di sviluppo e produzione toosupport. Le opzioni di distribuzione scelte possono essere diverse per ambienti diversi.

aggiornamento dell'applicazione Hello monitorato è hello toouse più comuni di aggiornamento nell'ambiente di produzione hello. Quando hello esegue l'aggiornamento dei criteri sono specificato, Service Fabric assicura che un'applicazione hello sia integra prima di avviare l'aggiornamento di hello.

 amministratore dell'applicazione Hello è possibile utilizzare vari domini di aggiornamento in sequenza applicazione la modalità di aggiornamento toohave il controllo totale hello aggiornamento lo stato di avanzamento tramite hello manuale di hello. Questa modalità è utile quando è necessario un criterio di valutazione salute personalizzato o complesso, o si verifica un aggiornamento non convenzionali (ad esempio, un'applicazione hello è già la perdita di dati).

Infine, hello automatizzati applicazione aggiornamento in sequenza è utile per lo sviluppo o test ambienti tooprovide una rapida iterazione del ciclo durante lo sviluppo del servizio.

## <a name="change-toomanual-upgrade-mode"></a>Modifica della modalità di aggiornamento toomanual
**Manuale**: aggiornamento dell'applicazione hello Stop nel hello UD e modifica corrente hello aggiornare tooUnmonitored modalità manuale. amministratore Hello deve chiamata toomanually **MoveNextApplicationUpgradeDomainAsync** tooproceed con hello aggiornare o attivare un'operazione di rollback avviando un nuovo aggiornamento. Dopo l'aggiornamento di hello entra in modalità manuale hello, rimane in modalità manuale hello fino a quando non viene avviato un nuovo aggiornamento. Hello **GetApplicationUpgradeProgressAsync** comando restituisce infrastruttura\_applicazione\_aggiornamento\_stato\_materiale\_Avanti\_in sospeso.

## <a name="upgrade-with-a-diff-package"></a>Aggiornare con un pacchetto Diff
Un'applicazione di Service Fabric può essere aggiornata effettuando il provisioning con un pacchetto applicazione completo e autonomo. Un'applicazione può inoltre essere aggiornata tramite un pacchetto delle differenze che contiene solo i file di applicazione hello aggiornato, hello aggiornata manifesto dell'applicazione e file manifesto del servizio hello.

Un pacchetto dell'applicazione completo contiene tutti i toostart necessarie di hello file ed esegue un'applicazione di Service Fabric. Un pacchetto diff contiene solo i file hello modificato tra il provisioning di ultima hello e l'aggiornamento corrente di hello più hello completo manifesto applicazione e servizio hello file manifesto. Qualsiasi riferimento nel manifesto dell'applicazione hello o manifesto del servizio che non possa essere trovata nel layout di compilazione hello viene cercata nell'archivio immagini hello.

I pacchetti dell'intera applicazione sono necessari per l'installazione prima di un cluster di toohello applicazione hello. Gli aggiornamenti successivi possono essere eseguiti con un pacchetto applicazione completo o con un pacchetto Diff.

L'uso di un pacchetto Diff è consigliato nei casi seguenti:

* Se è disponibile un pacchetto dell'applicazione di grandi dimensioni che fa riferimento a più file manifesto del servizio e/o a più pacchetti di codice, di configurazione o di dati.
* Un pacchetto delle differenze è preferito quando si dispone di un sistema di distribuzione che genera il layout di compilazione hello direttamente dal processo di compilazione dell'applicazione. In questo caso, anche se non è stato modificato il codice hello, assembly appena compilato ottenere un checksum diverso. Utilizzo di un pacchetto di applicazione completa richiederebbe si tooupdate hello versione per tutti i pacchetti di codice. Utilizzo di un pacchetto di differenze, è solo fornire file hello modificata e i file di manifesto hello in versione di hello è stata modificata.

Quando si aggiorna un'applicazione con Visual Studio, è possibile che il pacchetto di diff hello viene pubblicato automaticamente. un pacchetto diff toocreate hello manualmente, il manifesto dell'applicazione e hello manifesti di servizio devono essere aggiornati, ma solo i pacchetti hello modificato devono essere inclusi nel pacchetto finale dell'applicazione hello.

Ad esempio, iniziamo con hello seguito domanda (forniti per facilitare la comprensione i numeri di versione):

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

A questo punto, si supponga che si desiderava tooupdate solo hello codice pacchetto Service1 utilizzando un pacchetto diff tramite PowerShell. A questo punto, l'applicazione aggiornata è hello seguente struttura di cartelle:

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

In questo caso, aggiornare too2.0.0 manifesto di applicazione hello e manifesto del servizio per l'aggiornamento del pacchetto di service1 tooreflect hello codice hello. cartella Hello per il pacchetto di applicazione avrebbe hello seguente struttura:

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>Passaggi successivi
[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.

[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.

Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).

Apportare aggiornamenti applicazione compatibile da learning come toouse [la serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).

Risolvere i problemi comuni negli aggiornamenti dell'applicazione riferendosi passaggi toohello [risoluzione dei problemi gli aggiornamenti dell'applicazione](service-fabric-application-upgrade-troubleshooting.md).
