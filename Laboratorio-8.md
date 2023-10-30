Laboratorio 8
================
Jeff
2023-10-25

# Parte 1

## 1. Reporte Detallado de Missing Data

    ##        Columna Porcentaje de Missing Values Tipo_de_Dato
    ## 1          Sex                    27.868852      integer
    ## 2          Age                    13.661202      integer
    ## 3        Parch                     6.557377      integer
    ## 4     Embarked                     6.557377    character
    ## 5         Fare                     4.371585    character
    ## 6        SibSp                     1.639344      numeric
    ## 7  PassengerId                     0.000000      integer
    ## 8     Survived                     0.000000      integer
    ## 9       Pclass                     0.000000    character
    ## 10        Name                     0.000000      numeric
    ## 11      Ticket                     0.000000    character
    ## 12       Cabin                     0.000000    character

- Sex (Género): Hay 51 valores faltantes, lo que representa
  aproximadamente el 27.87% de los datos. Esta columna contenía valores
  identificados con “?”, por lo que se decidió tratarlos como valores
  faltantes.
- Age (Edad): Hay 25 valores faltantes, lo que representa
  aproximadamente el 13.66% de los datos.
- Parch (Número de padres/hijos a bordo): Hay 12 valores faltantes, lo
  que representa aproximadamente el 6.56% de los datos.
- Embarked (Puerto de embarque): Hay 12 valores faltantes, lo que
  representa aproximadamente el 6.56% de los datos.
- Fare (Tarifa): Hay 8 valores faltantes, lo que representa
  aproximadamente el 4.37% de los datos.
- SibSp (Número de hermanos/esposos a bordo): Hay 3 valores faltantes,
  lo que representa aproximadamente el 1.64% de los datos.

## 2. Modelo para Imputación de Missing Values

Para realizar el reporte detallado de missing data, todos los valores
faltanes fueron tratados con un valor NA. Sin embargo y de manera más
específica, el modelo y los valores a utilizar para tratar los missing
values serían:

1.  Sex (Sexo)

- Método de Imputación: Basado en el título en la columna “Name”.
- Justificación: Los títulos en los nombres pueden dar pistas sobre el
  género de la persona. Por ejemplo, “Mr.” generalmente indica un
  hombre, mientras que “Miss”, “Mrs.” o “Ms.” indican una mujer. Estos
  títulos pueden ser extraídos y utilizados para inferir el género.
- Valor de Imputación: Asignar “male” si el título es “Mr.”, “Master” o
  similares. Asignar “female” si el título es “Miss”, “Mrs.”, “Ms.” o
  similares.

2.  Age (Edad)

- Método de Imputación: Regresión o KNN basado en otras variables
  correlacionadas.
- Justificación: Utilizar un modelo predictivo que tome en cuenta
  variables correlacionadas (como “SibSp”, “Parch”, “Fare”, “Pclass” y
  “Sex”) para predecir e imputar la edad. Estas variables pueden ayudar
  a dar una estimación más precisa de la edad, por ejemplo, un pasajero
  de primera clase podría tener una edad promedio mayor que un pasajero
  de tercera clase.
- Valor de Imputación: Los valores predichos por el modelo.

3.  SibSp (Número de hermanos/cónyuges a bordo) y Parch (Número de
    padres/hijos a bordo)

- Método de Imputación: Basado en el grupo familiar y el ticket.
- Justificación:
  - Grupos Familiares: Si otros miembros de la familia están presentes
    en el barco (identificables por el apellido y/o el número de
    ticket), podemos asumir que el número de hermanos/cónyuges y
    padres/hijos debería ser al menos 1.
  - Número de Ticket: Si otros pasajeros comparten el mismo número de
    ticket, es probable que estén viajando juntos, lo que podría indicar
    una relación familiar o de grupo.
- Valor de Imputación:
  - Si se identifican otros miembros de la familia o pasajeros con el
    mismo número de ticket, establecer “SibSp” o “Parch” a 1 o al número
    adecuado basado en la información disponible.
  - Si no se puede determinar la relación, imputar con 0, asumiendo que
    el pasajero viajaba solo.

4.  Fare (Tarifa)

- Método de Imputación: Basado en la mediana condicional a la “Pclass”.
- Justificación: La tarifa está estrechamente relacionada con la clase
  del pasajero. Por lo tanto, imputar la tarifa basándose en la mediana
  de la tarifa de otros pasajeros en la misma clase puede proporcionar
  una estimación más precisa.
- Valor de Imputación: La mediana de “Fare” para pasajeros en la misma
  “Pclass”.

5.  Embarked (Puerto de embarque)

