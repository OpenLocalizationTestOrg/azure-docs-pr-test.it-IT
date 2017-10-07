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
# <a name="connector-version-release-history"></a>Cronologia di rilascio delle versioni dei connettori
Connettori di Hello per Forefront Identity Manager (FIM) e Microsoft Identity Manager (MIM) vengono aggiornati di frequente.

> [!NOTE]
> L'argomento riguarda solo FIM e MIM. Questi connettori non sono supportati per l'installazione in Azure AD Connect. Connettori rilasciati sono preinstallati in AADConnect durante l'aggiornamento toospecified compilazione.

Questo argomento elenca tutte le versioni di hello connettori che sono state rilasciate.

Collegamenti correlati:

* [Scaricare i connettori più recenti](http://go.microsoft.com/fwlink/?LinkId=717495)
* [connettore LDAP generico](active-directory-aadconnectsync-connector-genericldap.md)
* [connettore SQL generico](active-directory-aadconnectsync-connector-genericsql.md)
* [connettore per Servizi Web](http://go.microsoft.com/fwlink/?LinkID=226245)
* [connettore PowerShell](active-directory-aadconnectsync-connector-powershell.md)
* [connettore Lotus Domino](active-directory-aadconnectsync-connector-domino.md)


## <a name="116040-aadconnect-pending-release"></a>1.1.604.0 (versione in sospeso di AADConnect)


### <a name="fixed-issues"></a>Problemi risolti:

* Servizi Web generici:
  * Risoluzione di un problema che previene la creazione di un progetto SOAP quando si sono verificati due o più endpoint.
* Generic SQL:
  * Nell'operazione hello dell'importazione hello GSQL era non conversione ora correttamente, quando salvato tooconnector spazio. Hello formato di data e ora predefinito per spazio connettore di hello GSQL è stato modificato da 'aaaa-MM-GG: ssZ' too'yyyy-MM-GG: ssZ '.

## <a name="115510-aadconnect-115530"></a>1.1.551.0 (AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>Problemi risolti:

* Servizi Web generici:
  * strumento Wsconfig Hello non converte correttamente matrice Json hello da "richiesta di esempio" per il metodo di servizio REST hello. La causa di problemi con la serializzazione questa matrice Json per richiesta REST hello.
  * Lo strumento Web Service Connector Configuration non supporta l'utilizzo di simboli di spazio nei nomi attributo JSON 
    * Un criterio di sostituzione può essere aggiunti manualmente toohello WSConfigTool.exe.config file, ad esempio```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Lotus Notes:
  * Hello quando l'opzione **consentire rilascio degli attestati personalizzata per unità di organizzazione/aziendale** è disabilitato hello connettore si verifica un errore durante l'esportazione (aggiornamento) dopo l'esportazione di hello flusso tutti gli attributi sono tooDomino esportato, ma in fase di hello di Esporta una KeyNotFoundException viene restituito tooSync. 
    * Ciò accade perché hello rinominare l'operazione ha esito negativo durante il tentativo di toochange DN (attributo UserName) modificando uno dei seguenti attributi di hello:  
      - LastName
      - FirstName
      - MiddleInitial
      - AltFullName
      - AltFullNameLanguage
      - o
      - altcommonname

  * Se l'opzione **Allow custom certifiers for Organization/Organizational Units** (Consenti rilascio di attestati personalizzati per aziende/unità organizzative) è abilitata, ma il file di certificazione richiesto è vuoto, si verifica una KeyNotFoundException.

### <a name="enhancements"></a>Miglioramenti:

* Generic SQL:
  * **Scenario: riprogettato. Implementata la funzionalità:** "*"
  * **Descrizione della soluzione:** modificato l'approccio per la [gestione degli attributi di riferimento multivalore](active-directory-aadconnectsync-connector-genericsql.md).


### <a name="fixed-issues"></a>Problemi risolti:

* Servizi Web generici:
  * Impossibile importare la configurazione del server in presenza di Web Service Connector
  * Web Service Connector non funziona con più servizi Web

* Generic SQL:
  * Nessun tipo di oggetto elencato per l'attributo a valore singolo a cui si fa riferimento
  * L'importazione delta per la strategia Rilevamento modifiche elimina l'oggetto quando il valore viene rimosso alla tabella multivalore
  * OverflowException nel connettore GSQL con DB2 su AS/400

Lotus:
  * Aggiunta l'opzione tooenable\disable ricerca unità organizzative prima dell'apertura globalparameters della pagina

## <a name="114430"></a>1.1.443.0

Data di rilascio: marzo 2017

### <a name="enhancements"></a>Miglioramenti

* Generic SQL:</br>
  **Sintomi di scenario:** è una limitazione nota con connettore SQL in cui è solo consentire a un tipo di oggetto di riferimento tooone e richiedono un riferimento incrociato con membri hello. </br>
  **Descrizione soluzione:** In fase di elaborazione hello per i riferimenti sono stati "*" viene scelto l'opzione, verranno restituite tutte le combinazioni di tipi di oggetto motore di sincronizzazione toohello indietro.

>[!Important]
- In questo modo vengono creati molti segnaposti
- È necessario toomake hello denominazione sia univoco tra i tipi di oggetto.


* Generic LDAP:</br>
 **Scenario:** se solo alcuni contenitori sono selezionati in una partizione specifica, quindi ricerca hello ancora verrà eseguito in intera partizione. La partizione specifica sarà filtrata dal servizio di sincronizzazione ma non dal MA, il che potrebbe causare un calo delle prestazioni. </br>

 **Descrizione soluzione:** toomake codice modificato GLDAP connettore è possibile scorrere tutti i contenitori e cercare gli oggetti in ognuno di essi, anziché dover cercare nella partizione intero hello.


* Lotus Domino:

  **Scenario:** supporto dell'eliminazione della posta di Domino per la rimozione di un utente durante un'esportazione. </br>
  **Soluzione:** supporto dell'eliminazione della posta configurabile per la rimozione di un utente durante un'esportazione.

### <a name="fixed-issues"></a>Problemi risolti:
* Servizi Web generici:
 * Quando si modifica URL del servizio hello predefinita wsconfig SAP progetti tramite lo strumento di configurazione di servizio Web, quindi si verifica il seguente errore hello: Impossibile trovare una parte di percorso hello

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* Generic LDAP:
 * Il connettore GLDAP non vede tutti gli attributi in AD LDS
 * Procedura guidata interruzioni quando non viene rilevato alcun attributo UPN dallo schema di directory LDAP hello
 * Le importazioni differenziali generano errori di individuazione non presenti durante l'importazione completa, quando l'attributo "objectclass" non è selezionato
 * Una pagina di configurazione "Configurare le partizioni e gerarchie", non Mostra tutti gli oggetti cui tipo è uguale toohello partizione per i nuovi server hello generico  
LDAP. Essi mostravano solo gli oggetti della partizione di RootDSE.


* Generic SQL:
 * Correzione per il bug dell'attributo multivalore non importato per l'importazione differenziale watermark di Generic SQL
 * Quando si esportano valori di attributi multivalore eliminati/aggiunti, non vengono eliminati/aggiunti nell'origine dati.  


* Lotus Notes:
 * Un campo specifico "Nome completo" viene visualizzato nel metaverse hello correttamente tuttavia durante l'esportazione tooNotes hello valore per attributo hello è Null o vuota.
 * Correzione per l'errore di file di certificazione duplicato
 * Quando viene selezionato hello oggetto senza dati hello Lotus Domino connettore con altri oggetti quindi viene visualizzato l'errore individuazione hello durante l'esecuzione Full Import.
 * Durante l'importazione Delta è in esecuzione su hello connettore Lotus Domino, alla fine di hello di tale esecuzione, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe servizio talvolta restituisce un errore dell'applicazione.
 * L'appartenenza al gruppo globale funziona correttamente e viene mantenuta, tranne quando si esegue hello esportazione tootry tooremove un utente dall'appartenenza viene completata correttamente con un aggiornamento, ma non viene effettivamente rimossi utente hello dall'appartenenza Lotus Notes.
 * Una modalità di toochoose opportunità di esportazione come "Accoda elemento nella parte inferiore" è stato aggiunto nella configurazione GUI di Lotus MA tooappend nuovi elementi nella parte inferiore durante l'esportazione di hello per gli attributi multivalore.
 * Connettore aggiungerà hello necessaria logica toodelete hello file hello cartella della posta e l'ID insieme di credenziali.
 * Eliminare l'appartenenza non funziona per un membro NAB trasversale.
 * L'eliminazione dei valori da un attributo multivalore dovrebbe riuscire

## <a name="111170"></a>1.1.117.0
Data di rilascio: marzo 2016

**Nuovo connettore**  
Versione di hello iniziale [connettore SQL generico](active-directory-aadconnectsync-connector-genericsql.md).

**Nuove funzionalità:**

* Connettore Generic LDAP:
  * Aggiunta del supporto per l'importazione differenziale con Isode.
* Connettore Web Services:
  * Hello aggiornato csEntryChangeResult attività e setImportErrorCode attività tooallow oggetto gli errori a livello toobe restituito toohello indietro motore di sincronizzazione.
  * Hello aggiornato SAP6 e SAP6User modelli toouse hello nuovo oggetto errore di livello.
* Connettore Lotus Domino:
  * Per l'esportazione è necessario un file di certificazione per ogni rubrica. È possibile utilizzare hello stessa password per l'intera rilascio degli attestati toomake hello gestione più semplice.

**Problemi risolti:**

* Connettore Generic LDAP:
  * Per IBM Tivoli DS alcuni attributi di riferimento non venivano rilevati correttamente.
  * Per aprire LDAP durante un'importazione delta, gli spazi vuoti all'inizio di hello e alla fine di stringhe sono stati troncati.
  * Per Novell e NetIQ, un'esportazione che spostati di un oggetto tra le unità organizzative e contenitori e hello stesso tempo l'oggetto rinominato hello.
* Connettore Web Services:
  * Se il servizio web hello ha più endpoint per la stessa associazione, quindi hello Connector non correttamente individuare questi endpoint.
* Connettore Lotus Domino:
  * L'esportazione di hello fullName attributo tooa posta elettronica nel database non ha funzionato.
  * Un'esportazione che le aggiunte e rimosse membro da un gruppo, solo i membri aggiunti hello esportata.
  * Se un documento di note non è valido (hello attributo isValid set toofalse), quindi hello ha esito negativo connettore.

## <a name="older-releases"></a>Versioni precedenti
Prima di marzo 2016, hello connettori sono stati rilasciati come argomenti di supporto.

**Generic LDAP**

* [KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, settembre 2015
* [KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, marzo 2015
* [KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, gennaio 2015
* [KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, settembre 2014
* [KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, marzo 2014

**WebServices**

* [KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, settembre 2014

**PowerShell**

* [KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, settembre 2014

**Lotus Domino**

* [KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, settembre 2015
* [KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, marzo 2015
* [KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, agosto 2014
* [KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, febbraio 2014  
* [KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, ottobre 2013
* [KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, agosto 2013

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
