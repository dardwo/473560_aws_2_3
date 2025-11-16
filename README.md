1. Dodajemy 4 pliki pomocnicze
2. Tworzymy plik requirements.txt (jak w materialach)
3. Tworzymy Procfile (jak w materialach)
4. Inicjalizacja repo - git init, git add. , git commit -m ""
5. Uruchomic aplikacje Docker Desktop (mozna sprawdzic w termianlu docker ps)
6. Instalizuje pack z Paketo Builpacks CLI - brew install buildpacks/tap/pack (potwierdzenie poprawnej instalacji pack --version - tutaj odpowiedz; 0.38.2+git-f1c347c.build-6533)
7. Buduje aplikacje: pack build my-python-app \
  --builder paketobuildpacks/builder:base \
  --path .
8. I na koniec docker run --rm -e PORT=8000 -p 8000:8000 my-python-app
9. Mozemy sprawdzic czy dziala pod http://127.0.0.1:8000
10. Do wystawienia na heroku - heroku login; git push heroku main