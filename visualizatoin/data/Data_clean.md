<div style="width: 100%; clear: both;">
<div style="float: left; width: 50%;">
<img src="http://www.uoc.edu/portal/_resources/common/imatges/marca_UOC/UOC_Masterbrand.jpg" align="left">
</div>
</div>
<div style="float: right; width: 50%;">
<p style="margin: 0; padding-top: 22px; text-align:right;">M2.959 · Visualització de dades</p>
<p style="margin: 0; text-align:right;">Màster universitari de Ciència de Dades (Data science)</p>
<p style="margin: 0; text-align:right; padding-button: 100px;">Estudis d'Informàtica, Multimèdia i Telecomunicació</p>
</div>
</div>
<div style="width: 100%; clear: both;">
<div style="width:100%;">&nbsp;</div>

# Neteja i preparació de dades per la visualització final
## Neteja de dades

Abans de preparar el nostre fitxer de sortida d'acord al format que s'espera per fer la visualització hem de fer la neteja de dades. Però abans de continuar carregarem les nostres dades:


```python
import pandas as pd
```


```python
df = pd.read_csv("pax_data_195_agreements_12-11-19_final.csv", header = 0)

df.head()
```




<div>

<table border="0" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Con</th>
      <th>Contp</th>
      <th>PP</th>
      <th>PPName</th>
      <th>Reg</th>
      <th>AgtId</th>
      <th>Agt</th>
      <th>Dat</th>
      <th>Status</th>
      <th>...</th>
      <th>TjRep</th>
      <th>TjRSym</th>
      <th>TjRMa</th>
      <th>TjNR</th>
      <th>ImUN</th>
      <th>ImOth</th>
      <th>ImRef</th>
      <th>ImPK</th>
      <th>ImE</th>
      <th>ImSrc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Colombia</td>
      <td>Government</td>
      <td>38.0</td>
      <td>Colombia VI - Government-ELN post-2015 process</td>
      <td>Americas</td>
      <td>2045</td>
      <td>Joint Announcement by the National Government ...</td>
      <td>2017-10-24</td>
      <td>Multiparty signed/agreed</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Colombia</td>
      <td>Government</td>
      <td>38.0</td>
      <td>Colombia VI - Government-ELN post-2015 process</td>
      <td>Americas</td>
      <td>2043</td>
      <td>Comunicado Conjunto 5: Entre El Gobierno Nacio...</td>
      <td>2017-09-24</td>
      <td>Multiparty signed/agreed</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Colombia</td>
      <td>Government</td>
      <td>38.0</td>
      <td>Colombia VI - Government-ELN post-2015 process</td>
      <td>Americas</td>
      <td>1890</td>
      <td>Communicado Conjunto 4: Acuerdo de Quito</td>
      <td>2017-09-04</td>
      <td>Multiparty signed/agreed</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Colombia</td>
      <td>Government</td>
      <td>38.0</td>
      <td>Colombia VI - Government-ELN post-2015 process</td>
      <td>Americas</td>
      <td>1937</td>
      <td>Comunicado Conjunto 3</td>
      <td>2017-06-06</td>
      <td>Multiparty signed/agreed</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Colombia</td>
      <td>Government</td>
      <td>38.0</td>
      <td>Colombia VI - Government-ELN post-2015 process</td>
      <td>Americas</td>
      <td>1936</td>
      <td>Comunicado Conjunto 2</td>
      <td>2017-04-06</td>
      <td>Multiparty signed/agreed</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 267 columns</p>
</div>



Degut a tenim moltes columnes presents al dataframe i no totes són necesaries per la nostra visualització seleccionarem només aquelles que farem servir:


