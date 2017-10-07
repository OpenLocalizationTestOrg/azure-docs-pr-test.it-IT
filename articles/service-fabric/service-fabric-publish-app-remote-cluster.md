---
title: un cluster remoto tooa di app con Visual Studio aaaPublish | Documenti Microsoft
description: Informazioni su come toopublish un'infrastruttura di servizio remoto tooa applicazione cluster con Visual Studio.
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Distribuire e rimuovere applicazioni con Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [API FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Hello estensione Azure Service Fabric per Visual Studio fornisce un modo semplice, ripetibili e gestibile tramite script di toopublish un cluster di Service Fabric application tooa.

## <a name="hello-artifacts-required-for-publishing"></a>elementi di Hello necessari per la pubblicazione
### <a name="deploy-fabricapplicationps1"></a>Deploy-FabricApplication.ps1
Script di PowerShell che usa un percorso del profilo di pubblicazione come parametro per la pubblicazione di applicazioni dell'infrastruttura di servizi. Poiché questo script fa parte dell'applicazione, sono toomodify iniziale come necessario per l'applicazione.

### <a name="publish-profiles"></a>Profili di pubblicazione
Chiamata di una cartella nel progetto di applicazione di Service Fabric hello **PublishProfiles** contiene i file XML che archiviano informazioni essenziali per la pubblicazione di un'applicazione, ad esempio:

* Parametri di connessione del cluster Service Fabric
* File dei parametri di percorso tooan applicazione
* Impostazioni di aggiornamento

Per impostazione predefinita, l'applicazione include tre profili di pubblicazione: Local.1Node.xml, Local.5Node.xml e Cloud.xml. È possibile aggiungere altri profili copiando e incollando uno dei file predefiniti hello.

### <a name="application-parameter-files"></a>File di parametri dell'applicazione
Chiamata di una cartella nel progetto di applicazione di Service Fabric hello **ApplicationParameters** contiene file XML per i valori dei parametri del manifesto dell'applicazione specificata dall'utente. I file manifesto dell'applicazione possono essere parametrizzati in modo che si possano usare diversi valori per le impostazioni di distribuzione. toolearn ulteriori informazioni sull'applicazione di parametri dell'applicazione, vedere [gestire più ambienti in Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md).

> [!NOTE]
> Per i servizi actor compili il progetto hello prima di tentare il file hello tooedit in un editor o tramite hello pubblicare la finestra di dialogo. In questo modo verrà generato durante la compilazione di hello parte del file manifesto hello.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish un'applicazione utilizzando la finestra di dialogo di hello pubblicare l'applicazione di Service Fabric
Hello passaggi seguenti viene illustrato come un'applicazione utilizzando toopublish hello **pubblicare l'applicazione di Service Fabric** la finestra di dialogo fornita da strumenti di Visual Studio Service Fabric hello.

1. Scegliere hello dal menu di scelta rapida del progetto di applicazione di Service Fabric hello, **pubblica...** hello tooview **pubblicare l'applicazione di Service Fabric** la finestra di dialogo.
   
    ![Hello * * la finestra di dialogo Pubblica servizio Fabric applicazione * *][0]
   
    file Hello selezionato in hello **profilo di destinazione** elenco a discesa è dove tutte le impostazioni di hello, ad eccezione di **manifesto versioni**, vengono salvati. È possibile riutilizzare un profilo esistente o crearne uno nuovo scegliendo **< Gestione profili >** in hello **profilo di destinazione** elenco a discesa. Quando si sceglie un profilo di pubblicazione, il relativo contenuto vengono visualizzati nei campi corrispondenti di hello della finestra di dialogo hello. toosave le modifiche in qualsiasi momento, scegliere hello **Salva profilo** collegamento.    
2. In hello **endpoint della connessione** sezione, specificare l'endpoint di un cluster locale o remoto Service Fabric della pubblicazione. tooadd o modifica hello endpoint della connessione, fare clic su hello **Endpoint della connessione** elenco a discesa. elenco di Hello Mostra hello disponibili Service Fabric cluster connessione endpoint toowhich che è possibile pubblicare in base alle proprie sottoscrizioni Azure. Si noti che se non si è già connessi in tooVisual Studio, sarà richiesta toodo così.
   
    Utilizzare hello cluster selezione finestra di dialogo toochoose dal set di hello delle sottoscrizioni disponibili e i cluster.
   
    ![Hello * * la finestra di dialogo Seleziona servizio infrastruttura Cluster * *][1]
   
   > [!NOTE]
   > Se si desidera toopublish tooan endpoint arbitrario (ad esempio un cluster di terze parti), vedere hello **pubblicazione tooan cluster arbitrario endpoint** sezione riportata di seguito.
   > 
   > 
   
    Dopo aver scelto un endpoint, Visual Studio convalida cluster di Service Fabric hello connessione toohello selezionato. Se il cluster hello non è protetto, Visual Studio possono connettersi tooit immediatamente. Tuttavia, se il cluster hello è protetto, è necessario tooinstall un certificato nel computer locale prima di procedere. Vedere [come connessioni protette tooconfigure](service-fabric-visualstudio-configure-secure-connections.md) per ulteriori informazioni. Al termine, scegliere hello **OK** pulsante. cluster di Hello selezionato viene visualizzato in hello **pubblicare l'applicazione di Service Fabric** la finestra di dialogo.
3. In hello **File parametro applicazione** elenco a discesa passare tooan file dei parametri dell'applicazione. Un file di parametro dell'applicazione contiene i valori specificati dall'utente per i parametri nel file manifesto dell'applicazione hello. tooadd o modificare un parametro, scegliere hello **modifica** pulsante. Immettere o modificare il valore del parametro hello in hello **parametri** griglia. Al termine, scegliere hello **salvare** pulsante.
   
    ![Hello * * la finestra di dialogo Modifica parametri * *][2]
4. Hello utilizzare **hello aggiornamento applicazione** toospecify casella di controllo se questa azione di pubblicazione è un aggiornamento. Le operazioni di pubblicazione di aggiornamento differiscono dalle normali operazioni di pubblicazione. Per un elenco delle differenze, vedere l'articolo relativo all' [aggiornamento di un'applicazione dell'infrastruttura di servizi](service-fabric-application-upgrade.md) . impostazioni di aggiornamento tooconfigure, scegliere hello **configurare impostazioni di aggiornamento** collegamento. verrà visualizzato l'editor di aggiornamento parametro Hello. Vedere [configurare l'aggiornamento di un'applicazione di Service Fabric hello](service-fabric-visualstudio-configure-upgrade.md) toolearn ulteriori informazioni sui parametri di aggiornamento.
5. Scegliere hello **manifesto versioni...** hello tooview pulsante **modificare versioni** la finestra di dialogo. È necessario tooupdate versioni dell'applicazione e servizio per un punto di aggiornamento tootake. Vedere [tutorial di aggiornamento dell'applicazione di Service Fabric](service-fabric-application-upgrade-tutorial.md) toolearn come applicazione e le versioni del manifesto del servizio ridurre un processo di aggiornamento.
   
    ![Hello * * la finestra di dialogo Modifica versioni * *][3]
   
    Se un'applicazione hello e versioni del servizio usano controllo delle versioni semantico, ad esempio 1.0.0 o valori numerici in formato hello 1.0.0.0, selezionare hello **aggiornare automaticamente versioni dell'applicazione e servizio** opzione. Quando si sceglie questa opzione, il servizio hello e numeri di versione dell'applicazione vengono aggiornati automaticamente ogni volta che un codice, configurazione o versione del pacchetto di dati viene aggiornato. Se si preferiscono versioni hello tooedit manualmente, deselezionare hello casella di controllo toodisable questa funzionalità.
   
   > [!NOTE]
   > Per tooappear tutte le voci di pacchetto per un progetto attore, innanzitutto compilare hello progetto toogenerate voci hello nei file manifesto del servizio hello.
   > 
   > 
