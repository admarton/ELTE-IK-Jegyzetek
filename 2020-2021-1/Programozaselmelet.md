# Programozáselmélet Definíciók  (M-x set-input-method Tex)

## Relációk:
Def.: Legyenek A és B tetszőlegese nemüres halmazok. Ekkor az A×B halmaz az A és B Descartes szorzata, és  
      A×B := {(a,b) | a ∈ A ∧ b ∈ B }

Def.: Legyenek A és B tetszőleges nemüres halmazok. Ekkor az A×B halmaz minden R részhalmazát (az üres halmazt is) relációnak nevezzük.  

Def.: Legyenek A és B tetszőleges nemüres halmazok és R ⊆ A×B tetszőleges reléció. Azt mondjuk, hogy az R reláció determinisztikus, ha  
      ∀a ∈ A : |R(a)| ≤ 1
A determinisztikus relációkat másképpen függvénynek hívjuk. Jel.: R ∈ A→B.  
Ha ∀a∈ A : |R(a)| = 1 akkor R : A→B.

### Állapottér:
```
Def.: Legyenek A₁,...,Aₙ (ahol n ∈ ℕ⁺) típusérték-halmazok és v₁,...,vₙ a halmazokat azonosító egyedi címkék (változók).  
Az ezekből képzett, címkézett értékeknek egy {v₁:a₁,...,vₙ:aₙ} halmazát (ahol ∀i ∈ [1..n] : aᵢ ∈ Aᵢ) állapotnak nevezünk.  

Def.: Legyenek A₁,...,Aₙ (ahol n ∈ ℕ⁺) típusérték-halmazok és v₁,...,vₙ a halmazokat azonosító egyedi címkék (változók).  
Az ezekből képzett összes lehetséges {v₁:a₁,...,vₙ:aₙ} állapot (ahol ∀i ∈ [1..n] : aᵢ ∈ Aᵢ) halmazát állapottérnek nevezzük és (v₁:A₁,...,vₙ:Aₙ)-nel jelöljük.  
      (v₁:A₁,...,vₙ:Aₙ) := { {v₁:a₁,...,vₙ:aₙ} | ∀i ∈ [1..n] : aᵢ ∈ Aᵢ }  

Def.: Az A = (v₁:A₁,...,vₙ:Aₙ) állapottér címkéire (változók) úgy tekintünk mint vᵢ : A → Aᵢ függvényekre, ahol vᵢ(a) = aᵢ egy a={v₁:a₁,...,vₙ:aₙ} állapot esetén.  
```
## Feladat:
Def.: Feladatnak nevezünk egy F ⊆ A×A relációt.  

## Program:
```
Def.: Legyen A az úgynevezett alap-állapottér (fail ∉ A).  
Jelölje Ā azon véges komponensű állapottererek unióját, melyeknek altere az A alap-állapottér: Ā = ⋃_(A≤B) B.  
Az A feletti programnak hívjuk az S ⊆ A × (Ā ∪ {fail})** relációt, ha  
   1. Dₛ=A
   2. ∀a ∈ A: ∀α ∈ S(a) : |α| ≥ 1 és α₁ = a
   3. ∀α ∈ Rₛ : (∀i ∈ ℕ⁺ : i < |α| → αᵢ ≠ fail)
   4. ∀α ∈ Rₛ : (|α| < ∞ → α_|α| ∈ A ∪ {fail})

Új változó: A=(x:ℤ, y:ℤ)  
   	    {{x:8,y:3},<{x:8,y:3},{x:8,y:3,z:8},{x:3,y:3,z:8},{x:3,y:8}>}  
				    ᴸ>∉A		ᴸ>∉A
```
## Megoldás:
Def.: Az S program megoldja az F feladatot, ha  
      1. D_F ⊆ Dₚ₍ₛ₎
      2. ∀ a ∈ D_F : p(S)(a)⊆F(a)

## Programfüggvény
Def.: A p(S) ⊆ A×A reláció az S ⊆ A×(Ā ∪ {fail})** program programfüggvénye, ha  
      1. Dₚ₍ₛ₎ = {a ∈ A | S(a) ⊆ Ā*}
      2. ∀a ∈ Dₚ₍ₛ₎ : p(S)(a) = {b ∈ A | ∃α ∈ S(a) : b = α_|α|}
      
