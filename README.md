A fejlesztők kétféle információval látják el a kódoló ügynököket, és egyik hatása sincs megbízhatóan felmérve.

Az első a repó kontextusfájlja: AGENTS.md vagy CLAUDE.md. Több tízezer projekt használ ilyet. Idén két tanulmány mérte a hatásukat. Abban egyetértenek, hogy a feladatok megoldási arányát nem javítják. A költségek terén viszont ellentmondanak egymásnak: az egyik alacsonyabb tokenfogyasztást és rövidebb futásidőt mért, a másik több mint 20 százalékkal magasabb költséget.

A második a fejlesztő saját hipotézise a hiba okáról. Egy issue ritkán korlátozódik a hibajelenség leírására, jellemzően tartalmazza a bejelentő feltételezését is a hiba helyéről. Ez a feltételezés néha téves. Más területeken végzett kutatásokból ismert, hogy a modellek hajlamosak elfogadni a felhasználó magabiztosan megfogalmazott állítását akkor is, ha az hamis. Ennek hatását kódjavítási feladatokon még nem vizsgálták.

A két tényezőt egy kísérletben vizsgálom, valódi GitHub issue-kon, amelyekhez valódi tesztek tartoznak.

| | Nincs tipp | Helyes tipp | Téves tipp |
|---|---|---|---|
| **Nincs kontextusfájl** | | | |
| **Generált fájl** | | | |
| **Kézzel írt fájl** | | | |

Kilenc feltétel, mindegyikben azonos feladatkészlet és azonos ügynök, ismételt futtatásokkal. Három mérőszám: lefut-e a tesztkészlet, mennyi token fogyott, illetve hozzányúlt-e az ügynök ahhoz a fájlhoz, amelyre tévesen irányítottam.

Az utolsó mérőszám egyszerű diff-ellenőrzéssel megállapítható, mérlegelés és szubjektív ítélet nélkül. Ha a megadott hibahely a cache.py, a hiba valójában máshol van, és az ügynök mégis módosítja a cache.py-t, ez egyértelműen kimutatható.

A vizsgálat fő kérdése a táblázat jobb alsó cellája: egy jól megírt kontextusfájl ellenállóbbá teszi-e az ügynököt a téves fejlesztői feltételezéssel szemben, vagy csak további követendő utasításokat ad hozzá.

Az eredmény két részből áll: magából a vizsgálatból, valamint egy újrahasznosítható mérőkeretrendszerből és feladatkészletből, amelyet publikálok. Ha a mért hatások kicsinek bizonyulnak, a keretrendszer önmagában is felhasználható marad, egy vitatott kérdésben megfelelő statisztikai erővel kimutatott null eredmény pedig szintén érvényes eredmény.
