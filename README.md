# Lunas de Saturno
Modelo de n-cuerpos de Saturno y algunas de sus lunas.
## Autores
## Licencia
## Requerimientos
## Fuente de datos
### Ejemplo: Mimas y Saturno
En la siguiente imagen se muestran las condiciones iniciales (posición y velocidad) de Mimas con respecto a Saturno. Saturno, por ser el marco de referencia es el orígen (la posición 0,0,0) en el espacio y no tiene velocidades iniciales (0,0,0). Se pueden hacer más consultas de datos en Horizons de la NASA [aquí](https://ssd.jpl.nasa.gov/horizons.cgi).         
Todo debe de estar en m, kg, seg.        

![image](https://user-images.githubusercontent.com/28678081/103158099-d67f0780-477f-11eb-9f8e-caebb71069b7.png)

## Instrucciones de instalación y ejecución



## Introducción (marco teórico)
El problema de los n-cuerpos fue un modelo matemático sugerido por Isaac Newton en 1687 para poder modelar el comportamiento de nuestro sistema planetario, aunque esta técnica ha sido de gran ayuda en el modelizado de cualquier órbita planetaria. El modelizado de órbitas se basa en crear modelos matemáticos para simular el movimiento de un cuerpo masivo a medida que se mueve en órbita alrededor de otro cuerpo masivo debido a la gravedad.

Por su parte, Saturno tiene 82 lunas confirmadas con diámetro que varía desde unos cuantos metros hasta más grande que el del planeta Mercurio. Sus órbitas son diferentes a las de sus anillos y sus periodos orbitales también varían, por ejemplo el de Hyperion dura 21 días y el de Mimas dura 24 horas. En el presente trabajo usaremos el modelo numérico integrador de n-cuerpos usando las leyes de Newton para modelar parcialmente (no contamos con los recursos computacionales para modelarlo completo) el sistema de Saturno y sus ***(algunas)*** lunas. 

Usaremos el sistema internacional de unidades. (Creo que esto puede ir más en la metodología)
 
### Fórmulas de Newton e integración de posiciones 
Las fórmulas están escritas en negro por lo cual se recomienda usar fondo blanco.
#### Segunda ley de Newton   
<img src="https://render.githubusercontent.com/render/math?math=F = ma">     

#### Ley de la gravitación universal
<img src="https://render.githubusercontent.com/render/math?math=F = \frac{GMm}{r^2}">    

       
La diferencia es que como trabajamos en un campo vectorial de 3 dimensiones, tenemos que agregar el vector u que nos va a indicar la dirección de las fuerzas y F ahora es un vector también. Adicionalmente dividiremos entre r^3 en lugar de r^2.       
#### N-cuerpos
La ley de la gravitación universal describe la fuerza entre 2 cuerpos, para generalizarla a n-cuerpos, podemos sumar todas las fuerzas de un cuerpo con los demás y hacerle así para cada cuerpo.           
La suma queda así:      
<img src="https://render.githubusercontent.com/render/math?math=F = GM  \sum_{i} (\frac{m_i}{r_{i}^3})u_i ">     
 
Sustituimos <img src="https://render.githubusercontent.com/render/math?math=F = Ma">:     
<img src="https://render.githubusercontent.com/render/math?math=a = G  \sum_{i} (\frac{m_i}{r_{i}^3})u_i">      

Sabemos que <img src="https://render.githubusercontent.com/render/math?math=a = \frac{dv}{dt}">, entonces:     
<img src="https://render.githubusercontent.com/render/math?math=\frac{dv}{dt} = G  \sum_{i} (\frac{m_i}{r_{i}^3})u_i">         

Integramos y nos queda la velocidad:      
<img src="https://render.githubusercontent.com/render/math?math=v = G  \int \sum_{i} (\frac{m_i}{r_{i}^3})u_i \,dt">         

Como nada depende del tiempo, entonces:    
<img src="https://render.githubusercontent.com/render/math?math=v = G   \sum_{i} (\frac{m_i}{r_{i}^3})u_i \int \,dt">           
<img src="https://render.githubusercontent.com/render/math?math=v = G   \sum_{i} (\frac{m_i}{r_{i}^3})u_i (t1-t0)">           
<img src="https://render.githubusercontent.com/render/math?math=v = G   \sum_{i} (\frac{m_i}{r_{i}^3})u_i dt">        
Entonces ya sabemos cuál es la velocidad.      

Sabemos también que <img src="https://render.githubusercontent.com/render/math?math=v = \frac{dx}{dt}">, sustituimos:      
<img src="https://render.githubusercontent.com/render/math?math=\frac{dx}{dt} = v">       
Integramos:     
<img src="https://render.githubusercontent.com/render/math?math=x = \int v \,dt">       

Ahora sacamos a v de la integral aunque sí dependa del tiempo, lo que suponemos es que los saltos de tiempo son tan pequeños que tiene un efecto insignificante para los fines del modelo, entonces:        
<img src="https://render.githubusercontent.com/render/math?math=x = v \int \,dt">      
<img src="https://render.githubusercontent.com/render/math?math=x = v  (t1-t0)">
<img src="https://render.githubusercontent.com/render/math?math=x = v dt">        
La x calculada es el cambio de posición de una partícula después de un determinado dt. Entonces para calcular la posición nueva de la partícula sólo hay que sumarle el cambio calculado a la vieja posición.


## Justificación
Establecer un precedente de una modelación específica de las lunas de Saturno y al mismo tiempo usar, descubrir o/y crear e implementar técnicas que nos permitan hacer un modelo óptimo el cual nos sirva de herramienta para conocer el sistema de Saturno y saber qué le ocurrirá en el futuro.


## Objetivos
- Diseñar una métrica (o usar una existente) para saber cuánta precisión tiene nuestro modelo
- Converger con la solución del movimiento de las lunas de Saturno
- Visualizar el movimiento de algunos satélites de Saturno 

- Encontrar los parámetros óptimos. Entender qué efecto tienen diferentes pasos de integración en diferentes masas de cuerpos celestes a diferentes distancias y con diferentes velocidades
- Optimizar el código para que sea más rápido y así poder incluir más cuerpos celestes al mismo tiempo

## Metodología
## Implementación
## Pruebas
## Resultados
## Conclusiones
## Bibliografía