Def.: A p~(S) ⊆ A×(A ∪ {fail}) reláció az S ⊆ A×(Ā ∪ {fail})** program gyenge programfüggvénye, ha  
      1. Dₚ~₍ₛ₎ = {a ∈ A | S(a) ∩ (Ā ∪ {fail})* ≠ ∅}
      2. ∀a ∈ Dₚ~₍ₛ₎ : p~(S)(a) = {b ∈ A ∪ {fail} | ∃α ∈ S(a) ∩ (Ā ∪ {fail})* : b = α_|α|}

## Elemi programok
Def.: A tetszőleges állapttér, ∀a ∈ A: S(a) ⊆ {<a>,<a,fail>,<a,a,...>,<a,b>|b ∈ A}, akkor S elemi program.  
Def.: ∀a ∈ A : ABORT(a) = {<a,fail>}  
Def.: ∀a ∈ A : SKIP(a) = {<a>}  

ABORT és SKIP program is determinisztikus  

Def.: A tetszőleges állapottér, F ∈ A × A, S általános értékadás, ha ∀a ∈ A : S(a) = ...  
      = {<a,b>|b ∈ F(a)} ,ha a ∈ D_F és  
      = {<a,fail>} ,ha b ∉ D_F.  
Def.: A = (x,y), S szimultán étékadás, ha ∀a ∈ A : S(a)={<a,b>|b ∈ A ∧ x(b)=y(a) ∧ y(b)=x(a)}  

## Logikai függvény
Def.: Ha R ∈ A → 𝕃 ,akkor R egy logikai függvény.  
Def.: ⌈R⌉ = { a ∈ A | R(a)={igaz}} az R logiakai függvény igazsághalmaza.  
Def.: Ha Q : A → 𝕃 ,akkor Q olyan logikai függvény amiben ∀a ∈ A : |Q(a)|=1 (minden elemhez rendel valamit)  
Def.: IGAZ: A→𝕃, ∀a ∈ A : IGAZ(a) = {igaz}, ⌈IGAZ⌉=A  
Def.: HAMIS: A→𝕃, ∀a ∈ A : HAMIS(a) = {hamis}, ⌈HAMIS⌉=∅  
Def.: Tetszőleges Q,R ∈ A→𝕃, Q maga után volja R (Q ⇒ R), ha ⌈Q⌉⊆⌈R⌉.  

## Leggyengébb előfeltétel
Def.: Legyen R ∈ A→𝕃 és S program A felett. Ekkor az S program R utófeltételhez tartozó leggyengébb előfeltétele az az lf(S,R) : A→𝕃 függvény, amelyre:  
      ⌈lf(S,R)⌉ = {a ∈ A | a ∈ Dₚ₍ₛ₎ ∧ p(S)(a) ⊆ ⌈R⌉}.  
      
Tét.: Az lf tulajdonságai  
      Legyen S program, Q,R logikai függvény A felett. Ekkor  
      	     1.if(S,HAMIS)=HAMIS  
	     2.ha Q ⇒ R akkor lf(S,Q) ⇒ lf(S,R)  
	     3.lf(S,Q) ∧ lf(S,R) = lf(S,Q∧R)  
	     4.lf(S,Q) ∨ lf(S,R) ⇒ lf(S,Q∨R)  

## Feladat szigorítása
Def.: Az F₁ feladat szigorúbb mint F₂ feladat, ha  
      1. D_F₂ ⊆ D_F₁	      	   (ahol eddig nem volt elvárás, most lesz)  
      2. ∀a ∈ D_F₂ : F₁(a) ⊆ F₂(a)  
Tét.: Ha S program megoldja az F₁ feladatot, akkor megoldja F₂ feladatot is (ahol F₁ szigorúbb mint F₂).  

## Paramétertér
Def.: Legyen F ⊆ A×A feladat. B halmazt a feladat paraméterterének nevezzük, ha van olyan F₁ és F₂ reláció, hogy  
      F₁ ⊆ A×B  
      F₂ ⊆ B×A  
      F = F₂ ∘ F₁.  
Áll.: Legyen F ⊆ A×A feladatnak van paramétertere.  
Áll.: Legyen F ⊆ A×A feladatnak végtelen sok paramétertere van.  

