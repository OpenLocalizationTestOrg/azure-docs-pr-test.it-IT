---
title: concetti di Lab aaaDevTest | Documenti Microsoft
description: "Informazioni su concetti di base hello di DevTest Labs e come può rendere più facile toocreate, gestire e monitorare macchine virtuali di Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a>Concetti di Lab di sviluppo e test
## <a name="overview"></a>Panoramica
Hello seguente elenco contiene le definizioni e concetti chiave di DevTest Labs:

## <a name="labs"></a>Lab
Un ambiente lab è infrastruttura hello che comprende un gruppo di risorse, ad esempio macchine virtuali (VM), che consente una migliore gestione di tali risorse specificando i limiti e quote.

## <a name="virtual-machine"></a>Macchina virtuale
Una macchina virtuale di Azure è uno dei vari tipi di [risorse di calcolo scalabili e su richiesta](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) offerte da Azure. Consentono di macchine virtuali di Azure è hello flessibilità della virtualizzazione senza toobuy e mantenere hello l'hardware fisico viene eseguita, anche se è ancora necessario toomaintain hello VM mediante l'esecuzione di determinate attività, ad esempio la configurazione, l'applicazione di patch e installazione del software hello che viene eseguito su di esso.

L'articolo [Panoramica delle macchine virtuali Windows in Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) offre informazioni sugli aspetti da tenere in considerazione prima di creare una macchina virtuale, oltre a indicazioni su come creare e gestire la macchina virtuale stessa.

## <a name="claimable-vm"></a>Macchina virtuale a disposizione degli utenti
Una macchina virtuale di Azure a disposizione degli utenti è una macchina virtuale che può essere usata da qualsiasi utente di laboratorio che dispone delle autorizzazioni appropriate. Un amministratore del lab possibile preparare le macchine virtuali con gli elementi e le immagini di base specifiche e salvarle in pool tooa condiviso. Un utente di lab può quindi richiedere una macchina virtuale dal pool hello funzionante quando hanno bisogno di una configurazione che specifica.

Una macchina virtuale che è claimable non viene inizialmente assegnata tooany particolare utente, ma verrà visualizzati nell'elenco di tutti gli utenti in "Claimable virtual machines". Dopo che una macchina virtuale è richiesto da un utente, viene spostata verso l'alto tootheir area "virtual machines" e non è più claimable da altri utenti.

## <a name="environment"></a>Environment
Nella finestra di DevTest Labs, un ambiente si riferisce tooa raccolta di risorse di Azure in un ambiente lab. [Questo post di blog](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) viene illustrato come ambienti multi-VM toocreate i modelli di gestione risorse di Azure.

## <a name="base-images"></a>Immagini di base
Le immagini di base sono immagini di macchina virtuale con tutti gli strumenti di hello e impostazioni preinstallate e configurato tooquickly creare una macchina virtuale. È possibile fornire una macchina virtuale scegliendo una base esistente e aggiunta di un elemento tooinstall l'agente di test. È possibile quindi Salva hello il provisioning VM come una base in modo che hello base può essere utilizzata senza la necessità di agente di test hello tooreinstall per ogni processo di provisioning della macchina virtuale hello.

## <a name="artifacts"></a>Elementi
Gli elementi vengono utilizzati toodeploy e configurare l'applicazione dopo il provisioning di una macchina virtuale. Gli elementi possono essere:

* Strumenti che si desidera tooinstall su hello - VM, ad esempio gli agenti, Fiddler e Visual Studio.
* Azioni che si desidera toorun su hello - VM, come la clonazione di un repository.
* Applicazioni che si desidera tootest.

Gli elementi sono [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) file JSON che contengono istruzioni tooperform distribuzione e applicano la configurazione.

## <a name="artifact-repositories"></a>Repository di elementi
I repository di elementi sono repository git in cui vengono archiviati gli elementi. È possibile aggiungere il repository di artefatti toomultiple labs nell'organizzazione, consentendo il riutilizzo e la condivisione.

