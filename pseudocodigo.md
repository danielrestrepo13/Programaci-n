## Pseudocódigo - Juego de Rummy

INICIO

    FUNCION reglas_rummy()
        IMPRIMIR "==== REGLAS DE RUMMY ===="
        IMPRIMIR "- Se usa un mazo estándar de 52 cartas."
        IMPRIMIR "- Cada jugador recibe 3 cartas al inicio."
        IMPRIMIR "- En cada turno, puedes robar una carta y descartar una."
        IMPRIMIR "- Gana quien forme un trío de cartas del mismo valor primero."
    FIN_FUNCION

    FUNCION crear_mazo()
        DEFINIR valores COMO lista de ["2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A"]
        CREAR mazo duplicando valores 4 veces (52 cartas)
        MEZCLAR mazo aleatoriamente

        CREAR lista vacía mano
        PARA i DESDE 1 HASTA 3
            REMOVER carta del mazo y AGREGAR a mano
        FIN_PARA

        RETORNAR (mano, mazo)
    FIN_FUNCION

    FUNCION validar_ganador(mano)
        PARA CADA carta EN mano
            SI carta != mano[0] ENTONCES
                RETORNAR FALSO
            FIN_SI
        FIN_PARA
        RETORNAR VERDADERO
    FIN_FUNCION

    FUNCION jugar_rummy()
        (mano_jugador, mazo) = crear_mazo()
        (mano_computadora, mazo) = crear_mazo()
        pila_descarte = [mazo.pop()]  // Se inicia la pila de descarte con una carta

        turnos = 0

        MIENTRAS VERDADERO
            turnos = turnos + 1
            IMPRIMIR "Turno", turnos
            IMPRIMIR "Tu mano:", mano_jugador
            IMPRIMIR "Carta en la pila de descarte:", última carta en pila_descarte

            SI validar_ganador(mano_jugador) ENTONCES
                IMPRIMIR "¡Ganaste con la mano!", mano_jugador
                SALIR_DEL_BUCLE
            FIN_SI

            // TURNO DEL JUGADOR
            REPETIR
                IMPRIMIR "Elige una opción:"
                IMPRIMIR "1. Robar del mazo"
                IMPRIMIR "2. Robar de la pila de descarte"
                LEER opcion

                SI opcion == "1" Y mazo NO está vacío ENTONCES
                    carta_robada = remover carta del mazo
                    SALIR_DEL_BUCLE
                SI opcion == "2" Y pila_descarte NO está vacía ENTONCES
                    carta_robada = remover carta de pila_descarte
                    SALIR_DEL_BUCLE
                SINO
                    IMPRIMIR "Opción inválida o no hay cartas disponibles."
                FIN_SI
            HASTA opcion válida

            IMPRIMIR "Robaste la carta:", carta_robada

            REPETIR
                IMPRIMIR "¿Qué carta deseas descartar?"
                LEER carta_descartar
                SI carta_descartar está en mano_jugador O carta_descartar == carta_robada ENTONCES
                    SALIR_DEL_BUCLE
                SINO
                    IMPRIMIR "Esa carta no está en tu mano, intenta de nuevo."
                FIN_SI
            HASTA carta válida

            AGREGAR carta_descartar a pila_descarte
            SI carta_descartar != carta_robada ENTONCES
                REMOVER carta_descartar de mano_jugador
                AGREGAR carta_robada a mano_jugador
            FIN_SI

            SI validar_ganador(mano_computadora) ENTONCES
                IMPRIMIR "La computadora ha ganado con la mano:", mano_computadora
                SALIR_DEL_BUCLE
            FIN_SI

            // TURNO DE LA COMPUTADORA
            SI pila_descarte NO está vacía Y (azar elige tomar de descarte O mazo está vacío) ENTONCES
                carta_robada = remover carta de pila_descarte
            SINO
                carta_robada = remover carta de mazo
            FIN_SI

            carta_descartar = elegir aleatoriamente una carta de mano_computadora
            REMOVER carta_descartar de mano_computadora
            AGREGAR carta_robada a mano_computadora
            AGREGAR carta_descartar a pila_descarte

            IMPRIMIR "La computadora robó una carta y descartó", carta_descartar
        FIN_MIENTRAS

    FIN_FUNCION

    FUNCION principal()
        reglas_rummy()
        jugar_rummy()
    FIN_FUNCION

    principal()

FIN