## Specifikáció
Tét.: Legyen F ⊆ A×A feladat, B az F egy paramétertere, F₁ ⊆ A×B, F₂ ⊆ B×A, F = F₂ ∘ F₁.  
Legyen b ∈ B, és definiáljuk a következő állításokat:  
		⌈Q_b⌉ = { a ∈ A | (a,b) ∈ F₁} = F₁⁽⁻¹⁾(b)  
		⌈R_b⌉ = { a ∈ A | (b,a) ∈ F₂} = F₂(b)  
	Ekkor ha ∀b ∈ B : Q_b ⇒ lf(S,R_b),  akkor az S program megoldja az F feladatot.  

## Programkonstrukciók
```
• Szekvencia  
Def.: Legyen A közös alap-állapottere az S₁ és S₂ programoknak.  
Az (S₁; S₂) relációt az S₁ és S₂ programok szekvenciájának nevezzük, ha  
	(S₁; S₂)(a) =	{α ∈ Ā∞ 	| α ∈ S₁(a)} ∪  
	   	{α ∈ (Ā ∪ {fail})∗	| α ∈ S₁(a) ∧ α_|α| = fail} ∪  
		{γ ∈ (Ā ∪ {fail})∗∗	| γ = α ⊗ β ∧ α ∈ S₁(a) ∧ |α| < ∞ ∧ α_|α| ≠ fail ∧ β ∈ S₂(α_|α|)}  
 ┌───┐
 │ S │
 └─┬─┘
┌──┴──┐
│ S₁  │
├─────┤
│ S₂  │
└─────┘
									 
• Elágazás  
Def.: Legyen A közös alap-állapottere az S₁, . . . Sₙ programoknak. Legyenek továbbá π₁, . . . πₙ ∈ A → 𝕃 logikai függvények.  
Ekkor az IF ⊆ A×(Ā ∪ {fail})** relációt az Sᵢ programokból képzett πᵢ feltételek által meghatározott elágazásnak nevezzük és (π₁ : S₁, ... , πₙ : Sₙ)-nel jelöljük, ha  
      	 ∀a ∈ A : IF(a) = ω₀(a) ∪ ⋃ⁿᵢ₌₁ ωᵢ(a)  
ahol ∀i ∈ [i...n] :
	        ┌	Sᵢ(a),		ha a ∈ D_πᵢ ∧ πᵢ(a)
	ωᵢ(a) = ┤	Ø,		ha a ∈ D_πᵢ ∧ ¬πᵢ(a)
	        └	{<a, fail>},	ha a ∉ D_πᵢ
és
	        ┌	{<a, fail>},	ha ∀i ∈ [1...n] : (a ∈ D_πᵢ ∧ ¬πᵢ(a))
	ω₀(a) = ┤
	        └	Ø,		különben
    ┌────┐
    │ IF │
    └──┬─┘
┌────┬─┴─┬────┐
│\π₁ │...│\πₙ │
├────┼───┼────┤
│ S₁ │...│ Sₙ │
└────┴───┴────┘

• Ciklus
Def.: Legyen π ∈ A → L feltétel és S₀ ⊆ A × (Ā ∪ {fail})** program.
A DO ⊆ A × (Ā ∪{fail})** relációt az S₀ programból π feltétellel képzett ciklusnak nevezzük és (π, S₀)-lal jelöljük, ha ∀a ∈ A:
	        ┌	(S₀; DO)(a),	ha a ∈ D_π ∧ π(a)
	DO(a) = ┤	{<a>},		ha a ∈ D_π ∧ ¬π(a)
	        └	{<a, fail>},	ha a ∉ D_π
  ┌────┐
  │ DO │
  └─┬──┘
┌───┴────┐
│    π   │
│ ┌──────┤
│ │  S₀  │
└─┴──────┘
```

## Levezetési szabályok

• Szekvencia levezetési szabálya  
Tét.: Legyen S = (S₁; S₂) az A közös alap-állapotterű Sᵢ programokból képzett szekvencia. Legyenek Q, R, Q' logikai függvények A-n.  
Ha  
	1.  Q  ⇒ lf(S₁, Q')	//(Q elvisz Q'-be)  
	2.  Q' ⇒ lf(S₂, R)	//(Q' elvisz R-be)  
akkor  Q ⇒ lf(S, R)  

