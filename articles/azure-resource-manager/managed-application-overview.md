---
title: applicazioni gestite aaaOverview di Azure | Documenti Microsoft
description: Vengono descritti i concetti di hello per Azure applicazioni gestite
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 2fd1844a442515f4492c890c9798073475a66f88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-overview"></a>Panoramica delle applicazioni gestite di Azure

I fornitori che utilizzano Azure possono offrire soluzioni toocustomers tutto il mondo hello. Azure Marketplace è una raccolta di centinaia di modelli complessi e a più risorse, da fornitori proprietari e di terze parti. I clienti possono distribuire e iniziare a usare in pochi minuti le applicazioni piattaforma come servizio (PaaS) e software come servizio (SaaS). 

Sebbene hello Marketplace fornisce un modo eccellente per i clienti tooquickly distribuire un'offerta, hello cliente è responsabile per la gestione e l'aggiornamento delle soluzioni hello. Oltre fatturazione immagine di macchina virtuale hello, fornitori non applicano un addebito ai clienti per l'utilizzo di hello di un'applicazione. I fornitori, inoltre, non possono in alcun modo impedire ai clienti di modificare risorse cruciali delle applicazioni I fornitori, inoltre, non è possibile bloccare proprietà toointellectual di accesso che costituiscono un'applicazione. Le applicazioni gestite di Azure offrono soluzioni per questi problemi. 

Un'applicazione gestita è modello di soluzione tooa simili in hello Marketplace, con una differenza fondamentale. In un'applicazione gestita, le risorse di hello sono gruppo di risorse di provisioning tooa gestito dal fornitore hello. gruppo di risorse Hello è presente nella sottoscrizione del cliente hello, ma dispone di un'identità nel tenant del fornitore hello gruppo di risorse toohello di accesso.

## <a name="advantages-of-managed-applications"></a>Vantaggi delle applicazioni gestite

Gestito servizio (msp), fornitori di software indipendenti, e utilizzare soluzioni toodeliver applicazioni gestite tramite hello Marketplace o hello catalogo di servizi aziendali team IT centrale. Sebbene i clienti di distribuire tali applicazioni gestite le sottoscrizioni, che non dispongono di toomaintain, aggiornare o gestirle. Poiché i fornitori di gestire e supportano le applicazioni di hello, i clienti non sono toodevelop dominio specifico dell'applicazione knowledge toomanage queste applicazioni. I clienti possono acquisire automaticamente gli aggiornamenti dell'applicazione senza hello necessità tooworry sulla risoluzione dei problemi e la diagnosi di problemi con applicazioni hello.

Per i fornitori e i provider, le applicazioni gestite creano un'infrastruttura toosell del canale e il software tramite hello Marketplace. Applicazioni gestite forniscono anche un modo tooattach servizi e i clienti tooAzure supporto operativo. I fornitori di fatturare ai clienti tramite hello Azure sistema di fatturazione. È possibile utilizzare modelli toomanage hello vita delle applicazioni distribuite. Queste soluzioni sono cliente toohello indipendente e sealed, pertanto i fornitori possono offrire l'alta qualità del servizio. Questo approccio presenta vantaggi non solo per i fornitori di soluzioni PaaS e SaaS, Consente inoltre ai team di piattaforma centrale aziendale e integratori di sistema (SIs) chi desidera toopackage e rivendere le relative soluzioni.

## <a name="managed-application-types"></a>Tipi di applicazioni gestite
Sono disponibili due tipi di applicazioni gestite di Azure: catalogo di servizi e Marketplace.
 
### <a name="service-catalog"></a>Catalogo di servizi  

Con hello catalogo servizi, ai clienti di creare un catalogo di soluzioni approvate per Azure toobe utilizzato dagli utenti nella propria organizzazione. Gestire un catalogo di soluzioni di questo tipo è utile per i team IT centrali delle aziende. Mentre forniscono soluzioni per le organizzazioni possono usare hello catalogo tooensure osservanza determinati standard aziendali. I team sono in grado di controllare, aggiornare e gestire le applicazioni. I dipendenti possono usare hello catalogo tooeasily individuare ricca hello di applicazioni che sono consigliati e approvata da reparti IT. I clienti Vedere applicazioni di catalogo di servizi gestiti di hello che hanno creato. È inoltre possibile visualizzare hello ad altri utenti nella loro condivisione dell'organizzazione con le applicazioni gestite.
 
Per informazioni sulla pubblicazione di un'applicazione gestita del catalogo di servizi, vedere [Creare e pubblicare un'applicazione gestita del catalogo di servizi](managed-application-publishing.md).
 
Per informazioni sull'uso delle applicazioni gestite del catalogo di servizi, vedere [Utilizzare un'applicazione gestita di Azure](managed-application-consumption.md).
 
