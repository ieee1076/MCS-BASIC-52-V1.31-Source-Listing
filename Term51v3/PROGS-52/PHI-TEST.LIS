10 REM ******************************
20 REM *  Berechnung der Zahl Phi   *
30 REM *          bis zum           *
40 REM * "Multiplication Underflow" *
50 REM ******************************
100   B=1
110   A=1
120   N=.5
130   F=0
150    REM  DO 
160   F=A*B*N+F
170    PRINT F*4
180   N=N+N
190   C=SQR(A*A+B*B)
200   A=C/2
210   B=1-(SQR(1-A*A))
220    GOTO 150 :  REM LOOP
