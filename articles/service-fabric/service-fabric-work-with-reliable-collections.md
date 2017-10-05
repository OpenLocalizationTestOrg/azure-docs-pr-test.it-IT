---
title: Usare le raccolte Reliable Collections | Documentazione Microsoft
description: Procedure consigliate per lavorare con le raccolte Reliable Collections.
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: f53f13e4fb83b1cd370ec673e86e5311cd93055f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-reliable-collections"></a><span data-ttu-id="e42b0-103">Lavorare con le raccolte Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="e42b0-103">Working with Reliable Collections</span></span>
<span data-ttu-id="e42b0-104">Service Fabric offre un modello di programmazione con stato disponibile per gli sviluppatori .NET tramite Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="e42b0-104">Service Fabric offers a stateful programming model available to .NET developers via Reliable Collections.</span></span> <span data-ttu-id="e42b0-105">In particolare, Service Fabric offre classi ReliableDictionary e ReliableQueue.</span><span class="sxs-lookup"><span data-stu-id="e42b0-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="e42b0-106">Quando si usano queste classi, lo stato è partizionato (per la scalabilità), replicato (per la disponibilità) e le transazioni vengono eseguite all'interno di una partizione (per la semantica ACID).</span><span class="sxs-lookup"><span data-stu-id="e42b0-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="e42b0-107">Di seguito viene descritto l'uso tipico di un oggetto ReliableDictionary per osservarne le azioni.</span><span class="sxs-lookup"><span data-stu-id="e42b0-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record to log & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record to log & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