- Método de Imputación: Moda condicional a “Pclass” y “Fare”.
- Justificación: El puerto de embarque podría estar relacionado con la
  clase del pasajero y la tarifa pagada. Imputar basándose en la moda de
  grupos similares puede proporcionar una estimación más precisa.
- Valor de Imputación: El valor más común de “Embarked” para pasajeros
  en la misma “Pclass” o rango de “Fare”.

## 3. Filas Completas

    ## Número de filas completas: 100

    ##     PassengerId Survived Pclass
    ## 1             4        1      1
    ## 2             7        0      1
    ## 3            22        1      2
    ## 4            55        0      1
    ## 5            63        0      1
    ## 6            67        1      2
    ## 7            97        0      1
    ## 8            98        1      1
    ## 9           103        0      1
    ## 10          119        0      1
    ## 11          125        0      1
    ## 12          140        0      1
    ## 13          149        0      2
    ## 14          171        0      1
    ## 15          175        0      1
    ## 16          178        0      1
    ## 17          210        1      1
    ## 18          225        1      1
    ## 19          263        0      1
    ## 20          264        0      1
    ## 21          293        0      2
    ## 22          298        0      1
    ## 23          306        1      1
    ## 24          308        1      1
    ## 25          310        1      1
    ## 26          319        1      1
    ## 27          320        1      1
    ## 28          328        1      2
    ## 29          330        1      1
    ## 30          333        0      1
    ## 31          337        0      1
    ## 32          340        0      1
    ## 33          346        1      2
    ## 34          357        1      1
    ## 35          367        1      1
    ## 36          370        1      1
    ## 37          371        1      1
    ## 38          378        0      1
    ## 39          391        1      1
    ## 40          394        1      1
    ## 41          395        1      3
    ## 42          413        1      1
    ## 43          435        0      1
    ## 44          436        1      1
    ## 45          446        1      1
    ## 46          453        0      1
    ## 47          454        1      1
    ## 48          457        0      1
    ## 49          461        1      1
    ## 50          474        1      2
    ## 51          487        1      1
    ## 52          493        0      1
    ## 53          497        1      1
    ## 54          499        0      1
    ## 55          505        1      1
    ## 56          516        0      1
    ## 57          517        1      2
    ## 58          521        1      1
    ## 59          537        0      1
    ## 60          545        0      1
    ## 61          551        1      1
    ## 62          557        1      1
    ## 63          559        1      1
    ## 64          572        1      1
    ## 65          578        1      1
    ## 66          582        1      1
    ## 67          584        0      1
    ## 68          592        1      1
    ## 69          600        1      1
    ## 70          610        1      1
    ## 71          626        0      1
    ## 72          628        1      1
    ## 73          633        1      1
    ## 74          642        1      1
    ## 75          646        1      1
    ## 76          660        0      1
    ## 77          672        0      1
    ## 78          680        1      1
    ## 79          691        1      1
    ## 80          699        0      1
    ## 81          708        1      1
    ## 82          711        1      1
    ## 83          713        1      1
    ## 84          716        0      3
    ## 85          725        1      1
    ## 86          742        0      1
    ## 87          743        1      1
    ## 88          746        0      1
    ## 89          752        1      3
    ## 90          760        1      1
    ## 91          766        1      1
    ## 92          783        0      1
    ## 93          797        1      1
    ## 94          803        1      1
    ## 95          810        1      1
    ## 96          821        1      1
    ## 97          824        1      3
    ## 98          836        1      1
    ## 99          854        1      1
    ## 100         868        0      1
    ##                                                                                   Name
    ## 1                                         Futrelle, Mrs. Jacques Heath (Lily May Peel)
    ## 2                                                              McCarthy, Mr. Timothy J
    ## 3                                                                Beesley, Mr. Lawrence
    ## 4                                                       Ostby, Mr. Engelhart Cornelius
    ## 5                                                          Harris, Mr. Henry Birkhardt
    ## 6                                                         Nye, Mrs. (Elizabeth Ramell)
    ## 7                                                            Goldschmidt, Mr. George B
    ## 8                                                      Greenfield, Mr. William Bertram
    ## 9                                                            White, Mr. Richard Frasar
    ## 10                                                            Baxter, Mr. Quigg Edmond
    ## 11                                                         White, Mr. Percival Wayland
    ## 12                                                                  Giglio, Mr. Victor
    ## 13                                            Navratil, Mr. Michel ("Louis M Hoffman")
    ## 14                                                           Van der hoef, Mr. Wyckoff
    ## 15                                                             Smith, Mr. James Clinch
    ## 16                                                          Isham, Miss. Ann Elizabeth
    ## 17                                                                    Blank, Mr. Henry
    ## 18                                                        Hoyt, Mr. Frederick Maxfield
    ## 19                                                                   Taussig, Mr. Emil
    ## 20                                                               Harrison, Mr. William
    ## 21                                                              Levy, Mr. Rene Jacques
    ## 22                                                        Allison, Miss. Helen Loraine
    ## 23                                                      Allison, Master. Hudson Trevor
    ## 24  Penasco y Castellana, Mrs. Victor de Satode (Maria Josefa Perez de Soto y Vallejo)
    ## 25                                                      Francatelli, Miss. Laura Mabel
    ## 26                                                            Wick, Miss. Mary Natalie
    ## 27                            Spedden, Mrs. Frederic Oakley (Margaretta Corning Stone)
    ## 28                                                             Ball, Mrs. (Ada E Hall)
    ## 29                                                        Hippach, Miss. Jean Gertrude
    ## 30                                                           Graham, Mr. George Edward
    ## 31                                                           Pears, Mr. Thomas Clinton
    ## 32                                                        Blackwell, Mr. Stephen Weart
    ## 33                                                       Brown, Miss. Amelia "Mildred"
    ## 34                                                         Bowerman, Miss. Elsie Edith
    ## 35                                    Warren, Mrs. Frank Manley (Anna Sophia Atkinson)
    ## 36                                                       Aubart, Mme. Leontine Pauline
    ## 37                                                         Harder, Mr. George Achilles
    ## 38                                                           Widener, Mr. Harry Elkins
    ## 39                                                          Carter, Mr. William Ernest
    ## 40                                                              Newell, Miss. Marjorie
    ## 41                                 Sandstrom, Mrs. Hjalmar (Agnes Charlotta Bengtsson)
    ## 42                                                              Minahan, Miss. Daisy E
    ## 43                                                           Silvey, Mr. William Baird
    ## 44                                                           Carter, Miss. Lucile Polk
    ## 45                                                           Dodge, Master. Washington
    ## 46                                                     Foreman, Mr. Benjamin Laventall
    ## 47                                                            Goldenberg, Mr. Samuel L
    ## 48                                                           Millet, Mr. Francis Davis
    ## 49                                                                 Anderson, Mr. Harry
    ## 50                                        Jerwan, Mrs. Amin S (Marie Marthe Thuillard)
    ## 51                                     Hoyt, Mrs. Frederick Maxfield (Jane Anne Forby)
    ## 52                                                          Molson, Mr. Harry Markland
    ## 53                                                      Eustis, Miss. Elizabeth Mussey
    ## 54                                     Allison, Mrs. Hudson J C (Bessie Waldo Daniels)
    ## 55                                                               Maioni, Miss. Roberta
    ## 56                                                        Walker, Mr. William Anderson
    ## 57                                                        Lemore, Mrs. (Amelia Milley)
    ## 58                                                               Perreault, Miss. Anne
    ## 59                                                   Butt, Major. Archibald Willingham
    ## 60                                                          Douglas, Mr. Walter Donald
    ## 61                                                         Thayer, Mr. John Borland Jr
    ## 62                   Duff Gordon, Lady. (Lucille Christiana Sutherland) ("Mrs Morgan")
    ## 63                                              Taussig, Mrs. Emil (Tillie Mandelbaum)
    ## 64                                       Appleton, Mrs. Edward Dale (Charlotte Lamson)
    ## 65                                           Silvey, Mrs. William Baird (Alice Munger)
    ## 66                                Thayer, Mrs. John Borland (Marian Longstreth Morris)
    ## 67                                                                 Ross, Mr. John Hugo
    ## 68                                     Stephenson, Mrs. Walter Bertram (Martha Eustis)
    ## 69                                        Duff Gordon, Sir. Cosmo Edmund ("Mr Morgan")
    ## 70                                                           Shutes, Miss. Elizabeth W
    ## 71                                                               Sutton, Mr. Frederick
    ## 72                                                       Longley, Miss. Gretchen Fiske
    ## 73                                                           Stahelin-Maeglin, Dr. Max
    ## 74                                                                Sagesser, Mlle. Emma
    ## 75                                                           Harper, Mr. Henry Sleeper
    ## 76                                                          Newell, Mr. Arthur Webster
    ## 77                                                              Davidson, Mr. Thornton
    ## 78                                                  Cardeza, Mr. Thomas Drake Martinez
    ## 79                                                             Dick, Mr. Albert Adrian
    ## 80                                                            Thayer, Mr. John Borland
    ## 81                                                   Calderhead, Mr. Edward Pennington
    ## 82                                    Mayne, Mlle. Berthe Antonine ("Mrs de Villiers")
    ## 83                                                            Taylor, Mr. Elmer Zebley
    ## 84                                          Soholt, Mr. Peter Andreas Lauritz Andersen
    ## 85                                                       Chambers, Mr. Norman Campbell
    ## 86                                                       Cavendish, Mr. Tyrell William
    ## 87                                               Ryerson, Miss. Susan Parker "Suzette"
    ## 88                                                        Crosby, Capt. Edward Gifford
    ## 89                                                                 Moor, Master. Meier
    ## 90                            Rothes, the Countess. of (Lucy Noel Martha Dyer-Edwards)
    ## 91                                                Hogeboom, Mrs. John C (Anna Andrews)
    ## 92                                                              Long, Mr. Milton Clyde
    ## 93                                                         Leader, Dr. Alice (Farnham)
    ## 94                                                 Carter, Master. William Thornton II
    ## 95                                      Chambers, Mrs. Norman Campbell (Bertha Griggs)
    ## 96                                  Hays, Mrs. Charles Melville (Clara Jennings Gregg)
    ## 97                                                                  Moor, Mrs. (Beila)
    ## 98                                                         Compton, Miss. Sara Rebecca
    ## 99                                                           Lines, Miss. Mary Conover
    ## 100                                               Roebling, Mr. Washington Augustus II
    ##        Sex   Age SibSp Parch          Ticket     Fare           Cabin Embarked
    ## 1   female 35.00     1     0          113803  53.1000            C123        S
    ## 2     male 54.00     0     0           17463  51.8625             E46        S
    ## 3     male 34.00     0     0          248698  13.0000             D56        S
    ## 4     male 65.00     0     1          113509  61.9792             B30        C
    ## 5     male 45.00     1     0           36973  83.4750             C83        S
    ## 6   female 29.00     0     0      C.A. 29395  10.5000             F33        S
    ## 7     male 71.00     0     0        PC 17754  34.6542              A5        C
    ## 8     male 23.00     0     1        PC 17759  63.3583         D10 D12        C
    ## 9     male 21.00     0     1           35281  77.2875             D26        S
    ## 10    male 24.00     0     1        PC 17558 247.5208         B58 B60        C
    ## 11    male 54.00     0     1           35281  77.2875             D26        S
    ## 12    male 24.00     0     0        PC 17593  79.2000             B86        C
    ## 13    male 36.50     0     2          230080  26.0000              F2        S
    ## 14    male 61.00     0     0          111240  33.5000             B19        S
    ## 15    male 56.00     0     0           17764  30.6958              A7        C
    ## 16  female 50.00     0     0        PC 17595  28.7125             C49        C
    ## 17    male 40.00     0     0          112277  31.0000             A31        C
    ## 18    male 38.00     1     0           19943  90.0000             C93        S
    ## 19    male 52.00     1     1          110413  79.6500             E67        S
    ## 20    male 40.00     0     0          112059   0.0000             B94        S
    ## 21    male 36.00     0     0   SC/Paris 2163  12.8750               D        C
    ## 22  female  2.00     1     2          113781 151.5500         C22 C26        S
    ## 23    male  0.92     1     2          113781 151.5500         C22 C26        S
    ## 24  female 17.00     1     0        PC 17758 108.9000             C65        C
    ## 25  female 30.00     0     0        PC 17485  56.9292             E36        C
    ## 26  female 31.00     0     2           36928 164.8667              C7        S
    ## 27  female 40.00     1     1           16966 134.5000             E34        C
    ## 28  female 36.00     0     0           28551  13.0000               D        S
    ## 29  female 16.00     0     1          111361  57.9792             B18        C
    ## 30    male 38.00     0     1        PC 17582 153.4625             C91        S
    ## 31    male 29.00     1     0          113776  66.6000              C2        S
    ## 32    male 45.00     0     0          113784  35.5000               T        S
    ## 33  female 24.00     0     0          248733  13.0000             F33        S
    ## 34  female 22.00     0     1          113505  55.0000             E33        S
    ## 35  female 60.00     1     0          110813  75.2500             D37        C
    ## 36  female 24.00     0     0        PC 17477  69.3000             B35        C
    ## 37    male 25.00     1     0           11765  55.4417             E50        C
    ## 38    male 27.00     0     2          113503 211.5000             C82        C
    ## 39    male 36.00     1     2          113760 120.0000         B96 B98        S
    ## 40  female 23.00     1     0           35273 113.2750             D36        C
    ## 41  female 24.00     0     2         PP 9549  16.7000              G6        S
    ## 42  female 33.00     1     0           19928  90.0000             C78        Q
    ## 43    male 50.00     1     0           13507  55.9000             E44        S
    ## 44  female 14.00     1     2          113760 120.0000         B96 B98        S
    ## 45    male  4.00     0     2           33638  81.8583             A34        S
    ## 46    male 30.00     0     0          113051  27.7500            C111        C
    ## 47    male 49.00     1     0           17453  89.1042             C92        C
    ## 48    male 65.00     0     0           13509  26.5500             E38        S
    ## 49    male 48.00     0     0           19952  26.5500             E12        S
    ## 50  female 23.00     0     0 SC/AH Basle 541  13.7917               D        C
    ## 51  female 35.00     1     0           19943  90.0000             C93        S
    ## 52    male 55.00     0     0          113787  30.5000             C30        S
    ## 53  female 54.00     1     0           36947  78.2667             D20        C
    ## 54  female 25.00     1     2          113781 151.5500         C22 C26        S
    ## 55  female 16.00     0     0          110152  86.5000             B79        S
    ## 56    male 47.00     0     0           36967  34.0208             D46        S
    ## 57  female 34.00     0     0      C.A. 34260  10.5000             F33        S
    ## 58  female 30.00     0     0           12749  93.5000             B73        S
    ## 59    male 45.00     0     0          113050  26.5500             B38        S
    ## 60    male 50.00     1     0        PC 17761 106.4250             C86        C
    ## 61    male 17.00     0     2           17421 110.8833             C70        C
    ## 62  female 48.00     1     0           11755  39.6000             A16        C
    ## 63  female 39.00     1     1          110413  79.6500             E67        S
    ## 64  female 53.00     2     0           11769  51.4792            C101        S
    ## 65  female 39.00     1     0           13507  55.9000             E44        S
    ## 66  female 39.00     1     1           17421 110.8833             C68        C
    ## 67    male 36.00     0     0           13049  40.1250             A10        C
    ## 68  female 52.00     1     0           36947  78.2667             D20        C
    ## 69    male 49.00     1     0        PC 17485  56.9292             A20        C
    ## 70  female 40.00     0     0        PC 17582 153.4625            C125        S
    ## 71    male 61.00     0     0           36963  32.3208             D50        S
    ## 72  female 21.00     0     0           13502  77.9583              D9        S
    ## 73    male 32.00     0     0           13214  30.5000             B50        C
    ## 74  female 24.00     0     0        PC 17477  69.3000             B35        C
    ## 75    male 48.00     1     0        PC 17572  76.7292             D33        C
    ## 76    male 58.00     0     2           35273 113.2750             D48        C
    ## 77    male 31.00     1     0      F.C. 12750  52.0000             B71        S
    ## 78    male 36.00     0     1        PC 17755 512.3292     B51 B53 B55        C
    ## 79    male 31.00     1     0           17474  57.0000             B20        S
    ## 80    male 49.00     1     1           17421 110.8833             C68        C
    ## 81    male 42.00     0     0        PC 17476  26.2875             E24        S
    ## 82  female 24.00     0     0        PC 17482  49.5042             C90        C
    ## 83    male 48.00     1     0           19996  52.0000            C126        S
    ## 84    male 19.00     0     0          348124   7.6500           F G73        S
    ## 85    male 27.00     1     0          113806  53.1000              E8        S
    ## 86    male 36.00     1     0           19877  78.8500             C46        S
    ## 87  female 21.00     2     2        PC 17608 262.3750 B57 B59 B63 B66        C
    ## 88    male 70.00     1     1       WE/P 5735  71.0000             B22        S
    ## 89    male  6.00     0     1          392096  12.4750            E121        S
    ## 90  female 33.00     0     0          110152  86.5000             B77        S
    ## 91  female 51.00     1     0           13502  77.9583             D11        S
    ## 92    male 29.00     0     0          113501  30.0000              D6        S
    ## 93  female 49.00     0     0           17465  25.9292             D17        S
    ## 94    male 11.00     1     2          113760 120.0000         B96 B98        S
    ## 95  female 33.00     1     0          113806  53.1000              E8        S
    ## 96  female 52.00     1     1           12749  93.5000             B69        S
    ## 97  female 27.00     0     1          392096  12.4750            E121        S
    ## 98  female 39.00     1     1        PC 17756  83.1583             E49        C
    ## 99  female 16.00     0     1        PC 17592  39.4000             D28        S
    ## 100   male 31.00     0     0        PC 17590  50.4958             A24        S

