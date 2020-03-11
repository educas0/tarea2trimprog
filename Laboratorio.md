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

## Trabajo con la nueva API de Fechas (JDK >= 8) de JAVA

* La calificación total será de 0.5 puntos sobre 10 de la nota global trimestral y tendrá como fecha máximo de entrega el lunes 16 a las 14:00h mediante la actividad classroom que estará publicada en el foro de Programación de github aunque llegará al correo del alumno.
* El trabajo será entregado de manera indiviual y el cual consistirá en realizar una serie de ejercicios que pueden ser entregados con código adjunto o en un fichero markdown o pdf. En él se adjuntarán las soluciones que habéis realizado con los ejercicios propuestos más abajo. En un primer lugar tenéis que leer el siguiente contenido y luego realizar los ejercicios de más abajo.

#### Material:  [jdk 11](https://docs.oracle.com/en/java/javase/11/docs/api/index.html)

Desde la versión Java `1.0`, los años en el API empiezan en `1900` y los meses inician con el índice `0`. Por lo tanto, cualquier fecha representada haciendo uso de la clase `java.util.Date` no era legible. Por ejemplo, representaremos la fecha en que Java 8 fue liberado `18 de Marzo del 2014`:

```java
Date date = new Date(114, 2, 18);
System.out.println(date);
```

Como resultado de la línea anterior tenemos lo siguiente:

```java
Tue Mar 18 00:00:00 AEST 2014
```

En Java `1.1`, la clase `java.util.Calendar` fue agregada y varios métodos de la clase `java.util.Date` fueron deprecados. Hacer uso de la clase `java.util.Calendar` no dio mayores beneficios dado su diseño.

```java
Calendar calendar = new GregorianCalendar(2014, 2, 18);
System.out.println(calendar.getTime());
```

