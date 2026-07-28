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


# Actividad de clase 2
```
@15
D=A
@VAR
M=D
```
Guarda el valor 15 en una variable llamada VAR
# Actividad de clase 3
```
@10
D=A
@i
M=D
```
guarda el valor 10 en una variable i
# Actividad de clase 4
```
@i
D=M
@VAR
D=D-M
```
hace una resta

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

# 