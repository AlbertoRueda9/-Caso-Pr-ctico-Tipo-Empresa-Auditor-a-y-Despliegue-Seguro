#  Nginx + Apache

## 1. Descripción

En esta práctica se ha creado una arquitectura con:

- Nginx como Reverse Proxy.
- Apache como servidor Backend.
- Docker Compose para ejecutar los servicios.

Apache no tiene el puerto publicado directamente.


## 2. Puesta en marcha

Para iniciar los contenedores:

```bash
docker compose build
docker compose up -d
```
<img width="946" height="668" alt="image" src="https://github.com/user-attachments/assets/e34a542e-50a2-44e9-93c5-1347e6b97719" />
<img width="927" height="137" alt="image" src="https://github.com/user-attachments/assets/aafc8dc8-39b2-46d3-98f5-ae94f20a7ea5" />


Para comprobar que están funcionando:

```bash
docker compose ps
```

## 3. Prueba de Apache

Se comprueba que Apache funciona a través de Nginx:

```bash
curl -I http://app-gestion.empresa.local
```
<img width="812" height="220" alt="image" src="https://github.com/user-attachments/assets/afc9ae8b-fab5-45c4-8e41-4984c3715cc5" />

Resultado esperado:

```text
200 OK
```

## 4. Endpoint privado

Se ha creado el endpoint:

```text
/privado/
```

Para acceder es necesario utilizar:

```text
X-Auth-Token: DAW2026
```

### Sin token

```bash
curl -I http://app-gestion.empresa.local/privado/
```

Resultado esperado:

```text
403 Forbidden
```
<img width="835" height="127" alt="image" src="https://github.com/user-attachments/assets/bdff373d-dfdb-47b6-b86f-284cea04456f" />

### Con el token correcto

```bash
curl -I -H "X-Auth-Token: DAW2026" http://app-gestion.empresa.local/privado/
```

Resultado esperado:

```text
200 OK
```
<img width="1031" height="225" alt="image" src="https://github.com/user-attachments/assets/2ab4ab9e-be66-4bca-82e3-afecab50aaa6" />

## 5. Logs de Apache

Nginx envía la IP del cliente mediante `X-Forwarded-For`.

Apache utiliza `mod_remoteip` para registrar la IP real.

Para consultar los logs:

```bash
docker exec apache cat /usr/local/apache2/logs/access_log
```
<img width="827" height="106" alt="image" src="https://github.com/user-attachments/assets/474d3c3f-b7c3-455d-96fb-c81b42aac959" />

## 6. Resultado

La práctica cumple los tres objetivos:

- Nginx funciona como Reverse Proxy.
- Apache funciona como Backend.
- `/privado/` está protegido mediante `X-Auth-Token: DAW2026`.
- Apache registra la IP del cliente en los logs.

---

## 7. Parar los contenedores

Para detener la práctica:

```bash
docker compose down
```
