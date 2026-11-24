



Presentasi Akhir Tugas Pemrograman **KASDAD** 





Presented By: **Kasdiddy** 







<!-- Start of picture text -->
mast i= ten<br>Le ai<br>SS ee<br>Wavart £ OR ee Te<br><!-- End of picture text -->



<!-- Start of picture text -->
Dion Wisdom P.<br><!-- End of picture text -->

2406414536 

## Kasdiddy 









<!-- Start of picture text -->
Helven Marcia<br><!-- End of picture text -->

**M. Aly Haidarulloh Raihan Maulana H.** 2406425804 2406351024 



<!-- Start of picture text -->
Raihan Maulana H.<br><!-- End of picture text -->

2406359853 

2406425804 







##### Dataset 

**time temperature_2m (°C) relative_humidity_2m (%) dew_point_2m (°C) apparent_temperature (°C) precipitation (mm) pressure_msl (hPa) surface_pressure (hPa) cloud_cover (%) cloud_cover_low (%) cloud_cover_mid (%) cloud_cover_high (%) soil_temperature_100_to_255cm (°C) soil_moisture_0_to_7cm (m³/m³) soil_moisture_7_to_28cm (m³/m³) soil_moisture_28_to_100cm (m³/m³) soil_moisture_100_to_255cm (m³/m³) shortwave_radiation (W/m²) direct_radiation (W/m²) diffuse_radiation (W/m²) direct_normal_irradiance (W/m²) global_tilted_irradiance (W/m²) terrestrial_radiation (W/m²) is_day () sunshine_duration (s) electricity_shutdown** 



: Timestamp of data collection. 

: Air temperature at 2 meters above ground level, measured in degrees Celsius. : Relative humidity at 2 meters above ground level, measured in percentage. : Dew point temperature at 2 meters—the temperature at which air becomes saturated with water vapor, measured in degrees Celsius. : "Feels like" temperature perceived by the human body, measured in degrees Celsius. : Total amount of precipitation (rain) recorded over a specific period, measured in millimeters. : Atmospheric pressure at mean sea level, measured in hectopascals (hPa). : Atmospheric pressure at ground level, measured in hectopascals (hPa). : Percentage of the sky covered by clouds at a specific time. : Percentage of the sky covered by low-level clouds (near the surface). : Percentage of the sky covered by mid-level clouds (middle altitude). : Percentage of the sky covered by high-level clouds (high altitude). : Soil temperature at a depth of 100 to 255 cm from the surface, measured in degrees Celsius. : Soil water content at a depth of 0 to 7 cm, measured in cubic meters of water per cubic meter of soil. : Soil water content at a depth of 7 to 28 cm, measured in cubic meters of water per cubic meter of soil. : Soil water content at a depth of 28 to 100 cm, measured in cubic meters of water per cubic meter of soil. : Soil water content at a depth of 100 to 255 cm, measured in cubic meters of water per cubic meter of soil. : Shortwave radiation reaching the ground surface, measured in watts per square meter. : Direct radiation from the sun reaching the ground surface, measured in watts per square meter. : Diffuse (scattered) radiation reaching the ground surface, measured in watts per square meter. : Direct radiation measured perpendicular to the ground surface, measured in watts per square meter. : Total radiation received by a tilted surface, measured in watts per square meter. : Radiation emitted by the Earth's surface, measured in watts per square meter. : Indicator of whether the data was collected during the day (1) or night (0). : Duration of sunshine recorded during a specific period, measured in seconds. : Indicator of whether a power outage occurred at a specific time (1) or not (0). 







# Explanatory Data Analysis (EDA) 







1.Seberapa tidak seimbang (imbalanced) distribusi target electricity_shutdown dan berapa persentase kelas positifnya? 

###### 2. Bagaimana karakter distribusi precipitation dan apakah terdapat zeroinflation? 



<!-- Start of picture text -->
Distribusi target electricity_shutdown=<br>10000<br>8000<br>6000<br>4000<br>2000<br>(0)<br>0.0 10<br>0 = Tidak Mati Lampu | 1 = Mati Lampu<br><!-- End of picture text -->



<!-- Start of picture text -->
Co oe<br>10000 Distribusi Precipitation<br>8000<br>‘gz 6000<br>a<br>Z<br>E 4000<br>2000<br>0<br>° 7 os ipitati ay 20 =<br>ecipitation (mm)<br><!-- End of picture text -->



<!-- Start of picture text -->
.<br>Histogram (log-scale y)<br>107<br>10?<br>_;<br>3|<br>> |<br>§ 10? ‘<br>3 '<br>F |<br>i. #<br>{<br>10°; §<br>0 5 10 15 20 25<br>Curah Hujan (mm)<br><!-- End of picture text -->

heavily right-skewed zero-inflation yang signifikan → Membutuhkan skewness handling 

Sangat tidak seimbang Kelas positif 0.795% 

→ Membutuhkan imbalance handling 



<!-- Start of picture text -->
oe<br><!-- End of picture text -->





###### 3.Fitur cuaca apa yang memiliki korelasi tertinggi dengan precipitation? 

Korelasi linearitas (pearson) lemah dengan precipitation 

Tidak ada satupun fitur bawaan yang memiliki skor linearitas > 0.5 terhadap precipitation 

→ Model regresi berbasis linearitas seharusnya **tidak digunakan** untuk memprediksi precipitation 



<!-- Start of picture text -->
Pearson correlation<br>temperature_2m (°C)<br>relative_humidity_2m (%)<br>dew_point_2m (°C)<br>apparent_temperature (°C)<br>pressure_msl (hPa)<br>surface_pressure (hPa)<br>cloud_cover (%)<br>cloud_cover_low (%)<br>cloud_cover_mid (%)<br>cloud_cover_high (%) 1.0<br>vapour_pressure_deficit (kPa)<br>wind_speed_10m (km/h)<br>wind_speed_100m (km/h) 08<br>wind_direction_10m (°)<br>wind_direction_100m (°) 0.6<br>wind_gusts_10m (km/h)<br>soil_temperature_O_to_7cm (°C)<br>soil_temperature_7_to_28cm (°C) 0.4<br>soil_temperature_28_to_100cm (°C)<br>soil temperature_100_to_255cm (°C)<br>soil_moisture_0_to_7cm (m?/m?) 0.2<br>soil_moisture_7_to_28cm (m?/m?)<br>soil_moisture_100_to_255cmsoil_moisture_28 to_100cm (m?/m?)(m?/m?) 0.0<br>shortwave_radiation (W/m?)<br>direct_radiation (W/m?)<br>diffuse_radiation (W/m?)<br>direct_normal_ irradiance (W/m?)<br>global_tilted_irradiance (W/m?)<br>terrestrial_radiation (W/m?)<br>is_day ()<br>sunshine_duration (s)<br>precipitation (mm)<br>electricity_shutdown<br>precipitation (mm)<br><!-- End of picture text -->



<!-- Start of picture text -->
Spearman correlation<br>temperature_2m (°C)<br>relative_humidity_2m (%)<br>dew_point_2m (°C)<br>apparent_temperature (°C)<br>pressure_msl (hPa)<br>surface_pressure (hPa)<br>cloud_cover (%)<br>cloud_cover_low (%)<br>cloud_cover_mid (%)<br>cloud_cover_high (%) 10<br>vapour_pressure_deficit (kPa)<br>wind_speed_10m (km/h) os<br>wind_speed_100m (km/h) :<br>wind_direction_10m (°)<br>wind_direction_100m (°) 0.6<br>wind_gusts_10m (km/h)<br>soil_temperature_0_to_7cm (°C) 04<br>soil_temperature_7_to_28cm (°C) .<br>soil temperature_28_to_100cm (°C)<br>soil_temperature_100_to_255cm (°C) 0.2<br>soil_moisture_O_to_7cm (m?/m?)<br>soil_moisture_7_to_28cm (m?/m?)<br>soil_moisture_100_to_255cmsoil_moisture_28_to_100cm (m?/m*)(m?/m?) 0.0<br>shortwave_radiation (W/m?)<br>direct_radiation (W/m?)<br>diffuse_radiation (W/m?)<br>direct_normal_irradiance (W/m?)<br>global_tilted_irradiance (W/m?)<br>terrestrial_radiation (W/m?)<br>is_day ()<br>sunshine_duration (s)<br>precipitation (mm)<br>electricity_shutdown<br>precipitation (mm)<br><!-- End of picture text -->



