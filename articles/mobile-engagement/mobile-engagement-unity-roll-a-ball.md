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
# <span data-ttu-id="ca225-103"><a id="unity-roll-a-ball"></a>Creare il gioco Roll a Ball di Unity</span><span class="sxs-lookup"><span data-stu-id="ca225-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="ca225-104">In questa esercitazione vengono illustrati i passaggi principali di hello per leggermente modificata [Unity eseguire il rollback di un'esercitazione palla](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="ca225-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="ca225-105">Il gioco di esempio è costituito da un oggetto sferico 'player' che è controllato dall'utente di app hello e obiettivo di hello di gioco hello è too'collect' ritirabili oggetti dall'oggetto lettore di hello collisione con questi oggetti ritirabili.</span><span class="sxs-lookup"><span data-stu-id="ca225-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="ca225-106">Ciò presuppone una certa conoscenza di base dell'ambiente dell'editor di Unity.</span><span class="sxs-lookup"><span data-stu-id="ca225-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="ca225-107">Se si verificano problemi, quindi è consigliabile consultare l'esercitazione completa toohello.</span><span class="sxs-lookup"><span data-stu-id="ca225-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="ca225-108">Impostazione di gioco hello</span><span class="sxs-lookup"><span data-stu-id="ca225-108">Setting up hello game</span></span>
<span data-ttu-id="ca225-109">sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="ca225-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="ca225-110">Aprire l'**editor Unity** e fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="ca225-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="ca225-111">Fornire **nome del progetto** & **percorso**, selezionare **3D** e fare clic su **Create project**.</span><span class="sxs-lookup"><span data-stu-id="ca225-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="ca225-112">Salva scena predefinito hello appena creato come parte del nuovo progetto hello come con nome hello **MiniGame** all'interno di un nuovo  **\_scene** cartella **asset** cartella:</span><span class="sxs-lookup"><span data-stu-id="ca225-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="ca225-113">Creare un **oggetto 3D -> piano** come riproduzione hello campo e rinominare questo oggetto piano come **terra**</span><span class="sxs-lookup"><span data-stu-id="ca225-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="ca225-114">Componente di trasformazione hello reimpostazione per questo **terra** in modo che sia in hello origine dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="ca225-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="ca225-115">Deselezionare **Mostra griglia** da **menu Gizmos** per hello **terra** oggetto.</span><span class="sxs-lookup"><span data-stu-id="ca225-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="ca225-116">Hello aggiornamento **scala** componente hello **terra** oggetto toobe [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="ca225-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="ca225-117">Aggiungere un nuovo **oggetto 3D -> sfera** progetto toohello e rinominare sfera di questo oggetto come **Player**.</span><span class="sxs-lookup"><span data-stu-id="ca225-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="ca225-118">Seleziona hello **Player** dell'oggetto e fare clic su **Reimposta trasformazione** oggetto di piano toohello simile.</span><span class="sxs-lookup"><span data-stu-id="ca225-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="ca225-119">Aggiornamento **trasformazione -> posizione -> coordinata Y** componente hello Player Y come 0,5.</span><span class="sxs-lookup"><span data-stu-id="ca225-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="ca225-120">Creare una nuova cartella denominata **materiali** nel progetto hello in cui verrà creata player hello toocolor materiale di hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="ca225-121">Creare un nuovo **materiale** chiamato **Background** in questa cartella.</span><span class="sxs-lookup"><span data-stu-id="ca225-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="ca225-122">Aggiornare i colori hello del materiale hello aggiornando hello **Albedo** proprietà di esso.</span><span class="sxs-lookup"><span data-stu-id="ca225-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="ca225-123">È possibile selezionare valori RGB hello di [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="ca225-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="ca225-124">Trascinare questo materiale in hello scena vista tooapply colore toohello **terra** oggetto.</span><span class="sxs-lookup"><span data-stu-id="ca225-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="ca225-125">Infine aggiornare hello **trasformazione -> rotazione -> Y** too60 sull'oggetto luce direzionale hello per maggiore chiarezza.</span><span class="sxs-lookup"><span data-stu-id="ca225-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="ca225-126">Lettore hello mobile</span><span class="sxs-lookup"><span data-stu-id="ca225-126">Moving hello player</span></span>
<span data-ttu-id="ca225-127">sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="ca225-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="ca225-128">Aggiungere un **RigidBody** componente toohello **Player** oggetto.</span><span class="sxs-lookup"><span data-stu-id="ca225-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="ca225-129">Creare una nuova cartella denominata **script** in hello progetto.</span><span class="sxs-lookup"><span data-stu-id="ca225-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="ca225-130">Fare clic su **Add Component-> New Script -> C# Script**.</span><span class="sxs-lookup"><span data-stu-id="ca225-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="ca225-131">Assegnargli il nome **PlayerController** e fare clic su **Create and Add**.</span><span class="sxs-lookup"><span data-stu-id="ca225-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="ca225-132">Verrà creata e collegare un oggetto di Windows Media Player toohello di script.</span><span class="sxs-lookup"><span data-stu-id="ca225-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="ca225-133">Spostare lo script in hello **script** cartella nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="ca225-134">Aprire hello script per la modifica nell'editor di script preferito, aggiornare il codice di script hello con hello seguente di codice e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="ca225-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
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
6. <span data-ttu-id="ca225-135">Si noti lo script hello precedenti viene utilizzato un **velocità** proprietà.</span><span class="sxs-lookup"><span data-stu-id="ca225-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="ca225-136">Nell'editor di Unity hello, aggiornare hello velocità proprietà too10.</span><span class="sxs-lookup"><span data-stu-id="ca225-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="ca225-137">Riscontri **riprodurre** nell'Editor di Unity hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="ca225-138">A questo punto dovrebbe essere palla hello toocontrol in grado di utilizzare tastiera hello e deve ruotare e spostarsi all'interno.</span><span class="sxs-lookup"><span data-stu-id="ca225-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="ca225-139">Fotocamera hello mobile</span><span class="sxs-lookup"><span data-stu-id="ca225-139">Moving hello camera</span></span>
<span data-ttu-id="ca225-140">sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) e verrà associata hello **telecamera principale** toohello **Player** oggetto.</span><span class="sxs-lookup"><span data-stu-id="ca225-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="ca225-141">Hello aggiornamento **Transform.Position** toobe X = 0, Y = 10.5, Z = da-10.</span><span class="sxs-lookup"><span data-stu-id="ca225-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="ca225-142">Hello aggiornamento **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="ca225-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="ca225-143">Aggiungere un nuovo script chiamato **CameraController** toohello **MainCamera** e spostarla nella cartella Scripts hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="ca225-144">Aprire script hello per la modifica e aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="ca225-144">Open up hello script for editing and add hello following code in it:</span></span>
   
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
5. <span data-ttu-id="ca225-145">Nell'ambiente di Unity - trascinare variabile Player hello slot Player hello per l'oggetto principale fotocamera hello hello due sono associati tra loro.</span><span class="sxs-lookup"><span data-stu-id="ca225-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="ca225-146">Se si riscontra Play nell'editor di Unity hello e oggetto lettore palla hello ruota quindi verrà visualizzata hello fotocamera segue movimento hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="ca225-147">Configurare l'area di riproduzione hello</span><span class="sxs-lookup"><span data-stu-id="ca225-147">Setting up hello Play area</span></span>
<span data-ttu-id="ca225-148">sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="ca225-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="ca225-149">Verrà creata hello lati hello terra in modo che hello oggetto lettore palla non consegnare area riproduzione hello nel suo movimento.</span><span class="sxs-lookup"><span data-stu-id="ca225-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="ca225-150">Fare clic su **Create -> Create Empty -> Game Object** e assegnare il nome **Walls**</span><span class="sxs-lookup"><span data-stu-id="ca225-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="ca225-151">In questo oggetto Walls creare un nuovo oggetto andando su **3D Object -> Cube** e assegnare il nome "West wall".</span><span class="sxs-lookup"><span data-stu-id="ca225-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="ca225-152">Hello aggiornamento **trasformazione -> posizione** e **trasformazione -> scala** per questo oggetto parete occidentale.</span><span class="sxs-lookup"><span data-stu-id="ca225-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="ca225-153">Duplicare hello occidentale parete toocreate un **parete orientale** con hello aggiornato trasformare posizione e scala.</span><span class="sxs-lookup"><span data-stu-id="ca225-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="ca225-154">Duplicare hello orientale parete toocreate un **parete settentrionale** con hello aggiornato trasformare posizione e scala.</span><span class="sxs-lookup"><span data-stu-id="ca225-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="ca225-155">Duplicare parete settentrionale hello e creare un **parete meridionale** con hello aggiornato trasformare posizione e scala.</span><span class="sxs-lookup"><span data-stu-id="ca225-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="ca225-156">Creazione di oggetti da collezione</span><span class="sxs-lookup"><span data-stu-id="ca225-156">Creating Collectible objects</span></span>
<span data-ttu-id="ca225-157">sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="ca225-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="ca225-158">Si creerà alcune interessante ricerca oggetti che costituiranno set hello oggetti ritirabile quale oggetto lettore palla hello deve too'collect' da collisione con essi.</span><span class="sxs-lookup"><span data-stu-id="ca225-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="ca225-159">Creare un nuovo **oggetto 3D Cube** e denominarlo Pickup.</span><span class="sxs-lookup"><span data-stu-id="ca225-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="ca225-160">Regolare hello **trasformazione -> rotazione** & **trasformazione -> scala** dell'oggetto prelievo hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="ca225-161">Creare e collegare un **nuovo Script c#** chiamato **Rotator** toohello prelievo oggetto.</span><span class="sxs-lookup"><span data-stu-id="ca225-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="ca225-162">Assicurarsi che script di hello tooput nella cartella script hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="ca225-163">Aprire lo script per la modifica e aggiornarlo hello toobe seguenti:</span><span class="sxs-lookup"><span data-stu-id="ca225-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="ca225-164">Modalità di gioco hello hit hello Editor di Unity e il prelievo oggetti-Mostra ora essere rotazione sul suo asse.</span><span class="sxs-lookup"><span data-stu-id="ca225-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="ca225-165">Creare una nuova cartella denominata **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="ca225-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="ca225-166">Hello trascinare **prelievo** dell'oggetto e inserirlo nella cartella Prefabs hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="ca225-167">Creare un nuovo **oggetto Empty Game** chiamato **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="ca225-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="ca225-168">Reimpostare tooorigin relativa posizione e quindi trascinarlo hello prelievo in questo oggetto gioco.</span><span class="sxs-lookup"><span data-stu-id="ca225-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="ca225-169">Hello duplicato **prelievo** dell'oggetto e viene distribuito in hello **terra** oggetto attorno hello **Player** oggetto aggiornando hello **X e Z del Transform.Position**  valori in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="ca225-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="ca225-170">Creare un **nuovo materiale** chiamato **prelievo** e aggiornarlo toobe rosso nel colore aggiornando hello **proprietà Albedo** toowhat simile è per l'aggiornamento hello terra dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="ca225-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="ca225-171">Applicare gli oggetti di hello tooall materiale hello 4 prelievo.</span><span class="sxs-lookup"><span data-stu-id="ca225-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="ca225-172">La raccolta di oggetti di prelievo hello</span><span class="sxs-lookup"><span data-stu-id="ca225-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="ca225-173">sono i passaggi Hello da hello [esercitazione Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="ca225-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="ca225-174">Hello Player verrà aggiornato in modo che sia in grado di too'collect' hello oggetti prelievo da collisione con essi.</span><span class="sxs-lookup"><span data-stu-id="ca225-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="ca225-175">Aprire la console di hello **PlayerController** oggetto lettore toohello associata per la modifica di script e aggiornarlo toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ca225-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
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
2. <span data-ttu-id="ca225-176">Creare un nuovo **Tag** chiamato **Seleziona backup** (deve corrispondere novità nello script hello)</span><span class="sxs-lookup"><span data-stu-id="ca225-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="ca225-177">Applicare questo **Tag** oggetto prelievo Prefab toohello.</span><span class="sxs-lookup"><span data-stu-id="ca225-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="ca225-178">Abilitare **IsTrigger** casella di controllo per l'oggetto Prefab hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="ca225-179">Aggiungere un oggetto di Prefab tooPickup corpo rigida.</span><span class="sxs-lookup"><span data-stu-id="ca225-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="ca225-180">Per ottimizzare le prestazioni verranno aggiornati collider di hello statici sono stati utilizzati collider dinamica tooa.</span><span class="sxs-lookup"><span data-stu-id="ca225-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="ca225-181">Verificare infine hello **IsKinematic** proprietà dell'oggetto prefab hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="ca225-182">Riscontri **riprodurre** nell'editor di Unity hello e si sarà in grado di tooplay questo **il rollback di una palla** gioco spostando hello oggetto lettore utilizzando i tasti di direzione input.</span><span class="sxs-lookup"><span data-stu-id="ca225-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="ca225-183">Aggiornamento hello gioco per dispositivi mobili play</span><span class="sxs-lookup"><span data-stu-id="ca225-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="ca225-184">Nelle sezioni Hello precedenti esercitazione di base hello concluso da Unity.</span><span class="sxs-lookup"><span data-stu-id="ca225-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="ca225-185">Ora si modificherà hello gioco toomake il dispositivo mobile descrittivo.</span><span class="sxs-lookup"><span data-stu-id="ca225-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="ca225-186">Si noti che è stata utilizzata input da tastiera per hello gioco finora per il test.</span><span class="sxs-lookup"><span data-stu-id="ca225-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="ca225-187">Ora è necessario modificarlo in modo da poter controllare Windows Media player hello utilizzando movimento hello di hello telefono ad esempio utilizzando accelerometro come input hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="ca225-188">Aprire la console di hello **PlayerController** script per la modifica e aggiornamento hello **FixedUpdate** movimento di hello toouse metodo dall'oggetto lettore di hello accelerometro toomove hello.</span><span class="sxs-lookup"><span data-stu-id="ca225-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="ca225-189">Questa esercitazione si conclude una base creazione di gioco con Unity e sarà possibile distribuirla in un dispositivo di un gioco di hello tooplay scelta.</span><span class="sxs-lookup"><span data-stu-id="ca225-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

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