<span data-ttu-id="e42b0-108">Tutte le operazioni sugli oggetti ReliableDictionary (ad eccezione di ClearAsync che non è annullabile) richiedono un oggetto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="e42b0-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="e42b0-109">Questo oggetto è associato a tutte le modifiche che si tenta di apportare a qualsiasi oggetto ReliableDictionary e/o ReliableQueue all'interno di una singola partizione.</span><span class="sxs-lookup"><span data-stu-id="e42b0-109">This object has associated with it any and all changes you’re attempting to make to any reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="e42b0-110">Acquisire un oggetto ITransaction chiamando il metodo CreateTransaction della partizione "StateManager".</span><span class="sxs-lookup"><span data-stu-id="e42b0-110">You acquire an ITransaction object by calling the partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="e42b0-111">Nel codice precedente, l'oggetto ITransaction viene passato al metodo AddAsync dell'oggetto ReliableDictionary.</span><span class="sxs-lookup"><span data-stu-id="e42b0-111">In the code above, the ITransaction object is passed to a reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="e42b0-112">Internamente, i metodi di dizionario che accettano una chiave acquisiscono un blocco di lettura/scrittura associato alla chiave.</span><span class="sxs-lookup"><span data-stu-id="e42b0-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with the key.</span></span> <span data-ttu-id="e42b0-113">Se il metodo modifica il valore della chiave, il metodo acquisisce un blocco di scrittura sulla chiave; se il metodo legge solo dal valore della chiave, allora acquisisce un blocco di lettura sulla chiave.</span><span class="sxs-lookup"><span data-stu-id="e42b0-113">If the method modifies the key’s value, the method takes a write lock on the key and if the method only reads from the key’s value, then a read lock is taken on the key.</span></span> <span data-ttu-id="e42b0-114">Poiché AddAsync modifica il valore della chiave sul nuovo valore ottenuto, viene acquisito il blocco di scrittura della chiave.</span><span class="sxs-lookup"><span data-stu-id="e42b0-114">Since AddAsync modifies the key’s value to the new, passed-in value, the key’s write lock is taken.</span></span> <span data-ttu-id="e42b0-115">Pertanto, se 2 (o più) thread tentano di aggiungere i valori alla stessa chiave nello stesso momento, un thread acquisirà il blocco di scrittura e gli altri verranno bloccati.</span><span class="sxs-lookup"><span data-stu-id="e42b0-115">So, if 2 (or more) threads attempt to add values with the same key at the same time, one thread will acquire the write lock and the other threads will block.</span></span> <span data-ttu-id="e42b0-116">Per impostazione predefinita, i metodi si interrompono fino a 4 secondi per acquisire il blocco; dopo 4 secondi, i metodi generano un'eccezione TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="e42b0-116">By default, methods block for up to 4 seconds to acquire the lock; after 4 seconds, the methods throw a TimeoutException.</span></span> <span data-ttu-id="e42b0-117">Se si preferisce, esistono overload del metodo che consentono di superare un valore di timeout esplicito.</span><span class="sxs-lookup"><span data-stu-id="e42b0-117">Method overloads exist allowing you to pass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="e42b0-118">In genere, si scrive il codice per reagire a un'eccezione TimeoutException rilevandola e tentando di effettuare nuovamente l'intera operazione (come illustrato nel codice precedente).</span><span class="sxs-lookup"><span data-stu-id="e42b0-118">Usually, you write your code to react to a TimeoutException by catching it and retrying the entire operation (as shown in the code above).</span></span> <span data-ttu-id="e42b0-119">In questo codice semplice, si sta chiamando ogni volta Task.Delay oltre i 100 millisecondi.</span><span class="sxs-lookup"><span data-stu-id="e42b0-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="e42b0-120">In realtà, potrebbe essere più opportuno usare un tipo di ritardo backoff esponenziale.</span><span class="sxs-lookup"><span data-stu-id="e42b0-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="e42b0-121">Una volta acquisito il blocco, AddAsync aggiunge i riferimenti dell'oggetto valore e chiave a un dizionario interno temporaneo associato all'oggetto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="e42b0-121">Once the lock is acquired, AddAsync adds the key and value object references to an internal temporary dictionary associated with the ITransaction object.</span></span> <span data-ttu-id="e42b0-122">Questa operazione viene eseguita per fornire la semantica di autolettura delle proprie scritture.</span><span class="sxs-lookup"><span data-stu-id="e42b0-122">This is done to provide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="e42b0-123">Vale a dire che, dopo aver chiamato AddAsync, una chiamata successiva a TryGetValueAsync (usando lo stesso oggetto ITransaction) restituirà il valore anche se non si è eseguito il commit della transazione.</span><span class="sxs-lookup"><span data-stu-id="e42b0-123">That is, after you call AddAsync, a later call to TryGetValueAsync (using the same ITransaction object) will return the value even if you have not yet committed the transaction.</span></span> <span data-ttu-id="e42b0-124">Successivamente, AddAsync serializza gli oggetti di chiave e valore in array di byte e aggiunge gli array a un file di log sul nodo locale.</span><span class="sxs-lookup"><span data-stu-id="e42b0-124">Next, AddAsync serializes your key and value objects to byte arrays and appends these byte arrays to a log file on the local node.</span></span> <span data-ttu-id="e42b0-125">Infine, AddAsync invia gli array di byte di tutte le repliche secondarie in modo che abbiano le stesse informazioni chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="e42b0-125">Finally, AddAsync sends the byte arrays to all the secondary replicas so they have the same key/value information.</span></span> <span data-ttu-id="e42b0-126">Anche se le informazioni chiave/valore sono stato scritte in un file di log, le informazioni non vengono considerate parte del dizionario fino a quando non è stato eseguito il commit della transazione a cui sono associate.</span><span class="sxs-lookup"><span data-stu-id="e42b0-126">Even though the key/value information has been written to a log file, the information is not considered part of the dictionary until the transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="e42b0-127">Nel codice precedente, la chiamata a CommitAsync esegue il commit di tutte le operazioni della transazione.</span><span class="sxs-lookup"><span data-stu-id="e42b0-127">In the code above, the call to CommitAsync commits all of the transaction’s operations.</span></span> <span data-ttu-id="e42b0-128">In particolare, aggiunge informazioni di commit al file di log sul nodo locale e invia anche il record di commit a tutte le repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="e42b0-128">Specifically, it appends commit information to the log file on the local node and also sends the commit record to all the secondary replicas.</span></span> <span data-ttu-id="e42b0-129">Una volta ricevuta la risposta da un quorum (maggioranza) delle repliche, tutte le modifiche ai dati vengono considerate permanenti e i blocchi associati alle chiavi modificate tramite l'oggetto ITransaction vengono rilasciati in modo che altri thread/transazioni possano modificare le stesse chiavi e i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="e42b0-129">Once a quorum (majority) of the replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via the ITransaction object are released so other threads/transactions can manipulate the same keys and their values.</span></span>

