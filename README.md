# Restaurante App - Gestión de Ventas y Manejo de Eventos (Semana 15)

# Propósito de la Semana 15

El propósito principal de esta actividad es comprender e implementar los fundamentos del manejo de eventos en aplicaciones de escritorio con Tkinter. Mediante un caso práctico de registro de ventas, se demuestra cómo las acciones del usuario activan controladores (callbacks) que coordinan la lógica del sistema sin saturar la interfaz gráfica ni perder la separación de responsabilidades.

# Evolución Realizada sobre el Proyecto Anterior

A partir de la versión del proyecto desarrollada en la Semana 14 (restaurante_app), se realizaron las siguientes mejoras evolutivas:

Adaptación de Dominio: Se adaptó la plantilla base docente del dominio de "biblioteca" al dominio propio del restaurante (reemplazando conceptos de libros/préstamos por productos/ventas).

Incorporación del Módulo de Ventas: Se integró una nueva sección en la interfaz gráfica para relacionar un usuario con un producto mediante componentes ttk.Combobox.

Integración Visual: Se incorporó el uso obligatorio de la carpeta assets/ para organizar íconos (assets/icons/) y el logo del sistema (assets/logo/).

# Estructura del Sistema

El proyecto mantiene una arquitectura modular orientada a objetos dividida en datos, modelos, servicios e interfaz gráfica:

```text
restaurante_app/
│
├── assets/                  # Recursos visuales (obligatorio)
│   ├── icons/              # Íconos para la interfaz
│   └── logo/               # Logotipo de la aplicación
│
├── datos/                   # Archivos de persistencia JSON
│   ├── productos.json      # Catálogo de productos del restaurante
│   ├── usuarios.json       # Registro de usuarios/clientes
│   └── ventas.json         # Historial de ventas realizadas
│
├── modelos/                 # Clases de dominio
│   ├── __init__.py
│   ├── producto.py
│   ├── usuario.py
│   └── venta.py            # Entidad Venta (id, usuario, producto, fecha)
│
├── servicios/               # Capa de lógica de negocio y persistencia
│   ├── __init__.py
│   ├── archivo_servicio.py
│   └── restaurante_servicio.py    # Gestión de operaciones y validaciones
│
├── ui/                      # Capa de Interfaz Gráfica
│   ├── __init__.py
│   ├── login_view.py
│   └── main_view.py        # Vista principal con formulario y Treeview de ventas
│
├── main.py                  # Punto de entrada de la aplicación
└── README.md                # Documentación del proyecto
```



# Nueva Gestión de Ventas

La nueva sección de ventas permite seleccionar un usuario registrado y un producto disponible. Al accionar el registro:

Se valida que los campos de selección no estén vacíos.

Se instancia la entidad Venta con un ID autoincremental y la fecha/hora actual.

Se actualiza la vista inmediatamente reflejando la transacción en una tabla ttk.Treeview.

# Uso de command= y Callbacks

El flujo de eventos sigue estrictamente el patrón desacoplado:

Acción del usuario: El usuario presiona el botón Registrar Venta.

Disparo mediante command=: El botón en main_view.py está configurado con command=self.on_registrar_venta_click.

Ejecución del Callback: El método callback on_registrar_venta_click() captura los datos seleccionados de los combos en la UI.

Delegación a Servicio: El callback solicita la operación a RestauranteServicio.registrar_venta(), garantizando que la UI no contenga lógica de negocio.

Respuesta Visual: El callback recibe la respuesta del servicio, limpia el formulario, refresca la tabla Treeview y muestra un mensaje de éxito (messagebox).

# Persistencia en ventas.json

Toda venta registrada exitosamente es delegada a la clase RestauranteServicio, la cual procesa la información y la guarda de forma permanente en el archivo datos/ventas.json. Al reiniciar la aplicación, las ventas previas son leídas automáticamente desde este archivo JSON para garantizar la continuidad de los datos.

# Pasos Necesarios para Ejecutar main.py

Requisitos previos:

Tener instalado Python 3.8 o superior.

Asegurarse de que el entorno cuente con el módulo tkinter habilitado.

Clonar o descargar el proyecto:
Asegúrate de mantener intacta la estructura de carpetas descrita arriba.

Ejecución desde la terminal:
Abre una consola o terminal en la carpeta raíz del proyecto (restaurante_app/) y ejecuta el siguiente comando:

python main.py

