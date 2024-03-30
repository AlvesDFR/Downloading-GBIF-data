# Downloading species occurrence data from GBIF into R

This is a short tutorial on how we can download data from GBIF.  
Here, I use the RGBIF package from r to obtain longitude and latitude data, as well as other information that may be relevant.

## Índice
- [First steps](#first-steps)
- [Searching for taxonkeys](#searching-for-taxonkeys)
- [Downloading data](#downloading-data)
- [Selecting and saving data](#selecting-and-saving-data)
- [Contato](#contato)

## First steps
- 1) It is necessary to register at https://www.gbif.org/.

- 2) Write down your login details:  
      GBIF_USER="XXXXXXX"  
      GBIF_PWD="12345678"  
      GBIF_EMAIL="XXXXXXXXX@XXXXXX.com.br"

- 3) Install the rgbif package.

```
install.packages("rgbif")
```

- 4) Set up your GBIF credentials in r environment:
 ```
usethis::edit_r_environ()
```
Paste your data (GBIF_USER, GBIF_PWD and GBIF_EMAIL) into .Renviron

     
## Searching for taxonkeys
Searching for the taxonkey for the species
```python
taxon_key <- occ_search(scientificName = sp)$data
unique(taxon_key$taxonKey)
```

## Downloading data
Download data for each unique taxonkey
```
gbif_download <- occ_download(pred("taxonKey", TAXON_KEY_HERE),format = "SIMPLE_CSV")
occ_download_wait(gbif_download)
df <- occ_download_get(gbif_download) %>% occ_download_import()
```

## Selecting and saving data


<img src="dados_gbif.jpg" width="1500">  

```
occ_gbif<-data.frame(df$species, df$decimalLongitude, df$decimalLatitude, df$gbifID, df$datasetKey, df$year, df$coordinatePrecision)  
colnames(occ_gbif)<-c('sp','longitude','latitude','gbifID','datasetID','year','precision')  
occ_gbif<-occ_gbif[complete.cases(occ_gbif[,2:3]),] 
```


## Contato
<img src="curriculum4.jpg" width="150">

Para mais informações, entre em contato comigo em meu endereço de e-mail: douglas_biologo@yahoo.com.br
