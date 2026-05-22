# 🔐 Demonstration af Softwaretest i Loginmoduler

## 📘 Projektbeskrivelse

Dette projekt demonstrerer forskellige softwaretestmetoder anvendt på et simpelt login-system. Fokus ligger på inputvalidering, password-regler, brute force-beskyttelse, CRUD-funktionalitet samt testpyramiden.

**Navn:** Lawin Bamarne
**Dato:** 05-02-2026  
**Projekt:** Demonstration af testteknikker i loginmoduler

---

# 🧪 1. Input Validering

## Ækvivalenspartitionering (Brugernavn: 3–20 tegn)

Input opdeles i logiske grupper, så repræsentative værdier kan testes uden at gennemgå alle mulige kombinationer.

| Type | Klasse | Eksempel | Forventet resultat |
|---|---|---|---|
| Gyldig | Minimum | "abc" | ✔ Godkendt |
| Gyldig | Normal | "testbruger01" | ✔ Godkendt |
| Ugyldig | For kort | "ab" | ✖ Afvist |
| Ugyldig | Tom | "" | ✖ Afvist |
| Ugyldig | For langt | 21 tegn | ✖ Afvist |

---

## Grænseværdianalyse (Password: minimum 8 tegn)

Test af værdier omkring grænsen, hvor fejl typisk opstår.

| Test | Password | Resultat | Funktion |
|---|---|---|---|
| Under grænsen | "1234567" | ✖ Afvist | validate_password() |
| På grænsen | "12345678" | ✔ Gyldig | validate_password() |
| Over grænsen | "123456789" | ✔ Gyldig | validate_password() |

---

# 🔐 2. Sikkerhedslogik

## Brute Force Beskyttelse (Cycle Process Test)

Denne test gennemgår hele login-forløbet:

1. Oprettelse af bruger  
2. Korrekt login  
3. Flere fejlede loginforsøg  
4. Konto låses efter tre forsøg  
5. Korrekt password afvises ved låst konto  
6. Konto nulstilles og adgang gives igen  

---

## Beslutningstabel (Decision Table Test)

| Regel | Password korrekt | Konto låst | Systemrespons |
|---|---|---|---|
| R1 | Ja | Nej | Adgang tilladt |
| R2 | Nej | Nej | Adgang nægtet |
| R3 | Nej | Ja | Konto låst |
| R4 | Ja | Ja | Konto låst |

---

# 🗂 3. CRUD Test (Brugerhåndtering)

Systemet skal kunne håndtere hele brugerens livscyklus.

## Create
Opret ny bruger i systemet.

## Read
Hent og vis brugerdata.

## Update
Ændr password eller brugeroplysninger.

## Delete
Slet bruger sikkert fra systemet.

---

# 🏗 4. Testpyramiden

## Unit Tests
Tester små individuelle funktioner som password-validering.

## Integration Tests
Tester samspillet mellem loginforsøg og låsefunktion.

## System Tests
Tester hele login-flowet fra start til slut.

---

# 🚪 5. Kvalitets Gates

Før systemet kan frigives, skal følgende krav være opfyldt:

- Inputvalidering fungerer korrekt
- Password-regler overholdes
- Brute force-beskyttelse virker
- CRUD-funktionalitet er verificeret
- Loginflow fungerer stabilt

---

# 💻 Eksempel på Unit Test

```python
def validate_password(password):
    return len(password) >= 8

def test_password():
    assert validate_password("12345678") == True
    assert validate_password("1234567") == False
```

---

# ✅ Konklusion

Projektet demonstrerer, hvordan forskellige softwaretestmetoder kan anvendes til at forbedre kvalitet, stabilitet og sikkerhed i login-systemer. Testteknikker som ækvivalenspartitionering, grænseværdianalyse, decision tables og CRUD-tests bidrager til en mere struktureret og sikker softwareudvikling.
