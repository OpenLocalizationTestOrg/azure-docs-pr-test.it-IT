---
title: cronologia delle versioni aaaConnector | Documenti Microsoft
description: Questo argomento vengono elencate tutte le versioni di hello connettori per Forefront Identity Manager (FIM) e Microsoft Identity Manager (MIM)
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
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="88947-103">Cronologia di rilascio delle versioni dei connettori</span><span class="sxs-lookup"><span data-stu-id="88947-103">Connector Version Release History</span></span>
<span data-ttu-id="88947-104">Connettori di Hello per Forefront Identity Manager (FIM) e Microsoft Identity Manager (MIM) vengono aggiornati di frequente.</span><span class="sxs-lookup"><span data-stu-id="88947-104">hello Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="88947-105">L'argomento riguarda solo FIM e MIM.</span><span class="sxs-lookup"><span data-stu-id="88947-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="88947-106">Questi connettori non sono supportati per l'installazione in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="88947-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="88947-107">Connettori rilasciati sono preinstallati in AADConnect durante l'aggiornamento toospecified compilazione.</span><span class="sxs-lookup"><span data-stu-id="88947-107">Released Connectors are preinstalled on AADConnect when upgrading toospecified Build.</span></span>

<span data-ttu-id="88947-108">Questo argomento elenca tutte le versioni di hello connettori che sono state rilasciate.</span><span class="sxs-lookup"><span data-stu-id="88947-108">This topic list all versions of hello Connectors that have been released.</span></span>

<span data-ttu-id="88947-109">Collegamenti correlati:</span><span class="sxs-lookup"><span data-stu-id="88947-109">Related links:</span></span>

