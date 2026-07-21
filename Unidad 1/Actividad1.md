# Actividad 1
//EJC 1
			@1
			D=A
			@2
			D=D+A
			@16
			M=D
(END)
			@END
			0;JMP

// EJC 2
@15
D=A
@VAR
M=D

//EJC 3
@10
D=A
@i
M=D

//EJC 4 
@i
D=M
@VAR
D=D-M


//EJC 5
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