---
title: aaaTroubleshoot RBAC Azure | Documenti Microsoft
description: Assistenza per problemi o domande sulle risorse del controllo degli accessi in base al ruolo.
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a>Risoluzione dei problemi del controllo degli accessi in base al ruolo

In questo articolo documento risponde alle domande comuni su hello specifici diritti di accesso che vengono concesse ai ruoli, in modo da sapere quali tooexpect quando si utilizzano ruoli nel portale di Azure hello hello e possibile risolvere i problemi di accesso. Questi tre ruoli coprono tutti i tipi di risorsa:

* Proprietario  
* Collaboratore  
* Reader  

I proprietari e i collaboratori dispongono dell'accesso completo toohello gestione esperienza, ma non è possibile assegnare un collaboratore accesso tooother utenti o gruppi. Le cose interessanti un po' più con il ruolo di lettore hello, in modo che sia in cui è necessario passare del tempo. Vedere hello [articolo avviato get Role-Based Access Control](role-based-access-control-configure.md) per informazioni dettagliate sulla modalità di accesso toogrant.

## <a name="app-service-workloads"></a>Carichi di lavoro del servizio app
### <a name="write-access-capabilities"></a>Funzionalità di accesso in scrittura
Se si concede a un'utente accesso in sola lettura tooa singolo web app, sono disabilitate alcune funzionalità che non è prevedibile. Hello seguenti funzionalità di gestione richiede **scrivere** accedere tooa web app (Collaboratore o proprietario) e non sono disponibili in qualsiasi scenario di sola lettura.

* Comandi (quali avvio, interruzione e così via)
* Modifica di impostazioni quali la configurazione generale, le impostazioni di scalabilità, di backup e di monitoraggio.
* Accesso a credenziali di pubblicazione e altri segreti, quali le impostazioni delle app e le stringhe di connessione.
* Streaming dei log
* Configurazione dei log di diagnostica
* Console (prompt dei comandi)
* Distribuzioni attive e recenti, per la distribuzione continua del Git locale
* Spesa prevista
* Test Web
* Rete virtuale (solo lettura tooa visibile se una rete virtuale è stata configurata in precedenza da un utente con accesso in scrittura).

Se non è possibile accedere a uno di questi riquadri, è necessario tooask l'amministratore per l'app web di collaboratore accesso toohello.

### <a name="dealing-with-related-resources"></a>Gestione delle risorse correlate
Le app Web sono complicate da presenza hello di alcune risorse diverse che interazione. Di seguito è illustrato un tipico gruppo di risorse con alcuni siti Web:

![Gruppo di risorse per app Web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

Di conseguenza, se si autorizza l'applicazione web di accesso toojust hello, gran parte delle funzionalità di hello nel Pannello di hello sito Web nel portale di Azure hello è disabilitata.

Questi elementi richiedono **scrivere** accedere toohello **piano di servizio App** corrispondente sito Web tooyour:  

* App web hello di visualizzazione del piano tariffario (Free o Standard)  
* Configurazione di scalabilità, ossia numero di istanze, dimensione della macchina virtuale, impostazioni di scalabilità automatica  
* Quote, ad esempio archiviazione, larghezza di banda e CPU  

Questi elementi richiedono **scrivere** toohello accesso intero **gruppo di risorse** che contiene il sito Web:  

* I certificati SSL e associazioni (i certificati SSL possono essere condivisi tra siti in hello stesso gruppo di risorse e posizione geografica)  
* Regole di avviso  
* Impostazioni di scalabilità automatica  
* Componenti di Application Insights  
* Test Web  

## <a name="virtual-machine-workloads"></a>Carichi di lavoro delle macchine virtuali
Molto come con le app web, alcune funzionalità nel pannello macchine virtuali hello richiedono una macchina virtuale di accesso in scrittura toohello o tooother risorse nel gruppo di risorse hello.

Macchine virtuali sono nomi tooDomain correlati, le reti virtuali, gli account di archiviazione e le regole di avviso.

Questi elementi richiedono **scrivere** accedere toohello **macchina virtuale**:

* Endpoint  
* Indirizzi IP  
* Dischi  
* Estensioni  

Questi cubi richiedono **scrivere** hello tooboth accesso **macchina virtuale**, hello e **gruppo di risorse** (insieme a nome di dominio hello) che non sia:  

* Set di disponibilità  
* Set con carico bilanciato  
* Regole di avviso  

Se non è possibile accedere a uno di questi riquadri, chiedere all'amministratore per gruppo di risorse toohello accesso collaboratore.

## <a name="see-more"></a>Altro
* [Controllo di accesso basato su ruoli](role-based-access-control-configure.md): Introduzione a RBAC in hello portale di Azure.
* [Ruoli predefiniti](role-based-access-built-in-roles.md): ottenere informazioni sui ruoli hello forniti come standard in RBAC.
* [Ruoli personalizzati in Azure RBAC](role-based-access-control-custom-roles.md): informazioni su come toocreate ruoli personalizzati toofit le esigenze di accesso.
* [Creare un report della cronologia delle modifiche relative all'accesso](role-based-access-control-access-change-history-report.md): monitoraggio delle modifiche nelle assegnazioni dei ruoli nel controllo degli accessi in base al ruolo.

