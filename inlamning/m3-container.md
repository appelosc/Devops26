## Steg 1
1. Den första raden `FROM python:3.12-slim` avgör python versionen.

2. `COPY requirements.txt` och `RUN pip install...` kommer före COPY eftersom de installerar alla requirements och är cachade. Ifall vi ändrar någon kod i vår app så körs alla commandon EFTER app igen. Ifall de är efter `COPY app ./app` skulle köra pip install på alla requirements VARJE gång vi ändrar koden -> inte effektivt byggt image.

3. Nej. `EXPOSE 8000` är endast dokumentation i dockerfilen

Testar gissningen på riktigt:

<img src="screenshots/m3-container/curl-fail.png" alt="Curl fail" width="600">

curl anropet misslyckas

<img src="screenshots/m3-container/curl-success.png" alt="Curl success" width="600">

curl anropet lyckas

## Steg 3 Testa containers

Testar ifall containerna byggs som de borde med `docker compose up --build`

<img src="screenshots/m3-container/docker-compose-up.png" alt="docker compose up" width="600">

Frontenden går att nå i webbläsaren via localhost:8080

<img src="screenshots/m3-container/frontend-webb.png" alt="frontend på webb" width="600">

## Steg 4 Dockerignore

pycache byggs med i vår image före vi lagar en .dockerignore

<img src="screenshots/m3-container/before-dockerignore.png" alt="före dockerignore" width="600">


Skapar dockerignore för både `/frontend` och `/backend`

<img src="screenshots/m3-container/dockerignore.png" alt="dockerignore innehåll" width="600">

Bevis på att pychache inte mer byggs me i imagen efter `.dockerignores`

<img src="screenshots/m3-container/after-dockerignore.png" alt="efter dockerignore" width="600">

## Steg 5 GHCR

Gjorde steg 5 och loggade in med token, tagga images med latest och pushade taggade imagena till GHRC

<img src="screenshots/m3-container/ghrc-backend.png" alt="ghrc för backend image" width="600">

`latest`tagg på `template-app-backend`

<img src="screenshots/m3-container/ghrc-frontend.png" alt="ghrc för frontend image" width="600">

`latest`tagg på `template-app-frontend`


