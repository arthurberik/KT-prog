Faili elektrihinnad.txt on salvestatud info ühe perioodi elektrihindade kohta. Failis on iga päeva
kohta 2 rida infot: kuupäev ja hind ning need on antud iga päeva kohta samas järjekorras. Hinna
andmetüüp on ujukomaarv. Lisaks ei ole ette teada, mitme päeva kohta failis infot on.
Näide faili elektrihinnad.txt võimalikust sisust
13-09-2021
134.99
14-09-2021
141.60
15-09-2021
160.36
16-09-2021
145.19
17-09-2021
141.09
18-09-2021
121.19
19-09-2021
93.47
Kirjuta programm, mis leiab ja väljastab ekraanile, millisel kuupäeval oli elektrihind kõige kõrgem,
kui palju elekter sel päeval maksis ning kui palju raha kulus sel päeval kütmiseks, kui kütteks kulus
24 kWh elektrit (tulemus ümardada kahe kohani pärast koma). Väljundis peab kuupäev olema
näites toodud kujul. Lisaks arvutab ja väljastab programm ekraanile, mis oli perioodi keskmine
elektrihind. Hind tuleb ümardada kahe kohani pärast koma. Programm peab salvestama keskmise
elektrihinna faili keskmine.txt.
Näide programmi võimalikust väljundist (kasutaja sisend on paksus kirjas)
Sisesta failinimi: elektrihinnad.txt
Kõrgeim elektrihind oli 15.09.2021 - 160.36 €/MWh
Kütteks kulus 3.85 eurot.
Keskmine elektrihind oli 133.98 €/MWh
Näide faili keskmine.txt võimalikust sisust
Keskmine elektrihind oli 133.98 €/MWh

# Elektrihinnad

# Küsime kasutajalt faili nime
faili_nimi = input("Sisesta failinimi: ").strip()

try:
    with open(faili_nimi, "r", encoding="utf-8") as f:
        read_lines = [line.strip() for line in f if line.strip()]
except FileNotFoundError:
    print(f"Faili '{faili_nimi}' ei leitud.")
    exit()

# Loome kuupäeva ja hinna paarid
kuupäevad = []
hinnad = []

i = 0
while i < len(read_lines):
    kuupäev = read_lines[i]
    hind = float(read_lines[i+1])
    kuupäevad.append(kuupäev)
    hinnad.append(hind)
    i += 2

# Kõrgeim hind
maks_hind = max(hinnad)
maks_index = hinnad.index(maks_hind)
maks_kuupäev = kuupäevad[maks_index]

# Kütte kulu 24 kWh jaoks
kytte_kwh = 24
kulu = round((maks_hind * kytte_kwh) / 1000, 2)  # €/kWh -> kWh kulu eurodes

# Keskmine hind
keskmine = round(sum(hinnad) / len(hinnad), 2)

# Väljund
print(f"Kõrgeim elektrihind oli {maks_kuupäev} - {maks_hind:.2f} €/MWh")
print(f"Kütteks kulus {kulu:.2f} eurot.")
print(f"Keskmine elektrihind oli {keskmine:.2f} €/MWh")

# Salvestame faili keskmine.txt
with open("keskmine.txt", "w", encoding="utf-8") as f_out:
    f_out.write(f"Keskmine elektrihind oli {keskmine:.2f} €/MWh\n")

