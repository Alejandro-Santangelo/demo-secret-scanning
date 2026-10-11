\# Demo: Secret Scanning \& Push Protection en 【entity-GitHub¦canonical\_name=GitHub】



\## Que es esto?

Esta demo muestra como 【entity-GitHub¦canonical\_name=GitHub】 te protege de subir secretos por accidente. Si intentas hacer push de un token de Slack, 【entity-AWS¦canonical\_name=AWS】, Google, etc, 【entity-GitHub¦canonical\_name=GitHub】 te bloquea el push con error GH013.



\## 1) Configuracion en 【entity-GitHub¦canonical\_name=GitHub】



1\. Entra a tu repo en 【entity-github¦canonical\_name=GitHub】.com

2\. Arriba anda a Settings

3\. A la izquierda: Code security and analysis

4\. Activa estas dos opciones:

&#x20;  - Secret scanning -> Enable

&#x20;  - Push protection -> Enable



Listo. Desde ahora, si haces push con un secreto, 【entity-GitHub¦canonical\_name=GitHub】 lo rechaza.



\## 2) Requisitos



\- Git instalado

\- Git Bash (en Windows)

\- Repo clonado: git clone https://github.com/Alejandro-Santangelo/demo-secret-scanning.git



\## 3) Prueba del bloqueo - Paso a paso en Git Bash



PASO 1: Crear un .env con un secreto REAL de proveedor

Para que GitHub lo detecte, tiene que tener formato de proveedor conocido. Ejemplo Slack empieza con xoxb- y sigue con numeros.



Ejecuta en Git Bash (reemplaza por un token con formato valido):

echo "tu token de slack con formato real aqui" > .env

Si pones DB\_PASSWORD=1234 NO lo va a detectar, tiene que ser formato Slack, 【entity-AWS¦canonical\_name=AWS】, etc.



PASO 2: Intentar subirlo

git add .env

git commit -m "intentando subir secreto"

git push



PASO 3: Ver el bloqueo

Vas a ver este error y el push no sube:

remote: error: GH013: Repository rule violations found

remote: - GITHUB PUSH PROTECTION

remote: - Push cannot contain secrets

remote: - Slack API Token - path: .env:1



Tu secreto nunca llego a 【entity-GitHub¦canonical\_name=GitHub】. Quedo protegido localmente.



\## 4) El error comun que NO funciona



Borrar el archivo NO alcanza:

git rm .env -f

git commit -m "borro secreto"

git push -> SIGUE FALLANDO



Por que? Porque el secreto quedo en el commit anterior, en el historial.



\## 5) Como arreglarlo bien



Tenes que borrar los commits donde estaba el secreto:

git log --oneline -3

git reset --hard HEAD\~2

Verifica que el .env ya no existe: ls -la

git push -> Ahora SI pasa



\## 6) Buenas practicas para siempre



1\. Crea un archivo .gitignore en la raiz del proyecto y pon dentro:

.env

node\_modules/

dist/



2\. Nunca subas .env. En su lugar sube .env.example con contenido vacio:

SLACK\_TOKEN=

DB\_PASSWORD=



\## 7) Dato extra



GitHub solo detecta patrones de proveedores. Si inventas tu propia variable MI\_SUPER\_CLAVE=12345, GitHub SI la deja pasar. Por eso el .gitignore es obligatorio, no dependas solo de GitHub.



\---

Demo para estudiantes - Git / GitHub

