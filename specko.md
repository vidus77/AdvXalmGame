# A Memória-kártyajáték specifikációja


## Szerző helyesebben interpretáló
Vida Zoltán ( [Plesz Gábor, NetAcademia, 2018 tananyaga](https://github.com/Xaml201805) alapján)


## A programozáshoz felhasznált környeze
### Visual Studio 2015
 - Community csomag
 - GitHub környezet
 - Markdown [Extension](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.MarkdownEditor) felhasználásával 
   - Javasolt *.md formátum UTF8 


## A specifikáció feladata

 - bár a játék teljes mértékben a fent emített tanfolyami anyagra épül, a kiviteklezás különbözni fog egy kicsit, más tervezéssel egy-két apró változtatással másik játékot csinálni belőle. 
 - A markánsan különböző funkciókat részletesebben is specifikálandók. 
 - A fejlesztés Deklaratív és procedulális programozásra épül.

## Általános bemutatás
Szeretnénk készíteni egy reakcióidő mérő játékot. A játék egymás után mutat kártyalapokat, és nekünk meg kell mondanunk, hogy a mutatott lap egyezik-e az előzővel, vagy sem. Ha jól válaszolunk pontot kapunk. A játék méri az egyes reakcióidőt, és az átlagos reakcióidőt is. A végén a top 5 eredményt is megmutatja.

## Forgatókönyv
 A _Felhasználó_ elindítja a játékot és és néhány játékot játszik, ezáltal képet nyer az aktuális reakció idejéről, koncentrációképességéről.

## A Játékmenet
- Kezdéskor kapunk egy kártyát, 
- Az, hogy jó-e a káártya lóre el kell döljön, nem a lapok számától füg
  - (1.) A kártyának vagy jónak vagy nem jónak kell lennie nagyjából 50% eséllyel
- majd a játék indításával a kártyánkat egy új váltja fel. A játék indítása, az Indítás gombbal megy.
- A visszajelzésünkre (egyforma/nem egyforma) 
- a játék jelzi egy zöld pipával/piros kereszttel, hogy a válaszunk helyes vagy helytelen.
- a játékot billentyűzettel lehessen játszani
- A válasznak megfelelő pontot számolja, 
- méri az egyes reakcióidőt 
- és az átlagos reakcióidőt is. 
- A játék meghatározott ideig tart, amit a kezdéstől egy visszaszámláló óra jelez. 
- A játék végén látjuk a pontszámunkat, 
- és a top 5 pontszámot. 
- Ha akarjuk újrakezdhetjük a játékot, vagy kiléphetünk.
- 
## A markánsan különböző funkciók
 1. Tekintettel arra, hogy játék közben két gombot használunk, azok lenyomásának esélyeit ki kell egyenlítenünk.  
 2. Az eredeti programtól eltérő lesz a gombok elhelyezkedése
 3. Jó lenne visszaszámlálással indítani a játékot az első lap megjelenéséig. 

## A játék főképernyőjének eredeti verziója

```
+---------------------------------------------------------------------------------------------------+
| +----------+  +---------------------------------------------------------------------------------+ |
| |          |  | Információk, eredmény, visszajelzés                                             | |
| | Toplista |  +---------------------------------------------------------------------------------+ |
| |          |                                                                                      |
| |          |                                                                                      |
| |          |         +---------------------------+         +---------------------------+          |
| |          |         |                           |         |                           |          |
| |          |         |  Visszajelzés, hogy a     |         |                           |          |
| |          |         |  válasz jó volt+e         |         |   Kártya a játékhoz       |          |
| |          |         |  vagy sem                 |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         |                           |         |                           |          |
| |          |         +---------------------------+         +---------------------------+          |
| |          |                                                                                      |
| |          |  +---------------------------------------------------------------------------------+ |
| |          |  | Különböző gombok, amik egymás mellett szépen következnek                        | |
| |          |  |                                                                                 | |
| +----------+  +---------------------------------------------------------------------------------+ |
+---------------------------------------------------------------------------------------------------+
```
# A játék főképernyőjének módosított verziója

```
+---------------------------------------------------------------------------------------------------+
|   +-----------+  +---------------------------------------------------------------------------+    |
|   |           |  |                  Információk, eredmény, ^isszajelzés                      |    |
|   |  Toplista |  +---------------------------------------------------------------------------+    |
|   |           |                                                                                   |
|   |           |                                                                                   |
|   |           |  +--------------------+   +---------------------------+   +------------------+    |
|   |           |  |                    |   |                           |   |                  |    |
|   |           |  | Visszajelzés, hogy |   |    Kártya a játékhoz      |   |  Diagrammok      |    |
|   |           |  | ^álasz jó ^olt+e   |   |                           |   |                  |    |
|   |           |  | vagy sem           |   |                           |   |                  |    |
|   |           |  |                    |   |                           |   |                  |    |
|   |           |  |                    |   |                           |   |                  |    |
|   |           |  |                    |   |                           |   |                  |    |
|   |           |  |                    |   |                           |   |                  |    |
|   |           |  |                    |   |                           |   |                  |    |
|   |           |  |                    |   |                           |   |                  |    |
|   |           |  |                    |   |                           |   |                  |    |
|   |           |  |                    |   |                           |   |                  |    |
|   |           |  |                    |   |                           |   |                  |    |
|   +-----------+  +--------------------+   +---------------------------+   +------------------+    |
|                                                                                                   |
|   +------------------------------------------------------------------------------------------+    |
|   |    Különböző gombok, amik egymás mellett szépen következnek                              |    |
|   |                                                                                          |    |
|   +------------------------------------------------------------------------------------------+    |
|                                                                                                   |
+---------------------------------------------------------------------------------------------------+
```

 - A képernyőn lesz két fő sor, az alsóban a kezelő gombok, a fölső sorban minden más
  - a felső rész baloldalán lesz egy tartalomfüggő szélességű (nem nyújyható ) és egy változtatható szálességű oszlop minden a fejlécnek és a grafikus elemeknek
  - Az alsó sor gombjai WrapPanelben középen lesznek 
  - - A gombok feliratai es nyilai is lesznek. 
    - A rossz valasz nyila jobboldalon lesz a felirathoz képest
