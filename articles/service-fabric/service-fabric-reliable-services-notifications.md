---
title: Notifiche di Reliable Services | Microsoft Docs
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
ms.openlocfilehash: c6a53d851510ed5e6eec1f3ac0f636ad034a6d4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="aad32-103">Notifiche di Reliable Services</span><span class="sxs-lookup"><span data-stu-id="aad32-103">Reliable Services notifications</span></span>
<span data-ttu-id="aad32-104">Le notifiche consentono ai client di tenere traccia delle modifiche apportate a un oggetto a cui sono interessati.</span><span class="sxs-lookup"><span data-stu-id="aad32-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span></span> <span data-ttu-id="aad32-105">Le notifiche sono supportate da due tipi di oggetto: *Reliable State Manager* e *Reliable Dictionary*.</span><span class="sxs-lookup"><span data-stu-id="aad32-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="aad32-106">I motivi comuni per l'uso di notifiche sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="aad32-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="aad32-107">Compilazione di viste materializzate, come indici secondari o visualizzazioni filtrate aggregate dello stato della replica.</span><span class="sxs-lookup"><span data-stu-id="aad32-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span></span> <span data-ttu-id="aad32-108">Un esempio è costituito da un indice ordinato di tutte le chiavi in un oggetto Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="aad32-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="aad32-109">Invio di dati di monitoraggio, ad esempio il numero di utenti aggiunti nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="aad32-109">Sending monitoring data, such as the number of users added in the last hour.</span></span>

<span data-ttu-id="aad32-110">Le notifiche vengono attivate come parte dell'applicazione dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="aad32-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="aad32-111">Per questo motivo, le notifiche devono essere gestite nel più breve tempo possibile e gli eventi sincroni non devono includere operazioni dispendiose.</span><span class="sxs-lookup"><span data-stu-id="aad32-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="aad32-112">Notifiche di Reliable State Manager</span><span class="sxs-lookup"><span data-stu-id="aad32-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="aad32-113">Reliable State Manager prevede notifiche per gli eventi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aad32-113">Reliable State Manager provides notifications for the following events:</span></span>

* <span data-ttu-id="aad32-114">Transazione</span><span class="sxs-lookup"><span data-stu-id="aad32-114">Transaction</span></span>
  * <span data-ttu-id="aad32-115">Commit</span><span class="sxs-lookup"><span data-stu-id="aad32-115">Commit</span></span>
* <span data-ttu-id="aad32-116">State Manager</span><span class="sxs-lookup"><span data-stu-id="aad32-116">State manager</span></span>
  * <span data-ttu-id="aad32-117">Ricompilazione</span><span class="sxs-lookup"><span data-stu-id="aad32-117">Rebuild</span></span>
  * <span data-ttu-id="aad32-118">Aggiunta di uno stato affidabile</span><span class="sxs-lookup"><span data-stu-id="aad32-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="aad32-119">Rimozione di uno stato affidabile</span><span class="sxs-lookup"><span data-stu-id="aad32-119">Removal of a reliable state</span></span>

<span data-ttu-id="aad32-120">Reliable State Manager tiene traccia delle transazioni correnti in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="aad32-120">Reliable State Manager tracks the current inflight transactions.</span></span> <span data-ttu-id="aad32-121">L'unica modifica dello stato della transazione che causa l'attivazione di una notifica è il commit.</span><span class="sxs-lookup"><span data-stu-id="aad32-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span></span>