<!-- Start of picture text -->
ES<br><!-- End of picture text -->





###### 4.Apakah terdapat pola temporal (jam/bulan/hari) pada shutdown listrik dan kapan puncaknya terjadi? 



<!-- Start of picture text -->
Shutdown Rate per Jam<br>0.0175<br>0.0150<br>2> 0.0125<br>3<br>£ 0.0100<br>5<br>8 0.0075<br>2a<br>0.0050<br>0.0025<br>0.0000<br>° 5 10 15 20<br>Hour<br><!-- End of picture text -->



<!-- Start of picture text -->
Shutdown Rate per Hari<br>0.016<br>0.014<br>0.012<br>0.010<br>0.008<br>0.006<br>0.004<br>0 1 2 3 4 5 6<br>Day of Week<br><!-- End of picture text -->

Peak hour = 20 



<!-- Start of picture text -->
Peak day =  1<br><!-- End of picture text -->





<!-- Start of picture text -->
Shutdown Rate per Bulan<br>0.025<br>0.020<br>0.015<br>0.010<br>0.005<br>0.000<br>2 4 6 8 10 2<br>Month<br><!-- End of picture text -->

Peak month = 3 

→ Fitur time menjadi indikator penting untuk shutdown listrik 



<!-- Start of picture text -->
ae<br><!-- End of picture text -->



###### 5.Apakah ada korelasi yang kuat atau multikolinearitas di antara fitur-fitur independen itu sendiri? 

Pasangan fitur dengan nilai korelasi absolut tinggi (mendekati 1 atau -1) mengindikasikan adanya multikolinearitas. 

- → Ini perlu diperhatikan dalam pemilihan fitur, terutama jika tujuannya adalah clustering. 



