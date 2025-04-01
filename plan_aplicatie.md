# Plan Aplicație Comandă Mâncare Pensiune

## 1. Prezentare Generală

Aplicația pentru gestionarea comenzilor de mâncare pentru pensiune este o soluție locală, dezvoltată cu Flutter, care rulează pe o tabletă și permite înregistrarea, gestionarea și raportarea comenzilor de mâncare pentru cele 6 camere ale pensiunii.

## 2. Arhitectura Aplicației

### Tech Stack

- **Framework**: Flutter
- **State Management**: Provider
- **Bază de date locală**: SQLite (prin pachetul sqflite)
- **Generare PDF**: pdf, printing
- **Partajare**: share_plus

### Structura Proiectului

```
lib/
├── models/           # Modelele de date
├── screens/          # Ecranele aplicației
├── providers/        # Provider-i pentru state management
├── services/         # Servicii (DB, PDF, printare)
├── widgets/          # Widgets reutilizabile
├── utils/            # Utilități și helper-i
└── main.dart         # Punctul de intrare al aplicației
```

## 3. Modelul de Date

### Categoria

```dart
class Category {
  final int id;
  final String name;
  final String iconPath;
  bool isActive;
  int displayOrder;
}
```

### Produsul

```dart
class Product {
  final int id;
  final int categoryId;
  final String name;
  final double price;
  final String description;
  bool isAvailable;
  int displayOrder;
}
```

### Comanda

```dart
class Order {
  final int id;
  final int roomNumber;
  final DateTime orderTime;
  final List<OrderItem> items;
  final String notes;
  bool isPaid;
}
```

### Elementul Comandă

```dart
class OrderItem {
  final int id;
  final int orderId;
  final int productId;
  final int quantity;
  final double priceAtOrder;
  final String productName;
}
```

## 4. Descrierea Ecranelor și Funcționalităților

### 4.1 Ecranul Principal (Home Screen)

- Afișează butoane mari pentru fiecare categorie de meniu
- Buton pentru accesarea rapoartelor
- Buton pentru administrarea meniului (protejat cu parolă)

### 4.2 Ecranul de Categorie (Category Screen)

- Listează toate produsele din categoria selectată
- Afișează numele și prețul produselor
- Opțiune de adăugare a produselor în comanda curentă (cu cantitate)

### 4.3 Ecranul de Comandă (Order Screen)

- Afișează lista produselor adăugate în comanda curentă
- Permite modificarea cantității sau eliminarea produselor
- Selectarea camerei pentru care se face comanda (1-6)
- Opțiune pentru adăugarea de note la comandă
- Buton de finalizare și salvare a comenzii

### 4.4 Ecranul de Rapoarte (Reports Screen)

- Filtrare după dată (zi, săptămână, lună)
- Filtrare după cameră
- Vizualizarea tuturor comenzilor conform filtrelor
- Generare și imprimare raport PDF
- Export și partajare prin WhatsApp

### 4.5 Ecranul de Administrare Meniu (Menu Admin Screen)

- Protejat cu parolă simplă
- Listarea tuturor categoriilor cu opțiuni de adăugare/editare/dezactivare
- Pentru fiecare categorie, listarea și gestionarea produselor
- Formulare simple pentru adăugare/editare produse
- Opțiuni de reordonare a categoriilor și produselor
- Marcarea produselor ca disponibile/indisponibile

## 5. Tehnologii și Pachete

### Pachete principale

- [ ] **sqflite**: Pentru baza de date SQLite
- [ ] **provider**: Pentru state management
- [ ] **path_provider**: Pentru gestionarea locațiilor de stocare
- [ ] **pdf**: Pentru generarea documentelor PDF
- [ ] **printing**: Pentru trimiterea documentelor la imprimantă
- [ ] **share_plus**: Pentru partajarea rapoartelor prin WhatsApp
- [ ] **flutter_slidable**: Pentru interacțiuni de tip swipe pe liste
- [ ] **intl**: Pentru formatarea datelor și a valutei

## 6. Planul de Implementare

### Faza 1: Configurare și Structură (Săptămâna 1)

- [ ] Crearea proiectului Flutter nou
- [ ] Configurarea dependențelor în pubspec.yaml
- [ ] Implementarea modelului de date
  - [ ] Crearea class Category
  - [ ] Crearea class Product
  - [ ] Crearea class Order
  - [ ] Crearea class OrderItem
