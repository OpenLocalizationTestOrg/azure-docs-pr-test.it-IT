---
title: aaaUnity eseguire il rollback di un'esercitazione palla
description: "Passaggi toocreate hello di rollback Unity classico un gioco palla che è un prerequisito per tutte le esercitazioni Unity Engagement Mobile"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a id="unity-roll-a-ball"></a>Creare il gioco Roll a Ball di Unity
In questa esercitazione vengono illustrati i passaggi principali di hello per leggermente modificata [Unity eseguire il rollback di un'esercitazione palla](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). Il gioco di esempio è costituito da un oggetto sferico 'player' che è controllato dall'utente di app hello e obiettivo di hello di gioco hello è too'collect' ritirabili oggetti dall'oggetto lettore di hello collisione con questi oggetti ritirabili. Ciò presuppone una certa conoscenza di base dell'ambiente dell'editor di Unity. Se si verificano problemi, quindi è consigliabile consultare l'esercitazione completa toohello. 

### <a name="setting-up-hello-game"></a>Impostazione di gioco hello
sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. Aprire l'**editor Unity** e fare clic su **New**. 
   
    ![][51] 
2. Fornire **nome del progetto** & **percorso**, selezionare **3D** e fare clic su **Create project**.
   
    ![][52]
3. Salva scena predefinito hello appena creato come parte del nuovo progetto hello come con nome hello **MiniGame** all'interno di un nuovo  **\_scene** cartella **asset** cartella:
   
    ![][53]
4. Creare un **oggetto 3D -> piano** come riproduzione hello campo e rinominare questo oggetto piano come **terra**
   
    ![][1]
5. Componente di trasformazione hello reimpostazione per questo **terra** in modo che sia in hello origine dell'oggetto. 
   
    ![][3]
6. Deselezionare **Mostra griglia** da **menu Gizmos** per hello **terra** oggetto.
   
    ![][4]
7. Hello aggiornamento **scala** componente hello **terra** oggetto toobe [X = 2, Y = 1, Z = 2]. 
   
    ![][5]
8. Aggiungere un nuovo **oggetto 3D -> sfera** progetto toohello e rinominare sfera di questo oggetto come **Player**. 
   
    ![][6]
9. Seleziona hello **Player** dell'oggetto e fare clic su **Reimposta trasformazione** oggetto di piano toohello simile. 
10. Aggiornamento **trasformazione -> posizione -> coordinata Y** componente hello Player Y come 0,5.  
    
    ![][7]
11. Creare una nuova cartella denominata **materiali** nel progetto hello in cui verrà creata player hello toocolor materiale di hello. 
12. Creare un nuovo **materiale** chiamato **Background** in questa cartella. 
    
    ![][8]
13. Aggiornare i colori hello del materiale hello aggiornando hello **Albedo** proprietà di esso. È possibile selezionare valori RGB hello di [0,32,64]. 
    
    ![][9]
14. Trascinare questo materiale in hello scena vista tooapply colore toohello **terra** oggetto. 
    
    ![][10]
15. Infine aggiornare hello **trasformazione -> rotazione -> Y** too60 sull'oggetto luce direzionale hello per maggiore chiarezza. 
    
    ![][12]

### <a name="moving-hello-player"></a>Lettore hello mobile
sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. Aggiungere un **RigidBody** componente toohello **Player** oggetto. 
   
    ![][13]
2. Creare una nuova cartella denominata **script** in hello progetto. 
3. Fare clic su **Add Component-> New Script -> C# Script**. Assegnargli il nome **PlayerController** e fare clic su **Create and Add**. Verrà creata e collegare un oggetto di Windows Media Player toohello di script.  
   
    ![][14]
4. Spostare lo script in hello **script** cartella nel progetto hello. 
5. Aprire hello script per la modifica nell'editor di script preferito, aggiornare il codice di script hello con hello seguente di codice e salvarlo. 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. Si noti lo script hello precedenti viene utilizzato un **velocità** proprietà. Nell'editor di Unity hello, aggiornare hello velocità proprietà too10.  
   
    ![][15]
7. Riscontri **riprodurre** nell'Editor di Unity hello. A questo punto dovrebbe essere palla hello toocontrol in grado di utilizzare tastiera hello e deve ruotare e spostarsi all'interno. 

### <a name="moving-hello-camera"></a>Fotocamera hello mobile
sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) e verrà associata hello **telecamera principale** toohello **Player** oggetto. 

1. Hello aggiornamento **Transform.Position** toobe X = 0, Y = 10.5, Z = da-10.  
2. Hello aggiornamento **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.  
   
    ![][16]
3. Aggiungere un nuovo script chiamato **CameraController** toohello **MainCamera** e spostarla nella cartella Scripts hello. 
   
    ![][17]
4. Aprire script hello per la modifica e aggiungere hello seguente codice:
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. Nell'ambiente di Unity - trascinare variabile Player hello slot Player hello per l'oggetto principale fotocamera hello hello due sono associati tra loro. 
   
    ![][18]
6. Se si riscontra Play nell'editor di Unity hello e oggetto lettore palla hello ruota quindi verrà visualizzata hello fotocamera segue movimento hello.  

