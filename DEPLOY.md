# DEPLOY.md

the_tinder_files · v1.0 · static site · geen build nodig

## wat zit erin

```
index.html    de hele site (versleuteld)
dl/           versleutelde downloads en pagina's
.nojekyll     zegt tegen github pages: niks aan veranderen
README.md     de voorkant van de repo
DEPLOY.md     dit bestand
```

houd `index.html` en `dl/` naast elkaar en hernoem niks.

alles is versleuteld: AES-256-GCM, sleutel via PBKDF2-SHA256 (600.000 iteraties).
zonder de code is het onleesbaar. de code ken jij.

## route a · github transfer (aanbevolen)

1. open `MIGRATION.md` op de site en maak alle 6 pre-transfer checks groen
2. klik `request transfer ›` en dien het issue in
3. kim keurt goed → jij krijgt een mail van github → accept
4. in jouw repo: **Settings → Pages → Deploy from a branch → `main` / `(root)` → Save**
5. custom domain: vul `theonlinearchives.nl` in (zie *domein*), vink **Enforce HTTPS** aan
6. de site ziet zelf dat hij verhuisd is: `✓ migrated · welcome home`

let op: github pages verhuist niet automatisch mee met de repo.
tussen stap 3 en 4 is de site even offline. dat is normaal.

## route b · ergens anders (`npm run migrate`)

- **netlify**: app.netlify.com/drop → sleep de map erin
- **cloudflare pages**: create project → direct upload → map uploaden
- **eigen server**: kopieer de map naar je webroot

https is verplicht: de ontsleuteling (web crypto) werkt alleen via https of localhost.
lokaal testen: `python3 -m http.server` in de map → `http://localhost:8000`
(`file://` werkt niet, dan kan de site `dl/` niet ophalen)

## domein

`theonlinearchives.nl` kan mee: houderwijziging of verhuistoken via de registrar (vraag kim).

voor github pages, bij de registrar:

```
A      @     185.199.108.153
A      @     185.199.109.153
A      @     185.199.110.153
A      @     185.199.111.153
CNAME  www   <jouw-github-naam>.github.io
```

## swag/

bestellingen worden per webadres opgeslagen (localStorage).
op een nieuw adres staat alles weer op "niet besteld".
bestel de comic en het kaartspel opnieuw in `swag/` om ze in `assets/` en `bin/` te ontgrendelen. kost niks.
hetzelfde geldt voor de pre-transfer checks en de "new"-labels.

## daarna

`git clone`, aanpassen wat je wil. het is jouw repo nu.
