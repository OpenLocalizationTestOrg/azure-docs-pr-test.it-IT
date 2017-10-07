---
title: aaaGetting avviato con il Cloud in Microsoft Azure | Documenti Microsoft
description: Eseguire OSS o Pivotal Cloud Foundry in Microsoft Azure
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Cloud Foundry in Azure

Cloud Foundry è una piattaforma distribuita come servizio (PaaS) open source per la compilazione, la distribuzione e l'uso di applicazioni a 12 fattori sviluppate in una vasta gamma di linguaggi e framework. Questo documento descrive le opzioni di hello che è per l'esecuzione Foundry Cloud in Azure e come è possibile iniziare.

## <a name="cloud-foundry-offerings"></a>Offerte Cloud Foundry

Esistono due forme di Cloud Foundry toorun disponibile in Azure: Cloud Foundry (OSS CF) open source e fondamentale Cloud Foundry (PCF). CF OSS è un interamente [open source](https://github.com/cloudfoundry) versione Foundry Cloud gestito da hello Foundation Foundry Cloud. Foundry Cloud fondamentale è una distribuzione aziendale di Cloud Foundry da fondamentale Software Inc. Verranno esaminate alcune delle differenze di hello tra due offerte hello.

### <a name="open-source-cloud-foundry"></a>Open-Source Cloud Foundry

È possibile distribuire i sistemi operativi Cloud Foundry in Azure prima distribuzione director BOSH e quindi distribuendo Foundry Cloud, utilizzando hello [istruzioni fornite in GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md). toolearn ulteriori informazioni sull'utilizzo di OSS CF, vedere hello [documentazione](https://docs.cloudfoundry.org/) fornito da hello Foundation Foundry Cloud.

Microsoft fornisce il supporto di sforzo per OSS CF tramite hello seguendo i canali della community:

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>Canale bosh-azure-cpi in [Cloud Foundry Slack](https://slack.cloudfoundry.org/)
- [Lista di distribuzione cf-bosh](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- Problemi di GitHub per hello [IPC](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) e [broker di servizio](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> livello di Hello del supporto per le risorse di Azure, ad esempio hello le macchine virtuali in cui viene eseguito il Cloud, è basato sul contratto di supporto tecnico di Azure. Supporto della community di sforzo solo componenti toohello Foundry specifiche del Cloud.

### <a name="pivotal-cloud-foundry"></a>Pivotal Cloud Foundry

Fondamentale Foundry Cloud include hello stessa piattaforma di base come distribuzione hello OSS, insieme a un set di strumenti di gestione proprietario e del supporto aziendale. toorun PCF in Azure, è necessario acquistare una licenza da Pivotal. offerta PCF Hello da hello Azure marketplace include una licenza di valutazione di 90 giorni.

gli strumenti di Hello includono [fondamentale Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), un'applicazione web che semplifica la distribuzione e gestione di base, il Cloud e [fondamentale Manager di app](https://docs.pivotal.io/pivotalcf/console/), un'applicazione web per la gestione gli utenti e applicazioni.

Inoltre toohello canali di supporto per CF di sistemi operativi sopra elencati, un PCF licenza si toocontact Pivotal per il supporto. Microsoft e Pivotal stato attivato il supporto dei flussi di lavoro che consentono di toocontact delle parti di assistenza e sono le richieste indirizzate in modo appropriato a seconda di dove si trova il problema di hello.

## <a name="azure-service-broker"></a>Service Broker di Azure

Cloud Foundry incoraggia hello ["dodici fattore app"](https://12factor.net/) metodologia, che favorisce una netta separazione tra i processi dell'applicazione senza stato e il backup di servizi con informazioni sullo stato. [Service Broker](https://docs.cloudfoundry.org/services/api.html) offrono tooprovision un sistema coerente e associare tooapplications di servizi di backup. Hello [broker servizio Azure](https://github.com/Azure/meta-azure-service-broker) fornisce alcune hello chiavi servizi Azure tramite il canale, inclusa l'archiviazione di Azure e SQL Azure.

Se si utilizza Foundry Cloud fondamentale, hello service broker è stata è anche [disponibile sotto forma di riquadro](https://docs.pivotal.io/azure-sb/installing.html) da hello rete centrale.

## <a name="related-resources"></a>Risorse correlate

### <a name="visual-studio-team-services-plugin"></a>Plug-in di Visual Studio Team Services

Cloud Foundry è lo sviluppo di software tooagile adatto, tra cui utilizzo hello di integrazione continua (CI) e il recapito continuo (CD). Se si utilizzano Visual Studio Team Services (VSTS) toomanage i progetti e si desidera tooset di una pipeline CI/CD Foundry Cloud di destinazione, è possibile utilizzare hello [VSTS Cloud Foundry compilare estensione](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension). rende semplice tooconfigure Hello plug-in e automatizzare le distribuzioni tooCloud Foundry, se in esecuzione in Azure o in un altro ambiente.

## <a name="next-steps"></a>Passaggi successivi

- [Distribuzione centrale Foundry Cloud da hello Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [Distribuire un tooCloud app Foundry in Azure](./cloudfoundry-deploy-your-first-app.md)
