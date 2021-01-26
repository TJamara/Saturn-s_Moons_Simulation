# Lunas de Saturno
Modelo de n-cuerpos de Saturno y algunas de sus lunas.     
Ésta es una versión nueva del modelo que parte de [este repositorio](https://github.com/itztli/n-body) cuyo autor es [itztli](https://github.com/itztli).
## Autores
Rafael Pérez - <tinoco21.30@gmail.com>    
Elena Bedolla - <maria.elena.bedolla.zamudio@gmail.com>      
Javier Navarro - <javojavojavojavo@gmail.com>
## Licencia
GNU General Public License v3.0
## Requerimientos
- python3      

Las siguientes librerías de python3:      

- matplotlib
- json      

Probado en Ubuntu20 y Windows10
## Fuente de datos
### Ejemplo: Mimas y Saturno
En la siguiente imagen se muestran las condiciones iniciales (posición y velocidad) de Mimas con respecto a Saturno. Saturno, por ser el marco de referencia es el origen (la posición 0,0,0) en el espacio y no tiene velocidades iniciales (0,0,0). Se pueden hacer más consultas de datos en Horizons de la NASA [aquí](https://ssd.jpl.nasa.gov/horizons.cgi).                 

![image](https://user-images.githubusercontent.com/28678081/103158099-d67f0780-477f-11eb-9f8e-caebb71069b7.png)

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
Para graficar la divergencia, comparamos los cálculos arrojados por nuestro modelo contra los datos de las observaciones reales de Horizons. Para ello excribimos en mimas_data.txt las posiciónes diarias de Mimas en un intervalo de 30 días. La función read_horizon() lee esos datos para posteriormete compararlos con los generados por el modelo.

## Pruebas
### 1: 4 cuerpos, dt= 0.5 y 3 meses de modelado (minutos en ejecución)
El plot tardó aproximadamente 4 horas. Nótese que estamos graficando puntos, pero están tan juntos que parecen líneas.           
![r1_2](https://user-images.githubusercontent.com/28678081/105621256-43131380-5dcb-11eb-9304-182e1a0e16b1.jpg)
### 2: Con algunas horas de modelado (minutos en ejecución), nos dimos cuenta que con dt=1 sí converge.
![p1](https://user-images.githubusercontent.com/28678081/105621390-8326c600-5dcc-11eb-8fb0-f505331975d0.jpg)
## Resultados
Después de varias pruebas, encontramos que dt = 2 nos dió los resultados más rápidos sin sacrificar la convergencia. En el sistema modelado están uncluídos 8 cuerpos: Saturno, Mimas, Encelados, Tethys, Dione, Rhea, Titan y Iapetus. El intervalo de tiempo modelado es de 30 días: del 24 de diciembre de 2020 al 23 de enero de 2021. El tiempo total de ejecución fue de aproximadamente 10 minutos.

### Gráfica de divergencia (usando a Mimas)
Muestra el error acumulado en metros en el eje y, y los días del mes en el eje x. El error (divergencia) se calcula con las mediciones reales de posición de Horizons de cada mes (30 mediciones) menos las  generadas con éste modelo.  El cálculo del error se hizo usando únicamente las posiciones de Mimas.         
![Error](https://user-images.githubusercontent.com/28678081/105878453-b03ec880-5fc6-11eb-8815-dc04cfd4ea82.png)
Típicamente se obtiene que el error o distancia con la posición real diverge de manera lineal respecto al tiempo. Probablemente tenga que ver con la simplicidad del modelo ya que el sistema de Saturno y sus satélites e incluso anillos es mucho más complejo. Pero aun así, despues de 30 dias, Mimas solo se separa 200,000 km aproximadamente, lo cual no podría no ser tanto para objetos astronómicos, el tiempo de modelado y el uso de números sin precisión arbitraria.
### Visualización de órbitas

![R1](https://user-images.githubusercontent.com/28678081/105872492-1a07a400-5fc0-11eb-872f-e9481ec02e9f.png)       

![R3](https://user-images.githubusercontent.com/28678081/105876213-5d641180-5fc4-11eb-8ba0-4b098d81f379.png)
En ésta imagen se observa que las órbitas de las Lunas de Saturno no están todas en el mismo plano.

## Conclusiones
Pudimos experimentar cómo rápidamente aumentan los recursos para ejecutar el código y visualizar el plot en medida en que aumentamos el número de partículas y el tiempo a modelar, por eso la importancia de elegír el dt óptimo para reducir las operaciones en órdenes de magnitud.
## Bibliografía
- Victor de la Luz, 2021 n-body     
https://github.com/itztli/n-body
- JPL. 2020. JPL Solar System Dynamics HORIZONS Web-Interface CA, USA. Dataset accessed    
[2020-12-24] at https://ssd.jpl.nasa.gov/horizons.cgi
