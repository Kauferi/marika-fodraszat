# Szobi Marika Fodrászat – Astro weboldal

Statikus Astro-oldal: Kezdőlap, Árlista, Kapcsolat (e-mail küldő űrlappal), Köszönöm oldal.
A fodrász a `/admin` címen (Decap CMS) maga szerkesztheti az árlistát, a nyitvatartást és az elérhetőségeket.

## Helyi futtatás

```bash
npm install
npm run dev        # http://localhost:4321
```

A szerkesztőfelület helyi kipróbálása (GitHub nélkül):
1. A `public/admin/config.yml` fájlban vedd ki a `#` jelet a `local_backend: true` elől.
2. Egy második terminálban: `npx decap-server`
3. Nyisd meg: http://localhost:4321/admin/
   Itt felvehetsz új kategóriát, új szolgáltatást, árat módosíthatsz – a változás a `src/data/*.json` fájlokba íródik.

## Hol van a tartalom?

| Fájl | Mit tartalmaz |
|---|---|
| `src/data/arlista.json` | Árlista kategóriákkal és szolgáltatásokkal |
| `src/data/beallitasok.json` | Név, szlogen, bemutatkozás, cím, telefon, e-mail, nyitvatartás |
| `src/config.ts` | A kapcsolati űrlap Web3Forms kulcsa |
| `public/admin/config.yml` | A szerkesztőfelület mezői |

## Élesítés – teendők

1. **Kapcsolati űrlap:** a https://web3forms.com oldalon add meg a fodrász e-mail-címét, a kapott kulcsot írd be a `src/config.ts`-be. Az üzenetek ide érkeznek.
2. **GitHub:** töltsd fel a projektet az ügyfél GitHub-tárolójába (`node_modules` és `dist` nélkül), és írd át a tároló nevét a `public/admin/config.yml`-ben (`repo:`).
3. **Cloudflare:** Workers & Pages → Create → Import a repository. Build parancs: `npm run build`, kimeneti mappa: `dist`. Utána hozzáadod a saját domaint.
4. **Szerkesztő-belépés (OAuth):** a Decap GitHub-belépéséhez egy kis OAuth segédprogram kell. Ezt egyszer telepítsd Cloudflare Workerre (pl. a `sterlingwes/decap-proxy` vagy hasonló nyílt forráskódú projekt alapján), és az URL-jét írd a `config.yml` `base_url` sorába. Ugyanaz a segédprogram az összes ügyfeledet kiszolgálhatja.
5. **Domain:** a `astro.config.mjs` `site` sorába írd a végleges címet (a Köszönöm oldalra való átirányítás ehhez igazodik).
6. **Adatvédelem:** élesítés előtt kell egy rövid adatkezelési tájékoztató oldal (az űrlap személyes adatot gyűjt).
