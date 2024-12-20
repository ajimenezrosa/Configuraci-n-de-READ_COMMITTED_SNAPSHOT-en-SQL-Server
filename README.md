# Configuración de READ_COMMITTED_SNAPSHOT en SQL Server

![](https://www.mssqltips.com/images_newsletter/6368_NewsletterImage.png)

El comando que veremos a continuación permite habilitar el nivel de aislamiento `READ_COMMITTED_SNAPSHOT` en una base de datos de SQL Server, una funcionalidad que mejora el rendimiento de las transacciones al evitar bloqueos innecesarios en las operaciones de lectura.

## Comando

```sql
ALTER DATABASE [ABOMOD]
SET READ_COMMITTED_SNAPSHOT ON
WITH ROLLBACK IMMEDIATE;
```

### Explicación del Código
1. **ALTER DATABASE [ABOMOD]**:
   Especifica la base de datos sobre la cual se aplicará la configuración. En este caso, la base de datos objetivo es `ABOMOD`.

2. **SET READ_COMMITTED_SNAPSHOT ON**:
   Activa el nivel de aislamiento `READ_COMMITTED_SNAPSHOT` para la base de datos. Este modo permite que las lecturas se realicen utilizando versiones de datos confirmadas en lugar de bloquear las filas.

3. **WITH ROLLBACK IMMEDIATE**:
   Indica que cualquier transacción activa en la base de datos será finalizada inmediatamente para aplicar el cambio. Esto asegura que la configuración entre en efecto sin demoras.

## Ventajas de Utilizar READ_COMMITTED_SNAPSHOT

1. **Reducción de Bloqueos**:
   Al usar versiones de datos en lugar de bloqueos, las operaciones de lectura no interfieren con las de escritura, mejorando la concurrencia.

2. **Mejor Rendimiento**:
   Las aplicaciones experimentan menos conflictos entre transacciones, lo que reduce los tiempos de espera y mejora el rendimiento general del sistema.

3. **Facilidad de Implementación**:
   No requiere modificaciones significativas en el código de la aplicación, ya que sigue utilizando el nivel de aislamiento `READ COMMITTED` de manera transparente.

4. **Mayor Escalabilidad**:
   Es ideal para sistemas con alta concurrencia, ya que evita que las lecturas bloqueen escrituras y viceversa.

## Consideraciones
- Habilitar esta opción puede incrementar el uso del `tempdb`, ya que es donde se almacenan las versiones de los datos.
- Es importante monitorear el rendimiento del servidor después de activar esta funcionalidad para asegurarse de que está beneficiando al sistema.

## Ejemplo de Uso
Supongamos que una aplicación realiza consultas intensivas de lectura mientras se ejecutan transacciones de escritura simultáneas. Habilitar `READ_COMMITTED_SNAPSHOT` evita que las operaciones de lectura se bloqueen, asegurando un flujo continuo de las transacciones y mejorando la experiencia del usuario.

## Documentación Adicional
Para más información sobre el nivel de aislamiento y su implementación en SQL Server, puedes consultar la [documentación oficial de Microsoft](https://learn.microsoft.com/en-us/sql/).

Este ajuste puede marcar una gran diferencia en sistemas de alta concurrencia, asegurando tanto la integridad de los datos como un excelente rendimiento.

