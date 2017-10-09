---
title: aaaApplication o servizio maratona specifiche dell'utente | Documenti Microsoft
description: Creare un servizio Marathon specifico per un'applicazione o un'utente
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, Marathon, Micro-Service, controller di dominio/sistema operativo, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Creare un servizio Marathon specifico per un'applicazione o un'utente
Il servizio contenitore di Azure fornisce un set di server master in cui vengono preconfigurati Apache Mesos e Marathon. Possono essere utilizzati tooorchestrate le applicazioni in cluster hello, ma ottimale non toouse hello server master a questo scopo. Ad esempio, modifiche di configurazione hello di maratona richiede accesso al server master di hello stessi e per apportare modifiche, questa incoraggia univoco server master che sono leggermente diversi hello standard e toobe necessità di e gestito in modo indipendente. Inoltre, configurazione hello richiesto da un team potrebbe non essere ottimale hello per un altro team.

In questo articolo verrà illustrato come tooadd un servizio maratona specifico dell'utente o applicazione.

Poiché questo servizio apparterrà tooa singolo utente o del team, sono tooconfigure disponibile in alcun modo che lo desiderano. Inoltre, il servizio contenitore di Azure verrà garantire il funzionamento di un servizio hello toorun. Se il servizio di hello non riesce, il servizio contenitore di Azure verrà viene riavviato. La maggior parte del tempo di hello non anche noterai che aveva i tempi di inattività.

## <a name="prerequisites"></a>Prerequisiti
[Distribuire un'istanza del servizio di contenitore di Azure di](container-service-deployment.md) con orchestrator digitare DC/OS e [assicurarsi che i client possano connettersi cluster tooyour](../container-service-connect.md). Inoltre, hello i passaggi seguenti.

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Creare un servizio Marathon specifico per un'applicazione o un'utente
Iniziare creando un file di configurazione JSON che definisce il nome di hello del servizio di applicazione hello che si desidera toocreate. Nell'esempio si utilizza `marathon-alice` come nome di framework hello. Salvare il file di hello come `marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

Successivamente, utilizzare l'istanza maratona di hello DC/OS CLI tooinstall hello con le opzioni hello impostate nel file di configurazione:

```bash
dcos package install --options=marathon-alice.json marathon
```

Verrà visualizzato il `marathon-alice` servizio in esecuzione nella scheda Servizi hello dell'interfaccia utente controller di dominio o del sistema operativo. Hello dell'interfaccia utente sarà `http://<hostname>/service/marathon-alice/` se si desidera tooaccess è direttamente.

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a>Impostare hello DC/OS CLI tooaccess servizio hello
È possibile facoltativamente configurare tooaccess il controller di dominio/OS CLI questo nuovo servizio impostazione hello `marathon.url` proprietà toopoint toohello `marathon-alice` istanza come indicato di seguito:

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

È possibile verificare quale istanza di maratona in cui viene usata l'interfaccia CLI con hello `dcos config show` comando. È possibile ripristinare il master del servizio maratona con il comando hello toousing `dcos config unset marathon.url`.

