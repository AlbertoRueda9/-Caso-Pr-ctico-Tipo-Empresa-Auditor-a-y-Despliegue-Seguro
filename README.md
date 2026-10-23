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

Para comprobar que están funcionando:

```bash
docker compose ps
```

## 3. Prueba de Apache

Se comprueba que Apache funciona a través de Nginx:

```bash
curl -I http://app-gestion.empresa.local
```

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

### Con el token correcto

```bash
curl -I -H "X-Auth-Token: DAW2026" http://app-gestion.empresa.local/privado/
```

Resultado esperado:

```text
200 OK
```

## 5. Logs de Apache

Nginx envía la IP del cliente mediante `X-Forwarded-For`.

Apache utiliza `mod_remoteip` para registrar la IP real.

Para consultar los logs:

```bash
docker exec apache cat /usr/local/apache2/logs/access_log
```

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
