
# Actividad 1 - Cuestionario de contexto

- Contestar cuestionario de cotexto:
	- Cuestionario de diagnóstico para conocer tu punto de partida en redes/seguridad y tus expectativas del curso y de los CTF. Duración: 4–6 minutos. Tus respuestas no afectan tu calificación.
- Disponemos de 20 minutos

# Actividad 2 - Unirse a redes
- Para dar por completada la tarea:
	- Whatsapp : unirse al grupo de avisos en whatsapp
	- Discord: crear usuario discord y unirse al servidor (agregar a hoja de cuentas)
		- Una vez dentro asegurate tener acceso al canal #clase-uaz-ctfs-ej26
	- Youtube: seguir canal de youtube
	- Facebook: unirse a grupo de noticas en facebook
	- X : seguir cuenta de x
	Nota: usa enlaces en classroom

# Actividad 03 - Elaborar cuestionario
- Elaborar un cuestionario, con al menos 20 preguntas y sus respectivas respuestas en documento pdf del tema: 03 Concursos CTF
- No olvides crear una portada con el nombre de la materia, la tarea de que se trata, tu nombre y matricula

# Actividad 04 - Crear repositorio con documentación
Para considerar esta actividad como completada, deberás:
- Crear una cuenta en picoCTF y agregarla a la hoja de cuentas
- Unirse al classroom de la clase dentro de picoCTF >. Cpwxby8oP
- Instalar Obsidian
- Instalar Git
- Crear una cuenta en github 
- Crear un repositorio público y agregar el enlace a la hoja de cuentas
- Crear llaves SSH y agregarlas a github
- Haber subido la documentación al repositorio

## Generar llaves ssh y ver el contenido de llave publica
```
ssh-keygen -t rsa
cd .ssh
type id_rsa.pub
```
## Subir documentación a github
###  Inicializar repositorio y configurar usuario – correo:
```
cd Documents\notas-hacking
git init
git config user.name "hackadvisermx"
git config user.email "hackadviser@gmail.com"
git config --list
```
### Subir la documentación
```
git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:hackadvisermx/notas-hacking.git
git push -u origin main
```
### Subir cambios cada vez que se agreguen mas archivos o modifiquen algunos

```
git add .
git commit -m "cambios"
git push
```

