🧱 1. Instalación de FastAPI y entorno

a. Crear un entorno virtual (recomendado)

python3 -m venv venv
source venv/bin/activate

b. Instalar FastAPI y Uvicorn

pip install fastapi uvicorn

🔹 FastAPI es el framework principal
🔹 Uvicorn es el servidor ASGI para correr tu app

⸻

🚀 2. Crear e iniciar un proyecto FastAPI

Estructura inicial de carpetas

fastapi-project/
├── app/
│   ├── main.py         # archivo principal
│   ├── models.py       # modelos de datos (opcional)
│   ├── routes.py       # rutas organizadas (opcional)
│   └── ...
├── requirements.txt
└── .gitignore

Código básico en app/main.py

from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hola, FastAPI"}

Correr el servidor

uvicorn app.main:app --reload

--reload reinicia el servidor automáticamente en cada cambio.

⸻

☁️ 3. Subir a GitHub

a. Inicializar Git

git init
git add .
git commit -m "Inicial proyecto FastAPI"

b. Subir a un repositorio

git remote add origin https://github.com/tu_usuario/tu_repo.git
git push -u origin master


⸻

🛑 4. .gitignore recomendado para FastAPI

# Entorno virtual
venv/

# Archivos Python
__pycache__/
*.pyc

# Configuración del editor
.vscode/
.idea/

# Archivos de sistema
.DS_Store

# Archivos de entorno
.env


⸻

📦 5. Librerías recomendadas

pip install pydantic[dotenv] python-dotenv sqlalchemy databases

Librería	¿Para qué sirve?
pydantic	Validación de datos
python-dotenv	Cargar variables del archivo .env
sqlalchemy	ORM para bases de datos relacionales
databases	Conexión asíncrona a bases de datos

Luego guarda las dependencias:

pip freeze > requirements.txt


⸻

🛠️ 6. Crear endpoints GET, POST, PUT, DELETE

from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

# Modelo de ejemplo
class Item(BaseModel):
    name: str
    description: str = None
    price: float

# Base de datos ficticia
fake_db = {}

@app.get("/items/{item_id}")
def get_item(item_id: int):
    return fake_db.get(item_id, {"error": "No encontrado"})

@app.post("/items/")
def create_item(item_id: int, item: Item):
    fake_db[item_id] = item.dict()
    return {"message": "Item creado", "item": item}

@app.put("/items/{item_id}")
def update_item(item_id: int, item: Item):
    fake_db[item_id] = item.dict()
    return {"message": "Item actualizado"}

@app.delete("/items/{item_id}")
def delete_item(item_id: int):
    if item_id in fake_db:
        del fake_db[item_id]
        return {"message": "Item eliminado"}
    return {"error": "Item no encontrado"}
