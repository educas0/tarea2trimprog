# Laboratorio Trimestre 2 Programación

## Fechas:

* La clase `java.util.Date` se utiliza para tratar con fechas y tiempos. Si creas un simple objeto `Date` verás que se 
crearán fechas de diversas formas. Puedes consultar en cualquier documentación API como:
[JDK 11](https://docs.oracle.com/en/java/javase/11/docs/api/index.html) para ver cuáles son los posibles argumentos de `Date`.

* `Calendar`es un objeto estático con el cual también se puede trabajar con fechas. `Calendar.getInstance()` es un método que permite 
obtener instacias Date. 

* `SimpleFormatDate` de tal forma que se pueden asignar patrones de fecha:

```
SimpleDateFormat dateFormat = new SimpleDateFormat("dd-MM-yy");
```
* El objeto `LocalTime` también sirve para conseguir la fecha actual o transformar un formato LocalDate dada una fecha.

```
//Use of LocalDate
final LocalDate now = LocalDate.now();
final LocalDate birthdate2 = LocalDate.of(2012, 6, 30);
final LocalDate birthdate3 = LocalDate.of(2012, 6, 30);

LocalDate puede tener un aproximación de nanosegundos:
LocalDateTime.of(year, month, dayOfMonth, hour, minute, second, nanoOfSecond);


```

Existen cuatro métodos interesantes de LocalDate para comparar fechas:
`isBefore`, `isAfter`, `compareTo`, `equals`, `isEquals`.

* Con **ZoneId** podemos configurar las zonas temporales del mundo y **TimeZone** es otro objeto estático para configuraciones. 

### Ejercicio

1. Crear fechas y formatos para : `""dd-MM-yyyy"` y `""dd-MM-yyyy HH:mm:ss E"`
2. Utilizando el objeto `Calendar` configurar la fecha para  `Mon Dec 31 00:00:00 IST 1990`
3. DateFormat es una clase abstracta y **SimpleDateFormat** es una clase que hereda de la anterior. Averigua utilizando la última cómo se parsea (o convierte) un String a Formato Fecha de la fecha  "02/25/2016"
4. Crea un ejemplo de uso para los métodos `isEquals` y `isBefore` de LocalDate
5. Averigua todas las zonas temporales disponibles con utilizando **ZoneId** . Configura con **TimeZone** la zona horaria a **Canada/Yukon**
6. Averigua para averiguar cuántos dias han pasado entre dos fechas **LocalDate**
```
LocalDate d1 = LocalDate.of(2017, 5, 1);
LocalDate d2 = LocalDate.of(2017, 5, 18);
```
Utilizar el método de ` ChronoUnit.DAYS.between(...)`

7. Utilizando LocalDate y ChronoUnit.
  * Suma un día a la fecha de hoy.
  * Suma una hora a la fecha de hoy.
  * Averigua los días que hay entre la fecha de hoy y tred días más añadidos.
  `
