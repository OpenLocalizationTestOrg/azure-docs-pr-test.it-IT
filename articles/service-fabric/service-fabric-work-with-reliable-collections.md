---
title: aaaWorking con le raccolte affidabile | Documenti Microsoft
description: Hello le procedure consigliate per l'utilizzo di raccolte affidabile.
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
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a><span data-ttu-id="64063-103">Lavorare con le raccolte Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="64063-103">Working with Reliable Collections</span></span>
<span data-ttu-id="64063-104">Service Fabric offre un con stato sviluppatori too.NET disponibili di modelli tramite raccolte affidabile di programmazione.</span><span class="sxs-lookup"><span data-stu-id="64063-104">Service Fabric offers a stateful programming model available too.NET developers via Reliable Collections.</span></span> <span data-ttu-id="64063-105">In particolare, Service Fabric offre classi ReliableDictionary e ReliableQueue.</span><span class="sxs-lookup"><span data-stu-id="64063-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="64063-106">Quando si usano queste classi, lo stato è partizionato (per la scalabilità), replicato (per la disponibilità) e le transazioni vengono eseguite all'interno di una partizione (per la semantica ACID).</span><span class="sxs-lookup"><span data-stu-id="64063-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="64063-107">Di seguito viene descritto l'uso tipico di un oggetto ReliableDictionary per osservarne le azioni.</span><span class="sxs-lookup"><span data-stu-id="64063-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

