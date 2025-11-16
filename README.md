Dodajemy cztery pliki pomocnicze z materiałów.

Tworzymy plik requirements.txt zgodnie z materiałami.

W materiałach używaliśmy uWSGI, jednak Paketo Buildpacks nie współpracuje z uWSGI przy Pythonie 3.11 (uWSGI uruchamia własny interpreter, a Paketo dostarcza minimalny runtime, co powoduje błąd No module named 'encodings').
Dlatego w Procfile używamy Gunicorn:

web: gunicorn main:app --bind 0.0.0.0:$PORT


Gunicorn działa poprawnie z Paketo, korzysta z Pythona dostarczonego przez buildpacki, main:app wskazuje na aplikację WSGI w pliku main.py, a --bind 0.0.0.0:$PORT ustawia nasłuch na wymaganym porcie.

Inicjalizujemy repozytorium:

git init
git add .
git commit -m "Initial version"


Upewniamy się, że Docker Desktop jest uruchomiony (docker ps).

Instalujemy Pack CLI:

brew install buildpacks/tap/pack


(narzędzie do budowania aplikacji za pomocą Buildpacks)

Budujemy aplikację:

pack build my-python-app \
  --builder paketobuildpacks/builder-jammy-full \
  --path .


Uruchamiamy obraz Dockera:

docker run --rm -e PORT=8000 -p 8000:8000 my-python-app


Sprawdzamy działanie aplikacji pod:
http://127.0.0.1:8000

Opcjonalnie — wystawienie na Heroku:

heroku login
git push heroku main