## <a name="formulas"></a>Formule
Le formule, nelle immagini toobase addizione, forniscono un meccanismo per il provisioning rapido di VM. Nella formula di DevTest Labs è un elenco di predefinito proprietà valori usati toocreate un lab di macchina virtuale.
Con le formule, le macchine virtuali con hello stesso insieme di proprietà, ad esempio l'immagine di base, dimensioni di macchina virtuale, rete virtuale ed elementi - è possibile creare senza la necessità toospecify ogni volta che tali proprietà. Quando si crea una macchina virtuale da una formula, è possono utilizzare i valori predefiniti di hello come-viene modificato o.

## <a name="policies"></a>Criteri
I criteri consentono di controllare i costi nel lab. Ad esempio, è possibile creare un criterio tooautomatically arrestare le macchine virtuali in base a una pianificazione definita.

## <a name="caps"></a>Limiti
BLOC MAIUSC è uno spreco di toominimize meccanismo nell'ambiente lab. Ad esempio, è possibile impostare un numero di hello toorestrict estremità di macchine virtuali che possono essere creati per ogni utente o in un ambiente lab.

## <a name="security-levels"></a>Livelli di sicurezza
L'accesso sicuro è determinato dal controllo degli accessi in base al ruolo di Azure. toounderstand accedere come funziona, ma consente toounderstand hello differenze un'autorizzazione, un ruolo e un ambito, come definito da RBAC.

* -Un'autorizzazione è un'azione di accesso definito tooa specifica (ad esempio, con accesso in lettura tooall-macchine virtuali).
* Ruolo: un ruolo è un set di autorizzazioni che possono essere raggruppati e tooa utente assegnato. Ad esempio, hello *proprietario della sottoscrizione* ruolo ha accesso alle risorse tooall all'interno di una sottoscrizione.
* -Un ambito è un livello nella gerarchia di hello di una risorsa di Azure, ad esempio un gruppo di risorse, un unico laboratorio o l'intera sottoscrizione hello.

Nell'ambito di hello di DevTest Labs, sono disponibili due tipi di autorizzazioni utente per i ruoli toodefine: proprietario del lab e utente lab.

* Proprietario del lab, il proprietario di un lab ha tooany di accedere alle risorse nell'ambiente lab hello. Pertanto, il proprietario di un lab può modificare i criteri, leggere e scrivere tutte le macchine virtuali, modificare la rete virtuale hello e così via.
* Utente del lab: può visualizzare tutte le risorse del lab, ad esempio VM, criteri e reti virtuali, ma non può modificare i criteri o le VM create da altri utenti.

toosee come toocreate ruoli personalizzati in DevTest Labs, consultare l'articolo toohello, [concedere le autorizzazioni utente criteri lab toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Poiché gli ambiti sono gerarchici, quando un utente ha le autorizzazioni per un determinato ambito, gli vengono automaticamente concesse tali autorizzazioni per ogni ambito di livello inferiore incluso. Ad esempio, se un utente viene assegnato il ruolo di toohello del proprietario della sottoscrizione, quindi hanno accesso tooall alle risorse di una sottoscrizione, che includono tutte le macchine virtuali, tutte le reti virtuali e tutte le esercitazioni. Pertanto, un proprietario della sottoscrizione eredita automaticamente ruolo hello del proprietario del lab. Tuttavia, hello opposto non è true. Il proprietario di un lab ha lab tooa accesso, ovvero un ambito inferiore rispetto a livello di sottoscrizione hello. Pertanto, il proprietario di un lab non sarà in grado di toosee le macchine virtuali o reti virtuali o le risorse che sono di fuori di lab hello.

## <a name="azure-resource-manager-templates"></a>Modelli di Gestione risorse di Azure
Tutti i concetti illustrati in questo articolo possono essere configurati utilizzando i modelli di gestione risorse di Azure, che consentono di hello definire hello infrastruttura/di configurazione della soluzione Azure e distribuire ripetutamente in uno stato coerente.

[Comprendere la struttura di hello e sintassi dei modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) descrive hello struttura di una proprietà del modello e hello Gestione risorse di Azure sono disponibili in diverse sezioni di hello di un modello.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Passaggi successivi
[Creare un lab in Azure DevTest Labs](devtest-lab-create-lab.md)
