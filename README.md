# Fiscal config

Cote și plafoane fiscale, centralizate pentru toate site-urile de contabilitate.

## Cum se folosește

1. **În producție**: găzduit pe GitHub într-un repo separat (ex: `cifrapro/fiscal-config`).
2. **Citit prin jsDelivr CDN**, fără rate limit:
   ```
   https://cdn.jsdelivr.net/gh/USER/REPO@main/2026.json
   ```
3. **Update**: schimbi `2026.json` în repo, comiti, deploy automat. Toate site-urile preiau în 24h (cache `revalidate`).

## Convenții

- Un fișier per an: `2025.json`, `2026.json`, `2027.json`.
- `current.json` = symlink (sau copie) către anul curent. Site-urile citesc `current.json`.
- Toate cotele sunt fracții (0.25, nu 25). Multiplicarea cu 100 se face în UI.
- Sumele monetare sunt în RON, fără separator de mii.

## Versionare

Câmpul `version` urmează formatul `<an>.<patch>`:
- `2026.1` = prima publicare a cotelor pe 2026
- `2026.2` = corecție (de ex., schimbare salariu minim mid-year)

Folosește tag-uri git (`v2026.1`) pentru a forța o versiune specifică:
```
https://cdn.jsdelivr.net/gh/USER/REPO@v2026.1/2026.json
```

## Ce NU pune aici

- Logică de calcul (rămâne în cod).
- Texte de UI (rămân în config-ul fiecărui site).
- Date personale sau firme (cote, doar cote).
