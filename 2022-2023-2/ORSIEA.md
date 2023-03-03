# Osztott rendszerek specifikációja és implementációja

# 1. EA

- Fogalmak tömege lesz
- Leggyengébb előfeltétel a leggyengébb előfeltétele a tárgynak és a programozásnak is
- Időtől függő logika kell a programozáshoz, párhuzamaos programozáshoz

- Bevezetés a programozásba
    - Fóti Ákos
- Párhuzamos és elosztott programozás
    - Horváth Zoltán
    - Tárgymutató - fogalmak
    - Tételek és lemmák jegyzéke
    - Jelölések jegyzéke - Gyakran használt jelölések
- Ajánlott irodalom
    - Parallel Program Design - Chendy K.M., Mistr J.
    - 1978 Tony Howre C.A.R.- Communicating Sequential Processis
        - Occam nyelv alapja
        - Actor alapú párhuzamosság
        - Ada és erlang processek
    - Hennessy - Theory  of processes
    - 1976 Dejkstra - Disciplin of programming
    - Lamport - Temporal logic of actions

## Étkező filozófusok

- Filozófusok körben ülnek, közös villák vannak és középről esznek
- Most egyszerre veszik fel mindkét villát, atomi-pillanatszerű művelet
- Négy állapot a filozófusnak
    - Gondolkodik
    - Van villa
    - Eszik
    - Otthon van
- Nem egy pillanatbeli logikai operátorok
    - Jövőidejű temporális logikai operátorok
- $ f(i).g \triangleright f(i).v \bigvee f(i).o $
    - Ha gondolkodik, akkor utána csak villás állapotban lehet vagy otthon lehet
    - Nem biztos, hogy valaha fog villát fogni
    - **unless**
- $ f(i).v \triangleright f(i).e $
    - Ha villa van nála, akkor enni fog
    - Nem biztos, hogy továbblép
    - Kiéheztetheti a többit
- $ f(i).e \mapsto f(i).g $
    - Ha eszik, utána mindenképp gondolokdni fog
    - **ensures**
- $ f(i).g \hookrightarrow f(i).o $
    -  odavezet, leadsto
    - Egyszer hazamegy 
