# Pasos para la configuración

1. Para esto se requiere tener docker y docker compose instalador en el servidor.

- Tener los siguientes directorios

```plaintext
mosquitto/config
mosquitto/data
mosquitto/log
```

- Copiar el archivo `mosquitto.conf` y ponerlo dentro del directorio `mosquitto/config/`
- Construir el contenedor

```bash
docker compose up -d
```

2. Seguidamente entras a la terminal del contenedor creado mqtt-server, lo hace con el siguiente comando:

```bash
docker exec -it mqtt-broker sh
```

- Y por último crear un usuario y contraseña para acceder al broker mqtt, lo puedes hacer con el siguiente comando:

```bash
mosquitto_passwd -c /mosquitto/config/passwd user_name
```

El comando anterior genera un archivo con el hash de contraseña creada, quedando en la siguiente ruta `/mosquitto/config/passwd`

- Una vez termine de poner la contraseña al usuario edita el archivo `/mosquitto/config/mosquitto.conf` y busca las siguientes líneas, y pon lo que se indica aquí, es importante esto para que tome la contraseña para las conexiones de usuario, de lo contrario no tendrá seguridad para la conexión. Descomenta la línea que dice lo siguiente `# password_file /mosquitto/config/passwd` debe quedar como la siguiente línea y no olvide poner `allow_anonymous false`

```bash
password_file /mosquitto/config/passwd
allow_anonymous false
```

- Haciendo lo anterior ya puede salir de la terminal usando `Ctrl+d` o escribiendo `exit`
  Y para terminar reinicia el contenedor: Esto se hace fuera del contenedor

```bash
docker restart mqtt-broker
```
