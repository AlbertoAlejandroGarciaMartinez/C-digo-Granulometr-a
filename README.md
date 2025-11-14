# C-digo-Granulometr-
El desarrollo de una herramienta digital para modelar el análisis granulométrico requiere la aplicación rigurosa de la metodología de la programación, que incluye fases de análisis, diseño algorítmico, codificación y validación. El propósito del programa, dada su complejidad y los múltiples cálculos y decisiones que implica, se beneficiará enormemente del uso de programación modular y estructuras de datos organizadas.
A continuación, se detalla cómo los conceptos de programación extraídos de las fuentes se aplican a los requisitos de su práctica de ingeniería civil:
1. Análisis y Definición del Problema
La primera fase es el Análisis del problema, que implica comprender detalladamente qué debe hacer el programa.
• Entrada de Datos: Se requiere leer el diámetro de los tamices y las masas retenidas, además de los límites de plasticidad (LL, IP) si se requiere la clasificación completa [User Query].
    ◦ Estos datos de entrada deben ser almacenados en variables suscritas (arreglos o vectores). Los vectores son ideales para manejar colecciones de datos homogéneos (todos del mismo tipo), como la serie de diámetros o la serie de masas retenidas.
• Proceso (Cálculos): El algoritmo debe transformar los datos de entrada en resultados. Esto implica cálculos secuenciales (porcentajes) y la aplicación de fórmulas matemáticas para obtener y [User Query, 160].
    ◦ El cálculo de (Coeficiente de Uniformidad) y (Coeficiente de Curvatura), así como los diámetros , se realizarán mediante expresiones aritméticas que combinan variables, constantes y operadores.
• Salida (Resultados): Los resultados incluyen la curva granulométrica, los parámetros calculados y la clasificación SUCS/AASHTO, culminando en un reporte PDF [User Query, 87, 230].
2. Diseño del Algoritmo y Programación Modular
Dada la variedad de tareas (lectura, cálculos específicos, clasificación, graficación, generación de PDF), el diseño debe emplear la Programación Modular (diseño descendente). Esto permite dividir el problema en módulos más pequeños (funciones y procedimientos) para mejorar la legibilidad y la reutilización de código.
Las tareas clave se pueden asignar a módulos específicos:
Tarea (Módulo)	Tipo de Subprograma	Justificación según la Lógica de Programación
LeerDatosEnsayo	Procedimiento	Encargado de la Entrada de los tamices y masas. Debe utilizar ciclos (Mientras o Para) para leer repetidamente la información de los vectores de datos.
CalcularPorcentajes	Procedimiento/Función	Procesa los vectores de masas retenidas para obtener porcentajes. Utiliza ciclos y expresiones aritméticas.
CalcularD10/D30/D60	Función	Calcula el valor específico del diámetro a partir de la curva (requiere interpolación). Una función es apropiada ya que devuelve un único valor.
CalcularCuCc	Función	Calcula los coeficientes de uniformidad y curvatura, devolviendo un único valor (o dos, si se define como un objeto o estructura que encapsule ambos).
ClasificarSuelo	Procedimiento/Función	Aplica las reglas SUCS y AASHTO. Debe basarse fuertemente en estructuras de decisión (Selección).
GenerarReportePDF	Procedimiento	Maneja la salida final, incluyendo la impresión de los resultados y la gráfica.
3. Implementación de Lógica y Estructuras de Control
Uso de Arreglos (Vectores)
Los datos del ensayo (diámetros y masas) deben almacenarse en vectores. Los ciclos (Para-FinPara) son la forma más eficiente de ingresar y procesar esta colección de datos, permitiendo que el algoritmo se adapte a un número variable de tamices (dimensión).
Lógica de Clasificación (Estructuras Selectivas)
La clasificación del suelo (SUCS/AASHTO) es la parte más compleja en términos de lógica, ya que implica múltiples criterios interdependientes (grueso/fino, bien/mal graduado, plasticidad) [User Query]. Esto requiere el uso intensivo de estructuras de decisión.
• Decisiones Anidadas (Escalera): Para determinar el tipo de suelo según los rangos de y , se usarán estructuras Si-Entonces-SiNo anidadas (decisiones en cascada).
    ◦ Por ejemplo, determinar si el suelo es "Bien Graduado" o "Mal Graduado" dependerá de la evaluación de condiciones compuestas que utilizan operadores lógicos (Y o O) para conectar expresiones relacionales:
        ▪ Si (Cu >= 4) Y (1 < Cc) Y (Cc < 3) Entonces... [User Query].