<span data-ttu-id="64063-108">Tutte le operazioni sugli oggetti ReliableDictionary (ad eccezione di ClearAsync che non è annullabile) richiedono un oggetto ITransaction.</span><span class="sxs-lookup"><span data-stu-id="64063-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="64063-109">Questo oggetto è associato a qualsiasi modifiche che si sta tentando di toomake tooany affidabile dizionario e/o gli oggetti di coda affidabile all'interno di una singola partizione.</span><span class="sxs-lookup"><span data-stu-id="64063-109">This object has associated with it any and all changes you’re attempting toomake tooany reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="64063-110">Acquisire un ITransaction oggetto chiamando partizione hello del metodo CreateTransaction di StateManager.</span><span class="sxs-lookup"><span data-stu-id="64063-110">You acquire an ITransaction object by calling hello partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="64063-111">Nel codice hello precedente oggetto ITransaction hello viene passato metodo AddAsync del dizionario di tooa affidabile.</span><span class="sxs-lookup"><span data-stu-id="64063-111">In hello code above, hello ITransaction object is passed tooa reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="64063-112">Internamente, i metodi di dizionario che accetta una chiave di acquisire un blocco di lettura/scrittura associato alla chiave hello.</span><span class="sxs-lookup"><span data-stu-id="64063-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with hello key.</span></span> <span data-ttu-id="64063-113">Se il metodo hello consente di modificare il valore della chiave di hello, metodo hello acquisisce un blocco di scrittura sulla chiave hello e se il metodo hello legge solo dal valore della chiave di hello, quindi un blocco di lettura viene eseguito sulla chiave hello.</span><span class="sxs-lookup"><span data-stu-id="64063-113">If hello method modifies hello key’s value, hello method takes a write lock on hello key and if hello method only reads from hello key’s value, then a read lock is taken on hello key.</span></span> <span data-ttu-id="64063-114">Poiché AddAsync modifica toohello valore della chiave hello nuovo, viene utilizzato valore passato, il blocco di scrittura della chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="64063-114">Since AddAsync modifies hello key’s value toohello new, passed-in value, hello key’s write lock is taken.</span></span> <span data-ttu-id="64063-115">In tal caso, se i thread 2 (o più) tentano tooadd valori con hello stessa chiave in hello stesso tempo un thread acquisisce il blocco di scrittura hello e hello altri thread verrà bloccata.</span><span class="sxs-lookup"><span data-stu-id="64063-115">So, if 2 (or more) threads attempt tooadd values with hello same key at hello same time, one thread will acquire hello write lock and hello other threads will block.</span></span> <span data-ttu-id="64063-116">Per impostazione predefinita, il blocco di metodi per i blocchi di hello tooacquire secondi too4; dopo 4 secondi e i metodi di hello generano un TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="64063-116">By default, methods block for up too4 seconds tooacquire hello lock; after 4 seconds, hello methods throw a TimeoutException.</span></span> <span data-ttu-id="64063-117">Se si preferisce, gli overload del metodo esiste consentendo si toopass un valore di timeout esplicito.</span><span class="sxs-lookup"><span data-stu-id="64063-117">Method overloads exist allowing you toopass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="64063-118">In genere, si scrive il tooa tooreact codice TimeoutException rilevandola e ritentare l'intera operazione hello (come illustrato nel codice hello sopra).</span><span class="sxs-lookup"><span data-stu-id="64063-118">Usually, you write your code tooreact tooa TimeoutException by catching it and retrying hello entire operation (as shown in hello code above).</span></span> <span data-ttu-id="64063-119">In questo codice semplice, si sta chiamando ogni volta Task.Delay oltre i 100 millisecondi.</span><span class="sxs-lookup"><span data-stu-id="64063-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="64063-120">In realtà, potrebbe essere più opportuno usare un tipo di ritardo backoff esponenziale.</span><span class="sxs-lookup"><span data-stu-id="64063-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="64063-121">Una volta che viene acquisito il blocco di hello, AddAsync aggiunge chiave hello e tooan dizionario temporaneo interno associato hello ITransaction oggetto fa riferimento a oggetto valore.</span><span class="sxs-lookup"><span data-stu-id="64063-121">Once hello lock is acquired, AddAsync adds hello key and value object references tooan internal temporary dictionary associated with hello ITransaction object.</span></span> <span data-ttu-id="64063-122">Questa operazione viene eseguita tooprovide si con la semantica di operazioni di lettura-your-proprietari-scrittura.</span><span class="sxs-lookup"><span data-stu-id="64063-122">This is done tooprovide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="64063-123">Vale a dire, dopo aver chiamato AddAsync, un tooTryGetValueAsync chiamata successiva (utilizzando hello stesso oggetto ITransaction) restituirà il valore di hello anche se non si è ancora commit transazione hello.</span><span class="sxs-lookup"><span data-stu-id="64063-123">That is, after you call AddAsync, a later call tooTryGetValueAsync (using hello same ITransaction object) will return hello value even if you have not yet committed hello transaction.</span></span> <span data-ttu-id="64063-124">Successivamente, AddAsync serializza la chiave e valore toobyte matrici di oggetti e aggiunge questi file di log tooa matrici byte nel nodo locale hello.</span><span class="sxs-lookup"><span data-stu-id="64063-124">Next, AddAsync serializes your key and value objects toobyte arrays and appends these byte arrays tooa log file on hello local node.</span></span> <span data-ttu-id="64063-125">Infine, AddAsync invia hello byte matrici tooall hello repliche secondarie in modo che hanno hello stessa chiave/valore informazioni.</span><span class="sxs-lookup"><span data-stu-id="64063-125">Finally, AddAsync sends hello byte arrays tooall hello secondary replicas so they have hello same key/value information.</span></span> <span data-ttu-id="64063-126">Anche se le informazioni chiave/valore hello sono stato scritto il file di log tooa, informazioni di hello non viene considerate parte del dizionario hello finché non è stato eseguito il commit delle transazioni hello che sono associate.</span><span class="sxs-lookup"><span data-stu-id="64063-126">Even though hello key/value information has been written tooa log file, hello information is not considered part of hello dictionary until hello transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="64063-127">Nel codice hello sopra riportato, hello chiamata tooCommitAsync esegue il commit di tutte le operazioni della transazione hello.</span><span class="sxs-lookup"><span data-stu-id="64063-127">In hello code above, hello call tooCommitAsync commits all of hello transaction’s operations.</span></span> <span data-ttu-id="64063-128">In particolare, aggiunge file di log commit informazioni toohello nel nodo locale hello e invia anche repliche secondarie hello hello commit tooall record.</span><span class="sxs-lookup"><span data-stu-id="64063-128">Specifically, it appends commit information toohello log file on hello local node and also sends hello commit record tooall hello secondary replicas.</span></span> <span data-ttu-id="64063-129">Una volta che un quorum (maggioranza) delle repliche hello ha risposto, tutti i dati, le modifiche vengono considerate permanenti e i blocchi associati alle chiavi che sono state modificate tramite oggetto ITransaction hello vengono rilasciati in modo da altri thread/transazioni possono modificare hello stesse chiavi e i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="64063-129">Once a quorum (majority) of hello replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via hello ITransaction object are released so other threads/transactions can manipulate hello same keys and their values.</span></span>

