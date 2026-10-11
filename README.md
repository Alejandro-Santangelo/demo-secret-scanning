Demo: Como GitHub te protege de subir secretos

Que hace esta demo?

Muestra como la plataforma bloquea automaticamente un git push si detecta un token.



1\. Como activar la proteccion en tu repo

Crea un repo nuevo vacio (ej: demo-secret-prueba)

Entra a Settings > Code security and analysis

Activa Secret scanning y Push protection

2\. Como probar el bloqueo

Crea un .env de prueba con un token con formato real y luego intenta subirlo:



git add .env

git commit -m "prueba secreto"

git push



Vas a ver error GH013 en rojo. El push no sube.



3\. Por que borrar no alcanza?

Si haces git rm .env -f no alcanza, porque el secreto queda en el historial.



4\. Como arreglarlo

git reset --hard HEAD\~1

rm .env

git push



5\. Buena practica

Crea un .gitignore con:

.env

node\_modules/



Nunca subas .env, subi .env.example vacio.

