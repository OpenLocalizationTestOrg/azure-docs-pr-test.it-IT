---
title: gli eventi per le macchine virtuali Windows in Azure aaaScheduled | Documenti Microsoft
description: Eventi pianificati utilizzando il servizio Azure metadati hello per nelle macchine virtuali di Windows.
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a>Servizio metadati di Azure: eventi pianificati (anteprima) per VM Windows

> [!NOTE] 
> Le anteprime vengono apportate tooyou disponibili nella condizione hello che accetti toohello condizioni di utilizzo. Per altre informazioni, vedere [Condizioni Supplementari di Microsoft Azure le Anteprime di Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Gli eventi pianificati è uno dei servizi secondari hello in hello servizio metadati di Azure. Presenta informazioni sugli eventi imminenti, ad esempio i riavvii, in modo che l'applicazione possa prepararsi di conseguenza e limitare le interruzioni. Il servizio è disponibile per tutti i tipi di macchine virtuali di Azure, inclusi PaaS e IaaS. Gli eventi pianificati offre le attività di prevenzione di macchina virtuale ora tooperform effetto hello toominimize di un evento. 

Eventi pianificati è disponibile per VM sia Linux che Windows. Per informazioni su Eventi pianificati in Linux, vedere [Eventi pianificati per macchine virtuali Linux](../windows/scheduled-events.md).

## <a name="why-scheduled-events"></a>Perché usare gli eventi pianificati

Con agli eventi pianificati, è possibile eseguire passaggi impatto hello toolimit di piattaforma intiated manutenzione o le azioni avviate dall'utente nel servizio. 

Carichi di lavoro multi-istanza, che utilizza lo stato di replica tecniche toomaintain, potrebbe essere vulnerabile toooutages tra più istanze in corso. Tali interruzioni potrebbero comportare attività costose, ad esempio, la ricompilazione degli indici, o addirittura una perdita di replica. 

In molti altri casi, hello complessiva disponibilità del servizio può essere migliorata eseguendo la sequenza di arresto, ad esempio completamento (o annullamento) pertanto le transazioni, la riassegnazione attività tooother macchine virtuali in cluster hello (failover manuale), o la rimozione di hello Macchina virtuale da un pool di bilanciamento del carico di rete. 

Vi sono casi in cui informando un amministratore su un evento futuro o registrazione dell'evento contribuire a migliorare l'efficienza hello di applicazioni ospitate nel cloud hello.

Casi d'uso di Azure Metadata Service superfici agli eventi pianificati seguenti hello:
-   Manutenzione avviata dalla piattaforma, ad esempio implementazione del sistema operativo host
-   Chiamate avviate dall'utente, ad esempio riavvii iniziati dall'utente o ridistribuzione di una macchina virtuale


## <a name="hello-basics"></a>Nozioni di base Hello  

Servizio di metadati di Azure espone informazioni sull'esecuzione di macchine virtuali tramite un Endpoint REST accessibile dall'interno di hello macchina virtuale. informazioni Hello sono disponibile tramite un indirizzo IP non instradabile, in modo che non è esposta all'esterno di hello macchina virtuale.

### <a name="scope"></a>Scope
Gli eventi pianificati sono tooall esposto macchine virtuali in un servizio cloud o tooall macchine virtuali in un Set di disponibilità. Di conseguenza, è consigliabile controllare hello `Resources` campo hello evento tooidentify che le macchine virtuali verranno toobe interessati. 

### <a name="discovering-hello-endpoint"></a>Individuazione di endpoint hello
In caso di hello in cui viene creata una macchina virtuale in una rete virtuale (VNet), è disponibile da un IP statico non instradabile, servizio metadati hello `169.254.169.254`.
Se hello macchina virtuale non è stato creato in una rete virtuale, il case predefinito hello per servizi cloud e le macchine virtuali classiche, logica aggiuntiva è necessario toodiscover hello endpoint toouse. Vedere come troppo toothis esempio toolearn[individua endpoint host hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Controllo delle versioni 
Hello servizio metadati dell'istanza viene creata. Le versioni sono obbligatorie e la versione corrente di hello è `2017-03-01`.

> [!NOTE] 
> Versioni precedenti di anteprima di eventi pianificati supportati {più recente} come hello. api-version. Questo formato non è più supportato e verrà rimossa in futuro hello.

### <a name="using-headers"></a>Uso delle intestazioni
Quando si eseguono query hello Metadata Service, è necessario specificare l'intestazione di hello `Metadata: true` tooensure hello richiesta non è stata reindirizzata accidentalmente.

### <a name="enabling-scheduled-events"></a>Attivazione degli eventi pianificati
Hello prima volta che si effettua una richiesta per gli eventi pianificati, Azure consente implicitamente funzionalità hello sulla macchina virtuale. Di conseguenza, è possibile aspettarsi una risposta ritardata nella prima chiamata di backup tootwo minuti.

### <a name="user-initiated-maintenance"></a>Manutenzione avviata dall'utente
Manutenzione delle macchine virtuali tramite il portale di Azure, hello API, CLI, avviata dall'utente o PowerShell genera un evento pianificato. Questo consente la logica di preparazione tootest hello manutenzione dell'applicazione e tooprepare l'applicazione per la manutenzione avviata dall'utente.

Il riavvio di una macchina virtuale pianifica un evento di tipo `Reboot`. La ridistribuzione di una macchina virtuale pianifica un evento di tipo `Redeploy`.

> [!NOTE] 
> Attualmente è possibile pianificare un massimo di 10 operazioni di manutenzione avviata dall'utente. Questo limite viene aumentato prima della disponibilità generale di eventi pianificati.

> [!NOTE] 
> Attualmente la manutenzione avviata dall'utente che dà luogo a eventi pianificati non è configurabile. Questa funzionalità è pianificata per una versione successiva.

## <a name="using-hello-api"></a>Tramite l'API di hello

### <a name="query-for-events"></a>Query per gli eventi
È possibile eseguire una query per gli eventi pianificati sufficiente chiamata hello seguenti:

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

Una risposta contiene una serie di eventi pianificati. Una serie vuota indica che al momento non sono presenti eventi pianificati.
In caso di hello in cui sono presenti eventi pianificati, risposta hello contiene una matrice di eventi: 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>Proprietà degli eventi
|Proprietà  |  Descrizione |
| - | - |
| EventId | Identificatore globalmente univoco per l'evento. <br><br> Esempio: <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| EventType | Impatto che l'evento causa. <br><br> Valori: <br><ul><li> `Freeze`: hello macchina virtuale è pianificato toopause per alcuni secondi. Hello della CPU è sospesa, ma non ha alcun impatto su memoria, i file aperti o connessioni di rete. <li>`Reboot`: hello macchina virtuale è pianificata per riavviare il sistema (memoria non persistente viene persa). <li>`Redeploy`: hello macchina virtuale è pianificato toomove tooanother nodo (dischi temporanei andranno persi). |
| ResourceType | Tipo di risorsa su cui l'evento influisce. <br><br> Valori: <ul><li>`VirtualMachine`|
| Risorse| Elenco delle risorse su cui l'evento influisce. Questo è garantito macchine toocontain da almeno uno [dominio di aggiornamento](manage-availability.md), ma non può contenere tutti i computer hello UD. <br><br> Esempio: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Event Status | Stato dell'evento. <br><br> Valori: <ul><li>`Scheduled`: Questo evento è pianificato toostart dopo il tempo di hello specificato hello `NotBefore` proprietà.<li>`Started`: l'evento si è avviato.</ul> Non `Completed` o simile viene sempre fornito; evento hello non verrà restituito al termine dell'evento hello.
| NotBefore| Tempo dopo il quale l'evento può essere avviato. <br><br> Esempio: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Pianificazione degli eventi
Ogni evento è pianificata una quantità minima di tempo in futuro hello dipende dal tipo di evento. Questo tempo si riflette in una proprietà `NotBefore` dell'evento. 

|EventType  | Minimum Notice |
| - | - |
| Freeze| 15 minuti |
| Reboot | 15 minuti |
| Ripetere la distribuzione | 10 minuti |

### <a name="starting-an-event"></a>Avvio di un evento 

Dopo aver appreso di un imminente evento e completato la logica per l'arresto normale, è possibile approvare eventi in attesa di hello effettuando un `POST` chiamare il servizio metadati toohello con hello `EventId`. Ciò indica che è possibile abbreviare notifica minimo hello tooAzure ora (sempre). 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> Riconoscimento di un evento consente hello evento tooproceed per tutti i `Resources` nell'evento hello, non solo hello macchina virtuale che riconosce l'evento hello. È pertanto possibile tooelect un acknowledgement leader toocoordinate hello, che può essere semplice come macchina di prima hello in hello `Resources` campo.


## <a name="powershell-sample"></a>Esempio PowerShell 

Hello seguenti query di esempio hello servizio metadati per gli eventi pianificati e approva ogni evento in sospeso.

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a>Esempio C\# 

Hello esempio seguente è un semplice client che comunica con il servizio di metadati hello.

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

Gli eventi pianificati possono essere rappresentati mediante hello strutture di dati seguenti:

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

Hello seguenti query di esempio hello servizio metadati per gli eventi pianificati e approva ogni evento in sospeso.

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a>Esempio Python 

Hello seguenti query di esempio hello servizio metadati per gli eventi pianificati e approva ogni evento in sospeso.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Passaggi successivi 

- Altre informazioni sulle API disponibili in hello hello [servizio metadati dell'istanza](instance-metadata-service.md).
- Informazioni sulla [manutenzione pianificata per le macchine virtuali Windows in Azure](planned-maintenance.md).