Hay un total de 100 filas completas.

### 3.1 Columnas Completas

    ##   Completa_PassengerId Completa_Survived Completa_Pclass Completa_Name
    ## 1                 TRUE              TRUE            TRUE          TRUE
    ##   Completa_Sex Completa_Age Completa_SibSp Completa_Parch Completa_Ticket
    ## 1        FALSE        FALSE          FALSE          FALSE            TRUE
    ##   Completa_Fare Completa_Cabin Completa_Embarked
    ## 1         FALSE           TRUE             FALSE

Las columnas completas son: PassengerID, Survived, Pclass, Name, Ticket
y Cabin.

## 4. Tratar cada columna que contiene missing values

### a. Imputación general

### b. Modelo Regresión Lineal

    ## 
    ##  iter imp variable
    ##   1   1  Age  SibSp  Parch  Fare
    ##   2   1  Age  SibSp  Parch  Fare
    ##   3   1  Age  SibSp  Parch  Fare
    ##   4   1  Age  SibSp  Parch  Fare
    ##   5   1  Age  SibSp  Parch  Fare

### c. Outliers: Standard deviation approach

### Outliers: Percentiles

## 5. Comparación de métodos

El modelo de regresión lineal fue la mejor opción para llenar los datos
faltantes en el conjunto de datos del Titanic. Esto se debe a que este
modelo puede entender y seguir las tendencias y patrones en los datos,
usando otras columnas relacionadas para hacer predicciones más exactas.
Así, en lugar de asignar a todos los datos faltantes un único valor como
la media o la mediana, la regresión lineal los llena de manera más
inteligente y específica. Cuando se comparó los resultados con la tabla
original de Titanic, vimos que los valores que llenó la regresión lineal
estaban más cercanos a los reales, mostrando que este método fue más
preciso y útil que los demás métodos que probamos.