* [<span data-ttu-id="88947-110">Scaricare i connettori più recenti</span><span class="sxs-lookup"><span data-stu-id="88947-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="88947-111">[connettore LDAP generico](active-directory-aadconnectsync-connector-genericldap.md)</span><span class="sxs-lookup"><span data-stu-id="88947-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="88947-112">[connettore SQL generico](active-directory-aadconnectsync-connector-genericsql.md)</span><span class="sxs-lookup"><span data-stu-id="88947-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="88947-113">[connettore per Servizi Web](http://go.microsoft.com/fwlink/?LinkID=226245)</span><span class="sxs-lookup"><span data-stu-id="88947-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="88947-114">[connettore PowerShell](active-directory-aadconnectsync-connector-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="88947-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="88947-115">[connettore Lotus Domino](active-directory-aadconnectsync-connector-domino.md)</span><span class="sxs-lookup"><span data-stu-id="88947-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="88947-116">1.1.604.0 (versione in sospeso di AADConnect)</span><span class="sxs-lookup"><span data-stu-id="88947-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="88947-117">Problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="88947-117">Fixed issues:</span></span>

* <span data-ttu-id="88947-118">Servizi Web generici:</span><span class="sxs-lookup"><span data-stu-id="88947-118">Generic Web Services:</span></span>
  * <span data-ttu-id="88947-119">Risoluzione di un problema che previene la creazione di un progetto SOAP quando si sono verificati due o più endpoint.</span><span class="sxs-lookup"><span data-stu-id="88947-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="88947-120">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="88947-120">Generic SQL:</span></span>
  * <span data-ttu-id="88947-121">Nell'operazione hello dell'importazione hello GSQL era non conversione ora correttamente, quando salvato tooconnector spazio.</span><span class="sxs-lookup"><span data-stu-id="88947-121">In hello operation of import hello GSQL was not converting time correctly, when saved tooconnector space.</span></span> <span data-ttu-id="88947-122">Hello formato di data e ora predefinito per spazio connettore di hello GSQL è stato modificato da 'aaaa-MM-GG: ssZ' too'yyyy-MM-GG: ssZ '.</span><span class="sxs-lookup"><span data-stu-id="88947-122">hello default date and time format for connector space of hello GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' too'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="88947-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="88947-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="88947-124">Problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="88947-124">Fixed issues:</span></span>

* <span data-ttu-id="88947-125">Servizi Web generici:</span><span class="sxs-lookup"><span data-stu-id="88947-125">Generic Web Services:</span></span>
  * <span data-ttu-id="88947-126">strumento Wsconfig Hello non converte correttamente matrice Json hello da "richiesta di esempio" per il metodo di servizio REST hello.</span><span class="sxs-lookup"><span data-stu-id="88947-126">hello Wsconfig tool did not convert correctly hello Json array from "sample request" for hello REST service method.</span></span> <span data-ttu-id="88947-127">La causa di problemi con la serializzazione questa matrice Json per richiesta REST hello.</span><span class="sxs-lookup"><span data-stu-id="88947-127">This caused problems with serialization this Json array for hello REST request.</span></span>
  * <span data-ttu-id="88947-128">Lo strumento Web Service Connector Configuration non supporta l'utilizzo di simboli di spazio nei nomi attributo JSON</span><span class="sxs-lookup"><span data-stu-id="88947-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="88947-129">Un criterio di sostituzione può essere aggiunti manualmente toohello WSConfigTool.exe.config file, ad esempio```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="88947-129">A Substitution pattern can be added manually toohello WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="88947-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="88947-130">Lotus Notes:</span></span>
  * <span data-ttu-id="88947-131">Hello quando l'opzione **consentire rilascio degli attestati personalizzata per unità di organizzazione/aziendale** è disabilitato hello connettore si verifica un errore durante l'esportazione (aggiornamento) dopo l'esportazione di hello flusso tutti gli attributi sono tooDomino esportato, ma in fase di hello di Esporta una KeyNotFoundException viene restituito tooSync.</span><span class="sxs-lookup"><span data-stu-id="88947-131">When hello option **Allow custom certifiers for Organization/Organizational Units** is disabled then hello connector fails during export (Update) After hello export flow all attributes are exported tooDomino but at hello time of export a KeyNotFoundException is returned tooSync.</span></span> 
    * <span data-ttu-id="88947-132">Ciò accade perché hello rinominare l'operazione ha esito negativo durante il tentativo di toochange DN (attributo UserName) modificando uno dei seguenti attributi di hello:</span><span class="sxs-lookup"><span data-stu-id="88947-132">This happens because hello rename operation fails when it tries toochange DN (UserName attribute) by changing one of hello attributes below:</span></span>  
      - <span data-ttu-id="88947-133">LastName</span><span class="sxs-lookup"><span data-stu-id="88947-133">LastName</span></span>
      - <span data-ttu-id="88947-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="88947-134">FirstName</span></span>
      - <span data-ttu-id="88947-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="88947-135">MiddleInitial</span></span>
      - <span data-ttu-id="88947-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="88947-136">AltFullName</span></span>
      - <span data-ttu-id="88947-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="88947-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="88947-138">o</span><span class="sxs-lookup"><span data-stu-id="88947-138">ou</span></span>
      - <span data-ttu-id="88947-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="88947-139">altcommonname</span></span>

  * <span data-ttu-id="88947-140">Se l'opzione **Allow custom certifiers for Organization/Organizational Units** (Consenti rilascio di attestati personalizzati per aziende/unità organizzative) è abilitata, ma il file di certificazione richiesto è vuoto, si verifica una KeyNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="88947-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="88947-141">Miglioramenti:</span><span class="sxs-lookup"><span data-stu-id="88947-141">Enhancements:</span></span>

* <span data-ttu-id="88947-142">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="88947-142">Generic SQL:</span></span>
  * <span data-ttu-id="88947-143">**Scenario: riprogettato. Implementata la funzionalità:** "*"</span><span class="sxs-lookup"><span data-stu-id="88947-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="88947-144">**Descrizione della soluzione:** modificato l'approccio per la [gestione degli attributi di riferimento multivalore](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="88947-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="88947-145">Problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="88947-145">Fixed issues:</span></span>

* <span data-ttu-id="88947-146">Servizi Web generici:</span><span class="sxs-lookup"><span data-stu-id="88947-146">Generic Web Services:</span></span>
  * <span data-ttu-id="88947-147">Impossibile importare la configurazione del server in presenza di Web Service Connector</span><span class="sxs-lookup"><span data-stu-id="88947-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="88947-148">Web Service Connector non funziona con più servizi Web</span><span class="sxs-lookup"><span data-stu-id="88947-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="88947-149">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="88947-149">Generic SQL:</span></span>
  * <span data-ttu-id="88947-150">Nessun tipo di oggetto elencato per l'attributo a valore singolo a cui si fa riferimento</span><span class="sxs-lookup"><span data-stu-id="88947-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="88947-151">L'importazione delta per la strategia Rilevamento modifiche elimina l'oggetto quando il valore viene rimosso alla tabella multivalore</span><span class="sxs-lookup"><span data-stu-id="88947-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="88947-152">OverflowException nel connettore GSQL con DB2 su AS/400</span><span class="sxs-lookup"><span data-stu-id="88947-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="88947-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="88947-153">Lotus:</span></span>
  * <span data-ttu-id="88947-154">Aggiunta l'opzione tooenable\disable ricerca unità organizzative prima dell'apertura globalparameters della pagina</span><span class="sxs-lookup"><span data-stu-id="88947-154">Added option tooenable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="88947-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="88947-155">1.1.443.0</span></span>

<span data-ttu-id="88947-156">Data di rilascio: marzo 2017</span><span class="sxs-lookup"><span data-stu-id="88947-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="88947-157">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="88947-157">Enhancements</span></span>

* <span data-ttu-id="88947-158">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="88947-158">Generic SQL:</span></span></br><span data-ttu-id="88947-159">
  **Sintomi di scenario:** è una limitazione nota con connettore SQL in cui è solo consentire a un tipo di oggetto di riferimento tooone e richiedono un riferimento incrociato con membri hello.</span><span class="sxs-lookup"><span data-stu-id="88947-159">
  **Scenario Symptoms:**  It is a well-known limitation with hello SQL Connector where we only allow a reference tooone object type and require cross reference with members.</span></span> </br><span data-ttu-id="88947-160">
**Descrizione soluzione:** In fase di elaborazione hello per i riferimenti sono stati "*" viene scelto l'opzione, verranno restituite tutte le combinazioni di tipi di oggetto motore di sincronizzazione toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="88947-160">
**Solution description:** In hello processing step for references were "*" option is chosen, ALL combinations of object types will be returned back toohello sync engine.</span></span>

>[!Important]
- <span data-ttu-id="88947-161">In questo modo vengono creati molti segnaposti</span><span class="sxs-lookup"><span data-stu-id="88947-161">This will create many placeholders</span></span>
- <span data-ttu-id="88947-162">È necessario toomake hello denominazione sia univoco tra i tipi di oggetto.</span><span class="sxs-lookup"><span data-stu-id="88947-162">It is required toomake sure hello naming is unique cross object types.</span></span>


* <span data-ttu-id="88947-163">Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="88947-163">Generic LDAP:</span></span></br><span data-ttu-id="88947-164">
 **Scenario:** se solo alcuni contenitori sono selezionati in una partizione specifica, quindi ricerca hello ancora verrà eseguito in intera partizione.</span><span class="sxs-lookup"><span data-stu-id="88947-164">
**Scenario:** When only few containers are selected in specific partition, then hello search still will be done in whole partition.</span></span> <span data-ttu-id="88947-165">La partizione specifica sarà filtrata dal servizio di sincronizzazione ma non dal MA, il che potrebbe causare un calo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="88947-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="88947-166">**Descrizione soluzione:** toomake codice modificato GLDAP connettore è possibile scorrere tutti i contenitori e cercare gli oggetti in ognuno di essi, anziché dover cercare nella partizione intero hello.</span><span class="sxs-lookup"><span data-stu-id="88947-166">**Solution description:** Changed GLDAP connector's code toomake it possible go through all containers and search objects in each of them, instead of searching in hello whole partition.</span></span>


* <span data-ttu-id="88947-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="88947-167">Lotus Domino:</span></span>

  <span data-ttu-id="88947-168">**Scenario:** supporto dell'eliminazione della posta di Domino per la rimozione di un utente durante un'esportazione.</span><span class="sxs-lookup"><span data-stu-id="88947-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="88947-169">
  **Soluzione:** supporto dell'eliminazione della posta configurabile per la rimozione di un utente durante un'esportazione.</span><span class="sxs-lookup"><span data-stu-id="88947-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="88947-170">Problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="88947-170">Fixed issues:</span></span>
* <span data-ttu-id="88947-171">Servizi Web generici:</span><span class="sxs-lookup"><span data-stu-id="88947-171">Generic Web Services:</span></span>
 * <span data-ttu-id="88947-172">Quando si modifica URL del servizio hello predefinita wsconfig SAP progetti tramite lo strumento di configurazione di servizio Web, quindi si verifica il seguente errore hello: Impossibile trovare una parte di percorso hello</span><span class="sxs-lookup"><span data-stu-id="88947-172">When changing hello service URL in Default SAP wsconfig projects through WebService Configuration Tool then hello following error happens: Could not find a part of hello path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="88947-173">Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="88947-173">Generic LDAP:</span></span>
 * <span data-ttu-id="88947-174">Il connettore GLDAP non vede tutti gli attributi in AD LDS</span><span class="sxs-lookup"><span data-stu-id="88947-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="88947-175">Procedura guidata interruzioni quando non viene rilevato alcun attributo UPN dallo schema di directory LDAP hello</span><span class="sxs-lookup"><span data-stu-id="88947-175">Wizard breaks when no UPN attributes are detected from hello LDAP directory schema</span></span>
 * <span data-ttu-id="88947-176">Le importazioni differenziali generano errori di individuazione non presenti durante l'importazione completa, quando l'attributo "objectclass" non è selezionato</span><span class="sxs-lookup"><span data-stu-id="88947-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="88947-177">Una pagina di configurazione "Configurare le partizioni e gerarchie", non Mostra tutti gli oggetti cui tipo è uguale toohello partizione per i nuovi server hello generico</span><span class="sxs-lookup"><span data-stu-id="88947-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal toohello partition for Novel servers in hello Generic</span></span>  
<span data-ttu-id="88947-178">LDAP.</span><span class="sxs-lookup"><span data-stu-id="88947-178">LDAP MA.</span></span> <span data-ttu-id="88947-179">Essi mostravano solo gli oggetti della partizione di RootDSE.</span><span class="sxs-lookup"><span data-stu-id="88947-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="88947-180">Generic SQL:</span><span class="sxs-lookup"><span data-stu-id="88947-180">Generic SQL:</span></span>
 * <span data-ttu-id="88947-181">Correzione per il bug dell'attributo multivalore non importato per l'importazione differenziale watermark di Generic SQL</span><span class="sxs-lookup"><span data-stu-id="88947-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="88947-182">Quando si esportano valori di attributi multivalore eliminati/aggiunti, non vengono eliminati/aggiunti nell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="88947-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="88947-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="88947-183">Lotus Notes:</span></span>
 * <span data-ttu-id="88947-184">Un campo specifico "Nome completo" viene visualizzato nel metaverse hello correttamente tuttavia durante l'esportazione tooNotes hello valore per attributo hello è Null o vuota.</span><span class="sxs-lookup"><span data-stu-id="88947-184">A specific field "Full Name" is shown in hello metaverse correctly however when exporting tooNotes hello value for hello attribute is Null or Empty.</span></span>
 * <span data-ttu-id="88947-185">Correzione per l'errore di file di certificazione duplicato</span><span class="sxs-lookup"><span data-stu-id="88947-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="88947-186">Quando viene selezionato hello oggetto senza dati hello Lotus Domino connettore con altri oggetti quindi viene visualizzato l'errore individuazione hello durante l'esecuzione Full Import.</span><span class="sxs-lookup"><span data-stu-id="88947-186">When hello Object without any data is selected on hello Lotus Domino Connector with other objects then we receive hello Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="88947-187">Durante l'importazione Delta è in esecuzione su hello connettore Lotus Domino, alla fine di hello di tale esecuzione, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe servizio talvolta restituisce un errore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="88947-187">When Delta Import is being running on hello Lotus Domino Connector, at hello end of that run, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="88947-188">L'appartenenza al gruppo globale funziona correttamente e viene mantenuta, tranne quando si esegue hello esportazione tootry tooremove un utente dall'appartenenza viene completata correttamente con un aggiornamento, ma non viene effettivamente rimossi utente hello dall'appartenenza Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="88947-188">Group membership overall works fine and is maintained, except when running hello export tootry tooremove a user from membership it shows as successful with an update, but hello user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="88947-189">Una modalità di toochoose opportunità di esportazione come "Accoda elemento nella parte inferiore" è stato aggiunto nella configurazione GUI di Lotus MA tooappend nuovi elementi nella parte inferiore durante l'esportazione di hello per gli attributi multivalore.</span><span class="sxs-lookup"><span data-stu-id="88947-189">An opportunity toochoose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA tooappend new items at bottom during hello export for multi-valued attributes.</span></span>
 * <span data-ttu-id="88947-190">Connettore aggiungerà hello necessaria logica toodelete hello file hello cartella della posta e l'ID insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="88947-190">Connector will add hello needed logic toodelete hello file from hello Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="88947-191">Eliminare l'appartenenza non funziona per un membro NAB trasversale.</span><span class="sxs-lookup"><span data-stu-id="88947-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="88947-192">L'eliminazione dei valori da un attributo multivalore dovrebbe riuscire</span><span class="sxs-lookup"><span data-stu-id="88947-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="88947-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="88947-193">1.1.117.0</span></span>
<span data-ttu-id="88947-194">Data di rilascio: marzo 2016</span><span class="sxs-lookup"><span data-stu-id="88947-194">Released: 2016 March</span></span>

<span data-ttu-id="88947-195">**Nuovo connettore**</span><span class="sxs-lookup"><span data-stu-id="88947-195">**New Connector**</span></span>  
<span data-ttu-id="88947-196">Versione di hello iniziale [connettore SQL generico](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="88947-196">Initial release of hello [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="88947-197">**Nuove funzionalità:**</span><span class="sxs-lookup"><span data-stu-id="88947-197">**New features:**</span></span>

* <span data-ttu-id="88947-198">Connettore Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="88947-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="88947-199">Aggiunta del supporto per l'importazione differenziale con Isode.</span><span class="sxs-lookup"><span data-stu-id="88947-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="88947-200">Connettore Web Services:</span><span class="sxs-lookup"><span data-stu-id="88947-200">Web Services Connector:</span></span>
  * <span data-ttu-id="88947-201">Hello aggiornato csEntryChangeResult attività e setImportErrorCode attività tooallow oggetto gli errori a livello toobe restituito toohello indietro motore di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="88947-201">Updated hello csEntryChangeResult activity and setImportErrorCode activity tooallow object level errors toobe returned back toohello sync engine.</span></span>
  * <span data-ttu-id="88947-202">Hello aggiornato SAP6 e SAP6User modelli toouse hello nuovo oggetto errore di livello.</span><span class="sxs-lookup"><span data-stu-id="88947-202">Updated hello SAP6 and SAP6User templates toouse hello new object level error functionality.</span></span>
* <span data-ttu-id="88947-203">Connettore Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="88947-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="88947-204">Per l'esportazione è necessario un file di certificazione per ogni rubrica.</span><span class="sxs-lookup"><span data-stu-id="88947-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="88947-205">È possibile utilizzare hello stessa password per l'intera rilascio degli attestati toomake hello gestione più semplice.</span><span class="sxs-lookup"><span data-stu-id="88947-205">You can now use hello same password for all certifiers toomake hello management easier.</span></span>

<span data-ttu-id="88947-206">**Problemi risolti:**</span><span class="sxs-lookup"><span data-stu-id="88947-206">**Fixed issues:**</span></span>

* <span data-ttu-id="88947-207">Connettore Generic LDAP:</span><span class="sxs-lookup"><span data-stu-id="88947-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="88947-208">Per IBM Tivoli DS alcuni attributi di riferimento non venivano rilevati correttamente.</span><span class="sxs-lookup"><span data-stu-id="88947-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="88947-209">Per aprire LDAP durante un'importazione delta, gli spazi vuoti all'inizio di hello e alla fine di stringhe sono stati troncati.</span><span class="sxs-lookup"><span data-stu-id="88947-209">For Open LDAP during a delta import, whitespaces at hello beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="88947-210">Per Novell e NetIQ, un'esportazione che spostati di un oggetto tra le unità organizzative e contenitori e hello stesso tempo l'oggetto rinominato hello.</span><span class="sxs-lookup"><span data-stu-id="88947-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at hello same time renamed hello object failed.</span></span>
* <span data-ttu-id="88947-211">Connettore Web Services:</span><span class="sxs-lookup"><span data-stu-id="88947-211">Web Services Connector:</span></span>
  * <span data-ttu-id="88947-212">Se il servizio web hello ha più endpoint per la stessa associazione, quindi hello Connector non correttamente individuare questi endpoint.</span><span class="sxs-lookup"><span data-stu-id="88947-212">If hello web service had multiple end-points for same binding, then hello Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="88947-213">Connettore Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="88947-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="88947-214">L'esportazione di hello fullName attributo tooa posta elettronica nel database non ha funzionato.</span><span class="sxs-lookup"><span data-stu-id="88947-214">An export of hello fullName attribute tooa mail-in database did not work.</span></span>
  * <span data-ttu-id="88947-215">Un'esportazione che le aggiunte e rimosse membro da un gruppo, solo i membri aggiunti hello esportata.</span><span class="sxs-lookup"><span data-stu-id="88947-215">An export which both added and removed member from a group only exported hello added members.</span></span>
  * <span data-ttu-id="88947-216">Se un documento di note non è valido (hello attributo isValid set toofalse), quindi hello ha esito negativo connettore.</span><span class="sxs-lookup"><span data-stu-id="88947-216">If a Notes Document is invalid (hello attribute isValid set toofalse), then hello Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="88947-217">Versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="88947-217">Older releases</span></span>
<span data-ttu-id="88947-218">Prima di marzo 2016, hello connettori sono stati rilasciati come argomenti di supporto.</span><span class="sxs-lookup"><span data-stu-id="88947-218">Before March 2016, hello Connectors were released as support topics.</span></span>

<span data-ttu-id="88947-219">**Generic LDAP**</span><span class="sxs-lookup"><span data-stu-id="88947-219">**Generic LDAP**</span></span>

* <span data-ttu-id="88947-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, settembre 2015</span><span class="sxs-lookup"><span data-stu-id="88947-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="88947-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, marzo 2015</span><span class="sxs-lookup"><span data-stu-id="88947-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="88947-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, gennaio 2015</span><span class="sxs-lookup"><span data-stu-id="88947-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="88947-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, settembre 2014</span><span class="sxs-lookup"><span data-stu-id="88947-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="88947-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, marzo 2014</span><span class="sxs-lookup"><span data-stu-id="88947-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="88947-225">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="88947-225">**WebServices**</span></span>

* <span data-ttu-id="88947-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, settembre 2014</span><span class="sxs-lookup"><span data-stu-id="88947-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="88947-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="88947-227">**PowerShell**</span></span>

* <span data-ttu-id="88947-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, settembre 2014</span><span class="sxs-lookup"><span data-stu-id="88947-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="88947-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="88947-229">**Lotus Domino**</span></span>

* <span data-ttu-id="88947-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, settembre 2015</span><span class="sxs-lookup"><span data-stu-id="88947-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="88947-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, marzo 2015</span><span class="sxs-lookup"><span data-stu-id="88947-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="88947-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, agosto 2014</span><span class="sxs-lookup"><span data-stu-id="88947-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="88947-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, febbraio 2014</span><span class="sxs-lookup"><span data-stu-id="88947-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="88947-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, ottobre 2013</span><span class="sxs-lookup"><span data-stu-id="88947-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="88947-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, agosto 2013</span><span class="sxs-lookup"><span data-stu-id="88947-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="88947-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88947-236">Next steps</span></span>
<span data-ttu-id="88947-237">Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.</span><span class="sxs-lookup"><span data-stu-id="88947-237">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="88947-238">Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="88947-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
