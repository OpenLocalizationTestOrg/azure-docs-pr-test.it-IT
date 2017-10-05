---
title: Cronologia del rilascio delle versioni dei connettori | Documentazione Microsoft
description: Questo argomento include l'elenco di tutte le versioni dei connettori per Forefront Identity Manager (FIM) e Microsoft Identity Manager (MIM)
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="652d5-103">Cronologia di rilascio delle versioni dei connettori</span><span class="sxs-lookup"><span data-stu-id="652d5-103">Connector Version Release History</span></span>
<span data-ttu-id="652d5-104">I connettori per Forefront Identity Manager (FIM) e Microsoft Identity Manager (MIM) vengono aggiornati frequentemente.</span><span class="sxs-lookup"><span data-stu-id="652d5-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="652d5-105">L'argomento riguarda solo FIM e MIM.</span><span class="sxs-lookup"><span data-stu-id="652d5-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="652d5-106">Questi connettori non sono supportati per l'installazione in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="652d5-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="652d5-107">I Connettori rilasciati sono preinstallati su AADConnect quando si aggiorna alla Build specificata.</span><span class="sxs-lookup"><span data-stu-id="652d5-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="652d5-108">L'argomento include l'elenco di tutte le versioni dei connettori rilasciate.</span><span class="sxs-lookup"><span data-stu-id="652d5-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="652d5-109">Collegamenti correlati:</span><span class="sxs-lookup"><span data-stu-id="652d5-109">Related links:</span></span>

