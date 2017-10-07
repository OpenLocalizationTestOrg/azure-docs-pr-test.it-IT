---
title: notifiche di servizi aaaReliable | Documenti Microsoft
description: Documentazione concettuale per le notifiche di Reliable Services di Service Fabric
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a>Notifiche di Reliable Services
Le notifiche consentono ai client tootrack hello le modifiche apportate da oggetto tooan che si è interessati. Le notifiche sono supportate da due tipi di oggetto: *Reliable State Manager* e *Reliable Dictionary*.

I motivi comuni per l'uso di notifiche sono i seguenti:

* Compilazione materializzata visualizzazioni, ad esempio gli indici secondari o aggregato viste filtrate di stato della replica di hello. Un esempio è costituito da un indice ordinato di tutte le chiavi in un oggetto Reliable Dictionary.
* L'invio monitoraggio dei dati, ad esempio il numero di hello di utenti aggiunti in hello ultima ora.

Le notifiche vengono attivate come parte dell'applicazione dell'operazione. Per questo motivo, le notifiche devono essere gestite nel più breve tempo possibile e gli eventi sincroni non devono includere operazioni dispendiose.

## <a name="reliable-state-manager-notifications"></a>Notifiche di Reliable State Manager
Gestore degli stati affidabile fornisce notifiche per hello seguenti eventi:

* Transazione
  * Commit
* State Manager
  * Ricompilazione
  * Aggiunta di uno stato affidabile
  * Rimozione di uno stato affidabile

Gestore degli stati affidabile tiene traccia delle transazioni in-Flight corrente hello. modifica solo Hello allo stato di transazione che provoca un toobe notifica generato è una commit della transazione.

Reliable State Manager gestisce una raccolta di stati affidabili come Reliable Dictionary e Reliable Queue. Gestore degli stati affidabile genera notifiche quando la raccolta cambia: aggiunta o rimozione di uno stato affidabile o l'intera raccolta hello viene ricompilato.
raccolta affidabile di gestione dello stato di Hello viene ricompilato in tre casi:

* Ripristino: All'avvio di una replica, Ripristina lo stato precedente dal disco hello. Alla fine di hello del ripristino, viene utilizzato **NotifyStateManagerChangedEventArgs** toofire un evento che contiene il set di hello degli stati affidabili ripristinati.
* Copia completa: prima di una replica è possibile unire i set di configurazione hello, ha toobe compilato. In alcuni casi, ciò richiede una copia completa dello stato del gestore degli stati affidabile da hello replica primaria toobe toohello applicato inattivo replica secondaria. Gestore degli stati affidabile su hello replica secondaria utilizzi **NotifyStateManagerChangedEventArgs** toofire un evento che contiene il set di hello degli stati affidabili che acquisito dalla replica primaria hello.
* Ripristino: A In scenari di ripristino di emergenza, lo stato della replica hello può essere ripristinato da un backup tramite **RestoreAsync**. In questi casi, Usa affidabile gestore degli stati nella replica primaria hello **NotifyStateManagerChangedEventArgs** toofire un evento che contiene il set di hello di stati affidabili di ripristinarla dal backup hello.

tooregister per le notifiche delle transazioni e/o notifiche di gestione dello stato, è necessario tooregister con hello **TransactionChanged** o **StateManagerChanged** eventi Gestione stato affidabile. Un punto comune tooregister con questi gestori eventi è il costruttore di hello del servizio con stato. Quando si registra nel costruttore hello, da non perdere le notifiche che sono causata da una modifica nel corso della durata hello di **IReliableStateManager**.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

Hello **TransactionChanged** gestore eventi utilizza **NotifyTransactionChangedEventArgs** tooprovide dettagli sull'evento hello. Contiene la proprietà azione hello (ad esempio, **NotifyTransactionChangedAction.Commit**) che specifica il tipo di hello di modifica. Contiene inoltre proprietà della transazione hello che fornisce una transazione toohello di riferimento che ha modificato.

> [!NOTE]
> Oggi, **TransactionChanged** vengono generati solo se viene eseguito il commit delle transazioni hello. Hello azione viene quindi uguale troppo**NotifyTransactionChangedAction.Commit**. Ma in futuro hello, eventi potrebbero essere generati per altri tipi di modifiche dello stato delle transazioni. È consigliabile controllo azione hello e l'elaborazione di eventi hello solo se è previsto.
> 
> 

Di seguito è riportato un esempio del gestore eventi **TransactionChanged** .

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

Hello **StateManagerChanged** gestore eventi utilizza **NotifyStateManagerChangedEventArgs** tooprovide dettagli sull'evento hello.
**NotifyStateManagerChangedEventArgs** ha due sottoclassi: **NotifyStateManagerRebuildEventArgs** e **NotifyStateManagerSingleEntityChangedEventArgs**.
Utilizzare proprietà azione hello in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** sottoclasse corretto toohello:

