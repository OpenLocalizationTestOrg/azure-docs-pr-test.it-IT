---
title: aaaUnderstand e risolvere gli errori di WebHCat in HDInsight - Azure | Documenti Microsoft
description: "Informazioni su come gli errori più comuni di tooabout restituito da WebHCat in HDInsight e come tooresolve li."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>Comprendere e risolvere gli errori ricevuti da WebHCat in HDInsight

Informazioni sugli errori ricevuti quando si utilizza WebHCat con HDInsight e come tooresolve li. WebHCat viene utilizzata internamente dagli strumenti sul lato client, ad esempio Azure PowerShell e hello Data Lake Tools per Visual Studio.

## <a name="what-is-webhcat"></a>Che cos'è WebHCat

[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) è un'API REST per [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), un livello di gestione tabelle e risorse di archiviazione per Hadoop. WebHCat è abilitata per impostazione predefinita nei cluster HDInsight e viene utilizzato dai processi di toosubmit vari strumenti, ottenere lo stato del processo e così via senza registrazione toohello cluster.

## <a name="modifying-configuration"></a>Modifica della configurazione

> [!IMPORTANT]
> Numerosi errori hello elencati in questo documento si verificano perché è stato superato un numero massimo configurato. Quando la procedura di risoluzione hello viene indicato che è possibile modificare un valore, è necessario utilizzare uno di seguito modifica hello tooperform hello:

* Per **Windows** cluster: usare un valore di hello tooconfigure azione script durante la creazione del cluster. Per altre informazioni, vedere [Sviluppare azioni di script](hdinsight-hadoop-script-actions.md).

* Per **Linux** cluster: valore di hello toomodify utilizzare Ambari (web o l'API REST). Per altre informazioni, vedere [Gestire HDInsight tramite Ambari](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="default-configuration"></a>Configurazione predefinita

Se viene superato hello seguente i valori predefiniti, può influire negativamente sulle prestazioni WebHCat o causare errori:

| Impostazione | Risultato | Valore predefinito |
| --- | --- | --- |
| [yarn.scheduler.capacity.maximum-applications][maximum-applications] |numero massimo di processi che possono essere attive contemporaneamente Hello (in sospeso o in esecuzione) |10.000 |
| [templeton.exec.max-procs][max-procs] |numero massimo di Hello di richieste che possono essere serviti contemporaneamente |20 |
| [mapreduce.jobhistory.max-age-ms][max-age-ms] |Hello numero di giorni per cui la cronologia dei processi di conservazione |7 giorni |

## <a name="too-many-requests"></a>Numero eccessivo di richieste

**Codice di stato HTTP**: 429

| Causa | Risoluzione |
| --- | --- |
| È stato superato hello massimo di richieste simultanee gestite da WebHCat al minuto (impostazione predefinita 20) |Ridurre tooensure il carico di lavoro che non presenta più di hello numero massimo di richieste simultanee o aumentare il limite di richieste simultanee hello modificando `templeton.exec.max-procs`. Per altre informazioni, vedere [Modifica della configurazione](#modifying-configuration) |

## <a name="server-unavailable"></a>Server non disponibile

**Codice di stato HTTP**: 503

| Causa | Risoluzione |
| --- | --- |
| Questo codice di stato si verifica in genere durante il failover tra hello primari e secondari nodo head per cluster hello |Attendere due minuti, quindi ripetere l'operazione di hello |

## <a name="bad-request-content-could-not-find-job"></a>Contenuto richiesta non valido: impossibile trovare il processo

**Codice di stato HTTP**: 400

| Causa | Risoluzione |
| --- | --- |
| I dettagli dei processi sono stati rimossi in base alla cronologia processo hello pulitura |periodo di memorizzazione Hello predefinito per la cronologia processo è 7 giorni. periodo di memorizzazione predefinito Hello può essere cambiato modificando `mapreduce.jobhistory.max-age-ms`. Per altre informazioni, vedere [Modifica della configurazione](#modifying-configuration) |
| Processo è stato terminato a causa di failover tooa |Ripetere l'invio di processi di backup tootwo minuti |
| È stato utilizzato un ID processo non valido |Controllare se l'id di processo hello è corretto |

## <a name="bad-gateway"></a>Gateway non valido

**Codice di stato HTTP**: 502

| Causa | Risoluzione |
| --- | --- |
| Interno operazione di garbage collection in hello WebHCat processo |Attendere che l'operazione di garbage collection toofinish o riavviare servizio WebHCat hello |
| Timeout in attesa di una risposta dal servizio ResourceManager hello. Questo errore può verificarsi quando il numero di hello delle applicazioni attive esce massimo configurato di hello (impostazione predefinita a 10.000) |Attende attualmente in esecuzione processi toocomplete o aumentare il limite di processi simultanei di hello modificando `yarn.scheduler.capacity.maximum-applications`. Per ulteriori informazioni, vedere hello [Modifica configurazione](#modifying-configuration) sezione. |
| Il tentativo di tutti i processi tramite hello tooretrieve [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) chiamata durante `Fields` è troppo`*` |Non recuperare i dettagli di *tutti* i processi. Usare invece `jobid` tooretrieve dettagli per i processi di maggiori solo a determinati id di processo. Oppure, non utilizzare `Fields` |
| servizio WebHCat Hello è inattivo durante il failover del nodo head |Attendere per due minuti e ripetere l'operazione hello |
| Sono presenti più di 500 processi in sospeso inviati tramite WebHCat |Attendere il completamento dei processi attualmente in sospeso prima di inviare altri processi |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
