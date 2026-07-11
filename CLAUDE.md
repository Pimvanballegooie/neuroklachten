# VindJeFysio Netwerk — neuroklachten.net

Deze repo is één "spoke" in een hub-and-spoke netwerk van gespecialiseerde fysiotherapie-subsites. De hub is vindjefysio.net; spokes zijn o.a. rugnek, enkelvoet, beenklachten, kansrijkopgroeien, mentaalgezond, chronischezorg, armklachten, gezondoud en deze (neuroklachten).

## Architectuur
- Statische HTML/CSS/vanilla JS op GitHub Pages, custom domein via CNAME.
- Gedeelde Supabase-backend, project islujznszevdynguhjdc, met anon key in de frontend.
- Gedeelde tabellen: therapeuten, praktijken, therapeut_subcategorieen, therapeut_praktijken, subcategorieen, categorieen.
- Elke spoke deelt dezelfde structuur en bestanden: index.html, therapeut-aanmelden.html, mijn-profiel.html, therapeuten.html, privacy.html, protocollen.html (gegenereerd), sync_protocollen.py, .github/workflows/sync.yml, protocollen-config.json.

## Belangrijke conventies
- therapeut-aanmelden.html linkt ALTIJD relatief/lokaal binnen de eigen subsite (nooit naar vindjefysio.net).
- Praktijk/locatie-aanmelden loopt WEL centraal via vindjefysio.net/aanmelden.html?via=<domein>.
- Mails lopen via info@vindjefysio.net.
- Therapeut-registratie zet aangemeld_via op het eigen subsite-domein en actief=false (wacht op goedkeuring).
- Deze site: palet primair #2E9B8F (teal), light #E6F4F2, dark #237A70, navy #1F3A4D, accent #F5A623. Structuur = vijf losse aandoeningen (géén gebieden, géén thema's, géén netwerk-eis zoals het Lage Rugnetwerk bij rugnek): CVA en NAH (19), Parkinson (20), MS (21), Neuromusculaire aandoeningen (22), Duizeligheid en evenwicht (23) — categorie 3 "Neurologie" in Supabase. Elk domein = precies 1 subcategorie, dus geen geneste chips-per-domein en geen domein+thema-combinatiefilter zoals in rugnek.

## Sync-pipeline
- sync_protocollen.py haalt protocollen op uit publiek gedeelde Google Docs (export-link, geen API-key), zet markdown om naar HTML, genereert protocollen/<id>-makkelijk.html (patiënt) en -complex.html (therapeut) + protocollen.html + sitemap.xml.
- De workflow git-add regel moet zijn: git add protocollen/ protocollen.html sitemap.xml (op één regel).
- Google Docs moeten op "iedereen met de link kan bekijken" staan.
- Zones: cva-nah, parkinson, ms, neuromusculair, duizeligheid (één op één met de vijf domeinen, geen aparte thema-zone).