### <a name="marketplace"></a>Marketplace

Applicazioni gestite sono disponibili tramite hello Marketplace in hello portale di Azure. Dopo che il fornitore hello pubblica queste applicazioni, ma sono disponibili per tutti gli utenti all'interno o all'esterno di un'organizzazione tooconsume. Con questo approccio, file msp, ISV e SIs può offrire loro tooall soluzioni ai clienti di Azure. I clienti ottenere hello vantaggio derivante dall'utilizzo queste soluzioni complesse senza tooinvest necessità hello nella comprensione e gestione di soluzioni di hello. 

Attualmente gli editori possono rendere disponibile l'offerta come applicazione gestita o come modello di soluzione non gestito. componenti principali di Hello della pubblicazione di un'applicazione gestita includono i file di modello hello e file di definizione dell'interfaccia utente di hello. file di modello Hello descritte risorse hello vengono effettuato il provisioning. file di definizione dell'interfaccia utente di Hello viene descritto come hello necessari gli input per il provisioning di queste risorse vengono visualizzati nel portale di hello. Hello file necessari vengono compresso in un file con estensione zip e caricati tramite il portale di pubblicazione hello.
 
Per informazioni sulla pubblicazione di un Marketplace di toohello applicazione gestita, vedere [gestito di Azure le applicazioni in hello Marketplace](managed-application-author-marketplace.md).

Per informazioni sull'utilizzo di un'applicazione gestita da hello Marketplace, vedere [utilizzare Azure gestite le applicazioni in hello Marketplace](managed-application-consume-marketplace.md).

## <a name="key-concepts"></a>Concetti chiave

### <a name="managed-resource-group"></a>Gruppo di risorse gestite
Hello gruppo di risorse gestite è dove tutti hello Azure vengono create le risorse che vengono effettuato il provisioning nel modello di hello. Ad esempio, se accessorio hello è toocreate utilizzato un account di archiviazione, il gruppo di risorse contiene risorse di account di archiviazione hello. Non contiene risorse accessorio hello.

### <a name="appliance-package"></a>Pacchetto dell'appliance
server di pubblicazione Hello crea un pacchetto che contiene i file di modello hello e file createUIDefinition hello. In particolare, include i seguenti file hello:

- **applianceMainTemplate.json**: questo file di modello definisce tutte le risorse di hello sono a provisioning dal dispositivo hello. Questo file è un file di modello regolare utilizzati toocreate risorse.

- **MainTemplate.json**: questo file di modello definisce risorse accessorio hello (Microsoft.Solutions/appliances). Una proprietà chiave definita in questa risorsa è ManagedResourceGroupId. Questa proprietà indica quale gruppo di risorse viene utilizzato toohost hello risorse effettive definite in applianceMainTemplate.json.

- **applianceCreateUIDefinition.json**: questo file descrive la modalità di rendering dell'interfaccia utente necessaria per i parametri di hello definiti nel modello hello hello.

### <a name="authorization"></a>Authorization
server di pubblicazione Hello è necessario specificare autorizzazioni hello necessarie risorse di hello hello fornitore toomanage per conto cliente hello. Gruppo di risorse gestite toohello si applica l'autorizzazione. Impostare hello seguenti valori:

- **PrincipalID**: identificatore di Azure Active Directory (Azure AD) dell'utente di hello, gruppo o applicazione che utilizza gruppo di risorse gestite toogrant accesso toohello hello. Questo identificatore appartiene tenant toohello publisher.

- **RoleDefinitionID**: hello identificatore di Azure AD di hello ruolo assegnato toohello precedente ID entità. Può essere uno dei ruoli di controllo di accesso basato sui ruoli predefiniti di hello nel tenant del server di pubblicazione di hello. Per altre informazioni, vedere [Ruoli predefiniti per il controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-built-in-roles.md).

## <a name="next-steps"></a>Passaggi successivi

* Per informazioni sulla pubblicazione applicazioni gestite toohello Marketplace, vedere [gestito di Azure le applicazioni in hello Marketplace](managed-application-author-marketplace.md).
* Per informazioni sull'utilizzo di un'applicazione gestita da hello Marketplace, vedere [utilizzare Azure gestite le applicazioni in hello Marketplace](managed-application-consume-marketplace.md).
* Per informazioni sulla pubblicazione di un'applicazione gestita del catalogo di servizi, vedere [Creare e pubblicare un'applicazione gestita del catalogo di servizi](managed-application-publishing.md).
* Per informazioni sull'uso delle applicazioni gestite del catalogo di servizi, vedere [Utilizzare un'applicazione gestita di Azure](managed-application-consumption.md).
* toocreate un file di definizione dell'interfaccia utente, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).
