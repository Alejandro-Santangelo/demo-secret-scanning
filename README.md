# \# Demo: Secret Scanning \& Push Protection en GitHub

# 

# Objetivo: Demostrar que GitHub bloquea automaticamente el push si detecta secretos.

# 

# COMO PROBAR:

# 

# 1\. git clone https://github.com/Alejandro-Santangelo/demo-secret-scanning.git

# 

# 2\. Crear secreto de prueba:

# &#x20;  echo "xoxb- + tu token real" > .env

# &#x20;  Ejemplo formato: xoxb- + 12 numeros + guion + 13 numeros + guion + letras

# &#x20;  (No lo escribas completo aca porque GitHub te bloquea el README)

# 

# 3\. git add .env

# &#x20;  git commit -m "intentando subir slack token"

# &#x20;  git push -> VA A FALLAR con GH013

# 

# 4\. Error esperado: Push cannot contain secrets - Slack API Token

# 

# 5\. Borrar no alcanza: git rm .env -f / git commit / git push (sigue fallando)

# 

# 6\. Arreglo real: git reset --hard HEAD\~2

# 

# BUENAS PRACTICAS:

# \- .gitignore con .env

# \- Usar .env.example

