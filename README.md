# 🔐 Gestor Seguro de Credenciales SQL Server

## 👋 ¡Hola! Te doy la bienvenida a mi proyecto

Si alguna vez te pasó de tener que conectarte a múltiples bases de datos SQL Server y andar recordando usuarios, contraseñas, servidores... este proyecto es para vos. 

**¿El problema?** Gestionar credenciales de bases de datos es un quilombo. Las guardás en archivos de texto, las escribís en el código, o las tenés que estar ingresando cada vez. Es inseguro, tedioso y propenso a errores.

**¿La solución?** Un gestor de credenciales **super seguro** con encriptación AES-256, autenticación de dos factores (2FA), múltiples tipos de conexión, y una interfaz tanto gráfica como de línea de comandos. Todo encriptado, todo organizado, todo fácil de usar.

**¿Para quién?** Desarrolladores, DBAs, analistas de datos, o cualquiera que trabaje regularmente con SQL Server y quiera dejar de sufrir con las credenciales.

Este proyecto nació de mi propia frustración manejando conexiones a bases de datos en el trabajo. Empezó como un script simple y evolucionó a un sistema completo con todas las características de seguridad que necesitás en un entorno profesional.

---

## 📋 Índice

- [🎯 Descripción del Proyecto](#-descripción-del-proyecto)
- [⚡ Instalación Rápida](#-instalación-rápida)
- [🚀 Cómo Usar](#-cómo-usar)
- [✨ Características Principales](#-características-principales)
- [🛠️ Tecnologías Utilizadas](#️-tecnologías-utilizadas)
- [📁 Estructura del Proyecto](#-estructura-del-proyecto)
- [🤝 Contribuciones](#-contribuciones)
- [📜 Licencia](#-licencia)
- [🙏 Créditos y Agradecimientos](#-créditos-y-agradecimientos)
- [🚧 Estado Actual y Roadmap](#-estado-actual-y-roadmap)

---

## 🎯 Descripción del Proyecto

### ¿Qué hace exactamente?

El **Gestor Seguro de Credenciales SQL Server** es un sistema completo para almacenar, gestionar y usar credenciales de bases de datos de forma segura. Te permite:

- **Guardar credenciales encriptadas** con AES-256 y nunca más preocuparte por la seguridad
- **Conectarte a SQL Server** con un solo comando o click
- **Usar múltiples tipos de autenticación** (SQL, Windows, Certificados, JWT, SSH Tunnels)
- **Proteger con 2FA** tus conexiones más críticas
- **Automatizar scripts** con API keys seguras
- **Auditar todos los accesos** para compliance y seguridad

### ¿Para quién está pensado?

- **Desarrolladores** que se conectan a múltiples bases de datos
- **Administradores de bases de datos (DBAs)** que manejan muchos servidores
- **Analistas de datos** que acceden a diferentes ambientes (dev, test, prod)
- **Equipos de desarrollo** que necesitan compartir accesos de forma segura
- **Cualquier persona** que trabaje con SQL Server y valore la seguridad

### ¿Qué lo hace especial?

🔒 **Seguridad militar**: Encriptación AES-256 con PBKDF2 y 100,000 iteraciones
🎭 **Múltiples personalidades**: 5 tipos diferentes de autenticación
🛡️ **2FA incorporado**: Compatible con Google Authenticator
🔑 **API keys**: Para automatizar sin comprometer credenciales
📊 **Auditoría completa**: Registra todos los accesos
🎨 **Dos interfaces**: GUI amigable y CLI para scripts
🔄 **Pool de conexiones**: Optimización automática de recursos
⚡ **Reintentos inteligentes**: Manejo robusto de errores

---

## ⚡ Instalación Rápida

### Requisitos Previos

- **Python 3.8+** (recomiendo 3.10 o superior)
- **SQL Server** o **SQL Server Express** accesible
- **Windows, Linux o macOS** (testeado en todos)

### Paso 1: Clonar el Repositorio

```bash
git clone https://github.com/tu-usuario/gestor-credenciales-sql.git
cd gestor-credenciales-sql
```

### Paso 2: Instalar Dependencias

**Opción A - Instalación Básica (recomendada para empezar):**
```bash
pip install pyodbc cryptography
```

**Opción B - Instalación Completa (todas las características):**
```bash
pip install pyodbc cryptography pyotp qrcode[pil] sshtunnel psutil
```

**Opción C - Instalador Automático:**
```bash
python install_dependencies.py
```

### Paso 3: ¡Ejecutar!

**Interfaz Gráfica:**
```bash
python secure_credentials_manager.py
```

**Línea de Comandos:**
```bash
python secure_credentials_manager.py --cli
```

### Migración desde Versión Anterior

Si ya tenías una versión anterior del sistema:
```bash
python migrate_from_old.py
```

---

## 🚀 Cómo Usar

### Primera Vez - Configuración Inicial

1. **Ejecutá el programa:**
   ```bash
   python secure_credentials_manager.py
   ```

2. **Creá tu contraseña maestra** - Esta contraseña protege todas tus credenciales
3. **Agregá tu primer servidor** usando el botón "➕ Nuevo Servidor"
4. **¡Probá la conexión!** con el botón "🔌 Probar Conexión"

### Uso Cotidiano - Interfaz Gráfica

#### Gestionar Servidores
- **Agregar:** Botón "➕ Nuevo Servidor"
- **Editar:** Seleccioná un servidor y usá "✏️ Editar"
- **Eliminar:** Seleccioná y usá "🗑️ Eliminar"
- **Probar:** "🔌 Probar Conexión" para verificar que funcione

#### Características Avanzadas
- **🔐 2FA:** Botón "🔐 Configurar 2FA" - Genera QR para Google Authenticator
- **🔑 API Keys:** "🔑 Gestionar API Keys" para crear claves de automatización
- **💾 Backup:** "💾 Backup" para guardar tus credenciales
- **📄 Ejemplos:** "📄 Ver Código de Ejemplo" te muestra cómo usar en scripts

### Uso Cotidiano - Línea de Comandos

```bash
# Listar todos los servidores
python -m sql_credentials_system.cli list

# Agregar un nuevo servidor
python -m sql_credentials_system.cli add MiServidor

# Probar conexión
python -m sql_credentials_system.cli test MiServidor

# Ejecutar una consulta
python -m sql_credentials_system.cli query MiServidor "SELECT @@VERSION"

# Crear API key para scripts
python -m sql_credentials_system.cli apikeys create MiScript MiServidor

# Configurar 2FA
python -m sql_credentials_system.cli 2fa setup MiServidor
```

### Uso en Tus Scripts - API Simple

```python
from db_connector import connect_to_sql

# Conexión súper simple
conn = connect_to_sql('MiServidor')
cursor = conn.cursor()
cursor.execute("SELECT TOP 10 * FROM MiTabla")
resultados = cursor.fetchall()
conn.close()

# Con 2FA
conn = connect_to_sql('MiServidor', totp_code='123456')

# Con API Key (para scripts automatizados)
conn = connect_to_sql('MiServidor', api_key='sqlcred_tu_key_aqui')
```

### Tipos de Autenticación Soportados

1. **SQL Authentication** - Usuario y contraseña tradicional
2. **Windows Authentication** - Usa tu usuario de Windows
3. **Certificate Authentication** - Autenticación con certificados .pfx
4. **JWT/OAuth** - Para ambientes modernos con tokens
5. **SSH Tunnel** - Conexión a través de túnel SSH seguro

---

## ✨ Características Principales

### 🔒 Seguridad de Nivel Empresarial
- **Encriptación AES-256-CBC** con PBKDF2 y 100,000 iteraciones
- **Contraseña maestra** para proteger todas las credenciales
- **Salts únicos** para cada instalación
- **Nunca almacena credenciales en texto plano**

### 🛡️ Autenticación de Dos Factores (2FA)
- **Compatible con Google Authenticator**, Authy, y similares
- **Códigos QR** para configuración fácil
- **Protección adicional** para servidores críticos
- **Verificación de tiempo** con ventana de tolerancia

### 🔑 Sistema de API Keys
- **Automatización segura** sin exponer credenciales
- **Expiración configurable** para mayor seguridad
- **Revocación inmediata** cuando sea necesario
- **Auditoría completa** de uso

### 🎨 Dos Interfaces, Mismo Poder
- **GUI intuitiva** para uso diario
- **CLI completa** para scripts y automatización
- **API simple** para integrar en tus proyectos
- **Misma funcionalidad** en ambas

### 📊 Auditoría y Monitoreo
- **Registro completo** de todos los accesos
- **Timestamps precisos** de cada conexión
- **Logs estructurados** para análisis
- **Cumplimiento** de políticas de seguridad

### ⚡ Optimización de Rendimiento
- **Pool de conexiones** para reutilización eficiente
- **Reintentos automáticos** con backoff exponencial
- **Circuit breaker** para servicios que fallan
- **Timeouts configurables** para cada servidor

### 💾 Backup y Recuperación
- **Backups encriptados** de todas las configuraciones
- **Restauración completa** de credenciales
- **Exportación selectiva** de servidores específicos
- **Migración** entre instalaciones

---

## 🛠️ Tecnologías Utilizadas

### Lenguajes de Programación
- **Python 3.8+** - Lenguaje principal
- **SQL** - Para consultas de prueba y validación

### Librerías de Seguridad
- **cryptography** - Encriptación AES-256 y funciones criptográficas
- **pyotp** - Implementación de TOTP para 2FA
- **hashlib** - Hashing seguro de contraseñas

### Conectividad de Bases de Datos
- **pyodbc** - Conexión nativa a SQL Server
- **sshtunnel** - Túneles SSH para conexiones seguras

### Interfaz de Usuario
- **tkinter** - Interfaz gráfica nativa de Python
- **argparse** - CLI robusta con subcomandos
- **qrcode** - Generación de códigos QR para 2FA

### Herramientas de Desarrollo
- **pathlib** - Manejo moderno de archivos y rutas
- **json** - Serialización de configuraciones
- **logging** - Sistema de logs estructurado
- **datetime** - Manejo de timestamps y expiración

### Arquitectura y Patrones
- **Modular** - Separación clara de responsabilidades
- **Provider Pattern** - Para diferentes tipos de autenticación
- **Pool Pattern** - Para optimización de conexiones
- **Observer Pattern** - Para auditoría y logging

---

## 📁 Estructura del Proyecto

```
gestor-credenciales-sql/
├── 📄 secure_credentials_manager.py    # Entry point principal
├── 📄 db_connector.py                  # API simple para scripts
├── 📄 install_dependencies.py         # Instalador automático
├── 📄 migrate_from_old.py             # Migrador de versiones anteriores
├── 📁 sql_credentials_system/         # Sistema modular principal
│   ├── 📁 core/                       # Componentes centrales
│   │   ├── 📄 crypto.py               # Encriptación AES-256
│   │   ├── 📄 storage.py              # Almacenamiento seguro
│   │   ├── 📄 config.py               # Configuraciones globales
│   │   └── 📄 exceptions.py           # Excepciones personalizadas
│   ├── 📁 auth_providers/             # Tipos de autenticación
│   │   ├── 📄 base_provider.py        # Clase base y registro
│   │   ├── 📄 sql_provider.py         # SQL Authentication
│   │   ├── 📄 windows_provider.py     # Windows Auth
│   │   ├── 📄 certificate_provider.py # Certificados
│   │   ├── 📄 jwt_provider.py         # JWT/OAuth
│   │   └── 📄 ssh_tunnel_provider.py  # SSH Tunnels
│   ├── 📁 security/                   # Componentes de seguridad
│   │   ├── 📄 totp_manager.py         # 2FA/TOTP
│   │   ├── 📄 api_key_manager.py      # Gestión de API keys
│   │   └── 📄 audit_logger.py         # Logging de auditoría
│   ├── 📁 database/                   # Conectividad avanzada
│   │   ├── 📄 connector.py            # Conector principal
│   │   ├── 📄 connection_pool.py      # Pool de conexiones
│   │   └── 📄 retry_handler.py        # Reintentos y circuit breaker
│   ├── 📁 gui/                        # Interfaz gráfica
│   │   ├── 📄 main_window.py          # Ventana principal
│   │   └── 📁 dialogs/                # Diálogos específicos
│   ├── 📁 backup/                     # Sistema de backup
│   ├── 📁 utils/                      # Utilidades
│   ├── 📄 cli.py                      # Interfaz de línea de comandos
│   └── 📄 requirements.txt            # Dependencias
├── 📄 README.md                       # Este archivo
├── 📄 LICENSE                         # Licencia MIT
└── 📁 docs/                          # Documentación adicional
```

### Componentes Técnicos Principales

#### 🏗️ Core (Núcleo)
- **crypto.py**: Maneja toda la encriptación AES-256 con PBKDF2
- **storage.py**: Almacenamiento seguro de credenciales encriptadas
- **config.py**: Configuraciones globales del sistema
- **exceptions.py**: Excepciones personalizadas para mejor debugging

#### 🔐 Auth Providers (Proveedores de Autenticación)
- **base_provider.py**: Clase abstracta y registry pattern para extensibilidad
- **sql_provider.py**: Autenticación SQL Server tradicional
- **windows_provider.py**: Integrated Security de Windows
- **certificate_provider.py**: Autenticación con certificados digitales
- **jwt_provider.py**: Tokens JWT/OAuth para ambientes modernos
- **ssh_tunnel_provider.py**: Conexiones a través de túnel SSH

#### 🛡️ Security (Seguridad)
- **totp_manager.py**: Implementación completa de 2FA/TOTP
- **api_key_manager.py**: Gestión de claves para automatización
- **audit_logger.py**: Logging estructurado para compliance

#### 🗄️ Database (Base de Datos)
- **connector.py**: Conector principal con soporte para todos los auth types
- **connection_pool.py**: Pool inteligente para optimización de recursos
- **retry_handler.py**: Reintentos automáticos y circuit breaker pattern

---

## 🤝 Contribuciones

¡Me encantaría que contribuyas al proyecto! Toda ayuda es bienvenida, desde reportar bugs hasta agregar nuevas características.

### ¿Cómo Contribuir?

1. **Fork** el repositorio
2. **Creá** una rama para tu feature: `git checkout -b feature/nueva-caracteristica`
3. **Implementá** tus cambios
4. **Testeá** que todo funcione correctamente
5. **Commitea** tus cambios: `git commit -m 'Agrega nueva característica'`
6. **Push** a la rama: `git push origin feature/nueva-caracteristica`
7. **Abrí** un Pull Request

### Guía de Estilo

- **Código en español** para comentarios y variables cuando sea apropiado
- **Docstrings en español** para funciones y clases
- **PEP 8** para el estilo de código Python
- **Type hints** cuando sea posible
- **Tests** para nuevas funcionalidades

### Ideas para Contribuir

- 🆕 **Nuevos auth providers** (LDAP, Active Directory, etc.)
- 🎨 **Mejoras en la GUI** (temas, iconos, UX)
- 🔧 **Optimizaciones** de rendimiento
- 📚 **Documentación** y ejemplos
- 🐛 **Reportar bugs** o issues
- 🌐 **Soporte para otros SGBD** (MySQL, PostgreSQL)

### Código de Conducta

- **Respeto** por todos los contribuidores
- **Construcción colaborativa** de ideas
- **Feedback constructivo** en reviews
- **Inclusión** de diferentes perspectivas y enfoques

---

## 📜 Licencia

Este proyecto está licenciado bajo la **Licencia MIT** - mirá el archivo [LICENSE](LICENSE) para detalles completos.

### ¿Qué significa esto?

- ✅ **Uso comercial** permitido
- ✅ **Modificación** permitida
- ✅ **Distribución** permitida
- ✅ **Uso privado** permitido
- ❗ **Sin garantía** (uso bajo tu propio riesgo)
- ❗ **Incluir licencia** en distribuciones

### En Resumen

Podés usar este código en cualquier proyecto, modificarlo, venderlo, o lo que se te ocurra. Solo tenés que incluir la licencia original y no me hacés responsable si algo sale mal.

---

## 🙏 Créditos y Agradecimientos

### Inteligencias Artificiales que Ayudaron

Este proyecto fue desarrollado con la invaluable asistencia de:

- **🤖 Claude (Anthropic)** - Por el diseño de arquitectura, debugging, y mejores prácticas de seguridad
- **🧠 GitHub Copilot** - Por acelerar el desarrollo con autocompletado inteligente
- **💎 Gemini (Google)** - Por ideas de optimización y review de código

*Sin la ayuda de estas IAs, este proyecto habría tomado mucho más tiempo y no tendría el nivel de pulimiento que tiene hoy.*

### Recursos y Referencias

- **Microsoft ODBC Documentation** - Para implementación correcta de conexiones SQL Server
- **OWASP Guidelines** - Para mejores prácticas de seguridad
- **RFC 6238 (TOTP)** - Para implementación estándar de 2FA
- **Python Cryptography Documentation** - Para encriptación segura

### Comunidad

- **Stack Overflow** - Por resolver mil dudas durante el desarrollo
- **Reddit r/Python** - Por feedback y sugerencias de la comunidad
- **GitHub** - Por la plataforma que hace posible la colaboración

### Testers Beta

Gracias a todos los que probaron versiones tempranas y reportaron bugs:
- Los colegas de trabajo que aguantaron las versiones buggeadas
- La comunidad de developers que dio feedback constructivo

---

## 🚧 Estado Actual y Roadmap

### 📍 Estado Actual: **v3.0 - Estable**

El proyecto está en un estado **maduro y usable** para producción. Todas las características principales están implementadas y testeadas.

#### ✅ Completado en v3.0
- ✅ Sistema de encriptación AES-256 robusto
- ✅ 5 tipos de autenticación completos
- ✅ 2FA/TOTP con QR codes
- ✅ API keys con expiración
- ✅ GUI completa y funcional
- ✅ CLI con todos los comandos
- ✅ Sistema de backup/restore
- ✅ Auditoría y logging
- ✅ Connection pooling
- ✅ Migración desde versión anterior
- ✅ Documentación completa

### 🚀 Roadmap - Próximas Versiones

#### 📋 v3.1 - Mejoras de UX (Q1 2024)
- [ ] 🎨 **Temas visuales** para la GUI (dark/light mode)
- [ ] 📊 **Dashboard** con estadísticas de uso
- [ ] 🔍 **Búsqueda y filtrado** de servidores
- [ ] 📱 **GUI responsive** para diferentes tamaños de pantalla
- [ ] 🚀 **Auto-updates** del sistema

#### 📋 v3.2 - Extensibilidad (Q2 2024)
- [ ] 🔌 **Sistema de plugins** para auth providers personalizados
- [ ] 🌐 **Soporte multi-SGBD** (MySQL, PostgreSQL, Oracle)
- [ ] 📡 **API REST** para integraciones externas
- [ ] 🐳 **Docker containers** para deployment fácil
- [ ] ☁️ **Sync en la nube** (opcional y encriptado)

#### 📋 v3.3 - Enterprise Features (Q3 2024)
- [ ] 👥 **Multi-user** con roles y permisos
- [ ] 🏢 **Integration con Active Directory**
- [ ] 📈 **Métricas avanzadas** y reportes
- [ ] 🔔 **Alertas** de seguridad automáticas
- [ ] 🛡️ **Hardware security modules** (HSM) support

#### 📋 v4.0 - Nueva Arquitectura (Q4 2024)
- [ ] ⚡ **Reescritura en async/await** para mejor performance
- [ ] 🌊 **Streaming** de resultados para queries grandes
- [ ] 🧠 **Machine learning** para detección de anomalías
- [ ] 📱 **App mobile** companion
- [ ] 🌍 **Soporte completo i18n** (múltiples idiomas)

### 🐛 Issues Conocidos

#### 🔧 Menores
- En algunos sistemas Windows más viejos, la instalación de `cryptography` puede requerir Visual C++ Redistributable
- La GUI puede verse pixelada en pantallas con DPI muy alto
- El SSH tunnel provider requiere instalación manual de `sshtunnel`

#### 📝 Mejoras Planeadas
- Implementar auto-retry en GUI cuando falla una conexión
- Agregar shortcuts de teclado para acciones comunes
- Mejorar mensajes de error para ser más específicos

### 💡 Ideas Futuras

¿Tenés ideas para el proyecto? ¡Abrime un issue con la tag "enhancement"!

Algunas ideas que estoy considerando:
- **Plugin para VS Code** para conectar directo desde el editor
- **Integration con GitHub Actions** para CI/CD con bases de datos
- **Modo portable** para usar desde USB sin instalación
- **Web UI** para acceso remoto seguro
- **Integration con HashiCorp Vault** para environments enterprise

---

### 📞 Contacto y Soporte

- **🐛 Bugs:** [Abrí un issue](https://github.com/tu-usuario/gestor-credenciales-sql/issues)
- **💡 Feature requests:** [Discusiones](https://github.com/tu-usuario/gestor-credenciales-sql/discussions)
- **📖 Documentación:** Mirá la carpeta `docs/` para más detalles
- **❓ Preguntas:** Usá las [GitHub Discussions](https://github.com/tu-usuario/gestor-credenciales-sql/discussions)

---

**¡Gracias por usar el Gestor Seguro de Credenciales SQL Server!** 🎉

Si te resulta útil, no te olvides de dejarle una ⭐ al repositorio - ¡me ayuda muchísimo!

---

*Última actualización: Octubre 2024 | Versión 3.0*