• Clasificación por Plasticidad: Si se incluyen los límites de Atterberg (LL, IP), el algoritmo utilizará estas variables para la clasificación, lo que requiere otra serie de decisiones lógicas [User Query, 83].
4. Orientación a Objetos (Opcional, pero Recomendada)
Si bien las fuentes cubren la programación estructurada tradicional (algoritmos, pseudocódigo), la implementación en un lenguaje moderno como Python (sugerido en los ejercicios de programación) puede aprovechar la Programación Orientada a Objetos (POO).
Un enfoque orientado a objetos modelaría el proceso mediante la creación de una Clase Suelo que encapsularía:
• Atributos (Datos): Vectores de tamices y masas, LL, IP.
• Métodos (Comportamiento): Funciones para CalcularCuCc(), ClasificarSUCS(), GenerarGrafica(), y GenerarPDF().
La encapsulación de los datos (ocultación de la información) dentro del objeto asegura que los atributos del suelo solo sean manipulados a través de sus métodos definidos, mejorando la robustez y el mantenimiento del programa.
5. Documentación y Verificación
Finalmente, es crucial realizar una prueba de escritorio (validación) del algoritmo antes de la codificación final, siguiendo la lógica paso a paso con datos de prueba seleccionados. Esto garantiza que el algoritmo resuelva el problema y produzca los resultados esperados de manera confiable. La documentación del algoritmo y sus módulos es esencial para su mantenimiento futuro.



Su proyecto de análisis granulométrico es un excelente ejemplo de cómo la programación modular y el uso eficiente de estructuras de datos (arreglos) y estructuras de control (ciclos y decisiones) son fundamentales para resolver problemas complejos de ingeniería.
A continuación, se presenta un esquema algorítmico, utilizando el diseño descendente, dividiendo la solución en el programa principal (controlador) y varios submódulos (funciones y procedimientos) que cumplen tareas específicas:
-------------------------------------------------------------------------------- 
I. Estructura General y Declaración de Variables
El algoritmo principal se encarga de declarar las variables necesarias (globales) y coordinar la secuencia de ejecución de los módulos.
1. Variables Requeridas
Dado que se manejan listas de datos (tamices, masas) y resultados decimales (porcentajes, coeficientes), se deben usar vectores (arreglos unidimensionales) y tipos de datos Reales o Enteros.
Algoritmo ANALISIS_GRANULOMETRICO
    // Declaración de Variables Globales
    Definir N Como Entero                                 // Número de tamices
    Definir MasaTotal Como Real
    Definir LL, IP Como Real                              // Límites de Atterberg (Entrada opcional)
    
    // Vectores (Arrays) para almacenar datos e intermedios
    // Los vectores deben ser dimensionados dinámicamente o con un máximo predefinido [13, 14].
    Definir V_Diametros[N], V_Masas_Retenidas[N] Como Real
    Definir V_Masa_Acumulada[N], V_Pasa[N] Como Real      // Porcentaje que Pasa
    
    // Parámetros de Clasificación
    Definir D10, D30, D60, Cu, Cc Como Real
    Definir Clasificacion_SUCS, Clasificacion_AASHTO Como Cadena
    
    // Inicio del Programa Principal
    Inicio
        // 1. Entrada y pre-procesamiento
        LEER_DATOS_ENSAYO(N, V_Diametros, V_Masas_Retenidas)
        CALCULAR_PORCENTAJES(N, V_Masas_Retenidas, V_Masa_Acumulada, V_Pasa, MasaTotal)
        
        // 2. Cálculos de parámetros
        CALCULAR_PARAMETROS(N, V_Diametros, V_Pasa, D10, D30, D60, Cu, Cc)
        
        // 3. Clasificación
        LEER_LIMITES_ATTERBERG(LL, IP) // Opcional, si se requiere clasificación fina
        CLASIFICAR_SUELO(D10, D60, Cu, Cc, LL, IP, Clasificacion_SUCS, Clasificacion_AASHTO)
        
        // 4. Salida
        GENERAR_GRAFICA_Y_REPORTE(N, V_Diametros, V_Pasa, D10, D30, D60, Cu, Cc, Clasificacion_SUCS, Clasificacion_AASHTO)
        
    Fin
