---
title: "funzionalità di sicurezza di rete aaaProtect dati personali con Azure | Documenti Microsoft"
description: "Proteggere i dati personali usando le funzionalità di sicurezza di rete di Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a>Proteggere i dati personali con le funzionalità di sicurezza di rete: gruppi di sicurezza di rete e gateway applicazione di Azure

Questo articolo fornisce informazioni e procedure che consentono di utilizzare i gruppi di sicurezza di rete e di Gateway applicazione Azure tooprotect dati personali.

Un elemento importante per la sicurezza a più livelli strategia tooprotect hello informativa sulla privacy dei dati personali è una difesa contro gli attacchi comuni di vulnerabilità, ad esempio attacchi SQL injection o script tra siti. Il traffico di rete indesiderato mantenuti all'esterno della rete virtuale di Azure consente di evitare potenziali compromettere i dati sensibili e consente a Microsoft Azure tools toohelp proteggere i dati da utenti malintenzionati.

## <a name="scenario"></a>Scenario

Una società crociera di grandi dimensioni, la sede centrale negli Stati Uniti hello espansione relativo itinerari toooffer operazioni Mediterraneo hello, Adriatico e mare Baltico, nonché hello isole britannico. In linea di tali attività, che è stato acquisito diversi inferiori consultare linee basate in Italia, Germania, Danimarca e hello Regno Unito

la società Hello utilizza Microsoft Azure i dati aziendali toostore hello cloud ed eseguono applicazioni su macchine virtuali che elaborano e accedere ai dati. I dati includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito della base clienti globale, Include inoltre informazioni sulle risorse umane di tradizionali, ad esempio indirizzi, i numeri di telefono, codici fiscali e informazioni mediche relativi ai dipendenti della società in tutte le posizioni. riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma che include informazioni personali tootrack relazioni con i clienti correnti e precedenti.

Rete con i dipendenti aziendali accesso hello da sedi remote e agenzie di viaggio si trova in tutto il mondo hello hello aziendali hanno accesso alle risorse aziendali toosome e utilizzare le applicazioni web ospitate in macchine virtuali di Azure toointeract con esso.

## <a name="problem-statement"></a>Presentazione del problema

società Hello necessario proteggere la privacy hello di clienti e dati personali dei dipendenti da attacchi che sfruttano i software vulnerabilità toorun malware che potrebbe esporre i dati personali archiviati o utilizzato dalle applicazioni basate su cloud della società hello.

## <a name="company-goal"></a>Obiettivo dell'azienda

Hello tooensure obiettivo della società che non autorizzato di persone non è possibile accedere a applicazioni hello e reti virtuali di Azure aziendali e dati sono presenti, sfruttando vulnerabilità comuni. 

## <a name="solutions"></a>Soluzioni

Microsoft Azure offre sicurezza meccanismi toohelp impedire l'immissione di reti virtuali di Azure traffico indesiderato. Il controllo del traffico in ingresso e in uscita è in genere eseguito da firewall. In Azure, è possibile utilizzare hello Gateway applicazione con hello Firewall applicazione Web e sicurezza gruppi (rete), che opera come un semplice firewall distribuito. Questi strumenti consentono di toodetect e bloccare il traffico di rete indesiderato.

### <a name="application-gatewayweb-application-firewall"></a>Gateway applicazione/Web application firewall