<span data-ttu-id="aad32-122">Reliable State Manager gestisce una raccolta di stati affidabili come Reliable Dictionary e Reliable Queue.</span><span class="sxs-lookup"><span data-stu-id="aad32-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="aad32-123">Reliable State Manager attiva le notifiche quando viene modificata la raccolta con l'aggiunta o rimozione di uno stato affidabile o la ricompilazione dell'intera raccolta.</span><span class="sxs-lookup"><span data-stu-id="aad32-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span></span>
<span data-ttu-id="aad32-124">La raccolta di Reliable State Manager viene ricompilata in tre casi.</span><span class="sxs-lookup"><span data-stu-id="aad32-124">The Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="aad32-125">Recupero: quando viene avviata, una replica recupera il proprio stato precedente dal disco.</span><span class="sxs-lookup"><span data-stu-id="aad32-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span></span> <span data-ttu-id="aad32-126">Al termine del recupero, usa **NotifyStateManagerChangedEventArgs** per attivare un evento contenente il set di stati affidabili recuperati.</span><span class="sxs-lookup"><span data-stu-id="aad32-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span></span>
* <span data-ttu-id="aad32-127">Copia completa: prima che una replica possa essere aggiunta al set di configurazione, deve essere compilata.</span><span class="sxs-lookup"><span data-stu-id="aad32-127">Full copy: Before a replica can join the configuration set, it has to be built.</span></span> <span data-ttu-id="aad32-128">In alcuni casi, potrebbe essere necessario applicare una copia completa dello stato di Reliable State Manager dalla replica primaria alla replica secondaria inattiva.</span><span class="sxs-lookup"><span data-stu-id="aad32-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span></span> <span data-ttu-id="aad32-129">Reliable State Manager sulla replica secondaria usa **NotifyStateManagerChangedEventArgs** per attivare un evento contenente il set di stati affidabili acquisito dalla replica primaria.</span><span class="sxs-lookup"><span data-stu-id="aad32-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span></span>
* <span data-ttu-id="aad32-130">Ripristino: negli scenari di ripristino di emergenza, lo stato della replica può essere ripristinato da un backup tramite **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="aad32-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="aad32-131">In questi casi, Reliable State Manager sulla replica primaria usa **NotifyStateManagerChangedEventArgs** per attivare un evento contenente il set di stati affidabili ripristinato dal backup.</span><span class="sxs-lookup"><span data-stu-id="aad32-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span></span>

<span data-ttu-id="aad32-132">Per abilitare le notifiche delle transazioni e/o le notifiche di gestione dello stato, è necessario registrarsi negli eventi **TransactionChanged** o **StateManagerChanged** in Reliable State Manager.</span><span class="sxs-lookup"><span data-stu-id="aad32-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="aad32-133">Una posizione frequente per la registrazione in questi gestori eventi è il costruttore del servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="aad32-133">A common place to register with these event handlers is the constructor of your stateful service.</span></span> <span data-ttu-id="aad32-134">Con la registrazione sul costruttore, non si perde alcuna notifica causata da una modifica nel corso della durata di **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="aad32-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="aad32-135">Il gestore eventi **TransactionChanged** usa **NotifyTransactionChangedEventArgs** per fornire dettagli sull'evento.</span><span class="sxs-lookup"><span data-stu-id="aad32-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span></span> <span data-ttu-id="aad32-136">Contiene la proprietà dell'azione (ad esempio, **NotifyTransactionChangedAction.Commit**) che specifica il tipo di modifica,</span><span class="sxs-lookup"><span data-stu-id="aad32-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span></span> <span data-ttu-id="aad32-137">nonché la proprietà della transazione che fornisce un riferimento alla transazione modificata.</span><span class="sxs-lookup"><span data-stu-id="aad32-137">It also contains the transaction property that provides a reference to the transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="aad32-138">Gli eventi **TransactionChanged** vengono attualmente generati solo in caso di commit della transazione.</span><span class="sxs-lookup"><span data-stu-id="aad32-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span></span> <span data-ttu-id="aad32-139">L'azione è quindi uguale a **NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="aad32-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="aad32-140">È tuttavia possibile che in futuro vengano generati eventi per altri tipi di modifica dello stato della transazione.</span><span class="sxs-lookup"><span data-stu-id="aad32-140">But in the future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="aad32-141">È consigliabile controllare l'azione ed elaborare l'evento solo se previsto.</span><span class="sxs-lookup"><span data-stu-id="aad32-141">We recommend checking the action and processing the event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="aad32-142">Di seguito è riportato un esempio del gestore eventi **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="aad32-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="aad32-143">Il gestore eventi **StateManagerChanged** usa **NotifyStateManagerChangedEventArgs** per fornire dettagli sull'evento.</span><span class="sxs-lookup"><span data-stu-id="aad32-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="aad32-144">**NotifyStateManagerChangedEventArgs** ha due sottoclassi: **NotifyStateManagerRebuildEventArgs** e **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="aad32-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="aad32-145">La proprietà dell'azione in **NotifyStateManagerChangedEventArgs** viene usata per eseguire il cast di **NotifyStateManagerChangedEventArgs** nella sottoclasse corretta.</span><span class="sxs-lookup"><span data-stu-id="aad32-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="aad32-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="aad32-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="aad32-147">**NotifyStateManagerChangedAction.Add** e **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="aad32-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="aad32-148">Di seguito è riportato un esempio del gestore delle notifiche **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="aad32-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="aad32-149">Notifiche di Reliable Dictionary</span><span class="sxs-lookup"><span data-stu-id="aad32-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="aad32-150">Reliable Dictionary prevede notifiche per gli eventi seguenti.</span><span class="sxs-lookup"><span data-stu-id="aad32-150">Reliable Dictionary provides notifications for the following events:</span></span>