-------------------------------------------------------------------------------- 
II. Módulos de Entrada y Cálculos Secuenciales
Estos módulos utilizan estructuras secuenciales y ciclos (Para, Mientras) para procesar el conjunto de datos almacenados en los vectores.
1. Procedimiento: LEER_DATOS_ENSAYO
Este procedimiento se encarga de la entrada de datos, la cual debe realizarse mediante un ciclo iterando desde el primer tamiz hasta el último.
Procedimiento LEER_DATOS_ENSAYO(S N Por Referencia, S V_Diametros Por Referencia, S V_Masas_Retenidas Por Referencia)
    Definir I Como Entero
    
    Escribir "Ingrese el número de tamices (N):"
    Leer N
    
    // Asumiendo que los vectores se redimensionan automáticamente con N [14].
    
    Escribir "Introduzca los diámetros y masas retenidas:"
    Para I ← 1 Hasta N Hacer // Uso de un ciclo 'Para' [19, 20]
        Escribir "Diámetro del tamiz ", I, ":"
        Leer V_Diametros[I]
        Escribir "Masa retenida en tamiz ", I, " (g):"
        Leer V_Masas_Retenidas[I]
    Fin_Para
Fin_Procedimiento
2. Procedimiento: CALCULAR_PORCENTAJES
Calcula la masa total (usando un acumulador) y luego determina la masa acumulada y el porcentaje que pasa, lo cual requiere una secuencia de operaciones y ciclos.
Procedimiento CALCULAR_PORCENTAJES(E N, E V_Masas_Retenidas, S V_Masa_Acumulada, S V_Pasa, S MasaTotal Por Referencia)
    Definir I, MasaAcumulada_Temp Como Entero
    
    // Calcular Masa Total (Acumulación)
    MasaTotal ← 0
    Para I ← 1 Hasta N Hacer
        MasaTotal ← MasaTotal + V_Masas_Retenidas[I] // Uso de un acumulador [23]
    Fin_Para
    
    MasaAcumulada_Temp ← 0
    
    // Cálculo de porcentaje retenido y porcentaje que pasa
    Para I ← 1 Hasta N Hacer
        MasaAcumulada_Temp ← MasaAcumulada_Temp + V_Masas_Retenidas[I]
        
        // Cálculo del Porcentaje que Pasa (expresión aritmética) [24]
        // Se calcula el porcentaje que pasa restando el porcentaje retenido acumulado del 100%.
        V_Pasa[I] ← (1 - (MasaAcumulada_Temp / MasaTotal)) * 100 
    Fin_Para
Fin_Procedimiento
-------------------------------------------------------------------------------- 
III. Módulos de Cálculo de Parámetros ()
Estos módulos implican la aplicación de fórmulas directas y la búsqueda de valores por interpolación dentro del vector [User Query].
1. Procedimiento: CALCULAR_PARAMETROS
Este módulo llama a una función para obtener (Diámetros) y luego calcula los coeficientes y .
Procedimiento CALCULAR_PARAMETROS(E N, E V_Diametros, E V_Pasa, S D10, S D30, S D60, S Cu, S Cc)
    
    // 1. Búsqueda de Diámetros (Requiere función de interpolación)
    D10 ← OBTENER_D(10, N, V_Diametros, V_Pasa)
    D30 ← OBTENER_D(30, N, V_Diametros, V_Pasa)
    D60 ← OBTENER_D(60, N, V_Diametros, V_Pasa)
    
    // 2. Cálculo de Coeficientes (Expresiones aritméticas)
    Cu ← D60 / D10                                // Coeficiente de Uniformidad [User Query]
    Cc ← (D30^2) / (D60 * D10)                    // Coeficiente de Curvatura [User Query]
    
