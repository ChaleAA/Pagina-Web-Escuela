# Guía Paso a Paso: Integración Chul Hak San 🥋

Esta guía detalla las modificaciones y pasos tomados para replicar, integrar y hacer funcional el prototipo web de **Chul Hak San**.

## 1. Modificaciones Realizadas (Paso a Paso)

Los archivos originales se encontraban aislados en carpetas separadas (como `login_chul_hak_san`, `p_gina_de_inicio`, etc.), cada uno con un archivo `code.html`. El primer paso fue unificar todos estos archivos HTML en una sola raíz del proyecto llamada `ChulHakSan-Web` y nombrarlos semánticamente.

Las equivalencias de archivos son:
- `login_chul_hak_san/code.html` -> `login.html`
- `p_gina_de_inicio/code.html` -> `index.html` (El inicio principal)
- `panel_consolidado_alumno/code.html` -> `student.html`
- `panel_consolidado_instructor/code.html` -> `instructor.html`
- `panel_de_administraci_n/code.html` -> `admin.html`

### 2. Base de Datos y Sistema de Registro

Se implementó un sistema completo de **Inicio de Sesión (Login)** y **Registro** utilizando `localStorage` de JavaScript, permitiendo que la aplicación funcione localmente (directamente en tu navegador) sin necesidad de configurar un servidor o backend externo.

- **Base de Datos Simulada**: Los usuarios se guardan en el navegador bajo la clave `chulhaksan_users_db`. Hemos generado **90 usuarios iniciales** (30 administradores, 30 estudiantes y 30 instructores) que se cargan a través del archivo `database.js`. También puedes ver la estructura en bruto abriendo el archivo [users_db.json](file:///C:/Users/Usuario/.gemini/antigravity/scratch/ChulHakSan-Web/users_db.json).
- **Registro**: Se agregó un formulario oculto en la página de login. Si un usuario no tiene cuenta, puede alternar a este formulario ("Register here"), elegir un rol (Estudiante, Instructor, Administrador), y crear su usuario.
- **Validación Avanzada en el Login**: 
  - Si intentas ingresar con un usuario que no existe, aparece una alerta roja indicando: *"Account not found. You don't have an account, please register first."*
  - Si los datos son correctos, el sistema te redirigirá a la pantalla correcta dependiendo de tu rol registrado (por ejemplo, Admin va a `admin.html`, Instructor a `instructor.html`, Estudiante a `student.html`).

Para probarlo, hay cuentas creadas por defecto generadas para todas las categorías:
- **Admin**: `admin1` a `admin30` (Contraseña: `adminpass1`, etc.)
- **Student**: `student1` a `student30` (Contraseña: `studentpass1`, etc.)
- **Instructor**: `instructor1` a `instructor30` (Contraseña: `instructorpass1`, etc.)

### 3. Cómo se Enlazaron las Páginas Interiores (Linkeo)

Para convertir los diseños estáticos en un prototipo navegable:
1. **Navegación Inferior (Barra Móvil / Global)**:
   - Se actualizó la barra `<nav class="fixed bottom-0...">` en `index.html`, `student.html`, `instructor.html` y `admin.html`.
   - **Ícono 'Home'**: `href="index.html"`
   - **Ícono 'Training'**: `href="student.html"`
   - **Ícono 'Admin'**: `href="admin.html"`
   - **Ícono 'Profile'**: `href="instructor.html"`

2. **Barras Laterales y Cabeceras**:
   - En el panel de instructor (`instructor.html`) y admin (`admin.html`), los menús laterales de escritorio ("Quick Links") también fueron actualizados para apuntar a los archivos funcionales.

### 4. Cómo Ejecutar y Llevar este Proyecto a la Realidad

Este prototipo usa **HTML, Tailwind CSS (vía CDN) y JavaScript frontal** para la autenticación local.

#### Para probarlo ahora mismo de forma local:
1. Navega usando el Explorador de Windows hasta: `C:\Users\Usuario\.gemini\antigravity\scratch\ChulHakSan-Web\`
2. Haz **doble clic** en el archivo `login.html`.
3. Prueba iniciar sesión con los datos por defecto o crear una nueva cuenta interactuando con el sistema de registro. Observa los mensajes de validación y la redirección automática según roles.

#### Para expandirlo a Producción (Futuro):
El día que quieras llevar este prototipo a una web global con miles de usuarios, puedes tomar estas exactas vistas visuales y conectarlas a Node.js o Firebase, sustituyendo `localStorage` por consultas SQL/NoSQL reales. Todo el diseño ya está maquetado.