A partir de Java 8, la nueva Date API es amigable y esta basada en el proyecto [Joda-Time](http://www.joda.org/joda-time/) la cual fue adoptada como `JSR-310`.

En el paquete `java.time`, se puede encontrar las nuevas clases del Date API como `LocalDate`, `LocalTime`, `LocalDateTime`, `Instant`, `Duration` y `Period`, de las cuales hablaremos a continuación.

## LocalDate, LocalTime and LocalDateTime

### LocalDate

[LocalDate](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html), representa una fecha sin tener en cuenta el tiempo. Haciendo uso del método `of(int year, int month, int dayOfMonth)`, se puede crear un `LocalDate`.

```java
LocalDate date = LocalDate.of(1989, 11, 11); //1989-11-11
System.out.println(date.getYear()); //1989
System.out.println(date.getMonth()); //NOVEMBER
System.out.println(date.getDayOfMonth()); //11
```

También, se puede hacer uso del `enum` [Month](https://docs.oracle.com/javase/8/docs/api/java/time/Month.html) para dar legibilidad al código.

```java
LocalDate date = LocalDate.of(1989, Month.NOVEMBER, 11);
```

Finalmente, para capturar el `LocalDate` actual se puede usar el método `now()`:

```java
LocalDate date = LocalDate.now();
```

### LocalTime

De manera similar, se tiene [LocalTime](https://docs.oracle.com/javase/8/docs/api/java/time/LocalTime.html), la cual representa un tiempo determinado. Haciendo uso del método `of()`, esta clase puede crear un `LocalTime` teniendo en cuenta la hora y minuto; hora, minuto y segundo y finalmente hora, minuto, segundo y nanosegundo.

```java
LocalTime time = LocalTime.of(5, 30, 45, 35); //05:30:45:35
System.out.println(time.getHour()); //5
System.out.println(time.getMinute()); //30
System.out.println(time.getSecond()); //45
System.out.println(time.getNano()); //35
```

Finalmente, para capturar el `LocalTime` actual se puede usar el método `now()`:

```java
LocalTime time = LocalTime.now();
```

### LocalDateTime

[LocalDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html), es una clase compuesta, la cual combina las clases anteriormente mencionadas `LocalDate` y `LocalTime`.

En el siguiente fragmento de código se puede apreciar como construir un `LocalDateTime` haciendo uso de todos los campos (año, mes, día, hora, minuto, segundo, nanosegundo):

```java
LocalDateTime dateTime = LocalDateTime.of(1989, 11, 11, 5, 30, 45, 35); //1989-11-11T05:30:45.000000035
```

También, se puede crear un objeto `LocalDateTime` basado en los tipos `LocalDate` y `LocalTime`, a continuación se muestra el uso del método `of(LocalDate date, LocalTime time)`:

```java
LocalDate date = LocalDate.of(1989, 11, 11);
LocalTime time = LocalTime.of(5, 30, 45, 35);
LocalDateTime dateTime = LocalDateTime.of(date, time);
```

Finalmente, se puede capturar el `LocalDateTime` exacto de la ejecución usando el método `now()`, como se muestra a continuación.

```java
LocalDateTime dateTime = LocalDateTime.now();
```

**NOTA:** Estos objetos no tienen ninguna información relacionada al timezone.

## Instant

[Instant](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html), representa el número de segundos desde `1 de Enero de 1970`. Es un modelo de fecha y tiempo fácil de interpretar para una máquina.

```java
Instant instant = Instant.ofEpochSecond(120);
System.out.println(instant);
```

El código anterior da como resultado:

```java
1970-01-01T00:02:00Z
```

De igual manera que las clases ya mencionadas, `Instant` provee el método `now()`.

```java
Instant instant = Instant.now();
```

## Duration and Period

### Duration

[Duration](https://docs.oracle.com/javase/8/docs/api/java/time/Duration.html), hace referencia a la diferencia que existe entre dos objetos de tiempo.

En el siguiente ejemplo, la duración se calcula haciendo uso de dos objetos `LocalTime`:

```java
LocalTime localTime1 = LocalTime.of(12, 25);
LocalTime localTime2 = LocalTime.of(17, 35);
Duration duration = Duration.between(localTime1, localTime2);
```

Otra opción de calcular la duración entre dos objetos es usando dos objetos `LocalDateTime`:

```java
LocalDateTime localDateTime1 = LocalDateTime.of(2016, Month.JULY, 18, 14, 13);
LocalDateTime localDateTime2 = LocalDateTime.of(2016, Month.JULY, 20, 12, 25);
Duration duration = Duration.between(localDateTime1, localDateTime2);
```

También, se puede crear una duración basada en el método `of(long amount, TemporalUnit unit)`. En el siguiente ejemplo, se muestra como crear un `Duration` de un día.

```java
Duration oneDayDuration = Duration.of(1, ChronoUnit.DAYS);
```

Se puede apreciar el uso del enum [ChronoUnit](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/ChronoUnit.html), la cual es una implementación de `TemporalUnit` y nos brinda una serie de unidades de períodos de tiempo como `ERAS`, `MILLENNIA`, `CENTURIES`, `DECADES`, `YEARS`, `MONTHS`, `WEEKS`, etc.

También, se puede crear `Duration` basado en los métodos `ofDays(long days)`, `ofHours(long hours)`, `ofMilis(long milis)`, `ofMinutes(long minutes)`, `ofNanos(long nanos)`, `ofSeconds(long seconds)`. El ejemplo anterior puede ser reemplazado por la siguiente línea:

```java
Duration oneDayDuration = Duration.ofDays(1);
```

### Period

[Period](https://docs.oracle.com/javase/8/docs/api/java/time/Period.html), hace referencia a la diferencia que existe entre dos fechas.

```java
LocalDate localDate1 = LocalDate.of(2016, Month.JULY, 18);
LocalDate localDate2 = LocalDate.of(2016, Month.JULY, 20);
Period period = Period.between(localDate1, localDate2);
```

Se puede crear `Period` basado en el método `of(int years, int months, int days)`. En el siguiente ejemplo, se crea un período de `1 año 2 meses y 3 días`:

```java
Period period = Period.of(1, 2, 3);
```

Del mismo modo que `Duration`, se puede crear `Period` basado en los métodos `ofDays(int days)`, `ofMonths(int months)`, `ofWeeks(int weeks)`, `ofYears(int years)`.

```java
Period period = Period.ofYears(1);
```

## Manipulación

### Manipulando `LocalDate`

Haciendo uso de los métodos `withYear(int year)`, `withMonth(int month)`, `withDayOfMonth(int dayOfMonth)`, `with(TemporalField field, long newValue)` se puede modificar el `LocalDate`.

```java
LocalDate date = LocalDate.of(2016, Month.JULY, 25); //2016-07-25
LocalDate date1 = date.withYear(2017); //2017-07-25
LocalDate date2 = date.withMonth(8); //2016-08-25
LocalDate date3 = date.withDayOfMonth(27); //2016-07-27
LocalDate date4 = date.with(ChronoField.MONTH_OF_YEAR, 9); //2016-09-25
```

**NOTA:** Si en el último ejemplo usamos `ChronoField.HOUR_OF_DAY` la siguiente excepción será lanzada `java.time.temporal.UnsupportedTemporalTypeException: Unsupported unit: HourOfDay`.

### Manipulando `LocalTime`

Haciendo uso de los métodos `withHour(int hour)`, `withMinute(int minute)`, `withSecond(int second)`, `withNano(int nanoOfSecond)` se puede modificar el `LocalTime`.

```java
LocalTime time = LocalTime.of(14, 30, 35); //14:30:35
LocalTime time1 = time.withHour(20); //20:30:35
LocalTime time2 = time.withMinute(25); //14:25:35
LocalTime time3 = time.withSecond(23); //14:30:23
LocalTime time4 = time.withNano(24); //14:30:35.000000024
LocalTime time5 = time.with(ChronoField.HOUR_OF_DAY, 23); //23:30:35
```

**NOTA:** Si en el último ejemplo usamos `ChronoField.MONTH_OF_YEAR` la siguiente excepción será lanzada `java.time.temporal.UnsupportedTemporalTypeException: Unsupported unit: MonthOfYear`.

### Manipulando `LocalDateTime`

`LocalDateTime` provee los mismo métodos mencionados en las clases `LocalDate` y `LocalTime`.

```java
LocalDateTime dateTime = LocalDateTime.of(2016, Month.JULY, 25, 22, 11, 30);
LocalDateTime dateTime1 = dateTime.withYear(2017);
LocalDateTime dateTime2 = dateTime.withMonth(8);
LocalDateTime dateTime3 = dateTime.withDayOfMonth(27);
LocalDateTime dateTime4 = dateTime.withHour(20);
LocalDateTime dateTime5 = dateTime.withMinute(25);
LocalDateTime dateTime6 = dateTime.withSecond(23);
LocalDateTime dateTime7 = dateTime.withNano(24);
LocalDateTime dateTime8 = dateTime.with(ChronoField.HOUR_OF_DAY, 23);
```

### Uso de `TemporalAdjusters`

`LocalDate`, `LocalTime` y `LocalDateTime` proveen los siguientes métodos:

- `with(TemporalField field, long newValue)`
- `with(TemporalAdjuster adjuster)`

El primero de ellos ha sido revisado en los ejemplos anteriores. El  segundo brinda una serie de métodos que son útiles para cálculos.

```java
import static java.time.temporal.TemporalAdjusters.next;
import static java.time.temporal.TemporalAdjusters.firstDayOfNextMonth;
import static java.time.temporal.TemporalAdjusters.lastDayOfMonth;

LocalDateTime dateTime = LocalDateTime.of(2016, Month.JULY, 25, 22, 11, 30);
LocalDateTime dateTime1 = dateTime.with(next(DayOfWeek.SUNDAY)); //(1)
LocalDateTime dateTime2 = dateTime.with(firstDayOfNextMonth()); //(2)
LocalDateTime dateTime3 = dateTime.with(lastDayOfMonth()); //(3)
```

1. Retorna el próximo Domingo.
2. Retorna el primer día del siguiente mes (Agosto).
3. Retorna el último día del mes (Julio).

`TemporalAdjuster` es una `FunctionalInterface`, eso quiere decir que se puede crear una implementación propia haciendo uso de lambdas.

```java
LocalDateTime dateTime = LocalDateTime.of(2016, Month.JULY, 28, 22, 11, 30);
TemporalAdjuster tempAdj = temp -> nextDayAfterHolidays(LocalDateTime.from(temp));
LocalDateTime dateTime1 = dateTime.with(tempAdj);

public Temporal nextDayAfterHolidays(LocalDateTime dateTime) {
  LocalDate[] holidays = {
    LocalDate.of(2016, Month.JULY, 28),
    LocalDate.of(2016, Month.JULY, 29)
  };

  LocalDate date = dateTime.toLocalDate();
  boolean isHoliday = Arrays.stream(holidays)
                            .anyMatch(holiday -> holiday.isEqual(date));
  if (isHoliday) {
    return nextDayAfterHolidays(dateTime.plus(1, ChronoUnit.DAYS));
  }
  return dateTime;
}
```

## Operaciones

### Operaciones con `LocalDate`

Realizar operaciones como suma o resta de días, meses, años, etc es muy fácil con la nueva `Date API`. Los siguientes métodos `plus(long amountToAdd, TemporalUnit unit)`, `minus(long amountToSubtract, TemporalUnit unit)` proveen una manera general de realizar estas operaciones.

```java
LocalDate date = LocalDate.of(2016, Month.JULY, 18);
LocalDate datePlusOneDay = date.plus(1, ChronoUnit.DAYS);
LocalDate dateMinusOneDay = date.minus(1, ChronoUnit.DAYS);
```

Asimismo, puede hacerse uso de las siguientes unidades `ChronoUnit.YEARS`, `ChronoUnit.MONTHS`.

**NOTA:** Si en los ejemplos usamos `ChronoUnit.HOURS` la siguiente excepción será lanzada `java.time.temporal.UnsupportedTemporalTypeException: Unsupported unit: Hours`.

También se puede hacer cálculos basados en un `Period`. En el siguiente ejemplo, se crea un `Period` de 1 día para poder realizar los cálculos.

```java
LocalDate date = LocalDate.of(2016, Month.JULY, 18);
LocalDate datePlusOneDay = date.plus(Period.ofDays(1));
LocalDate dateMinusOneDay = date.minus(Period.ofDays(1));
```

Finalmente, haciendo uso de métodos explícitos como `plusDays(long daysToAdd)` y `minusDays(long daysToSubtract)` se puede indicar el valor a incrementar o reducir.

```java
LocalDate date = LocalDate.of(2016, Month.JULY, 18);
LocalDate datePlusOneDay = date.plusDays(1);
LocalDate dateMinusOneDay = date.minusDays(1);
```

### Operaciones con `LocalTime`

La nueva `Date API` perimite realizar operaciones como suma y resta de horas, minutos, segundos, etc. Al igual que `LocalDate`, los siguientes métodos `plus(long amountToAdd, TemporalUnit unit)`, `minus(long amountToSubtract, TemporalUnit unit)` proveen una manera general de realizar estas operaciones.

```java
LocalTime time = LocalTime.of(15, 30);
LocalTime timePlusOneHour = time.plus(1, ChronoUnit.HOURS);
LocalTime timeMinusOneHour = time.minus(1, ChronoUnit.HOURS);
```

Asimismo, puede hacerse uso de las siguientes unidades `ChronoUnit.MINUTES`, `ChronoUnit.SECONDS`, `ChronoUnit.NANOS`.

**NOTA:** Si en los ejemplos usamos `ChronoUnit.DAYS` la siguiente excepción será lanzada `java.time.temporal.UnsupportedTemporalTypeException: Unsupported unit: Days`.

También se puede hacer cálculos basados en un `Duration`. En el siguiente ejemplo, se crea un `Duration` de 1 hora para poder realizar los cálculos.

```java
LocalTime time = LocalTime.of(15, 30);
LocalTime timePlusOneHour = time.plus(Duration.ofHours(1));
LocalTime timeMinusOneHour = time.minus(Duration.ofHours(1));
```

Finalmente, haciendo uso de métodos explícitos como `plusHours(long hoursToAdd)` y `minusHours(long hoursToSubtract)` se puede indicar el valor a incrementar o reducir.

```java
LocalTime time = LocalTime.of(15, 30);
LocalTime timePlusOneHour = time.plusHours(1);
LocalTime timeMinusOneHour = time.minusHours(1);
```

### Operaciones con `LocalDateTime`

`LocalDateTime`, al ser una clase compuesta por `LocalDate` y `LocalTime` ofrece los mismos métodos para realizar operaciones.

```java
LocalDateTime dateTime = LocalDateTime.of(2016, Month.JULY, 28, 14, 30);
LocalDateTime dateTime1 = dateTime.plus(1, ChronoUnit.DAYS)
                                  .plus(1, ChronoUnit.HOURS);
LocalDateTime dateTime2 = dateTime.minus(1, ChronoUnit.DAYS)
                                  .minus(1, ChronoUnit.HOURS);
```

En el siguiente ejemplo, se hace uso de `Period` y `Duration`.

```java
LocalDateTime dateTime = LocalDateTime.of(2016, Month.JULY, 28, 14, 30);
LocalDateTime dateTime1 = dateTime.plus(Period.ofDays(1))
                                  .plus(Duration.ofHours(1));
LocalDateTime dateTime2 = dateTime.minus(Period.ofDays(1))
                                  .minus(Duration.ofHours(1));
```

Finalmente, haciendo uso de los métodos `plusX(long xToAdd)` o `minusX(long xToSubtract)`

```java
LocalDateTime dateTime = LocalDateTime.of(2016, Month.JULY, 28, 14, 30);
LocalDateTime dateTime1 = dateTime.plusDays(1)
                                  .plusHours(1);
LocalDateTime dateTime2 = dateTime.minusDays(1)
                                  .minusHours(1);
```

Además, métodos como `isBefore`, `isAfter`, `isEequal` están disponibles para comparar las siguientes clases `LocalDate`, `LocalTime` y `LocalDateTime`.

```java
LocalDate date1 = LocalDate.of(2016, Month.JULY, 28);
LocalDate date2 = LocalDate.of(2016, Month.JULY, 29);

boolean isBefore = date1.isBefore(date2); //true
boolean isAfter = date2.isAfter(date1); //true
boolean isEqual = date1.isEqual(date2); //false
```

## Formatos

Cuando se trabaja con fechas, en ocasiones se requiere de un formato personalizado. Java 8 ofrece la clase `java.time.format.DateTimeFormatter` la cual provee algunos formatos.

```java
LocalDate date = LocalDate.of(2016, Month.JULY, 25);
String date1 = date.format(DateTimeFormatter.BASIC_ISO_DATE); //20160725
String date2 = date.format(DateTimeFormatter.ISO_DATE); //2016-07-25
```

**NOTA:** Si en el último ejemplo usamos `DateTimeFormatter.ISO_DATE_TIME` la siguiente excepción será lanzada `java.time.temporal.UnsupportedTemporalTypeException: Unsupported field: HourOfDay`.

También se puede usar el método `ofPattern(String pattern)`, para definir un formato en particular.

```java
LocalDate date = LocalDate.of(2016, Month.JULY, 25);
String date1 = date.format(DateTimeFormatter.ofPattern("yyyy/MM/dd")); //2016/07/25
```

Por último, se puede hacer uso de la clase `java.time.format.DateTimeFormatterBuilder`.

```java
LocalDateTime dateTime = LocalDateTime.of(2016, Month.JULY, 25, 15, 30);
OffsetDateTime offsetDateTime = dateTime.atOffset(ZoneOffset.ofHours(-5));
DateTimeFormatter formatter = new DateTimeFormatterBuilder()
                                  .appendText(ChronoField.DAY_OF_MONTH)
                                  .appendLiteral(" ")
                                  .appendText(ChronoField.MONTH_OF_YEAR)
                                  .appendLiteral(" ")
                                  .appendText(ChronoField.YEAR)
                                  .appendOffsetId()
                                  .toFormatter();
String dateTime1 = offsetDateTime.format(formatter); //25 July 2016-05:00
```

------

### Ejercicios

1. Crear fechas y formatos para : `""dd-MM-yyyy"` y `""dd-MM-yyyy HH:mm:ss E"`
2. Utilizando el objeto `Calendar` configurar la fecha para  `Mon Dec 31 00:00:00 IST 1990`
3. DateFormat es una clase abstracta y **SimpleDateFormat** es una clase que hereda de la anterior. Averigua utilizando la última cómo se parsea (o convierte) un String a Formato Fecha de la fecha  "02/25/2016".
4. Utilizando el siguiente código:
```java
final LocalDate now = LocalDate.now();
final LocalDate birthdate2 = LocalDate.of(2012, 6, 30); 
final LocalDate birthdate3 = LocalDate.of(2012, 6, 30);
```

Utilizando `isBefore, isAfter, isEqual, equals, `etc, calcular:

* Si hoy es antes que **birthdate2**
* Si hoy es después que **birthdate2**
* Si es igual **birthdate2** y **birthdate3**

1. Averigua todas las zonas temporales disponibles con utilizando **ZoneId** . Configura con **TimeZone** la zona horaria a **Canada/Yukon**
2. Averigua para averiguar cuántos dias han pasado entre dos fechas **LocalDate**
```
LocalDate d1 = LocalDate.of(2017, 5, 1);
LocalDate d2 = LocalDate.of(2017, 5, 18);
```
Utilizar el método de ` ChronoUnit.DAYS.between(...)`

7. Utilizando LocalDate y ChronoUnit.
  * Suma un día a la fecha de hoy.
  * Suma una hora a la fecha de hoy.
  * Averigua los días que hay entre la fecha de hoy y tred días más añadidos.

8. Teniendo las siguientes declaraciones:

```java
LocalTime start = LocalTime.of(1, 0, 0); // hora, minuto, segundo
LocalTime end = LocalTime.of(2, 10, 20); // hora, minuto, segundo
```

Calcula las horas, minutos, segundos, milisegundos, microsegundos y nanosegundos transcurridos entre los dos tiempos.

9. Configura la zona horaria `Asia/Kolkata` y muestra la hora en esa zona horaria. Utiliza ZoneId y LocalTime.
10. Con el ejercicio anterior calcula la diferencia horaria entre tu zona horaria y la calculada anteriormente. 
  `