Fin_Procedimiento
Nota sobre OBTENER_D: La función OBTENER_D requeriría un ciclo para buscar el índice donde el porcentaje que pasa (V_Pasa) es inmediatamente mayor y menor que el valor buscado (10, 30, o 60), y luego aplicar una fórmula de interpolación. Este es un ejemplo de búsqueda secuencial en un vector.
-------------------------------------------------------------------------------- 
IV. Módulo de Clasificación (Estructuras de Decisión)
La clasificación según SUCS y AASHTO se basa en el porcentaje de material grueso/fino y en los coeficientes y . Esto requiere el uso intensivo de estructuras selectivas anidadas o en cascada.
1. Función/Procedimiento: CLASIFICAR_SUELO
Este algoritmo utiliza decisiones para determinar la clasificación granulométrica y de forma (Bien Graduado/Mal Graduado) [User Query].
Procedimiento CLASIFICAR_SUELO(E D10, E D60, E Cu, E Cc, E LL, E IP, S Clasificacion_SUCS, S Clasificacion_AASHTO)
    
    Definir P_Fino, P_Grava, P_Arena Como Real
    // Necesitaríamos calcular los porcentajes de Grava, Arena y Finos 
    // (P_Grava y P_Arena dependen de los tamices #4 y #200, respectivamente, 
    // que se deben obtener de V_Pasa)

    // A. CLASIFICACIÓN GRANULOMÉTRICA (Grava/Arena/Limo/Arcilla)
    
    // Ejemplo simplificado de la lógica:
    
    Si P_Grava > P_Arena Entonces
        // El suelo es predominantemente Grava (Grueso)
        
        Si P_Fino < 5 Entonces // Pocos finos
            Si (Cu >= 4) Y (Cc > 1) Y (Cc < 3) Entonces // Decisión compuesta [30, 31]
                Clasificacion_SUCS ← "GW (Grava Bien Graduada)"
            SiNo
                Clasificacion_SUCS ← "GP (Grava Mal Graduada)"
            Fin_Si
        
        SiNo Si P_Fino >= 12 Entonces // Muchos finos, requiere Límites de Atterberg
            // ... (Lógica de plasticidad: ML, CL, MH, CH)
            Si IP < 4 Entonces
                Clasificacion_SUCS ← "GM (Grava Limosa)"
            SiNo
                Clasificacion_SUCS ← "GC (Grava Arcillosa)"
            Fin_Si
        SiNo // P_Fino está entre 5% y 12% (Doble Símbolo)
            Clasificacion_SUCS ← "GP-GM" // Ejemplo
        Fin_Si
        
    SiNo // El suelo es predominantemente Arena (Grueso)
        
        Si P_Fino < 5 Entonces // Pocos finos
            Si (Cu >= 6) Y (Cc > 1) Y (Cc < 3) Entonces
                Clasificacion_SUCS ← "SW (Arena Bien Graduada)"
            SiNo
                Clasificacion_SUCS ← "SP (Arena Mal Graduada)"
            Fin_Si
            
        SiNo Si P_Fino >= 12 Entonces
            // ... (Lógica de plasticidad: ML, CL, MH, CH)
            Clasificacion_SUCS ← "SM o SC" // Clasificación por plasticidad
        Fin_Si
        
    Fin_Si
    
    // B. Clasificación AASHTO (requiere una serie separada de decisiones en cascada) [26]
    // ...
    
Fin_Procedimiento
-------------------------------------------------------------------------------- 
V. Módulo de Salida
El último módulo se enfoca en presentar los resultados al usuario, incluyendo la generación de la gráfica y el reporte, lo cual es una secuencia de acciones de salida.
Procedimiento GENERAR_GRAFICA_Y_REPORTE(E N, E V_Diametros, E V_Pasa, E D10, E D30, E D60, E Cu, E Cc, E Clasificacion_SUCS, E Clasificacion_AASHTO)
    
    // 1. Mostrar resultados en pantalla
    Escribir "*** REPORTE DE ANÁLISIS GRANULOMÉTRICO ***"
    Escribir "Diámetro D10: ", D10
    Escribir "Diámetro D30: ", D30
    Escribir "Diámetro D60: ", D60
    Escribir "Coeficiente de Uniformidad (Cu): ", Cu
    Escribir "Coeficiente de Curvatura (Cc): ", Cc
    Escribir "Clasificación SUCS: ", Clasificacion_SUCS
    Escribir "Clasificación AASHTO: ", Clasificacion_AASHTO
    
    // 2. Generación de la Curva Granulométrica (gráfica en escala logarítmica)
    // Se requiere una librería/función específica para trazar los vectores V_Diametros vs V_Pasa
    LLAMAR_FUNCION_GRAFICACION(V_Diametros, V_Pasa, "Curva Granulométrica")
    
    // 3. Generación del reporte PDF (implica la salida a un archivo externo)
    LLAMAR_PROCEDIMIENTO_IMPRIMIR_PDF(TODOS_LOS_RESULTADOS)
    
Fin_Procedimiento
La implementación práctica en Python (como se sugiere en la fuente) requerirá que cada uno de estos bloques de pseudocódigo se traduzca a funciones o métodos, aprovechando las capacidades de Python para manejar vectores (listas/arreglos de NumPy) y bibliotecas de graficación (como Matplotlib) y manejo de archivos (PDF). Recuerde que la lógica es lo importante, independientemente del lenguaje de programación final
