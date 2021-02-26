# Lunas de Saturno
Modelo de n-cuerpos de Saturno y algunas de sus lunas.     
Ésta es una versión nueva del modelo que parte de [este repositorio](https://github.com/itztli/n-body) cuyo autor es [itztli](https://github.com/itztli).
## Autores
Rafael Pérez - <tinoco21.30@gmail.com>    
Elena Bedolla - <maria.elena.bedolla.zamudio@gmail.com>      
Javier Navarro - <javojavojavojavo@gmail.com>
### Afiliación
![https://upload.wikimedia.org/wikipedia/commons/7/79/LOGO-COMPUESTO-UNAM-ENES_-_copia.png](https://user-images.githubusercontent.com/28678081/106318209-2e080b80-6235-11eb-944f-4d40f52ecedb.png)                
Somos estudiantes de 5to semestre (al momento de edición) de la Licenciatura Tecnologías para la Inforamción en Ciencias impartida en la UNAM en la Escuela Nacional de Estudios Superiores Unidad Morelia.

## Licencia
GNU General Public License v3.0
## Requerimientos
- python3      

Las siguientes librerías de python3:      

- matplotlib
- json      
- pandas
- numpy
- re
- datetime

Probado en Ubuntu20 y Windows10

## Ejecución
Clonar el git y correr n-body.py


## Introducción (marco teórico)
El problema de los n-cuerpos fue un modelo matemático sugerido por Isaac Newton en 1687 para poder modelar el comportamiento de nuestro sistema planetario, aunque esta técnica ha sido de gran ayuda en el modelizado de cualquier órbita planetaria. El modelizado de órbitas se basa en crear modelos matemáticos para simular el movimiento de un cuerpo masivo a medida que se mueve en órbita alrededor de otro cuerpo masivo debido a la gravedad.

Por su parte, Saturno tiene 82 lunas confirmadas con diámetro que varía desde unos cuantos metros hasta más grande que el del planeta Mercurio. Sus órbitas son diferentes a las de sus anillos y sus periodos orbitales también varían, por ejemplo el de Hyperion dura 21 días y el de Mimas dura 24 horas. En el presente trabajo usaremos el modelo numérico integrador de n-cuerpos usando las leyes de Newton para modelar Saturno y algunas de sus lunas ya que no contamos con los recursos computacionales para modelarlo completo). 


 
### Fórmulas de Newton e integración de posiciones 
Las fórmulas están escritas en negro por lo cual se recomienda usar fondo blanco.
#### Segunda ley de Newton   
<img src="https://render.githubusercontent.com/render/math?math=F = ma">     

#### Ley de la gravitación universal
<img src="https://render.githubusercontent.com/render/math?math=F = \frac{GMm}{r^2}">    

       
La diferencia es que como trabajamos en un campo vectorial de 3 dimensiones, tenemos que agregar el vector u que nos va a indicar la dirección de las fuerzas y F ahora es un vector también. Adicionalmente dividiremos entre <img src="https://render.githubusercontent.com/render/math?math=r^3"> en lugar de <img src="https://render.githubusercontent.com/render/math?math=r^2">.       
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
<img src="https://render.githubusercontent.com/render/math?math=v = G  ( \sum_{i} (\frac{m_i}{r_{i}^3})u_i) dt">        
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

## Metodología e implementación 
### Unidades
- Distancia: metros
- Masa: kilogramos
- Tiempo: segundos      

G está definida como variable global considerando las unidades anteriores.
### Clases y métodos
#### Particle
La clase Particle nos sirve para crear objetos partículas, cada uno con su respectiva posición, velocidad, masa, trajectoria y tiempo (inicializado en 0).
##### Métodos de Particle
- Están definidos getters para: posición, velocidad, energía cinética y para la trayectoria.    
- Está definido un setter de dt. \*\*\*Creo que no usamos este método     
- computeR: Regresa distancia entre 2 vectores. 
- computeU: Regresa la resta entre 2 vectores (la dirección de 'R').
- integrate: Actualiza la posición con el dt especificado. \*\*\*Creo que este método tampoco lo usamos, hace el trabajo de computeV, updateV y updatePosition, creo que no hace falta
- computeV: Calcula la velocidad de la partícula tomando en cuenta la posición y masa de otro único cuerpo.
- updateV: Suma una nueva velocidad (calculada en computeV) a la velocidad de la partícula actualizándola.
- updatePosition: Actualiza la posición sumándole la velocidad multiplicada por la misma posición. Si la variable save es 'True', entonces guarda la posición (en trajectoria) para su futura graficación.

#### Potential
La clase Potential pone a funcionar a todos los objetos partículas. Se inicializa con una lista de objetos Particle, en este caso Saturno y sus lunas, y con el dt.
##### Método integrante
Tiene 2 tareas:    
La primera consiste en iterar las partículas todas contra todas y actualizar sus velocidades tomando en cuenta cada interacción. La segunda tarea consiste en actualizar la posición de todas las partículas usando las velocidades previamente actualizadas.
### Definiendo partículas y parámetros
Para iterar el modelo debemos definir primero cuántas veces se va a iterar y de que tamaño va a ser el dt en cada iteración. También tenemos que llevar la cuenta del tiempo transcurrido para guardar la trayectoria que incluye el tiempo y la posición. Además tenemos que crear objetos partículas (Saturno y sus lunas en este caso), cuyas condiciones iniciales del 24 de diciembre de 2020 las guardamos en lunas.json.      

Ahora sí podemos iterar.
### Graficar
Usando la lista de posiciones (trayectory) de cada partícula, graficamos cada una con un color diferente y Saturno con un radio mayor al de sus lunas.
### Graficación de divergencia
Para graficar la divergencia, comparamos los cálculos arrojados por nuestro modelo contra los datos de las observaciones reales de Horizons. Para ello excribimos en mimas_data.txt y iapetus_data.txt las posiciónes diarias de Mimas y Iapetus en un intervalo de 30 días. La función read_horizon() lee esos datos para posteriormete compararlos con los generados por el modelo.

## Fuente de datos
### Ejemplo: Mimas y Saturno
En la siguiente imagen se muestran las condiciones iniciales (posición y velocidad) de Mimas con respecto a Saturno. Saturno, por ser el marco de referencia es el origen (la posición 0,0,0) en el espacio y no tiene velocidades iniciales (0,0,0). Se pueden hacer más consultas de datos en Horizons de la NASA [aquí](https://ssd.jpl.nasa.gov/horizons.cgi).                 

![image](https://user-images.githubusercontent.com/28678081/103158099-d67f0780-477f-11eb-9f8e-caebb71069b7.png)

## Pruebas
Partimos con los parámetros propuestos en el trabajo original: _dt = 1_ y _lenTime_ de 1 mes. 
### 1: 5 cuerpos, dt= 0.5 y 3 meses de modelado (minutos en ejecución)
El plot tardó aproximadamente 4 horas. Posteriormente hicimos pruebas con dt más grandes para disminuir el tiempo de ejecución y graficación. Nótese que estamos graficando puntos, pero están tan juntos que parecen líneas.           
![r1_2](https://user-images.githubusercontent.com/28678081/105621256-43131380-5dcb-11eb-9304-182e1a0e16b1.jpg)
### 2: Con algunas horas de modelado (+ minutos en ejecución), nos dimos cuenta que con dt=1 sí converge.  
Ahora incluimos los 8 cuerpos y modelando menos tiempo. Las pruebas fueron satisfactorias, pero se elevó el tiempo de ejecución.      
![p1](https://user-images.githubusercontent.com/28678081/105621390-8326c600-5dcc-11eb-8fb0-f505331975d0.jpg)
### 3: Para tratar de optimizar un poco y hacer menos pesada la gráfica, decidimos graficar menos puntos por cada cuerpo.
Graficamos 60 puntos por cada cuerpo, es decir guardamos las posiciones de cada partícula cada (1,296,000 ÷ 60) iteraciones para luego graficarlas, siendo 1,296,000 las iteraciones totales en 30 días de modelado y dt=2.       
![Captura de pantalla (355)](https://user-images.githubusercontent.com/60940649/106086897-972e3880-60e8-11eb-9dc7-75aef1b657ff.png)

## Resultados
Después de varias pruebas más, encontramos que dt = 2 nos dió los resultados más rápidos sin sacrificar la convergencia. En el sistema modelado están incluídos 8 cuerpos: Saturno, Mimas, Encelados, Tethys, Dione, Rhea, Titan y Iapetus. El intervalo de tiempo modelado es de 30 días: del 24 de diciembre de 2020 al 23 de enero de 2021. El tiempo total de ejecución fue de aproximadamente 10 minutos.

### Gráfica de divergencia (usando a Mimas y Iapetus)
- Eje x: _días_ 
- Eje y: _e/dp_, donde _e_ es el error en metros y _dp_ es la distancia promedio del satélite a Saturno.     


El error (divergencia) se calcula con la distancia euclideana entre mediciones reales de posición de Horizons de cada mes (30 mediciones) y las  generadas con éste modelo.  El cálculo del error se hizo usando únicamente las posiciones de Mimas y las de Iapetus.         



#### Mimas
![Error_conjunto_mimas](https://user-images.githubusercontent.com/28678081/106224057-31a18100-61a8-11eb-8d0f-6af58a308bda.png)        
Resulta que Mimas no converge, lo cual nos resultó muy extraño porque la gráfica muestra que Mimas se desvía demasiado y nuestras visualizaciones con puntitos no muestran perturbaciones tan extremas (¡del 100%!). Después de varias pruebas vimos que Mimas se iba atrasando en cada iteración, como si estuviera moviéndose en cámara lenta en la trayectoria correcta. Por eso pasó desapercibido en la etapa de pruebas, el error estaba escondido. 

#### Iapetus
![Error_conjunto_Iapetus](https://user-images.githubusercontent.com/28678081/106224064-36fecb80-61a8-11eb-9a7f-aba7f55d2f16.png)         
Se nos ocurrió medir la divergencia de Iapetus, ya que a diferencia de Mimas que cuenta con el periodo orbital más córto (y angosto) de 0.9 días, éste cuenta con el más largo de 79 días. Diverge muchísimo menos, ni siquiera llega a 0.01 e/dp.
### Visualización de órbitas

![R1](https://user-images.githubusercontent.com/28678081/105872492-1a07a400-5fc0-11eb-872f-e9481ec02e9f.png)       

![R3](https://user-images.githubusercontent.com/28678081/105876213-5d641180-5fc4-11eb-8ba0-4b098d81f379.png)           
En ésta imagen se observa que las órbitas de las Lunas de Saturno no están todas en el mismo plano.

![Captura de pantalla (354)](https://user-images.githubusercontent.com/60940649/106086709-51717000-60e8-11eb-97e4-0212b73b5bfe.png)

## Conclusiones
Cumplimos satisfactoriamente los objetivos.     

Diseñamos una métrica para evaluar nuestro modelo, la cual consistió en comparar sus predicciones con mediciones reales. Y aunque los resultados de convergencia del modelo fueron mezclados, nos dimos cuenta de la posibilidad de que en el modelado de un sistema algunos cuerpos converjan y otros no. Hicimos muchos más experimentos con dt's más pequeñas (ej.: 0.25) pero no observamos mejora alguna. 
> #### Hipótesis divergencia de Mimas
> Creemos que es necesario un dt muchísimo más pequeño para converger con la solución de órbitas mucho más angostas como la de Mimas. El 'movimiento' de cada partícula en el modelo de un dt a otro es recto, la pequeñez del dt hace que el movimiento parezca curvo. La idea es que la órbita de Mimas es tan pequeña que el dt ya no parece ser tan pequeño para ella, entonces la órbita modelada empieza a parecerse más a un polígono que a una curva. Cada dt la partícula avanza demasiado y para el siguiente dt tiene que corregir mucho la trayectoria dejando un 'pico' fuera de la órbita real, con las iteraciones los picos se van acumulando y la particula se va quedando atrás porque está recorriendo más camino (pasando por los picos). Sin embargo por el momento no tenemos suficientes pruebas para afirmarlo. Naturalmente surge la pregunta de cómo modelar un sistema cuyos cuerpos necesitan dt's muy diferentes para converger.    

Logramos visualizar consistentemente las órbitas de las lunas de Saturno.

Encontramos el dt óptimo al menos para Iapetus, partiendo del dt=1 propuesto en el trabajo en que éste se basó. 

Redujimos el número de puntos a graficar en el plot, haciéndolo mucho más eficiente.

Pudimos experimentar cómo rápidamente aumentan los recursos para ejecutar el código y visualizar el plot en medida en que aumentamos el número de partículas y el tiempo a modelar, por eso la importancia de elegir el dt óptimo para reducir las operaciones en órdenes de magnitud.     

Necesitamos seguir haciendo experimentos.
## Bibliografía
- Victor de la Luz, 2021 n-body     
https://github.com/itztli/n-body
- JPL. 2020. JPL Solar System Dynamics HORIZONS Web-Interface CA, USA. Dataset accessed    
[2020-12-24] at https://ssd.jpl.nasa.gov/horizons.cgi
