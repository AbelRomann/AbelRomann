Eres un desarrollador senior de React Native. Voy a construir una app móvil de gastos personales llamada [NOMBRE DE TU APP]. Necesito que me guíes paso a paso para completar la Fase 1 del proyecto.

## Stack definido
- React Native con Expo SDK (managed workflow)
- TypeScript estricto
- Expo Router (navegación file-based)
- expo-sqlite para base de datos local
- NativeWind para estilos (Tailwind en React Native)
- Zustand para estado global
- React Native Paper para componentes UI

## Lo que debe quedar listo al final de la Fase 1

### 1. Setup del proyecto
- Proyecto creado con: npx create-expo-app@latest --template
- TypeScript configurado correctamente
- NativeWind instalado y funcionando
- Estructura de carpetas organizada así:
  /app         → pantallas (Expo Router)
  /components  → componentes reutilizables
  /store       → estado global con Zustand
  /db          → lógica de base de datos SQLite
  /types       → interfaces y tipos TypeScript
  /constants   → colores, categorías, constantes

### 2. Base de datos SQLite
Crea el esquema completo con estas tablas:

transactions:
- id (INTEGER PRIMARY KEY AUTOINCREMENT)
- type (TEXT: 'income' | 'expense')
- amount (REAL)
- category_id (INTEGER FK)
- date (TEXT ISO 8601)
- description (TEXT nullable)
- payment_method (TEXT: 'cash' | 'card' | 'transfer' | 'other')
- created_at (TEXT)

categories:
- id (INTEGER PRIMARY KEY AUTOINCREMENT)
- name (TEXT)
- type (TEXT: 'income' | 'expense')
- icon (TEXT emoji)
- color (TEXT hex)

budgets:
- id (INTEGER PRIMARY KEY AUTOINCREMENT)
- category_id (INTEGER FK)
- amount (REAL)
- month (TEXT YYYY-MM)

savings_goals:
- id (INTEGER PRIMARY KEY AUTOINCREMENT)
- name (TEXT)
- target_amount (REAL)
- current_amount (REAL)
- deadline (TEXT nullable)
- created_at (TEXT)

Incluye también las categorías precargadas al inicializar la DB:

Gastos: Comida 🍔, Transporte 🚗, Servicios 💡, Entretenimiento 🎬, Salud 🏥, Compras 🛍️, Educación 📚, Hogar 🏠, Otros 📦

Ingresos: Salario 💼, Freelance 💻, Negocio 🏪, Regalo 🎁, Otros 💰

### 3. Tipos TypeScript
Define las interfaces completas para: Transaction, Category, Budget, SavingsGoal, PaymentMethod, TransactionType

### 4. Funciones CRUD de la DB
Para transactions necesito estas funciones:
- getAll(filters?: {type?, category_id?, month?, search?})
- getById(id)
- create(data)
- update(id, data)
- remove(id)
- getSummaryByMonth(month: string) → { totalIncome, totalExpense, balance }
- getExpensesByCategory(month: string) → agrupado por categoría

### 5. Estado global con Zustand
Store principal con:
- Lista de transacciones
- Transacción seleccionada
- Filtros activos
- Acciones: loadTransactions, addTransaction, updateTransaction, deleteTransaction

### 6. Navegación con Expo Router
Crea la estructura de rutas para estas pantallas (sin implementar el contenido aún, solo los archivos con un placeholder):
- / → Home / Dashboard
- /add-transaction → Formulario agregar
- /history → Historial
- /budgets → Presupuestos
- /reports → Reportes / Gráficas
- /settings → Ajustes

Incluye un tab bar en la parte inferior con íconos para: Home, Agregar, Historial, Reportes, Ajustes

### 7. Pantalla de Splash + tema base
- Splash screen configurada con expo-splash-screen
- Colores base del tema definidos en constants/colors.ts
- Soporte para modo oscuro con useColorScheme

## Instrucciones adicionales
- Todo el código en TypeScript estricto, sin usar 'any'
- Manejo de errores con try/catch en todas las operaciones de DB
- Comentarios en español donde sea útil
- Dame los comandos de instalación exactos antes del código
- Si hay algo que pueda romperse fácilmente, avísame antes de implementarlo

Empieza por el setup y la estructura de carpetas, luego continúa con la base de datos, y al final la navegación. Dame el código completo de cada archivo, no resúmenes.
