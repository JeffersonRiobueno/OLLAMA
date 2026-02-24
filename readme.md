
# OLLAMA — Local LLM con Open WebUI

Proyecto para levantar un servidor de modelos de lenguaje local (**Ollama**) junto con una interfaz web (**Open WebUI**) usando Docker Compose.

---

## Dependencias

| Herramienta | Versión mínima | Descripción |
|---|---|---|
| [Docker](https://docs.docker.com/get-docker/) | 20.10+ | Motor de contenedores |
| [Docker Compose](https://docs.docker.com/compose/install/) | 2.0+ | Orquestación de servicios |
| curl | cualquiera | Cliente HTTP para pruebas desde la terminal |

> **Nota:** No se requiere instalar Ollama ni Python de forma local; todo corre dentro de los contenedores.

---

## Instalación

1. Clona el repositorio:

```bash
git clone https://github.com/JeffersonRiobueno/OLLAMA.git
cd OLLAMA
```

2. (Opcional) Crea los directorios de volúmenes locales si no existen:

```bash
mkdir -p data models open-webui-data
```

---

## Ejecución

Levanta todos los servicios en segundo plano:

```bash
docker compose up -d
```

Verifica que los contenedores estén corriendo:

```bash
docker compose ps
```

Para detener los servicios:

```bash
docker compose down
```

### Servicios disponibles

| Servicio | URL | Descripción |
|---|---|---|
| Ollama API | http://localhost:11434 | API REST del servidor de modelos |
| Open WebUI | http://localhost:3000 | Interfaz web para chatear con los modelos |

---

## Ejemplos de uso

### Agregar un modelo

Descarga el modelo `llama3.2:3b` desde el registro de Ollama:

```bash
curl --location 'http://localhost:11434/api/pull' \
--header 'Content-Type: application/json' \
--data '{"model": "llama3.2:3b"}'
```

### Listar modelos disponibles

```bash
curl --location 'http://localhost:11434/v1/models'
```

Respuesta de ejemplo:

```json
{
  "object": "list",
  "data": [
    {
      "id": "llama3.2:3b",
      "object": "model",
      "created": 1700000000,
      "owned_by": "ollama"
    }
  ]
}
```

### Realizar una consulta al modelo

```bash
curl --location 'http://localhost:11434/v1/completions' \
--header 'Content-Type: application/json' \
--data '{
    "model": "llama3.2:3b",
    "prompt": "Cual es la definición de docker? Genera la respuesta breve con un tono técnico y solo en lenguaje Spanish"
}'
```

Respuesta de ejemplo:

```json
{
  "id": "cmpl-...",
  "object": "text_completion",
  "model": "llama3.2:3b",
  "choices": [
    {
      "text": "Docker es una plataforma de virtualización a nivel de sistema operativo que permite empaquetar aplicaciones y sus dependencias en contenedores ligeros y portables.",
      "index": 0,
      "finish_reason": "stop"
    }
  ]
}
```

---

## Interfaz Web (Open WebUI)

Accede a **http://localhost:3000** en tu navegador para usar la interfaz gráfica. Desde allí puedes:

- Seleccionar y conversar con cualquier modelo descargado.
- Gestionar el historial de conversaciones.
- Ajustar parámetros como temperatura y longitud máxima de respuesta.