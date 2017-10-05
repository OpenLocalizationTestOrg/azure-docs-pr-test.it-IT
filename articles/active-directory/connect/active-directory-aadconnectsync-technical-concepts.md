---
title: 'Servizio di sincronizzazione Azure AD Connect: Concetti tecnici | Documentazione Microsoft'
description: Illustra i concetti tecnici del servizio di sincronizzazione Azure AD Connect.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 6cf8debc6443bb60fc5f601ea4aa392eb2f13a8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Servizio di sincronizzazione Azure AD Connect: Concetti tecnici
Questo articolo è un riepilogo dell'argomento [Informazioni sull'architettura](active-directory-aadconnectsync-technical-concepts.md).

Il servizio di sincronizzazione Azure AD Connect si basa su una solida piattaforma di sincronizzazione di metadirectory.
Le sezioni seguenti presentano i concetti relativi alla sincronizzazione di metadirectory.
Basandosi su MIIS, ILM e FIM, i servizi di sincronizzazione di Azure Active Directory offrono una piattaforma innovativa per la connessione a origini dati, la sincronizzazione di dati tra origini dati e il provisioning e l'annullamento del provisioning delle identità.

![Concetti tecnici](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

Le sezioni successive includono altri dettagli sugli aspetti seguenti del servizio di sincronizzazione FIM:

* Connettore
* Flusso dell'attributo
* Spazio connettore
* Metaverse
* Provisioning

## <a name="connector"></a>Connettore
I moduli di codice utilizzati per comunicare con una directory connessa sono chiamati connettori (definiti in precedenza agenti di gestione (MA)).

Sono installati nel computer che esegue il servizio di sincronizzazione Azure AD Connect.
I connettori offrono la possibilità di comunicare senza agente usando protocolli di sistema remoto invece di basarsi sulla distribuzione di agenti specializzati. Ciò comporta una riduzione del rischio e dei tempi di distribuzione, in particolare in caso di applicazioni e sistemi critici.

Nell'immagine precedente il connettore è sinonimo di spazio connettore, ma include tutte le comunicazioni con il sistema esterno.

Il connettore è responsabile di tutte le funzionalità di importazione ed esportazione nel sistema. Gli sviluppatori potranno quindi evitare di concentrarsi su come connettere ogni sistema in modalità nativa quando usano il provisioning dichiarativo per personalizzare le trasformazioni dei dati.

Le importazioni e le esportazioni sono eseguite solo quando pianificato, permettendo un maggiore isolamento dalle modifiche apportate nel sistema, poiché le modifiche non vengono propagate automaticamente all'origine dati connessa. Gli sviluppatori, inoltre, possono creare connettori personalizzati per connettersi praticamente a qualsiasi origine dati.

## <a name="attribute-flow"></a>Flusso dell'attributo
Per metaverse si intende la visualizzazione consolidata di tutte le identità unite dagli spazi connettore vicini. Nella figura precedente il flusso di attributi è rappresentato tramite linee con frecce per il flusso in entrata e in uscita. Il flusso di attributi è il processo di copia o trasformazione dei dati da un sistema a un altro e tutti gli attributi sono associati a flussi di attributi in entrata o in uscita.

Il flusso dell'attributo si verifica in modo bidirezionale tra lo spazio connettore e il metaverse quando è pianificata l'esecuzione di operazioni di sincronizzazione (completa o delta).

Il flusso dell'attributo si verifica solo quando vengono eseguite le sincronizzazioni. I flussi di attributi sono definiti nelle regole di sincronizzazione. Le regole possono essere in entrata (ISR nella figura precedente) o in uscita (OSR nella figura precedente).

## <a name="connected-system"></a>Sistema connesso
Il sistema connesso (noto anche come directory connessa) fa riferimento al sistema remoto a cui il servizio di sincronizzazione Azure AD Connect è connesso e ai dati di identità nei quali vengono svolte operazioni di lettura e scrittura.

## <a name="connector-space"></a>Spazio connettore
Ogni origine dati connessa è rappresentata come sottoinsieme filtrato di oggetti e attributi nello spazio connettore.
Ciò permette al servizio di sincronizzazione di funzionare localmente, senza che sia necessario contattare il sistema remoto durante la sincronizzazione di oggetti, e limita le interazioni alle sole importazioni ed esportazioni.

Quando l'origine dati e il connettore sono in grado di fornire un elenco di modifiche (importazione delta), l'efficienza operativa aumenta in modo drastico, poiché saranno scambiate solo le modifiche successive all'ultimo ciclo di polling. Lo spazio connettore isola l'origine dati connessa dalla propagazione automatica delle modifiche, richiedendo che il connettore pianifichi le importazioni e le esportazioni. Ciò offre una maggiore sicurezza durante il test, l'anteprima o la conferma dell'aggiornamento successivo.

## <a name="metaverse"></a>Metaverse
Per metaverse si intende la visualizzazione consolidata di tutte le identità unite dagli spazi connettore vicini.

Poiché le identità sono collegate tra loro e l'autorità è assegnata a diversi attributi tramite i mapping di flusso di importazione, l'oggetto metaverse centrale inizia ad aggregare informazioni da più sistemi. Da questo flusso di attributi dell'oggetto, i mapping portano le informazioni ai sistemi in uscita.

Gli oggetti sono creati quando un sistema autorevole li proietta nel metaverse. Non appena vengono rimosse tutte le connessioni, l'oggetto metaverse sarà eliminato.

Gli oggetti nel metaverse non possono essere eliminati direttamente. Tutti i dati nell'oggetto devono essere forniti tramite il flusso di attributi. Il metaverse mantiene connettori permanenti con ogni spazio connettore. Questi connettori non richiedono una nuova valutazione per ogni esecuzione della sincronizzazione. Ciò significa che il servizio di sincronizzazione Azure AD Connect non deve individuare ogni volta l'oggetto remoto corrispondente. Sarà quindi possibile evitare la necessità di usare agenti costosi per impedire modifiche ad attributi che sarebbero normalmente responsabili della correlazione degli oggetti.

Quando rileva nuove origini dati che potrebbero includere oggetti preesistenti da gestire, il servizio di sincronizzazione Azure AD Connect usa un processo definito regola di join per valutare candidati potenziali con cui stabilire un collegamento.
Dopo la creazione del collegamento, la valutazione non viene ripetuta ed è permesso il flusso normale dell'attributo tra l'origine dati remota connessa e il metaverse.

## <a name="provisioning"></a>Provisioning
Quando un'origine autorevole proietta un nuovo oggetto nel metaverse, un nuovo oggetto spazio connettore può essere creato in un altro connettore che rappresenta un'origine dati connessa successiva.

In questo modo sarà stabilito implicitamente un collegamento e il flusso dell'attributo potrà procedere in modo bidirezionale.

Quando una regola determina che è necessario creare un nuovo oggetto spazio connettore, questa operazione è definita provisioning. Poiché tuttavia questa operazione si verifica solo nello spazio connettore, verrà applicata all'origine dati connessa solo quando sarà eseguita un'esportazione.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Servizio di sincronizzazione Azure AD Connect: Personalizzazione delle opzioni di sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
