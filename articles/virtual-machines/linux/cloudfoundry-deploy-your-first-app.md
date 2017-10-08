---
title: aaaDeploy il primo tooCloud app Foundry in Microsoft Azure | Documenti Microsoft
description: Distribuire un tooCloud applicazione Foundry in Azure
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>Distribuire il primo tooCloud app Foundry in Microsoft Azure

[Cloud Foundry](http://cloudfoundry.org) è una popolare piattaforma di applicazioni open source disponibile in Microsoft Azure. In questo articolo viene illustrata la modalità toodeploy e gestire un'applicazione in Cloud Foundry in un ambiente Azure.

## <a name="create-a-cloud-foundry-environment"></a>Creare un ambiente Cloud Foundry

Esistono diverse opzioni per la creazione di un ambiente Cloud Foundry in Azure:

- Hello utilizzare [offerta Foundry Cloud fondamentale] [ pcf-azuremarketplace] in hello Azure Marketplace toocreate un ambiente standard che include PCF Operations Manager e hello Azure Service Broker. È possibile trovare [le istruzioni per] [ pcf-azuremarketplace-pivotaldocs] offrire hello documentazione fondamentale per la distribuzione di marketplace hello.
- Creare un ambiente personalizzato [distribuendo manualmente Pivotal Cloud Foundry][pcf-custom].
- [Distribuire i pacchetti di hello open-source Foundry Cloud direttamente] [ oss-cf-bosh] impostando un [BOSH](http://bosh.io) director, una macchina virtuale che coordina distribuzione hello dell'ambiente Cloud Foundry hello.

> [!IMPORTANT] 
> Se si distribuisce PCF hello Azure Marketplace, prendere nota di hello SYSTEMDOMAINURL e richieste di credenziali di amministratore hello tooaccess hello fondamentale Manager di App, di cui sono descritti nella Guida alla distribuzione di hello marketplace. Essi è toocomplete necessari in questa esercitazione. Per le distribuzioni di marketplace, hello SYSTEMDOMAINURL è https://system modulo hello. *indirizzo ip*. cf.pcfazure.com.

## <a name="connect-toohello-cloud-controller"></a>Connettersi toohello Controller del Cloud

Hello Controller del Cloud è l'ambiente di Cloud Foundry tooa punto di ingresso principale hello per la distribuzione e la gestione delle applicazioni. core Hello Cloud Controller API (CCAPI) è un'API REST, ma è accessibile attraverso vari strumenti. In questo caso, si interagire con esso tramite hello [Cloud Foundry CLI][cf-cli]. È possibile installare hello CLI su Linux, MacOS o Windows, ma se si preferisce non tooinstall affatto, è disponibile preinstallato in hello [Azure Cloud Shell][cloudshell-docs].

toolog, anteporre `api` toohello SYSTEMDOMAINURL ottenuti dalla distribuzione marketplace hello. Poiché la distribuzione di hello predefinito utilizza un certificato autofirmato, è necessario includere anche hello `skip-ssl-validation` passare.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

Si è richiesta toolog in toohello Controller del Cloud. Utilizzare le credenziali dell'account amministratore hello acquisito dalle fasi di distribuzione di hello marketplace.

Cloud Foundry fornisce *organizzazioni* e *spazi* come team hello tooisolate di spazi dei nomi e gli ambienti in una distribuzione condivisa. distribuzione di marketplace PCF Hello include predefinito hello *sistema* dell'organizzazione e un set di spazi creato toocontain i componenti di base hello, ad esempio servizio di scalabilità automatica hello e hello Azure service broker. Per il momento, scegliere hello *sistema* spazio.


## <a name="create-an-org-and-space"></a>Creare un'organizzazione e uno spazio

Se si digita `cf apps`, viene visualizzato un set di applicazioni di sistema che sono state distribuite nello spazio di sistema hello all'interno dell'organizzazione sistema hello 

È consigliabile mantenere hello *sistema* org riservato per le applicazioni di sistema, quindi creare un toohouse org e spazio l'applicazione di esempio.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Utilizzare hello destinazione comando tooswitch toohello nuova organizzazione e lo spazio:

```bash
cf target -o testorg -s dev
```

A questo punto, quando si distribuisce un'applicazione, viene automaticamente creato nello spazio e hello nuova organizzazione. tooconfirm che sono attualmente alcuna App nello spazio/hello nuova organizzazione, non tipo `cf apps` nuovamente.

> [!NOTE] 
> Per ulteriori informazioni sulle organizzazioni e gli spazi e come possono essere utilizzati per il controllo di accesso basato sui ruoli (RBAC), vedere hello [documentazione Foundry Cloud][cf-orgs-spaces-docs].

## <a name="deploy-an-application"></a>Distribuire un'applicazione

Consente di usare un'applicazione di esempio Foundry Cloud chiamata Hello Spring Cloud, che viene scritto in linguaggio e in base a hello [Spring Framework](http://spring.io) e [avvio Spring](http://projects.spring.io/spring-boot/).

### <a name="clone-hello-hello-spring-cloud-repository"></a>Clonare il repository di hello Hello Spring Cloud

applicazione di esempio Hello Spring Cloud Hello è disponibile su GitHub. Clonarla ambiente tooyour e modificare nella nuova directory hello:

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>Compilare un'applicazione hello

Compilazione hello app usando [Apache Maven](http://maven.apache.org).

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>Distribuire un'applicazione hello con cf push

È possibile distribuire la maggior parte delle applicazioni tooCloud Foundry utilizzando hello `push` comando:

```bash
cf push
```

Quando si *push* un'applicazione, Cloud Foundry rileva hello tipo di applicazione (in questo caso, un'app Java) e identifica le relative dipendenze (in questo caso, framework di primavera hello). Viene quindi inserito tutto il necessario toorun il codice in un'immagine contenitore autonomo, nota come un *droplet*. Infine, le pianificazioni di Cloud Foundry hello applicazione su uno dei computer disponibili di hello nell'ambiente in uso e crea un URL in cui è possibile raggiungerli, disponibile nell'output di hello del comando hello.

![Output del comando push cf][cf-push-output]

applicazione hello-spring-cloud hello toosee, aprire hello fornito URL nel browser:

![Interfaccia utente predefinita per Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> ulteriori informazioni su cosa accade durante toolearn `cf push`, vedere [installazione delle applicazioni] [ cf-push-docs] in hello documentazione Foundry Cloud.

## <a name="view-application-logs"></a>Visualizzare i registri applicazioni

È possibile utilizzare i log di hello Cloud Foundry CLI tooview per un'applicazione in base al nome:

```bash
cf logs hello-spring-cloud
```

Per impostazione predefinita, hello Registra comando Usa *della parte finale del*, che mostra i nuovi log man mano che vengono scritte. toosee nuovi log visualizzati, aggiornare l'applicazione hello-spring-cloud hello nel browser hello.

registri tooview che sono già stati scritti, aggiungere hello `recent` passare:

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>Applicazione hello scala

Per impostazione predefinita, `cf push` crea solo una singola istanza dell'applicazione. tooensure la disponibilità elevata e scalabilità attiva per una velocità effettiva, in genere si desidera toorun più istanze delle applicazioni. È possibile ridimensionare le applicazioni già distribuite utilizzando hello `scale` comando:

```bash
cf scale -i 2 hello-spring-cloud
```

In esecuzione hello `cf app` comando in un'applicazione hello mostra che il Cloud è la creazione di un'altra istanza di un'applicazione hello. Una volta avviata, un'applicazione hello Foundry Cloud avvia automaticamente il bilanciamento del carico del traffico tooit.


## <a name="next-steps"></a>Passaggi successivi

- [Hello lettura documentazione Cloud Foundry][cloudfoundry-docs]
- [Impostare i plug-in Visual Studio Team Services hello per Cloud Foundry][vsts-plugin]
- [Configurare hello prolunga Analitica Log di Microsoft per il Cloud][loganalytics-nozzle]

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png