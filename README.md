# Base Agrhys

    Concerne toutes les tables :
      - les ids sont tous nommés id il est prëfërable pour une meilleure lecture de les nomer table_id
      - trop de reference a famille_id > id inutile et lors des requettes des effets "circulaires" ralentissent considécablement les requettes.


    Questions a poser :
    
    Est ce qu'on peut pas considerer que la derniere valeur corrigée est celle validée ?
    a qui sert station_site_id dans sensor_location_link ?
    
# <a id="sommaire">Sommaire</a>

| | | |
|:--|:--|:--|
| [base](#base)                               |[edata_va](#edatava)                 |[regroupement](#regroupement)|  
| [bdata](#bdata)                             |[erreursvalidees](#erreursvalidees)  |[s_regroupement](#sregroupement)|  
| [bdata_s](#bdatas)                          |[famille](#famille)                  |[sensor](#sensor)|
| [bdata_va](#bdatava)                        |[groupe3](#groupe3)                  |[sensor_location_link](#sensorlocationlink)|
| [caracteristique](#caracteristique)         |[groupemd](#groupemd)                |[sensor_suffixe](#sensorsuffixe)|
| [catchment](#catchment)                     |[instrument](#instrument)            |[site](#site)|
| [cdata](#cdata)                             |[j_bdata](#jbdata)                   |[site_exp](#siteexp)|
| [codemd](#codemd)                           |[j_edata](#jedata)                   |[staff](#staff)|
| [conditionnement](#conditionnement)         |[j_edata_s](#jedatas)                |[suivi_bdata](#suivibdata)|
| [data_type_hydras](#datatypehydras)         |[laboratoire](#laboratoire)          |[suivi_edata](#suiviedata)|
| [dimension_temporelle](#dimensiontemporelle)|[location](#location)                |[suivi_j_data](#suivijdata)|
| [echantillon](#echantillon)                 |[methodedanalyse](#methodedanalyse)  |[treedata](#treedata)|
| [edata_s](#edatas)                          |[mode_de_mesure](#modedemesure)      |[unite](#unite)|
|                                             |                                     |[variable_associee](#variableassociee)|



# <a id="base">base</a>

id|name |description                            |name_en        |
--|-----|---------------------------------------|---------------|
 1|bdata|Données brutes                         |Raw data       |
 2|cdata|Données corrigees (correction niveau 1)|Calculated data|
 3|edata|Données traitées (correction niveau 2) |Processed data |

permet de selectionner non pas la base comme son nom l'indique mais une table.

[Retour au sommaire](#sommaire) 

# <a id="bdata">bdata</a>


id      |famille_id|data_type_id|location_id|sensor_location_id|staff_sample_id|udate              |value |
--------|----------|------------|-----------|------------------|---------------|-------------------|------|
28775383|         1|           3|         52|                69|             10|2001-02-09 12:00:00| -6.23|
28775384|         1|           3|         52|                69|             10|2001-02-09 12:15:00| -6.24|
28775385|         1|           3|         52|                69|             10|2001-02-09 12:30:00| -6.19|

- id : ne represente pas une donnee identifiable (ce n'est pas une cle primaire valide) 
- famille_id : lien avec la table famille (famille des type de données)
- data_type_id : lien avec la table data_type_hydras ** à Verifier ** (liste des type de données)
    data_type_id ne fait reference a des données inscripte dans le script 
- location_id : lien avec la table location (Point de mesure)
- sensor_location_id : lien avec la table sensor (Capteur par type de donnee intra  instrument de mesure)
  On voit une redondance : famille_id et data_type_id sont dans sensor et aussi dans bdata il devrait etre supprimer de bdata du fait qu'on l'obtienne par sensor
- staff_sample_id : lien avec la table staff (Personnel = 10 car insertion auto) Comprends pas l'interet si on met 10 tout le temps ?

```
Lors de l'import journalier des données d'hydras des fichiers csv identifiés Brut par leur nom.
```
[Retour au sommaire](#sommaire) 

# <a id="bdatas">bdata_s</a>

s pour sensor ? a confirmer je n'ai pas encore trouvé la raison d'ëtre de cette table.

[Retour au sommaire](#sommaire) 

# <a id="bdatava">bdata_va</a>

va pour variable ? concrnant les variable associées.

[Retour au sommaire](#sommaire) 

# <a id="caracteristique">caracteristique</a>

id|nom            |description|idd|
--|---------------|-----------|---|
 2|Piezometer     |Piezo      |  4|
 3|Puits          |           |  1|
 4|Weather station|           |  3|
 1|Outlet         |Exutoire   |  2|

 un id et un idd ? cela semble etre un doublon (Caracterise  les points de mesures: exutoire,piezo,puits, stations meteo)

[Retour au sommaire](#sommaire) 

# <a id="catchment">catchment</a>

id|site_exp_id|name         |surface|country          |description                                                       |
--|-----------|-------------|-------|-----------------|------------------------------------------------------------------|
 2|          2|Kervidy      |    490|France, Morbihan |exutoire du lieu-dit Kervidy à Naizin suivi par INRA et OSU Rennes|
 1|          2|Naizin       |   1200|France, Morbihan |    exutoire de Stimoes suivi par le CEMAGREF                     |
16|          4|Pont_Lagot   |     22|France           |                                                                  |
18|          3|Sélune       | 103800|France, Manche   | Suivi amont et aval des barrages de la Selune                    |
14|          1|Coat_Timon_10|     57|France, Finistère|                                                                  |
13|          1|Coat_Timon_9 |     40|France, Finistère|                                                                  |

lieu de mesure (Bassin versant intra site_experimental)
country aurai put être divisé.

[Retour au sommaire](#sommaire) 

# <a id="cdata">cdata</a>

id       |famille_id|data_type_id|location_id|sensor_location_id|staff_sample_id|udate              |value|code1|code2|
---------|----------|------------|-----------|------------------|---------------|-------------------|-----|-----|-----|
111814317|         1|         101|         72|                84|             10|2004-12-10 15:19:00|-5.52|     |     |
111814318|         1|         101|         72|                84|             10|2004-12-10 15:34:00|-5.52|     |     |
111814319|         1|         101|         72|                84|             10|2004-12-10 15:49:00|-5.52|     |     |
111814320|         1|         101|         72|                84|             10|2004-12-10 16:04:00|-5.52|     |     |
111814321|         1|         101|         72|                84|             10|2004-12-10 16:19:00|-5.52|     |     |

données corrigées (Donnees corrigees issues du domaine corrigees de Hydras. Les donnees ont subies une correction mineure)

- idem que BDATA (aucune raison de doubler)
- code1 & code2 permetent d'identifier les raisons de la correction.

```
Lors de l'import journalier des données d'hydras des fichiers csv identifiés Corrigé par leur nom.
```

[Retour au sommaire](#sommaire) 

# <a id="codemd">codemd</a>

id|name|description                                                                                        |
--|----|---------------------------------------------------------------------------------------------------|
 1|1   |Code lié à la métadonnée code echantillon,point de prélevement ... Ce qui caractérise l'echantillon|
 2|2   |Caracteristique des appareils de mesure                                                            |

apparament Code lié à la métadonnée code echantillon,point de prélevement A verifier.

[Retour au sommaire](#sommaire) 

# <a id="conditionnement">conditionnement</a>

id|name                                                                                         |description|
--|---------------------------------------------------------------------------------------------|-----------|
 1|Na                                                                                           |           |
 2|Filtration 0.2+refrigere                                                                     |           |
 3|?                                                                                            |           |
 4|Filtration 0.45+refrigere                                                                    |           |
 5|Filtration 0.45 Jusque 2012 Puis 0.2- + Refrigere Sauf Sur Exutoire Moulinet Et Station Virey|           |
 6|Aucun                                                                                        |           |
 7|Filtration 0.2+ Refrigere                                                                    |           |
 8|Filtrat Sur 0.45                                                                             |           |
 9|Variable                                                                                     |           |
10|Filtration 0.2-acidificie-refrigere                                                          |           |


[Retour au sommaire](#sommaire) 

# <a id="datatypehydras">data_type_hydras</a>

id |name           |unit   |description                                                                             |famille_id|data_type_id|element_id|code_hydras|nomanalyse   |
---|---------------|-------|----------------------------------------------------------------------------------------|----------|------------|----------|-----------|-------------|
186|pH             |pH u.  |                                                                                        |         1|          18|          |           |             |
159|Ce-ICPMS-GR    |µg/L   |                                                                                        |         3|          61|          |           |             |
148|Cu-ICPMS-GR    |µg/L   |                                                                                        |         3|          50|          |           |             |
 91|h (limnigr)    |m      |Niv du cours d eau limnigraphe¶                                                         |         1|          20|       120|116        |Debit        |
150|Ga-ICPMS-GR    |µg/L   |                                                                                        |         3|          52|          |           |             |
158|La-ICPMS-GR    |µg/L   |                                                                                        |         3|          60|          |           |             |
  8|EhCorr in situ |mV     |                                                                                        |         2|          11|          |           |             |
  4|Uflow          |m/s    |mesure de la vitesse de l eau                                                           |         1|           4|       104|103        |vitesse      |
152|Rb-ICPMS-GR    |µg/L   |concentration en Rubidium par ICPMS                                                     |         3|          54|          |           |             |
153|Sr-ICPMS-GR    |µg/L   |concentration en Strontium par ICPMS                                                    |         3|          55|          |           |             |
155|Cd-ICPMS-GR    |µg/L   |concentration en Cadmium par ICPMS                                                      |         3|          57|          |           |             |
  3|Z              |m      | mesure de niveau                                                                       |         1|           3|       103|101        |niveau d eau |
156|Sb-ICPMS-GR    |µg/L   |concentration en Sb par ICPMS                                                           |         3|          58|          |           |             |
193|Abs230-GR      |a.u./m |Absorbance at 230 nm measured using an atomic absorption spectrophotometer Perkin Elmer |         3|          86|          |           |             |

- id : clef permettant le lien avec le type de données (hyddras)
- name, unit et description : infos sur le type de données.
- famille_id : lien avec la table famille (famille des type de données)
- data_type_id : INCOHERENCE lien avec la table elle même ?
- element_id : 
- code_hydras : lien avce Hydras ?
- nomanalyse : 

|regroupement_id|mode_de_mesure_id|name_en      |arrondi|symbole          |entete                                                    |s_regroupement_id|dimension_temporelle_id|
|---------------|-----------------|-------------|-------|-----------------|----------------------------------------------------------|-----------------|-----------------------|
|              2|                2|             |      2|pH               |Water pH measured continuously                            |                 |                      1|
|              3|                1|             |      3|Ce               |Cerium concentration by ICPMS                             |                7|                       |
|              3|                1|             |      3|Cu               |Copper concentration by ICPMS                             |                7|                       |
|              1|                2|h (limnigr)  |      3|h (limnigr)      |Stream water level measured on a limnigraph               |                 |                      1|
|              3|                1|             |      3|Ga               |Gallium concentrationby ICPMS                             |                7|                       |
|              3|                1|             |      3|La               |Lanthanum concentration by ICPMS                          |                7|                       |
|              2|                1|             |      0|EhCorr in situ   |Corrected in situ reduction/oxydation potential           |                1|                       |
|              1|                2|Uflow        |      3|Uflow            |Stream current velocity                                   |                 |                      1|
|              3|                1|             |      3|Rb               |Rubidium concentration by ICPMS                           |                7|                       |
|              3|                1|             |      3|Sr               |Strontium concentration by ICPMS                          |                7|                       |
|              3|                1|             |      3|Cd               |Cadmium concentration by ICPMS                            |                7|                       |
|              1|                2|Z            |      3|Z                |groundwater level from soil surface measured continuously |                 |                      1|
|              3|                1|             |      3|Sb               |Antimony concentration by ICPMS                           |                7|                       |
|              3|                1|             |      3|Abs230           |Absorbance at 230 nm                                      |                2|                       |

- regroupement_id : 
- mode_de_mesure_id : 
- name_en : 
- arrondi : 
- symbole : 
- entete : 
- s_regroupement_id : 
- dimension_temporelle_id : 


|sensorsuffixe_id|conditionnement_id|laboratoire_id|methodedanalyse_id|groupe3_id|codemd_id|groupemd_id|
|----------------|------------------|--------------|------------------|----------|---------|-----------|
|                |                  |              |                  |          |         |           |
|                |                10|             2|                15|          |         |           |
|                |                10|             2|                15|          |         |           |
|               2|                  |              |                  |          |         |           |
|                |                10|             2|                15|          |         |           |
|                |                10|             2|                15|          |         |           |
|                |                 1|             1|                 1|          |         |          3|
|               1|                  |              |                  |          |         |           |
|                |                10|             2|                15|          |         |           |
|                |                10|             2|                15|          |         |           |
|                |                10|             2|                15|          |         |           |
|               3|                  |              |                  |          |         |           |
|                |                10|             2|                15|          |         |           |
|                |                 2|             2|                 4|          |         |           |

- sensorsuffixe_id : 
- conditionnement_id : 
- laboratoire_id : 
- methodedanalyse_id : 
- groupe3_id : 
- codemd_id : 
- groupemd_id : 


[Retour au sommaire](#sommaire) 

# <a id="dimensiontemporelle">dimension_temporelle</a>

id|name                 |description|name_en              |
--|---------------------|-----------|---------------------|
 3|daily                |           |daily                |
 2|hourly               |           |hourly               |
 1|Acquisition time step|           |Acquisition time step|

dimension_temporelle des type de données 

 - name_en : sert a rien.

 
[Retour au sommaire](#sommaire) 

# <a id="echantillon">echantillon</a>

id    |refsas     |refgr|location_id|modeprelev|numechcrue|udate              |sondeph|sondeteau|sondeeh|sondecond|sondeo2|
------|-----------|-----|-----------|----------|----------|-------------------|-------|---------|-------|---------|-------|
     0|VA1315_R190|     |         95|          |          |2005-03-24 00:00:00|       |         |       |         |       |
302142|VA1320_R195|     |        101|          |          |2005-03-24 00:00:00|       |         |       |         |       |
302143|VA1321_R196|     |        100|          |          |2005-03-24 00:00:00|       |         |       |         |       |
302144|           |     |        104|          |          |2005-03-24 00:00:00|       |         |       |         |       |
302145|VA1318_R193|     |        103|          |          |2005-03-24 00:00:00|       |         |       |         |       |
302146|VA1319_R194|     |        102|          |          |2005-03-24 00:00:00|       |         |       |         |       |
302147|VA1297_R150|     |        112|          |          |2005-03-24 00:00:00|       |         |       |         |       |
302148|Pt103_     |     |        217|          |          |2005-03-30 00:00:00|       |         |       |         |       |
302149|Pt104_     |     |        208|          |          |2005-03-30 00:00:00|       |         |       |         |       |
302150|           |     |         30|          |          |2005-03-31 00:00:00|       |         |       |         |       |

- id : 
- refsas : 
- refgr : 
- location_id : 
- modeprelev : 
- numechcrue : 
- udate : 
- sondeph : 
- sondeteau : 
- sondeeh : 
- sondecond : 
- sondeo2 : 

[Retour au sommaire](#sommaire) 

# <a id="edata">edata</a>

id       |famille_id|data_type_id|location_id|sensor_location_id|staff_sample_id|udate              |value|code1|code2|
---------|----------|------------|-----------|------------------|---------------|-------------------|-----|-----|-----|
        0|         4|          11|        204|                 0|             10|2019-02-01 01:00:00|    0|    0|    0|
435061593|         4|           6|        204|                 0|             10|2019-02-01 01:00:00|    0|    0|    0|
435061594|         4|          10|        204|                 0|             10|2019-02-01 01:00:00|  4.4|    0|    0|
435061595|         4|          19|        204|                 0|             10|2019-02-01 01:00:00|   98|    0|    0|
435061596|         4|          11|        204|                 0|             10|2019-02-01 02:00:00|    0|    0|    0|
435061597|         4|           6|        204|                 0|             10|2019-02-01 02:00:00|    0|    0|    0|
435061598|         4|          10|        204|                 0|             10|2019-02-01 02:00:00|  2.9|    0|    0|
435061599|         4|          19|        204|                 0|             10|2019-02-01 02:00:00|   98|    0|    0|


données validées (Donnees validées issues du domaine vidae de Hydras. Les donnees ont subies une correction plus importante ou ont été reconstituées.
Données issues de climatik)

- idem que BDATA (aucune raison de doubler)
- code1 & code2 permetent d'identifier les raisons de la corrections.

[Retour au sommaire](#sommaire) 

# <a id="edatas">edata_s</a>

s pour sensor ? a confirmer je n'ai pas encore trouvé la raison d'ëtre de cette table.

[Retour au sommaire](#sommaire) 

# <a id="edatava">edata_va</a>

va pour variable ? concrnant les variable associées.

[Retour au sommaire](#sommaire) 

# <a id="erreursvalidees">erreursvalidees</a>

id|location_id|famille_id|data_type_id|base1_id|base2_id|datedeb|datefin|description|
--|-----------|----------|------------|--------|--------|-------|-------|-----------|

A quoi sert cette table ?

[Retour au sommaire](#sommaire) 

# <a id="famille">famille</a>

id|name     |description                    |name_en  |
--|---------|-------------------------------|---------|
 1|Sensor   |                               |Sensor   |
 4|Climate  |Donnees meteo issues d Agroclim|Climate  |
 2|Manual   |                               |Manual   |
 3|Chemistry|                               |Chemistry|

 les differentes familles de donnëes

[Retour au sommaire](#sommaire) 

# <a id="groupe3">groupe3</a>

id|name       |description|
--|-----------|-----------|
 0|azote      |           |
 2|phosphore  |           |
 3|carbone    |           |
 4|silice     |           |
 5|temperature|           |

[Retour au sommaire](#sommaire) 

# <a id="groupemd">groupemd</a>

id|name        |description|
--|------------|-----------|
 1|pH          |           |
 2|temperature |           |
 3|redox       |           |
 4|conductivite|           |
 5|o2          |           |
 6|doc         |           |
 7|dic         |           |
 8|phosphate   |           |

[Retour au sommaire](#sommaire) 

# <a id="instrument">instrument</a>

id |designation   |virtual|brand            |model               |serialnum   |description                          |
---|--------------|-------|-----------------|--------------------|------------|-------------------------------------|
216|CAN-PRE-18    |false  |OTT              |Orpheus Mini        |213432      |                                     |
220|CAN-PRE-56    |false  |                 |Orphéus mini        |            |                                     |
  9|CAN-PRE-10    |false  |STS              |STS DL/N            |289816      |                                     |
 11|CPT-PRT18     |false  |SDEC FRANCE      |SKT850T             |8551082     |                                     |
230|CAN-USS-01    |false  |CR2M             |SAB600              |Inconnu     |Centrale / capteurs ultrasons INRA   |
236|CAN-USS-07    |false  |CR2M             |SAB600              |Inconnu     |Centrale / capteurs ultrasons BRGM   |
233|CAN-USS-04    |false  |CR2M             |SAB600              |Inconnu     |Centrale / capteurs ultrasons INRA   |
 16|CPT-PRP-02    |false  |american sigma   |capteur de pression |            |                                     |
 17|CPT-PRP-03    |false  |american sigma   |capteur de pression |            |                                     |

 table indiquant l'instrument de mesure (instrument de mesure sa marque... modele)

- id : id
- designation : designation ressemblant plus a un code qu'à une désignation
- virtual : instrumunt physique on non
- brand : marque de l'instrument
- model : model de l'instrument
- serialnum : numéro de serie
- description : description de l'instrument

[Retour au sommaire](#sommaire) 

# <a id="jbdata">j_bdata</a>

id       |famille_id|data_type_id|location_id|udate              |value           |occurence|
---------|----------|------------|-----------|-------------------|----------------|---------|
150801501|         1|           5|         88|2008-11-21 00:00:00|            13.5|       37|
150801502|         1|           5|         88|2008-11-22 00:00:00|            13.5|       96|
150801503|         1|           5|         88|2008-11-23 00:00:00|            13.5|       96|
150801504|         1|           5|         88|2008-11-24 00:00:00|            13.5|       96|
150801505|         1|           5|         88|2008-11-25 00:00:00|            13.5|       96|
150801506|         1|           5|         88|2008-11-26 00:00:00|            13.5|       96|
150801507|         1|           5|         88|2008-11-27 00:00:00|            13.5|       96|
150801508|         1|           5|         88|2008-11-28 00:00:00|            13.5|       96|
150801509|         1|           5|         88|2008-11-29 00:00:00|            13.5|       96|
150801510|         1|           5|         88|2008-11-30 00:00:00|            13.5|       96|
150801511|         1|           5|         88|2008-12-01 00:00:00|            13.5|       96|

Donnees journalieres calculées à partir de données de bdata. Ces données dons utilisées pour les graphes affichés dans vidae

- idem que BDATA (aucune raison de multiplier la donnees)
- occurence :

[Retour au sommaire](#sommaire) 

# <a id="jedata">j_edata</a>

id      |famille_id|data_type_id|location_id|udate              |value |code1|code2|occurence|occurence_fiable|
--------|----------|------------|-----------|-------------------|------|-----|-----|---------|----------------|
 9976351|         4|           6|        204|2018-07-27 00:00:00|      |     |     |        0|               0|
 3946058|         2|           9|         34|2015-03-28 00:00:00|      |     |     |         |                |
10672000|         4|           6|        204|2018-10-26 00:00:00|      |     |     |       24|              24|
 3946059|         2|           9|         34|2015-03-29 00:00:00|      |     |     |         |                |
 3946060|         2|           9|         34|2015-03-30 00:00:00|      |     |     |         |                |
 3946061|         2|           9|         34|2015-03-31 00:00:00|      |     |     |         |                |
 3946062|         2|           9|         34|2015-04-01 00:00:00|      |     |     |         |                |


Donnees journalieres calculées à partir de données de edata. Ces données dons utilisées pour les graphes affichés dans vidae

- idem que j_bdata (aucune raison de multiplier la donnees)
- code1 :
- code2 :
- occurence :
- occurence_fiable :

[Retour au sommaire](#sommaire) 

# <a id="jedatas">j_edata_s</a>

id     |famille_id|data_type_id|location_id|udate              |value  |code1|code2|occurence|occurence_fiable|
-------|----------|------------|-----------|-------------------|-------|-----|-----|---------|----------------|
      0|         2|          14|         36|2001-11-07 00:00:00|    355|     |     |        1|               1|
3123368|         2|          14|         36|2001-11-14 00:00:00|    271|     |     |        1|               1|
3123369|         2|          14|         36|2001-11-21 00:00:00|    268|     |     |        1|               1|
3123370|         2|          14|         36|2001-11-28 00:00:00|    271|     |     |        1|               1|
3123371|         2|          14|         36|2001-12-05 00:00:00|    270|     |     |        1|               1|
3123372|         2|          14|         36|2001-12-18 00:00:00|    273|     |     |        1|               1|
3123373|         2|          14|         36|2002-01-02 00:00:00|    272|     |     |        1|               1|
3123374|         2|          14|         36|2002-01-09 00:00:00|    268|     |     |        1|               1|
3123375|         2|          14|         36|2002-01-16 00:00:00|    361|     |     |        1|               1|

Donnees journalieres calculées à partir de données de edata. Ces données dons utilisées pour les graphes affichés dans vidae

- idem que j_bdata (aucune raison de multiplier la donnees)
- code1 :
- code2 :
- occurence :
- occurence_fiable :

[Retour au sommaire](#sommaire) 

# <a id="laboratoire">laboratoire</a>

id|name                        |description                               |address                   |city         |zipcode|contactname      |contactmail                       |contactphone        |
--|----------------------------|------------------------------------------|--------------------------|-------------|-------|-----------------|----------------------------------|--------------------|
 1|Na                          |                                          |                          |             |       |                 |                                  |                    |
 5|?                           |                                          |                          |             |       |                 |                                  |                    |
 6|INRA St Gilles              |                                          |                          |             |       |                 |                                  |                    |
 2|UMR Géosciences Rennes      |Chimiste (Ingénieur d'Etudes)             |263 Avenue Général Leclerc|Rennes       |  35042|Patrice Petitjean| patrice.petitjean@univ-rennes1.fr| +33 223236087      |
 4|UMR SAS Quimper             |                                          |4 rue de stang Vihan      |Quimper      |  29000|                 |                                  | +33(0)2 98 95 01 91|
 3|UMR INRA/Agrocampus 1069 SAS|Ingénieur en techniques d'analyse chimique|65 Rue de Saint-Brieuc    | Rennes Cedex|  35042|Yannick Fauvel   |Yannick.fauvel@inra.fr            |02 23 48 56 67      |

[Retour au sommaire](#sommaire) 

# <a id="location">location</a>

id |site_id|name         |georef_system    |x         |y          |z      |depth|description                                                
---|-------|-------------|-----------------|----------|-----------|-------|-----|-----------------------------------------------------------
190|     34|T3B(150)     |relatif          |     -1.13|     -9.552|  0.428|  1.5|canne tensiométrique                                       
 50|     16|F2           |Lambert II etendu|168944.976|6784124.682|  16.85|    2|Piézomètre¶diamètre : 75 mm¶plein : 1,65  m¶crépinage : 0.3
 52|     16|F4           |Lambert II etendu|168920.465|6784046.144| 28.339|   15|Piézomètre¶diamètre : 115/125 mm¶plein : 14, 04 m¶crépinage
 54|     16|F5b          |Lambert II etendu|168852.655|6783964.281| 37.008|   20|Piézomètre¶diamètre: 115/125 mm¶plein: 18,6 m¶crépinage : 1

[Retour au sommaire](#sommaire) 

 # <a id="methodedanalyse">methodedanalyse</a>

id|name                                                                                    |description|
--|----------------------------------------------------------------------------------------|-----------|
 1|Na                                                                                      |           |
 2|COTmetre Shimadzu: Difference Entre La Concentration Mesuree En C Total Et C Inorganique|           |
 3|COTmetre Shimadzu                                                                       |           |
 4|* Spectrophotomètre ???,                                                                |           |

[Retour au sommaire](#sommaire) 

 # <a id="modedemesure">mode_de_mesure</a>

id|name  |description|name_en|
--|------|-----------|-------|
 0|Sensor|           |Sensor |
 1|Manual|           |Manual |

mode_de_mesure des type de données

[Retour au sommaire](#sommaire) 

 # <a id="regroupement">regroupement</a>

id|name             |description|name_en          |
--|-----------------|-----------|-----------------|
 1|Hydrology        |           |Hydrology        |
 3|Chemistry        |           |Chemistry        |
 5|Biophysics       |           |Biophysics       |
 4|Climate          |           |Climate          |
 2|Physico-chemistry|           |Physico-chemistry|

regroupement des types de données

[Retour au sommaire](#sommaire) 

 # <a id="sregroupement">s_regroupement</a>

id|name         |description                                                                                     |regroupement_id|
--|-------------|------------------------------------------------------------------------------------------------|---------------|
 0|Divers       |                                                                                                |              3|
 2|Carbon       |Analyses related to the monitoring of dissolved carbon dynamics                                 |              3|
 4|Major Cations|Cations analyses                                                                                |              3|
 3|Major Anions |Anions analyses                                                                                 |              3|

sous regroupement : table inutile les données devraient être dans regroupement avec une colonne en référence a elle meme et en l'absence pas de sous regroupement.

[Retour au sommaire](#sommaire) 

 # <a id="sensor">sensor</a>

id_designation |virtual|famille_id|data_type_id|brand |model       |serialnum|accuracy|description                                                                      |id |
---------------|-------|----------|------------|------|------------|---------|--------|---------------------------------------------------------------------------------|---|
CAN-PRE-19-Z   |false  |         1|           3|OTT   |Orpheus Mini|243514   |   0.002|Longueur hors tout = 3.70 m¶Gamme de mesure = 0.4 bar                            | 57|
CAN-PRE-52-Z   |false  |         1|           3|OTT   |Oprhéus mini|294341   |    0.01|Longueur hors tout : 14,2 m¶gamme de mesure 0-20m                                | 69|
CAN-PRE-02-Z   |false  |         1|           3|STS   |STS DL/N    |295802   |        |capteur piézométriqueinstallé le 19/07/2005réglé le 15/08/2005enregistrement a l | 65|
CAN-PRE-01-Z   |false  |         1|           3|STS   |STS DL/N    |295801   |        |capteur piézométriqueinstallé le 19/07/2005réglé le 15/08/2005enregistrement a l | 71|

[Retour au sommaire](#sommaire) 

 # <a id="sensorlocationlink">sensor_location_link</a>

id |location_id|udate_begin        |udate_end          |station_site_id|sensor_id|famille_id|data_type_id|
---|-----------|-------------------|-------------------|---------------|---------|----------|------------|
374|          4|2002-02-07 11:00:00|2002-04-11 10:45:00|               |       30|          |            |
297|         11|2011-12-19 11:15:00|                   |               |      181|         1|           3|
264|          1|2009-12-16 14:30:00|                   |               |      144|         1|           5|
196|         30|2006-12-06 16:30:00|2009-10-15 13:01:00|               |      144|         1|           5|
145|        130|2005-11-03 14:15:50|                   |              7|       84|         1|           9|
355|        207|2010-08-18 12:20:00|                   |               |      211|         1|           5|

Association du point de mesure et du capteur 
 
 - id : 
- location_id : lien avec la table location (Point de mesure)
- udate_begin : date debut du sensor
- udate_end : date de fin du sensor
- station_site_id : 
- sensor_id : 
- famille_id : lien avec la table famille (famille des type de données)
- data_type_id : lien avec la table data_type_hydras ** à Verifier ** (liste des type de données)

[Retour au sommaire](#sommaire) 

 # <a id="sensorsuffixe">sensor_suffixe</a>

id|name      |name_en    |famille_id|
--|----------|-----------|----------|
 0|Z         |Z          |         1|
 1|Uflow     |Uflow      |         1|
16|h         |h          |         1|

Suffixe le capteur par le type de données 

[Retour au sommaire](#sommaire) 

 # <a id="site">site</a>

id|catchment_id|cadastral_parcel_id|name                  |description                                                              |
--|------------|-------------------|----------------------|-------------------------------------------------------------------------|
 1|           2|                   |Gueriniec             |Transect lieu-dit Gueriniec ¶Propriétaire des parcelles :Gillard Michel  |
 2|           2|                   |Kerolland             |Transect du lieu-dit  Kerolland¶propriétaire: Le Douarin Dominique       |
 4|           2|                   |Fournello             |Transect lieu-dit Fournello¶Propriétaire : Le Toquin Jean Claude         |
 5|           2|                   |Exutoire              |Exutoire au lieu dit Kervidy (intersection de la route et du ruisseau)   |
22|          13|                   |Exutoire_Coat_Timon_9 | Exutoire N°9                                                            |

partie intra bassin versant

cadastral_parcel_id n'est pas utilisé

[Retour au sommaire](#sommaire) 

 # <a id="siteexp">site_exp</a>

id|nom                             |description                              |
--|--------------------------------|-----------------------------------------|
 3|Selune et Petits Fleuves Cotiers|                                         |
 2|Naizin                          |Site expérimental à Naizin (Morbihan)    |
 1|Kerbernez                       |Site expérimental à Plomelin  (Finistère)|
 4|Pont-Lagos                      |dfhjdg                                   |

Site experimental : Naizin, Kerbernez, Selune

[Retour au sommaire](#sommaire) 

 # <a id="staff">staff</a>

id|name          |firstname|email                                 |phone          |
--|--------------|---------|--------------------------------------|---------------|
 0|Hamon         |Yannick  |yannick.hamon@rennes.inra.fr          |02-23-48-57-90 |
 2|Le Henaff     |Genevieve|Genevieve.Lehenaff@rennes.inra.fr     |02-23-48-52-24 |
 5|Gilliet       |Nicolas  |gilliet@roazhon.inra.fr               |02-23-48-57-90 |

 Personnel = 10 car insertion auto

[Retour au sommaire](#sommaire) 

 # <a id="suivibdata">suivi_bdata</a>

id    |site_exp_id|caracteristique_id|location_id|famille_id|data_type_id|datedeb            |datefin            |n        |
------|-----------|------------------|-----------|----------|------------|-------------------|-------------------|---------|
     7|          2|                 1|         16|         1|           3|2014-03-15 21:15:00|2015-07-08 08:45:00|    46021|
710182|          1|                 1|         55|         1|           2|2001-09-07 09:00:00|2019-12-19 12:00:00| 25661712|
710183|          1|                 1|         55|         1|           5|2010-08-31 09:42:00|2019-12-19 12:00:00| 12679728|

[Retour au sommaire](#sommaire) 

# <a id="suiviedata">suivi_edata</a>

id    |site_exp_id|caracteristique_id|location_id|famille_id|data_type_id|datedeb            |datefin            |n      |
------|-----------|------------------|-----------|----------|------------|-------------------|-------------------|-------|
     0|          2|                 2|          1|         2|           3|2000-01-12 12:00:00|2018-01-25 12:00:00|    800|
684776|          2|                 2|          1|         2|           5|2000-01-12 12:00:00|2018-01-25 12:00:00|    800|
684777|          2|                 2|          1|         2|          11|2000-01-12 12:00:00|2018-01-25 12:00:00|    800|
684778|          2|                 2|          1|         2|          12|2000-01-12 12:00:00|2018-01-25 12:00:00|    800|
684779|          2|                 2|          1|         2|          14|2000-01-12 12:00:00|2018-01-25 12:00:00|    800|

Calcul de données validees insérées, date min, date max. Sert au tableau Gros doigts

[Retour au sommaire](#sommaire) 

# <a id="suivijdata">suivi_j_data</a>

id |location_id|famille_id|data_type_id|udate              |n |
---|-----------|----------|------------|-------------------|--|
  1|          1|         1|           3|2001-07-31 00:00:00|35|
  2|          1|         1|           3|2001-08-01 00:00:00|96|
  3|          1|         1|           3|2001-08-02 00:00:00|96|
  4|          1|         1|           3|2001-08-03 00:00:00|96|

[Retour au sommaire](#sommaire)

# <a id="suivibdata">suivibdata</a>

id|location_id|famille_id|data_type_id|datedeb            |datefin            |n      |
--|-----------|----------|------------|-------------------|-------------------|-------|
 1|          1|         1|           3|2001-07-31 15:15:00|2013-08-28 08:00:00| 419980|
 2|          1|         1|           5|2009-12-16 14:30:00|2013-08-28 08:00:00| 129671|
 3|          2|         1|           3|2001-07-31 15:15:00|2013-08-28 08:00:00| 394749|

 le ménage a du bon parfois...

[Retour au sommaire](#sommaire) 

# <a id="treedata">treedata</a>

id |td  |location_id|n|
---|----|-----------|-|
  1|1003|          1|1|
  2|1005|          1|1|
  3|2003|          1|1|

[Retour au sommaire](#sommaire) 

# <a id="unite">unite</a>

id|name         |description|
--|-------------|-----------|
 1|M            |           |
 2|Unite PH     |           |
 3|Na           |           |
 4|Degre Celsius|           |
 5|MV           |           |
 6|MicroS/cm    |           |
 7|Mg/L         |           |
 8|?            |           |
 9|Micro G/L    |           |
10|Pour Mille   |           |

[Retour au sommaire](#sommaire) 

# <a id="variableassociee">variable_associee</a>

id|name        |famille_id|data_type_id|description               |
--|------------|----------|------------|--------------------------|
 1|DateAnaPO4  |         3|          26|Date analyse de DateAnaPO4|
 2|DateAnaP-SAS|         3|          27|data analyse P-color-SAS  |

[Retour au sommaire](#sommaire) 
