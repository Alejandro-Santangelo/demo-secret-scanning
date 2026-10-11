# Demo: Como te protege Github de subir secret key 

## Que hace esta demo?
Muestra como la plataforma bloquea automaticamente un git push si detecta un token.

## 1. Como activar la proteccion

IMPORTANTE: Este repo (demo-secret-scanning) es SOLO de ejemplo para leer. No hagas push aca para no generar inconsistencias.

Para la practica crea TU PROPIO repo:

1. Crea un repo nuevo VACIO y en PUBLICO solo de ejemplo (ej: demo-secret-prueba) sin README
   Debe ser Publico, si es Privado con cuenta gratis no te aparece la opcion.
2. En tu repo nuevo entra a Settings > Code security and analysis
3. Activa Secret scanning y Push protection
4. Clonalo en tu PC para tener la carpeta local donde probar:
git clone https://github.com/TU_USUARIO/demo-secret-prueba.git
cd demo-secret-prueba

## 2. Como probar el bloqueo

Estando DENTRO de la carpeta de tu repo nuevo, vas a crear un archivo llamado .env (aclaracion: .env es el nombre completo, no lleva nada antes del punto):

Que es notepad? Es el editor de texto de Windows. Cuando pones "notepad .env" en Git Bash, se abre una ventanita para escribir.

Hace asi:
notepad .env
Se abre el Bloc de Notas. Pega un token de prueba con formato real , por ejemplo : xxxxxxxxxxxxxxxxxxxx , guardalo (Archivo > Guardar) y cerralo.

Verifica que se creo con: ls

Ahora intenta subirlo:
git add .env
git commit -m "prueba secreto"
git push

Vas a ver error GH013 en rojo. El push no sube.

## 3. Por que borrar no alcanza?

Si haces git rm .env -f no alcanza, porque el secreto queda en el historial.

## 4. Como arreglarlo

git reset --hard HEAD~1
rm .env
git push

## 5. Buena practica final

Crea un .gitignore en la RAIZ de tu repo:
notepad .gitignore
Pega:
.env
node_modules/

Guarda y subilo:
git add .gitignore
git commit -m "agrego gitignore"
git push

Nunca subas .env, subi .env.example vacio.
