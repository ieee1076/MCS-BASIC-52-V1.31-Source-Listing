10     REM *******************************
20     REM *   I2C Communication Test    *
30     REM * (C) H.-J. Boehling 08.29.99 *
40     REM *******************************  
50    ADDR=40H
60     FOR I=0 TO 255
70     PRINT I,
80     REM ===== I2C Write ===============
90     I2CSTART 
100    IF DBY(18H)=0 I2CPUT (ADDR) ELSE 260
110    IF DBY(18H)=0 I2CPUT (I) ELSE 260
120    I2CSTOP 
130    REM ===== I2C Read ================
140    I2CSTART 
150    IF DBY(18H)=0 I2CPUT (ADDR.OR.1) ELSE 260
160    IF DBY(18H)=0 I2CGET B ELSE 260
170    PRINT B
180    I2CSTOP 
190    NEXT 
195    GOTO 10
200    REM ===== Wait for key ============
210   K=GET :  IF K>0 THEN 210
220    PRINT "Weiter?"
230   K=GET :  IF K=0 THEN 230
240    GOTO 60
250    REM ===== I2C Error ===============
260   STATUS=DBY(18H)
270    FOR J=1 TO 3 :  I2CSTOP  :  NEXT 
280    IF STATUS.AND.2=2 THEN  PRINT "Time out error!"
290    IF STATUS.AND.4=4 THEN  PRINT "Busy error!"
300    IF STATUS.AND.8=8 THEN  PRINT "No acknowlege error!"
310    GOTO 90