<span data-ttu-id="64063-130">Se a CommitAsync non viene chiamato (in genere a causa la generazione di eccezione tooan), l'oggetto ITransaction hello Ottiene eliminato.</span><span class="sxs-lookup"><span data-stu-id="64063-130">If CommitAsync is not called (usually due tooan exception being thrown), then hello ITransaction object gets disposed.</span></span> <span data-ttu-id="64063-131">Quando esegue l'eliminazione di un oggetto ITransaction Commit, Service Fabric aggiunge file di log interruzione informazioni toohello del nodo locale e non è necessario toobe inviato tooany di hello repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="64063-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information toohello local node’s log file and nothing needs toobe sent tooany of hello secondary replicas.</span></span> <span data-ttu-id="64063-132">E quindi, in cui vengono rilasciati i blocchi associati alle chiavi che sono state modificate tramite la transazione hello.</span><span class="sxs-lookup"><span data-stu-id="64063-132">And then, any locks associated with keys that were manipulated via hello transaction are released.</span></span>

## <a name="common-pitfalls-and-how-tooavoid-them"></a><span data-ttu-id="64063-133">Problemi comuni e come tooavoid li</span><span class="sxs-lookup"><span data-stu-id="64063-133">Common pitfalls and how tooavoid them</span></span>
<span data-ttu-id="64063-134">Ora che si informazioni sul funzionano delle raccolte affidabile hello internamente, esaminiamo un alcuni usi impropri comuni di essi.</span><span class="sxs-lookup"><span data-stu-id="64063-134">Now that you understand how hello reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="64063-135">Vedere codice hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="64063-135">See hello code below:</span></span>

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

<span data-ttu-id="64063-136">Quando si lavora con un dizionario regolari di .NET, è possibile aggiungere un dizionario toohello chiave/valore e quindi modificare il valore di hello di una proprietà (ad esempio LastLogin).</span><span class="sxs-lookup"><span data-stu-id="64063-136">When working with a regular .NET dictionary, you can add a key/value toohello dictionary and then change hello value of a property (such as LastLogin).</span></span> <span data-ttu-id="64063-137">Tuttavia, questo codice non funziona correttamente con un ReliableDictionary.</span><span class="sxs-lookup"><span data-stu-id="64063-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="64063-138">Ricordare di hello discussione precedente, chiamata hello tooAddAsync serializza hello chiave/valore oggetti toobyte matrici e quindi Salva hello matrici tooa file locale e le invia inoltre repliche secondarie toohello.</span><span class="sxs-lookup"><span data-stu-id="64063-138">Remember from hello earlier discussion, hello call tooAddAsync serializes hello key/value objects toobyte arrays and then saves hello arrays tooa local file and also sends them toohello secondary replicas.</span></span> <span data-ttu-id="64063-139">Se in seguito si modifica una proprietà, questo viene modificato il valore della proprietà hello in memoria. non ha impatto sul file locale hello o dati di hello inviati toohello repliche.</span><span class="sxs-lookup"><span data-stu-id="64063-139">If you later change a property, this changes hello property’s value in memory only; it does not impact hello local file or hello data sent toohello replicas.</span></span> <span data-ttu-id="64063-140">Se il processo di hello arresti anomali, novità in memoria viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="64063-140">If hello process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="64063-141">Quando un nuovo processo viene avviato o se un'altra replica diventa primaria, quindi hello valore precedente della proprietà è ciò che è disponibile.</span><span class="sxs-lookup"><span data-stu-id="64063-141">When a new process starts or if another replica becomes primary, then hello old property value is what is available.</span></span>

