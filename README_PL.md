# 🛠️ Workflow Automatyzacji Przetwarzania Zamówień – Make.com

Ten projekt przedstawia kompletny workflow automatyzacji w Make.com, który służy do przetwarzania zamówień w formacie PDF, ekstrakcji danych klienta i zamówienia przy użyciu OCR Google Cloud Vision oraz OpenAI API, następnie generuje kody produktów na podstawie wewnętrznych danych firmy i dodaje zamówienia do systemu CRM.

---

## 📌 Cel automatyzacji

Zautomatyzować obsługę zamówień otrzymywanych w formacie PDF, eliminując konieczność ręcznego odczytu, ekstrakcji danych oraz wprowadzania zamówień do systemu CRM.

---

## 💡 Technologie i integracje

| Narzędzie        | Zastosowanie                                 |
|------------------|----------------------------------------------|
| Make.com         | Główne środowisko workflow                   |
| Webhook          | Odbieranie plików PDF z zamówieniami                         |
| Google Cloud Vision API (OCR)         | Przetwarzanie PDF na tekst                     |
| AirTable         | Baza danych z zamówieniami                     |
| OpenAI API       | Analiza treści zamówień, tworzenie kodów produktów                       |
| CRM (PlentyMarket) | Dodawanie zamówień do systemu             |

---
## 🗂️ Struktura workflow

Workflow składa się z **8 głównych faz**, przedstawionych poniżej:

---

### 1. 🔗 Webhook – Pobieranie zamówień

- **Opis:** Workflow rozpoczyna się od aktywacji webhooka Make, który przyjmuje pliki w formacie PDF z zamówieniami.
- **Działania:**
  - Odbiór plików z nowymi zamówieniami.
  - Iteracja po każdym zamówieniu (jeśli przychodzi wiele na raz).

<img width="1030" height="133" alt="image" src="https://github.com/user-attachments/assets/f85e5c5e-4c08-4851-bf5a-b908c354a084" />


---

### 2. 📄 OCR – Przetwarzanie PDF na tekst

- **Opis:** Każdy załączony PDF z zamówieniem jest przesyłany do Google Cloud Vision API w celu rozpoznania tekstu.
- **Działania:**
  - Przesyłanie PDF jako obrazów do OCR.
  - Odbiór tekstowego wyniku analizy.

<img width="403" height="171" alt="image" src="https://github.com/user-attachments/assets/d3ab6e51-a081-471b-92eb-6beb79e8c917" />


---

### 3. 🧠 Ekstrakcja danych – OpenAI API (GPT-4)

- **Opis:** Za pomocą GPT-4 analizowany jest tekst zamówienia, by wydobyć dane klienta i szczegóły zamówienia.
- **Działania:**
  - Przesłanie przetworzonego tekstu do OpenAI GPT-4 z promptem wyciągającym strukturę JSON.
  - Dane obejmują: nazwę klienta, dane kontaktowe, produkty, ilości.
  - Zapisanie wyniku w Airtable.

<img width="1147" height="275" alt="image" src="https://github.com/user-attachments/assets/e59becd9-8a7f-4fb0-97ad-b2d83ec03591" />


---

### 4. 🧮 Generowanie kodów produktów

- **Opis:** Na podstawie zamówionych produktów i danych z bazy Airtable tworzony jest unikalny kod dla każdego produktu.
- **Działania:**
  - Dopasowanie nazw produktów do wewnętrznych kodów.
  - Obsługa wyjątków dla niestandardowych produktów.

<img width="1251" height="104" alt="image" src="https://github.com/user-attachments/assets/976c8748-bc9e-4dfb-b75e-5c420e6d6426" />


---

### 5. ✅ Walidacja poprawności kodów

- **Opis:** Sprawdzenie, czy do każdego produktu przypisano poprawny kod.
- **Działania:**
  - Weryfikacja braków lub niezgodności w kodach.
  - Oznaczenie błędnych zamówień do ręcznego przeglądu.

<img width="327" height="617" alt="image" src="https://github.com/user-attachments/assets/487609bc-7763-43ea-8f59-125ab346f35a" /> <img width="294" height="624" alt="image" src="https://github.com/user-attachments/assets/4c458ef0-506a-4ae1-9db6-528cc0df2705" />



---

### 6. 📦 Weryfikacja ilości (sztuki vs. paczki)

- **Opis:** Upewnienie się, że ilość zamówionego towaru została prawidłowo zinterpretowana (czy klient podał liczbę sztuk czy paczek).
- **Działania:**
  - Analiza jednostki miary z tekstu.

---

### 7. ✍️ Aktualizacja rekordu w Airtable

- **Opis:** Po przetworzeniu kodów i ilości, dane zostają zaktualizowane w bazie danych Airtable.
- **Działania:**
  - Uzupełnienie rekordu o: kody produktów, ilości.

<img width="1120" height="213" alt="image" src="https://github.com/user-attachments/assets/da009165-b50f-4ce1-bbf0-6e0ade05bd26" />


---

### 8. 📤 Dodanie zamówienia do CRM

- **Opis:** Finalnym krokiem jest dodanie kompletnego zamówienia do systemu CRM firmy.
- **Działania:**
  - Przesłanie danych zamówienia do API CRM.
  - Aktualizacja statusu w Airtable.

<img width="584" height="93" alt="image" src="https://github.com/user-attachments/assets/9e3168f0-2fdf-426e-ae6f-d836ed1641e0" />



---
## **Autor**
Stworzony przez Rafał Zajkowski.
