Für eine realistische KI‑Influencerin brauchst du vor allem Tools aus vier Bereichen: **Look/Charakter**, **Konsistenz**, **Bewegung/Video** und **Drumherum (Audio/Workflow)**.reddit+2​

## 1. Look & Charakter

- **Basis‑Modelle (SDXL, Flux, Wan‑Bildmodelle)**
    
    - Was: Große KI‑Modelle, die aus Text/Bild neue Bilder machen (realistische Portraits, Fashion, Szenen).hyperstack+1​
        
    - Wie: Du gibst Prompt + Einstellungen ein, das Modell erzeugt Einzelbilder deiner Influencerin (Gesicht, Körper, Outfits), die später als Referenz für Video dienen.cobaltexplorer+1​
        
- **LoRA (z.B. Instagirl V2, eigene Charakter‑LoRA)**
    
    - Was: Kleine Zusatz‑Modelle, die einen Stil oder eine bestimmte Person einem Basis‑Modell „aufprägen“ (Instagram‑Look, dein individueller Charakter).comfyui+2​
        
    - Wie: Du lädst im Workflow zuerst das Basis‑Modell, dann eine oder mehrere LoRAs mit einer Stärke (z.B. 0.7); sie verändern den Output Richtung gewünschtem Stil/Charakter.everlyheights+1​
        
