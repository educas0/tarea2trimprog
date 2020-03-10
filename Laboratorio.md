# Laboratorio Trimestre 2 Programación

## Fechas:

* La clase `java.util.Date` se utiliza para tratar con fechas y tiempos. Si creas un simple objeto `Date` verás que se 
crearán fechas de diversas formas. Puedes consultar en cualquier documentación API como:
![JDK 11] (https://docs.oracle.com/en/java/javase/11/docs/api/index.html) para ver cuáles son los posibles argumentos de `Date`.

* `Calendar`es un objeto estático con el cual también se puede trabajar con fechas. `Calendar.getInstance()` es un método que permite 
obtener instacias Date. 

* `SimpleFormatDate` de tal forma que se pueden asignar patrones de fecha:

```
SimpleDateFormat dateFormat = new SimpleDateFormat("dd-MM-yy");
```

### Ejercicio

Realiza una investigación para crear fechas y formatos para : `""dd-MM-yyyy"` y `""dd-MM-yyyy HH:mm:ss E"`
