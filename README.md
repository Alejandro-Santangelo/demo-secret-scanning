# Demo: Como te protege Github  de subir secret key 

## Que hace esta demo?
Muestra como la plataforma bloquea automaticamente un git push si detecta un token.

## 1. Como activar la proteccion

IMPORTANTE: Este repo que estas viendo (demo-secret-scanning) es SOLO de ejemplo para leer. No lo clones para modificar ni hagas push aca para no generar inconsistencias.

Para la practica crea TU PROPIO repo de prueba:

1. Crea un repo nuevo VACIO y en PUBLICO solo de ejemplo (ej: demo-secret-prueba) sin README
   Debe ser Publico, si es Privado con cuenta gratis no aparece Push Protection.
2. Entra a Settings > Code security and analysis de TU repo nuevo
3. Activa Secret scanning y Push protection
4. Clonalo en tu PC para tener el repo local donde hacer la prueba:
git clone https://github.com/TU_USUARIO/demo-secret-prueba.git
cd demo-secret-prueba

## 2. Como probar el bloqueo (aca dentro del repo nuevo)

Estando DENTRO de la carpeta demo-secret-prueba, crea el archivo .env:

Opcion A con Git Bash:
echo "PEGA ACA UN TOKEN DE PRUEBA CON FORMATO REAL" > .env

Opcion B con Notepad:
notepad .env
(Pega el token, guarda y cerra)

Verifica que se creo: ls

Ahora intenta subirlo:
git add .env
git commit -m "prueba secreto"
git push

Vas a ver error GH013 en rojo.

## 3. Por que borrar no alcanza?

git rm .env -f no alcanza, queda en el historial.

## 4. Como arreglarlo correctamente

git reset --hard HEAD~1
rm .env
git push

## 5. Buena practica final

Crea un .gitignore en la RAIZ:
notepad .gitignore
Pega:
.env
node_modules/

git add .gitignore
git commit -m "agrego gitignore"
git push