<span data-ttu-id="64063-142">Non si sottolinea sufficientemente quanto sia facile tipo hello toomake di errore illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="64063-142">I cannot stress enough how easy it is toomake hello kind of mistake shown above.</span></span> <span data-ttu-id="64063-143">E si solo apprenderà errore hello se/quando si arresta il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="64063-143">And, you will only learn about hello mistake if/when hello process goes down.</span></span> <span data-ttu-id="64063-144">codice hello toowrite modo corretto di Hello è semplicemente tooreverse hello due righe:</span><span class="sxs-lookup"><span data-stu-id="64063-144">hello correct way toowrite hello code is simply tooreverse hello two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="64063-145">Ecco un altro esempio che mostra un errore comune:</span><span class="sxs-lookup"><span data-stu-id="64063-145">Here is another example showing a common mistake:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

<span data-ttu-id="64063-146">Nuovamente, con regolari dizionari di .NET, codice hello sopra funziona correttamente ed è un modello comune: developer hello utilizza una chiave toolook un valore.</span><span class="sxs-lookup"><span data-stu-id="64063-146">Again, with regular .NET dictionaries, hello code above works fine and is a common pattern: hello developer uses a key toolook up a value.</span></span> <span data-ttu-id="64063-147">Se il valore di hello esiste, hello imposta un valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="64063-147">If hello value exists, hello developer changes a property’s value.</span></span> <span data-ttu-id="64063-148">Con le raccolte affidabile, tuttavia, questo codice presenta hello stesso problema come già illustrato: **è necessario non modificare un oggetto dopo che aver assegnato tooa affidabile insieme.**</span><span class="sxs-lookup"><span data-stu-id="64063-148">However, with reliable collections, this code exhibits hello same problem as already discussed: **you MUST not modify an object once you have given it tooa reliable collection.**</span></span>

<span data-ttu-id="64063-149">Hello corretto tooupdate modo un valore in un insieme affidabile, si riferisce tooget toohello esistente e provare a oggetto hello cui tooby questo riferimento non modificabile.</span><span class="sxs-lookup"><span data-stu-id="64063-149">hello correct way tooupdate a value in a reliable collection, is tooget a reference toohello existing value and consider hello object referred tooby this reference immutable.</span></span> <span data-ttu-id="64063-150">Quindi, creare un nuovo oggetto che è una copia esatta dell'oggetto originale hello.</span><span class="sxs-lookup"><span data-stu-id="64063-150">Then, create a new object which is an exact copy of hello original object.</span></span> <span data-ttu-id="64063-151">A questo punto, è possibile modificare lo stato di hello di questo nuovo oggetto e scrivere hello nuovo oggetto nella raccolta hello in modo che si ottiene serializzato toobyte matrici, file locale toohello aggiunti e inviati toohello repliche.</span><span class="sxs-lookup"><span data-stu-id="64063-151">Now, you can modify hello state of this new object and write hello new object into hello collection so that it gets serialized toobyte arrays, appended toohello local file and sent toohello replicas.</span></span> <span data-ttu-id="64063-152">Dopo il commit di hello modifiche agli oggetti in memoria hello, file locale hello, in modo che tutte le repliche di hello hello stesso stato.</span><span class="sxs-lookup"><span data-stu-id="64063-152">After committing hello change(s), hello in-memory objects, hello local file, and all hello replicas have hello same exact state.</span></span> <span data-ttu-id="64063-153">Tutto è in posizione.</span><span class="sxs-lookup"><span data-stu-id="64063-153">All is good!</span></span>

