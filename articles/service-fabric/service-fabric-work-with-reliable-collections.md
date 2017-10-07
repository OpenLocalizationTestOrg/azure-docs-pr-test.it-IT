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
# <a name="working-with-reliable-collections"></a>Lavorare con le raccolte Reliable Collections
Service Fabric offre un con stato sviluppatori too.NET disponibili di modelli tramite raccolte affidabile di programmazione. In particolare, Service Fabric offre classi ReliableDictionary e ReliableQueue. Quando si usano queste classi, lo stato è partizionato (per la scalabilità), replicato (per la disponibilità) e le transazioni vengono eseguite all'interno di una partizione (per la semantica ACID). Di seguito viene descritto l'uso tipico di un oggetto ReliableDictionary per osservarne le azioni.

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

Tutte le operazioni sugli oggetti ReliableDictionary (ad eccezione di ClearAsync che non è annullabile) richiedono un oggetto ITransaction. Questo oggetto è associato a qualsiasi modifiche che si sta tentando di toomake tooany affidabile dizionario e/o gli oggetti di coda affidabile all'interno di una singola partizione. Acquisire un ITransaction oggetto chiamando partizione hello del metodo CreateTransaction di StateManager.

Nel codice hello precedente oggetto ITransaction hello viene passato metodo AddAsync del dizionario di tooa affidabile. Internamente, i metodi di dizionario che accetta una chiave di acquisire un blocco di lettura/scrittura associato alla chiave hello. Se il metodo hello consente di modificare il valore della chiave di hello, metodo hello acquisisce un blocco di scrittura sulla chiave hello e se il metodo hello legge solo dal valore della chiave di hello, quindi un blocco di lettura viene eseguito sulla chiave hello. Poiché AddAsync modifica toohello valore della chiave hello nuovo, viene utilizzato valore passato, il blocco di scrittura della chiave di hello. In tal caso, se i thread 2 (o più) tentano tooadd valori con hello stessa chiave in hello stesso tempo un thread acquisisce il blocco di scrittura hello e hello altri thread verrà bloccata. Per impostazione predefinita, il blocco di metodi per i blocchi di hello tooacquire secondi too4; dopo 4 secondi e i metodi di hello generano un TimeoutException. Se si preferisce, gli overload del metodo esiste consentendo si toopass un valore di timeout esplicito.

In genere, si scrive il tooa tooreact codice TimeoutException rilevandola e ritentare l'intera operazione hello (come illustrato nel codice hello sopra). In questo codice semplice, si sta chiamando ogni volta Task.Delay oltre i 100 millisecondi. In realtà, potrebbe essere più opportuno usare un tipo di ritardo backoff esponenziale.

Una volta che viene acquisito il blocco di hello, AddAsync aggiunge chiave hello e tooan dizionario temporaneo interno associato hello ITransaction oggetto fa riferimento a oggetto valore. Questa operazione viene eseguita tooprovide si con la semantica di operazioni di lettura-your-proprietari-scrittura. Vale a dire, dopo aver chiamato AddAsync, un tooTryGetValueAsync chiamata successiva (utilizzando hello stesso oggetto ITransaction) restituirà il valore di hello anche se non si è ancora commit transazione hello. Successivamente, AddAsync serializza la chiave e valore toobyte matrici di oggetti e aggiunge questi file di log tooa matrici byte nel nodo locale hello. Infine, AddAsync invia hello byte matrici tooall hello repliche secondarie in modo che hanno hello stessa chiave/valore informazioni. Anche se le informazioni chiave/valore hello sono stato scritto il file di log tooa, informazioni di hello non viene considerate parte del dizionario hello finché non è stato eseguito il commit delle transazioni hello che sono associate.

Nel codice hello sopra riportato, hello chiamata tooCommitAsync esegue il commit di tutte le operazioni della transazione hello. In particolare, aggiunge file di log commit informazioni toohello nel nodo locale hello e invia anche repliche secondarie hello hello commit tooall record. Una volta che un quorum (maggioranza) delle repliche hello ha risposto, tutti i dati, le modifiche vengono considerate permanenti e i blocchi associati alle chiavi che sono state modificate tramite oggetto ITransaction hello vengono rilasciati in modo da altri thread/transazioni possono modificare hello stesse chiavi e i relativi valori.

