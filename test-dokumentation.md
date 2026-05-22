# Demonstration af testteknikker i loginmoduler

Dette projekt undersøger, hvordan forskellige softwaretestmetoder kan anvendes til at validere og sikre et simpelt login-system.

## Projektinformation
- Dato: 05-02-2026
- Projekt: Demonstration af testteknikker i loginmoduler

---

# 1. Input Validering

## Ækvivalenspartitionering
Brugernavn: 3–20 tegn

| Type | Klasse | Eksempel | Forventet resultat |
|---|---|---|---|
| Gyldig | Minimum | "abc" | ✔ Godkendt |
| Gyldig | Normal | "testbruger01" | ✔ Godkendt |
| Ugyldig | For kort | "ab" | ✖ Afvist |
| Ugyldig | Tom | "" | ✖ Afvist |
| Ugyldig | For langt | 21 tegn | ✖ Afvist |

## Grænseværdianalyse
Password: minimum 8 tegn

| Test | Password | Resultat | Funktion |
|---|---|---|---|
| Under grænsen | "1234567" | ✖ Afvist | validate_password() |
| På grænsen | "12345678" | ✔ Gyldig | validate_password() |
| Over grænsen | "123456789" | ✔ Gyldig | validate_password() |

---

# 2. Sikkerhedslogik

## Brute force beskyttelse (Cycle Test)

1. Oprettelse: Bruger registreres  
2. Korrekt login: Adgang gives  
3. Fejlforsøg: Tre mislykkede forsøg udløser spærring  
4. Låst konto: Selv korrekt password afvises, indtil kontoen nulstilles  

## Beslutningstabel

| Regel | Password korrekt | Konto låst | Systemrespons |
|---|---|---|---|
| R1 | Ja | Nej | Adgang tilladt |
| R2 | Nej | Nej | Adgang nægtet |
| R3 | Nej | Ja | Konto låst |
| R4 | Ja | Ja | Konto låst |

---

# 3. CRUD Test (Brugerhåndtering)

Systemet skal kunne håndtere hele livscyklussen for en bruger:

- Create: Opret ny bruger
- Read: Hent brugerdata
- Update: Ændring af password eller oplysninger
- Delete: Sikker fjernelse af brugerprofil

---

# 4. Testpyramide & Kvalitets Gates

## Testlag

- Unit Tests: Validering af små funktioner
- Integration Tests: Samspil mellem login og låsefunktion
- System Tests: Gennemløb af hele loginflowet

## Kvalitets Gates

Systemet skal bestå:

- Input Gate
- Security Gate
- Release Gate
