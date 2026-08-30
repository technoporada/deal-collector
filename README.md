# Deal Collector

Agregator darmowych gier i programów z **SteamDB, Epic Games, GOG i SharewareOnSale**.
Asynchroniczne scrapery, web UI (FastAPI + statyczny frontend), ulubione, deduplikacja
po hashowaniu (title+url+source).

## Funkcje

- ℹ️ Zbiera z 4 źródeł (SteamDB `upcoming/free`, Epic `freeGamesPromotions` API, GOG `?price=free`, SharewareOnSale)
- 📊 Web UI (`/`): lista ofert, przycisk „Odśwież”, kategorie, ulubione (⭐)
-🛡️ Zapamiętuje ulubione w `deals.json`
- 🔁 Asynchroniczny (aiohttp) — zbiera wszystkie źródła równolegle (przez konwencję async/await)
- 🧾 Czyszczenie tytułów/cen, filtr poprawności oferty (`is_valid_deal`)

## Struktura

```
main.py                  # FastAPI (API + statik)
scrapers/
├─ base_scraper.py       # Deal (dataclass), BaseScraper (ABC), czyszczenie
├─ steamdb_scraper.py
├─ epic_scraper.py
├─ gog_scraper.py
└─ shareware_scraper.py
frontend/                # index.html + app.js + style.css
requirements.txt
```

## Uruchomienie

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload
```

Otwórz: http://127.0.0.1:8000

## API

| Ścieżka | Metoda | Zapis |
|---|---|---|
| `/api/deals` | GET | lista ofert (opcjonalnie `?category=`) |
| `/api/favorites` | GET | ulubione |
| `/api/favorites/{id}` | POST / DELETE | dodaj/usuń ulubione |
| `/api/scrape` | POST | uruchom scrapowanie |

## Wymagania

- Python 3.9+
- Biblioteki z `requirements.txt`

## Licencja

MIT — patrz `LICENSE`.