<span data-ttu-id="e42b0-130">Se CommitAsync non viene chiamato (in genere a causa di un'eccezione generata), l'oggetto ITransaction viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="e42b0-130">If CommitAsync is not called (usually due to an exception being thrown), then the ITransaction object gets disposed.</span></span> <span data-ttu-id="e42b0-131">Quando viene eliminato un oggetto ITransaction su cui non è stato eseguito il commit, Service Fabric aggiunge informazioni sull'interruzione al file di log del nodo locale e non è necessario inviare alcun elemento alle repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="e42b0-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information to the local node’s log file and nothing needs to be sent to any of the secondary replicas.</span></span> <span data-ttu-id="e42b0-132">A quel punto, i blocchi associati alle chiavi modificate tramite la transazione vengono rilasciati.</span><span class="sxs-lookup"><span data-stu-id="e42b0-132">And then, any locks associated with keys that were manipulated via the transaction are released.</span></span>

## <a name="common-pitfalls-and-how-to-avoid-them"></a><span data-ttu-id="e42b0-133">Inconvenienti comuni e come evitarli</span><span class="sxs-lookup"><span data-stu-id="e42b0-133">Common pitfalls and how to avoid them</span></span>
<span data-ttu-id="e42b0-134">Dopo averne appreso il funzionamento interno, ecco alcuni casi di uso improprio delle Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="e42b0-134">Now that you understand how the reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="e42b0-135">Osserviamo il seguente codice:</span><span class="sxs-lookup"><span data-stu-id="e42b0-135">See the code below:</span></span>

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes the name/user, logs the bytes,
   // & sends the bytes to the secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // The line below updates the property’s value in memory only; the
   // new value is NOT serialized, logged, & sent to secondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

<span data-ttu-id="e42b0-136">Quando si usa un normale dizionario .NET, è possibile aggiungere una coppia chiave/valore al dizionario e quindi modificare il valore di una proprietà (ad esempio LastLogin).</span><span class="sxs-lookup"><span data-stu-id="e42b0-136">When working with a regular .NET dictionary, you can add a key/value to the dictionary and then change the value of a property (such as LastLogin).</span></span> <span data-ttu-id="e42b0-137">Tuttavia, questo codice non funziona correttamente con un ReliableDictionary.</span><span class="sxs-lookup"><span data-stu-id="e42b0-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="e42b0-138">Come visto in precedenza, la chiamata ad AddAsync serializza gli oggetti chiave/valore agli array di byte, salva gli array in un file locale e invia gli array anche alle repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="e42b0-138">Remember from the earlier discussion, the call to AddAsync serializes the key/value objects to byte arrays and then saves the arrays to a local file and also sends them to the secondary replicas.</span></span> <span data-ttu-id="e42b0-139">Se successivamente si modifica una proprietà, questa operazione modifica il valore della proprietà solo nella memoria, senza influire sul file locale o sui dati inviati alle repliche.</span><span class="sxs-lookup"><span data-stu-id="e42b0-139">If you later change a property, this changes the property’s value in memory only; it does not impact the local file or the data sent to the replicas.</span></span> <span data-ttu-id="e42b0-140">Se il processo si arresta in modo anomalo, il contenuto della memoria viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="e42b0-140">If the process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="e42b0-141">Quando viene avviato un nuovo processo o un'altra replica diventa primaria, è disponibile il valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="e42b0-141">When a new process starts or if another replica becomes primary, then the old property value is what is available.</span></span>

<span data-ttu-id="e42b0-142">Non è possibile sottolineare a sufficienza quanto sia semplice effettuare l'errore descritto in alto.</span><span class="sxs-lookup"><span data-stu-id="e42b0-142">I cannot stress enough how easy it is to make the kind of mistake shown above.</span></span> <span data-ttu-id="e42b0-143">Sarà possibile apprendere l'errore solo se/quando il processo si interrompe.</span><span class="sxs-lookup"><span data-stu-id="e42b0-143">And, you will only learn about the mistake if/when the process goes down.</span></span> <span data-ttu-id="e42b0-144">Il modo corretto per scrivere il codice è semplicemente invertire le due righe:</span><span class="sxs-lookup"><span data-stu-id="e42b0-144">The correct way to write the code is simply to reverse the two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="e42b0-145">Ecco un altro esempio che mostra un errore comune:</span><span class="sxs-lookup"><span data-stu-id="e42b0-145">Here is another example showing a common mistake:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (user.HasValue) {
      // The line below updates the property’s value in memory only; the
      // new value is NOT serialized, logged, & sent to secondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

<span data-ttu-id="e42b0-146">Anche qui, con i dizionari regolari .NET, il codice indicato in alto funziona correttamente ed è un modello comune: lo sviluppatore usa una chiave per cercare un valore.</span><span class="sxs-lookup"><span data-stu-id="e42b0-146">Again, with regular .NET dictionaries, the code above works fine and is a common pattern: the developer uses a key to look up a value.</span></span> <span data-ttu-id="e42b0-147">Se il valore esiste, lo sviluppatore modifica un valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="e42b0-147">If the value exists, the developer changes a property’s value.</span></span> <span data-ttu-id="e42b0-148">Con le raccolte Reliable Collections, tuttavia, questo codice presenta lo stesso problema già illustrato: **non SI DEVE modificare un oggetto dopo averlo assegnato a una raccolta Reliable Collections.**</span><span class="sxs-lookup"><span data-stu-id="e42b0-148">However, with reliable collections, this code exhibits the same problem as already discussed: **you MUST not modify an object once you have given it to a reliable collection.**</span></span>

<span data-ttu-id="e42b0-149">Il modo corretto per aggiornare un valore in una raccolta Reliable Collections è fare riferimento al valore esistente e tenere in considerazione l'oggetto a cui fa riferimento tramite il riferimento non modificabile.</span><span class="sxs-lookup"><span data-stu-id="e42b0-149">The correct way to update a value in a reliable collection, is to get a reference to the existing value and consider the object referred to by this reference immutable.</span></span> <span data-ttu-id="e42b0-150">Quindi, creare un nuovo oggetto come copia esatta dell'oggetto originale.</span><span class="sxs-lookup"><span data-stu-id="e42b0-150">Then, create a new object which is an exact copy of the original object.</span></span> <span data-ttu-id="e42b0-151">A questo punto, è possibile modificare lo stato di questo nuovo oggetto e scrivere il nuovo oggetto nella raccolta in modo che venga serializzato in array di byte, aggiunto al file locale e inviato alle repliche.</span><span class="sxs-lookup"><span data-stu-id="e42b0-151">Now, you can modify the state of this new object and write the new object into the collection so that it gets serialized to byte arrays, appended to the local file and sent to the replicas.</span></span> <span data-ttu-id="e42b0-152">Dopo aver eseguito il commit delle modifiche, gli oggetti interni alla memoria, il file locale e tutte le repliche hanno lo stesso stato.</span><span class="sxs-lookup"><span data-stu-id="e42b0-152">After committing the change(s), the in-memory objects, the local file, and all the replicas have the same exact state.</span></span> <span data-ttu-id="e42b0-153">Tutto è in posizione.</span><span class="sxs-lookup"><span data-stu-id="e42b0-153">All is good!</span></span>

<span data-ttu-id="e42b0-154">Il codice seguente illustra il modo corretto per aggiornare un valore in una raccolta Reliable Collections:</span><span class="sxs-lookup"><span data-stu-id="e42b0-154">The code below shows the correct way to update a value in a reliable collection:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with the same state as the current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In the new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update the key’s value to the updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-to-prevent-programmer-error"></a><span data-ttu-id="e42b0-155">Definire tipi di dati non modificabili per evitare errori del programmatore</span><span class="sxs-lookup"><span data-stu-id="e42b0-155">Define immutable data types to prevent programmer error</span></span>
<span data-ttu-id="e42b0-156">Idealmente, il compilatore dovrebbe segnalare gli errori quando si crea inavvertitamente codice che modifica lo stato di un oggetto considerato non modificabile.</span><span class="sxs-lookup"><span data-stu-id="e42b0-156">Ideally, we’d like the compiler to report errors when you accidentally produce code that mutates state of an object that you are supposed to consider immutable.</span></span> <span data-ttu-id="e42b0-157">Tuttavia, il compilatore C# non è in grado di farlo.</span><span class="sxs-lookup"><span data-stu-id="e42b0-157">But, the C# compiler does not have the ability to do this.</span></span> <span data-ttu-id="e42b0-158">Pertanto, per evitare potenziali errori del programmatore, si consiglia di definire i tipi da usare con le raccolte Reliable Collections come tipi non modificabili.</span><span class="sxs-lookup"><span data-stu-id="e42b0-158">So, to avoid potential programmer bugs, we highly recommend that you define the types you use with reliable collections to be immutable types.</span></span> <span data-ttu-id="e42b0-159">In particolare, questo significa che è opportuno fermarsi ai principali tipi di valore (ad esempio numeri [Int32, UInt64, etc.], DateTime, Guid, TimeSpan e simili).</span><span class="sxs-lookup"><span data-stu-id="e42b0-159">Specifically, this means that you stick to core value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and the like).</span></span> <span data-ttu-id="e42b0-160">E, ovviamente, è anche possibile usare le stringhe.</span><span class="sxs-lookup"><span data-stu-id="e42b0-160">And, of course, you can also use String.</span></span> <span data-ttu-id="e42b0-161">È preferibile evitare proprietà della raccolta poiché la serializzazione e la deserializzazione può spesso influire negativamente sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e42b0-161">It is best to avoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="e42b0-162">Tuttavia, se si intende usare le proprietà della raccolta, è consigliabile l'uso di libreria di raccolte .NET non modificabili ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="e42b0-162">However, if you want to use collection properties, we highly recommend the use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="e42b0-163">Questa libreria è disponibile per il download all'indirizzo http://nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e42b0-163">This library is available for download from http://nuget.org.</span></span> <span data-ttu-id="e42b0-164">Si consiglia anche di sigillare le classi e rendere i campi di sola lettura quando possibile.</span><span class="sxs-lookup"><span data-stu-id="e42b0-164">We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="e42b0-165">Il tipo UserInfo riportato di seguito mostra come definire un tipo non modificabile sfruttando i consigli indicati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e42b0-165">The UserInfo type below demonstrates how to define an immutable type taking advantage of aforementioned recommendations.</span></span>

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert the deserialized collection to an immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has to set it. So instead, the getter is public and the setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId to the ItemsBidding
   // collection by creating a new immutable UserInfo object with the added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

<span data-ttu-id="e42b0-166">Anche ItemId è un tipo non modificabile, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e42b0-166">The ItemId type is also an immutable type as shown here:</span></span>

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="e42b0-167">Controllo delle versioni dello schema (aggiornamenti)</span><span class="sxs-lookup"><span data-stu-id="e42b0-167">Schema versioning (upgrades)</span></span>
<span data-ttu-id="e42b0-168">Internamente, le raccolte Reliable Collections serializzano gli oggetti usando DataContractSerializer di .NET.</span><span class="sxs-lookup"><span data-stu-id="e42b0-168">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="e42b0-169">Gli oggetti serializzati sono persistenti sul disco locale della replica primaria e vengono anche trasmessi alle repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="e42b0-169">The serialized objects are persisted to the primary replica’s local disk and are also transmitted to the secondary replicas.</span></span> <span data-ttu-id="e42b0-170">Con l'evoluzione del servizio, è probabile che si desideri modificare il tipo di dati (schema) richiesti dal servizio.</span><span class="sxs-lookup"><span data-stu-id="e42b0-170">As your service matures, it’s likely you’ll want to change the kind of data (schema) your service requires.</span></span> <span data-ttu-id="e42b0-171">Il controllo delle versioni dei dati deve essere eseguito con estrema attenzione.</span><span class="sxs-lookup"><span data-stu-id="e42b0-171">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="e42b0-172">Innanzitutto, si deve essere sempre in grado di deserializzare i dati precedenti.</span><span class="sxs-lookup"><span data-stu-id="e42b0-172">First and foremost, you must always be able to deserialize old data.</span></span> <span data-ttu-id="e42b0-173">In particolare, ciò significa che il codice di deserializzazione deve essere infinitamente compatibile con le versioni precedenti: la versione 333 del codice del servizio deve essere in grado di operare sui dati inseriti in una raccolta Reliable Collections dalla versione 1 del codice del servizio 5 anni fa.</span><span class="sxs-lookup"><span data-stu-id="e42b0-173">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able to operate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="e42b0-174">Il codice del servizio viene aggiornato un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="e42b0-174">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="e42b0-175">Pertanto, durante un aggiornamento, vengono eseguite contemporaneamente due diverse versioni del codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="e42b0-175">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="e42b0-176">È necessario evitare che la nuova versione del codice del servizio usi il nuovo schema dal momento che le versioni precedenti del codice del servizio potrebbero non essere in grado di gestire il nuovo schema.</span><span class="sxs-lookup"><span data-stu-id="e42b0-176">You must avoid having the new version of your service code use the new schema as old versions of your service code might not be able to handle the new schema.</span></span> <span data-ttu-id="e42b0-177">Quando possibile, si consiglia di progettare ogni versione del servizio perché sia compatibile con tutte le versioni precedenti, a partire dalla versione 1.</span><span class="sxs-lookup"><span data-stu-id="e42b0-177">When possible, you should design each version of your service to be forward compatible by 1 version.</span></span> <span data-ttu-id="e42b0-178">In particolare, questo significa che V1 del codice del servizio deve essere in grado di ignorare tutti gli elementi dello schema che non vengono gestiti in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="e42b0-178">Specifically, this means that V1 of your service code should be able to simply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="e42b0-179">Tuttavia, deve essere in grado di salvare i dati che non conosce in modo esplicito e riscriverli quando si aggiorna il valore o la chiave del dizionario.</span><span class="sxs-lookup"><span data-stu-id="e42b0-179">However, it must be able to save any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="e42b0-180">Sebbene sia possibile modificare lo schema di una chiave, è necessario assicurarsi che il codice hash e l'algoritmo di uguaglianza della chiave siano stabili.</span><span class="sxs-lookup"><span data-stu-id="e42b0-180">While you can modify the schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="e42b0-181">Se si modifica il funzionamento di questi algoritmi, non sarà più possibile cercare la chiave all'interno del ReliableDictionary.</span><span class="sxs-lookup"><span data-stu-id="e42b0-181">If you change how either of these algorithms operate, you will not be able to look up the key within the reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="e42b0-182">In alternativa, è possibile eseguire un aggiornamento noto come aggiornamento a 2 fasi.</span><span class="sxs-lookup"><span data-stu-id="e42b0-182">Alternatively, you can perform what is typically referred to as a 2-phase upgrade.</span></span> <span data-ttu-id="e42b0-183">Con un aggiornamento a 2 fasi, viene effettuato l'aggiornamento del servizio da V1 a V2: V2 contiene il codice in grado di gestire la nuova modifica dello schema, che non può essere eseguito.</span><span class="sxs-lookup"><span data-stu-id="e42b0-183">With a 2-phase upgrade, you upgrade your service from V1 to V2: V2 contains the code that knows how to deal with the new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="e42b0-184">Quando il codice V2 legge i dati V1, opera su di esso e scrive i dati V1.</span><span class="sxs-lookup"><span data-stu-id="e42b0-184">When the V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="e42b0-185">Quindi, al termine dell'aggiornamento di tutti i domini di aggiornamento, è possibile in qualche modo segnalare alle istanze V2 in esecuzione che l'aggiornamento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="e42b0-185">Then, after the upgrade is complete across all upgrade domains, you can somehow signal to the running V2 instances that the upgrade is complete.</span></span> <span data-ttu-id="e42b0-186">(uno modo consiste nell'implementare un aggiornamento della configurazione; ovvero un aggiornamento a 2 fasi). A questo punto, le istanze V2 possono leggere i dati V1, convertirli in dati V2, operare su di essi e scriverli nella forma di dati V2.</span><span class="sxs-lookup"><span data-stu-id="e42b0-186">(One way to signal this is to roll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, the V2 instances can read V1 data, convert it to V2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="e42b0-187">Quando altre istanze leggono i dati V2, non è necessario convertirli: possono operano su di essi e scrivere dati V2.</span><span class="sxs-lookup"><span data-stu-id="e42b0-187">When other instances read V2 data, they do not need to convert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e42b0-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e42b0-188">Next Steps</span></span>
<span data-ttu-id="e42b0-189">Per informazioni sulla creazione di contratti dati compatibili con versioni successive, vedere [Contratti dati compatibili con versioni successive](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="e42b0-189">To learn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="e42b0-190">Per informazioni sulle procedure consigliate per il controllo delle versioni dei contratti dati, vedere [Controllo delle versioni dei contratti dati](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="e42b0-190">To learn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="e42b0-191">Per informazioni su come implementare contratti dati a tolleranza di versione, vedere [Callback di serializzazione a tolleranza di versione](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="e42b0-191">To learn how to implement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="e42b0-192">Per informazioni su come fornire una struttura di dati che può interagire con più versioni, vedere [Interfaccia IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="e42b0-192">To learn how to provide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
