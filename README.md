# SoilScope - Soil-Plant-Atmosphere Simulator

**Project Status: Phase 11 Completed - Digital Twin Polish & Immersive Stability**

SoilScope on tieteellisesti tarkka maaperä-kasvi-ilmakehä-jatkumon (SPAC) simulaattori, joka yhdistää pelillistetyn oppimisen ja laskennallisen ekofysiologian.

---

## ✅ Toteutetut Ominaisuudet

### 🌊 Hydrologia & Fysiikka
- **1D Richards-yhtälö** numeerisella ratkaisijalla
- **Van Genuchten-Mualem** maahydrauliikka
- **Hystereesi** (kuivatus/kostutus)
- **Bypass Flow** dynaamisesti kytkettyjen lierojen makrohuokosten kautta
- **Kapillaarinen nousu** kuivumisnäkymässä
- **Dynaaminen auringonsäteily**: Kytketty fotosynteesiin reaaliaikaisella PAR-muunnoksella (W/m² → µmol m⁻² s⁻¹)

### 🌱 Kasvin Fysiologia (SPAC)
- **Farquhar-von Caemmerer-Berry (FvCB)** C3-fotosynteesimalli
- **Tardieu ilmarakomalli** stomataaliselle konduktanssille
- **Jarvis kompensoiva vedenotto** - kuivat kerrokset kompensoivat
- **C-ROOT** dynaaminen juuriarkkitehtuuri gravotropismilla (pääjuuret kasvavat pystysuoraan alaspäin)
- **Synkronoitu usean kasvin SPAC-jatkumo**: Animaatiot ja ratkaisijat tukevat useita kasveja samanaikaisesti, versot ja juuret on ankkuroitu täsmälleen samaan pisteeseen.
- **Orgaaninen kasvikomponentti**: Proceduraalinen `CustomPainter`-pohjainen kasvi, joka visualisoi verson ja juuriston kasvua dynaamisesti.
- **Hiilen hallinta (POM/MAOM)**: Dynaaminen labiilin ja stabiilin hiilen säätely, Rhizosphere Priming Effect -ketjun aktivointi ja hiukkasfysiikan Q10-vaste.
- **Dynaaminen virtausseuranta**: ravinteet ja vesi hakeutuvat todellisiin juurenpäihin

### 🧪 Biogeokemia
- **Rhizosphere Priming Effect**: juurieritteet aktivoivat mikrobit kausaalisessa ketjussa
- **TEA Redox-tikapuut**: O₂ → NO₃⁻ → MnO₂ → Fe(III) → SO₄²⁻ → CH₄
- **Tieteellinen Redox-kalibrointi**: Päivitetyt kynnysarvot `chemistry_solver.dart`:ssa ja Nernst-yhtälön laskenta
- **Michaelis-Menten entsyymikinetiikka** (urease, phosphatase, cellulase, protease)
- **Mykorritsasymbioosi** dynaaminen verkosto ja C-P-N vaihto
- **Energiatehokas Kemotaksis (Vähimmän Energian Periaate)**: Kaikki organismit (juuret, sienirihmastot ja mikrobit) hakeutuvat resursseihin energiatehokkaasti (Fickin laki & Cost-Benefit).
- **Symbioottinen Louhinta**: Orgaanisen fosforin ja typen muokkaus liukoiseksi Michaelis-Menten -kinetiikalla.
- **C/N Immobilisaatio**: Mikrobit sitovat typpeä, kun C/N-suhde > 25.
- **Tillage-muokkaushäiriöt**: Maan muokkaus rikkoo sienirihmastoverkoston (80% vähennys).
- **POM/MAOM hiilimalli** (Microbial Carbon Pump)
- **Typen kierto** (DNDC): nitrifikaatio, denitrifikaatio, immobilisaatio "morphing"-animaatioilla
- **Sähköstaattinen fysiikka**: Coulombin laki ohjaa ionien hakeutumista varautuneille pinnoille

