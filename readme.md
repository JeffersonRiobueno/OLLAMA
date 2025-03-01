


## Consultas

curl --location 'http://localhost:11434/v1/completions' \
--header 'Content-Type: application/json' \
--data '{
    "model": "llama3.2:3b",
    "prompt": "Cual es la de definición de docker?,Genera la respuesta breve con un tono tecnico y solo en lenguaje en Spanish  "
}'


## Listar Modelos

curl --location 'http://localhost:11434/v1/models'


## Agregar Modelos

curl --location 'http://localhost:11434/api/pull' \
--header 'Content-Type: application/json' \
--data '{"model": "llama3.2:3b"}'