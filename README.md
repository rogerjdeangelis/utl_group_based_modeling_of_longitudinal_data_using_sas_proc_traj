# utl_group_based_modeling_of_longitudinal_data_using_sas_proc_traj
Group-based modeling of longitudinal data using SAS proc traj. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Group-based modeling of longitudinal data using SAS proc traj

    see Bobby Jones PhD
    https://www.andrew.cmu.edu/user/bjones/download.htm

    Macro trajplotnew is on the end of this.


    INPUT (full data below)
    =====

      DATA_ID    DATA_X1    DATA_X2    DATA_X3     DATA_X4    DATA_X5     DATA_X6    TIME_ID    TIME_1    TIME_2    TIME_3    TIME_4    TIME_5    TIME_6

          1       5.6589     9.3398     3.7703     17.3607     8.8243      9.2814        1         1         2         3         4         5         6
          2      23.5928    11.7522     7.6841     12.8298    13.0018      9.6649        2         1         2         3         4         5         6
          3      15.4690     8.7565     6.4932     11.2608    10.4200     17.4055        3         1         2         3         4         5         6
          4       7.3120    11.6875    12.4762      8.8904     6.5216      7.7012        4         1         2         3         4         5         6
          5      12.8437    11.0877     7.6500     10.2689    12.4532     11.5574        5         1         2         3         4         5         6
          6       3.5220    15.2850     7.8603      7.1138    17.9538      4.1676        6         1         2         3         4         5         6
          7      21.1623     7.8593     2.1487      7.7093    11.8849      7.2252        7         1         2         3         4         5         6
          8       4.8269    17.2334     3.8911     12.4933    10.2298     11.9138        8         1         2         3         4         5         6
     ....


    PROCESS
    =======

    proc traj data=have
             out = want_of
         outplot = want_op
         outstat = want_os ci95M;
      id data_ID;
      data_x1-data_x6;
      indep time_1-time_6;
      order 2 2 2 2;
      model cnorm;
      max 130;
    run;quit;

    * create the plot;
    %include "c:/oto/trajplotnew.sas";

    options orientation=landscape;
    ods pdf file="d:/taj/pdf/utl_group_based_modeling_of_longitudinal_data_using_sas_proc_traj.pdf";
    ods graphics on / reset=all border=on height=7in width=10in
    %trajplotnew(op,os,,"Mockdata","6 month paid");
    run;quit;
    ods pdf close;


    OUTPUT
    ======

    PRINTED OUTPUT

                            Maximum Likelihood Estimates
                            Model: Censored Normal (CNORM)

                                       Standard       T for H0:
     Group   Parameter    Estimate        Error     Parameter=0   Prob > |T|

     1       Intercept    -3.88723   2413.67456          -0.002       0.9987

     2       Intercept    10.12817      1.99722           5.071       0.0000
             Linear        0.08336      1.30659           0.064       0.9491
             Quadratic    -0.02593      0.18272          -0.142       0.8872

     3       Intercept   -14.97350      4.46576          -3.353       0.0008
             Linear       30.41782      2.92162          10.411       0.0000
             Quadratic    -2.36117      0.40857          -5.779       0.0000

     4       Intercept    48.69136      2.57835          18.885       0.0000
             Linear       -4.71569      1.68682          -2.796       0.0053
             Quadratic    -0.04105      0.23589          -0.174       0.8619

     5       Intercept   109.43984      2.23288          49.013       0.0000
             Linear      -16.67056      1.46081         -11.412       0.0000
             Quadratic     0.05674      0.20429           0.278       0.7813

             Sigma         7.80791      0.19989          39.061       0.0000

             Group membership
     1             (%)     0.00021      0.01296           0.016       0.9869
     2             (%)    38.46199      4.31426           8.915       0.0000
     3             (%)     7.69226      2.36298           3.255       0.0012
     4             (%)    23.07634      3.73623           6.176       0.0000
     5             (%)    30.76919      4.09281           7.518       0.0000

     BIC= -2934.27 (N=780)  BIC= -2918.14 (N=130)  AIC= -2892.33  L= -2874.33


    GROUP NUMBER ADDED

    WANT_OF total obs=130

      GROUP DATA_ID  DATA_X1  DATA_X2  DATA_X3  DATA_X4  DATA_X5  DATA_X6  TIME_1  TIME_2  TIME_3  TIME_4  TIME_5  TIME_6  GRP1PRB  GRP2PRB  GRP3PRB  GRP4PRB

        1       1      5.66     9.34     3.77    17.36     8.82     9.28      1       2       3       4       5       6      1         0        0        0
        1       2     23.59    11.75     7.68    12.83    13.00     9.66      1       2       3       4       5       6      1         0        0        0
        1       3     15.47     8.76     6.49    11.26    10.42    17.41      1       2       3       4       5       6      1         0        0        0
        1       4      7.31    11.69    12.48     8.89     6.52     7.70      1       2       3       4       5       6      1         0        0        0
        1       5     12.84    11.09     7.65    10.27    12.45    11.56      1       2       3       4       5       6      1         0        0        0

        2     127     45.90    46.46    15.61    24.95    25.36    22.73      1       2       3       4       5       6      0         1        0        0
        2     128     59.17    33.16    37.38    31.25    28.75    14.89      1       2       3       4       5       6      0         1        0        0
        2     129     51.15    36.98    22.37    27.22    17.23    19.60      1       2       3       4       5       6      0         1        0        0
        2     130     55.05    44.90    32.51    45.27    17.18     5.36      1       2       3       4       5       6      0         1        0        0


    PLOT TABLE
    ==========

    WANT_OP total obs=6

       T     AVG1      AVG2     AVG3      AVG4     PRED1     PRED2     PRED3     PRED4     L95M1     U95M1     L95M2     U95M2     L95M3     U95M3     L95M4     U95M4

       1   10.4747   45.0561   11.236   93.2505   10.5377   43.9346   13.2348   92.8259   7.86661   13.2088   41.3775   46.4917    7.5592   18.9104   90.6114   95.040
       2    9.7370   37.0473   39.467   74.7440   10.5427   39.0958   36.4175   76.3257   8.90936   12.1761   37.5321   40.6595   33.7091   39.1259   74.9716   77.679
       3   10.1691   34.0545   55.410   61.4588   10.5009   34.1748   55.0294   59.9389   8.70436   12.2974   32.4549   35.8948   52.0513   58.0075   58.4499   61.428
       4    9.8086   30.6091   67.953   44.3505   10.4124   29.1719   68.9190   43.6656   8.61491   12.2098   27.4478   30.8961   65.9409   71.8972   42.1765   45.154
       5   10.6719   24.1595   75.915   25.7802   10.2775   24.0888   78.0864   27.5061   8.64192   11.9131   22.4937   25.6839   75.3782   80.7946   26.1446   28.867
       6    9.2989   18.4564   84.086   12.1370   10.0968   18.9391   82.5314   11.7054   7.42070   12.7729   16.1392   21.7390   78.1026   86.9603    8.7652   14.645


    BETA (coeficients for quadratic)

    WANT_OS total obs=4

    Obs      BETA0        BETA1      BETA2     BETA3    BETA4    BETA5       PI

     1       10.128      0.0833    -0.02593      .        .        .      38.4621
     2       48.691     -4.7157    -0.04106      .        .        .      23.0764
     3      -14.973     30.4176    -2.36114      .        .        .       7.6923
     4      109.440    -16.6704     0.05672      .        .        .      30.7692

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    data have;
       input data_id data_x1-data_x6 time_id time_1-time_6  @@;
    cards4;
    1 5.66 9.34 3.77 17.36 8.82 9.28 1 1 2 3 4 5 6 2 23.59 11.75 7.68 12.83 13 9.66
    2 1 2 3 4 5 6 3 15.47  8.76 6.49 11.26 10.42 17.41 3 1 2 3 4 5 6 4 7.31 11.69
    12.48 8.89 6.52 7.7 4 1 2 3 4 5 6 5 12.84 11.09 7.65 10.27 12.45 11.56 5 1 2 3 4
    5 6 6 3.52 15.29 7.86 7.11 17.95 4.17 6 1 2 3 4 5 6 7 21.16 7.86 2.15 7.71 11.88
    7.23 7 1 2 3 4 5 6 8 4.83 17.23 3.89 12.49 10.23 11.91 8 1 2 3 4 5 6 9 8.64 9.5
    8.45 12.65 6.79 1.95 9 1 2 3 4 5 6 10 9.85 9.7 10.13 11.62 6.64 8.43 10 1 2 3 4
    5 6 11 8.58 10.39 5.57 8.23 16.15 3.67 11 1 2 3 4 5 6 12 6.19 2.68 8.66 4.75
    10.02 11.61 12 1 2 3 4 5 6 13 0.98 9.83 14.44 7.79 8.38 19.04 13 1 2 3 4 5 6 14
    7.08 13.29 8.28 18.24 5.46 8.78 14 1 2 3 4 5 6 15 20.6 10.45 21.66 6.23 14.18
    9.04 15 1 2 3 4 5 6 16 11.17 9.54 7.95 1.15 8.67 10.93 16 1 2 3 4 5 6 17 12.38
    15.44 15.45 9.36 9.94 7.78 17 1 2 3 4 5 6 18 7.37 3.49 9.81 17.8 16.49 9.06 18 1
    2 3 4 5 6 19 0.28 17.56 14.12 14.03 15.43 15.45 19 1 2 3 4 5 6 20 6.97 20.07
    9.32 16.51 19.39 1.46 20 1 2 3 4 5 6 21 10.31 12.45 7.91 6.08 11.33 1.39 21 1 2
    3 4 5 6 22 10.45 4.53 6.64 16.63 8.89 16.18 22 1 2 3 4 5 6 23 13.23 14.27 13.31
    6.68 9.89 0.66 23 1 2 3 4 5 6 24 16.68 4.69 6.56 18.02 15.44 9.22 24 1 2 3 4 5 6
    25 18.43 2.54 8.5 9.05 4.76 8.75 25 1 2 3 4 5 6 26 6.2 16.45 10.89 11.36 10.79
    11.3 26 1 2 3 4 5 6 27 11.19 10.51 9.85 15.2 9.16 5.4 27 1 2 3 4 5 6 28 10.03
    9.81 9.4 6.93 18.35 8.14 28 1 2 3 4 5 6 29 17.23 4.67 15.33 12.21 10.26 16.29 29
    1 2 3 4 5 6 30 9.23 11.11 6.25 12.86 19.68 7.23 30 1 2 3 4 5 6 31 21.94 12.42
    13.33 9.04 8.63 19.89 31 1 2 3 4 5 6 32 8.51 8.78 5.38 2.78 12.75 0.39 32 1 2 3
    4 5 6 33 16.57 12.82 15.75 4.31 11.31 3.33 33 1 2 3 4 5 6 34 11.1 8.91 4.64
    10.36 12.62 11.83 34 1 2 3 4 5 6 35 13.09 5.44 7.63 9.32 14.16 7.42 35 1 2 3 4 5
    6 36 4.75 11.62 14.37 0.78 8.37 10.6 36 1 2 3 4 5 6 37 1.74 8.51 5.16 12.6 12.43
    5.73 37 1 2 3 4 5 6 38 14.41 8.91 9.81 3.74 8.6 10.98 38 1 2 3 4 5 6 39 4.73
    9.15 10.32 6.89 12.67 10.35 39 1 2 3 4 5 6 40 7.93 10.76 15.36 0.17 10.2 16.17
    40 1 2 3 4 5 6 41 11.14 2.26 13.77 9.41 13.64 1.21 41 1 2 3 4 5 6 42 15.67 2.19
    9.94 9.56 0.01 8.28 42 1 2 3 4 5 6 43 17.87 11.81 7.66 8.05 9.34 13.18 43 1 2 3
    4 5 6 44 14.44 14.1 11.53 11.56 7.28 1.47 44 1 2 3 4 5 6 45 11.29 4.05 6.39 3.54
    9.28 15.31 45 1 2 3 4 5 6 46 7.27 6.5 15.14 11.67 11.58 10.37 46 1 2 3 4 5 6 47
    6.88 13.48 22.26 9.27 10.73 7.35 47 1 2 3 4 5 6 48 3.72 7.57 18.71 15.95 6.22
    12.55 48 1 2 3 4 5 6 49 5.49 5.62 14.69 8.57 5.97 13.59 49 1 2 3 4 5 6 50 7.72
    5.96 6.16 11.55 0.43 14.27 50 1 2 3 4 5 6 51 76.72 78.9 67.3 55.61 33.56 16.45
    51 1 2 3 4 5 6 52 74.4 61.54 52.2 45.5 29.11 12.09 52 1 2 3 4 5 6 53 104.61
    72.75 64.58 41.64 24.65 22.16 53 1 2 3 4 5 6 54 88.11 77.97 64.19 44.49 27.16
    8.19 54 1 2 3 4 5 6 55 95.66 73.09 43.16 57.36 28.63 4.76 55 1 2 3 4 5 6 56
    73.35 67.14 68.7 39.34 24.58 9.15 56 1 2 3 4 5 6 57 78.96 81.7 74.5 50.1 23.76
    5.91 57 1 2 3 4 5 6 58 94.91 87.12 61.44 55.04 35.63 13.17 58 1 2 3 4 5 6 59
    96.35 84.59 57.61 40.27 16.2 14.91 59 1 2 3 4 5 6 60 94.99 67.03 65.28 32.93
    36.74 6.46 60 1 2 3 4 5 6 61 93 83.11 65.53 37.35 30.34 10.63 61 1 2 3 4 5 6 62
    90.04 74.69 64.46 27.88 28.84 3.62 62 1 2 3 4 5 6 63 99.05 78.69 69.64 43.58
    19.42 16.87 63 1 2 3 4 5 6 64 100.4 61.22 67.69 29.16 26.85 2.57 64 1 2 3 4 5 6
    65 85.26 61.95 48.43 37.17 18.51 19.6 65 1 2 3 4 5 6 66 77.91 90.53 56.11 18.27
    6.53 1.83 66 1 2 3 4 5 6 67 101.34 75.68 47.98 27.44 26.89 13.48 67 1 2 3 4 5 6
    68 103.9 77.74 50.92 35.81 38.76 5.11 68 1 2 3 4 5 6 69 90.97 60.87 57.83 47.44
    21.32 4.42 69 1 2 3 4 5 6 70 106.12 83.7 55.54 54.53 47.47 10.07 70 1 2 3 4 5 6
    71 101.56 75.96 75.55 41.95 16.45 20.59 71 1 2 3 4 5 6 72 91.63 79.16 38.95
    52.34 27.51 3.53 72 1 2 3 4 5 6 73 80.59 84.99 57.04 40.35 28.94 8.22 73 1 2 3 4
    5 6 74 107.13 76.97 58.7 45.06 29.89 22.55 74 1 2 3 4 5 6 75 105.24 71.13 79.11
    22.27 23 18.37 75 1 2 3 4 5 6 76 104.88 65.92 67.72 46.71 41.73 21.11 76 1 2 3 4
    5 6 77 103.78 78.6 68.22 50.02 36.38 15.91 77 1 2 3 4 5 6 78 89.61 68.66 47.22
    56.34 37.14 11.52 78 1 2 3 4 5 6 79 85.1 67.57 70.29 55.26 18.08 23.46 79 1 2 3
    4 5 6 80 97.09 78.93 72.49 37.31 15.87 16.76 80 1 2 3 4 5 6 81 85.47 96.49 51.67
    49.25 34.75 5.34 81 1 2 3 4 5 6 82 99.06 85.94 55.05 39.84 37.73 7.3 82 1 2 3 4
    5 6 83 98.75 65.29 76.39 57.81 7.17 12.15 83 1 2 3 4 5 6 84 91.46 73.99 53.5
    55.98 15.14 15.29 84 1 2 3 4 5 6 85 86.39 83.64 61.26 49.19 6.82 6.13 85 1 2 3 4
    5 6 86 89.51 71 59.98 45.35 22.64 21.15 86 1 2 3 4 5 6 87 96.95 69.82 59.8 62.19
    14.3 11.43 87 1 2 3 4 5 6 88 88.99 65.21 62.49 35.64 33.94 12.16 88 1 2 3 4 5 6
    89 113.38 66.42 68.48 55.9 13.31 26.04 89 1 2 3 4 5 6 90 87.4 64.06 71.35 54.35
    25.47 5.02 90 1 2 3 4 5 6 91 17.13 39.13 61.08 67.99 67.56 84.16 91 1 2 3 4 5 6
    92 0.4 37.51 57.82 67.05 77.77 88.27 92 1 2 3 4 5 6 93 13.16 35.03 55 64.31
    73.81 84.01 93 1 2 3 4 5 6 94 14.82 38.76 53.93 63.18 80.64 81.02 94 1 2 3 4 5 6
    95 19.21 45.22 51.31 74.37 77.22 88.42 95 1 2 3 4 5 6 96 13.84 46.12 57.33 71.05
    74.93 83.68 96 1 2 3 4 5 6 97 16.75 55.2 49.95 67.56 66.84 82.34 97 1 2 3 4 5 6
    98 6.39 29.75 50.06 65.17 87.95 77.36 98 1 2 3 4 5 6 99 7.47 26.67 59.72 69.09
    77.78 88.81 99 1 2 3 4 5 6 100 3.19 41.28 57.9 69.76 74.65 82.79 100 1 2 3 4 5 6
    101 32.69 36.65 26.36 22.13 18.29 21.91 101 1 2 3 4 5 6 102 52.59 53.22 44.51
    36.6 17.42 30.16 102 1 2 3 4 5 6 103 36.99 42.17 33.39 60.83 29.55 25.69 103 1 2
    3 4 5 6 104 50.85 33.82 29.11 36.64 20.36 45.11 104 1 2 3 4 5 6 105 44.52 21.2
    13.1 25.18 33.11 0.81 105 1 2 3 4 5 6 106 56.73 33.07 21.48 5.09 24.83 20.2 106
    1 2 3 4 5 6 107 41.69 37.42 27.11 35.7 24.59 23.56 107 1 2 3 4 5 6 108 51.68
    45.17 27.53 17.01 21.5 24.02 108 1 2 3 4 5 6 109 55.87 26.62 28.66 24.57 26.9
    20.63 109 1 2 3 4 5 6 110 38.18 37.55 29.73 25.33 18.11 12.21 110 1 2 3 4 5 6
    111 47.86 27.81 44.14 43.8 30.14 12.99 111 1 2 3 4 5 6 112 44.59 25.3 41.47
    26.47 36.29 21.01 112 1 2 3 4 5 6 113 23.32 35.42 28.36 29.97 30.28 8.87 113 1 2
    3 4 5 6 114 32.75 52.58 28.89 11.87 8.58 25.81 114 1 2 3 4 5 6 115 59.17 39.81
    17.24 22.22 24.22 25.43 115 1 2 3 4 5 6 116 48.77 38.43 49.44 52.01 39.77 7.24
    116 1 2 3 4 5 6 117 34.35 38.12 44.17 44.64 22.13 13.01 117 1 2 3 4 5 6 118
    30.31 63.57 46.11 32.58 30.91 21.3 118 1 2 3 4 5 6 119 41.29 34.28 58.78 26.43
    28.67 36.6 119 1 2 3 4 5 6 120 53.96 27.97 55.62 40.71 16.31 15.96 120 1 2 3 4 5
    6 121 43.78 25.09 51.64 14.17 33.1 25.6 121 1 2 3 4 5 6 122 40.75 42.12 15.91
    20.61 8.8 1.24 122 1 2 3 4 5 6 123 42.92 34.11 46.06 34.9 31.72 1.55 123 1 2 3 4
    5 6 124 37.72 39.72 26.14 38.26 23.44 6.82 124 1 2 3 4 5 6 125 51.53 28.48 49.7
    28.34 16.41 10.5 125 1 2 3 4 5 6 126 45.55 30.21 29.1 33.52 20.84 32.87 126 1 2
    3 4 5 6 127 45.9 46.46 15.61 24.95 25.36 22.73 127 1 2 3 4 5 6 128 59.17 33.16
    37.38 31.25 28.75 14.89 128 1 2 3 4 5 6 129 51.15 36.98 22.37 27.22 17.23 19.6
    129 1 2 3 4 5 6 130 55.05 44.9 32.51 45.27 17.18 5.36 130 1 2 3 4 5 6
    ;;;;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    proc traj data=have
             out = want_of
         outplot = want_op
         outstat = want_os ci95M;
      id data_ID;
      data_x1-data_x6;
      indep time_1-time_6;
      order 2 2 2 2;
      model cnorm;
      max 130;
    run;quit;

    * create the plot;
    %include "c:/oto/trajplotnew.sas";

    options orientation=landscape;
    ods pdf file="d:/taj/pdf/taj_mockdata.pdf";
    ods graphics on / reset=all border=on height=7in width=10in
    %trajplotnew(op,os,,"Mockdata","6 month paid");
    run;quit;
    ods pdf close;

    *_              _       _       _
    | |_ _ __ __ _ (_)_ __ | | ___ | |_ _ __   _____      __
    | __| '__/ _` || | '_ \| |/ _ \| __| '_ \ / _ \ \ /\ / /
    | |_| | | (_| || | |_) | | (_) | |_| | | |  __/\ V  V /
     \__|_|  \__,_|/ | .__/|_|\___/ \__|_| |_|\___| \_/\_/
                 |__/|_|
    ;
    /* SAS macro to plot expected trajectories with CI's from PROC TRAJ */
    /* H. Seltman and J. Lam, 1/19/98                                   */

    /* Parameters:
        Name of outplot= dataset (not in quotes)
        Name of outstat= dataset (not in quotes)
        Title (in quotes)
        Subtitle (in quotes)
        Label for Y axis (in quotes, default is 'Outcome')
        Label for X axis (in quotes, default is 'T') */

    /* Sample calls:
        proc traj outplot=op outstat=os;
          ...
        run;
        %trajplot(op,os,'Main Title','Subtitle','y-axis text','x-axis text')
        %trajplot(op,os,'Main Title',' ','y-axis text','x-axis text')
        %trajplot(op,os,'Main Title','Subtitle','y-axis text')
        %trajplot(op,os,'Main Title','Subtitle')
        %trajplot(op,os,'Main Title') */

    %macro trajplotnew(PlotFile,StatFile,Title1,Title2,Ylab,Xlab);
      %local Cnt GpPcts;
      %local pi1 pi2 pi3 pi4 pi5 pi6 pi7 pi8 pi9;
      %local maxcolor col1 col2 col3 col4 col5;
      %local i j clr pline mline uline;

      goptions reset=global gunit=pct cback=white colors=(black blue green red orange)
        htitle=6 htext=3 ftext=zapf border;
      %CntPred(&PlotFile)
      %let Cnt=&PredCnt;

      /* Table of colors -- cycles back through used colors after maxcolor */
      %let maxcolor=5;
      %let col1=%STR(red);
      %let col2=%STR(green);
      %let col3=%STR(blue);
      %let col4=%STR(black);
      %let col5=%STR(orange);
      %DO i=%EVAL(&maxcolor + 1) %TO &Cnt;
        %let j=%EVAL(&i - &maxcolor);
        %let clr=&&col&j;
        %let col&i=&clr;
      %END;

      %DO i=1 %TO &Cnt;
        %let clr=&&col&i;
        symbol&i  color=&clr interpol=join value=&i. height=3;
      %END;
      %DO i=1 %TO &Cnt;
        %let clr=&&col&i;
        symbol1&i color=&clr interpol=join line=2;
      %END;
      %DO i=1 %TO &Cnt;
        %let clr=&&col&i;
        symbol2&i color=&clr interpol=join line=41;
      %END;
      %DO i=1 %TO &Cnt;
        %let clr=&&col&i;
        symbol3&i color=&clr interpol=join line=41;
      %END;

      %if %length(&Ylab)=0 %then %let Ylab='Outcome';
      %if %length(&Xlab)=0 %then %let Xlab='T';

      /* Dynamically create predn*t ... lines */
      %LET pline=;
      %LET mline=;
      %LET uline=;
      %DO i=1 %TO &Cnt;
        %LET pline=%STR(&pline pred&i*t);
        %LET mline=%STR(&mline l95m&i*t);
        %LET uline=%STR(&uline u95m&i*t);
      %END;

      /* Get group percentages */
      %GetPIs
      %let GpPcts=;
      %do i=1 %to &Cnt;
         %let GpPcts=%str(&GpPcts %'&&pi&i%');
      %end;
      %do i=1 %to &Cnt;
         %let GpPcts=%str(&GpPcts %' %');
      %end;
        %do i=1 %to &Cnt;
         %let GpPcts=%str(&GpPcts %' %');
      %end;
      %do i=1 %to &Cnt;
         %let GpPcts=%str(&GpPcts %' %');
      %end;


      /* Make plots */
      legend1 label=('Group Percents') value=(%unquote(&GpPcts)) across=&Cnt;

      proc gplot data=&PlotFile;
        title1 &Title1;
        title2 &Title2;
        format t 12.2 pred1 12.2;
        plot &pline &mline &uline / overlay legend=legend1;
        label t=&Xlab;
        label pred1=&Ylab;
      run;

     %OUT:
    %mend trajplotnew;


    /* Macro to find number of times in plot file */
    %macro CntPred(PltData);
      %global PredCnt NumV;
      %let PredCnt=0;
      proc contents data=&PltData noprint out=CPredTmp(keep=name)
       out2=CPredTmp2(keep=numvars);
      run;
      data _null_;
        retain icnt 0;
        set CPredTmp;
        if index(name,"PRED")>0 then icnt=icnt+1;
        call symput('PredCnt',left(put(icnt,12.)));
      run;
      data _null_;
        set CPredTmp2;
        call symput('NumV',left(put(numvars,12.)));
      run;
      proc datasets nolist;
        delete CPredTmp CPredTmp2;
      run;
    %mend CntPred;


    /* Macro to get group percentages from stat file */
    %macro GetPIs;
      data _null_;
        set &StatFile;
        call symput('pi'||left(put(_n_,1.)),left(put(pi,4.1)));
      run;
    %mend GetPIs;


