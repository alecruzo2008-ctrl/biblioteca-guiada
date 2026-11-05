# Biblioteca guiada con Flask

API REST de práctica que consulta libros en Open Library y guarda búsquedas y libros en una base de datos SQLite local.

## Requisitos

- Python 3.11 o superior
- Git
- Postman o una extensión compatible en VS Code

## Instalación en Windows

Abre PowerShell en la carpeta del proyecto y ejecuta:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Crea un archivo `.env` en la carpeta principal con estas variables:

```text
DATABASE_URL=sqlite:///biblioteca.db
OPENLIBRARY_CONTACT=tu_correo_de_contacto
```

Reemplaza el correo de ejemplo por uno autorizado. No publiques `.env` en GitHub.

## Iniciar el servidor

Con el entorno virtual activo, ejecuta:

```powershell
python app.py
```

El servidor estará disponible en `http://127.0.0.1:5000`.

## Rutas disponibles

| Método | Ruta | Función |
|---|---|---|
| GET | `/salud` | Comprueba que el servidor esté activo |
| GET | `/libros/buscar?titulo=python` | Busca libros por título |
| GET | `/libros/autor?nombre=borges` | Busca libros por autor |
| GET | `/libros/isbn/9780132350884` | Consulta un libro por ISBN |
| GET | `/historial` | Muestra búsquedas recientes |
| POST | `/biblioteca` | Guarda un libro local |
| GET | `/biblioteca` | Lista los libros guardados |
| DELETE | `/biblioteca/<id>` | Elimina un libro local por su ID |

Para crear un libro, envía un POST a `/biblioteca` con un cuerpo JSON como este:

```json
{
  "titulo": "Clean Code",
  "autor": "Robert C. Martin",
  "isbn": "9780132350884",
  "anio": 2008
}
```

## Pruebas

Usa Postman para enviar las peticiones. Las búsquedas válidas normalmente responden `200`; una entrada inválida, `400`; un libro guardado, `201`; un ISBN duplicado, `409`; y una eliminación correcta, `200`.

Open Library es un servicio externo. Sus datos y disponibilidad pueden variar.