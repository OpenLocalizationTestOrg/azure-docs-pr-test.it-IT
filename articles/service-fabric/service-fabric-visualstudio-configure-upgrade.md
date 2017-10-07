---
title: aggiornamento di hello aaaConfigure di un'applicazione di Service Fabric | Documenti Microsoft
description: Informazioni su come tooconfigure hello impostazioni per l'aggiornamento di un'applicazione di Service Fabric con Microsoft Visual Studio.
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Configurare l'aggiornamento hello di un'applicazione di Service Fabric in Visual Studio
Visual Studio tools per Azure Service Fabric forniscono supporto per l'aggiornamento per la pubblicazione toolocal o dei cluster remoti. Esistono tre scenari in cui si desidera tooupgrade la versione più recente tooa di applicazione non sostituisce un'applicazione hello durante i test e debug:

* Dati dell'applicazione non venga persi durante l'aggiornamento di hello.
* Disponibilità resta alta in modo non qualsiasi interruzione del servizio durante l'aggiornamento di hello, se non esistono che sufficienti le istanze del servizio distribuiti in domini di aggiornamento.
* Durante l'aggiornamento, possono essere eseguiti test in un'applicazione.

## <a name="parameters-needed-tooupgrade"></a>Parametri necessari tooupgrade
È possibile scegliere tra due tipi di distribuzione: normale o aggiornata. Una distribuzione normale Cancella i dati nel cluster hello e informazioni sulla distribuzione precedente distribuzione di un aggiornamento mantiene il. Quando si aggiorna un'applicazione di Service Fabric in Visual Studio, è necessario tooprovide parametri di aggiornamento dell'applicazione e i criteri di controllo di integrità. Aggiornamento dell'applicazione i parametri consentono di controllare l'aggiornamento di hello, mentre i criteri di controllo di integrità determinano se l'aggiornamento di hello ha avuto esito positivo. Vedere l'articolo relativo all' [aggiornamento di un'applicazione di Service Fabric e i parametri di aggiornamento](service-fabric-application-upgrade-parameters.md) per ulteriori dettagli.

Sono disponibili tre modalità di aggiornamento: *Monitored*, *UnmonitoredAuto* e *UnmonitoredManual*.

* Un aggiornamento di monitoraggio consente di automatizzare l'aggiornamento di hello e applicazione controllo di integrità.
* Un aggiornamento UnmonitoredAuto consente di automatizzare l'aggiornamento di hello, ma ignora hello verifica integrità dell'applicazione.
* Quando si esegue un aggiornamento UnmonitoredManual, è necessario toomanually aggiornare ogni dominio di aggiornamento.

Ogni modalità di aggiornamento richiede diversi set di parametri. Vedere [parametri di aggiornamento dell'applicazione](service-fabric-application-upgrade-parameters.md) toolearn ulteriori informazioni sulle opzioni di aggiornamento disponibili hello.

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>Aggiornamento di un'applicazione di Infrastruttura di servizi in Visual Studio
Se si utilizza tooupgrade strumenti di Visual Studio Service Fabric hello un'applicazione di Service Fabric, specificare un toobe processo pubblica un aggiornamento anziché una distribuzione normale controllando hello **l'aggiornamento di un'applicazione hello** controllare casella.

### <a name="tooconfigure-hello-upgrade-parameters"></a>parametri di aggiornamento hello tooconfigure
1. Fare clic su hello **impostazioni** pulsante Avanti toohello casella di controllo. Hello **modifica parametri aggiornamento** viene visualizzata la finestra di dialogo. Hello **modifica parametri aggiornamento** la finestra di dialogo supporta la modalità aggiornamento hello monitorati, UnmonitoredAuto e UnmonitoredManual.
2. Selezionare la modalità di aggiornamento hello toouse desiderati e quindi compilare griglia parametro hello.

    Ogni parametro ha valori predefiniti. parametro facoltativo Hello *DefaultServiceTypeHealthPolicy* accetta un input di tabella hash. Di seguito è riportato un esempio di hello input formato della tabella hash per *DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *ServiceTypeHealthPolicyMap* è un altro parametro facoltativo che accetta un input di tabella hash in hello seguente formato:

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    Ecco un esempio reale:

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. Se si seleziona la modalità di aggiornamento UnmonitoredManual, è necessario avviare un toocontinue console PowerShell manualmente e completare hello processo di aggiornamento. Fare riferimento troppo[aggiornamento dell'applicazione di Service Fabric: argomenti avanzati](service-fabric-application-upgrade-advanced.md) toolearn manuale aggiornare works.

## <a name="upgrade-an-application-by-using-powershell"></a>Aggiornare un'applicazione con PowerShell
È possibile utilizzare i cmdlet di PowerShell tooupgrade un'applicazione di Service Fabric. Per informazioni dettagliate, vedere [Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) e [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx).

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Specificare un criterio di controllo di integrità nel file manifesto dell'applicazione hello
Ogni servizio in un'applicazione di Service Fabric può avere i propri parametri di criteri di integrità che eseguono l'override di valori predefiniti di hello. È possibile fornire i valori di parametro nel file manifesto dell'applicazione hello.

Hello esempio seguente viene illustrato come tooapply salute univoca controllare criteri per ogni servizio nel manifesto dell'applicazione hello.

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulla distribuzione di un'applicazione, vedere [Distribuire un'applicazione esistente in Infrastruttura di servizi di Azure](service-fabric-deploy-existing-app.md).