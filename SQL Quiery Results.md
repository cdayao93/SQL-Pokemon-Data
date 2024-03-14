Top 10 Strongest Pokemon by TotalStats
SELECT Name, Type_1, Type_2, Total
FROM pokemon
ORDER BY Total DESC
LIMIT 10;

![image](https://github.com/cdayao93/SQL-Pokemon-Data/assets/147434719/fb6ffabb-a68a-4ea4-8c45-443b0fc73680)


Distribution of Pokemon Types- This query creates a subquery that selects all types(both Type1 and Type2 from the dataset, counting them separately while considering 
Type 2 only if it is not null to avoid including Pokemon without a secondary type.Then, in the outer query, it sums these counts for each type across both Type_1 and Type_2, 
giving a total count of Pokémon for each type, which accurately reflects the distribution of types without duplicates

SELECT Type, SUM(Count) AS TotalCount
FROM (
  SELECT Type_1 AS Type, COUNT(*) AS Count
  FROM pokemon
  GROUP BY Type_1
  UNION ALL
  SELECT Type_2, COUNT(*)
  FROM pokemon
  WHERE Type_2 IS NOT NULL
  GROUP BY Type_2
) AS CombinedTypes
GROUP BY Type
ORDER BY TotalCount DESC;

![image](https://github.com/cdayao93/SQL-Pokemon-Data/assets/147434719/1527d094-e1ee-448d-b48b-52a89bb9a250)
![image](https://github.com/cdayao93/SQL-Pokemon-Data/assets/147434719/fcc41a3c-3766-4b6f-a62b-b159661088ff)

Most Common Type of Pokemon( I guess cause the ocean is huge)

SELECT Type_1, COUNT(*) AS Count
FROM pokemon
GROUP BY Type_1
UNION
SELECT Type_2, COUNT(*)
FROM pokemon
WHERE Type_2 IS NOT NULL
GROUP BY Type_2
ORDER BY Count DESC
LIMIT 1;

![image](https://github.com/cdayao93/SQL-Pokemon-Data/assets/147434719/cf3001bf-ecbb-42e4-9750-6706b1b2c24a)


Average Stats For Each Tupe (Type1)
SELECT Type_1, AVG(Total) AS AvgTotal, AVG(HP) AS AvgHP, AVG(Attack) AS AvgAttack, AVG(Defense) AS AvgDefense, AVG(Sp_Atk) AS AvgSpAtk, AVG(Sp_Def) AS AvgSpDef, AVG(Speed) AS AvgSpeed
FROM pokemon
GROUP BY Type_1
ORDER BY AvgTotal DESC;

Type_1	  AvgTotal	          AvgHP	                AvgAttack	          AvgDefense	        AvgSpAtk	          AvgSpDef	          Av gSpeed
Dragon	  522.5	83	          83                    101.70833333333333	 81.14583333333333	 87.72916666666667	83.95833333333333	  84.95833333333333
Steel	    498.6458333333333	  72.875	              93.1875	            114	                77.64583333333333	  81.14583333333333	  59.791666666666664
Flying	  496.5625	          77.625	              92.125	            73.6875	            83.1875	            79.625	            90.3125
Fighting	465.2692307692308	  76.96153846153847	    105.0576923076923	  77.63461538461539	  57.17307692307692	  71.11538461538461	  77.32692307692308
Fire	    462.9240506329114	  71.81012658227849	    85.50632911392405	  70.46835443037975	  87.0126582278481	  72.86075949367088	  75.26582278481013
Ice	      462.7291666666667	  79.64583333333333	    84.9375	            77.75	              75.10416666666667	  74.3125	            70.97916666666667
Rock	    459.4935064935065	  68.66233766233766	    92.22077922077922	  94.53246753246754	  65.97402597402598	  72.94805194805195	  65.15584415584415
Dark	    458.8813559322034	  74.61016949152543	    86.8135593220339	  72.79661016949153	  73.42372881355932	  72.22033898305085	  79.01694915254237
Fairy	    458.51851851851853	70.38888888888889	    67.05555555555556	  70.53703703703704	  85.92592592592592	  98.29629629629629	  66.31481481481481
Psychic	  452.6756756756757	  68.16216216216216	    75.33333333333333	  66.45045045045045	  92.37837837837837	  77.36936936936937	  72.98198198198199
Electric	447.8607594936709	  63.65822784810127	    73.13924050632912	  65.59493670886076	  87.49367088607595	  70.37974683544304	  87.59493670886076
Poison	  447.37254901960785	77.03921568627452	    78	                78.2156862745098	  70.41176470588235	  74.86274509803921	  68.84313725490196
Ghost    	445.78846153846155	64.59615384615384	    73.0576923076923	  78.32692307692308	  83.53846153846153	  80.76923076923077	  65.5
Ground	  443.4468085106383	  74.68085106382979	    92.48936170212765	  87.55319148936171	  56.76595744680851	  67.65957446808511	  64.29787234042553
Water	    440.3269230769231	  73.12179487179488	    77.5576923076923	  73.12820512820512	  75.92948717948718	  71.53846153846153	  69.05128205128206
Grass	    430.97478991596637	68.02521008403362	    78.02521008403362	  73.04201680672269	  76.23529411764706	  72.00840336134453	  63.739495798319325
Normal	  416.26174496644296	78.3489932885906	    77.00671140939598	  61.85234899328859	  59.4496644295302	  66.44295302013423	  73.16107382550335
Bug	      398.1465517241379	  61.96551724137931	    70.09482758620689  	69.18103448275862	  64.3103448275862	  64.22413793103448	  68.37068965517241


AVG Stats Across All Generations(Gen 6 has a few bangers in there)

SELECT Generation, AVG(Total) AS AvgTotal, AVG(HP) AS AvgHP, AVG(Attack) AS AvgAttack, AVG(Defense) AS AvgDefense, AVG(Sp_Atk) AS AvgSpAtk, AVG(Sp_Def) AS AvgSpDef, AVG(Speed) AS AvgSpeed
FROM pokemon
GROUP BY Generation
ORDER BY Generation;


Generation	AvgTotal	          AvgHP	              AvgAttack	          AvgDefense	        AvgSpAtk	          AvgSpDef	          AvgSpeed
1	          407.0794701986755	  64.21192052980132	  72.54966887417218	  68.2251655629139	  67.13907284768212	  66.01986754966887	  68.93377483443709
2	          392.0472440944882	  66.09448818897638	  69.05511811023622	  65.07874015748031	  66.09448818897638	  67.16535433070867	  58.55905511811024
3	          408.2482269503546	  65.42553191489361	  73.93617021276596	  69.47517730496453	  68.90780141843972	  67.04255319148936	  63.46099290780142
4	          478.75539568345323	77.97841726618705	  83.51079136690647	  81.13669064748201	  79.87769784172662	  80.83453237410072	  75.41726618705036
5	          437.77272727272725	71.625	            83.26704545454545	  72.14772727272727	  72.375	            68.55681818181819	  69.80113636363636
6	          486.9310344827586	  72.62068965517241	  86.29885057471265	  79.42528735632185	  87.73563218390805	  82.49425287356321	  78.35632183908046
7	          468.5067567567568	  72.55405405405405	  87.89864864864865	  79.45945945945945	  77.99324324324324	  76.02027027027027	  74.58108108108108
8          	462.9119496855346	  74.69182389937107	  84.64779874213836	  76.44025157232704	  77.16981132075472	  76.94339622641509	  73.01886792452831
9	          463.82191780821915	78.48630136986301	  84.41095890410959	  77.17808219178082	  72.66438356164383	  73.54794520547945	  77.61643835616438


Comparison on Mega Pokemon(Mewtwo and Rayquaza are GOATED)
SELECT Name, Type_1, Type_2, Total, HP, Attack, Defense, Sp_Atk, Sp_Def, Speed
FROM pokemon
WHERE Name LIKE 'Mega_%'
OR Name IN (SELECT Name FROM pokemon WHERE Name NOT LIKE 'Mega_%' AND Name IN (SELECT Name FROM pokemon WHERE Name LIKE 'Mega_%'));

Name	            Type_1	    Type_2	    Total	  HP	  Attack	Defense	Sp_Atk	Sp_Def	Speed
Mega_Venusaur	    Grass	      Poison	    625	    80	  100	    123	    122	    120	    80
Mega_Charizard_X	Fire	      Dragon	    634	    78	  130	    111	    130    	85	    100
Mega_Charizard_Y	Fire	      Flying	    634	    78	  104	    78      159	    115	    100
Mega_Blastoise	  Water	      NULL	      630	    79	  103	    120	    135	    115	    78
Mega_Beedrill	    Bug	        Poison	    495	    65	  150	    40	    15	    80    	145
Mega_Pidgeot	    Normal	    Flying	    579	    83	  80	    80	    135	    80	    121
Mega_Alakazam	    Psychic	    NULL	      600	    55	  50	    65	    175	    105	    150
Mega_Slowbro	    Water	      Psychic	    590	    95	  75	    180	    130	    80	    30
Mega_Gengar	      Ghost	      Poison	    600	    60	  65	    80	    170	    95	    130
Mega_Kangaskhan	  Normal	    NULL	      590	    105	  125	    100	    60	    100	    100
Mega_Pinsir	      Bug	        Flying	    600	    65	  155	    120	    65	    90	    105
Mega_Gyarados	    Water	      Dark	      640	    95	  155	    109	    70	    130	    81
Mega_Aerodactyl	  Rock	      Flying	    615	    80	  135	    85	    70	    95	    150
Mega_Mewtwo_X	    Psychic	    Fighting	  780	    106	  190	    100	    154	    100	    130
Mega_Mewtwo_Y	    Psychic	    NULL	      780	    106	  150	    70	    194	    120	    140
Meganium	        Grass	      NULL	      525	    80	  82	    100	    83	    100	    80
Mega_Ampharos	    Electric	  Dragon	    610	    90	  95	    105	    165	    110	    45
Mega_Steelix	    Steel	      Ground	    610	    75	  125	    230	    55	    95	    30
Mega_Scizor	      Bug	        Steel	      600	    70	  150	    140	    65	    100	    75
Mega_Heracross	  Bug	        Fighting	  600	    80	  185	    115	    40	    105	    75
Mega_Houndoom	    Dark	      Fire	      600	    75	  90	    90	    140	    90	    115
Mega_Tyranitar	  Rock	      Dark	      700	    100	  164	    150	    95	    120	    71
Mega_Sceptile	    Grass	      Dragon	    630	    70	  110	    75	    145	    85	    145
Mega_Blaziken	    Fire	      Fighting	  630	    80	  160	    80	    130	    80	    100
Mega_Swampert	    Water	      Ground	    635	    100	  150	    110	    95	    110	    70
Mega_Gardevoir	  Psychic	    Fairy	      618	    68	  85	    65	    165	    135	    100
Mega_Sableye	    Dark	      Ghost	      480	    50	  85	    125	    85	    115	    20
Mega_Mawile	      Steel	      Fairy	      480	    50	  105	    125	    55	    95	    50
Mega_Aggron	      Steel	      NULL	      630	    70	  140	    230	    60	    80	    50
Mega_Medicham	    Fighting	  Psychic	    510	    60	  100	    85	    80	    85	    100
Mega_Manectric	  Electric	  NULL	      575	    70	  75	    80	    135	    80	    135
Mega_Sharpedo	    Water	      Dark	      560	    70	  140	    70	    110	    65	    105
Mega_Camerupt	    Fire	      Ground	    560	    70    120	    100	    145	    105	    20
Mega_Altaria	    Dragon	    Fairy	      590	    75	  110	    110	    110	    105	    80
Mega_Banette	    Ghost	      NULL	      555	    64	  165	    75	    93	    83	    75
Mega_Absol	      Dark	      NULL	      565	    65	  150	    60	    115	    60	    115
Mega_Glalie	      Ice	        NULL	      580	    80	  120	    80	    120	    80	    100
Mega_Salamence	  Dragon	    Flying	    700	    95	  145	    130	    120	    90	    120
Mega_Metagross	  Steel	      Psychic	    700	    80	  145	    150	    105	    110	    110
Mega_Latias	      Dragon	    Psychic	    700	    80	  100	    120	    140	    150	    110
Mega_Latios	      Dragon	    Psychic	    700	    80	  130	    100	    160	    120	    110
Mega_Rayquaza	    Dragon	    Flying	    780	    105	  180	    100	    180	    100	    115
Mega_Lopunny	    Normal	    Fighting	  580	    65	  136	    94	    54	    96	    135
Mega_Garchomp	    Dragon	    Ground	    700	    108	  170	    115	    120	    95	    92
Mega_Lucario	    Fighting	  Steel	      625	    70	  145	    88	    140	    70	    112
Mega_Abomasnow	  Grass	      Ice	        594	    90	  132	    105	    132	    105	    30
Mega_Gallade	    Psychic	    Fighting	  618	    68	  165	    95	    65	    115    	110
Mega_Audino	      Normal	    Fairy	      545	    103	  60	    126	    80	    126    	50
Mega_Diancie	    Rock	      Fairy	      700	    50	  160    	110    	160    	110    	110
