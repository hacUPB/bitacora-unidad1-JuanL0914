
# Unidad 1

# Sesiones 1 y 2

# Actividad 1: Ciclo fetch-decode-execute
```
@1
D=A
@2
D=D+A
@16
M=D
(END)
@END
0;JMP
```
La RAM cambia cuando en la ROM llega a M=D en la linea 16 de 0 a 3 y cuando llega ahi entra en bucle infinito
La diferencia de RAM y ROM:
ROM: Guarda el programa (instrucciones), es solo de lectura, no cambia durante la ejecucion
RAM: Guarda los datos (resultados/variables), se lee y escribe constantemente mientras corre el programa
![prueba](<Captura de pantalla 2026-08-04 144435.png>)


# Actividad de clase 2

```
@15
D=A
@VAR
M=D
```

Guarda el valor 15 en una variable llamada VAR
![prueba](<Captura de pantalla 2026-08-04 144551.png>)
# Actividad de clase 3

```
@10
D=A
@i
M=D
```

guarda el valor 10 en una variable i
![prueba](<Captura de pantalla 2026-08-04 144859.png>)
# Actividad de clase 4

```
@i
D=M
@VAR
D=D-M
```

hace una resta
![prueba](<Captura de pantalla 2026-08-04 145048.png>)
# Actividad de clase 5

```
@1000
D=A
@i
M=D
(LOOP)
@i
D=M
@CONT
D;JEQ
@i
M=M-1
@LOOP
0;JMP
(CONT)
@CONT
0;JMP
```

hace una cuenta regresiva del 1000 va restando 1 cada vuelta del bucle hasta que llega a 0 cuando llega a 0 salta a CONT donde se queda en un bucle infinito
![Restando del 1000 de 1 en 1 hasta 0](<Captura de pantalla 2026-08-04 145140.png>) ![cuando llega 0 queda en bucle](<Captura de pantalla 2026-08-04 145215.png>)
# Sesion 3 y 4

# Actividad de clase 6
```
@SCREEN
D=A
@i
M=D

(READKEYBOARD)
@KBD
D=M
@KEYPRESSED
D;JNE
@i
D=M
@SCREEN
D=D-A
@READKEYBOARD
D;JLE
@i
M=M-1
A=M
M=0
@READKEYBOARD
0;JMP

(KEYPRESSED)
@i
D=M
@KBD
D=D-A
@READKEYBOARD
D;JGE
@i
A=M
M=-1
@i
M=M+1
@READKEYBOARD
0;JMP
```

este codigo cambia la pantalla en negro al presionar el espacio se ejecuta en bucle hasta que se presione el espacio
![sin presionar espacio](<Captura de pantalla 2026-08-04 145437.png>)
![al presionar espacio](<Captura de pantalla 2026-08-04 145640.png>)
# Actividad 7: control de flujo con saltos
```
 @5
 D=M
 @10
 D=D-A
 @MENOR
 D;JLT
 @7
 M=0
 @END
 0;JMP

 (MENOR)
 @7
 M=1

 (END)
 @END
 0;JMP 
```
![Cuando 5 es >= a 10](<Captura de pantalla 2026-08-04 143759.png>)
![Cuando 5 es < a 10](<Captura de pantalla 2026-08-04 143929.png>)

# Actividad 8
```
@i         
M=1          // i=1 (contador, inicia en 1)
@sum
M=0         // sum = 0 (acumulador, inicia en 0)

(LOOP)
@i
D=M         // D=i
@5          
D=D-A       // D = i - 5
@FIN
D;JGT       //si D > 0 (i > 5 ) sale del bucle

@i
D=M         //D = i (suma)
@sum
M=D+M       // sum = sum + i

@i
M=M+1       // i = i + 1 (Avanza el contador)
@LOOP
0;JMP       // repite bucle

(FIN)
@sum
D=M         // D = sum (resultado final)
@12
M=D         // RAM[12] = sum

(END)
@END
0;JMP   // Bucle infinito
``` 
el programa suma los numeros del 1 al 5 usando un bucle, y guarda el resultado en la direccion de memoria 12 (RAM[12])

inicia un contador i=1 y un acumulador sum = 0
en cada vuelta (loop) compara i con 5:si i > 5 sale del bucle
si no, suma i al acumulador (sum + sum + i)
y aumenta el contador ( i = i + 1)
al salir del bucle copia el valor final y lo añade en RAM[12]
Termina en un bucle infinito
![.](<Captura de pantalla 2026-08-04 151910.png>)

# Actividad 9 : Punto en la pantalla
```
@SCREEN
D=A
@16348
A=D
M=-1

(END)
@END
0;JMP
```
![.](<Captura de pantalla 2026-08-04 152813.png>)

# Actividad 10: Linea en el medio de la pantalla