• Elágazás levezetési szabálya  
Tét.: Legyen  IF = (π₁ : S₁, ... , πₙ : Sₙ) a közös A alap-állapotterű Sᵢ programokból képzett, A feletti πᵢ logikai függvényekkel meghatározott elágazás.  
Legyenek továbbá Q és R logikai függvények A-n.  
Ha  
	1.  Q ⇒ ⋁ⁿᵢ₌₁ πᵢ				//(Legalább az egyik feltétel teljesül, kiértékelhető)  
	2.  Q ⇒ ⋀ⁿᵢ₌₁ (πᵢ ∨ ¬πᵢ)			//(Mindegyik feltétel kiértékelhető)  
	3.  ∀i ∈ [1..n] :  Q ∧ πᵢ ⇒ lf( Sᵢ, R)		//(Ha a πᵢ feltétel teljesül, akkor Sᵢ olyan állapotban áll meg amire R igaz)  
akkor Q ⇒ lf( IF, R )  
	
• Ciklus levezetési szabálya  
Tét.: Legyen DO = (π, S₀) az A alap-állapottér feletti S₀ programból és a π ∈ A → 𝕃 feltétellel képzett ciklus.  
Továbbá legyenek P, Q és R logikai függvények A-n és t: A → ℤ függvény adottak.  
Ha  
	1. Q ⇒ P			//(Ciklus elején igaz a ciklus-invariáns)  
	2. P ∧ ¬π ⇒ R			//(Ha a ciklus befejeződik akkor R-be jutunk)  
	3. P ⇒ π ∨ ¬π			//(Ha az invariáns teljesül akkor a feltétel kiértékelhető)  
	4. P ∧ π ⇒ t > 0		//(Ha a feltétel igaz, akkor a termináló függvény nagyobb mint 0)  
	5. P ∧ π ⇒ lf(S₀, P)  
	6. P ∧ π ∧ t = t₀ ⇒ lf(S₀, t < t₀)  / ∀t₀ ∈ ℤ  
akkor Q ⇒ lf(DO, R)  

//(5-6. P ∧ π ∧ t = t₀ ⇒ lf(S₀, P ∧ t < t₀ ) ⇔ (Ha igaz az invariáns és a ciklusfeltétel és t egy egész, akkor S₀-t végrahajtva az S₀ helyesen terminál ott ahol P igaz és t értéke csökken)  
      	      	      	     	         //(S₀-t végrehajtva az invariáns megmarad és a termináló függvény értéke csökken)  
//(Nem lehet végtelen mert ṯ csökken és nagyobb kell legyen mint 0 ha a feltétel igaz)  
//(S₀ is megold egy feladatot: az [P ∧ π ∧ t=t₀] előfeltételü és [P ∧ t<t₀] utófeltételű feladatot)  