Hello [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) componente (WAF) di hello [Gateway applicazione Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protegge le applicazioni web, che sono sempre più destinazioni di attacchi dannosi che sfruttano noti comuni vulnerabilità. Un Web application firewall centralizzato permette di proteggersi dagli attacchi Web e semplifica la gestione della sicurezza senza richiedere alcuna modifica alle applicazioni.

Il Web application firewall di Azure gestisce varie categorie di attacco, tra cui SQL injection, cross-site scripting, violazioni e anomalie del protocollo HTTP, bot, crawler, scanner, errori di configurazione comuni delle applicazioni, Denial of Service HTTP e altri attacchi comuni come inserimento di comandi, HTTP Request Smuggling, HTTP Response Splitting e Remote File Inclusion. 

È possibile creare un gateway applicazione con WAF o aggiungere il gateway applicazione esistente di WAF tooan. In entrambi i casi, il gateway applicazione di Azure richiede una propria subnet.

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a>Come creare un gateway applicazione con WAF 

toocreate un nuovo gateway applicazione con WAF abilitata, hello seguenti:

1. Log nel portale di Azure toohello in hello **Preferiti** riquadro del portale di hello, fare clic su **New**

2. In hello **New** pannello, fare clic su **rete**.

3. Fare clic su **Gateway applicazione**.

4. Passare il portale di Azure, toohello **fare clic su nuovo \> rete \> Gateway applicazione.**

   ![Creazione di gateway applicazione](media/protect-netsec/app-gateway-01.png)

5. In hello **nozioni di base** blade che viene visualizzata, immettere i valori di hello per hello seguenti campi: nome di livello (Standard o WAF), dimensioni di SKU (Small, Medium o Large), numero (2 per la disponibilità elevata), sottoscrizione, il gruppo di risorse, e Percorso.

6. In hello **impostazioni** pannello visualizzato sotto **rete virtuale**, fare clic su **scegliere una rete virtuale**. Questo passaggio viene visualizzata immettere hello scegliere Pannello di rete virtuale.

7. Fare clic su **Crea nuovo** tooopen hello **crea rete virtuale** blade.

8. Immettere i seguenti valori hello: nome, lo spazio degli indirizzi, il nome di Subnet, intervallo di indirizzi di Subnet. Fare clic su **OK**.

9. In hello **impostazioni** pannello **configurazione IP Frontend**, scegliere il tipo di indirizzo IP hello.

10. Fare clic su **Scegliere un indirizzo IP pubblico** e quindi su **Crea nuovo**.

11. Accettare il valore di predefinito hello e fare clic su **OK.**

12. In hello **impostazioni** pannello **configurazione Listener**, selezionare toouse HTTP o HTTPS in **protocollo**. toouse HTTPS, è necessario un certificato.

13. Configurare le impostazioni specifiche di hello WAF: **Firewall stato** (**abilitato**) e **modalità Firewall** (**prevenzione**). Se si sceglie **rilevamento** come modalità di hello, viene registrato solo il traffico.

14. Hello revisione **riepilogo** pagina e fare clic su **OK**. Gateway applicazione hello ora viene messo in coda e creato.

Dopo aver creato il gateway di applicazione hello, è possibile esplorare tooit nel portale di hello e continuare la configurazione di gateway applicazione hello.

![Gateway applicazione creato](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a>Come è possibile aggiungere l'applicazione di WAF tooan esistente?

tooupdate un WAF toosupport di gateway applicazione esistente in modalità di prevenzione, hello seguenti:

1. Nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**.

2. Fare clic su hello Gateway applicazione esistente in hello **tutte le risorse** blade. 
>[!NOTE]
Nota: Se sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere il nome di hello in hello filtro in base al nome... zona DNS hello accesso tooeasily casella.
3. Fare clic su **firewall applicazione Web** e aggiornare le impostazioni di gateway applicazione hello: **aggiornamento tooWAF livello** (selezionata), **Firewall stato** (abilitato),  **Modalità firewall** (programmi). È inoltre necessario tooconfigure hello set di regole e configurare le regole disattivate.

Per ulteriori informazioni su come un nuovo gateway applicazione con WAF toocreate e in che modo la gateway tooadd WAF tooan esistente dell'applicazione, vedere [creare un gateway applicazione con firewall applicazione web tramite il portale di hello.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)

### <a name="network-security-groups"></a>Gruppi di sicurezza di rete

Oggetto [il gruppo di sicurezza di rete](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) () contiene un elenco di regole di sicurezza che consentono o negano tooresources il traffico di rete connessa troppo[reti virtuali di Azure](https://docs.microsoft.com/azure/virtual-network/) (VNet). È possibile NSGs toosubnets associato o singole macchine virtuali. Quando un gruppo è subnet tooa associato, hello regole tooall risorse toohello connesso subnet. Il traffico può essere limitato ulteriormente associando anche un gruppo tooa macchina virtuale o scheda di rete.

I gruppi di sicurezza di rete contengono quattro proprietà: nome, area, gruppo di risorse e regole.
>[!Note]
Anche se è presente un gruppo in un gruppo di risorse, può essere associato tooresources in qualsiasi gruppo di risorse come risorsa hello fa parte di hello stessa area Azure hello gruppo.

Le regole dei gruppi di sicurezza di rete contengono nove proprietà: nome, protocollo (TCP, UDP o \*, che include sia ICMP che UDP e TCP), intervallo di porte di origine, intervallo di porte di destinazione, prefisso dell'indirizzo di origine, prefisso dell'indirizzo di destinazione, direzione (in ingresso o in uscita), priorità (tra 100 e 4096) e tipo di accesso (consenso o rifiuto). NSGs tutti contengono un set di regole predefinite che possono essere eliminati o sottoposto a override da creare regole hello.

#### <a name="how-do-i-implement-nsgs"></a>Come implementare gruppi di sicurezza di rete

Implementazione NSGs richiede la pianificazione e ci sono diverse considerazioni di progettazione, è necessario tootake in considerazione. Sono inclusi i limiti sul numero di hello di NSGs per sottoscrizione e le regole per ogni gruppo; Progettazione di rete virtuale e subnet, regole speciali, il traffico ICMP, isolamento dei livelli con subnet, servizi di bilanciamento del carico e altro ancora.

Per altre indicazioni per la pianificazione e l'implementazione di gruppi di sicurezza di rete e uno scenario di distribuzione di esempio, vedere [Filtrare il traffico di rete con gruppi di sicurezza di rete](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

#### <a name="how-do-i-create-rules-in-an-nsg"></a>Come creare regole in un gruppo di sicurezza di rete

toocreate in ingresso di regole in un gruppo esistente, hello seguenti:

1. Fare clic su **Esplora** e quindi su **Gruppi di sicurezza di rete**.

2. Selezionare nell'elenco hello di NSGs **front-end di NSG**e quindi **regole di sicurezza in ingresso.**

3. Nell'elenco di hello delle regole di sicurezza in ingresso, fare clic su **Aggiungi.**

4. Immettere i valori hello in hello seguenti campi: nome, priorità, origine, protocollo, origine intervallo, destinazione, destinazione intervallo di porte e azione.

nuova regola Hello apparirà hello NSG dopo alcuni secondi.

![Regole di sicurezza di rete](media/protect-netsec/inbound-security.png)

Per altre istruzioni su come creare regole toocreate NSGs nelle subnet e associare un gruppo a una subnet front-end e back-end, vedere [creare gruppi di sicurezza di rete utilizzando hello portale di Azure.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)

## <a name="next-steps"></a>Passaggi successivi

[Azure Network Security (Sicurezza di rete di Azure)](https://azure.microsoft.com/blog/azure-network-security/)

[Procedure consigliate per la sicurezza della rete di Azure](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[Ottenere informazioni su un gruppo di sicurezza di rete](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[Web application firewall (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
