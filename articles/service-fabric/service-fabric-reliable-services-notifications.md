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
# <a name="reliable-services-notifications"></a><span data-ttu-id="38ba5-103">Notifiche di Reliable Services</span><span class="sxs-lookup"><span data-stu-id="38ba5-103">Reliable Services notifications</span></span>
<span data-ttu-id="38ba5-104">Le notifiche consentono ai client tootrack hello le modifiche apportate da oggetto tooan che si è interessati.</span><span class="sxs-lookup"><span data-stu-id="38ba5-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="38ba5-105">Le notifiche sono supportate da due tipi di oggetto: *Reliable State Manager* e *Reliable Dictionary*.</span><span class="sxs-lookup"><span data-stu-id="38ba5-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="38ba5-106">I motivi comuni per l'uso di notifiche sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="38ba5-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="38ba5-107">Compilazione materializzata visualizzazioni, ad esempio gli indici secondari o aggregato viste filtrate di stato della replica di hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="38ba5-108">Un esempio è costituito da un indice ordinato di tutte le chiavi in un oggetto Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="38ba5-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="38ba5-109">L'invio monitoraggio dei dati, ad esempio il numero di hello di utenti aggiunti in hello ultima ora.</span><span class="sxs-lookup"><span data-stu-id="38ba5-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="38ba5-110">Le notifiche vengono attivate come parte dell'applicazione dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="38ba5-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="38ba5-111">Per questo motivo, le notifiche devono essere gestite nel più breve tempo possibile e gli eventi sincroni non devono includere operazioni dispendiose.</span><span class="sxs-lookup"><span data-stu-id="38ba5-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="38ba5-112">Notifiche di Reliable State Manager</span><span class="sxs-lookup"><span data-stu-id="38ba5-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="38ba5-113">Gestore degli stati affidabile fornisce notifiche per hello seguenti eventi:</span><span class="sxs-lookup"><span data-stu-id="38ba5-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="38ba5-114">Transazione</span><span class="sxs-lookup"><span data-stu-id="38ba5-114">Transaction</span></span>
  * <span data-ttu-id="38ba5-115">Commit</span><span class="sxs-lookup"><span data-stu-id="38ba5-115">Commit</span></span>
* <span data-ttu-id="38ba5-116">State Manager</span><span class="sxs-lookup"><span data-stu-id="38ba5-116">State manager</span></span>
  * <span data-ttu-id="38ba5-117">Ricompilazione</span><span class="sxs-lookup"><span data-stu-id="38ba5-117">Rebuild</span></span>
  * <span data-ttu-id="38ba5-118">Aggiunta di uno stato affidabile</span><span class="sxs-lookup"><span data-stu-id="38ba5-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="38ba5-119">Rimozione di uno stato affidabile</span><span class="sxs-lookup"><span data-stu-id="38ba5-119">Removal of a reliable state</span></span>