## Új programkonstrukciók
```
• Atomi utasítás: [S]
Def.: Legyen A tetsz ̋oleges állapottér, S program az A állapottér felett.
	∀a ∈ A: [S](a) = S(a)
      
//Megszakítás nélkül hajtjuk végre. S nem tartalmazhat ciklust vagy várakoztató utasítást.

• Várakoztató utasítás: await B then S ta
Def.: Legyen A közös állapottere az S programnak és a β logikai függvénynek ( őrfeltételnek).
				┌[S](a)				,ha a ∈ D_β ∧ β(a)
∀a ∈ A: (await β then S ta)(a)=	┤ (SKIP; await β then S ta)(a)	,ha a ∈ D_β ∧ ¬β(a)
				└{<a, fail>}			,ha a ∉ D_β

//Amennyiben a β  őrfeltétel igaz, az S program atomi utasításként a β kiértékelésével egyszerre hajtódik végre. S nem tartalmazhat ciklust vagy várakoztató utasítást.
//Ha β kiértékelhető de hamis, az utasítást tartalmazó folyamat blokkolttá válik.
//A végrehajtás nem tud továbblépni a várakoztató utasításon, amíg egy másik folyamat nem „segít” és változtatja meg az állapotot úgy hogy β teljesüljön.

• Párhuzamos blokk: parbegin S₁||...||Sₙ parend
Def.: Legyen A közös alap-állapottere az S₁...Sₙ programoknak.
	∀a ∈ A: ( parbegin S₁||...||Sᵢ||...||Sₙ parend )(a) = ⋃ⁿᵢ₌₁Bᵢ(a)
 ahol
	┌(Sᵢ;  parbegin S₁||...||Sᵢ₋₁||Sᵢ₊₁||...||Sₙ parend )(a)		,ha Sᵢ nem megszakítható az a állapottérből indulva
Bᵢ(a)=	┤
	└(uᵢ;  parbegin S₁||...||Sᵢ₋₁||Tᵢ||Sᵢ₊₁||...||Sₙ parend )(a)	,ha Sᵢ(a)=(uᵢ;Tᵢ)(a) ahol uᵢ nem megszakítható az a állapotból indulva

//Befejeződik, ha minden komponensprogramja terminál.
//Végrehajtása valamely ágnak kiválasztását és az ott lévő komponens első utasításának, illetve a kapott maradék programnak egymás utáni végrehajtását jelenti.
```
## Új programkonstrukciók levezetési szabályai
```
• Atomi művelet levezetési szabálya
Tét.: Legyen S A feletti program.
Ha
	Q ⇒ lf(S,R)
akkor Q ⇒ lf([S],R)

• Várakozó utasítás levezetési szabálya
Tét.: Legyen A közös állapottere az S programnak és a β logikai függvénynek ( őrfeltételnek).
Ha
	1. Q ⇒ β ∨ ¬β		//őrfeltétel kiértékelhető
	2. Q ∧ β ⇒ lf(S,R)	//ha az őrfeltétel teljesül akkor a program helyesen fejeződik be
akkor Q ⇒ lf(await β then S ta,R)

• Párhuzamos blokk levezetési szabálya
Tét.: Legyen T: parbegin S₁|| ... ||Sₙ parend
Ha
	1. Q ⇒ Q₁ ∧ Q₂ ∧ ... ∧ Qₙ	//"belépés"
	2. R₁ ∧ R₂ ∧ ... ∧ Rₙ ⇒ R	//"kilépés"
	3. ∀i ∈ [1 .. n]: Qᵢ ⇒ lf(Sᵢ, Rᵢ)	//mindegyik komponens helyes
	4. Interferencia mentesség teljesül
	5. Holtpontmentes a T
akkor Q ⇒ lf(T, R)
```
## Interferencia mentesség:
	Külön külön helyes programok egymás mellett elromolhatnak, pl ugyan azt az értéket változtatják  
	pre(Sⱼ) ⇒ lf (Sⱼ, post(Sⱼ))  
	Csak kritikus utasítésokat kell megnézni  

## Kritikus utasítás
	∘ értékadás  
	∘ atomi program amiben van értékadás  

Def.: u kritikus utasítás nem interferál az Sⱼ program teljes helyességi formulájával  
Ha  
	1. preᵤ ∧ post(Sⱼ) ⇒ lf( u, post(Sⱼ))  
	2. preᵤ ∧ preₛ ⇒ lf( u, preₛ)	//s az Sⱼ összes utasítása  
	3. preᵤ ∧ Inv ∧ t=t₀ ⇒ lf( u, t ≤ t₀) ∀t₀ ∈ ℤ //Inv = ciklus INVariáns  

Def.: Sᵢ komponens nem interferál az Sⱼ (i ≠ j) teljes helyességi formulájával, ha Sᵢ bármely kritikus utasítása new interferál az Sⱼ teljes helyességi furmulájával.  

## Holtpont
S-ben csak egy párhuzamos blokk van, és abban csak két részprogram van.  
S holtpontban van D(S) = [D(S₁) ∧ post(S₂)] ∨ [D(S₂) ∧ post(S₁)] ∨ [D(S₁) ∧ D(S₂)]  

### Általánosan
S-ben m db "await" : A₁...Aₘ és n db "par" : T₁...Tₙ  
D(S) = [⋁ᵐⱼ₌₁ (pre(Aⱼ ) ∧ ¬Bⱼ )] ∨ [⋁ⁿₖ₌₁ D1(Tₖ)]  

T-ben n db program : S₁...Sₙ  
D1(T) = [⋀ⁿᵢ₌₁ (post(Sᵢ) ∨ D(Sᵢ))] ∧ [⋁ⁿᵢ₌₁ D(Sᵢ)]  
