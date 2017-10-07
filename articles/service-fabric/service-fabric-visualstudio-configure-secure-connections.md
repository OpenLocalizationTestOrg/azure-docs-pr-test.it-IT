---
title: aaaConfigure secure Azure Service Fabric connessioni cluster | Documenti Microsoft
description: Informazioni su come usare toouse Visual Studio tooconfigure proteggere le connessioni che sono supportate dal cluster di Azure Service Fabric hello.
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a>Configurare i cluster di Service Fabric tooa connessioni protette da Visual Studio
Informazioni su come toouse Visual Studio toosecurely accedere a un cluster di Azure Service Fabric con i criteri di controllo di accesso configurati.

## <a name="cluster-connection-types"></a>Tipi di connessione del cluster
Sono supportati due tipi di connessioni per il cluster di Azure Service Fabric hello: **non sicure** connessioni e **basata sui certificati x509** connessioni protette. Per i cluster di Service Fabric ospitati in locale, sono supportate anche le autenticazioni **Windows** e **dSTS**. È il tipo di connessione tooconfigure hello cluster quando viene creato il cluster hello. Dopo averla creata, non è possibile modificare il tipo di connessione hello.

strumenti di Visual Studio Service Fabric Hello supportano tutti i tipi di autenticazione per la connessione tooa cluster per la pubblicazione. Vedere [impostazione di un cluster di Service Fabric dal portale di Azure hello](service-fabric-cluster-creation-via-portal.md) per istruzioni su come tooset di un cluster di Service Fabric sicura.

## <a name="configure-cluster-connections-in-publish-profiles"></a>Configurare le connessioni del cluster in profili di pubblicazione
Se si pubblica un progetto di infrastruttura di servizio da Visual Studio, usare hello **pubblicare l'applicazione di Service Fabric** della finestra di dialogo toochoose un cluster di Azure Service Fabric. In **Endpoint connessione** selezionare un cluster esistente nella sottoscrizione.

![Hello * * la finestra di dialogo Pubblica servizio Fabric applicazione * * è tooconfigure utilizzata una connessione di Service Fabric.][publishdialog]

Hello **pubblicare l'applicazione di Service Fabric** la finestra di dialogo connessione cluster hello viene convalidato automaticamente. Se richiesto, accedere tooyour account Azure. Se la convalida viene eseguita, significa che il sistema disponga di hello corretto tooconnect toohello cluster installati in modo sicuro i certificati o il cluster è non sicure. Errori di convalida possono essere causati da problemi di rete o senza che sia il cluster protetto di tooconnect tooa sistema configurato correttamente.

![Hello * * pubblicare servizi dell'infrastruttura dell'applicazione * * la finestra di dialogo Convalida un oggetto esistente, configurato correttamente la connessione di cluster Service Fabric.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a>tooconnect tooa sicura cluster
1. Verificare che sia possibile accedere a uno dei certificati client hello hello trust tra cluster di destinazione. certificato di Hello in genere viene condiviso un file di scambio di informazioni personali (PFX). Vedere [impostazione di un cluster di Service Fabric dal portale di Azure hello](service-fabric-cluster-creation-via-portal.md) per la modalità di accesso client tooa tooconfigure hello server toogrant.
2. Installare il certificato attendibile di hello. toodo, fare doppio clic sul file con estensione pfx hello o utilizzare hello PowerShell script Import-PfxCertificate tooimport hello certificati. Installare il certificato di hello troppo**Cert: \LocalMachine\My**. È OK tooaccept tutte le impostazioni predefinite durante l'importazione del certificato hello.
3. Scegliere hello **pubblica...**  comando dal menu di scelta rapida hello di hello di hello progetto tooopen **pubblica l'applicazione Azure** la finestra di dialogo e i cluster di destinazione selezionare hello. strumento Hello automaticamente risolve connessione hello e Salva i parametri in hello pubblicano la connessione sicura hello profilo.
4. Facoltativo: È possibile modificare hello pubblicare profilo toospecify una connessione protetta del cluster.
   
   Poiché si sta modificando manualmente le informazioni di certificato hello toospecify file XML del profilo di pubblicazione hello, nome dell'archivio certificati toonote hello assicurarsi, archiviare, posizione e identificazione personale del certificato. È necessario tooprovide questi valori per l'archivio del certificato hello nome e percorso dell'archivio. Vedere [procedura: recuperare hello identificazione personale del certificato](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) per ulteriori informazioni.
   
   È possibile utilizzare hello *ClusterConnectionParameters* parametri toospecify hello PowerShell parametri toouse quando ci si connette il cluster di Service Fabric toohello. I parametri validi sono quelli che sono accettati dal cmdlet Connect-ServiceFabricCluster hello. Per un elenco dei parametri disponibili, vedere [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) .
   
   Se si pubblica tooa remota del cluster, è necessario parametri di toospecify hello appropriati per tale cluster specifico. Hello Ecco un esempio di connessione tooa non sicure cluster:
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   Di seguito è riportato un esempio di connessione tooan x509 basata sui certificati cluster sicuro:
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. Modificare altre impostazioni necessarie, ad esempio i parametri di aggiornamento e il percorso di file di parametro dell'applicazione e quindi pubblicare l'applicazione da hello **pubblicare l'applicazione di Service Fabric** nella finestra di dialogo di Visual Studio.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'accesso ai cluster di Infrastruttura di servizi, vedere l'articolo relativo a come [visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