- [ ] Configurarea bazei de date SQLite
  - [ ] Crearea tabelelor
  - [ ] Implementarea metodelor CRUD pentru fiecare model
- [ ] Crearea provider-ilor pentru state management
  - [ ] Provider pentru meniu
  - [ ] Provider pentru coșul de cumpărături/comandă curentă
  - [ ] Provider pentru istoric comenzi

### Faza 2: Implementarea Ecranelor de Bază (Săptămâna 1-2)

- [ ] Implementarea ecranului principal
  - [ ] Layout pentru butoanele de categorii
  - [ ] Navigare către ecranele corespunzătoare
- [ ] Implementarea ecranului de categorie
  - [ ] Listarea produselor
  - [ ] Funcționalitate de adăugare în comandă
- [ ] Implementarea ecranului de comandă
  - [ ] Afișarea produselor adăugate
  - [ ] Funcționalitate modificare cantitate
  - [ ] Selector cameră
  - [ ] Câmp pentru note
  - [ ] Salvare comandă
- [ ] Testarea fluxului de bază al aplicației
  - [ ] Adăugare produse în comandă
  - [ ] Finalizare comandă
  - [ ] Verificare salvare în baza de date

### Faza 3: Administrare și Raportare (Săptămâna 2-3)

- [ ] Implementarea ecranului de administrare meniu
  - [ ] Autentificare cu parolă
  - [ ] Managementul categoriilor
  - [ ] Managementul produselor
  - [ ] Reordonare și activare/dezactivare
- [ ] Implementarea ecranului de rapoarte
  - [ ] Filtre pentru dată și cameră
  - [ ] Vizualizarea comenzilor
  - [ ] Calcul total comenzi
- [ ] Integrarea generării PDF și a funcționalității de printare
  - [ ] Template pentru rapoarte
  - [ ] Generare PDF
  - [ ] Integrare cu imprimanta
- [ ] Implementarea funcționalității de partajare
  - [ ] Export PDF
  - [ ] Integrare cu WhatsApp

### Faza 4: Testare și Rafinare (Săptămâna 3)

- [ ] Testarea completă a aplicației
  - [ ] Testare pe tableta țintă
  - [ ] Verificare scenariu de utilizare completă
  - [ ] Testarea imprimării și exportului
- [ ] Optimizarea interfeței pentru utilizabilitate
  - [ ] Ajustarea dimensiunilor elementelor
  - [ ] Îmbunătățirea contrastului și lizibilității
  - [ ] Adăugare feedback vizual pentru acțiuni
- [ ] Verificarea performanței pe tableta țintă
  - [ ] Testare cu volume mari de date
  - [ ] Optimizare unde este necesar
- [ ] Rezolvarea bug-urilor identificate
  - [ ] Prioritizare și rezolvare bug-uri

## 7. Considerații Suplimentare

### Backup și Restaurare

- [ ] Funcționalitate pentru exportul bazei de date
- [ ] Funcționalitate pentru importul bazei de date
- [ ] Backup automat periodic al datelor

### Performanță

- [ ] Optimizări pentru tablete cu specificații medii/scăzute
- [ ] Gestionarea eficientă a memoriei pentru operare îndelungată
- [ ] Compresie imagini și resurse

### Utilizabilitate

- [ ] Butoane mari, ușor de apăsat
- [ ] Text clar și vizibil
- [ ] Feedback vizual pentru toate acțiunile
- [ ] Confirmare pentru acțiunile importante

### Extensibilitate

- [ ] Cod structurat pentru adăugarea facilă a unor funcționalități viitoare
- [ ] Documentație pentru dezvoltare ulterioară
- [ ] Posibilitatea de integrare cu un sistem POS în viitor

## 8. Lista de Verificare Finală pentru Lansare

- [ ] Toate funcționalitățile principale sunt implementate
- [ ] Baza de date funcționează corect
- [ ] Rapoartele se generează și se printează corect
- [ ] Interfața este optimizată pentru tableta țintă
- [ ] Aplicația funcționează fără erori
- [ ] Backup și restaurare funcționează
- [ ] Personalul pensiunii este instruit pentru utilizarea aplicației
- [ ] Documentația de utilizare este creată
- [ ] APK final este generat și instalat pe tableta destinație
