# Dolores Hoy

Tablero en Flutter que consume **5 APIs gratuitas** aplicando buenas prácticas de seguridad.
Desarrollo Móvil Integral · UTNG
## APIs utilizadas

| # | API | Dato | Clave |
|---|-----|------|-------|
| 1 | Open-Meteo | Clima actual de Dolores Hidalgo | No |
| 2 | Frankfurter | Tipo de cambio peso-dólar-euro | No |
| 3 | Nager.Date | Próximos días festivos de México | No |
| 4 | Wikipedia (es) | Resumen de Dolores Hidalgo | No |
| 5 | NASA APOD | Foto astronómica del día | Sí |

## Medidas de seguridad aplicadas

- **HTTPS obligatorio:** `ClienteSeguro` rechaza cualquier dirección `http://` antes de enviar datos.
- **Claves fuera del código:** la clave de la NASA entra al compilar con `--dart-define-from-file=secrets.json`; el archivo está en `.gitignore`.
- **Plantilla sin secretos:** se sube `secrets.json.example` con `DEMO_KEY`.
- **Timeout de 8 segundos y límite de 1 MB** por respuesta.
- **Validación de entradas:** coordenadas, años y texto de Wikipedia (vacío, longitud, caracteres de control).
- **Protección contra path injection:** las rutas se arman con `pathSegments`.
- **Validación de salidas:** tipos de datos, `media_type` y URLs de imagen solo `https`.
- **Logs sin secretos:** `ClienteSeguro.redactar()` oculta la clave y `ConfigClaves.toString()` no la imprime completa.
- **Errores seguros:** los errores inesperados muestran un mensaje genérico al usuario.
- **Resiliencia:** si una API falla, las otras cuatro siguen funcionando.

## Cómo ejecutarlo

    copy secrets.json.example secrets.json
    flutter pub get
    flutter run --dart-define-from-file=secrets.json

Para usar tu propia clave, regístrala gratis en https://api.nasa.gov y ponla en `secrets.json`.

## Pruebas

    flutter test

## Evidencias

### Pruebas
![Terminal](capturas/captura01.png)
![Terminal](capturas/captura02.png)
![Terminal](capturas/captura03.png)
![Terminal](capturas/captura04.png)
![Terminal](capturas/captura05.png)

### App
![App](capturas/captura1.jpeg)
![App](capturas/captura2.jpeg)
![App](capturas/captura3.jpeg)

## Evidencia de TDD (ciclo Rojo → Verde por ronda)

En cada ronda se escribe primero la prueba, se ve fallar (rojo), se implementa lo mínimo para que pase (verde) y después se mejora el código.

### Ronda 1: Cliente seguro
**Rojo:** la prueba falla porque aún no existe `cliente_seguro.dart`.

![Ronda 1 rojo](capturas/ronda1_rojo.png)

**Verde:** con `cliente_seguro.dart` implementado, la prueba pasa.

![Ronda 1 verde](capturas/ronda1_verde.png)

### Ronda 2: Seguridad (claves y configuración)
**Rojo:**

![Ronda 2 rojo](capturas/ronda2_rojo.png)

**Verde:**

![Ronda 2 verde](capturas/ronda2_verde.png)

### Ronda 3: Servicios (las 5 APIs)
**Rojo:**

![Ronda 3 rojo](capturas/ronda3_rojo.png)

**Verde:**

![Ronda 3 verde](capturas/ronda3_verde.png)

### Ronda 4: TableroViewModel
**Rojo:**

![Ronda 4 rojo](capturas/ronda4_rojo.png)

**Verde:**

![Ronda 4 verde](capturas/ronda4_verde.png)

### Resultado final: todas las pruebas pasando
![Todas las pruebas](capturas/final_todas_verde.png)
![Todas las pruebas](capturas/final_todas_verdes.png)