* <span data-ttu-id="aad32-151">Ricompilazione: chiamata quando l'oggetto **ReliableDictionary** ha recuperato il proprio stato da un backup o uno stato locale copiato o ripristinato.</span><span class="sxs-lookup"><span data-stu-id="aad32-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="aad32-152">Cancellazione: chiamata quando lo stato di **ReliableDictionary** è stato cancellato tramite il metodo **ClearAsync**.</span><span class="sxs-lookup"><span data-stu-id="aad32-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span></span>
* <span data-ttu-id="aad32-153">Aggiunta: chiamata quando è stato aggiunto un elemento a **ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="aad32-153">Add: Called when an item has been added to **ReliableDictionary**.</span></span>
* <span data-ttu-id="aad32-154">Aggiornamento: chiamata quando è stato aggiornato un elemento in **IReliableDictionary** .</span><span class="sxs-lookup"><span data-stu-id="aad32-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="aad32-155">Rimozione: chiamata quando è stato eliminato un elemento in **IReliableDictionary** .</span><span class="sxs-lookup"><span data-stu-id="aad32-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="aad32-156">Per ricevere le notifiche di Reliable Dictionary, è necessario registrarsi nel gestore eventi **DictionaryChanged** in **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="aad32-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="aad32-157">Una posizione frequente per la registrazione in questi gestori eventi è la notifica di aggiunta **ReliableStateManager.StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="aad32-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="aad32-158">La registrazione al momento dell'aggiunta di **IReliableDictionary** a **IReliableStateManager** garantisce che non verrà persa alcuna notifica.</span><span class="sxs-lookup"><span data-stu-id="aad32-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="aad32-159">**ProcessStateManagerSingleEntityNotification** è il metodo di esempio chiamato dall'esempio **OnStateManagerChangedHandler** precedente.</span><span class="sxs-lookup"><span data-stu-id="aad32-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="aad32-160">Il codice precedente imposta l'interfaccia **IReliableNotificationAsyncCallback** e **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="aad32-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="aad32-161">Poiché **NotifyDictionaryRebuildEventArgs** contiene un'interfaccia **IAsyncEnumerable**, che richiede un'enumerazione asincrona, le notifiche di ricompilazione vengono attivate tramite **RebuildNotificationAsyncCallback** anziché **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="aad32-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="aad32-162">Nel codice precedente, nell'ambito dell'elaborazione della notifica di ricompilazione, viene cancellato prima lo stato aggregato mantenuto.</span><span class="sxs-lookup"><span data-stu-id="aad32-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span></span> <span data-ttu-id="aad32-163">Poiché la raccolta Reliable Collections viene ricompilata con un nuovo stato, tutte le notifiche precedenti sono irrilevanti.</span><span class="sxs-lookup"><span data-stu-id="aad32-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="aad32-164">Il gestore eventi **DictionaryChanged** usa **NotifyDictionaryChangedEventArgs** per fornire dettagli sull'evento.</span><span class="sxs-lookup"><span data-stu-id="aad32-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="aad32-165">**NotifyDictionaryChangedEventArgs** ha cinque sottoclassi.</span><span class="sxs-lookup"><span data-stu-id="aad32-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="aad32-166">Usare la proprietà dell'azione in **NotifyDictionaryChangedEventArgs** per eseguire il cast di **NotifyDictionaryChangedEventArgs** nella sottoclasse corretta.</span><span class="sxs-lookup"><span data-stu-id="aad32-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="aad32-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="aad32-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="aad32-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="aad32-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="aad32-169">**NotifyDictionaryChangedAction.Add** e **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="aad32-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="aad32-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="aad32-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="aad32-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="aad32-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="aad32-172">Consigli</span><span class="sxs-lookup"><span data-stu-id="aad32-172">Recommendations</span></span>
* <span data-ttu-id="aad32-173">*Completare* gli eventi di notifica nel più breve tempo possibile.</span><span class="sxs-lookup"><span data-stu-id="aad32-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="aad32-174">*Non eseguire* operazioni dispendiose (ad esempio, operazioni di I/O) nell'ambito di eventi sincroni.</span><span class="sxs-lookup"><span data-stu-id="aad32-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="aad32-175">*Controllare* il tipo di azione prima di elaborare l'evento.</span><span class="sxs-lookup"><span data-stu-id="aad32-175">*Do* check the action type before you process the event.</span></span> <span data-ttu-id="aad32-176">In futuro potrebbero essere aggiunti nuovi tipi di azione.</span><span class="sxs-lookup"><span data-stu-id="aad32-176">New action types might be added in the future.</span></span>

