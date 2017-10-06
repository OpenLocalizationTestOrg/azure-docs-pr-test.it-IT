---
title: dati aaaSample in Azure contenitori, SQL Server, blob e tabelle Hive | Documenti Microsoft
description: "Modalità di archiviazione in vari enviromnents Azure tooexplore dati."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Campionare i dati in contenitori BLOB di Azure, SQL Server e nelle tabelle Hive
Questo documento collega tootopics che illustra come toosample i dati archiviati in uno dei tre percorsi diversi di Azure:

* **I dati del contenitore BLOB di Azure** vengono campionati scaricandoli a livello di programmazione ed eseguendo il successivo campionamento usando un codice Python di esempio.
* **Dati di SQL Server** campionato utilizzando il linguaggio di programmazione Python hello e SQL. 
* **Dati della tabella hive** vengono campionati utilizzando le query Hive.

esempio Hello **menu** collegamenti toohello argomenti che descrivono come dati toosample da ognuno di questi ambienti di archiviazione di Azure. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

Questa attività di campionamento è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

**Perché campionare i dati?**

Se si prevede di tooanalyze set di dati hello è grande, è in genere un tooreduce di dati di buona toodown esempio hello è tooa più piccolo ma rappresentativo e gestibile dimensioni. Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità. Il relativo ruolo nel processo di Cortana Analitica hello è tooenable rapida la creazione di prototipi di funzioni di elaborazione dei dati hello e modelli di machine learning.

