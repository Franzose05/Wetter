##Packages##

# install.packages("httr")
# install.packages("jsonlite")
library(httr)
library(jsonlite)


## Stadt und API-Key
city <- "Stuttgart"
api_key <- "37902b8224263aa490b5dee0c2574ea1"

# URL bauen
url <- paste0(
  "https://api.openweathermap.org/data/2.5/weather?q=",
  URLencode(city),
  "&appid=", api_key,
  "&units=metric&lang=de"
)

# Anfrage senden
res <- GET(url)
json_text <- content(res, as = "text", encoding = "UTF-8")
data <- fromJSON(json_text)

# Wetterdaten extrahieren
wetterlage <- data$weather$description[1]
temperatur <- round(data$main$temp, 1)

# HTML-Template lesen
template <- readLines("wetter_template.html.txt", encoding = "UTF-8")

# Platzhalter ersetzen
output <- gsub("\\[STADT\\]", city, template)
output <- gsub("\\[WETTER\\]", wetterlage, output)
output <- gsub("\\[TEMP\\]", temperatur, output)

# Fertige Datei schreiben
writeLines(output, "index.html", useBytes = TRUE)