<!-- Start of picture text -->
temperature_2m Matriks Korelasi Umum Semua Fitur Numerik 156<br>relative humiity_2m c oory am07 0000 am020 on012 om01702000 Jam)om on01s 00oz ooon [il | aisoes 01200s 20000 |e205 omoe onox omors ee 257 || oon |[owae | om008 00801 207aos<br>corse denenpeance pon.2m [l) 037 diama2 020 0 012 0 1400 9m01 o ntn B-00) 001 00 06 2 60 0 7 a»00s 08Bl [ose270co cn019 [emcos o ne exaot onon ] ovae [ om  lem[aie] om [omee [ omeat [ie t l om at otevs ono[eas] on200<br>pressures! 029 007 |936 029 on 005 017 928 on on 012 014 018 020 oo oor on oor on on on oon os om oo 01 020 015 00 019 009 018 025<br>surface pressure 013 000 028 020 O11 005 016 027 004 008 009 016 018 014 025 |034 023 006 034 032 027 035 003 003 014 008 003 012 009 008 012 001 017<br>dowd.cover 00/02 023 et on on [eo 017 007 ai 005 01 a1 009 010 007 17 |B 023 018 Os 90 018 0 an 90 008 0m on Om On Om<br>doud_cover.low 001 012 014 000 005 005 04 000 010 006 007 007 011 012 00> 002 016 017 OM 002 O62 000 001 006 G15 010 ao O10 005 002 om 00 0x<br>loud cover.mid 001 037 038 001 | 037 ow (0) BJ > 218 001 0 a0 on 10 0 0% 0m 2 on om oun 018 008 038 007 019 908 004 oo 01 025 on 007<br>sence doud.cress o v e r.highcet FIT902 029 021co FIaot |028on anoo lona17 om010 020018 ow oie oo o xo on018 a0om ee:oo om ou ‘001on om00s (aaon027 01oe o nm|e 8x | 019ev [BB]00  om023 | 013om [see20 IEE007 018| 207M1 00 76 012205 0.90<br>wind speed_10m os [| on om 911 008 007 006 008 aoe [os | om on [ese oe 010 008 905 906 000 oo 8 oe oe om ae om one om 008 008 on<br>wind speed 100m 015 |027 006 000 012 0 012 007 012 0m 026 ou 0 024 005 010 008 000 062 003 oo 020 017 071 014 020 020 013 016 008 om 015<br>winddirection.10m 008 012 007 006 014 014 005 067 009 018 032 009 O14 00) 904 009 006 007 019 021 02 027 011 ON O06 012 91 O08 010 012 01 O01 O14<br>{<br>wind direction 100m 205 011 aos 067 018 918 cos om on on 019 01 a1 007 905 008 007 007 022 025 02 |082 009 01 003 012 0m 06 008 010 0c 002 019 0.25<br>wid, gusts_10m (=) ES am ou on on 01 20 oo 07 00s om 00% on om 0m om on on 20<br>sotsempeae.907m 1234 025 0 0m 00 on Joe om 208 005 017 00 00% 208 000 006 xe [em om<br>sail temperature 7_t0.28em 626 008 oe on car oe 010 00) 006 014 000 02 005 aon 006 00s 026 001 009 0m 015 00 on 001 018 om oo 04 0 on [ea) =<br>solltemperature28,t0.100cm 012 905 032 022 035 023 007 016 003 0 001 010 010 006 087 908 017 cot 003 ore 01s 008 202 005 007 cos 004 oo aoe 000 on (BB) -0.00<br>soiltemperature100 t0.255¢m 008 002 013 013 007 006 017 017 005 908 a0 006 008 007 007 006 ao» | 026 29 012 019 014 000 002 006 005 00 003 900 000 oot ~<br>soil moisture 0_to7em | 995 (or ccs |935 [oa on on (oe en a 006 000 019 022 ac 006 om 008 009 82 020 007 02 012 002 om 019 Om 005 008<br>sellmosture_7.0.28em aot |030 | 035 006 |933032 02 002 | 028 fn ee 20 002 02 0% 002 0m 00 00 022 0m 018 0m om om 02 001 01 017 001 004<br>sellsoilmoisturemoisture100.t0.255c22,0 100¢ m 00aot 01 56 |0289st aot023 028 027 015on 90 28 0 18 [os os013 00 01 00 )1 02 07 024|a32 00 )3 00 63 0 1509 01 s6 0194 0 021 90 0 75 0 o0 7 0 0810 09 0 21 00 65 on000 00 78 008 901099 om207 -=0.25<br>shortwave radiation [a (Co) -: ee em ox an 0 0m 001 20 02 0m om om or 00 002<br>rect radiation [ey on oo 003 016 906 015 019 om oy on on an 00 0 920 035 007 005 os « | eco a0 000 9003<br>ate aan [RF oe) 82 014 016 015 007004 foe on 206 00 801 005 096 007 00s 007 007 059 | BM 022 om 200<br>Paver «|. Ee. Reeeerieeeyery| . (ieee |. eeleesieesiey)eraieraien -| =| sn<br>obal<br>tited radiance [lM oe | an 903 205 ao 008 on Jom ox on om 0 008 00 91 20 9 on 07 00 902<br>terrestrial radiation (le Bo | 970 012 008 010 0m 008 Joe ox 000 006 02 008 099 002 002 008 005 ° o ers<br>sunshine durationdoy (RRIF) oo m e PBB os0 200m 012m 90oes o son 207om [| om ors0% aseon o wm ou 00 48 2000m 20019 0 0116 008oo 007om 0 “ «| ‘ asea on o nm<br>precipitation 062 008 G16 005 012 012 025 02 025 O11 007 008 aoe Gol 002 aM O16 011 000 004 [aH 017 008 008 007 001 022 amt 007 O21 015 cot ce ae 0.78<br>tour 016 006 |@30| 023 20) 001 012 ao» on 007 0m ams arr on am a oe our 201 000 088 aol 901 000 00) 000 co 00) 00) om oni on om eo<br>month 207 00 010 007 018 017 000 0m 007 012 005 On 915 9M 019 007 008 on 28 204 a0 001 007 202 902 om 002 902 001 202 00 082 0m<br>£ € £€ ¢ Be Be ¢ § § € € € £€ § §€ £ § § € $¢ $ § FE § & FE<br>SSS PEF ER ERE EES EEE EEE EES ER EE EEE EET GE<br>225 2 § & = EF Pe F Ps gg se sess pee EE EE 8S<br>eR Ege EE SEE EET ESS REE EER EA Ee EEG : £<br>a 23 5 8 3 Bee Ee SE EF EE RE Ee REE E zB é 5<br>¢ Ff + ee ee ee ee 5 3<br>3 i : ' 3 § 28 @€ ee § ¢ 23 *<br>: : PERE? it y 4<br>3 & &€ # oo & s<br>eas |<br>* 3<br><!-- End of picture text -->





- 6.Fitur mana yang berkorelasi serta dampak fitur tersebut beberapa jam yang lalu terhadap presipitasi saat ini 

Fitur **cloud_cover** , **soil_moisture** , **dew_point** merupakan prediktor utama. 

Lag efektif pada **1-3jam** tolerable hingga 6jam 

→ Dapat dilakukan **feature engineering** berupa feature lag terutama untuk prediktor utama 



<!-- Start of picture text -->
Dampak Fitur Cuaca (Lag 1-12 Jam) Terhadap Presipitasi Saat Ini<br>ID- -0.05 0.05 0.05 0.05 -0.05 0.05 -0.05 0.05 0.05 0.05 0.05 0.05 05<br>temperature_2m (EDEC) 0.06 0.06 0.14 0.27 0.29<br>relative_humidity_2m(%)- 0.01 -0.06 0.10 0.11 0.10 0.06 0.01 0.07 0.13<br>dew_point_2m (JEQEC) Ue 0.47 1.44 0.40 0.33 0.26 Psy 0.02 0.09 013 0.14<br>apparent_temperature ((JEJ/EC) 0.30 0.36 0.37 0.35 0.29 0.11 0.01 0.11 EEE 0250 027 | o4<br>pressure_msl(hPa)- 0.17 0.13 0.08 0.03 0.01 0.02 0.02 0.00 0.02 0.04 0.05 -0.03<br>surface_pressure (hPa)- 0.14 0.10 0.05 0.00 0.03 0.04 0.03 0.00 0.04 0.06 -0.07 -0.06<br>cloud_cover (%) .51 0.4¢ 0.31 0.24 0.18 0.13 0.10 0.08 0.08 0.09 0.09 0.11<br>8<br>cloud_cover_low (%) Ma 0.34 0.27 016 0.12 0.08 0.07 0.05 0.03 0.03 0.04<br>cloud_cover_mid (%) ag 0.38 0.31 0.25 0.15 0.11 0.08 0.08 0.08 0.09 0.11<br>cloud_cover_high (%)- 0.14 0.11 0.08 0.06 0.05 0.05 0.05 0.07 0.08 0.09 0.11 0.12<br>vapour_pressure_deficit (kPa)- 0.04 0.11 0.15 0.16 0.13 0.08 0.01 0.07 0.13 0.18 Ee) 025 | 02<br>wind_speed_10m (km/h) - 0.15 0.15 0.14 0.11 0.07 0.02 0.04 0.06 0.09 0.10 010 -0.10<br>wind_speed_100m (km/h) - 0.13 0.11 0.09 0.06 0.02 0.02 0.05 0.08 0.08 0.08 0.07 -0.06<br>wind_direction_10m (QEDE)- -0.05 0.05 0.06 0.05 0.04 0.02 0.01 0.04 0.05 0.08 0.11 0.14 &<br>s wind_direction_100m (QEQE)- -0.01 0.01 0.01 0.00 0.00 0.03 0.04 0.06 0.08 0.10 0.13 0.14 -o1 :<br>fs} wind_gusts_10m (km/h) eI 0.37 0.34 0.29 0.15 0.06 8=6-0.01 0.08 013 017 0.19 8<br>soil_temperature_7_to_28cm ([JEJEC)- 0.12 0.04 0.04 0.13 0.28 0.32 0.34 0.34 0.31 0.27 3<br>soil_temperature_100_to_255cmsoil_temperature_28 to_100cm ({JE[EC)-(JEQEC)- -0.070.10 0.070.10 0.070.10 0.070.10 -0.07010 -0.06010 -0.060.10 0.050.10 0100.04 0.040.10 -0.03010 0.03 -0.10 -0.0<br>soil_moisture_0_to_7cm (m?/m?) 0.38 0.31 0.26 0.23<br>soil_moisture_7_to_28cm (m?/m?) -ursy 0.24<br>soil_moisture_28_to_100cm (m?/m?) 8 0.17 8 0.17 Ol 1 0.18 0.1 . ( 8 0.17 --0.21<br>soil_moisture_100_to_255cm (m?/m?)- 0.14 0.14 0.14 0.14 0.14 0.14 0.14 0.14 0.14 0.14 0.14 0.14<br>shortwave_radiation (W/m?) 0.31 0.37 .40 0.39 0.35 0.28 0.09 0.01 0.11 0.19, 0.26<br>direct_radiation (W/m?) 7 ez) 0.31 0.35 0.35 0.32 0.26 0.17 0.08 -0.02 0.12 0.20 Bert)<br>diffuse_radiation (W/m?) OEE ROLE 044 041 036 | 028 010 000 0.09 017 70.2<br>direct_normal_irradiance (W/m?) 0.27 0.32 0.33 0.31 0.26 ( 0.09 -0.01 0.11 -0.26<br>global_tilted_irradiance (W/m?) 0.31 0.37 2.40 0.39 0.35 0.28 0.09 0.01 0.11 0.19 -0.26<br>terrestrial_radiation (W/m?) OEE) 0.44 0.4 0.43 0.37 0.29 0.09 0.01 011 0.18 | Ph)<br>is_day () 0.29 0.33 0.36 0.37 0.34 0.30 0.24 0.08 -0.03 -0.13 aad<br>sunshine_duration (s) 0.27 0.31 0.31 0.29 0.24 a7 009 0.01 0.10 0.18<br>laglh Lag2h Lag3h tLag4h LagSh Lag6h Lag7h Lag 8h lag 9h Lag 10h Lag 11h Lag 12h<br>Jeda Waktu ke Belakang<br><!-- End of picture text -->



<!-- Start of picture text -->
oe<br><!-- End of picture text -->





<!-- Start of picture text -->
Analisis Periode Cuaca Ekstrem<br>Suhu bulanan Total curah hujan bulanan<br>32 _o--3o_o —@ooMaksimum «oo<br>30 ~e---0--@<br>=" \ ana<br>Nee<br>E<br>oe 28 ® E 400<br>26<br>mI 200 ln<br>22 qT 0<br>Jan Feb Mar Apr Mei jun Jul. Agu Sep Okt’ «Nov Des Jan Feb Mar Apr Mei jun Jul. Agu Sep Okt» Nov Des<br>92 Kelembapan relatif bulanan Pola harian rata-rata<br>28-—se ~saecm= -90<br>90 aN /<br>27 - \ t<br>\ U<br>88 26 - .\ 7 L 85<br>3 86 Y 25 - ‘ # x<br>84 x ¢ - 80<br>24 - ‘ 7<br>\ ,<br>82 | 23 -——~ \ ri — Suny (°C) -75<br>80 22 - ——__I SoU? — = Kelembapan(%)<br>Jan Feb Mar Apr Mei Jun ul,» Agu Sep Okt’ = Nov Des (0) 3 6 9 12 15 18 21<br>Jam<br>10 hari dengan curah hujan harian tertinggi<br>2022-09-30A 6.7m<br>2023-02-09 42.6 mm<br>2022-10-02 a, 40-5 mm<br>2022-10-26 a! 40-2 mm<br>2022-12-05 224mm<br>2022-01-20a 3.3mm<br>2022-12-26CT 25.6 mm<br>2023-03-02 ns 25-5mm<br>2022-10-21ET 23.2 mm<br>2022-11-25a! 23.2mm<br>0 10 20 30 40 50 60 70<br>Total curah hujan harian (mm)<br><!-- End of picture text -->

###### 7.Apakah terdapat periode waktu tertentu yang memiliki karakteristik cuaca ekstrem? 

   - 1.Suhu panas ekstrem di bulan Mei–Juni 2023, dengan puncak 31.5°C pada pukul 12:00–13:00. 

   - 2.Kelembapan ekstrem di Oktober– November, dengan rata-rata mencapai 88–89%. 

   - 3.Hujan ekstrem paling sering terjadi di Oktober–Februari.. 

   - 4.Juli–Agustus adalah musim paling kering (128–182 mm). 

- → Periode cuaca ekstrem ini berpotensi membentuk cluster tersendiri (sangat panas, sangat lembap, curah hujan tinggi, curah hujan rendah). 





###### 9.Bagaimana pola wind_speed_10m dan wind_speed_100m? 



<!-- Start of picture text -->
Analisis Pola Wind Speed: 10m vs 100m<br>Scatter Wind Speed 10m vs 100m<br>Distribusi Kecepatan Angin 10m vs 100m (r = 0.903) Boxplot Perbandingan Ketinggian Angin<br>0.14 — 10m 30 == Trendline a 30 8<br>— 100m a“<br>0.12 : _ 25 at 25<br>| < “ =<br>0.10 £ 6,3 = °<br>~ 20 ee eee § 20<br>— 60 ORs 4<br>28 0.08 5 . RS ikwf 5<br>& 0.06 t | 502 BeBeetie <15g<br>0.04 ! 10 hs a & 10<br>I = e ap y<br>14 z ’ @<br>i 5 ie 5<br>0.02 I = é Re =<br>I ne<br>I ”; aoa<br>0.00 4 0 . 0<br>—-10 0 10 20 30 40 0 5 10 15 20 10m 100m<br>Kecepatan Angin (km/h) Wind Speed 10m (km/h)<br><!-- End of picture text -->



<!-- Start of picture text -->
*%<br><!-- End of picture text -->

nilai korelasi  r ≈ 0.903 

###### Berkorelasi sangat tinggi akan tetapi tidak sempurna (>0.95) 

- → Kedua fitur tidak bersifat redundan dan dapat dipertahankan untuk clustering features 

- → Dapat dipertimbangkan untuk membuat fitur turunan berupa wind_shear (wind_speed_100m - wind_speed_10m) 





###### 10.Apakah volume dan ekstremitas hujan menengah-lebat (>3 mm & >7 mm) berbeda signifikan antara hari normal dan hari pemadaman? 



<!-- Start of picture text -->
DistribusiistribusiHujanHujan SaatSaat TurunTurun HujHujan (> 77 mm) Outlierjutlier CurahCurahHujHujan (> 77mm)<br>ertriey.statsonn 27.5 °<br>0.30 FI 25.0<br>0.25 22.5<br>g 20.0<br>B 020 2 3<br>Fa g 175 8<br>& 0.15: 3£ 50<br>0.10 25 ==<br>0.05 10.0<br>75<br>on 5 10 15 20 3.~C«OO Ne OF ti 0} Por Outat 1<br>jormal Operation (0) wer Outage (1)<br>Precipitation Electricity Status<br><!-- End of picture text -->



<!-- Start of picture text -->
Distribusi Hujan Saat Turun Hujan (> 3 mm) Outlier Curah Hujan (> 3 mm)<br>0.175 electricity_shutdown °<br>— 2s<br>re<br>0.150<br>20<br>0.125 8<br>& 8<br>2g v.10 £4,<br>8 0.075 rfg$<br>10<br>0.050<br>0.025 5<br>:<br>0.000 ———<br>-5 0 5 10 15 20 35 30 Normal Operation (0) Power Outage (1)<br>Precipitation Electricity Status<br><!-- End of picture text -->



###### Risiko pemadaman listrik terbukti tidak linear dengan intensitas hujan melainkan 

terkonsentrasi di kisaran 10-14 mm 

fitur yang berelasi kuat dengan presipitasi (soil_moisture_0_to_7cm dan fitur fisik terkait) berpeluang  sebagai prediktor. 

- → Terapkan log transform pada fitur skewed seperti soil moisture dan VPD untuk menekan dominasi outlier 

- → Gunakan RobustScaler secara universal sebelum masuk ke model apapun karena data cuaca rentan terhadap nilai ekstrem 

- → Buat fitur interaksi seperti storm_composite (angin × kelembaban × tutupan awan) dan soil_wetness_gradient (selisih moisture antar lapisan tanah) untuk menangkap hubungan non-linear antar variabel 





# General Preprocessing 







<!-- Start of picture text -->
I<br><!-- End of picture text -->

###### **Fix corrupted column names** 



<!-- Start of picture text -->
ENCODING MAP = [<br>r oir OLEL [WEE ace | + eek Sa - > aG ’<br>r'\x81E E|@EBE ry ,<br>roa 13/m3, 1 5<br>r i = 2» 2')><br>]<br>def fix_col_name(col):<br>for pattern, replacement in ENCODING MAP:<br>col = re.sub(pattern, replacement, col)<br>return col<br><!-- End of picture text -->



<!-- Start of picture text -->
train_df = pd.read_csv(‘ - )<br>test_df = pd.read_csv(' - )<br>train_df.columns = [fix_col_name(c) for c in train_df.columns]<br>test_df.columns = [fix_col_name(c) for c in test_df.columns]<br>print( ‘Train col S er fix:', list(train_df.columns[:5]), )<br><!-- End of picture text -->



###### **Drop ID & Target** 



<!-- Start of picture text -->
cleaneddf = cleaned_df.dropna(subset=[‘electricity shutdown’, ‘ID‘])<br><!-- End of picture text -->

###### **Drop Duplicate** 



<!-- Start of picture text -->
cleaneddf = cleaned df.drop duplicates()<br><!-- End of picture text -->





###### **Missing Value Handling** 

###### interpolasi dan forward & backward fill 



<!-- Start of picture text -->
cleaned_df = cleaned_df.sort_values(' ") .reset_index(drop= )<br>kolom_numerik = cleaned_df.select_dtypes(include= ’ 4° }).columns<br>cleaned_df[kolom_numerik] = cleaned_df[kolom_numerik]. interpolate (method= » Limit_direction=<br>cleaned_df[kolom_numerik] = cleaned_df[kolom_numerik].ffill().bfill()<br>print(f cleaned_df.isnull().sum().sum )<br><!-- End of picture text -->



###### **Outlier Handling** 





<!-- Start of picture text -->
cap_cols = [c for c in kolom_numerik if c not in [ ri » ‘ID']]<br>lower_bounds = {}<br>upper_bounds = {}<br>for col in cap cols:<br>Ql = cleaned_df[col].quantile(@.25)<br>Q3 = cleaned_df[col].quantile(@.75)<br>IQR = Q3 - Ql<br>lower_bounds[col] = Q1 - 1.5 * IQR<br>upper_bounds[col] = Q3 + 1.5 * IQR<br>for col in cap cols:<br>cleaned_df[col] = cleaned_df[col].clip(lower=lower_bounds[{col], upper=upper_bounds[col])<br>print(t' 1 I i cleaned_df.shape[@]} i cleaned_df.shape[1 )<br><!-- End of picture text -->







**Transformasi Data** Temporal features & Cyclical encoding 



<!-- Start of picture text -->
processed _ df[ ] = processed _df[ ]-dt.hour<br>processed df[‘d ] = processed_df[‘t ].dt.dayofweek<br>processed _df[ ] = processed _df[ ].dt.month<br>processed _df[ ] = np.sin(2 * np.pi * processed_df[ ] / 24)<br>processed _df[ ] = np.cos(2 * np.pi * processed _df[ ] / 24<br>processed _df[ sin’] = np.sin(2 * np.pi * processed_df t / 12<br>processed _df[ t ] = np.cos(2 * np.pi * processed _df[ th'] / 12<br><!-- End of picture text -->









# TP 1: Classification (Decission Tree, Random Forest, LGBoost, XGBoost, KNN) 







<!-- Start of picture text -->
oa<br><!-- End of picture text -->



<!-- Start of picture text -->
processed_df<br>processed _df[ ] == processedprocessed_df[_df ]-rolling(24,]-rolling(6, min_periods=1)min_periods=1) .mean(.mean()<br>processed df ] = processed_df -rolling(12, min_periods=1) .mean<br>processed_df[ ] = processed_df[ ].diff(3).fillna(@<br>processed df = (processed_df == 20).astype(int)<br>processed _df[ _ uf ] = (processed_df[ ] == 3)-astype(int<br>processed _df = processed_df -rolling(12, min_periods=1)-.std().fillna(@<br>processed _df[ ] = processed_df[ ]-rolling(24, min_periods=1) .mean()<br>processed df = processeddf ].diff (6) .fillna(@<br>processed df = processeddf ] * processed_df ]<br>processed df ] = processed_df * processeddf<br>processed_df[ Z Z J= processed_df[ = ] * processed_df[ a J<br>processed _df[ gust t ] = processed_df[ t ] / (processed_df[ ] + 1e-5)<br>processed_df[ ] = processed_df[ ] - processed_df[ ]<br>processed _df[ SS d ] = processed_df[ ssure_ms Pa)*] - processed _df['s ac sure Pa)*]<br>soil_col = [c for c in processed_df.columns if |<br>if soil_col:<br>processed _df u ##'] = processed_df - processed_df[soil_col[@]}]<br>else:<br>processed df ]=0<br>rad_direct = [c for c in processed _df.columns if c.startswith(‘d ct diatio ]<br>rad_short = [c for c in processed_df.columns if c.startswith<br>if rad_direct and rad_short:<br>else:<br>processed_df[processed _df ]]=90= processed_df[rad_direct[@]] / (processed_df[rad_short[@]] + 1e-5)<br><!-- End of picture text -->



<!-- Start of picture text -->
oe<br><!-- End of picture text -->



**Feature Engineering** 



###### **Split Feature & Target** 

Menggunakan stratified split Khusus **Random Forest** menggunakan temporal split 





<!-- Start of picture text -->
X = processed_df.drop(columns=[ I Z ])<br>y = processed_ df[ ]<br>X_train, X_val, y_ train, y_val = train_test_split(x, y, test_size=0.2, random_state=SEED, stratify=y)<br>print(f i X_train. shape {X_val.shape}, Counter (y_val )<br>n_split = int(len(Xx) * @.8)<br>X_train_rf, X_val_rf = X.iloc[{:n_split], X.iloc[n_split:]<br>y_train_rf, yval_rf = y.iloc[:n_split], y.iloc[n_split:]<br>print(f"Te a -- a X_train_rf.shape a X_val_rf.shape Counter(y_val_rf )<br>model metrics = {}<br><!-- End of picture text -->

**Cross Validation** StratifiedKFold dengan n_splits=4 



<!-- Start of picture text -->
cv_tree = StratifiedKFold(n_splits=4, shuffle=True, random_state=SEED)<br><!-- End of picture text -->







###### **Imbalance Handling** 

SMOTEENN: Oversampling + Noise Cleaning Untuk **Decision Tree** & **KNN** 





<!-- Start of picture text -->
# SMOTEENN for DT and KNN - kombinasi over+undersampling menghilangkan noise di batas keputusan yang muncul saat menggu<br>smoteenn = SMOTEENN(random_state=SEED)<br>X_train_resampled, y_train_resampled = smoteenn.fit_resample(X_train_clean, y_train)<br>print("Setelah SMOTEENN >", Counter(y_train_resampled))<br><!-- End of picture text -->

RandomUnderSampler: Undersampling Untuk **Random Forest** 



<!-- Start of picture text -->
# RandomUnderSampler for RF bagging RF sudah mendiversifikasi sampel, undersampling memastikan s<br>rus = RandomUnderSampler (random_state=SEED)<br>X_train_resampled_rf, y_train_resampled_rf = rus.fit_resample(X_train_rf_clean, y_train_rf)<br>print("Setelah RandomUnderSampler:", Counter(y_train_resampled_rf))<br><!-- End of picture text -->

Scale positive class weight (scale_pos_weight): memberi bobot lebih besar ke kelas positif (minority class) saat training. Untuk **XGBoost** 



<!-- Start of picture text -->
oa<br><!-- End of picture text -->



<!-- Start of picture text -->
print(f"scale_pos_weig {scale_pos_weight}")<br>scale_pos_weight = int((y_train == @).sum() / (y_train == 1).sum())<br><!-- End of picture text -->





###### **Imbalance Handling** 

class_weight=balanced: otomatis menghitung bobot tiap class berdasarkan frekuensi data. 



###### Untuk **LGBoost** 



<!-- Start of picture text -->
# class weight='balanced' - pembobotan loss native lebih stabil dari resampling untuk boosted trees, mer<br>base_lgbm_pipeline = Pipeline([<br>(‘scaler’', StandardScaler()),<br>(‘model', LGBMClassifier(class_ weight=‘balanced', random_state=SEED, n_jobs=-1, verbose=-1))<br>])<br><!-- End of picture text -->

**Feature Selection** Sequential Feature Selector dengan direction ‘forward’ dan jumlah fitur ‘auto’ (1/2 * total fitur) 

Untuk **Decision Tree** , **Random Forest** , dan **KNN** 



<!-- Start of picture text -->
se<br><!-- End of picture text -->



<!-- Start of picture text -->
sfs_tree = SequentialFeatureSelector(<br>estimator=best_tremod e l,_ n_features_to_select='auto',<br>direction='forward', scoring='f1l', cv=cv_tree, n_jobs=-1<br><!-- End of picture text -->





###### **Hyperparameter Tuning** 

GridSearchCV: Coba semua kombinasi parameter, lalu pilih yang performanya paling bagus. Untuk **Decision Tree** & **KNN** 



<!-- Start of picture text -->
param_grid_tree_ . _ = {<br>model__criterion':. : ['gini',— ‘entropy'],<br>"model __max_depth': [3, 5, 7, 10, None],<br>‘model__min_samples_split': [2, 5, 10],<br>‘model__min—samples 7leaf': [1, 2, 4]<br>}<br>base_tree_pipeline = Pipeline([<br>('scaler', StandardScaler()),<br>(‘model', DecisionTreeClassifier(random_state=SEED))<br>1)<br>grid_tree = GridSearchcCvi(<br>base treepipeline, param_grid tree,<br>CV=CV tree,| scoring='f1',= 'o4a n_jobs=-1,: verbose=1<br>_ _<br>)<br>grid_tree.fit(X_train_resampled, y_train_resampled)<br><!-- End of picture text -->



RandomizedSearchCV: Mencoba kombinasi parameter secara acak (random) 

###### Untuk **LightGBM** & **XGBoost** 



<!-- Start of picture text -->
2 aram_dist_lgbma =e = t<br>model__n_estimators': [100, 200, 300],<br>*model_max_depth': [4, 6, 8, -1],<br>‘model__learning_rate': [@.01, 0.05, 0.1],<br>‘model__num_leaves’: [31, 63, 127],<br>‘model__min_child_samples': [5, 10, 20]<br>}<br>#<br>class_weight="balanced' - pembobotan loss native lebih stabil dari resamp<br>base_lgbm_pipeline = Pipeline(([<br>(‘scaler’, StandardScaler()),<br>(EEET Wel GIES ISIN (IES) SLC WSN<br>random_state=SEED, n_jobs=-1, verbose=-1))<br>]))<br>rand_lgbm = RandomizedSearchcv(<br>base_lgbm_pipeline, param_dist_lgbm,<br>it =20, = lgb ; . ='f1',<br>never cvecv_'6 ms scoring<br>random_state=SEED, n_jobs=-1, verbose=1<br>)<br>rand_lgbm.fit(X_train_clean, y_train)<br><!-- End of picture text -->





###### Kaggle Score Graph 

Classification F1 





<!-- Start of picture text -->
Kaggle F1-Score Comparison: Public vs Private Leaderboard<br>mmm Public<br>Mam Private<br>0.06<br>0.0559<br>0.0506<br>0.05<br>0.0454<br>0.0425<br>w 0.04<br>5 0.0360<br>0) 0.0314<br>i 0.03 0.0291 0.0287 0.0291 0.0287 0.0290<br>0.0243<br>0.02<br>0.01<br>0.00<br>. ee ct iN uM st \e<br>pecision © gando™ son " ygnts® 40800 ensers®<br>Model<br><!-- End of picture text -->







# TP 2: Regression 







###### **Feature Engineering** 

Hanya beberapa fitur terbaik dari FE sebelumnya 



<!-- Start of picture text -->
# Fitur Interaksi & Cuaca (Sama seperti sebelumnya)<br>df_reg[ ‘wind _rolling6h'] = df_reg[ 'wind_speed_1@1 n/h)'].rolling(6, min_periods=1) .mean()<br>df_reg[‘pressure_drop3h'] = df_reg['surface_ pressure (hPa) ‘].diff(3).fillna(@)<br># Perhatikan: pastikan nama kolom temperatur sesuai dengan di datasetmu (tadi ada karakter aneh E..C)<br>df_reg[ ‘humid_heat'] = df_reg[ ‘temperature _2m (\x81E\x81EC)'] * df_reg['‘relative| humidity_21 ‘7<br>df_reg[‘cloud_humidity_index'] = df_reg['cloud_cover (%)'] * df_reg[ ‘relative_humidity_21 "J<br>df_reg[ ‘wind_gust_ratio'] = df_reg[‘wind_gusts_10m (km/h)'] / (df_reg[ 'wind_speed_10 km/h)’] + 1e-5)<br>df_reg['pressure_diff'] = df_reg['‘pressure_msl (hPa)'] - df_reg['surface_pressure (hPa)']<br><!-- End of picture text -->







###### **Additional Feature Engineering** 

###### **Untuk XGBoost, KNN, 2- stage** 

- 1.Lag Features 

- 2.Dew Point Depression (jarak suhu ke titik embun) 

- 3.Tren 3 jam terakhir kolom cloud_cover dan vapour_pressure_deficit (vpd) 

4. Perbedaan vpd dalam 3 jam 



<!-- Start of picture text -->
# Fit Lag<br>lag_cols = [<br>cloud_cover A<br>cloud_cover_mid "<br>shortwave i ) V h<br>]<br>lag_periods = [1, 2, 3]<br>lag_series = []<br>for col in lag_ cols:<br>if col in X.columns:<br>for lag in lag_periods:<br>safe_name = col.replace(" ", *).replace("(", "").replace(")", ).replace( 9 ").replace("2", "2")<br>lag_series.append(X[col].shift(lag).rename(f"{safe_name} lag{lag}h"))<br>if lag_series:<br>X = pd.concat([X] + lag_series, axis=1)<br># Dew Point Depressio Jarak Suhu ke Titik Embun)<br>if “temperat 2m ( in X.columns and “dé t 1 Cc)" in X.columns:<br># Rolling Aggregates re Jam Terakhir<br>cols_to_roll = ["cloud_cove ", “vapour_pressure_deficit (kPa)"]<br>for col in cols_to_roll:<br>if col in X.columns:<br>safe_name = col.replace(" ", "_").replace("(", "").replace(")", "").replace("/", "_")<br>X[f"{safe_name} roll_mea "] = X[col].rolling(window=3, min_periods=1) .mean()<br>X[f#"{safe_name} rol] | "] = X[col].rolling(window=3, min_periods=1).std().fillna(@)<br><!-- End of picture text -->



<!-- Start of picture text -->
Se<br><!-- End of picture text -->



<!-- Start of picture text -->
if "vapour_pressure_deficit (kPa)" in X.columns:<br>X["vpd_diff_3h"] = X["vapour_pressure_ deficit (kPa)"].diff(3)<br><!-- End of picture text -->





**Cross Validation & Split Feature** KFold dengan n_splits=4 (Decision Tree) dan n_splits=3 (RandomForest) 





<!-- Start of picture text -->
cv = KFold(n_splits=4, shuffle=True, random_state=SEED)<br><!-- End of picture text -->

TimeSeriesSplit dengan n_splits=5 (XGBoost & KNN) 



<!-- Start of picture text -->
tscv = TimeSeriesSplit(n_splits=5, gap=0)<br>fold_scores = []<br><!-- End of picture text -->

###### **Feature Selection** 

Sequential Feature Selector dengan direction ‘forward’ dan jumlah fitur 5 (hasil tuning) Untuk **Decision Tree** dan **Random Forest** 



<!-- Start of picture text -->
sfs_tree = SequentialFeatureSelector(estimator=model_tree,<br>n_features_to_select=5,<br>direction='forward',<br>scoring='r2',<br>cv=cv_tree, n_jobs=-1)<br><!-- End of picture text -->





###### **Hyperparameter Tuning** 

###### **Optuna** 

lebih efisien dibanding GridSearchCV atau RandomizedSearchCV. 

**Decision Tree** , **KNN** , **XGBoost** , **2-Stage** → Parameter yang dicari disesuaikan dengan model 



<!-- Start of picture text -->
optuna. logging. set_verbosity(optuna.logging. WARNING)<br>cv = KFold(n_splits=4, shuffle= , random _state=SEED)<br>def objective(trial):<br>rparame Dac<br>params = {<br>8 trial.suggest_int("max_depth", 2, 20),<br>g trial.suggest_int it", 2, 50),<br>s B trial.suggest_int(" > 1, 30),<br>= res": trial.suggest_categorical ("max_ 7 r, 32", None]),<br>iterion": trial.suggest_categorical iterion", - iedman_mse", lute_er ),<br>:trial.suggest_float( 1 » 0.0, @.1),<br>3 trial.suggest_float ( » 0.0, 0.05),<br>}<br>model = DecisionTreeRegressor(random_state=SEED, **params)<br>sfs = SequentialFeatureSelector(<br>estimator=model,<br>n_features_to_select=5,<br>direction= ;<br>scoring= ;<br>cv=cv,<br>n_jobs=-1<br>)<br>pipeline = Pipeline(<br>, StandardScaler()),<br>» KNNImputer()),<br>» sfs),<br>» model),<br>1p)<br>scores = cross_val_score(pipeline, X, y, scoring="r2", cv=cv, n_jobs=-1)<br>return scores.mean()<br><!-- End of picture text -->





###### **Classification** 

Melakukan klasifikasi (hujan or not) sebelum dilakukan regresi curah hujan. 

###### **2-Stage with XGB** 

- → Mengurangi beban regresi dimana model tidak perlu melakukan prediksi pada data yang diklasifikasikan sebagai tidak hujan 



<!-- Start of picture text -->
rain_binary train = (y train > @).astype(int<br>pos_ratio = (rain_binary train == @).sum() / max(1, (rain_binary train == 1).sum<br>+ ts_clf_objective(trial):<br>params = {<br>learning = trial.suggest_float( ‘learning e', @.02, 0.2, log= 5<br>ul B trial.suggest_int am » 3, 10),<br>ght": trial.suggest_int ght", 1, 12),<br>ample": trial .suggest_float ample’, @.6, 1.0),<br>: trial.suggest_float » 0.6, 1.0),<br>g da‘: trial.suggest_float g lambda’, 1e-4, 5.0, log=-True),<br>: pos_ratio,<br>e 1000,<br>2 SEED,<br>bs": =i<br>aucs = []<br>best_iters = []<br>for tr_idx, val_idx in tscv.split(X_train_clean):<br>clf = xgb.XGBClassifier(**params, early stopping _rounds=25)<br>clf.fit(X_train_clean.iloc[tr_idx], rain_binary_train.iloc[tr_idx],<br>eval_set=[(X_train_clean.iloc[val_idx], rain_binary train.iloc[val_idx])],<br>verbose= )<br>proba = clf.predict_proba(X_train_clean.iloc[val_idx])[:, 1]<br>aucs.append(roc_auc_score(rain_binary train.iloc[val_idx], proba<br>best_iters.append(clf.best_iteration<br>trial. set_user_attr( a ees’, max(1@, int(np.median(best_iters))))<br>return -float(np.mean(aucs<br>ts_clf_study = optuna.create_study(direction= » sampler=TPESampler(seed=SEED<br>ts_clf_study.optimize(ts_clf_objective, n_trials=25, show_progress_bar=|<br>ts_clf_best = ts_clf_study.best_params.copy(<br>ts_clf_trees = ts_clf_study.best_trial.user_attrs[‘optimal_trees’]<br>print (+f ts_clf_best<br>print a ees: {ts_clf_trees} | -ts_clf_study.best_value: .4f}")<br>ts_clf_final = xgb.XGBClassifier(<br>**ts_clf_best,<br>objective= 5<br>tree_method= F<br>scale_pos_weight=pos_ratio,<br>n_estimators-ts_clf_trees,<br>random_state=SEED,<br>n_jobs=-1,<br>ts_clf_final.fit(X_train_clean, rain_binary train<br><!-- End of picture text -->







###### Kaggle Score Graph 

Regression R2 





<!-- Start of picture text -->
Kaggle F1-Score Comparison: Public vs Private Leaderboard<br>mmm Public<br>0.8 Mm Private<br>0.7, 0.6935 0.7126 0.6996 0.6706<br>0.6151<br>0.6 0.5606 os615 __ 02782 05825 0.5819<br>» 0.5<br>°<br>is]<br>a<br>a 0.4<br>ue<br>0.3<br>0.2<br>0.1<br>0.0<br>. ee Kt yGB0°st nNNn oytade<br>Decision © aand© cn Fore<br>Model<br><!-- End of picture text -->







# TP 3: Clustering 





# Feature Engineering 



###### **Data Transform** 

###### **Log Transform** 



<!-- Start of picture text -->
# — Parse ‘time’ columd 2H<br>df[‘time'] = pd.to_datetime(df['time'], errors='coerce’)<br>df = df.dropna(subset=[‘time’ ])<br># — Extract raw temporal features ——HH——<br>df[ “hour” | = df[ time’ ] .dt hour<br>df[‘month'] = df[‘'time'].dt.month<br>. .<br>*<br>cyclical encoding ;<br>df[{*hour_sin']<br>df[*hour_cos'] = np.sin(2 * np.pi * df[‘hour'] / 24)<br>df[‘month_sin'] = np. cossin (2 * np.pi * df[‘ hm o ur']nth'] / 2412 )<br>df[‘month_cos*] = np.cos(2 * np.pi * df[‘month"] / 12)<br># Drop raw time.<br>;<br>df = df.drop(columns=[ ‘time’, ‘hour’, ‘month*])<br><!-- End of picture text -->

Log Transform pada fitur skewed untuk mengurangi dominasi outlier 



<!-- Start of picture text -->
# Logip Transform pada Fitur Skewed<br>skewed features = [<br>‘vapour_pressure deficit (kPa)",<br>‘soilmoisture@ to 7cm (m?/m?)',<br>“soilmoisture_7 to 28cm (m3/m?)",<br>‘soilmoisture_28<br>to 10@cm (m3/m?)"',<br>‘precipitation (mm)'<br>]<br>for feat in skewed features:<br>if feat in df.columns:<br>df[feat] = np.logip(df[feat].clip(lower=0))<br>df = df.rename(columns={feat: f'{feat} logip'})<br><!-- End of picture text -->





# Feature Engineering 



###### **Feature Selection** 

###### **Dimensionality Reduction** 

- Hapus fitur yang paling banyak berkorelasi tinggi e Hierarchical 

**HDBSCAN** : UMAP menjadi 10D **Hierarchical** : PCA menjadi 2D **Bisecting K-Means** : PCA menjadi 2D 

- K-Means 



<!-- Start of picture text -->
if HDBSCAN_REDUCTION_METHOD == ‘UMAP':<br># — UMAR,<br>print(f"Running UMAP: {X_scaled.shape[1]}D > {N_COMPONENTS_FULL}D")<br>reducer_full = umap.UMAP(<br>n_components=N_COMPONENTS_FULL,<br>n_neighbors=30,<br>min_dist=0.0,<br>metric='euclidean',<br>random_state=RANDOM_STATE,<br>n_jobs=-1,<br>) verbose=False<br>X_reduced = reducer_full.fit_transform(X_scaled)<br>else:<br>: ae ing PCA: {X_scaled.shape[1]}D » {N_COMPONENTS FULL}D")<br>prinreducer_fullunning= PCA(n_components=N_COMPONENTS_FULL,: {X_scaled.shape > {Ni random_state=RANDOM_STATE)_<br>X_reduced = reducer_full.fit_transform(X_scaled)<br>explained = reducer_full.explained_variance_ratio_.cumsum()<br>print(f" Explained variance (cumulative): {explained[-1]*100:.1f}%")<br><!-- End of picture text -->

###### **Feature Scaling** 

Robust Scaler : HDBSCAN, Hierarchical Standard Scaler : K-Means, Bisecting K-Means 



<!-- Start of picture text -->
# — Standacdsealers -—MHH WH<br>feature_names = df .columns .tolist()<br># scaler = StandardScaler()<br>scaler = Robustscaler()<br>x_scaled = scaler. fit_transform(df{feature_names: ] )<br><!-- End of picture text -->





# Hyperparameter Tuning 



###### **Grid Search** 



<!-- Start of picture text -->
param grid = {<br>"‘min_cluster_size': [25, 50, 75, 100, 125, 150, 175, 20@],<br>"min_samples' : [5, 10, 26, 3@, 50, 100, 125, 150, 175, 20@],<br>}<br><!-- End of picture text -->



<!-- Start of picture text -->
param grid = {<br>“n_clusters': all_n_clusters,<br>‘linkage’: ['ward', ‘complete’, ‘single’, ‘average’|<br>}<br><!-- End of picture text -->

`⟵` Hierarchical 

`⟵` HDBSCAN 

###### **Optuna** 

`⟵` Bisecting K-Means 









<!-- Start of picture text -->
Cluster Size Distribution 357<br>(4a 2%)<br>350<br>300<br>2 250<br>= 203<br>aa (27.4%) 181<br>‘5 200 (24.4%)<br>—<br>a 150<br>£3<br>=<br>100<br>50<br>0<br>Cluster -1 Cluster 0 Cluster 1<br>HoascadExtreme.tNQIS@) | nincamples=200<br><!-- End of picture text -->

###### **Terbentuk 3 Kluster** 

## HDBSCAN 

Penentuan Cluster 1 sebagai cuaca ekstrem berdasarkan feature profile 



<!-- Start of picture text -->
*<br><!-- End of picture text -->



##### Cluster Profilling 



<!-- Start of picture text -->
Feature Profile by Cluster<br>(Normalized 0-1 for comparability)<br>1.0 mmm Cluster -1 — Extreme<br>Mmm Cluster 0 — Normal<br>a Cluster 1 — Normal<br>° 0.8<br>37]<br>>cS<br>0.6<br>=<br>Le]<br>=ov<br>no]<br>g 0.4<br>r]<br>E<br>[o}<br>so SS 0 ef e xo<br>Each featyseMormalizedae independently; not suitass®os?for cross-feature comparison. 40”roa oeae ye*ae aeae<br>e™ ev? we or? ai<br>& oe<br><!-- End of picture text -->



Cluster profiling memberikan indikasi bahwa: 



<!-- Start of picture text -->
*<br><!-- End of picture text -->

**Cluster -1 (Ekstrem / Badai)** : Didominasi oleh tingkat tutupan awan yang maksimal (mendekati 1.0) dengan suhu, radiasi matahari, dan kecepatan angin yang menurun drastis. 

- **Cluster 0 (Normal - Tropis Cerah)** : Memiliki suhu, hembusan angin (wind gusts), dan radiasi matahari tertinggi dengan tutupan awan yang sangat minim. 

**Cluster 1 (Normal - Transisi Lembap)** : Dicirikan oleh kelembapan relatif tertinggi dengan parameter lainnya berada di level moderat, merepresentasikan cuaca mendung ringan. 



#### Aglomerative Hierarchical 

###### **Terbentuk 4 Kluster** 

Berdasarkan profilling, kluster 1 (hijau) paling cocok untuk cuaca ekstrem 



<!-- Start of picture text -->
Dendrogram — Average Linkage (Final Cut: k=4 clusters)<br>Colored branches show the final 4 clusters selected by the model<br>--- Cut at k=4 clusters<br>80<br>ov<br>UV<br>Cc<br>oC<br>a 60<br>fa}<br>ov<br>to)]<br>o<br>oad ido ada IaLabi<br><32D 40 LoLIU Loo LPI LIdod<br>fo)]<br>i<br>$<br>< 20<br>0<br>ae & © FR F HR HF FEF FC F F F F F RHR RF F FB HR HR HF FCF HF F FS HR F F GF F<br>~- = se =~ SNS SBS SB NH NS B HN NHN BSB SB HB B SF FS 4B B Hf HB ~ B BB 8H HB BB BS<br>Sampled 741 points | Method: Average | Metric: Euclidean | linkage=average | n_clusters=4 Data Points / Merged Clusters<br><!-- End of picture text -->



##### Cluster Profilling 



<!-- Start of picture text -->
r<br>r<br><!-- End of picture text -->



<!-- Start of picture text -->
Radar Chart: Agglomerative Cluster Profiles (Normalized, Expanded Features)<br>Wind Speed 10M<br>ee oo<br>Wind Gusts 70M — 7 - Dew Point 2M<br>/<br>/ \<br>Cloud Co f 0 8 ompdrQrure 2m<br>\ |<br>\<br>_—~——<br>— Cluster Cluster0<br>—— Cluster ClusterTerrestrial1  Radiatio oisture 0 To 7Cm<br>——~~ ClusterCluster Cluster Cluster 23° SLSunshine Duration<br><!-- End of picture text -->

###### cluster_label_map = 

- 2: 'Cerah / Terik',          # radiation maks, sunshine tertinggi 

- 0: 'Berangin / Tidak Stabil', # wind tertinggi, outlier score tertinggi 

- 3: 'Setelah Hujan',           # radiation & sunshine rendah, soil basah 

- 1: 'Ekstrem',        # sunshine ~0, cloud cover & wind speed tinggi 





<!-- Start of picture text -->
Distribusi Hasil K-Means Clustering (K=4)<br>Jumlah Observasi per Cluster 38.9%5,456 Proporsi Cluster<br>5000 || Cluster 0<br>4000 - { 3,690 |<br>a (26.3%) Cluster 3<br>c<br>a<br>fs) 3000 2,344 abs) Cluster 1<br>s (16.7%)<br>§ 2000 |<br>1000 ae ae a —<br>Cluster 2<br>0<br>0 1 2 3<br>Cluster<br><!-- End of picture text -->



<!-- Start of picture text -->
*<br>Se<br><!-- End of picture text -->

## K-Means 



###### **Terbentuk 4 Kluster** 

**Cluster Cerah & Kering :** Cuaca stabil dengan suhu tinggi, minim hujan, dan kelembaban rendah. Mewakili musim kemarau. Tingkat bahaya: Rendah. 

**Cluster Berawan Normal :** Cuaca moderat dengan awan ringan–sedang, angin tenang, dan tanpa hujan signifikan. Umum terjadi saat musim transisi. Tingkat bahaya: Rendah. 

**Cluster Hujan Sedang :** Curah hujan dan kelembaban tinggi dengan awan tebal, namun angin masih normal. Berpotensi banjir lokal jika berkepanjangan. Tingkat bahaya: Sedang. 

**Cluster Cuaca Ekstrem / Badai :** Hujan deras, angin kencang, tekanan rendah, dan awan sangat tebal. Jarang terjadi tetapi berdampak besar. Tingkat bahaya: Tinggi. 



#### Bisecting K-Means 

###### **Terbentuk 2 Kluster** 

Berdasarkan tuning, skor terbaik adalah 2 kluster 





<!-- Start of picture text -->
*<br>ste<br><!-- End of picture text -->



<!-- Start of picture text -->
Distribusi Hasil Bisecting K-Means Clustering (K=2)<br>Jumlah Observasi per Cluster 9393 Proporsi Cluster<br>(66.4%)<br>8000 t<br>Cluster 0<br>B<br>S 6000<br>$ 4,713<br>é (33.6%)<br>8 4000<br>E<br>3<br>Cluster 1<br>2000<br>0 0<br>Cluster<br><!-- End of picture text -->





##### Cluster Profilling 



<!-- Start of picture text -->
# Pilih fitur-fitur kunci yang relevan untuk cuaca ekstrem<br>key_features = processed _df.columns<br><!-- End of picture text -->



<!-- Start of picture text -->
# Hitung “extreme score" per cluster: berapa banyak threshold yang dilampaui<br>cluster_means = df_labeled.groupby( ‘cluster’ )[key features] .mean()<br>extreme_score = {}<br>for cluster_id in cluster_means.index:<br>score = 0<br>for feat_keyword, threshold in thresholds.items(): _<br>col = [c for c in key_features if feat_keyword in c] 8<br>if col and cluster_means.loc[cluster_id, col[@]] >= threshold: z<br>score += 1 3<br>extreme_score[cluster_id] = score =<br>print(pd.Series(extreme_score, name='extreme_score’ ))<br># Cluster dengan skor tertinggi + labeli sebagai “ekstrem"<br><!-- End of picture text -->



<!-- Start of picture text -->
Distribusi Hasil Bisecting K-Means Clustering (K=2)<br>Jumlah Observasi per Cluster 2, Proporsi Cluster<br>8000<br>_ Cluster0<br>8 6000<br>z (33.6%)<br>3 4000<br>= Clucterd<br>2000<br>0<br>, '<br>Cluster<br><!-- End of picture text -->





##### Cluster Profilling 



<!-- Start of picture text -->
Bisecting K-Means — Distribusi Fitur: Normal vs Ekstrem<br>Temperature 2M Relative Humidity 2M Wind Gusts 10M Cloud Cover Precipitation Shortwave Radiation<br>“ 50<br>100 1000<br>100 2<br>30<br>90 40<br>28 80 20 800<br>26 80 30 60 15 600<br>24<br>70 20 40 10 400<br>22<br>20 60 10 20 5 200<br>18 50 °<br>0 0 0<br>Normal Ekstrem Normal Ekstrem Normal Ekstrem Normal Ekstrem Normal Ekstrem Normal Ekstrem<br><!-- End of picture text -->

###### **Bisecting K-Means memisahkan dua profil cuaca yang berbeda secara signifikan.** 



Cluster Ekstrem: curah hujan tinggi, angin kencang, dan suhu lebih panas dengan distribusi yang lebih lebar dan bervariasi. 

Cluster Normal: suhu sejuk stabil, kelembapan tinggi konsisten, dan hampir tanpa hujan. 



##### Summary 

###### **EDA of the day** 



|**TP**|**Best Model**|**Metrics**|**Score**|
|---|---|---|---|
|Classification|LightGBM|F1|0.050|
|Regression|XGBoost|R²|0.712|
|Clustering|HDBSCAN|Silhouette|0.687|



Dataset cuaca dengan target electricity_shutdown terbukti merupakan masalah yang highly non-linear dan imbalanced. Pendekatan yang paling efektif adalah model berbasis tree (LightGBM/Random Forest) yang dikombinasikan dengan feature engineering temporal dan handling imbalance yang disesuaikan per model. 

###### **EDA #4 | Pola temporal shutdown listrik dengan peak spesifik** 

Peak shutdown teridentifikasi secara spesifik dari data → justified pembuatan binary risk flag is_peak_hour (hour==20) dan is_peak_month (month==3) sebagai EDA-driven feature engineering 

**EDA #6 | Lag efektif 1–3 jam dengan cloud_cover, soil_moisture, dew_point sebagai prediktor utama** Efek temporal lag 1–3 jam pada precipitation → justified pembuatan lag features (cloud_cover lag 1h/2h/3h, dll.) di TP1 dan TP2. 

###### **EDA #2: Zero-inflation pada precipitation** 

Zero-inflation berarti distribusi precipitation tidak bisa dimodelkan dengan satu model regresi tunggal → justified penggunaan 2-stage model di TP2 yang memisahkan 'hujan vs tidak hujan' sebelum memprediksi intensitasnya 







<!-- Start of picture text -->
TP 1<br><!-- End of picture text -->



<!-- Start of picture text -->
TP 2<br><!-- End of picture text -->



<!-- Start of picture text -->
TP 3<br><!-- End of picture text -->

### Notebook 

<u>https://colab.research.google.com/drive/1f6rIsnD 9vKtakRl5aFj6WP8CvjW0vva8?usp=sharing</u> 

<u>https://colab.research.google.com/drive/1GZO6 W5apg7hOxfi1mDps820ZpALgdtB7?usp=sharing</u> 

<u>https://colab.research.google.com/drive/1kfb9U OJdbJ0RPmwKfVmTZMe2Rlsw5lsc?usp=sharing</u> 

### Video 



<!-- Start of picture text -->
Link Youtube<br><!-- End of picture text -->

https://youtu.be/105h9 YqjIdE 









## Thank you so much 

Any Question? 

Presented By: **Kasdiddy** 