### 🎮 Interaktiivinen Hallintapaneeli & Digital Twin
- **Eristetty HUD-kerros (Viewport)**: Kamerasta riippumaton kiinteä käyttöliittymäkerros. 
- **Nanovision (Mikroskooppi)**: Mikroskooppiominaisuus, joka mahdollistaa yksityiskohtaisen poikkileikkausnäkymän juurista, lehdistä ja mikrobeista.
- **3-Kerroksinen UI**: visualisointi keskittyy biologisesti aktiiviseen pintamaahan (Top 50cm)
- **Atmosfäärin ohjaus**: Kaasunvaihdon ($CO_2$, $H_2O$) dynaamiset animaatiot synkronoitu kunkin kasvin lehvästön sijaintiin.
- **Tieteelliset kaaviot**: Mollier-diagrammi ja PAR-näkymä Control Panelissa tarkempaan atmosfäärin analyysiin.
- **Isolate-pohjainen fysiikka (30 FPS)**: tuhansien hiukkasten dynaaminen laskenta on optimoitu tasaiseen 30 FPS tahtiin.
- **LOD (Level of Detail)**: hiukkasrenderöinti skaalautuu zoom-tason mukaan suorituskyvyn varmistamiseksi
- **Full-Screen Immersive Digital Twin**: Simulaatio täyttää koko ruudun dynaamisesti säätyvällä horisontilla ja ilmakehällä.
- **Flutter Overlay Inspector**: Korkean fideliteetin bioväylätietojen tarkastelu on toteutettu dynaamisena Flutter-kerroksena.
- **SPAC-kausaalisuusnuolet**: Kaasunvaihdon ja veden virtauksen animaatiot sisältävät nyt suuntanuolet ja realiaikaisen voimakkuussäädön, jotka visualisoivat biovirtauksia.
- **Typenkierron havainnointitila**: Mahdollistaa N-yhdisteiden ($NH_4^+$, $NO_3^-$) korostamisen ja muiden himmentämisen `FlutterQuickActions`-paneelista.
- **Tilan tallennus & Toisto**: Integroitu `SharedPreferences`-pohjainen tilan tallennus ja aikajanan toistonäppäimet.
- **Dynaaminen Skenaarioeditori (Scenario Builder)**: Luo omia skenaarioita säätämällä maalajeja, alkukosteutta ja viljelysuunnitelmia (lannoitus, kastelu, muokkaus).


### 🧮 Logic Lab - Visuaalinen biofysiikan editori
- **Node-pohjainen graafieditori** tieteellisten kaavojen tarkasteluun ja dynaamiseen testaamiseen.
- **Tuetut funktiot ja matemaattinen pohja:**
  - **Q10 (Lämpötilakerroin):** $f(T) = Q_{10}^{((T - 20) / 10)}$
  - **Michaelis-Menten (Entsyymikinetiikka):** $v = V_{max} \cdot \frac{[S]}{(K_m + [S])}$
  - **van Genuchten (Vedenpidätys):** $\theta(h) = \theta_r + \frac{\theta_s - \theta_r}{[1 + |\alpha h|^n]^m}$
  - **Farquhar-von Caemmerer-Berry (FvCB):** $A_c = V_{cmax} \cdot \frac{C_i - \Gamma^*}{C_i + K_c(1 + O/K_o)}$
  - **Nernst-yhtälö (Redox):** $pe = pe_0 - \frac{1}{n} \cdot \log_{10}\frac{[red]}{[ox]}$
  - **Chemotaxis (Fickin laki):** $J = -D \cdot \frac{C_2 - C_1}{dx}$
  - **Cost-Benefit (Vähimmän energian periaate):** $A = \frac{C}{D + P}$
- **Live-evaluointi** simulaatiodatalla
- **UX-parannukset**: Työkaluvihjeet (Tooltips) ja reaaliaikainen yksiköiden muotoilu solmuille.

### 🔬 Validointi & Diagnostiikka
- **Tilastolliset metriikat**: RMSE, NSE, R², MAE
- **Kytkentämatriisi** järjestelmädiagnostiikkaan
- **Science Validation Tab**: Reaaliaikainen tilastollisten mittareiden (RMSE, NSE, R²) seuranta käyttöliittymässä.
- **50 yksikkötestiä** biofysiikan solvereiden varmistamiseen

---

## 🚀 Käynnistys

```bash
# Asenna riippuvuudet
flutter pub get

# Generoi Freezed-koodi
dart run build_runner build --delete-conflicting-outputs

# Käynnistä sovellus
flutter run
```

---

## 📄 Lisenssi

Tämä projekti on lisensoitu **PolyForm Noncommercial License 1.0.0** -lisenssillä.

- **Sallittu:** Lähdekoodin tarkastelu, yksityinen käyttö, akateeminen käyttö ja tutkimuskäyttö.
- **Kielletty:** Kaupallinen hyödyntäminen ilman erillistä sopimusta tekijän kanssa.

Katso täydet ehdot tiedostosta [LICENSE.md](LICENSE.md).

### Käytetyt kirjastot ja niiden lisenssit

| Kirjasto | Käyttötarkoitus | Lisenssi |
| :--- | :--- | :--- |
| **Flutter SDK** | Käyttöliittymäkehys | BSD-3-Clause |
| **Flame** | 2D-pelimoottori ja animaatiot | MIT |
| **Flutter Riverpod** | Reaktiivinen tilanhallinta | MIT |
| **Equations** | Matemaattiset ratkaisijat | MIT |
| **Oxygen** | Kevyt ECS-fysiikkamoottori | MIT |
| **Flutter SVG** | Vektorigrafiikan renderöinti | MIT |
| **Freezed** | Immuuttomat datamallit | MIT |
| **Intl** | Kansainvälistyminen ja lokalisointi | BSD-3-Clause |
| **Shared Preferences** | Paikallinen asetusten tallennus | BSD-3-Clause |
| **Flutter Secure Storage** | Suojattu avainten tallennus | BSD-3-Clause |
| **JSON Annotation** | JSON-serialisointi | BSD-3-Clause |