* [<span data-ttu-id="652d5-110">Scaricare i connettori più recenti</span><span class="sxs-lookup"><span data-stu-id="652d5-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="652d5-111">[connettore LDAP generico](active-directory-aadconnectsync-connector-genericldap.md) </span><span class="sxs-lookup"><span data-stu-id="652d5-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="652d5-112">[connettore SQL generico](active-directory-aadconnectsync-connector-genericsql.md) </span><span class="sxs-lookup"><span data-stu-id="652d5-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="652d5-113">[connettore per Servizi Web](http://go.microsoft.com/fwlink/?LinkID=226245) </span><span class="sxs-lookup"><span data-stu-id="652d5-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="652d5-114">[connettore PowerShell](active-directory-aadconnectsync-connector-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="652d5-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="652d5-115">[connettore Lotus Domino](active-directory-aadconnectsync-connector-domino.md) </span><span class="sxs-lookup"><span data-stu-id="652d5-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="652d5-116">1.1.604.0 (versione in sospeso di AADConnect)</span><span class="sxs-lookup"><span data-stu-id="652d5-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="652d5-117">Problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="652d5-117">Fixed issues:</span></span>

* <span data-ttu-id="652d5-118">Servizi Web generici:</span><span class="sxs-lookup"><span data-stu-id="652d5-118">Generic Web Services:</span></span>
  * <span data-ttu-id="652d5-119">Risoluzione di un problema che previene la creazione di un progetto SOAP quando si sono verificati due o più endpoint.</span><span class="sxs-lookup"><span data-stu-id="652d5-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="652d5-120">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="652d5-120">Generic SQL:</span></span>
  * <span data-ttu-id="652d5-121">Nell'operazione di importazione GSQL non convertiva correttamente l'ora, quando salvato nello spazio del connettore.</span><span class="sxs-lookup"><span data-stu-id="652d5-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="652d5-122">Il formato di data e ora predefinito per lo spazio del connettore di GSQL è stato modificato da "aaaa-MM-GG: ssZ" a "aaaa-MM-GG: ssZ".</span><span class="sxs-lookup"><span data-stu-id="652d5-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="652d5-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="652d5-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="652d5-124">Problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="652d5-124">Fixed issues:</span></span>

* <span data-ttu-id="652d5-125">Servizi Web generici:</span><span class="sxs-lookup"><span data-stu-id="652d5-125">Generic Web Services:</span></span>
  * <span data-ttu-id="652d5-126">Lo strumento Wsconfig non ha convertito correttamente la matrice Json dalla "richiesta di esempio" per il metodo di servizio REST.</span><span class="sxs-lookup"><span data-stu-id="652d5-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="652d5-127">Si sono verificati problemi con la serializzazione di questa matrice Json per la richiesta REST.</span><span class="sxs-lookup"><span data-stu-id="652d5-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="652d5-128">Lo strumento Web Service Connector Configuration non supporta l'utilizzo di simboli di spazio nei nomi attributo JSON</span><span class="sxs-lookup"><span data-stu-id="652d5-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="652d5-129">Il criterio di sostituzione può essere aggiunto manualmente al file WSConfigTool.exe.config, ad esempio```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="652d5-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="652d5-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="652d5-130">Lotus Notes:</span></span>
  * <span data-ttu-id="652d5-131">Se l'opzione **Consenti rilascio di attestati personalizzati per aziende/unità organizzative** è disattivata, il connettore ha esito negativo durante l'esportazione (aggiornamento); dopo il flusso di esportazione tutti gli attributi vengono esportati in Domino, ma al momento dell'esportazione viene restituita una KeyNotFoundException a Sync.</span><span class="sxs-lookup"><span data-stu-id="652d5-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="652d5-132">Ciò accade perché l'operazione di ridenominazione non riesce quando tenta di modificare il parametro DN (attributo UserName) modificando uno dei seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="652d5-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="652d5-133">LastName</span><span class="sxs-lookup"><span data-stu-id="652d5-133">LastName</span></span>
      - <span data-ttu-id="652d5-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="652d5-134">FirstName</span></span>
      - <span data-ttu-id="652d5-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="652d5-135">MiddleInitial</span></span>
      - <span data-ttu-id="652d5-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="652d5-136">AltFullName</span></span>
      - <span data-ttu-id="652d5-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="652d5-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="652d5-138">o</span><span class="sxs-lookup"><span data-stu-id="652d5-138">ou</span></span>
      - <span data-ttu-id="652d5-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="652d5-139">altcommonname</span></span>

  * <span data-ttu-id="652d5-140">Se l'opzione **Allow custom certifiers for Organization/Organizational Units** (Consenti rilascio di attestati personalizzati per aziende/unità organizzative) è abilitata, ma il file di certificazione richiesto è vuoto, si verifica una KeyNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="652d5-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="652d5-141">Miglioramenti:</span><span class="sxs-lookup"><span data-stu-id="652d5-141">Enhancements:</span></span>

* <span data-ttu-id="652d5-142">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="652d5-142">Generic SQL:</span></span>
  * <span data-ttu-id="652d5-143">**Scenario: riprogettato. Implementata la funzionalità:** "*"</span><span class="sxs-lookup"><span data-stu-id="652d5-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="652d5-144">**Descrizione della soluzione:** modificato l'approccio per la [gestione degli attributi di riferimento multivalore](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="652d5-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="652d5-145">Problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="652d5-145">Fixed issues:</span></span>

* <span data-ttu-id="652d5-146">Servizi Web generici:</span><span class="sxs-lookup"><span data-stu-id="652d5-146">Generic Web Services:</span></span>
  * <span data-ttu-id="652d5-147">Impossibile importare la configurazione del server in presenza di Web Service Connector</span><span class="sxs-lookup"><span data-stu-id="652d5-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="652d5-148">Web Service Connector non funziona con più servizi Web</span><span class="sxs-lookup"><span data-stu-id="652d5-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="652d5-149">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="652d5-149">Generic SQL:</span></span>
  * <span data-ttu-id="652d5-150">Nessun tipo di oggetto elencato per l'attributo a valore singolo a cui si fa riferimento</span><span class="sxs-lookup"><span data-stu-id="652d5-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="652d5-151">L'importazione delta per la strategia Rilevamento modifiche elimina l'oggetto quando il valore viene rimosso alla tabella multivalore</span><span class="sxs-lookup"><span data-stu-id="652d5-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="652d5-152">OverflowException nel connettore GSQL con DB2 su AS/400</span><span class="sxs-lookup"><span data-stu-id="652d5-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="652d5-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="652d5-153">Lotus:</span></span>
  * <span data-ttu-id="652d5-154">Aggiunta l'opzione per abilitare/disabilitare la ricerca delle unità organizzative prima dell'apertura della pagina GlobalParameters</span><span class="sxs-lookup"><span data-stu-id="652d5-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="652d5-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="652d5-155">1.1.443.0</span></span>

<span data-ttu-id="652d5-156">Data di rilascio: marzo 2017</span><span class="sxs-lookup"><span data-stu-id="652d5-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="652d5-157">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="652d5-157">Enhancements</span></span>

* <span data-ttu-id="652d5-158">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="652d5-158">Generic SQL:</span></span></br><span data-ttu-id="652d5-159">
  **Sintomi dello scenario:** è un limite noto del connettore SQL quando si consente il riferimento a un solo tipo di oggetto e si richiede un riferimento incrociato con i membri.</span><span class="sxs-lookup"><span data-stu-id="652d5-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="652d5-160">
**Descrizione della soluzione:** nella fase di elaborazione per i riferimenti in cui si sceglie l'opzione "*", TUTTE le combinazioni di tipi di oggetto saranno restituite al motore di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="652d5-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="652d5-161">In questo modo vengono creati molti segnaposti</span><span class="sxs-lookup"><span data-stu-id="652d5-161">This will create many placeholders</span></span>
- <span data-ttu-id="652d5-162">È necessario assicurarsi che il nome sia univoco tra i tipi di oggetto.</span><span class="sxs-lookup"><span data-stu-id="652d5-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="652d5-163">Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="652d5-163">Generic LDAP:</span></span></br><span data-ttu-id="652d5-164">
 **Scenario:** anche quando vengono selezionati solo alcuni contenitori nella partizione specifica, la ricerca viene comunque eseguita nell'intera partizione.</span><span class="sxs-lookup"><span data-stu-id="652d5-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="652d5-165">La partizione specifica sarà filtrata dal servizio di sincronizzazione ma non dal MA, il che potrebbe causare un calo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="652d5-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="652d5-166">**Descrizione della soluzione:** il codice del connettore GLDAP modificato consente di esaminare tutti i contenitori e cercare oggetti in ciascuno di essi, anziché cercare nell'intera partizione.</span><span class="sxs-lookup"><span data-stu-id="652d5-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="652d5-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="652d5-167">Lotus Domino:</span></span>

  <span data-ttu-id="652d5-168">**Scenario:** supporto dell'eliminazione della posta di Domino per la rimozione di un utente durante un'esportazione.</span><span class="sxs-lookup"><span data-stu-id="652d5-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="652d5-169">
  **Soluzione:** supporto dell'eliminazione della posta configurabile per la rimozione di un utente durante un'esportazione.</span><span class="sxs-lookup"><span data-stu-id="652d5-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="652d5-170">Problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="652d5-170">Fixed issues:</span></span>
* <span data-ttu-id="652d5-171">Servizi Web generici:</span><span class="sxs-lookup"><span data-stu-id="652d5-171">Generic Web Services:</span></span>
 * <span data-ttu-id="652d5-172">Quando si modifica l'URL del servizio nei progetti predefiniti SAP wsconfig tramite lo strumento di configurazione del servizio Web si verifica l'errore seguente: Impossibile trovare una parte del percorso</span><span class="sxs-lookup"><span data-stu-id="652d5-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="652d5-173">Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="652d5-173">Generic LDAP:</span></span>
 * <span data-ttu-id="652d5-174">Il connettore GLDAP non vede tutti gli attributi in AD LDS</span><span class="sxs-lookup"><span data-stu-id="652d5-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="652d5-175">La procedura guidata si interrompe quando non viene rilevato alcun attributo UPN dallo schema di directory LDAP</span><span class="sxs-lookup"><span data-stu-id="652d5-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="652d5-176">Le importazioni differenziali generano errori di individuazione non presenti durante l'importazione completa, quando l'attributo "objectclass" non è selezionato</span><span class="sxs-lookup"><span data-stu-id="652d5-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="652d5-177">La pagina di configurazione "Configurare partizioni e gerarchie" non mostra gli oggetti il cui tipo è uguale alla partizione per i server Novel nel MA Generic</span><span class="sxs-lookup"><span data-stu-id="652d5-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="652d5-178">LDAP.</span><span class="sxs-lookup"><span data-stu-id="652d5-178">LDAP MA.</span></span> <span data-ttu-id="652d5-179">Essi mostravano solo gli oggetti della partizione di RootDSE.</span><span class="sxs-lookup"><span data-stu-id="652d5-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="652d5-180">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="652d5-180">Generic SQL:</span></span>
 * <span data-ttu-id="652d5-181">Correzione per il bug dell'attributo multivalore non importato per l'importazione differenziale watermark di Generic SQL</span><span class="sxs-lookup"><span data-stu-id="652d5-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="652d5-182">Quando si esportano valori di attributi multivalore eliminati/aggiunti, non vengono eliminati/aggiunti nell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="652d5-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="652d5-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="652d5-183">Lotus Notes:</span></span>
 * <span data-ttu-id="652d5-184">Un campo specifico "Cognome" è visualizzato correttamente nel metaverse, tuttavia durante l'esportazione in Notes il valore dell'attributo è Null o Empty.</span><span class="sxs-lookup"><span data-stu-id="652d5-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="652d5-185">Correzione per l'errore di file di certificazione duplicato</span><span class="sxs-lookup"><span data-stu-id="652d5-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="652d5-186">Quando si seleziona l'oggetto senza dati nel connettore Lotus Domino con altri oggetti, viene visualizzato l'errore di individuazione durante un'importazione completa.</span><span class="sxs-lookup"><span data-stu-id="652d5-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="652d5-187">Quando viene eseguita un'importazione differenziale nel connettore Lotus Domino, alla fine dell'esecuzione il servizio Microsoft.IdentityManagement.MA.LotusDomino.Service.exe talvolta restituisce un errore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="652d5-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="652d5-188">L'appartenenza ai gruppi nel complesso funziona bene e viene mantenuta, tranne quando l'esportazione per tentare di rimuovere un utente dall'appartenenza viene completata correttamente con un aggiornamento ma l'utente non viene effettivamente rimosso dall'appartenenza a Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="652d5-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="652d5-189">La possibilità di scegliere la modalità di esportazione "Aggiungi elemento in fondo" è stato aggiunta nell'interfaccia utente grafica di Lotus MA per accodare i nuovi elementi in fondo durante l'esportazione per gli attributi multivalore.</span><span class="sxs-lookup"><span data-stu-id="652d5-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="652d5-190">Il connettore aggiungerà la logica necessaria per eliminare il file dalla cartella di posta elettronica e l'insieme di credenziali degli ID.</span><span class="sxs-lookup"><span data-stu-id="652d5-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="652d5-191">Eliminare l'appartenenza non funziona per un membro NAB trasversale.</span><span class="sxs-lookup"><span data-stu-id="652d5-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="652d5-192">L'eliminazione dei valori da un attributo multivalore dovrebbe riuscire</span><span class="sxs-lookup"><span data-stu-id="652d5-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="652d5-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="652d5-193">1.1.117.0</span></span>
<span data-ttu-id="652d5-194">Data di rilascio: marzo 2016</span><span class="sxs-lookup"><span data-stu-id="652d5-194">Released: 2016 March</span></span>

<span data-ttu-id="652d5-195">**Nuovo connettore**</span><span class="sxs-lookup"><span data-stu-id="652d5-195">**New Connector**</span></span>  
<span data-ttu-id="652d5-196">Versione iniziale del [connettore SQL generico](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="652d5-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="652d5-197">**Nuove funzionalità:**</span><span class="sxs-lookup"><span data-stu-id="652d5-197">**New features:**</span></span>

* <span data-ttu-id="652d5-198">Connettore Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="652d5-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="652d5-199">Aggiunta del supporto per l'importazione differenziale con Isode.</span><span class="sxs-lookup"><span data-stu-id="652d5-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="652d5-200">Connettore Web Services:</span><span class="sxs-lookup"><span data-stu-id="652d5-200">Web Services Connector:</span></span>
  * <span data-ttu-id="652d5-201">Aggiornamento dell’attività csEntryChangeResult e dell’attività setImportErrorCode per consentire che gli errori a livello di oggetto siano restituiti al motore di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="652d5-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="652d5-202">Aggiornamento dei modelli SAP6 e SAP6User per l’uso della nuova funzionalità di errore a livello di oggetto.</span><span class="sxs-lookup"><span data-stu-id="652d5-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="652d5-203">Connettore Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="652d5-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="652d5-204">Per l'esportazione è necessario un file di certificazione per ogni rubrica.</span><span class="sxs-lookup"><span data-stu-id="652d5-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="652d5-205">È ora possibile usare la stessa password per tutti i file di certificazione semplificando la gestione.</span><span class="sxs-lookup"><span data-stu-id="652d5-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="652d5-206">**Problemi risolti:**</span><span class="sxs-lookup"><span data-stu-id="652d5-206">**Fixed issues:**</span></span>

* <span data-ttu-id="652d5-207">Connettore Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="652d5-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="652d5-208">Per IBM Tivoli DS alcuni attributi di riferimento non venivano rilevati correttamente.</span><span class="sxs-lookup"><span data-stu-id="652d5-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="652d5-209">Per Open LDAP, nelle importazioni differenziali, gli spazi vuoti all’inizio e alla fine delle stringhe venivano troncati.</span><span class="sxs-lookup"><span data-stu-id="652d5-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="652d5-210">Per Novell e NetIQ un'esportazione che sposta un oggetto fra unità organizzative/contenitori e contemporaneamente rinominano l'oggetto non riescono.</span><span class="sxs-lookup"><span data-stu-id="652d5-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="652d5-211">Connettore Web Services:</span><span class="sxs-lookup"><span data-stu-id="652d5-211">Web Services Connector:</span></span>
  * <span data-ttu-id="652d5-212">Se il servizio Web aveva più endpoint per lo stesso binding, il connettore non individuava correttamente questi endpoint.</span><span class="sxs-lookup"><span data-stu-id="652d5-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="652d5-213">Connettore Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="652d5-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="652d5-214">L’esportazione dell’attributo fullName in un database di posta elettronica in ingresso non funzionava.</span><span class="sxs-lookup"><span data-stu-id="652d5-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="652d5-215">Le esportazioni che aggiungevano e rimuovevano membri da un gruppo esportavano solo i membri aggiunti.</span><span class="sxs-lookup"><span data-stu-id="652d5-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="652d5-216">Se un documento di Notes non è valido (l'attributo isValid è impostato su false), l'operazione del connettore non riesce.</span><span class="sxs-lookup"><span data-stu-id="652d5-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="652d5-217">Versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="652d5-217">Older releases</span></span>
<span data-ttu-id="652d5-218">Prima di marzo 2016, i connettori venivano rilasciati come argomenti relativi al supporto.</span><span class="sxs-lookup"><span data-stu-id="652d5-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="652d5-219">**Generic LDAP**</span><span class="sxs-lookup"><span data-stu-id="652d5-219">**Generic LDAP**</span></span>

* <span data-ttu-id="652d5-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, settembre 2015</span><span class="sxs-lookup"><span data-stu-id="652d5-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="652d5-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, marzo 2015</span><span class="sxs-lookup"><span data-stu-id="652d5-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="652d5-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, gennaio 2015</span><span class="sxs-lookup"><span data-stu-id="652d5-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="652d5-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, settembre 2014</span><span class="sxs-lookup"><span data-stu-id="652d5-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="652d5-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, marzo 2014</span><span class="sxs-lookup"><span data-stu-id="652d5-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="652d5-225">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="652d5-225">**WebServices**</span></span>

* <span data-ttu-id="652d5-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, settembre 2014</span><span class="sxs-lookup"><span data-stu-id="652d5-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="652d5-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="652d5-227">**PowerShell**</span></span>

* <span data-ttu-id="652d5-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, settembre 2014</span><span class="sxs-lookup"><span data-stu-id="652d5-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="652d5-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="652d5-229">**Lotus Domino**</span></span>

* <span data-ttu-id="652d5-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, settembre 2015</span><span class="sxs-lookup"><span data-stu-id="652d5-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="652d5-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, marzo 2015</span><span class="sxs-lookup"><span data-stu-id="652d5-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="652d5-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, agosto 2014</span><span class="sxs-lookup"><span data-stu-id="652d5-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="652d5-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, febbraio 2014</span><span class="sxs-lookup"><span data-stu-id="652d5-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="652d5-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, ottobre 2013</span><span class="sxs-lookup"><span data-stu-id="652d5-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="652d5-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, agosto 2013</span><span class="sxs-lookup"><span data-stu-id="652d5-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="652d5-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="652d5-236">Next steps</span></span>
<span data-ttu-id="652d5-237">Ulteriori informazioni sulla configurazione della [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="652d5-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="652d5-238">Ulteriori informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="652d5-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
