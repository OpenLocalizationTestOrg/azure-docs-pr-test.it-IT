---
title: aaaHow tooupgrade progetti toohello versione corrente di hello gli strumenti di Azure | Documenti Microsoft
description: Informazioni su come progetto di Azure tooupgrade nella versione corrente di Visual Studio toohello di hello gli strumenti di Azure
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>Come tooupgrade progetti toohello versione corrente di hello Azure Tools per Visual Studio
## <a name="overview"></a>Panoramica
Dopo aver installato una versione corrente di hello di strumenti di Azure hello (o una versione precedente che è successiva alla versione 1.6), tutti i progetti creati mediante una versione precedente alla 1.6 (novembre 2011) verranno aggiornate automaticamente non appena vengono aperti. Se per creare progetti tramite hello 1.6 (novembre 2011) versione di questi strumenti e avere la versione installata, è possibile aprire i progetti nella versione precedente di hello e decidere in un secondo momento se tooupgrade li.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Modifiche apportate al progetto durante l'aggiornamento
Se un progetto viene automaticamente aggiornato o si specifica che si desidera, il progetto è tooupgrade toowork con le versioni correnti di alcuni assembly e alcune proprietà vengono modificate anche come descritto in questa sezione. Se il progetto richiede altre modifiche di toobe compatibile con la versione più recente di hello degli strumenti di hello, è necessario apportare queste modifiche manualmente.

* il file Web. config Hello per i ruoli web e il file app. config hello per i ruoli di lavoro vengono aggiornati tooreference versione più recente di hello di Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll.
* gli assembly Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll e Microsoft.WindowsAzure.ServiceRuntime.dll Hello sono aggiornati toohello nuove versioni.
* Profili di pubblicazione sono stati archiviati nel file di progetto Azure hello (. ccproj) sono file separato tooa spostato, con estensione azurepubxml hello, in hello **pubblica** sottodirectory.
* Alcune proprietà hello profilo di pubblicazione vengono aggiornate toosupport funzionalità nuove e modificate. **AllowUpgrade** viene sostituito da **DeploymentReplacementMethod** perché è possibile aggiornare un servizio cloud distribuito in modo simultaneo o incrementale.
* proprietà Hello **UseIISExpressByDefault** viene aggiunta e impostare toofalse in modo che hello server web che viene utilizzato per il debug non verranno modificati automaticamente da Internet Information Services (IIS) tooIIS Express. IIS Express è server web di hello predefinito per i progetti creati con le versioni più recenti degli strumenti hello hello.
* Se la memorizzazione nella cache di Azure è ospitato in uno o più ruoli del progetto, alcune proprietà nella configurazione del servizio hello (file con estensione cscfg) e nella definizione di servizio (file con estensione csdef) vengono modificate quando si aggiorna un progetto. Se il progetto hello Usa hello del pacchetto NuGet di Caching di Azure, il progetto di hello è toohello aggiornato la versione più recente del pacchetto di hello. È consigliabile aprire il file Web. config hello e verificare che la configurazione client hello è stata gestita correttamente durante il processo di aggiornamento hello. Se si aggiungono gli assembly client di memorizzazione nella cache di hello riferimenti tooAzure senza utilizzare il pacchetto NuGet di hello, questi assembly non verranno aggiornati; è necessario aggiornare manualmente le nuove versioni toohello di riferimenti.

> [!IMPORTANT]
> Per progetti F #, è necessario aggiornare manualmente gli assembly di riferimenti tooAzure in modo che fanno riferimento a versioni più recenti di hello di tali assembly.
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>La modalità di progetto la versione corrente di toohello tooupgrade di Azure
1. Installazione hello corrente aggiornare la versione di hello strumenti di Azure nell'installazione hello di Visual Studio che si vuole toouse per hello progetto e quindi aprire hello progetto che si desidera tooupgrade. Se il progetto di hello è stato creato con una versione precedente alla 1.6 (novembre 2011), il progetto hello è la versione corrente di toohello aggiornato automaticamente. Se il progetto hello è stato creato con hello versione di novembre 2011 e tale versione è ancora installata, verrà aperto il progetto di hello in tale versione.
2. In Esplora soluzioni, il menu di scelta rapida aprire hello hello nodo di progetto, scegliere **proprietà**, quindi scegliere hello **applicazione** scheda della finestra di dialogo hello visualizzata.
   
    Hello **applicazione** scheda Mostra versione degli strumenti hello associata progetto hello. Se viene visualizzato versione corrente di hello degli strumenti di Azure, il progetto di hello è già stato aggiornato. Se è stato installato una versione più recente degli strumenti hello rispetto a quale scheda hello illustrato, un **aggiornamento** pulsante viene visualizzato.
3. Scegliere hello **aggiornamento** pulsante tooupgrade una versione corrente di toohello progetto degli strumenti hello.
4. Compilare il progetto hello e quindi risolvere gli eventuali errori risultanti dalle modifiche API. Per informazioni su come toomodify il codice per la nuova versione hello, vedere la documentazione di hello per hello API specifica.

