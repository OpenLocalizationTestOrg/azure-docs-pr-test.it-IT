---
title: indirizzi di gestione dell'ambiente del servizio App aaaAzure
description: Gli indirizzi di gestione di elenchi hello utilizzati toocommand un ambiente del servizio App
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a>Indirizzi di gestione dell'Ambiente del servizio app

Hello Environment(ASE) di servizio App è una distribuzione di hello servizio App di Azure in una subnet nella rete virtuale di Azure (VNet).  Hello ASE deve essere accessibile da hello Azure App Service in modo che possa essere gestito.  Il traffico di gestione di ASE attraversa rete controllata dall'utente hello.  Proviene da Azure App Service management server toohello VIP pubblico associato ASE hello.  Per informazioni dettagliate su hello ASE rete di dipendenze leggere [rete hello ambiente del servizio App e considerazioni sulla][networking].  Per informazioni generali su ASE hello è possibile iniziare con [toohello introduzione ambiente del servizio App][intro].

Questo documento vengono elencati gli IP di origine hello per gestione traffico toohello ASE. È possibile utilizzare questi toolock di gruppi di sicurezza di rete toocreate indirizzi il traffico in ingresso verso il basso o utilizzare in tabelle di routing in base alle esigenze.  toouse queste informazioni è necessario toouse:

* indirizzi IP Hello elencati per tutte le aree
* area che viene distribuito il ASE in toohello corrispondenza di indirizzi IP di Hello.

traffico di gestione Hello in arrivo provenienti da questi indirizzi IP tooports 454 e 455.

| Region | Indirizzi |
|--------|-----------|
| Tutte le aree | 70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141 |
| Stati Uniti centro-meridionali e Stati Uniti centro-settentrionali | 23.102.188.65, 191.236.154.88 |
| Australia sudorientale e Australia orientale | 23.101.234.41, 104.210.90.65 |
| Stati Uniti occidentali e Stati Uniti orientali | 104.45.227.37, 191.236.60.72 |
| Europa occidentale ed Europa settentrionale | 191.233.94.45, 191.237.222.191 |
| Stati Uniti centro-occidentali e Stati Uniti occidentali 2 | 13.78.148.75, 13.66.225.188 |
| Stati Uniti centrali e Stati Uniti orientali 2 | 104.43.165.73, 104.46.108.135 |
| Asia orientale e Asia sudorientale | 23.99.115.5, 104.215.158.33 |
| Giappone orientale e Giappone occidentale | 104.41.185.116, 191.239.104.48 |
| Canada centrale e Canada orientale | 40.85.230.101, 40.86.229.100 |
| Regno Unito occidentale e Regno Unito meridionale | 51.141.8.34, 51.140.185.75 |
| Corea meridionale e Corea centrale | 52.231.200.177, 52.231.32.117 |
| Brasile meridionale e Stati Uniti centro-meridionali| 104.41.46.178, 23.102.188.65 |
| India centrale e India meridionale | 104.211.98.24, 104.211.225.66 |
| India occidentale e India meridionale | 104.211.160.229, 104.211.225.66 |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
