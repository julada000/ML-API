# Aplikacja ML-API

To jest aplikacja ML-API oparta na Flasku, uruchomiona w kontenerze Docker i Docker Compose.
Aplikacja będzie dostępna pod adresem: http://127.0.0.1:5000

## Uruchamianie aplikacji

### 1. Lokalnie 

1. Skopiuj repozytorium na swoje urządzenie:
   ```bash
   https://github.com/julada000/ML-API.git
   ```
   ```bash
   cd ML-API
   ``` 
3. Zainstaluj wymagane biblioteki: Przejdź do katalogu, w którym masz plik requirements.txt i uruchom:
   ```bash
   pip install -r requirements.txt
   ```
4. Uruchom aplikację lokalnie: W terminalu, w tym samym katalogu co plik app.py, uruchom aplikację:
   ```bash
   python app.py
   ```
5. Testowanie aplikacji: Możesz teraz testować swoje API (np. endpoint /predict) za pomocą narzędzi takich jak Postman lub cURL.

### 2. Za pomocą Dockera

1. Zbudowanie obrazu Docker: W terminalu przejdź do katalogu, w którym masz plik Dockerfile, a następnie wykonaj komendę:
   ```bash
   docker build -t my-ml-app .
   ```
Komenda ta utworzy obraz Docker o nazwie my_ml_app

2. Uruchomienie kontenera: Po zbudowaniu obrazu, uruchom kontener:
   ```bash
    docker run -p 5000:5000 my-ml-app
   ```
3. Testowanie aplikacji: Możesz testować aplikację, używając cURL lub Postman. Jeśli aplikacja jest uruchomiona na porcie 5000, endpoint POST /predict można przetestować, wysyłając dane w żądaniu.

### 3. Za pomocą Docker Compose

1. Utwórz plik docker-compose.yml: Jeśli jeszcze tego nie zrobiłeś, utwórz plik docker-compose.yml w katalogu głównym projektu. Plik ten może wyglądać tak:

   ```bash
   version: "3.8"

   services:
     ml_app:
       build: .
       ports:
         - "5000:5000"
       networks:
         - my_network
       depends_on:
         - redis

     redis:
       image: "redis:latest"
       restart: always
       ports:
         - "6379:6379"
       networks:
         - my_network

   networks:
     my_network:
       driver: bridge
   ```

2. Uruchom aplikację za pomocą Docker Compose: Aby uruchomić całą aplikację (w tym Redis) za pomocą Docker Compose, użyj polecenia:
   
       docker-compose up --build    
