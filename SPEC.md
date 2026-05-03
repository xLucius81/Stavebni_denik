# SPEC – Stavební deník (webová aplikace)

## Správce systému
- **Jméno:** Petr Říha, přezdívka Lucius
- **Email:** petr@lbcomputers.cz
- **Obor:** Elektroinstalace, Havířov
- **Role:** Správce s neomezenými právy

---

## Technologický stack (rozhodnut)
| Vrstva | Technologie |
|--------|-------------|
| Backend | Node.js + Express |
| Databáze | PostgreSQL na Railway |
| Frontend | HTML / CSS / JS |
| Soubory | Cloudinary |
| Emaily | Resend nebo SendGrid (z petr@lbcomputers.cz) |
| AI vrstva | Claude API (claude-sonnet-4-20250514) |
| Hosting | Railway (přes GitHub) |
| Fáze 1 | Single-tenant pro Petra |
| Fáze 2 | Multi-tenant (odloženo) |

---

## Aktuální stav prototypu

### Soubory
- `stavebni_denik_beta_v1.html` – původní prototyp (78 KB)
- `stavebni_denik_beta_v2.html` – **aktuální verze** (132 KB) ← pracovat s tímto

### Co je hotovo v beta_v2

#### Část 1 – Základní struktura
- [x] Topbar s názvem aplikace, tmavý/světlý režim, tlačítko Nový deník, avatar
- [x] Sidebar s navigací (Hlavní panel, Aktivní/Ukončené zakázky, Denní záznamy, Přehledy, Uživatelé, Nastavení, Profil)
- [x] Responsivní design – hamburger menu na mobilu
- [x] Toast notifikace

#### Část 1 – Hlavní panel
- [x] 4 stat dlaždice: Aktivní zakázky, Ukončené zakázky, Záznamy tento měsíc, Záznamy celkem
- [x] Pořadí dlaždic nastavitelné v Nastavení (drag & drop) – **ukládá se do pořadí na panelu**
- [x] Avízo o čekajících registracích (banner)
- [x] Karty aktivních zakázek s realizačním týmem, milníky etap, progress barem
- [x] Tabulka ukončených zakázek
- [x] Poslední záznamy

#### Část 1 – Zakázky / Nový deník
- [x] Číslo zakázky, typ (Silnoproud/Slaboproud)
- [x] Dodávky Silnoproud: Běžný materiál, Kabely a vodiče, Kabelové trasy, Koncové prvky, Rozvaděče, Svítidla + přidat vlastní
- [x] Systémy Slaboproud: ACS, AP, CCTV, EPS, EZS, DT, PZTS, SK, STA + přidat vlastní
- [x] Datum zahájení, předpokládané ukončení
- [x] **GPS na úrovni zakázky** (adresa + souřadnice) – pro počasí
- [x] **Realizační tým** na formuláři i na kartě zakázky: Projektový manažer, Přípravář, Stavbyvedoucí, Rozpočtář, Vedoucí technik
- [x] Milníky etap (předdefinované + vlastní, výběr checkboxy)

#### Část 1 – Uživatelé
- [x] Čekající registrace s tlačítky Schválit/Zamítnout
- [x] Modal schválení: výběr deníků, platnost od/do, role
- [x] Aktivní uživatelé + vypršelé účty
- [x] Role: Správce, Elektrikář, Investor
- [x] **Log přihlášení s exportem** – filtr uživatel + období → Excel

#### Část 1 – Nastavení
- [x] Název aplikace (živě v topbaru)
- [x] Zobrazovat jméno/přezdívku/oboje
- [x] Tmavý/světlý režim toggle
- [x] **Drag & drop pořadí dlaždic** (ukládá se)
- [x] Logo společnosti (nahrát/změnit/odstranit) – pro exporty + přihlašovací stránku
- [x] Nastavení exportů: název firmy, IČO, GPS záloha
- [x] Správa pracovníků (číselník): PR, KD, TN, JB + přidat nového

#### Část 1 – Profil správce
- [x] Foto (nahrát/změnit/odstranit) – promítne se do topbaru, sidebaru, uživatelů
- [x] Jméno, přezdívka, email, telefon, adresa, heslo
- [x] Role pill "Správce systému"

