---
title: 'Servizio di sincronizzazione Azure AD Connect: Concetti tecnici | Documentazione Microsoft'
description: Illustra i concetti tecnici hello di sincronizzazione di Azure AD Connect.
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
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Servizio di sincronizzazione Azure AD Connect: Concetti tecnici
In questo articolo è riportato un riepilogo di argomento hello [Understanding architecture](active-directory-aadconnectsync-technical-concepts.md).

Il servizio di sincronizzazione Azure AD Connect si basa su una solida piattaforma di sincronizzazione di metadirectory.
Nelle sezioni che seguono Hello hello concetti per la sincronizzazione di metadirectory.
Basandosi su MIIS, ILM e FIM, hello Azure Active Directory Sync Services fornisce piattaforma innovativa hello per le origini toodata connessione, la sincronizzazione dei dati tra origini dati, nonché hello provisioning e deprovisioning delle identità.

![Concetti tecnici](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

Hello le sezioni seguenti fornisce ulteriori dettagli sui seguenti aspetti del servizio di sincronizzazione FIM hello hello:

* Connettore
* Flusso dell'attributo
* Spazio connettore
* Metaverse
* Provisioning

## <a name="connector"></a>Connettore
moduli di codice Hello toocommunicate utilizzato con una directory connessa sono chiamati connettori (precedentemente noti come agenti di gestione (definiti)).

Sono installati nel computer di hello che esegue la sincronizzazione di Azure AD Connect. i connettori di Hello forniscono hello possibilità senza agente tooconverse tramite protocolli di sistema remoto invece di basarsi sulla distribuzione di hello di agenti specializzati. Ciò comporta una riduzione del rischio e dei tempi di distribuzione, in particolare in caso di applicazioni e sistemi critici.

Nella figura hello precedente, il connettore di hello è sinonimo di spazio connettore hello ma include tutte le comunicazioni con sistema esterno hello.

Hello connettore è responsabile di tutto importare ed esportare sistema toohello funzionalità e consente agli sviluppatori di concentrarsi toounderstand come tooconnect tooeach sistema in modo nativo quando l'utilizzo delle trasformazioni di dati toocustomize provisioning dichiarativo.

Importazioni ed esportazioni sono eseguite solo quando pianificato, permettendo ulteriormente un isolamento dalle modifiche apportate nel sistema hello, poiché le modifiche non vengono propagate automaticamente origine dati connessa toohello. Inoltre, gli sviluppatori possono creare connettori personalizzati per la connessione toovirtually qualsiasi origine dati.

## <a name="attribute-flow"></a>Flusso dell'attributo
metaverse Hello è hello consolidato visualizzare tutte le identità unite dagli spazi connettore vicini. Nella figura hello precedente, il flusso di attributi viene rappresentato tramite linee con frecce per il flusso in ingresso e in uscita. Flusso di attributi è il processo di hello di copia o trasformazione dei dati da un sistema tooanother e tutti gli attributi flussi (in ingresso o in uscita).

Flusso di attributi si verifica bidirezionale tra spazio connettore hello e metaverse di hello quando le operazioni di sincronizzazione (completa o delta) sono pianificati toorun.

Il flusso dell'attributo si verifica solo quando vengono eseguite le sincronizzazioni. I flussi di attributi sono definiti nelle regole di sincronizzazione. Possono essere in entrata (ISR nella figura hello precedente) o in uscita (OSR nella figura hello precedente).

## <a name="connected-system"></a>Sistema connesso
Sistema connesso (noto anche come directory connessa) fa riferimento il sistema remoto toohello Azure sincronizzazione di Active Directory Connect è connesso tooand lettura e scrittura tooand di dati di identità da.

## <a name="connector-space"></a>Spazio connettore
Ogni origine dati connessa è rappresentata come sottoinsieme filtrato di hello oggetti e attributi nello spazio connettore hello.
Questo consente toooperate servizio di sincronizzazione hello in locale senza sistema remoto hello toocontact necessità hello quando la sincronizzazione degli oggetti hello e limita l'interazione tooimports e consente di esportare solo.

Quando origine dati hello e connettore hello hanno hello possibilità tooprovide un elenco di modifiche (importazione delta), quindi hello l'efficienza operativa aumenta notevolmente come solo le modifiche apportate dall'ultimo polling hello ciclo viene scambiati. spazio connettore Hello isola l'origine dati connessa hello dalla propagazione automatica richiedendo che pianificazione connettore hello importazioni e le esportazioni delle modifiche. Questa aggiunta assicurazione concede tranquillità durante il test, la visualizzazione in anteprima o conferma hello di aggiornamento successivo.

## <a name="metaverse"></a>Metaverse
metaverse Hello è hello consolidato visualizzare tutte le identità unite dagli spazi connettore vicini.

Poiché le identità sono collegate tra loro e l'autorità è assegnata a diversi attributi tramite il mapping di flusso di importazione, oggetto metaverse centrale hello inizia tooaggregate informazioni da più sistemi. Da questo flusso di attributi di oggetto, i mapping portano toooutbound sistemi informatici.

Gli oggetti vengono creati quando un sistema autorevole li proietta hello metaverse. Non appena vengono rimosse tutte le connessioni, viene eliminato l'oggetto metaverse hello.

Impossibile modificare direttamente gli oggetti nel metaverse hello. Tutti i dati nell'oggetto hello devono essere forniti tramite il flusso di attributi. Hello metaverse mantiene connettori permanenti con ogni spazio connettore. Questi connettori non richiedono una nuova valutazione per ogni esecuzione della sincronizzazione. Ciò significa che la sincronizzazione di Azure AD Connect non dispone di toolocate hello corrispondente remoto oggetto ogni volta. Questo evita hello necessità di usare agenti costosi tooprevent modifiche tooattributes che sarebbero normalmente responsabili della correlazione oggetti hello.

Quando rileva nuove origini dati che potrebbero includere oggetti preesistenti toobe gestito, utilizza la sincronizzazione di Azure AD Connect è necessario un processo chiamato un join regola tooevaluate i candidati potenziali con cui tooestablish un collegamento.
Una volta stabilito il collegamento di hello, la valutazione non viene ripetuta e flusso normale di attributi può verificarsi tra origine dati remota connessa hello e hello metaverse.

## <a name="provisioning"></a>Provisioning
Quando un'origine autorevole proietta può essere creato un nuovo oggetto Metaverse hello un nuovo oggetto spazio connettore in un altro connettore che rappresenta un'origine dati connessa a valle.

In questo modo sarà stabilito implicitamente un collegamento e il flusso dell'attributo potrà procedere in modo bidirezionale.

Ogni volta che una regola rileva che un nuovo oggetto spazio connettore toobe creato, viene chiamato il provisioning. Tuttavia, poiché questa operazione avviene solo all'interno dello spazio connettore hello, non riportati nell'origine dati connessa hello fino a quando non viene eseguita un'esportazione.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Servizio di sincronizzazione Azure AD Connect: Personalizzazione delle opzioni di sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
