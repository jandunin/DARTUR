# DARTUR — kalkulator wycieczek

Kalkulator ofertowy biura podróży DARTUR (jeden samodzielny plik HTML).
Hostowany na własnym FTP (`darturlublin.pl`), wgrywany **automatycznie z GitHub**
przy każdej zmianie — bez ręcznego uploadu, bez Netlify.

- Źródło: [`kalkulator/dartur-kalkulator.html`](kalkulator/dartur-kalkulator.html)
- Adres docelowy: `https://darturlublin.pl/kalkulator/dartur-kalkulator.html`

## Jak działa auto-deploy

1. Zmieniasz `kalkulator/dartur-kalkulator.html` i wysyłasz na GitHub (`git push`).
2. GitHub Actions (`.github/workflows/deploy-ftp.yml`) wgrywa plik na FTP.
3. Po ~minucie zmiana jest na stronie.

## Konfiguracja jednorazowa (raz, po utworzeniu repo)

1. **Sekret z hasłem FTP** — GitHub → repo **Settings** → **Secrets and variables**
   → **Actions** → **New repository secret**:
   - Name: `FTP_PASSWORD`
   - Secret: *(hasło do konta FTP `partech`)*
2. **Sprawdź ścieżkę na serwerze** — w `.github/workflows/deploy-ftp.yml` pole
   `server-dir`. Domyślnie `./domains/darturlublin.pl/public_html/kalkulator/`.
   Uruchom workflow ręcznie (**Actions → Run workflow**) i sprawdź, czy plik
   pojawił się pod `darturlublin.pl/kalkulator/`. Jeśli nie — popraw `server-dir`.

Deploy **nie czyści** serwera (`dangerous-clean-slate: false`) — wgrywa tylko
zmienione pliki, więc nie rusza reszty strony (WordPress).