#### Část 2 – Denní záznamy ✅ HOTOVO
- [x] Výběr zakázky (zobrazeno: D9.10)
- [x] **Týdenní pás / kalendář** – navigace šipkami, zelená tečka = má záznam, 🔒 = uzamčeno
- [x] **Počasí** – OpenMeteo API, GPS zakázky (50.8503, 14.8687), časy 6:00/12:00/18:00
- [x] **Zamykání dnů** – pouze správce, po zamčení nelze editovat, tlačítko v topbaru
- [x] **AI asistent** – textarea pro WhatsApp text elektrikáře, volání Claude API, rozlišení standard/vícepráce
- [x] **Sekce Osoby na staveništi** – výběr z číselníku, příchod/odchod/přestávka → výpočet hodin
- [x] **Kopírování osob** – výběr dne, checkboxy pro jednotlivé osoby + **"Vybrat vše"**, počítadlo vybraných
- [x] **Sekce Materiál** – název, množství, MJ, dodavatel, č. DL, datum DL
- [x] **Sekce Mechanizmy** – dodavatel, název, příjezd/odjezd → výpočet doby
- [x] **Sekce Provedené práce** – typ (Standard/Vícepráce), popis, objekt, podlaží, místnost, příloha
- [x] Vícepráce: spotřebovaný materiál, status (Čeká/Schváleno/Fakturováno), kliknutím cykluje
- [x] **Sekce Další záznamy** – typ konzultace (multi-select: Architekt, Dodavatel mat., Dodavatel rozvaděčů, Dodavatel svítidel, Investor, Koordinátor BOZP, Projektant, Revizní technik, Stavbyvedoucí, TDI, TIČR) + volný text
- [x] **Sekce Fotodokumentace** – nahrání fotek, zobrazení thumbnailů

### Část 3 – Přehledy (PENDING)
- [x] Souhrn víceprací za celý projekt – popis, datum, pracovník, status; filtr dle statusu
- [x] Souhrn odpracovaných hodin – výběr pracovníků + období (od/do nebo měsíc)
- [x] **Export víceprací** → Excel + PDF s hlavičkou (název, číslo, adresa zakázky + logo firmy)
- [x] **Export hodin** → Excel + PDF s hlavičkou
- [x] Fotodokumentace v přehledech

---

## Co zbývá udělat
- [ ] Část 4


### Přihlašovací stránka (PENDING)
- [ ] Logo + název aplikace
- [ ] Formulář přihlášení + odkaz na registraci
- [ ] Patička: ochranná známka, verze, autor

### Budoucí rozšíření (odloženo)
- [ ] Rozpočet a fakturace
- [ ] Multi-tenant systém

---

## Databázový model (navržen, odsouhlasen)
Tabulky: `users`, `user_access`, `login_log`, `zakazky`, `milniky`, `denik_dny`, `osoby`, `material`, `mechanizmy`, `prace`, `viceprace_material`, `dalsi_zaznamy`, `pocasi`, `fotodokumentace`, `nastaveni`

---

## Číselník profesí pracovníků
Vedoucí technik, Technik, Pomocný technik, Elektrikář silnoproud, Elektrikář slaboproud, Revizní technik, Koordinátor BOZP, Dodavatel rozvaděčů, Dodavatel svítidel

---

## Design systém
- **Styl:** navy sidebar (#162438), bílé karty, teal akcenty (#0d9485)
- **Font:** Inter
- **Tmavý režim:** plně funkční přes CSS proměnné
- **Responsivní:** hamburger < 680px, 2 sloupce statistik na tabletu

---

## Technické poznámky pro Claude

### Jak psát velké soubory (>100 KB)
**VŽDY** používat `create_file` tool – nikdy bash heredoc (limit 100 KB).
Na konci vždy `cp` do `/mnt/user-data/outputs/` a `present_files`.

### Při zahájení nového chatu
1. Přečíst tento SPEC.md
2. Ověřit `ls /home/claude/` – soubory se mezi chaty **NEUCHOVÁVAJÍ**
3. Pracovat vždy od nejnovější verze – aktuálně `beta_v2`
4. Při velkých změnách vždy inkrementovat verzi (beta_v3, beta_v4…)

### Otevřené otázky / poznámky k ladění
1. Duplikuje se několik zobrazení: "Přehledy v přehledech" a pak stejný přehled po rozkliknutí "Zakázky". To je špatně. Vytvoř přehled všech všech zakázek, jak aktivních (realizace), uzamčených, v přípravě. U těchto zakázek bude zobrazeno.
2. Slovo "Aktivní" u zakázek nahradit "Realice" a zkratka bude "R". Budeme rozlišovat zakázky: Příprava ("P", pokud zákazku do aplikace přidám, ale nebudou tam prozatím probíhat žádné práce), "Realizace", "Uzavřeno"
2. Přehled na zvolené zakázce bude dostupný pouze po rozkliknutí zakázky a bude se týkat pouze dané zakázky.
3. V přehledu z menu v levé části se budou zobrazovat všechny zakázky. Prvky, které zde budou musíme vybrat.
3. Seznam pracovníků oddělit. Seznam pracovníků bude jiný na zakázce, kde jsou denní záznamy. Jiný bude pak v nastavení celé aplikace. V nastavení aplikace budou zobrazeni uživatelé, kteří mají do aplikace přístup. Jak správců, tak i všech uživatelů, kteří budou mít buď trvalý přístup nebo dočasný (např. investoři, koordinátor BOZP, apod.) Rozdělení do skupin podle práv a také podle vypršení povoleného přístupu. Správce (Petr Říha) má neomezená práva.

---

*Naposledy aktualizováno: 3. 5. 2026 22:37:00*