- **Charakter‑LoRA‑Training (optional später)**
    
    - Was: Eigene LoRA trainieren nur auf dein OC‑Gesicht/Influencerin, damit sie in allen Posen wiedererkennbar bleibt.youtube​[everlyheights](https://everlyheights.tv/stablediffusion/create-consistent-original-character-loras-in-stable-diffusion/)​
        
    - Wie: Du sammelst 15–30 Bilder deines Charakters, trainierst daraus eine LoRA (online‑Trainer oder lokal), und nutzt sie dann wie jede andere LoRA im Workflow.[everlyheights](https://everlyheights.tv/stablediffusion/create-consistent-original-character-loras-in-stable-diffusion/)​youtube​
        

## 2. Konsistenz & Kontrolle im Bild

- **IP‑Adapter / Referenzbild‑Adapter**
    
    - Was: Module, die 1–5 Referenzbilder einlesen und Aussehen/Outfit im neuen Bild „festhalten“ – eine Art „leichte LoRA aus Bildern“.stable-diffusion-art+1​
        
    - Wie: Du gibst ein oder mehrere Portraits deiner Influencerin an den IP‑Adapter‑Node; der steuert dann das Hauptmodell, damit Gesicht und Style ähnlich bleiben, auch wenn Prompt/Posen wechseln.reddit+1​
        
- **ControlNet (OpenPose, Depth, HED, Face)**
    
    - Was: Zusätzliche Netze, die Form/Struktur steuern (Pose, Kontur, Tiefe, Gesichter).comfyui+1​
        
    - Wie:
        
        - OpenPose: Nutzt ein Strichmännchen/Skelett aus einem Bild/Video, damit der Körper genau dieser Pose folgt.[comfyui](https://comfyui.org/en/future-of-portrait-editing-with-controlnet-lora)​
            
        - Depth: Nutzt Tiefeninformation für korrekte Perspektive.
            
        - HED/Canny: Nutzt Kanten, damit Layout/Outfit erhalten bleiben.
            
        - Du verbindest sie mit deinem Hauptmodell, gibst ein Referenzbild ein – die KI ändert Stil/Charakter, behält aber Struktur/Posen.stable-diffusion-art+1​
            
- **Face‑Fix / Gesichts‑Inpainting**
    
    - Was: Zweiter Durchgang, der nur das Gesicht korrigiert (Schärfe, Symmetrie), wenn es in einem Frame verrutscht ist.youtube​[stable-diffusion-art](https://stable-diffusion-art.com/fast-consistent-character-video2video/)​
        
    - Wie: Workflow rendert zuerst das Video, erkennt dann Gesichter pro Frame und malt diese Bereiche mit einem spezialisierten Face‑Model/LoRA neu.[stable-diffusion-art](https://stable-diffusion-art.com/fast-consistent-character-video2video/)​
        

## 3. Bewegung & Video

- **Image‑to‑Video‑Modelle (Wan 2.x / Wan 2.5, andere Video‑Modelle)**
    
    - Was: Video‑Modelle, die aus einem Standbild + einem Prompt oder Referenzvideo einen bewegten Clip machen.stable-diffusion-art+2​
        
    - Wie:
        
        - Du wählst ein Standbild deiner Influencerin (Look aus Schritt 1).
            
        - Du gibst ein Bewegungs‑Referenzvideo (z.B. du selbst, wie du gestikulierst).
            
        - Der I2V‑Node erzeugt ein Video, in dem deine Figur diese Bewegung ausführt – mit Stil/Look aus Bild + LoRAs.runcomfy+2​
            
- **Motion‑/Pose‑Extraktion aus Video (OpenPose‑Video, andere Motion‑Kontroller)**
    
    - Was: Tools, die aus deinem Real‑Video pro Frame ein Skelett oder Motion‑Daten ziehen.comfyui+1​
        
    - Wie:
        
        - Du jagst dein Real‑Video durch OpenPose‑Video‑Nodes, bekommst eine Sequenz von Posen.
            
        - Diese Posen steuerst du dann mit ControlNet OpenPose im Bild/Video‑Modell an, damit die KI‑Influencerin 1:1 deine Bewegung nachmacht.stable-diffusion-art+1​
            
- **AI‑Motion‑Capture / VTuber‑Software (für Live)**
    
    - Was: Programme, die per Webcam oder Handy deine Mimik und Bewegung in Echtzeit auf ein 2D‑ oder 3D‑Avatar‑Rig übertragen.remocapp+1​
        
    - Wie: Du nutzt Tools wie Remocapp/VSeeFace & Co., um einen Avatar live zu bewegen; später können KI‑Modelle aus diesen Streams wieder hochwertige Clips generieren oder Outfits/Style drüberlegen.reddit+1​
        

## 4. ComfyUI‑Basics, die du wirklich verstehen solltest

- **Nodes / Workflows**
    
    - Was: Jeder Schritt (Modell laden, LoRA anwenden, ControlNet, I2V…) ist ein Node; alles zusammen ergibt deinen Influencer‑Pipeline‑Workflow.stable-diffusion-art+1​
        
    - Wie: Du verbindest Nodes von „Input“ (Prompt, Bilder, Videos) über „Modell‑Bearbeitung“ bis „Output“ (Bilder/Video‑Dateien) und kannst diesen Workflow immer wiederverwenden.blenderneko.github+1​
        
- **KSampler / Sampling‑Einstellungen**
    
    - Was: Der eigentliche Bild‑Sampler; kontrolliert Qualität, Stil und Rauschen (Steps, Sampler‑Typ, CFG).[comfyui](https://comfyui.org/en/future-of-portrait-editing-with-controlnet-lora)​
        
    - Wie: Höhere Steps = sauberere Details (langsamer); CFG steuert, wie streng das Modell dem Prompt folgt. Gute Werte sind wichtig, damit Gesichter stabil bleiben und nicht „flackern“.stable-diffusion-art+1​
        
- **Batch‑Generierung & Seeds**
    
    - Was: Mehrere Bilder/Frames mit derselben „Zufallsbasis“ erstellen (Seed), um Konsistenz zu erhöhen.[reddit](https://www.reddit.com/r/comfyui/comments/1cnbtez/i_need_recommendations_for_creating_consistent/)​
        
    - Wie: Du fixierst den Seed und generierst Varianten (Prompt, Pose, Outfit ändern); so bleibt der Charakter aber erkennbar derselbe.cobaltexplorer+1​
        
- **API‑Nodes (Wan 2.5, Seedance, Runway etc.)**
    
    - Was: Nodes, die nicht lokal rechnen, sondern Jobs zu einem Online‑Service schicken; dort läuft das schwere Video‑Modell.comfy+2​
        
    - Wie: Du trägst API‑Key ein, stellst Dauer/Resolution ein, schickst deinen Job – der Service gibt ein Video zurück, das im Workflow gespeichert oder weiterbearbeitet wird.comfy+2​
        

## 5. Audio, Stimme & Social

- **Text‑to‑Speech / Voice‑KI**
    
    - Was: KI‑Stimmen, mit denen deine Influencerin sprechen kann (eigene Stimme klonen oder komplett neue Persona).hypefy+1​
        
    - Wie: Du schreibst das Script, lässt es von der Voice‑KI sprechen, synchronisierst später Mundbewegungen per Lip‑Sync‑Tool mit dem generierten Video.d-id+1​
        
- **Lip‑Sync‑Tools**
    
    - Was: Passen Mundbewegungen an Audio an, damit deine Influencerin glaubwürdig spricht.popai+1​
        
    - Wie: Du gibst Video + Audio in ein Lip‑Sync‑Tool; es generiert Frame‑genaue Mundstellungen, teils direkt integriert in VTuber/Avatar‑Programme.d-id+1​
        

---

Wenn du möchtest, kann die nächste Antwort diese Liste in eine klare **Lern‑Reihenfolge** für dich umwandeln (z.B. 1. LoRAs & IP‑Adapter, 2. ControlNet, 3. I2V mit Wan, 4. Face‑Fix & Audio), damit du Schritt für Schritt ohne Überforderung reinkommst.

1. [https://www.reddit.com/r/comfyui/comments/1cnbtez/i_need_recommendations_for_creating_consistent/](https://www.reddit.com/r/comfyui/comments/1cnbtez/i_need_recommendations_for_creating_consistent/)
2. [https://comfyui.org/en/future-of-portrait-editing-with-controlnet-lora](https://comfyui.org/en/future-of-portrait-editing-with-controlnet-lora)
3. [https://hypefy.ai/blog/how-to-create-an-ai-influencer](https://hypefy.ai/blog/how-to-create-an-ai-influencer)
4. [https://www.hyperstack.cloud/blog/case-study/everything-you-need-to-know-about-stable-diffusion](https://www.hyperstack.cloud/blog/case-study/everything-you-need-to-know-about-stable-diffusion)
5. [https://comfy.icu/docs/models](https://comfy.icu/docs/models)
6. [https://cobaltexplorer.com/2023/06/character-sheets-for-stable-diffusion/](https://cobaltexplorer.com/2023/06/character-sheets-for-stable-diffusion/)
7. [https://everlyheights.tv/stablediffusion/create-consistent-original-character-loras-in-stable-diffusion/](https://everlyheights.tv/stablediffusion/create-consistent-original-character-loras-in-stable-diffusion/)
8. [https://www.youtube.com/watch?v=n_x44pTLpak](https://www.youtube.com/watch?v=n_x44pTLpak)
9. [https://stable-diffusion-art.com/fast-consistent-character-video2video/](https://stable-diffusion-art.com/fast-consistent-character-video2video/)
10. [https://www.youtube.com/watch?v=w8oJa0k2g1M](https://www.youtube.com/watch?v=w8oJa0k2g1M)
11. [https://stable-diffusion-art.com/wan-2-1/](https://stable-diffusion-art.com/wan-2-1/)
12. [https://www.runcomfy.com/de/models/wan-ai/wan2-5](https://www.runcomfy.com/de/models/wan-ai/wan2-5)
13. [https://blog.comfy.org/p/wan-25-preview-api-nodes-in-comfyui](https://blog.comfy.org/p/wan-25-preview-api-nodes-in-comfyui)
14. [https://docs.comfy.org/tutorials/video/wan/vace](https://docs.comfy.org/tutorials/video/wan/vace)
15. [https://remocapp.com/blog/posts/422/ai-motion-capture-vtuber-livestreams](https://remocapp.com/blog/posts/422/ai-motion-capture-vtuber-livestreams)
16. [https://arxiv.org/html/2503.00842v1](https://arxiv.org/html/2503.00842v1)
17. [https://www.reddit.com/r/vtubertech/comments/1c07hsa/portable_tracking_for_a_vtuber/](https://www.reddit.com/r/vtubertech/comments/1c07hsa/portable_tracking_for_a_vtuber/)
18. [https://stable-diffusion-art.com/comfyui/](https://stable-diffusion-art.com/comfyui/)
19. [https://blenderneko.github.io/ComfyUI-docs/](https://blenderneko.github.io/ComfyUI-docs/)
20. [https://docs.comfy.org/tutorials/partner-nodes/runway/video-generation](https://docs.comfy.org/tutorials/partner-nodes/runway/video-generation)
21. [https://docs.comfy.org/tutorials/partner-nodes/pricing](https://docs.comfy.org/tutorials/partner-nodes/pricing)
22. [https://www.d-id.com/blog/ai-video-influencer-marketing/](https://www.d-id.com/blog/ai-video-influencer-marketing/)
23. [https://www.popai.pro/resources/ai-tools/how-to-create-ai-influencer-videos/](https://www.popai.pro/resources/ai-tools/how-to-create-ai-influencer-videos/)