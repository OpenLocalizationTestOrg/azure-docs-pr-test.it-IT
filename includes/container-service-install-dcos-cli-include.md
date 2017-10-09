---
title: hello aaaInstall CLI di controller di dominio o del sistema operativo | Documenti Microsoft
description: Installare hello CLI di controller di dominio o del sistema operativo.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, Micro-Service, controller di dominio/sistema operativo, Azure
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> Questa procedura è necessaria per l'uso di cluster ACS basati su controller di dominio/sistema operativo. Non è alcuna necessità toodo questo per i cluster basato su sciame ACS.
> 
> 

Prima di tutto, [connettersi cluster basato su controller di dominio/OS ACS tooyour](../articles/container-service/container-service-connect.md). Dopo aver eseguito questo, è possibile installare hello CLI di controller di dominio o del sistema operativo del computer client con comandi hello riportati di seguito:

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Se si usa una versione precedente di Python, è possibile che vengano visualizzati avvisi di tipo "InsecurePlatformWarnings". È possibile ignorare questi avvisi.

In ordine tooget avviato senza dover riavviare la shell, eseguire:

```bash
source ~/.bashrc
```

Questo passaggio non sarà necessario quando si avviano nuove shell.

È ora possibile verificare tale hello che CLI è installato:

```bash
dcos --help
```