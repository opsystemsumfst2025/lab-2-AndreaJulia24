# Labor 2. — Fajlrendszerek es Jogosultsagok megoldasa

## 0.Kornyezet bemelegites: 

**ls -l kimenet megfigyelése:**
A `setup_lab.sh` futtatása után a kritikus fájlok és könyvtárak jogosultságai a következők voltak:
- locked_room: `d----------` (oktális: **000**). Sem a User, sem a Group, sem az Others nem fér hozzá. Ez megerősítette a kiinduló, "elrontott" biztonsági állapotot.

**cat /proc/cpuinfo | head -5 magyarázata:**
Ez a fájl nem a lemezen tárolódik, hanem a kernel generálja futásidőben, demonstrálva a Linux "minden fájl" koncepcióját.

## 5.Gondolkodasi kerdesek:
# 1.Miért van szükség egy könyvtárnak futtatási bitre, mielőtt cd-zhetnél bele?
- A konyvtarakon levo futtatasi ('x') bit , a bejarasi (traverse) jogosultsagot jelenti.Ez teszi lehetove,hogy a 
kernel engedelyezze a usernek a belepest a konyvtarba ('cd') es hozzaferjen a benne levo fajlokhoz. Olvasasi ('r') 
jog nelkuli ('ls' nem mukodik), de a futtatasi joggal megis elerhetoek a fajlok,ha ismerjuk a nevuket.

# 2.Milyen kockázatot jelentene a chmod 777 evidence/script.sh parancs?
- A '777' (rwxrwxrwx) teljes olvasasi, irasi, es futtatasi jogot mindenki szamara a rendszeren(User,Group,Others).
- A legnagyobb kockazat az,hogy barki a rendszeren(pl. egy rosszindulatu felhasznalo) megvaltoztatja (irhatja) a szkript tartalmat,
rosszindulatu kodot illeszthet bele, majd futtathatja azt, komoly biztonsagi rest okozva.

# 3.Hogyan dönti el a fix_system.sh, hogy melyik fájl kapjon 644 és melyik 700 jogosultságot?
- A szkript a fajl kiterjesztese alapjan hoz dontest, a 'find' parancsban hasznalt '-name' opcioval.
- A 'find' ...-name '*.txt' parancs kivalasztja az osszes .txt vegzodesi fajlt, es a '644' jogosultsagot(olvasas mindenki szamara,
iras csak a user szamara) rendeli hozza.
- A 'find' ...-name '*.sh' parancs kivalasztja az osszes .sh vegzodesu fajlt, es a '700' jogosultsagot(teljes hozzaferes CSAK 
a user szamara) rendeli hozza.
