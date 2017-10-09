---
title: aaaViewing e modifica i nomi host | Documenti Microsoft
description: Come tooview e modificare nomi host per macchine virtuali di Azure, web e ruoli di lavoro per la risoluzione dei nomi
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>Visualizzazione e modifica di nomi host
tooallow toobe di istanze del ruolo a cui fa riferimento il nome host, è necessario impostare il valore di hello per nome host hello nel file di configurazione di servizio hello per ogni ruolo. A tale scopo, aggiungere toohello di nome host desiderato hello **vmName** attributo di hello **ruolo** elemento. valore di hello Hello **vmName** attributo viene utilizzato come base per il nome host hello di ogni istanza del ruolo. Ad esempio, se **vmName** è *webrole* e sono disponibili tre istanze del ruolo, i nomi host hello di istanze di hello saranno *webrole0*, *webrole1* , e *webrole2*. Non è necessario un nome host per le macchine virtuali nel file di configurazione hello toospecify perché il nome host hello per una macchina virtuale viene popolato in base al nome di macchina virtuale hello. Per altre informazioni sulla configurazione di un servizio di Microsoft Azure, vedere [Schema di configurazione dei servizi di Azure (file .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>Visualizzazione dei nomi host
È possibile visualizzare i nomi host hello delle macchine virtuali e istanze del ruolo in un servizio cloud utilizzando gli strumenti di hello indicati di seguito.

### <a name="azure-portal"></a>Portale di Azure
È possibile utilizzare hello [portale di Azure](http://portal.azure.com) nomi di host tooview hello per le macchine virtuali nel pannello della panoramica hello per una macchina virtuale. Tenere presente che hello pannello viene visualizzato il valore per **nome** e **nome Host**. Sebbene siano inizialmente hello stesso, la modifica del nome host hello non verrà modificato il nome di hello della macchina virtuale hello o istanza del ruolo.

Le istanze del ruolo possono essere visualizzate anche nel portale di Azure hello, ma quando si elencano le istanze di hello in un servizio cloud, il nome host hello non viene visualizzato. Verrà visualizzato un nome per ogni istanza, ma tale nome non rappresenta il nome host hello.

### <a name="service-configuration-file"></a>File di configurazione del servizio
È possibile scaricare i file di configurazione del servizio di hello per un servizio distribuito dalla hello **configura** pannello del servizio hello hello portale di Azure. È quindi possibile cercare hello **vmName** attributo per hello **nome ruolo** nome host dell'elemento toosee hello. Tenere presente che questo nome host viene utilizzato come base per il nome host hello di ogni istanza del ruolo. Ad esempio, se **vmName** è *webrole* e sono disponibili tre istanze del ruolo, i nomi host hello di istanze di hello saranno *webrole0*, *webrole1* , e *webrole2*.

### <a name="remote-desktop"></a>Desktop remoto
Dopo aver abilitato Desktop remoto (Windows), comunicazione remota di Windows PowerShell (Windows), o le macchine virtuali tooyour connessioni SSH (Linux e Windows) o le istanze del ruolo, è possibile visualizzare il nome host hello da una connessione attiva di Desktop remoto in vari modi:

* Al prompt dei comandi di hello o al terminale SSH, digitare il nome host.
* Digitare ipconfig/tutti i comandi di hello richiesto (solo Windows).
* Nome della visualizzazione hello computer nel sistema hello impostazioni (solo Windows).

### <a name="azure-service-management-rest-api"></a>API REST di gestione dei servizi di Azure
Da un client REST, seguire queste istruzioni:

1. Assicurarsi di aver toohello di tooconnect un certificato client portale di Azure. tooobtain un certificato client, seguire i passaggi di hello presentati in [come: informazioni sul Download e importazione delle impostazioni di pubblicazione e sottoscrizione](https://msdn.microsoft.com/library/dn385850.aspx). 
2. Impostare una voce di intestazione denominata x-ms-version con un valore di 2013-11-01.
3. Inviare una richiesta nel seguente formato hello: https://management.core.windows.net/\<annullamento della sottoscrizione dell'id\>/services/hostedservices/\<-nome del servizio\>? dettaglio incorporare = true
4. Cercare hello **HostName** per ogni elemento **RoleInstance** elemento.

> [!WARNING]
> È inoltre possibile visualizzare il suffisso di dominio interno hello per il servizio cloud da hello risposta chiamata REST selezionando hello **InternalDnsSuffix** elemento, o eseguendo ipconfig/da un prompt dei comandi in una sessione di Desktop remoto (Windows) o /etc/resolv.conf cat in esecuzione da un terminale SSH (Linux).
> 
> 

## <a name="modifying-a-hostname"></a>Modifica di un nome host
È possibile modificare il nome host hello per qualsiasi macchina virtuale o istanza del ruolo caricando un file di configurazione del servizio modificato o rinominando computer hello da una sessione Desktop remoto.

## <a name="next-steps"></a>Passaggi successivi
[Risoluzione del nome (DSN)](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Schema di configurazione dei servizi di Azure (file .cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Attività di configurazione di Rete virtuale di Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Specificare le impostazioni DNS tramite i file di configurazione di rete](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

