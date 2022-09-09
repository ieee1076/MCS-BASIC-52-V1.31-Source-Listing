10     REM *****************************************
20     REM *  I2C-Communication with MCS-51-BASIC  *
30     REM *   over Ports 1.5 (SCL) and 1.6 (SDA)  *
40     REM *                                       *
50     REM *      (C) H.-J. Boehling 07.29.99      *
60     REM *    http://home.nexgo.de/H.Boehling    *
70     REM *                                       *
80     REM *****************************************
90     REM
100   CLKL=0DFH : CLKH=20H : DATL=0BFH : DATH=40H
110    REM +++ I2C Test ++++++++++++++++++++++++++++
120    REM This test sends out value 0 to 255 to a PCF8574 and read it back 
130   ADDR=040H :  REM I2C address
140    FOR BYTEOUT=0 TO 255
150    GOSUB 270
160    IF (ACK.OR.OUT)>0 THEN 220
170    GOSUB 350
180    IF (ACK.OR.OUT)>0 THEN 220
190    PRINT "Read back:",BYTEIN
200    NEXT 
210    GOTO 130
220    REM +++ I2C Transmission error ++++++++++++++
230    GOSUB 810 :  REM Stop condition
240    IF ACK>0 THEN  PRINT "ACK failed!"
250    IF OUT>0 THEN  PRINT "Time out!"
260    GOTO 150
270    REM *** Send Data to I2C ********************
280    GOSUB 730 :  REM Start condition
290   BOUT=ADDR.AND.0FEH :  REM Set write mode
300    GOSUB 420 :  REM Send address out
310   BOUT=BYTEOUT
320    GOSUB 420 :  REM Send byte out 
330    GOSUB 810 :  REM Stop condition
340    RETURN 
350    REM *** Read Data from I2C ******************
360    GOSUB 730 :  REM Start condition  
370   BOUT=ADDR.OR.1 :  REM Set read mode
380    GOSUB 420 :  REM Send address out
390    GOSUB 580 :  REM read byte in 
400    GOSUB 810 :  REM Stop condition
410    RETURN 
420    REM === I2C Send Byte =======================
430   BIT=80H : WERT=0.5
440    FOR I=1 TO 8
450   SDA=(BOUT.AND.BIT)*WERT :  REM Set data to bit of byte
460   BIT=BIT/2 : WERT=WERT+WERT :  REM Set pointer to next bit
470    GOSUB 860 :  REM Make clock low
480   PT1=PORT1.AND.DATL : PORT1=PT1.OR.SDA :  REM Send bit out
490    GOSUB 890 :  REM Make clock high
500    NEXT 
510    REM --- Get ACK -----------------------------
520    GOSUB 860 :  REM Make clock low
530    GOSUB 950 :  REM Make data high
540    GOSUB 890 :  REM Make clock high
550   ACK=PORT1.AND.DATH :  REM If data is high ACK failed
560    GOSUB 860 :  REM Make clock low
570    RETURN 
580    REM === I2C Get Byte ========================
590   BYTEIN=0 : WERT=0.5
600    FOR I=1 TO 8
610    GOSUB 860 :  REM Make clock low
620    GOSUB 950 :  REM Make data high
630    GOSUB 890 :  REM Make clock high
640   SDA=(PORT1.AND.DATH)/WERT :  REM Read data...
650   BYTEIN=BYTEIN.OR.SDA :  REM ...to bit of byte
660   WERT=WERT+WERT :  REM Set pointer to next bit
670    NEXT 
680    REM --- Do ACK -----------------------------
690    GOSUB 860 :  REM Make clock low
700    GOSUB 920 :  REM Make data low to set ACK oK
710    GOSUB 890 :  REM Make clock high
720    RETURN 
730    REM === I2C Start condition ================
740   OUT=0 :  REM Reset time out counter
750    GOSUB 950 :  REM Make data high
760    GOSUB 890 :  REM Make clock high
770    IF OUT=3 THEN 800 :  REM Wait 3 times for clock and data high 
780    IF (PORT1.AND.60H)<>60H THEN OUT=OUT+1 :  GOTO 770
790    GOSUB 920 :  REM Make data low (start condition)  
800    RETURN 
810    REM === I2C Stop condition =================
820    GOSUB 920 :  REM Make data low
830    GOSUB 890 :  REM Make clock high
840    GOSUB 950 :  REM Make data high
850    RETURN 
860    REM --- Set Port 1.5 (SCL) to Low ----------
870   PT1=PORT1.AND.CLKL : PORT1=PT1
880    RETURN 
890    REM --- Set Port 1.5 (SCL) to High ---------
900   PT1=PORT1.OR.CLKH : PORT1=PT1
910    RETURN 
920    REM --- Set Port 1.6 (SDA) to Low ----------
930   PT1=PORT1.AND.DATL : PORT1=PT1
940    RETURN 
950    REM --- Set Port 1.6 (SDA) to High ---------
960   PT1=PORT1.OR.DATH : PORT1=PT1
970    RETURN 
