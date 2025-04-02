    PROCESSOR 16F877A
    #include <xc.inc>

    ; Definir el vector de reset
    PSECT udata_acs
    resetVector:
        GOTO inicio  ; Saltar al inicio del programa

    ; Sección de código principal
    PSECT code
inicio:
    BANKSEL TRISB
    CLRF TRISB      ; Configurar PORTB como salida
    
    BANKSEL PORTB 
    CLRF PORTB  ;; Asegura que los LEDs comienzan apagados
    
loop:
    BSF PORTB, 0    ; Encender LED en RB0
    BCF PORTB, 1    ; Apagar LED EN RB1
    CALL  delay     ; Espera un tiempo
   
    BCF PORTB, 0 ; Apagar LED en RB0
    BSF PORTB, 1 ; Encender LED en RB1
    CALL delay   ; Espere un tiempo
    
    BSF PORTB, 2   ; Encender LED en RB2
    CALL delay ; Espere un tiempo
    
    BCF PORTB, 2 ; Apagar LED EN RB2
    CALL delay  ; Espere un tiempo

    GOTO loop       ; Mantenerse en bucle infinito
    
   
    

    delay:
        MOVLW 0xFF  
        MOVWF 0x20  
    loop1:
        MOVLW 0xFF  
        MOVWF 0x21  
    loop2:
        DECFSZ 0x21, f
        GOTO loop2
        DECFSZ 0x20, f
        GOTO loop1
        RETURN

    END
