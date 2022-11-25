 Integradora-Digitales-2022
###### hola mundo
# ˗ˏˋIntegradora-Digitales-2022´ˎ˗
## ⿻Consignas:

 ###### 1. Debe poder ajustarse el tiempo solo cuando este no esta corriendo o en pausa, es decir cuando el horno esta en espera.
###### 2. . Un pulsador permitir´a comenzar la cuenta regresiva o bien pausara/reanudara si ya habiıa comenzado.
 ###### 3.  Un pulsador permite cancelar en cualquier momento la cuenta regresiva y regresar a el estado de espera.
######  4. . Mientras el horno esta en espera, las salidas deben estar apagadas. Al comenzar la cuenta regresiva se enciende el quemador y el ventilador.
 ###### 5. Cuando se alcanzan las 3/4 partes del tiempo (puede ser aproximado), se debe activar la valvula de vapor.

######  6. Mientras el tiempo este pausado, se debe apagar el ventilador.
######  7.Al finalizar el tiempo deben apagarse el quemador, ventilador y valvula(si estuviese encendida) y sonar el buzzer 10 segundos para luego regresar al estado de espera.


## ⿻Se forma por:   

  ###### • 1 display que indicaran el tiempo de cocci´on en minutos ( 0 a F, hexadecimal)
  ###### • 4 leds indicando la salida activa (quemador, ventilador, v´alvula de vapor y un buzzer)
  ###### • 2 pulsadores que permiten ajustar el tiempo deseado
  ###### • 1 pulsador que comienza el tiempo, y permite pausar.
  ###### • 1 pulsador que permite cancelar el tiempo.

  # ˗ˏˋInforme´ˎ˗

  ## ⿻Diagrama de flujo
![image](https://user-images.githubusercontent.com/111539493/203899804-1cbfed28-e07c-45df-b16d-ca8365496761.png)





  ## ⿻Circuito
![790dc733-32ac-49c6-b0d4-99dfa2beb2af](https://user-images.githubusercontent.com/111539493/203897726-f7d11b60-e14c-4e6a-ae2b-dc3e509c2f09.jpg)


## ⿻Codigo

#### » Lo primero a realizar fue la definicion de las macros, una estaba unicamente enfocada en los botones, la siguinete en las funciones del horno. 
```C
#define boton1 ((PIND >> 2) & 0x01)
#define boton2 ((PIND >> 3) & 0x01)
#define boton3 ((PIND >> 4) & 0x01)
#define boton4 ((PIND >> 5) & 0x01)
#define quemador ((PINB >> 0) & 0x01)
#define ventilador ((PINB >> 1) & 0x01)
#define valvula vapor((PINB >> 2) & 0x01)
#define buzzer ((PINB >> 3) & 0x01)
```

#### » Como siguiente paso a realizar definimos las entradas y salidas. Luego de define el contador el cual empieza desde 0 para que empiece a contar desde el 0.

```C
int cont = 0;
```
#### » Continuamos seteando los puertos 

###### ↳Esta parte correspone a los botones▸ entradas.

```C
  DDRD &= ~(1 << PD2);
  DDRD &= ~(1 << PD3);
  DDRD &= ~(1 << PD4);
  DDRD &= ~(1 << PD5);
```
###### ↳Esta parte correspone a las funciones del horno (leds)▸ salidas.

```C
  DDRB |= (1 << PB0); 
  DDRB |= (1 << PB1);
  DDRB |= (1 << PB2);
  DDRB |= (1 << PB3);
 ```
###### ↳Esta parte correspone a los puertos que se dirigen al registro de desplazamiento.

```C
  PORTC |=(1<<PC4);
  PORTC |=(1<<PC3);
  PORTC |=(1<<PC1);
  PORTC |=(1<<PC0);
```
#### » Usamos un WHILE el cual sera el encargado de que todo dentro de el se cumpla y se repita al llegar a final.

