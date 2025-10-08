# KT-prog

Programmeerimise 1. kontrolltöö 12.10.2023

Ülesanne 1. Linux (10 p)

Vabavara kogukonnas toimus operatsioonisüsteemi Linux sõprade kohtumine, kus selgitati välja Linuxi versioonide kasutajate arvud. Tulemused salvestati faili linux.txt, kus info Linuxi iga versiooni kohta on kahel real: esimesel real on versiooni nimi ja teisel kasutajate arv. Versioonide arv failis ei ole teada.

Näide faili linux.txt võimalikust sisust

text
Ubuntu
10
Mint
3
Pop!_OS
1
Fedora
4
Arch
6
Kirjuta programm, mis

küsib kasutajalt andmefaili nime,

küsib kasutajalt Linuxi versiooni nime,

kuvab ekraanile
o sisestatud Linuxi versiooni nime koos kasutajate arvuga,
o suurima kasutajate arvuga Linuxi versiooni nime koos kasutajate arvuga,
o vähima kasutajate arvuga Linuxi versiooni nime koos kasutajate arvuga,

salvestab faili populaarne.txt samale reale aastaarv 2023, suurima kasutajate arvuga Linuxi versiooni nime ja selle kasutajate arvu.

Kui neid (suurim, vähim) on mitu, siis kuvatakse ekraanile (ja salvestatakse faili) neist esimene info. Eeldame, et kasutaja sisestab andmed õigesti.

Näide programmi tööst (kasutaja sisend on paksus kaldkirjas)

text
Sisesta andmefaili nimi: linux.txt
Sisesta Linuxi versiooni nimi: Arch
Versioonil Arch kasutajate arv on 6.
Suurima kasutajate arvuga on Ubuntu, mille kasutajaid on 10.
Vähima kasutajate arvuga on Pop!_OS, mille kasutajaid on 1.
Faili populaarne.txt sisu

text
2023 Ubuntu 10



# Küsimine kasutajalt faili nime
faili_nimi = input("Sisesta andmefaili nimi: ")

# Küsimine kasutajalt Linuxi versiooni nime
versiooni_nimi = input("Sisesta Linuxi versiooni nimi: ")

# Faili lugemine
versioonid = []
try:
    with open(faili_nimi, "r", encoding="utf-8") as f:
        read_lines = [line.strip() for line in f if line.strip()]
        for i in range(0, len(read_lines), 2):
            nimi = read_lines[i]
            arv = int(read_lines[i + 1])
            versioonid.append((nimi, arv))
except FileNotFoundError:
    print(f"Faili '{faili_nimi}' ei leitud.")
    exit()
except ValueError:
    print("Failis on vale andmevorming.")
    exit()

# Otsime sisestatud versiooni
tulemus = None
for nimi, arv in versioonid:
    if nimi == versiooni_nimi:
        tulemus = (nimi, arv)
        break

if tulemus:
    print(f"Versioonil {tulemus[0]} kasutajate arv on {tulemus[1]}.")
else:
    print(f"Versiooni '{versiooni_nimi}' ei leitud.")

# Suurima ja vähima kasutajate arvu leidmine
max_versioon = max(versioonid, key=lambda x: x[1])
min_versioon = min(versioonid, key=lambda x: x[1])

print(f"Suurima kasutajate arvuga on {max_versioon[0]}, mille kasutajaid on {max_versioon[1]}.")
print(f"Vähima kasutajate arvuga on {min_versioon[0]}, mille kasutajaid on {min_versioon[1]}.")

# Kirjutame faili populaarne.txt
with open("populaarneme.txt", "w", encoding="utf-8") as f_out:
    f_out.write(f"2023 {max_versioon[0]} {max_versioon[1]}\n")