### <a name="setting-up-hello-play-area"></a>Configurare l'area di riproduzione hello
sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141). Verrà creata hello lati hello terra in modo che hello oggetto lettore palla non consegnare area riproduzione hello nel suo movimento. 

1. Fare clic su **Create -> Create Empty -> Game Object** e assegnare il nome **Walls**
   
    ![][19]
2. In questo oggetto Walls creare un nuovo oggetto andando su **3D Object -> Cube** e assegnare il nome "West wall". 
   
    ![][20]
3. Hello aggiornamento **trasformazione -> posizione** e **trasformazione -> scala** per questo oggetto parete occidentale. 
   
    ![][21]
4. Duplicare hello occidentale parete toocreate un **parete orientale** con hello aggiornato trasformare posizione e scala. 
   
    ![][22]
5. Duplicare hello orientale parete toocreate un **parete settentrionale** con hello aggiornato trasformare posizione e scala. 
   
    ![][23]
6. Duplicare parete settentrionale hello e creare un **parete meridionale** con hello aggiornato trasformare posizione e scala. 
   
    ![][24]

### <a name="creating-collectible-objects"></a>Creazione di oggetti da collezione
sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141). Si creerà alcune interessante ricerca oggetti che costituiranno set hello oggetti ritirabile quale oggetto lettore palla hello deve too'collect' da collisione con essi. 

1. Creare un nuovo **oggetto 3D Cube** e denominarlo Pickup. 
2. Regolare hello **trasformazione -> rotazione** & **trasformazione -> scala** dell'oggetto prelievo hello. 
   
    ![][25]
3. Creare e collegare un **nuovo Script c#** chiamato **Rotator** toohello prelievo oggetto. Assicurarsi che script di hello tooput nella cartella script hello. 
   
    ![][26]
4. Aprire lo script per la modifica e aggiornarlo hello toobe seguenti: 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. Modalità di gioco hello hit hello Editor di Unity e il prelievo oggetti-Mostra ora essere rotazione sul suo asse.
6. Creare una nuova cartella denominata **Prefabs** 
   
    ![][27]
7. Hello trascinare **prelievo** dell'oggetto e inserirlo nella cartella Prefabs hello.
   
    ![][28]
8. Creare un nuovo **oggetto Empty Game** chiamato **Pickups**. Reimpostare tooorigin relativa posizione e quindi trascinarlo hello prelievo in questo oggetto gioco.  
   
    ![][29]
9. Hello duplicato **prelievo** dell'oggetto e viene distribuito in hello **terra** oggetto attorno hello **Player** oggetto aggiornando hello **X e Z del Transform.Position**  valori in modo appropriato. 
   
    ![][30]
10. Creare un **nuovo materiale** chiamato **prelievo** e aggiornarlo toobe rosso nel colore aggiornando hello **proprietà Albedo** toowhat simile è per l'aggiornamento hello terra dell'oggetto. 
    
    ![][31]
11. Applicare gli oggetti di hello tooall materiale hello 4 prelievo.
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>La raccolta di oggetti di prelievo hello
sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141). Hello Player verrà aggiornato in modo che sia in grado di too'collect' hello oggetti prelievo da collisione con essi. 

1. Aprire la console di hello **PlayerController** oggetto lettore toohello associata per la modifica di script e aggiornarlo toohello seguenti:  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. Creare un nuovo **Tag** chiamato **Seleziona backup** (deve corrispondere novità nello script hello)  
   
    ![][33]
   
    ![][34]
3. Applicare questo **Tag** oggetto prelievo Prefab toohello. 
   
    ![][35]
4. Abilitare **IsTrigger** casella di controllo per l'oggetto Prefab hello.
   
    ![][36]
5. Aggiungere un oggetto di Prefab tooPickup corpo rigida. Per ottimizzare le prestazioni verranno aggiornati collider di hello statici sono stati utilizzati collider dinamica tooa. 
   
    ![][37]
6. Verificare infine hello **IsKinematic** proprietà dell'oggetto prefab hello. 
   
    ![][38]
7. Riscontri **riprodurre** nell'editor di Unity hello e si sarà in grado di tooplay questo **il rollback di una palla** gioco spostando hello oggetto lettore utilizzando i tasti di direzione input. 

### <a name="updating-hello-game-for-mobile-play"></a>Aggiornamento hello gioco per dispositivi mobili play
Nelle sezioni Hello precedenti esercitazione di base hello concluso da Unity. Ora si modificherà hello gioco toomake il dispositivo mobile descrittivo. Si noti che è stata utilizzata input da tastiera per hello gioco finora per il test. Ora è necessario modificarlo in modo da poter controllare Windows Media player hello utilizzando movimento hello di hello telefono ad esempio utilizzando accelerometro come input hello. 

Aprire la console di hello **PlayerController** script per la modifica e aggiornamento hello **FixedUpdate** movimento di hello toouse metodo dall'oggetto lettore di hello accelerometro toomove hello. 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

Questa esercitazione si conclude una base creazione di gioco con Unity e sarà possibile distribuirla in un dispositivo di un gioco di hello tooplay scelta. 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