```python

select_col = ["Con", "Contp", "Agt", "Dat", "Status", "GCh", "GChRhet", "GChAntid", "GChSubs", "GChOth", "GDis", "GDisRhet", "GDisAntid", "GDisSubs",
"GDisOth", "GAge", "GAgeRhet", "GAgeAntid", "GAgeSubs", "GAgeOth", "GMig", "GMigRhet", "GMigAntid", "GMigSubs", "GMigOth", "GRa", "GRaRhet", "GRaAntid", "GRaSubs", "GRaOth",
"GRe", "GReRhet", "GReAntid", "GReSubs", "GReOth", "GInd", "GIndRhet", "GIndAntid", "GIndSubs", "GIndOth", "GOth", "GOthRhet",  "GOthAntid", "GOthSubs", "GOthOth","GRef", "GRefRhet",
"GRefSubs", "GRefOth", "GSoc", "GSocRhet", "GSocAntid", "GSocSubs", "GSocOth", "GeWom", "GeMe", "GeSo", "GeLgbti", "GeLgbtiPos", "GeLgbtiNeg", "Pol", "PolGen", "PolNewInd", "PolNewTemp",
"Cons", "PolPar", "PolParTrans", "PolParOth", "EqGen", "Prot", "ProtCiv", "ProtGrp", "ProtLgl", "ProtOth", "HrFra", "HrfSp", "HrfBor", "HrfTinc", "HrfOth", "HrCp", "JusCr",
"JusCrSp", "JusCrSys", "JusCrPow", "StDef"]

df_f1 = df[select_col]

df_f1.head()
```




<div>

<table border="0" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Con</th>
      <th>Contp</th>
      <th>Agt</th>
      <th>Dat</th>
      <th>Status</th>
      <th>GCh</th>
      <th>GChRhet</th>
      <th>GChAntid</th>
      <th>GChSubs</th>
      <th>GChOth</th>
      <th>...</th>
      <th>HrfSp</th>
      <th>HrfBor</th>
      <th>HrfTinc</th>
      <th>HrfOth</th>
      <th>HrCp</th>
      <th>JusCr</th>
      <th>JusCrSp</th>
      <th>JusCrSys</th>
      <th>JusCrPow</th>
      <th>StDef</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Joint Announcement by the National Government ...</td>
      <td>2017-10-24</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Comunicado Conjunto 5: Entre El Gobierno Nacio...</td>
      <td>2017-09-24</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Communicado Conjunto 4: Acuerdo de Quito</td>
      <td>2017-09-04</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Comunicado Conjunto 3</td>
      <td>2017-06-06</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Comunicado Conjunto 2</td>
      <td>2017-04-06</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 85 columns</p>
</div>




```python
df_f1.columns[df_f1.isnull().any()].tolist()
```




    []



Com podem veure un cop hem seleccionat aquelles columnes que volem fer servir per la nostra visualització, no ens queda cap columna que contingui valors nulls.

## Preparació de dades

Ara que ja sabem que no tenim valor buits, hem de seleccionar separar els països que estan separats per /, per fer-ho començarem amb una descripció del tipus de dates que tenim a cada columna.


```python
df_f1.dtypes
```




    Con            object
    Contp          object
    Agt            object
    Dat            object
    Status         object
    GCh             int64
    GChRhet         int64
    GChAntid        int64
    GChSubs         int64
    GChOth          int64
    GDis            int64
    GDisRhet        int64
    GDisAntid       int64
    GDisSubs        int64
    GDisOth         int64
    GAge            int64
    GAgeRhet        int64
    GAgeAntid       int64
    GAgeSubs        int64
    GAgeOth         int64
    GMig            int64
    GMigRhet        int64
    GMigAntid       int64
    GMigSubs        int64
    GMigOth         int64
    GRa             int64
    GRaRhet         int64
    GRaAntid        int64
    GRaSubs         int64
    GRaOth          int64
                    ...  
    GeMe            int64
    GeSo            int64
    GeLgbti         int64
    GeLgbtiPos      int64
    GeLgbtiNeg      int64
    Pol             int64
    PolGen          int64
    PolNewInd       int64
    PolNewTemp      int64
    Cons            int64
    PolPar          int64
    PolParTrans     int64
    PolParOth       int64
    EqGen           int64
    Prot            int64
    ProtCiv         int64
    ProtGrp         int64
    ProtLgl         int64
    ProtOth         int64
    HrFra           int64
    HrfSp           int64
    HrfBor          int64
    HrfTinc         int64
    HrfOth          int64
    HrCp            int64
    JusCr           int64
    JusCrSp         int64
    JusCrSys        int64
    JusCrPow        int64
    StDef           int64
    Length: 85, dtype: object