6. Al termine che specifica le impostazioni necessarie, hello scegliere hello **pubblica** pulsante toopublish toohello l'applicazione selezionata cluster di Service Fabric. vengono applicate le impostazioni di Hello specificato toohello processo di pubblicazione.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>Consente di pubblicare endpoint cluster arbitrario tooan (inclusi i cluster di terze parti)
Hello funzionalità di pubblicazione di Visual Studio è ottimizzata per la pubblicazione di cluster tooremote associato a una delle sottoscrizioni di Azure. Tuttavia, è possibile toopublish tooarbitrary endpoint (ad esempio, i cluster di terze parti di Service Fabric) da direttamente modifica hello XML del profilo di pubblicazione. Come descritto in precedenza, tre profili di pubblicazione vengono forniti per impostazione predefinita:**Local.1Node.xml**, **Local.5Node.xml**, e **Cloud.xml**, ma sono toocreate iniziale profili aggiuntivi per ambienti diversi. Ad esempio, è possibile toocreate un profilo per la pubblicazione di cluster tooparty, talvolta denominato **Party.xml**.

Se ci si connette tooan non protette del cluster, tutto ciò che ha richiesto è endpoint della connessione hello cluster, ad esempio `partycluster1.eastus.cloudapp.azure.com:19000`. In quanto pubblicare endpoint della connessione hello in hello case, profilo avrà un aspetto simile al seguente:

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  Se ci si connette tooa protetta cluster, è necessario anche dettagli hello tooprovide del certificato client hello da hello archivio locale toobe utilizzato per l'autenticazione. Per ulteriori informazioni, vedere [cluster di Service Fabric configurazione connessioni protette tooa](service-fabric-visualstudio-configure-secure-connections.md).

  Una volta configurato il profilo di pubblicazione, è possibile farvi riferimento in hello pubblicare la finestra di dialogo come illustrato di seguito.

  ![Nuovo profilo di pubblicazione nella finestra di dialogo di pubblicazione][4]

  Si noti che in questo caso, hello nuovo profilo di pubblicazione punta tooone hello predefinito parametro dei file dell'applicazione. Questo comportamento è appropriato se si desidera toopublish hello stesso numero di tooa di configurazione di applicazione degli ambienti. Al contrario, nei casi in cui si desidera toohave configurazioni diverse per ogni ambiente che si desidera toopublish a, sarebbe più utile toocreate un file di parametro dell'applicazione corrispondente.

## <a name="next-steps"></a>Passaggi successivi
processo di pubblicazione hello tooautomate in un ambiente di integrazione continua, vedere toolearn [configurare l'integrazione continua di Service Fabric](service-fabric-set-up-continuous-integration.md).

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
