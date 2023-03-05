# Számítógépes grafika

# 1. GY
- Vad Viktor András
- vva@inf.elte.hu

- Alapok
- Ablak és eseménykezelés
- OpenGl API
    - Grafikus pipeline

- Követelmények
    - Órán kell feladatot csinálni, pont jár érte
    - Házi feladat
    - Jó hozzászólás is leht pont
    - 2 beadandó - ha nincs az -15 pont
    - 4 órás ZH a félév végén
        - órai anyagból
        - mindent lehet használni
    - vagy nagy beadandó

## OpenGl

- GPU kezelő
- Grafikára használják
- Single instruction, multiple data achitecture
- Gép a gépben
    - Memória másolások
- IrisGL az alapja
- Ez egy szabvány
- 2008 Khronos Group vette át
- Eléggé öregszik
- Kázi objektum orientált
    - Fura logika

### Ablakozó rendszer és események

- OS-től ablak
- Üzenetek az appnak

### Double buffer

- Villódzik amikor éppen rajzol
- Kettős rendszer
    - Egyikben van a kirajzolt frame
    - Másikba meg éppen rajzol
- OS kicseréli a két képet
- Tearing - V-Sync
    - GPU és Monitor framerate szinkronizálása

### Simple DirectMedia Layer 2.0

- FOSS keretrendszer
- Elfedi és megkönnyíti az OS hívást
- Illeszkedik az OGL-hez

### GL Extension Wrapper (GLEW)

- Hiavtalos OpenGL inicializáció több száz sor lehet. Driver hívások és hibalehetőség.
- GLEW-el egy függvény

### OpenGL Mathematics (GLM)

- Matematika könyvtár az OGL-hez

### Házi

- ALT+Enter ful size
- MouseMoove szín váltás
- Csak bizonyos gomb lenyomásakor legyen