Separem el nom de les ciutats que es troben en una mateixa linia del dataset separades per /, en fer la separació tindrem dues ciutats diferents amb la mateixa informació però separades.


```python
# Add row for each country
for (_,r) in df_f1.iterrows():
    if "/" in r["Con"]:
        for country in r["Con"].split("/"):
            new_row = r.copy()
            new_row["Con"] = country
            df_f1.loc[len(df_f1)] = new_row

# Delete all countries that stay presents in the same row
b = 0
for (_,r) in df_f1.iterrows():
    if "/" in r["Con"]:
        df_f1.drop(b, inplace = True)    
    b = b + 1
df_f1.reset_index(drop=True, inplace=True)

# Check not present contries splited with /
for (_,r) in df_f1.iterrows():
    if "/" in r["Con"]:
        print(r["Con"])
```

    /Applications/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:7: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame

    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      import sys
    /Applications/anaconda3/lib/python3.7/site-packages/pandas/core/frame.py:3940: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame

    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      errors=errors)


Comprobem que només surti un pais en la columna Con del dataframe:


```python
df_f1.Con.unique()
```




    array(['Colombia', 'El Salvador', 'Guatemala', 'Haiti', 'Honduras',
           'Mexico', 'Nicaragua', 'Venezuela', 'Costa Rica', 'Ecuador',
           'Peru'], dtype=object)




```python
df_f1.Contp.unique()
```




    array(['Government', 'Inter-group', 'Government/territory', 'Territory'],
          dtype=object)



#### Creació del csv que és graficará


```python
df_f1.head()
```




<div>

<table border="0" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Con</th>
      <th>Contp</th>
      <th>Agt</th>
      <th>Dat</th>
      <th>Status</th>
      <th>GCh</th>
      <th>GChRhet</th>
      <th>GChAntid</th>
      <th>GChSubs</th>
      <th>GChOth</th>
      <th>...</th>
      <th>HrfSp</th>
      <th>HrfBor</th>
      <th>HrfTinc</th>
      <th>HrfOth</th>
      <th>HrCp</th>
      <th>JusCr</th>
      <th>JusCrSp</th>
      <th>JusCrSys</th>
      <th>JusCrPow</th>
      <th>StDef</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Joint Announcement by the National Government ...</td>
      <td>2017-10-24</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Comunicado Conjunto 5: Entre El Gobierno Nacio...</td>
      <td>2017-09-24</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Communicado Conjunto 4: Acuerdo de Quito</td>
      <td>2017-09-04</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Comunicado Conjunto 3</td>
      <td>2017-06-06</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Colombia</td>
      <td>Government</td>
      <td>Comunicado Conjunto 2</td>
      <td>2017-04-06</td>
      <td>Multiparty signed/agreed</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 85 columns</p>
</div>



Creamos una única columna que unifique todos los valores diferentes de justicia, simplemente saber si hace algun tipo de ferencia politica.


```python
just_list = []
for index, row in df_f1.iterrows():
    if row["JusCr"] != 0 or row["JusCrSp"] != 0 or row["JusCrSys"] != 0 or row["JusCrPow"] != 0:
        just_list.append(1)
    else:
        just_list.append(0)

df_f1["Jus"] = just_list
```

    /Applications/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:8: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy




```python
countryG = df_f1.groupby("Con")
listcheck = []
sequence = []
seq_len = []

for country in df_f1.Con.unique():
    s = ""
    contp = countryG.get_group(country).groupby("Contp")
    #s = s+country+"-"
    for tp in df_f1.Contp.unique():
        try:
            a = contp.get_group(tp).groupby("HrFra")
            #s = s+tp+"-"
            for fa in df_f1.HrFra.unique():
                try:
                    b = a.get_group(fa).groupby("Prot")
                    #s = s+"HrFra_"+str(fa)+"-"
                    for prot in df_f1.Prot.unique():
                        try:
                            c = b.get_group(prot).groupby("GCh")
                            #s = s+"Prot_"+str(prot)+"-"
                            for gch in df_f1.GCh.unique():
                                try:
                                    d = c.get_group(gch).groupby("GDis")
                                    #s = s+"GCh_"+str(gch)+"-"
                                    for gdis in df_f1.GDis.unique():
                                        try:
                                            e = d.get_group(gdis).groupby("GInd")
                                            #s = s+"GDis_"+str(gdis)+"-"
                                            for gin in df_f1.GInd.unique():
                                                try:
                                                    f = e.get_group(gin).groupby("GMig")
                                                    #s = s+"GInd_"+str(gin)+"-"
                                                    for gm in df_f1.GMig.unique():
                                                        try:
                                                            g = f.get_group(gm).groupby("GSoc")
                                                            #s = s+"GMig_"+str(gm)+"-"
                                                            for soc in df_f1.GSoc.unique():
                                                                try:
                                                                    h = g.get_group(soc).groupby("Jus")
                                                                    #s = s+"GSoc_"+str(soc)+"-"
                                                                    for jus in df_f1.JusCr.unique():
                                                                        try:
                                                                            i = h.get_group(jus)

                                                                            s = country+"-"+tp+"-"+"HrFra_"+str(fa)+"-"+"Prot_"+str(prot)+"-"+"GCh_"+str(gch)+"-"+"GDis_"+str(gdis)+"-"+"GInd_"+str(gin)+"-"+"GMig_"+str(gm)+"-"+"GSoc_"+str(soc)+"-"+"Jus_"+str(jus)+"-"
                                                                            listcheck.append(len(i))
                                                                            sequence.append(s)
                                                                            seq_len.append(len(i))
                                                                        except:
                                                                            continue
                                                                except:
                                                                    continue   
                                                        except:
                                                            continue
                                                except:
                                                    continue
                                        except:
                                            continue
                                except:
                                    continue
                        except:
                            continue
                except:
                    continue

        except:
            continue

print(sum(listcheck))

seq_final = []
for i in range(0, len(sequence)):
    a = sequence[i][:-1].replace("Government", "Gov")
    b = a.replace("territory", "Ter")
    c = b.replace("Territory", "Ter")
    d = c.replace("Inter-group", "Int/grp")
    seq_final.append(d)
    print(d , seq_len[i])


```

    214
    Colombia-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 80
    Colombia-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_3-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_1-GMig_0-GSoc_0-Jus_0 3
    Colombia-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_2-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_0-GCh_3-GDis_0-GInd_0-GMig_0-GSoc_1-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_0-GCh_3-GDis_0-GInd_1-GMig_0-GSoc_0-Jus_1 1
    Colombia-Gov-HrFra_0-Prot_0-GCh_2-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_0-GCh_1-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_0-GCh_1-GDis_1-GInd_3-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_3-GCh_0-GDis_0-GInd_3-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_3-GCh_3-GDis_2-GInd_3-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_1-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 8
    Colombia-Gov-HrFra_0-Prot_1-GCh_0-GDis_0-GInd_3-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_1-GCh_0-GDis_0-GInd_2-GMig_0-GSoc_0-Jus_0 2
    Colombia-Gov-HrFra_0-Prot_1-GCh_0-GDis_2-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_0-Prot_1-GCh_3-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_1 1
    Colombia-Gov-HrFra_0-Prot_2-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 2
    Colombia-Gov-HrFra_0-Prot_2-GCh_3-GDis_0-GInd_1-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_1-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 6
    Colombia-Gov-HrFra_1-Prot_1-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 2
    Colombia-Gov-HrFra_1-Prot_1-GCh_1-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_1-Prot_2-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_3-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_3-Prot_3-GCh_3-GDis_3-GInd_3-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_3-Prot_3-GCh_3-GDis_3-GInd_3-GMig_0-GSoc_2-Jus_1 2
    Colombia-Gov-HrFra_3-Prot_1-GCh_2-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_2-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_2-Prot_0-GCh_3-GDis_0-GInd_1-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov-HrFra_2-Prot_1-GCh_3-GDis_1-GInd_3-GMig_0-GSoc_0-Jus_1 1
    Colombia-Int/grp-HrFra_0-Prot_0-GCh_2-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Int/grp-HrFra_0-Prot_0-GCh_1-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Colombia-Gov/Ter-HrFra_0-Prot_0-GCh_1-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    El Salvador-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 8
    El Salvador-Gov-HrFra_0-Prot_0-GCh_0-GDis_2-GInd_0-GMig_0-GSoc_0-Jus_0 1
    El Salvador-Gov-HrFra_0-Prot_3-GCh_0-GDis_2-GInd_0-GMig_0-GSoc_0-Jus_0 1
    El Salvador-Gov-HrFra_0-Prot_1-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    El Salvador-Gov-HrFra_0-Prot_1-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_1 1
    El Salvador-Gov-HrFra_0-Prot_1-GCh_2-GDis_3-GInd_0-GMig_0-GSoc_0-Jus_0 1
    El Salvador-Gov-HrFra_2-Prot_1-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_1 1
    El Salvador-Gov-HrFra_2-Prot_1-GCh_2-GDis_2-GInd_0-GMig_0-GSoc_0-Jus_1 1
    Guatemala-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 6
    Guatemala-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_3-GMig_0-GSoc_0-Jus_1 1
    Guatemala-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_1-GMig_0-GSoc_0-Jus_0 1
    Guatemala-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_2-GMig_0-GSoc_0-Jus_0 1
    Guatemala-Gov-HrFra_1-Prot_0-GCh_0-GDis_0-GInd_1-GMig_0-GSoc_0-Jus_0 2
    Guatemala-Gov-HrFra_1-Prot_0-GCh_1-GDis_0-GInd_1-GMig_0-GSoc_0-Jus_0 1
    Guatemala-Gov-HrFra_3-Prot_0-GCh_0-GDis_0-GInd_1-GMig_0-GSoc_0-Jus_0 1
    Guatemala-Gov-HrFra_3-Prot_0-GCh_0-GDis_0-GInd_2-GMig_0-GSoc_0-Jus_1 1
    Guatemala-Gov-HrFra_3-Prot_0-GCh_2-GDis_0-GInd_3-GMig_0-GSoc_0-Jus_0 1
    Guatemala-Gov-HrFra_3-Prot_0-GCh_2-GDis_3-GInd_3-GMig_0-GSoc_0-Jus_0 1
    Guatemala-Gov-HrFra_3-Prot_0-GCh_2-GDis_2-GInd_3-GMig_2-GSoc_0-Jus_0 1
    Guatemala-Gov-HrFra_3-Prot_3-GCh_0-GDis_0-GInd_2-GMig_0-GSoc_0-Jus_1 1
    Guatemala-Gov-HrFra_3-Prot_3-GCh_2-GDis_0-GInd_3-GMig_2-GSoc_0-Jus_1 1
    Haiti-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 4
    Honduras-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 2
    Honduras-Gov-HrFra_1-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Mexico-Gov/Ter-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_3-GMig_0-GSoc_0-Jus_0 1
    Mexico-Gov/Ter-HrFra_3-Prot_0-GCh_0-GDis_0-GInd_3-GMig_0-GSoc_0-Jus_1 1
    Mexico-Gov/Ter-HrFra_3-Prot_0-GCh_2-GDis_0-GInd_3-GMig_2-GSoc_0-Jus_0 1
    Mexico-Gov/Ter-HrFra_3-Prot_3-GCh_2-GDis_0-GInd_3-GMig_2-GSoc_0-Jus_1 1
    Mexico-Gov/Ter-HrFra_3-Prot_1-GCh_0-GDis_0-GInd_3-GMig_0-GSoc_0-Jus_1 1
    Mexico-Gov/Ter-HrFra_2-Prot_0-GCh_0-GDis_0-GInd_3-GMig_1-GSoc_0-Jus_0 1
    Nicaragua-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 5
    Nicaragua-Gov-HrFra_0-Prot_0-GCh_2-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Nicaragua-Gov-HrFra_0-Prot_0-GCh_2-GDis_2-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Nicaragua-Gov-HrFra_1-Prot_1-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Venezuela-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Costa Rica-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Ecuador-Ter-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 11
    Ecuador-Ter-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_2-GMig_0-GSoc_0-Jus_0 1
    Ecuador-Ter-HrFra_0-Prot_1-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Ecuador-Ter-HrFra_0-Prot_1-GCh_0-GDis_0-GInd_2-GMig_0-GSoc_0-Jus_0 1
    Peru-Ter-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 11
    Peru-Ter-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_2-GMig_0-GSoc_0-Jus_0 1
    Peru-Ter-HrFra_0-Prot_1-GCh_0-GDis_0-GInd_0-GMig_0-GSoc_0-Jus_0 1
    Peru-Ter-HrFra_0-Prot_1-GCh_0-GDis_0-GInd_2-GMig_0-GSoc_0-Jus_0 1



