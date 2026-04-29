# data-contabilitate

Cote și plafoane fiscale pentru România, centralizate într-un singur fișier folosit de toate site-urile de contabilitate.

## Structură

Un singur fișier: **`current.json`**.

Câmpul `year` din interior arată anul valid. Istoricul versiunilor e disponibil prin git (`git log`, `git show <commit>:current.json`).

## Cum se folosește

Site-urile fac fetch de la jsDelivr CDN, fără rate limit:

```
https://cdn.jsdelivr.net/gh/RazvanBordinc/data-contabilitate@main/current.json
```

În Next.js, cu cache de 24h:

```ts
const res = await fetch(
  'https://cdn.jsdelivr.net/gh/RazvanBordinc/data-contabilitate@main/current.json',
  { next: { revalidate: 86400 } }
);
const config = await res.json();
```

## Update anual

La schimbarea cotelor (an nou, modificare legislativă):

1. Editezi `current.json` cu noile valori și actualizezi `year`, `version`, `lastUpdated`.
2. `git commit -m "update: cote 2027"` și `git push`.
3. jsDelivr refresh în câteva minute, site-urile preiau în 24h.

## Versionare strictă (opțional)

Folosește tag-uri git pentru versiuni stabile:

```bash
git tag v2026.1
git push origin v2026.1
```

Apoi un site poate fixa o versiune anume:

```
https://cdn.jsdelivr.net/gh/RazvanBordinc/data-contabilitate@v2026.1/current.json
```

## Convenții

- Toate cotele sunt fracții (`0.25` nu `25`). Multiplicarea cu 100 se face în UI.
- Sumele monetare sunt în RON, fără separator de mii.
- Câmpul `version` urmează `<an>.<patch>`: `2026.1`, `2026.2` (corecție mid-year), `2027.1` etc.

## Ce NU pune aici

- Logică de calcul (rămâne în cod).
- Texte de UI (rămân în config-ul fiecărui site).
- Date personale sau firme.