* **NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** e **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**

Di seguito è riportato un esempio del gestore delle notifiche **StateManagerChanged** .

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a>Notifiche di Reliable Dictionary
Dizionario affidabile fornisce notifiche per hello seguenti eventi:

* Ricompilazione: chiamata quando l'oggetto **ReliableDictionary** ha recuperato il proprio stato da un backup o uno stato locale copiato o ripristinato.
* Cancella: Viene chiamato quando lo stato di hello **ReliableDictionary** è stato cancellato tramite hello **ClearAsync** (metodo).
* Aggiungere: Viene chiamato quando un elemento è stato aggiunto troppo**ReliableDictionary**.
* Aggiornamento: chiamata quando è stato aggiornato un elemento in **IReliableDictionary** .
* Rimozione: chiamata quando è stato eliminato un elemento in **IReliableDictionary** .

notifiche di dizionario affidabile tooget, è necessario tooregister con hello **DictionaryChanged** nel gestore dell'evento **IReliableDictionary**. Un punto comune è tooregister con questi gestori eventi in hello **ReliableStateManager.StateManagerChanged** aggiungere la notifica.
La registrazione quando **IReliableDictionary** viene aggiunto troppo**IReliableStateManager** assicura che tutte le notifiche andrà perduto.

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> **ProcessStateManagerSingleEntityNotification** è il metodo di esempio hello che hello precedente **OnStateManagerChangedHandler** chiamate di esempio.
> 
> 

codice precedente Hello imposta hello **IReliableNotificationAsyncCallback** interfaccia, insieme con **DictionaryChanged**. Poiché **NotifyDictionaryRebuildEventArgs** contiene un **IAsyncEnumerable** interfaccia, che richiede toobe enumerati in modo asincrono, le notifiche di ricompilazione vengono attivate tramite ** RebuildNotificationAsyncCallback** anziché **OnDictionaryChangedHandler**.

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> Hello precedente di codice, come parte della notifica di ricompilazione hello di elaborazione, hello prima gestiti aggregato stato viene cancellato. Poiché raccolta affidabile di hello ricompilazione con un nuovo stato, tutte le notifiche precedenti sono irrilevanti.
> 
> 

Hello **DictionaryChanged** gestore eventi utilizza **NotifyDictionaryChangedEventArgs** tooprovide dettagli sull'evento hello.
**NotifyDictionaryChangedEventArgs** ha cinque sottoclassi. Utilizzare proprietà action hello in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** sottoclasse corretto toohello:

* **NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** e **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a>Consigli
* *Completare* gli eventi di notifica nel più breve tempo possibile.
* *Non eseguire* operazioni dispendiose (ad esempio, operazioni di I/O) nell'ambito di eventi sincroni.
* *Eseguire* controllare il tipo di azione hello prima di elaborare l'evento hello. In futuro hello, è potrebbero aggiungervi nuovi tipi di azione.

Ecco alcuni aspetti tookeep presente:

* Le notifiche vengono attivate come parte dell'esecuzione di hello di un'operazione. Ad esempio, una notifica di ripristino viene attivata come ultimo passaggio di hello di un'operazione di ripristino. Un ripristino non verrà completata fino a quando non viene elaborato l'evento di notifica hello.
* Poiché le notifiche vengono attivate come parte di hello dell'esecuzione di operazioni, visualizzate solo le notifiche per le operazioni di commit in locale. E poiché le operazioni sono consentite solo toobe commit localmente (in altre parole, registrato), potrebbero o potrebbe non essere annullate in hello future.
* Nel percorso di rollforward hello, una singola notifica viene generata per ogni operazione applicata. Ciò significa che se la transazione T1 include Create(X) Delete(X) e Create(X), si otterrà una notifica per la creazione di hello di X, uno per l'eliminazione di hello e uno per la creazione di hello nuovamente nell'ordine specificato.
* Per le transazioni che contengono più operazioni, le operazioni vengono applicate nell'ordine di hello in cui sono stati ricevuti nella replica primaria di hello utente hello.
* Come parte dell'elaborazione di un'incoerenza, alcune operazioni potrebbero essere annullate. Le notifiche vengono generate per tali operazioni di annullamento, rollback dello stato di hello di hello replica tooa indietro stabile punto. Una differenza importante delle notifiche di annullamento è che gli eventi con chiavi duplicate vengono aggregati. Ad esempio, se viene annullata transazione T1, si noterà tooDelete(X) una singola notifica.

## <a name="next-steps"></a>Passaggi successivi
* [Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Guida introduttiva a Reliable Services di Microsoft Azure Service Fabric](service-fabric-reliable-services-quick-start.md)
* [Eseguire il backup e il ripristino di Reliable Services (ripristino di emergenza)](service-fabric-reliable-services-backup-restore.md)
* [Guida di riferimento per gli sviluppatori per Reliable Collections](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

