# My Jenkins Templates

Kolekcja szablonów Jenkinsfile do automatyzacji procesów CI/CD dla różnych typów projektów. Wszystkie szablony są w pełni parametryzowane i dostosowane do pracy z Jenkinsem działającym na HTTPS z unikalnymi tokenami dla każdego zadania.

## 📋 Dostępne Szablony

### 1. 🐳 Docker Container (`docker-container/`)

Szablon do budowania pojedynczego kontenera Docker z repozytorium GitHub.

**Parametry:**

-   `CONT_NAME` - Nazwa kontenera (wymagane)
-   `GITHUB_REPO_URL` - URL repozytorium GitHub (wymagane)

**Etapy:**

-   ✅ Walidacja parametrów
-   📁 Tworzenie katalogu projektu
-   📥 Klonowanie repozytorium
-   🔒 Skan bezpieczeństwa z Snyk
-   🏗️ Budowanie obrazu Docker

### 2. 🐳🐳 Docker Multi-Containers (`docker-multi-containers/`)

Szablon do uruchamiania aplikacji wielokontenerowych z docker-compose.

**Parametry:**

-   `CONT_NAME` - Nazwa kontenera (wymagane)
-   `GITHUB_REPO_URL` - URL repozytorium GitHub (wymagane)

**Etapy:**

-   ✅ Walidacja parametrów
-   📁 Tworzenie katalogu projektu
-   📥 Klonowanie repozytorium
-   🔒 Skan bezpieczeństwa z Snyk
-   📖 Odczyt konfiguracji z docker-compose.yml
-   🔍 Sprawdzenie wersji oprogramowania
-   🚀 Uruchomienie kontenerów Docker
-   🛡️ Skan bezpieczeństwa OWASP ZAP
-   🧹 Czyszczenie nieużywanych obrazów Docker

### 3. ⚛️ Docker Next.js (`docker-next/`)

Szablon specjalnie dostosowany do aplikacji Next.js w kontenerach Docker.

**Parametry:**

-   `CONT_NAME` - Nazwa kontenera (wymagane)
-   `GITHUB_REPO_URL` - URL repozytorium GitHub (wymagane)

**Etapy:**

-   ✅ Walidacja parametrów
-   📁 Tworzenie katalogu projektu
-   📥 Klonowanie repozytorium
-   🔒 Skan bezpieczeństwa z Snyk
-   🔍 Sprawdzenie wersji oprogramowania
-   🚀 Uruchomienie kontenerów Docker
-   🧹 Czyszczenie nieużywanych obrazów Docker

### 4. 🟢 Node.js App (`node-app/`)

Szablon do uruchamiania aplikacji Node.js z konfiguracją NGINX.

**Parametry:**

-   `GITHUB_URL` - URL repozytorium GitHub
-   `REPO_NAME` - Nazwa repozytorium
-   `SERV_PORT` - Port serwera aplikacji

**Etapy:**

-   📥 Klonowanie repozytorium
-   🔧 Ładowanie zmiennych środowiskowych
-   🔍 Sprawdzenie wersji oprogramowania
-   📦 Instalacja zależności
-   ⚙️ Konfiguracja NGINX
-   🚀 Uruchomienie projektu

## 🔧 Wymagania

### Jenkins

-   Jenkins z włączonym HTTPS
-   Unikalne tokeny dla każdego zadania
-   Zainstalowane pluginy:
    -   Git Plugin
    -   Docker Plugin
    -   NodeJS Plugin
    -   Pipeline Plugin

### Narzędzia na Jenkinsie

-   Docker
-   Docker Compose
-   Node.js 20
-   Snyk CLI
-   OWASP ZAP (dla skanów bezpieczeństwa)
-   NGINX (dla aplikacji Node.js)

## 🚀 Sposób Użycia

### 1. Utwórz nowe zadanie Jenkins

1. Przejdź do Jenkins → New Item
2. Wybierz "Pipeline"
3. Wprowadź nazwę zadania (np. "Docker-Build-Pipeline")

**Uwaga:** To zadanie będzie służyć jako szablon dla wielu projektów - każdy może używać tego samego zadania z różnymi parametrami.

### 2. Skonfiguruj Pipeline

1. W sekcji "Pipeline" wybierz "Pipeline script from SCM"
2. Wybierz "Git" jako SCM
3. Wprowadź URL tego repozytorium (z szablonami Jenkinsfile)
4. Ustaw branch na `main`
5. W "Script Path" wpisz ścieżkę do wybranego szablonu (np. `docker-container/Jenkinsfile`)

**Uwaga:** Pipeline będzie uruchamiany z repozytorium docelowym (przekazanym przez parametr `GITHUB_REPO_URL` lub `GITHUB_URL`), ale skrypt Jenkinsfile będzie pobierany z tego repozytorium z szablonami.

### 3. Dodaj parametry

W sekcji "Build Triggers" → "This project is parameterized" dodaj wymagane parametry:

**Dla szablonów Docker:**

-   `CONT_NAME` (String Parameter)
-   `GITHUB_REPO_URL` (String Parameter)

**Dla Node.js App:**

-   `GITHUB_URL` (String Parameter)
-   `REPO_NAME` (String Parameter)
-   `SERV_PORT` (String Parameter)

### 4. Uruchom zadanie

1. Kliknij "Build with Parameters"
2. Wprowadź wartości parametrów (w tym URL repozytorium docelowego)
3. Kliknij "Build"

**Alternatywnie:** Skonfiguruj webhook w repozytorium docelowym, aby automatycznie uruchamiał pipeline z odpowiednimi parametrami.

## 🔒 Bezpieczeństwo

Wszystkie szablony zawierają wbudowane skany bezpieczeństwa:

-   **Snyk** - skanowanie zależności, obrazów Docker i konfiguracji IaC
-   **OWASP ZAP** - testy penetracyjne aplikacji web (tylko docker-multi-containers)

## 📁 Struktura Repozytorium

```
my-jenkins-templates/
├── docker-container/
│   └── Jenkinsfile          # Pojedynczy kontener Docker
├── docker-multi-containers/
│   └── Jenkinsfile          # Wielokontenerowa aplikacja
├── docker-next/
│   └── Jenkinsfile          # Aplikacja Next.js
├── node-app/
│   └── Jenkinsfile          # Aplikacja Node.js z NGINX
└── README.md
```

## 🔄 Aktualizacje

Szablony są regularnie aktualizowane z najnowszymi praktykami CI/CD i narzędziami bezpieczeństwa. Sprawdzaj regularnie dostępne aktualizacje.

## 🤝 Wsparcie

W przypadku problemów lub pytań dotyczących szablonów, utwórz issue w tym repozytorium lub skontaktuj się z zespołem DevOps.

---

**Uwaga:** Upewnij się, że Jenkins ma odpowiednie uprawnienia do klonowania repozytoriów i uruchamiania kontenerów Docker.
