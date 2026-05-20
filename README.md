<div align="center">

# ControlCash

**ControlCash** es una aplicación iOS para gestionar finanzas personales, registrar ingresos y gastos, consultar el saldo disponible y visualizar reportes mediante gráficas claras e intuitivas.

![Swift](https://img.shields.io/badge/Swift-5.0-orange?logo=swift&logoColor=white)
![SwiftUI](https://img.shields.io/badge/SwiftUI-UI-blue?logo=swift&logoColor=white)
![iOS](https://img.shields.io/badge/iOS-18%2B-lightgrey?logo=apple)
![CoreData](https://img.shields.io/badge/Core%20Data-Persistence-0A84FF)
![Status](https://img.shields.io/badge/status-en%20desarrollo-yellow)
![License](https://img.shields.io/badge/license-no%20definida-lightgrey)

</div>

---

## Descripción

ControlCash permite llevar un control básico de movimientos financieros personales desde una app móvil. El usuario puede crear una cuenta, iniciar sesión, registrar ingresos o gastos por categoría, consultar su saldo total y revisar reportes visuales por día, mes o año.

Además, el proyecto incluye un módulo de **Market Exchange** que muestra información de acciones como precio actual, porcentaje de variación y una gráfica de comportamiento reciente.

> **Nota:** La sección de mercado financiero tiene fines informativos y de aprendizaje. No representa asesoría financiera.

---

## Características principales

- Registro e inicio de sesión de usuarios.
- Persistencia local de usuarios con Core Data.
- Panel principal con saludo personalizado y saldo total.
- Registro de movimientos como ingresos o gastos.
- Categorías para clasificar movimientos:
  - Ingreso
  - Deudas
  - Entretenimiento
  - Comida
  - Transporte
- Formato monetario en pesos mexicanos (`MXN`).
- Lista de movimientos ordenados por fecha.
- Gráfica tipo dona para visualizar gastos por categoría.
- Reportes filtrados por día, mes o año.
- Gráfica de barras para analizar movimientos financieros.
- Sección de acciones con watchlist inicial.
- Consumo de datos financieros externos mediante API.
- Interfaz construida con SwiftUI.

---

## Capturas de pantalla

Agrega tus capturas en una carpeta como `docs/screenshots/` y reemplaza los placeholders:

| Login | Inicio | Reportes | Market Exchange |
|---|---|---|---|
| ![Login](docs/screenshots/login.png) | ![Home](docs/screenshots/home.png) | ![Reportes](docs/screenshots/reportes.png) | ![Market Exchange](docs/screenshots/market.png) |

---

## Tecnologías utilizadas

- **Swift 5**
- **SwiftUI**
- **Core Data**
- **Charts**
- **Combine**
- **URLSession**
- **Xcode**
- **Finnhub API** para datos financieros
- **Clearbit Logo API** para logos de compañías

---

## Estructura del proyecto

```text
ControlCash/
├── appFinanzas.xcodeproj/              # Proyecto de Xcode
├── appFinanzas/
│   ├── Assets.xcassets/                # Assets de la app
│   ├── ContentView.swift               # Vistas principales y navegación
│   ├── Persistence.swift               # Configuración de Core Data
│   ├── appFinanzasApp.swift            # Punto de entrada de la app
│   ├── Helpers/
│   │   ├── Extensions.swift            # Extensiones de colores y utilidades
│   │   ├── JSONDecoders.swift          # Modelos para respuestas JSON
│   │   ├── StockModel.swift            # Modelo de acciones
│   │   └── generadorDePrueba.swift     # Datos de prueba para reportes
│   ├── MarketExchangeViews/
│   │   ├── Requests/APIRequest.swift   # Cliente para consumir datos financieros
│   │   ├── ViewModel/StocksViewModel.swift
│   │   ├── HeaderView.swift
│   │   ├── LineChart.swift
│   │   ├── PortfolioCard.swift
│   │   ├── SearchStockView.swift
│   │   ├── StockCard.swift
│   │   ├── StockCell.swift
│   │   └── WatchlistView.swift
│   ├── ReportesView/
│   │   └── HeaderReportes.swift
│   └── appFinanzas.xcdatamodeld/        # Modelo de Core Data
├── StockMockData.swift                  # Datos mock para gráficas de acciones
└── README.md
```

---

## Requisitos

- macOS con Xcode instalado.
- Xcode compatible con iOS 18 o superior.
- iOS 18+ como deployment target del proyecto.
- Conexión a internet para consultar datos de acciones.
- Cuenta de desarrollador o equipo configurado en Xcode si deseas ejecutar en dispositivo físico.

---

## Instalación y ejecución

1. Clona el repositorio:

```bash
git clone https://github.com/Gerryyyy4/ControlCash.git
```

2. Entra a la carpeta del proyecto:

```bash
cd ControlCash
```

3. Abre el proyecto en Xcode:

```bash
open appFinanzas.xcodeproj
```

4. Selecciona un simulador o dispositivo físico.

5. Ejecuta la app con:

```text
Cmd + R
```

---

## Configuración de API

El módulo **Market Exchange** utiliza una API externa para obtener información de acciones.

Actualmente, el cliente de API se encuentra en:

```text
appFinanzas/MarketExchangeViews/Requests/APIRequest.swift
```

Para un entorno profesional, se recomienda **no guardar tokens directamente en el código fuente**. Una alternativa más segura es mover el token a un archivo de configuración local ignorado por Git, por ejemplo:

```text
Config.xcconfig
```

Ejemplo recomendado:

```text
FINNHUB_API_TOKEN=tu_token_aqui
```

Y agregar el archivo al `.gitignore`:

```gitignore
Config.xcconfig
```

---

## Uso de la aplicación

1. Abre la app.
2. Crea una cuenta desde la pantalla de registro.
3. Inicia sesión con tu usuario.
4. Consulta tu saldo en la pantalla principal.
5. Agrega ingresos o gastos desde la pestaña **Ingresos/Gastos**.
6. Revisa reportes financieros desde la pestaña **Reportes**.
7. Consulta información de acciones desde **Market Exchange**.
8. Cierra sesión desde la configuración de usuario.

---

## Modelo de datos

El proyecto utiliza Core Data para almacenar información local. El modelo actual incluye:

| Entidad | Campos |
|---|---|
| `Usuario` | `username`, `password` |
| `Item` | `timestamp` |

Los movimientos financieros se manejan actualmente mediante un `ObservableObject` (`MovimientosStore`) con datos iniciales en memoria. Como mejora futura, se puede crear una entidad `Movimiento` en Core Data para conservar los movimientos después de cerrar la app.

---

## Estado actual del proyecto

Funcionalidades implementadas:

- Navegación principal con `TabView`.
- Login y registro local.
- Dashboard con saldo total.
- Registro de movimientos.
- Reportes por intervalo de tiempo.
- Gráficas con Swift Charts.
- Watchlist inicial de acciones (`AAPL`, `NVDA`, `NFLX`).
- Consumo de datos financieros mediante `URLSession`.

Limitaciones actuales:

- Los movimientos financieros no se persisten todavía en Core Data.
- Las contraseñas se almacenan como texto plano; para producción se recomienda hashing seguro.
- La búsqueda de acciones muestra ejemplos estáticos y puede conectarse dinámicamente al endpoint de búsqueda.
- Los botones de depósito y retiro están preparados visualmente, pero aún no tienen lógica implementada.

---

## Roadmap

- [ ] Persistir movimientos financieros en Core Data.
- [ ] Crear entidad `Movimiento` con monto, categoría, referencia, fecha y usuario.
- [ ] Asociar movimientos al usuario autenticado.
- [ ] Mover el token de API a configuración segura.
- [ ] Implementar búsqueda real de acciones desde la interfaz.
- [ ] Agregar lógica para depósito y retiro en el módulo de portafolio.
- [ ] Mejorar seguridad del login con hashing de contraseñas.
- [ ] Agregar validaciones más completas en formularios.

---


## Contribución

Las contribuciones son bienvenidas. Puedes proponer mejoras mediante issues o pull requests.

1. Haz un fork del repositorio.
2. Crea una rama para tu cambio:

```bash
git checkout -b feature/nueva-funcionalidad
```

3. Realiza tus cambios y crea un commit:

```bash
git commit -m "feat: add new feature"
```

4. Sube la rama:

```bash
git push origin feature/nueva-funcionalidad
```

5. Abre un Pull Request.

---


## Autor

Desarrollado por [Gerryyyy4](https://github.com/Gerryyyy4).

---

<div align="center">

Hecho con SwiftUI para facilitar el control de finanzas personales.

</div>