```python
data = {
    "sequence": seq_final,
    "length": seq_len
}

df_final = pd.DataFrame(data, columns = ["sequence", "length"])

df_final.head()
```




<div>

<table border="0" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sequence</th>
      <th>length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Colombia-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_...</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Colombia-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Colombia-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_...</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Colombia-Gov-HrFra_0-Prot_0-GCh_0-GDis_0-GInd_...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Colombia-Gov-HrFra_0-Prot_0-GCh_3-GDis_0-GInd_...</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_final.to_csv("paceX.csv", header=False, index=False)
```


```python
countryG = df_f1.groupby("Con")

for country in df_f1.Con.unique():
    cg = countryG.get_group(country)
    print(country, len(cg))

```

    Colombia 129
    El Salvador 15
    Guatemala 19
    Haiti 4
    Honduras 3
    Mexico 6
    Nicaragua 8
    Venezuela 1
    Costa Rica 1
    Ecuador 14
    Peru 14


En cas de que dos ciutats tinguin el mateix nombre de repeticions, l'ordre per seleccionar el color, és l'ordre alfabetic.


```python
for i in df_f1:
    print(i)
```

    Con
    Contp
    Agt
    Dat
    Status
    GCh
    GChRhet
    GChAntid
    GChSubs
    GChOth
    GDis
    GDisRhet
    GDisAntid
    GDisSubs
    GDisOth
    GAge
    GAgeRhet
    GAgeAntid
    GAgeSubs
    GAgeOth
    GMig
    GMigRhet
    GMigAntid
    GMigSubs
    GMigOth
    GRa
    GRaRhet
    GRaAntid
    GRaSubs
    GRaOth
    GRe
    GReRhet
    GReAntid
    GReSubs
    GReOth
    GInd
    GIndRhet
    GIndAntid
    GIndSubs
    GIndOth
    GOth
    GOthRhet
    GOthAntid
    GOthSubs
    GOthOth
    GRef
    GRefRhet
    GRefSubs
    GRefOth
    GSoc
    GSocRhet
    GSocAntid
    GSocSubs
    GSocOth
    GeWom
    GeMe
    GeSo
    GeLgbti
    GeLgbtiPos
    GeLgbtiNeg
    Pol
    PolGen
    PolNewInd
    PolNewTemp
    Cons
    PolPar
    PolParTrans
    PolParOth
    EqGen
    Prot
    ProtCiv
    ProtGrp
    ProtLgl
    ProtOth
    HrFra
    HrfSp
    HrfBor
    HrfTinc
    HrfOth
    HrCp
    JusCr
    JusCrSp
    JusCrSys
    JusCrPow
    StDef
    Jus



```python
just_list = []
for index, row in df_f1.iterrows():
    if row["JusCr"] != 0 or row["JusCrSp"] != 0 or row["JusCrSys"] != 0 or row["JusCrPow"] != 0:
        just_list.append(1)
    else:
        just_list.append(0)

df_f1["Jus"] = just_list

```

    /Applications/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:8: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