### Conclusiones

El preprocesamiento de datos es una etapa crucial en cualquier flujo de
trabajo de ciencia de datos. Las decisiones tomadas durante esta etapa
pueden tener un impacto significativo en el rendimiento de los modelos
de aprendizaje automático. Es importante elegir métodos de imputación y
normalización adecuados basados en la naturaleza de los datos y el
problema específico que se está abordando. Además, siempre es crucial
validar los resultados y asegurarse de que los métodos aplicados hayan
mejorado efectivamente la calidad de los datos sin introducir sesgos
indeseados.

# Parte 2

## 1. Normalización de las columnas numéricas

## 2. Comparación de estadísticos

    ## $Standarization
    ## $Standarization$Titanic_MD
    ##   PassengerId           Survived           Pclass            Name          
    ##  Min.   :-1.835101   Min.   :-1.4279   Min.   :-0.3712   Length:183        
    ##  1st Qu.:-0.776621   1st Qu.:-1.4279   1st Qu.:-0.3712   Class :character  
    ##  Median : 0.006613   Median : 0.6965   Median :-0.3712   Mode  :character  
    ##  Mean   : 0.000000   Mean   : 0.0000   Mean   : 0.0000                     
    ##  3rd Qu.: 0.893065   3rd Qu.: 0.6965   3rd Qu.:-0.3712                     
    ##  Max.   : 1.759278   Max.   : 0.6965   Max.   : 3.5108                     
    ##                                                                            
    ##      Sex                 Age               SibSp             Parch        
    ##  Length:183         Min.   :-2.22319   Min.   :-0.7137   Min.   :-0.6132  
    ##  Class :character   1st Qu.:-0.74756   1st Qu.:-0.7137   1st Qu.:-0.6132  
    ##  Mode  :character   Median :-0.01231   Median :-0.7137   Median :-0.6132  
    ##                     Mean   : 0.00000   Mean   : 0.0000   Mean   : 0.0000  
    ##                     3rd Qu.: 0.78688   3rd Qu.: 0.8340   3rd Qu.: 0.7141  
    ##                     Max.   : 2.83280   Max.   : 3.9294   Max.   : 4.6958  
    ##                     NA's   :25         NA's   :3         NA's   :12       
    ##     Ticket               Fare            Cabin             Embarked        
    ##  Length:183         Min.   :-1.0251   Length:183         Length:183        
    ##  Class :character   1st Qu.:-0.6395   Class :character   Class :character  
    ##  Mode  :character   Median :-0.2860   Mode  :character   Mode  :character  
    ##                     Mean   : 0.0000                                        
    ##                     3rd Qu.: 0.1503                                        
    ##                     Max.   : 5.6263                                        
    ##                     NA's   :8                                              
    ## 
    ## $Standarization$Titanic
    ##   PassengerId           Survived           Pclass            Name          
    ##  Min.   :-1.835101   Min.   :-1.4279   Min.   :-0.3712   Length:183        
    ##  1st Qu.:-0.776621   1st Qu.:-1.4279   1st Qu.:-0.3712   Class :character  
    ##  Median : 0.006613   Median : 0.6965   Median :-0.3712   Mode  :character  
    ##  Mean   : 0.000000   Mean   : 0.0000   Mean   : 0.0000                     
    ##  3rd Qu.: 0.893065   3rd Qu.: 0.6965   3rd Qu.:-0.3712                     
    ##  Max.   : 1.759278   Max.   : 0.6965   Max.   : 3.5108                     
    ##      Sex                 Age               SibSp             Parch        
    ##  Length:183         Min.   :-2.22160   Min.   :-0.7211   Min.   :-0.6300  
    ##  Class :character   1st Qu.:-0.74626   1st Qu.:-0.7211   1st Qu.:-0.6300  
    ##  Mode  :character   Median : 0.02081   Median :-0.7211   Median :-0.6300  
    ##                     Mean   : 0.00000   Mean   : 0.0000   Mean   : 0.0000  
    ##                     3rd Qu.: 0.75592   3rd Qu.: 0.8313   3rd Qu.: 0.6952  
    ##                     Max.   : 2.83342   Max.   : 3.9362   Max.   : 4.6707  
    ##     Ticket               Fare            Cabin             Embarked        
    ##  Length:183         Min.   :-1.0306   Length:183         Length:183        
    ##  Class :character   1st Qu.:-0.6416   Class :character   Class :character  
    ##  Mode  :character   Median :-0.2840   Mode  :character   Mode  :character  
    ##                     Mean   : 0.0000                                        
    ##                     3rd Qu.: 0.1482                                        
    ##                     Max.   : 5.6799                                        
    ## 
    ## 
    ## $MinMaxScaling
    ## $MinMaxScaling$Titanic_MD
    ##   PassengerId        Survived          Pclass            Name          
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.00000   Length:183        
    ##  1st Qu.:0.2945   1st Qu.:0.0000   1st Qu.:0.00000   Class :character  
    ##  Median :0.5124   Median :1.0000   Median :0.00000   Mode  :character  
    ##  Mean   :0.5105   Mean   :0.6721   Mean   :0.09563                     
    ##  3rd Qu.:0.7590   3rd Qu.:1.0000   3rd Qu.:0.00000                     
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :1.00000                     
    ##                                                                        
    ##      Sex                 Age             SibSp            Parch       
    ##  Length:183         Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
    ##  Class :character   1st Qu.:0.2919   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Mode  :character   Median :0.4373   Median :0.0000   Median :0.0000  
    ##                     Mean   :0.4397   Mean   :0.1537   Mean   :0.1155  
    ##                     3rd Qu.:0.5953   3rd Qu.:0.3333   3rd Qu.:0.2500  
    ##                     Max.   :1.0000   Max.   :1.0000   Max.   :1.0000  
    ##                     NA's   :25       NA's   :3        NA's   :12      
    ##     Ticket               Fare            Cabin             Embarked        
    ##  Length:183         Min.   :0.00000   Length:183         Length:183        
    ##  Class :character   1st Qu.:0.05797   Class :character   Class :character  
    ##  Mode  :character   Median :0.11112   Mode  :character   Mode  :character  
    ##                     Mean   :0.15412                                        
    ##                     3rd Qu.:0.17672                                        
    ##                     Max.   :1.00000                                        
    ##                     NA's   :8                                              
    ## 
    ## $MinMaxScaling$Titanic
    ##   PassengerId        Survived          Pclass            Name          
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.00000   Length:183        
    ##  1st Qu.:0.2945   1st Qu.:0.0000   1st Qu.:0.00000   Class :character  
    ##  Median :0.5124   Median :1.0000   Median :0.00000   Mode  :character  
    ##  Mean   :0.5105   Mean   :0.6721   Mean   :0.09563                     
    ##  3rd Qu.:0.7590   3rd Qu.:1.0000   3rd Qu.:0.00000                     
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :1.00000                     
    ##      Sex                 Age             SibSp            Parch       
    ##  Length:183         Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
    ##  Class :character   1st Qu.:0.2919   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Mode  :character   Median :0.4436   Median :0.0000   Median :0.0000  
    ##                     Mean   :0.4395   Mean   :0.1548   Mean   :0.1189  
    ##                     3rd Qu.:0.5890   3rd Qu.:0.3333   3rd Qu.:0.2500  
    ##                     Max.   :1.0000   Max.   :1.0000   Max.   :1.0000  
    ##     Ticket               Fare            Cabin             Embarked        
    ##  Length:183         Min.   :0.00000   Length:183         Length:183        
    ##  Class :character   1st Qu.:0.05797   Class :character   Class :character  
    ##  Mode  :character   Median :0.11126   Mode  :character   Mode  :character  
    ##                     Mean   :0.15358                                        
    ##                     3rd Qu.:0.17567                                        
    ##                     Max.   :1.00000                                        
    ## 
    ## 
    ## $MaxAbsScaler
    ## $MaxAbsScaler$Titanic_MD
    ##   PassengerId          Survived          Pclass           Name          
    ##  Min.   :0.002247   Min.   :0.0000   Min.   :0.3333   Length:183        
    ##  1st Qu.:0.296067   1st Qu.:0.0000   1st Qu.:0.3333   Class :character  
    ##  Median :0.513483   Median :1.0000   Median :0.3333   Mode  :character  
    ##  Mean   :0.511647   Mean   :0.6721   Mean   :0.3971                     
    ##  3rd Qu.:0.759551   3rd Qu.:1.0000   3rd Qu.:0.3333                     
    ##  Max.   :1.000000   Max.   :1.0000   Max.   :1.0000                     
    ##                                                                         
    ##      Sex                 Age             SibSp            Parch       
    ##  Length:183         Min.   :0.0115   Min.   :0.0000   Min.   :0.0000  
    ##  Class :character   1st Qu.:0.3000   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Mode  :character   Median :0.4437   Median :0.0000   Median :0.0000  
    ##                     Mean   :0.4462   Mean   :0.1537   Mean   :0.1155  
    ##                     3rd Qu.:0.6000   3rd Qu.:0.3333   3rd Qu.:0.2500  
    ##                     Max.   :1.0000   Max.   :1.0000   Max.   :1.0000  
    ##                     NA's   :25       NA's   :3        NA's   :12      
    ##     Ticket               Fare            Cabin             Embarked        
    ##  Length:183         Min.   :0.00000   Length:183         Length:183        
    ##  Class :character   1st Qu.:0.05797   Class :character   Class :character  
    ##  Mode  :character   Median :0.11112   Mode  :character   Mode  :character  
    ##                     Mean   :0.15412                                        
    ##                     3rd Qu.:0.17672                                        
    ##                     Max.   :1.00000                                        
    ##                     NA's   :8                                              
    ## 
    ## $MaxAbsScaler$Titanic
    ##   PassengerId          Survived          Pclass           Name          
    ##  Min.   :0.002247   Min.   :0.0000   Min.   :0.3333   Length:183        
    ##  1st Qu.:0.296067   1st Qu.:0.0000   1st Qu.:0.3333   Class :character  
    ##  Median :0.513483   Median :1.0000   Median :0.3333   Mode  :character  
    ##  Mean   :0.511647   Mean   :0.6721   Mean   :0.3971                     
    ##  3rd Qu.:0.759551   3rd Qu.:1.0000   3rd Qu.:0.3333                     
    ##  Max.   :1.000000   Max.   :1.0000   Max.   :1.0000                     
    ##      Sex                 Age             SibSp            Parch       
    ##  Length:183         Min.   :0.0115   Min.   :0.0000   Min.   :0.0000  
    ##  Class :character   1st Qu.:0.3000   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Mode  :character   Median :0.4500   Median :0.0000   Median :0.0000  
    ##                     Mean   :0.4459   Mean   :0.1548   Mean   :0.1189  
    ##                     3rd Qu.:0.5938   3rd Qu.:0.3333   3rd Qu.:0.2500  
    ##                     Max.   :1.0000   Max.   :1.0000   Max.   :1.0000  
    ##     Ticket               Fare            Cabin             Embarked        
    ##  Length:183         Min.   :0.00000   Length:183         Length:183        
    ##  Class :character   1st Qu.:0.05797   Class :character   Class :character  
    ##  Mode  :character   Median :0.11126   Mode  :character   Mode  :character  
    ##                     Mean   :0.15358                                        
    ##                     3rd Qu.:0.17567                                        
    ##                     Max.   :1.00000

## Conclusiones

- La media de todas las variables numéricas se ha centrado en cero y la
  desviación estándar se ha escalado a uno. Al comparar “titanic_MD.csv”
  y “titanic.csv”, las estadísticas descriptivas son similares, lo que
  indica que la imputación y la normalización han sido efectivas para
  hacer que los conjuntos de datos sean comparables.
- Los valores de todas las variables numéricas están ahora en el rango
  de 0 a 1. Nuevamente, las estadísticas descriptivas entre
  “titanic_MD.csv” y “titanic.csv” son similares después de la
  normalización.
- Los datos se han escalado dividiendo cada valor por el valor absoluto
  máximo de la columna. Las estadísticas descriptivas son similares a
  las obtenidas con MinMax Scaling.
