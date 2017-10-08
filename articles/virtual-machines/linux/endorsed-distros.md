---
title: aaaEndorsed distribuzioni di Linux | Documenti Microsoft
description: Informazioni sulle distribuzioni di Linux approvate in Azure, che includono le linee guida per Ubuntu, CentOS, Oracle e SUSE.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f006972d4611434c62b72a1d8df60caf753e15f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Linux in distribuzioni approvate da Azure
Partner di forniscono immagini Linux in hello Azure Marketplace. Stiamo lavorando con vari Linux community tooadd anche altre versioni toohello approvate lista di distribuzione. In hello frattempo per distribuzioni che non sono disponibili da hello Marketplace, è possibile sempre fare proprie Linux seguendo le istruzioni di hello in [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo di Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>Distribuzioni e versioni supportate
Hello nella tabella seguente sono elencate le distribuzioni di Linux hello e le versioni supportate in Azure. Fare riferimento troppo[immagini di supporto per Linux in Microsoft Azure](https://support.microsoft.com/en-us/kb/2941892) per informazioni più dettagliate.

i driver di Hello Linux Integration Services (LIS) per Hyper-V e Azure sono moduli di kernel Microsoft contribuisce direttamente kernel Linux upstream toohello.  Alcuni driver LIS sono integrate in kernel della distribuzione hello per impostazione predefinita. Le distribuzioni precedenti basate su Red Hat Enterprise (RHEL)/CentOS sono disponibili come download separato in [Linux Integration Services versione 4.1 per Hyper-V](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409). Vedere [requisiti kernel Linux](create-upload-generic.md#linux-kernel-requirements) per ulteriori informazioni sui driver LIS hello.

Hello agente Linux di Azure è già pre-installato nelle immagini di Azure Marketplace hello e in genere è disponibile dal repository di pacchetti di distribuzione hello. Il codice sorgente è disponibile su [GitHub](https://github.com/azure/walinuxagent).

| Distribuzione | Versione | Driver | Agente |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3+, 7.0+ |CentOS 6.3: [download LIS](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4 +: nel kernel |Pacchetto: in [repo](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/) sotto "WALinuxAgent" <br/>Codice sorgente: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |Nel kernel |Codice sorgente: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7,9 +, 8.2 + |Nel kernel |Pacchetto: in repo sotto "waagent" <br/>Codice sorgente: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |Nel kernel |Pacchetto: in repo sotto "WALinuxAgent" <br/>Codice sorgente: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux. |RHEL 6.7+, 7.1+ |Nel kernel |Pacchetto: in repo sotto "WALinuxAgent" <br/>Codice sorgente: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES per SAP<br>11 SP4<br>12 SP1+|Nel kernel |Pacchetto:<p> per 11 in [Cloud: strumenti](https://build.opensuse.org/project/show/Cloud:Tools) archivio<br>per 12 inclusi nel modulo "Cloud pubblico" in "python-azure-agent"<br/>Codice sorgente: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.1+ |Nel kernel |Pacchetto: in repository [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) sotto "python-azure-agent" <br/>Codice sorgente: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16.10 |Nel kernel |Pacchetto: in repo sotto "WALinuxAgent" <br/>Codice sorgente: [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>Partner

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

Dal sito Web CoreOS hello:

*CoreOS è progettato per la protezione, l’uniformità e l’affidabilità. Anziché installare i pacchetti tramite yum o apt, CoreOS utilizza toomanage contenitori di Linux i servizi di livello superiore di astrazione. Il codice di un servizio singolo e tutte le dipendenze vengono inserite in un contenitore che può essere eseguito su uno o più macchine CoreOS.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ è una società di servizi che è progettato per lo sviluppo di hello e implementazione di soluzioni professionali tramite software gratuito e di consulenza indipendenti. Come azienda leader nell'open source, Credativ ha ottenuto un riconoscimento internazionale, con molti reparti IT che ricorrono ai suoi servizi di assistenza. In collaborazione con Microsoft, Credativ sta attualmente preparando immagini Debian corrispondenti per Debian 8 (Jessie) e Debian precedente a 7 (Wheezy). Entrambe le immagini sono appositamente progettati toorun in Azure e possono essere facilmente gestite tramite platform hello. Credativ supporteranno manutenzione a lungo termine hello e l'aggiornamento delle immagini Debian hello per Azure tramite il relativo centri di supporto di origine aprire.

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Strategia di Oracle è toooffer un ampio portafoglio di soluzioni per cloud pubblici e privati. strategia di Hello offre ai clienti scelta e la flessibilità nella modalità distribuzione software Oracle in cloud di Oracle e altri cloud. Partnership di Oracle con Microsoft consente il software Oracle toodeploy clienti in cloud pubblici e privati di Microsoft con confidenza hello di certificazione e di supporto da Oracle.  L'impegno e gli investimenti di Oracle in ambito di soluzioni per cloud Oracle pubblico e privato rimangono invariati.

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/strategic-Alliance/Microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

salve fornitore mondiale di soluzioni open source, Red Hat più del 90% di aziende classificate Fortune 500 consente di risolvere le problematiche di business, allineare IT e strategie di business e la preparazione per il futuro hello della tecnologia. Per raggiungere questi obiettivi, Red Hat fornisce soluzioni sicure tramite un modello di business aperto e uno schema di sottoscrizioni conveniente e prevedibile.

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server su Azure è una piattaforma collaudata che offre un'affidabilità e una sicurezza superiori per il cloud computing. Piattaforma Linux versatile del SUSE si integra perfettamente con toodeliver di servizi cloud di Azure un ambiente cloud facilmente gestibile. Con le applicazioni certificate più 9,200 oltre 1800 fornitori di software indipendenti per SUSE Linux Enterprise Server, SUSE assicura che i carichi di lavoro eseguito supportati in hello data center può essere distribuiti con fiducia in Azure.

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

Le competenze di Canonical in ambito di engineering e le regole di governance della community aperta sono alla base del successo di Ubuntu nelle tecnologie per client, server e cloud computing, inclusi servizi cloud personali per i consumatori. La visione del Canonical di una piattaforma unificata, disponibile in Ubuntu, dal telefono toocloud, fornisce una famiglia di interfacce coerente per hello telefono, tablet, TV e desktop. Questo obiettivo rende la prima scelta hello Ubuntu per istituzioni diverse da responsabili toohello i provider di cloud pubblico di consumo e preferito tra singoli tecnici.

Con gli sviluppatori ed engineering Center tutto il mondo hello, Canonical è posizionato in modo univoco toopartner con i produttori di hardware, i provider di contenuti e toomarket software sviluppatori toobring Ubuntu soluzioni per i PC, server e dispositivi palmari.