Se a CommitAsync non viene chiamato (in genere a causa la generazione di eccezione tooan), l'oggetto ITransaction hello Ottiene eliminato. Quando esegue l'eliminazione di un oggetto ITransaction Commit, Service Fabric aggiunge file di log interruzione informazioni toohello del nodo locale e non è necessario toobe inviato tooany di hello repliche secondarie. E quindi, in cui vengono rilasciati i blocchi associati alle chiavi che sono state modificate tramite la transazione hello.

## <a name="common-pitfalls-and-how-tooavoid-them"></a>Problemi comuni e come tooavoid li
Ora che si informazioni sul funzionano delle raccolte affidabile hello internamente, esaminiamo un alcuni usi impropri comuni di essi. Vedere codice hello riportato di seguito:

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

Quando si lavora con un dizionario regolari di .NET, è possibile aggiungere un dizionario toohello chiave/valore e quindi modificare il valore di hello di una proprietà (ad esempio LastLogin). Tuttavia, questo codice non funziona correttamente con un ReliableDictionary. Ricordare di hello discussione precedente, chiamata hello tooAddAsync serializza hello chiave/valore oggetti toobyte matrici e quindi Salva hello matrici tooa file locale e le invia inoltre repliche secondarie toohello. Se in seguito si modifica una proprietà, questo viene modificato il valore della proprietà hello in memoria. non ha impatto sul file locale hello o dati di hello inviati toohello repliche. Se il processo di hello arresti anomali, novità in memoria viene eliminato. Quando un nuovo processo viene avviato o se un'altra replica diventa primaria, quindi hello valore precedente della proprietà è ciò che è disponibile.

Non si sottolinea sufficientemente quanto sia facile tipo hello toomake di errore illustrato in precedenza. E si solo apprenderà errore hello se/quando si arresta il processo di hello. codice hello toowrite modo corretto di Hello è semplicemente tooreverse hello due righe:


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

Ecco un altro esempio che mostra un errore comune:

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

Nuovamente, con regolari dizionari di .NET, codice hello sopra funziona correttamente ed è un modello comune: developer hello utilizza una chiave toolook un valore. Se il valore di hello esiste, hello imposta un valore della proprietà. Con le raccolte affidabile, tuttavia, questo codice presenta hello stesso problema come già illustrato: **è necessario non modificare un oggetto dopo che aver assegnato tooa affidabile insieme.**

Hello corretto tooupdate modo un valore in un insieme affidabile, si riferisce tooget toohello esistente e provare a oggetto hello cui tooby questo riferimento non modificabile. Quindi, creare un nuovo oggetto che è una copia esatta dell'oggetto originale hello. A questo punto, è possibile modificare lo stato di hello di questo nuovo oggetto e scrivere hello nuovo oggetto nella raccolta hello in modo che si ottiene serializzato toobyte matrici, file locale toohello aggiunti e inviati toohello repliche. Dopo il commit di hello modifiche agli oggetti in memoria hello, file locale hello, in modo che tutte le repliche di hello hello stesso stato. Tutto è in posizione.

Hello di codice seguente viene mostrato hello modo corretto tooupdate un valore in un insieme affidabile:

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

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>Definire un errore del programmatore di tooprevent tipi di dati non modificabili
Idealmente, desideriamo tooreport gli errori del compilatore di hello quando si creano accidentalmente il codice che viene modificato lo stato di un oggetto, si dovrebbe tooconsider non modificabile. Ma, hello il compilatore c# non dispone di hello possibilità toodo questo. In questo caso, tooavoid potenziali programmatore bug, è consigliabile definire i tipi di hello che usa con i tipi di raccolte affidabile toobe non modificabile. In particolare, ciò significa che si osserva toocore i tipi di valore (ad esempio numeri [Int32, UInt64, e così via.], DateTime, Guid, TimeSpan e hello simile). E, ovviamente, è anche possibile usare le stringhe. È una proprietà di raccolta tooavoid migliore come la serializzazione e deserializzazione li può spesso può ridurre le prestazioni. Tuttavia, se si desidera toouse le proprietà della raccolta, è consigliabile utilizzare hello di. Libreria di raccolte non modificabili di rete ([Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)). Questa libreria è disponibile per il download all'indirizzo http://nuget.org. Si consiglia anche di sigillare le classi e rendere i campi di sola lettura quando possibile.