<span data-ttu-id="aad32-177">Occorre tenere presente i concetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aad32-177">Here are some things to keep in mind:</span></span>

* <span data-ttu-id="aad32-178">Le notifiche vengono attivate come parte dell'esecuzione di un'operazione.</span><span class="sxs-lookup"><span data-stu-id="aad32-178">Notifications are fired as part of the execution of an operation.</span></span> <span data-ttu-id="aad32-179">Una notifica di ripristino, ad esempio, viene attivata come ultimo passaggio di un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="aad32-179">For example, a restore notification is fired as the last step of a restore operation.</span></span> <span data-ttu-id="aad32-180">Un ripristino non viene completato finché non viene elaborato l'evento di notifica.</span><span class="sxs-lookup"><span data-stu-id="aad32-180">A restore will not finish until the notification event is processed.</span></span>
* <span data-ttu-id="aad32-181">Poiché le notifiche vengono attivate nell'ambito dell'applicazione di operazioni, i client visualizzano solo le notifiche per le operazioni con commit in locale.</span><span class="sxs-lookup"><span data-stu-id="aad32-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="aad32-182">Poiché è garantito solo il commit in locale (in altri termini, la registrazione), inoltre, potrebbe non essere possibile annullare le operazioni in futuro.</span><span class="sxs-lookup"><span data-stu-id="aad32-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span></span>
* <span data-ttu-id="aad32-183">Nel percorso di ripristino viene attivata una singola notifica per ogni operazione applicata.</span><span class="sxs-lookup"><span data-stu-id="aad32-183">On the redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="aad32-184">Di conseguenza, se la transazione T1 include Create(X), Delete(X) e Create(X), si riceverà una notifica per la creazione di X, una per l'eliminazione e una per una nuova creazione, nell'ordine specificato.</span><span class="sxs-lookup"><span data-stu-id="aad32-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span></span>
* <span data-ttu-id="aad32-185">Per le transazioni che contengono più operazioni, queste verranno applicate nell'ordine in cui sono state ricevute nella replica primaria dall'utente.</span><span class="sxs-lookup"><span data-stu-id="aad32-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span></span>
* <span data-ttu-id="aad32-186">Come parte dell'elaborazione di un'incoerenza, alcune operazioni potrebbero essere annullate.</span><span class="sxs-lookup"><span data-stu-id="aad32-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="aad32-187">Per queste operazioni di annullamento vengono generate notifiche, con rollback dello stato della replica a un punto stabile.</span><span class="sxs-lookup"><span data-stu-id="aad32-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span></span> <span data-ttu-id="aad32-188">Una differenza importante delle notifiche di annullamento è che gli eventi con chiavi duplicate vengono aggregati.</span><span class="sxs-lookup"><span data-stu-id="aad32-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="aad32-189">Se la transazione T1 viene annullata, ad esempio, viene visualizzata una singola notifica per Delete(X).</span><span class="sxs-lookup"><span data-stu-id="aad32-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aad32-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aad32-190">Next steps</span></span>
* [<span data-ttu-id="aad32-191">Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="aad32-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="aad32-192">Guida introduttiva a Reliable Services di Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="aad32-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="aad32-193">Eseguire il backup e il ripristino di Reliable Services (ripristino di emergenza)</span><span class="sxs-lookup"><span data-stu-id="aad32-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="aad32-194">Guida di riferimento per gli sviluppatori per Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="aad32-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