<span data-ttu-id="64063-154">Hello di codice seguente viene mostrato hello modo corretto tooupdate un valore in un insieme affidabile:</span><span class="sxs-lookup"><span data-stu-id="64063-154">hello code below shows hello correct way tooupdate a value in a reliable collection:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a><span data-ttu-id="64063-155">Definire un errore del programmatore di tooprevent tipi di dati non modificabili</span><span class="sxs-lookup"><span data-stu-id="64063-155">Define immutable data types tooprevent programmer error</span></span>
<span data-ttu-id="64063-156">Idealmente, desideriamo tooreport gli errori del compilatore di hello quando si creano accidentalmente il codice che viene modificato lo stato di un oggetto, si dovrebbe tooconsider non modificabile.</span><span class="sxs-lookup"><span data-stu-id="64063-156">Ideally, we’d like hello compiler tooreport errors when you accidentally produce code that mutates state of an object that you are supposed tooconsider immutable.</span></span> <span data-ttu-id="64063-157">Ma, hello il compilatore c# non dispone di hello possibilità toodo questo.</span><span class="sxs-lookup"><span data-stu-id="64063-157">But, hello C# compiler does not have hello ability toodo this.</span></span> <span data-ttu-id="64063-158">In questo caso, tooavoid potenziali programmatore bug, è consigliabile definire i tipi di hello che usa con i tipi di raccolte affidabile toobe non modificabile.</span><span class="sxs-lookup"><span data-stu-id="64063-158">So, tooavoid potential programmer bugs, we highly recommend that you define hello types you use with reliable collections toobe immutable types.</span></span> <span data-ttu-id="64063-159">In particolare, ciò significa che si osserva toocore i tipi di valore (ad esempio numeri [Int32, UInt64, e così via.], DateTime, Guid, TimeSpan e hello simile).</span><span class="sxs-lookup"><span data-stu-id="64063-159">Specifically, this means that you stick toocore value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and hello like).</span></span> <span data-ttu-id="64063-160">E, ovviamente, è anche possibile usare le stringhe.</span><span class="sxs-lookup"><span data-stu-id="64063-160">And, of course, you can also use String.</span></span> <span data-ttu-id="64063-161">È una proprietà di raccolta tooavoid migliore come la serializzazione e deserializzazione li può spesso può ridurre le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="64063-161">It is best tooavoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="64063-162">Tuttavia, se si desidera toouse le proprietà della raccolta, è consigliabile utilizzare hello di. Libreria di raccolte non modificabili di rete ([Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="64063-162">However, if you want toouse collection properties, we highly recommend hello use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="64063-163">Questa libreria è disponibile per il download all'indirizzo http://nuget.org. Si consiglia anche di sigillare le classi e rendere i campi di sola lettura quando possibile.</span><span class="sxs-lookup"><span data-stu-id="64063-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="64063-164">Hello UserInfo tipo riportato di seguito viene illustrato come toodefine un non modificabile digitare sfruttando i consigli menzionati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="64063-164">hello UserInfo type below demonstrates how toodefine an immutable type taking advantage of aforementioned recommendations.</span></span>

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
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