Hello UserInfo tipo riportato di seguito viene illustrato come toodefine un non modificabile digitare sfruttando i consigli menzionati in precedenza.

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

tipo ItemId Hello è anche un tipo immutabile, come illustrato di seguito:

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

## <a name="schema-versioning-upgrades"></a>Controllo delle versioni dello schema (aggiornamenti)
Internamente, le raccolte Reliable Collections serializzano gli oggetti usando DataContractSerializer di .NET. gli oggetti serializzato Hello sono disco locale della replica primaria toohello persistente e trasmesso toohello repliche secondarie. Evoluzione del servizio, è probabile che si tipo hello toochange dei dati (schema), che il servizio lo richiede. Il controllo delle versioni dei dati deve essere eseguito con estrema attenzione. In primo luogo, è necessario essere sempre in grado di toodeserialize vecchi dati. In particolare, questo significa che il codice di deserializzazione deve essere compatibile con le versioni precedenti all'infinito: 333 versione del codice del servizio deve essere in grado di toooperate sui dati inseriti in un insieme affidabile dalla versione 1 del codice del servizio 5 anni.

Il codice del servizio viene aggiornato un dominio di aggiornamento alla volta. Pertanto, durante un aggiornamento, vengono eseguite contemporaneamente due diverse versioni del codice del servizio. È necessario evitare nuova versione di hello del codice del servizio utilizzano hello nuovo schema come le versioni precedenti del codice del servizio potrebbero non essere in grado di toohandle schema di nuovo hello. Se possibile, è consigliabile progettare ogni versione del servizio toobe compatibile con le versioni di 1 versione. In particolare, ciò significa che V1 del codice del servizio deve essere in grado di toosimply ignorare tutti gli elementi dello schema non gestisce in modo esplicito. Tuttavia, deve essere in grado di toosave tutti i dati non conoscere in modo esplicito e scriverlo semplicemente indietro quando si aggiorna un valore o la chiave del dizionario.

> [!WARNING]
> Mentre è possibile modificare lo schema di hello di una chiave, è necessario assicurarsi che sono stabili codice hash della chiave e algoritmi di equals. Se si modifica uno di questi algoritmi funzionamento, non sarà in grado di toolook backup chiave di hello all'interno di dizionario affidabile hello mai nuovamente.
>
>

In alternativa, è possibile eseguire ciò che è in genere indicati tooas 2 fasi l'aggiornamento. Con un aggiornamento della fase 2, aggiornare il servizio da V1 tooV2: V2 contiene codice hello che conosca toodeal con questo codice, nuova modifica dello schema di hello ma non la modalità di esecuzione. Quando hello V2 codice legge i dati di V1, opera su di esso e lo scrive dati V1. Quindi, dopo l'aggiornamento di hello è stata completata in tutti i domini di aggiornamento, è possibile in qualche modo segnalare toohello le istanze di V2 in esecuzione che l'aggiornamento hello è stata completata. (Unidirezionale toosignal tooroll un aggiornamento di configurazione; questo è ciò che crea un aggiornamento in fase di 2.) A questo punto, hello V2 istanze possono leggere i dati V1, convertirlo dati tooV2, operano su di esso e scriverlo sotto forma di dati V2. Quando le altre istanze leggerli V2, non richiedono tooconvert, ma semplicemente operano su di esso e scrivere dati V2.

## <a name="next-steps"></a>Passaggi successivi
toolearn sulla creazione di contratti dati compatibili con, vedere [contratti dati compatibili con versioni](https://msdn.microsoft.com/library/ms731083.aspx).

procedure consigliate di toolearn nei contratti dati di controllo delle versioni, vedere [controllo delle versioni del contratto dati](https://msdn.microsoft.com/library/ms731138.aspx).

toolearn come i contratti dati a tolleranza di versione tooimplement, vedere [callback di serializzazione a tolleranza di versione](https://msdn.microsoft.com/library/ms733734.aspx).

toolearn tooprovide una struttura di dati che può interagire tra più versioni, vedere [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).
