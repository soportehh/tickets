# tickets

Generación de tickets de IT



### Propósito General

Has creado un **Sistema de Gestión de Tickets (v2)**, una aplicación web completa diseñada para que los usuarios puedan enviar solicitudes de soporte y para que un administrador pueda gestionarlas. La aplicación funciona en tiempo real, lo que significa que todos los cambios se reflejan al instante sin necesidad de recargar la página.

### Tecnologías Utilizadas

* **Frontend:** HTML
* **Estilos:** Tailwind CSS (cargado desde un CDN)
* **Lógica:** JavaScript (todo en el mismo archivo HTML)
* **Backend y Base de Datos:** Google Firebase (específicamente **Firestore** para la base de datos en tiempo real y **Firebase Authentication** para la gestión de usuarios).

---

### Flujo de la Aplicación y Características

La aplicación se divide en dos modos de operación: **Modo Usuario** (por defecto) y **Modo Administrador**.

#### 1. Características para Todos los Usuarios

* **Autenticación:** Al cargar la página, la aplicación inicia sesión automáticamente (ya sea de forma anónima o usando un token de la plataforma) y muestra un `UID de Agente` único en el encabezado.
* **Creación de Tickets:** En el panel izquierdo, cualquier usuario puede rellenar un formulario para crear un nuevo ticket. Este formulario incluye:
    * Nombre Completo
    * Correo Electrónico
    * **Departamento** (como Ventas, Administración, Trafico, etc.)
    * Asunto (Soporte técnico, Solicitud de equipo, etc.)
    * Descripción del problema
    * Prioridad (Baja, Media, Alta)
* **Panel de Estadísticas:** En la parte derecha, se muestra un resumen visual del estado de todos los tickets:
    * Tickets Totales
    * Abiertos
    * En Progreso
    * Cerrados
* **Visualización y Búsqueda:** Debajo de las estadísticas, el usuario ve la lista de todos los tickets. Puede:
    * **Buscar:** Usar una barra de búsqueda para filtrar por nombre, asunto, descripción o ID del ticket.
    * **Filtrar:** Combinar filtros por Estado, Prioridad y Departamento.
* **Vista de Detalle (Solo Lectura):** Al hacer clic en cualquier ticket, se abre un modal que muestra toda la información, incluyendo:
    * Información general (ID, fecha, prioridad, departamento).
    * Una pestaña de **"Historial de Estados"** (quién cambió el estado y cuándo).
    * Una pestaña de **"Notas Internas"** (si el administrador ha añadido alguna).

#### 2. Funcionalidades del "Modo Administrador"

Este modo desbloquea funciones de gestión y está protegido por una contraseña (`HandhelsV21,`).

* **Activación:** El administrador activa un interruptor de "Modo Administrador", introduce la contraseña y la interfaz se actualiza.
* **Gestión de Estado:** En la lista principal de tickets, al administrador le aparece un botón en cada ticket (que no esté cerrado) para cambiar su estado.
    * El flujo es: `Abierto` -> `En Progreso` -> `Cerrado`.
    * **Importante:** Según la última modificación, los tickets **Cerrados no se pueden reabrir**; el botón desaparece y se muestra el texto "Ticket cerrado permanentemente".
* **Gestión en el Modal de Detalle:** Cuando un administrador abre el modal de un ticket:
    * **Añadir Notas Internas:** Puede escribir y guardar notas que solo son visibles en esta vista detallada.
    * **Eliminar Tickets:** Tiene acceso a un botón de "Eliminar Ticket", que pide una confirmación antes de borrar el ticket permanentemente de la base de datos.