<span data-ttu-id="64063-165">tipo ItemId Hello è anche un tipo immutabile, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="64063-165">hello ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="64063-166">Controllo delle versioni dello schema (aggiornamenti)</span><span class="sxs-lookup"><span data-stu-id="64063-166">Schema versioning (upgrades)</span></span>
<span data-ttu-id="64063-167">Internamente, le raccolte Reliable Collections serializzano gli oggetti usando DataContractSerializer di .NET.</span><span class="sxs-lookup"><span data-stu-id="64063-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="64063-168">gli oggetti serializzato Hello sono disco locale della replica primaria toohello persistente e trasmesso toohello repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="64063-168">hello serialized objects are persisted toohello primary replica’s local disk and are also transmitted toohello secondary replicas.</span></span> <span data-ttu-id="64063-169">Evoluzione del servizio, è probabile che si tipo hello toochange dei dati (schema), che il servizio lo richiede.</span><span class="sxs-lookup"><span data-stu-id="64063-169">As your service matures, it’s likely you’ll want toochange hello kind of data (schema) your service requires.</span></span> <span data-ttu-id="64063-170">Il controllo delle versioni dei dati deve essere eseguito con estrema attenzione.</span><span class="sxs-lookup"><span data-stu-id="64063-170">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="64063-171">In primo luogo, è necessario essere sempre in grado di toodeserialize vecchi dati.</span><span class="sxs-lookup"><span data-stu-id="64063-171">First and foremost, you must always be able toodeserialize old data.</span></span> <span data-ttu-id="64063-172">In particolare, questo significa che il codice di deserializzazione deve essere compatibile con le versioni precedenti all'infinito: 333 versione del codice del servizio deve essere in grado di toooperate sui dati inseriti in un insieme affidabile dalla versione 1 del codice del servizio 5 anni.</span><span class="sxs-lookup"><span data-stu-id="64063-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able toooperate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="64063-173">Il codice del servizio viene aggiornato un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="64063-173">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="64063-174">Pertanto, durante un aggiornamento, vengono eseguite contemporaneamente due diverse versioni del codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="64063-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="64063-175">È necessario evitare nuova versione di hello del codice del servizio utilizzano hello nuovo schema come le versioni precedenti del codice del servizio potrebbero non essere in grado di toohandle schema di nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="64063-175">You must avoid having hello new version of your service code use hello new schema as old versions of your service code might not be able toohandle hello new schema.</span></span> <span data-ttu-id="64063-176">Se possibile, è consigliabile progettare ogni versione del servizio toobe compatibile con le versioni di 1 versione.</span><span class="sxs-lookup"><span data-stu-id="64063-176">When possible, you should design each version of your service toobe forward compatible by 1 version.</span></span> <span data-ttu-id="64063-177">In particolare, ciò significa che V1 del codice del servizio deve essere in grado di toosimply ignorare tutti gli elementi dello schema non gestisce in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="64063-177">Specifically, this means that V1 of your service code should be able toosimply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="64063-178">Tuttavia, deve essere in grado di toosave tutti i dati non conoscere in modo esplicito e scriverlo semplicemente indietro quando si aggiorna un valore o la chiave del dizionario.</span><span class="sxs-lookup"><span data-stu-id="64063-178">However, it must be able toosave any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="64063-179">Mentre è possibile modificare lo schema di hello di una chiave, è necessario assicurarsi che sono stabili codice hash della chiave e algoritmi di equals.</span><span class="sxs-lookup"><span data-stu-id="64063-179">While you can modify hello schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="64063-180">Se si modifica uno di questi algoritmi funzionamento, non sarà in grado di toolook backup chiave di hello all'interno di dizionario affidabile hello mai nuovamente.</span><span class="sxs-lookup"><span data-stu-id="64063-180">If you change how either of these algorithms operate, you will not be able toolook up hello key within hello reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="64063-181">In alternativa, è possibile eseguire ciò che è in genere indicati tooas 2 fasi l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="64063-181">Alternatively, you can perform what is typically referred tooas a 2-phase upgrade.</span></span> <span data-ttu-id="64063-182">Con un aggiornamento della fase 2, aggiornare il servizio da V1 tooV2: V2 contiene codice hello che conosca toodeal con questo codice, nuova modifica dello schema di hello ma non la modalità di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="64063-182">With a 2-phase upgrade, you upgrade your service from V1 tooV2: V2 contains hello code that knows how toodeal with hello new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="64063-183">Quando hello V2 codice legge i dati di V1, opera su di esso e lo scrive dati V1.</span><span class="sxs-lookup"><span data-stu-id="64063-183">When hello V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="64063-184">Quindi, dopo l'aggiornamento di hello è stata completata in tutti i domini di aggiornamento, è possibile in qualche modo segnalare toohello le istanze di V2 in esecuzione che l'aggiornamento hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="64063-184">Then, after hello upgrade is complete across all upgrade domains, you can somehow signal toohello running V2 instances that hello upgrade is complete.</span></span> <span data-ttu-id="64063-185">(Unidirezionale toosignal tooroll un aggiornamento di configurazione; questo è ciò che crea un aggiornamento in fase di 2.) A questo punto, hello V2 istanze possono leggere i dati V1, convertirlo dati tooV2, operano su di esso e scriverlo sotto forma di dati V2.</span><span class="sxs-lookup"><span data-stu-id="64063-185">(One way toosignal this is tooroll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, hello V2 instances can read V1 data, convert it tooV2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="64063-186">Quando le altre istanze leggerli V2, non richiedono tooconvert, ma semplicemente operano su di esso e scrivere dati V2.</span><span class="sxs-lookup"><span data-stu-id="64063-186">When other instances read V2 data, they do not need tooconvert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64063-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64063-187">Next Steps</span></span>
<span data-ttu-id="64063-188">toolearn sulla creazione di contratti dati compatibili con, vedere [contratti dati compatibili con versioni](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="64063-188">toolearn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="64063-189">procedure consigliate di toolearn nei contratti dati di controllo delle versioni, vedere [controllo delle versioni del contratto dati](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="64063-189">toolearn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="64063-190">toolearn come i contratti dati a tolleranza di versione tooimplement, vedere [callback di serializzazione a tolleranza di versione](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="64063-190">toolearn how tooimplement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="64063-191">toolearn tooprovide una struttura di dati che può interagire tra più versioni, vedere [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="64063-191">toolearn how tooprovide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