<span data-ttu-id="38ba5-120">Gestore degli stati affidabile tiene traccia delle transazioni in-Flight corrente hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="38ba5-121">modifica solo Hello allo stato di transazione che provoca un toobe notifica generato è una commit della transazione.</span><span class="sxs-lookup"><span data-stu-id="38ba5-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="38ba5-122">Reliable State Manager gestisce una raccolta di stati affidabili come Reliable Dictionary e Reliable Queue.</span><span class="sxs-lookup"><span data-stu-id="38ba5-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="38ba5-123">Gestore degli stati affidabile genera notifiche quando la raccolta cambia: aggiunta o rimozione di uno stato affidabile o l'intera raccolta hello viene ricompilato.</span><span class="sxs-lookup"><span data-stu-id="38ba5-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="38ba5-124">raccolta affidabile di gestione dello stato di Hello viene ricompilato in tre casi:</span><span class="sxs-lookup"><span data-stu-id="38ba5-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="38ba5-125">Ripristino: All'avvio di una replica, Ripristina lo stato precedente dal disco hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="38ba5-126">Alla fine di hello del ripristino, viene utilizzato **NotifyStateManagerChangedEventArgs** toofire un evento che contiene il set di hello degli stati affidabili ripristinati.</span><span class="sxs-lookup"><span data-stu-id="38ba5-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="38ba5-127">Copia completa: prima di una replica è possibile unire i set di configurazione hello, ha toobe compilato.</span><span class="sxs-lookup"><span data-stu-id="38ba5-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="38ba5-128">In alcuni casi, ciò richiede una copia completa dello stato del gestore degli stati affidabile da hello replica primaria toobe toohello applicato inattivo replica secondaria.</span><span class="sxs-lookup"><span data-stu-id="38ba5-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="38ba5-129">Gestore degli stati affidabile su hello replica secondaria utilizzi **NotifyStateManagerChangedEventArgs** toofire un evento che contiene il set di hello degli stati affidabili che acquisito dalla replica primaria hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="38ba5-130">Ripristino: A In scenari di ripristino di emergenza, lo stato della replica hello può essere ripristinato da un backup tramite **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="38ba5-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="38ba5-131">In questi casi, Usa affidabile gestore degli stati nella replica primaria hello **NotifyStateManagerChangedEventArgs** toofire un evento che contiene il set di hello di stati affidabili di ripristinarla dal backup hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="38ba5-132">tooregister per le notifiche delle transazioni e/o notifiche di gestione dello stato, è necessario tooregister con hello **TransactionChanged** o **StateManagerChanged** eventi Gestione stato affidabile.</span><span class="sxs-lookup"><span data-stu-id="38ba5-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="38ba5-133">Un punto comune tooregister con questi gestori eventi è il costruttore di hello del servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="38ba5-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="38ba5-134">Quando si registra nel costruttore hello, da non perdere le notifiche che sono causata da una modifica nel corso della durata hello di **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="38ba5-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="38ba5-135">Hello **TransactionChanged** gestore eventi utilizza **NotifyTransactionChangedEventArgs** tooprovide dettagli sull'evento hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="38ba5-136">Contiene la proprietà azione hello (ad esempio, **NotifyTransactionChangedAction.Commit**) che specifica il tipo di hello di modifica.</span><span class="sxs-lookup"><span data-stu-id="38ba5-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="38ba5-137">Contiene inoltre proprietà della transazione hello che fornisce una transazione toohello di riferimento che ha modificato.</span><span class="sxs-lookup"><span data-stu-id="38ba5-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="38ba5-138">Oggi, **TransactionChanged** vengono generati solo se viene eseguito il commit delle transazioni hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="38ba5-139">Hello azione viene quindi uguale troppo**NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="38ba5-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="38ba5-140">Ma in futuro hello, eventi potrebbero essere generati per altri tipi di modifiche dello stato delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="38ba5-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="38ba5-141">È consigliabile controllo azione hello e l'elaborazione di eventi hello solo se è previsto.</span><span class="sxs-lookup"><span data-stu-id="38ba5-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="38ba5-142">Di seguito è riportato un esempio del gestore eventi **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="38ba5-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="38ba5-143">Hello **StateManagerChanged** gestore eventi utilizza **NotifyStateManagerChangedEventArgs** tooprovide dettagli sull'evento hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="38ba5-144">**NotifyStateManagerChangedEventArgs** ha due sottoclassi: **NotifyStateManagerRebuildEventArgs** e **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="38ba5-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="38ba5-145">Utilizzare proprietà azione hello in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** sottoclasse corretto toohello:</span><span class="sxs-lookup"><span data-stu-id="38ba5-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="38ba5-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="38ba5-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="38ba5-147">**NotifyStateManagerChangedAction.Add** e **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="38ba5-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="38ba5-148">Di seguito è riportato un esempio del gestore delle notifiche **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="38ba5-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="38ba5-149">Notifiche di Reliable Dictionary</span><span class="sxs-lookup"><span data-stu-id="38ba5-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="38ba5-150">Dizionario affidabile fornisce notifiche per hello seguenti eventi:</span><span class="sxs-lookup"><span data-stu-id="38ba5-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="38ba5-151">Ricompilazione: chiamata quando l'oggetto **ReliableDictionary** ha recuperato il proprio stato da un backup o uno stato locale copiato o ripristinato.</span><span class="sxs-lookup"><span data-stu-id="38ba5-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="38ba5-152">Cancella: Viene chiamato quando lo stato di hello **ReliableDictionary** è stato cancellato tramite hello **ClearAsync** (metodo).</span><span class="sxs-lookup"><span data-stu-id="38ba5-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="38ba5-153">Aggiungere: Viene chiamato quando un elemento è stato aggiunto troppo**ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="38ba5-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="38ba5-154">Aggiornamento: chiamata quando è stato aggiornato un elemento in **IReliableDictionary** .</span><span class="sxs-lookup"><span data-stu-id="38ba5-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="38ba5-155">Rimozione: chiamata quando è stato eliminato un elemento in **IReliableDictionary** .</span><span class="sxs-lookup"><span data-stu-id="38ba5-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="38ba5-156">notifiche di dizionario affidabile tooget, è necessario tooregister con hello **DictionaryChanged** nel gestore dell'evento **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="38ba5-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="38ba5-157">Un punto comune è tooregister con questi gestori eventi in hello **ReliableStateManager.StateManagerChanged** aggiungere la notifica.</span><span class="sxs-lookup"><span data-stu-id="38ba5-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="38ba5-158">La registrazione quando **IReliableDictionary** viene aggiunto troppo**IReliableStateManager** assicura che tutte le notifiche andrà perduto.</span><span class="sxs-lookup"><span data-stu-id="38ba5-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="38ba5-159">**ProcessStateManagerSingleEntityNotification** è il metodo di esempio hello che hello precedente **OnStateManagerChangedHandler** chiamate di esempio.</span><span class="sxs-lookup"><span data-stu-id="38ba5-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="38ba5-160">codice precedente Hello imposta hello **IReliableNotificationAsyncCallback** interfaccia, insieme con **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="38ba5-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="38ba5-161">Poiché **NotifyDictionaryRebuildEventArgs** contiene un **IAsyncEnumerable** interfaccia, che richiede toobe enumerati in modo asincrono, le notifiche di ricompilazione vengono attivate tramite ** RebuildNotificationAsyncCallback** anziché **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="38ba5-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="38ba5-162">Hello precedente di codice, come parte della notifica di ricompilazione hello di elaborazione, hello prima gestiti aggregato stato viene cancellato.</span><span class="sxs-lookup"><span data-stu-id="38ba5-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="38ba5-163">Poiché raccolta affidabile di hello ricompilazione con un nuovo stato, tutte le notifiche precedenti sono irrilevanti.</span><span class="sxs-lookup"><span data-stu-id="38ba5-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="38ba5-164">Hello **DictionaryChanged** gestore eventi utilizza **NotifyDictionaryChangedEventArgs** tooprovide dettagli sull'evento hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="38ba5-165">**NotifyDictionaryChangedEventArgs** ha cinque sottoclassi.</span><span class="sxs-lookup"><span data-stu-id="38ba5-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="38ba5-166">Utilizzare proprietà action hello in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** sottoclasse corretto toohello:</span><span class="sxs-lookup"><span data-stu-id="38ba5-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="38ba5-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="38ba5-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="38ba5-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="38ba5-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="38ba5-169">**NotifyDictionaryChangedAction.Add** e **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="38ba5-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="38ba5-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="38ba5-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="38ba5-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="38ba5-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="38ba5-172">Consigli</span><span class="sxs-lookup"><span data-stu-id="38ba5-172">Recommendations</span></span>
* <span data-ttu-id="38ba5-173">*Completare* gli eventi di notifica nel più breve tempo possibile.</span><span class="sxs-lookup"><span data-stu-id="38ba5-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="38ba5-174">*Non eseguire* operazioni dispendiose (ad esempio, operazioni di I/O) nell'ambito di eventi sincroni.</span><span class="sxs-lookup"><span data-stu-id="38ba5-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="38ba5-175">*Eseguire* controllare il tipo di azione hello prima di elaborare l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="38ba5-176">In futuro hello, è potrebbero aggiungervi nuovi tipi di azione.</span><span class="sxs-lookup"><span data-stu-id="38ba5-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="38ba5-177">Ecco alcuni aspetti tookeep presente:</span><span class="sxs-lookup"><span data-stu-id="38ba5-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="38ba5-178">Le notifiche vengono attivate come parte dell'esecuzione di hello di un'operazione.</span><span class="sxs-lookup"><span data-stu-id="38ba5-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="38ba5-179">Ad esempio, una notifica di ripristino viene attivata come ultimo passaggio di hello di un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="38ba5-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="38ba5-180">Un ripristino non verrà completata fino a quando non viene elaborato l'evento di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="38ba5-181">Poiché le notifiche vengono attivate come parte di hello dell'esecuzione di operazioni, visualizzate solo le notifiche per le operazioni di commit in locale.</span><span class="sxs-lookup"><span data-stu-id="38ba5-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="38ba5-182">E poiché le operazioni sono consentite solo toobe commit localmente (in altre parole, registrato), potrebbero o potrebbe non essere annullate in hello future.</span><span class="sxs-lookup"><span data-stu-id="38ba5-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="38ba5-183">Nel percorso di rollforward hello, una singola notifica viene generata per ogni operazione applicata.</span><span class="sxs-lookup"><span data-stu-id="38ba5-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="38ba5-184">Ciò significa che se la transazione T1 include Create(X) Delete(X) e Create(X), si otterrà una notifica per la creazione di hello di X, uno per l'eliminazione di hello e uno per la creazione di hello nuovamente nell'ordine specificato.</span><span class="sxs-lookup"><span data-stu-id="38ba5-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="38ba5-185">Per le transazioni che contengono più operazioni, le operazioni vengono applicate nell'ordine di hello in cui sono stati ricevuti nella replica primaria di hello utente hello.</span><span class="sxs-lookup"><span data-stu-id="38ba5-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="38ba5-186">Come parte dell'elaborazione di un'incoerenza, alcune operazioni potrebbero essere annullate.</span><span class="sxs-lookup"><span data-stu-id="38ba5-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="38ba5-187">Le notifiche vengono generate per tali operazioni di annullamento, rollback dello stato di hello di hello replica tooa indietro stabile punto.</span><span class="sxs-lookup"><span data-stu-id="38ba5-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="38ba5-188">Una differenza importante delle notifiche di annullamento è che gli eventi con chiavi duplicate vengono aggregati.</span><span class="sxs-lookup"><span data-stu-id="38ba5-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="38ba5-189">Ad esempio, se viene annullata transazione T1, si noterà tooDelete(X) una singola notifica.</span><span class="sxs-lookup"><span data-stu-id="38ba5-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38ba5-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38ba5-190">Next steps</span></span>
* [<span data-ttu-id="38ba5-191">Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="38ba5-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="38ba5-192">Guida introduttiva a Reliable Services di Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="38ba5-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="38ba5-193">Eseguire il backup e il ripristino di Reliable Services (ripristino di emergenza)</span><span class="sxs-lookup"><span data-stu-id="38ba5-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="38ba5-194">Guida di riferimento per gli sviluppatori per Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="38ba5-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

