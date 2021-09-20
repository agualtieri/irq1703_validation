rm(list=ls())

library(openxlsx)
library(tidyverse)
library(cleaninginspectoR)

## load data
df <- read.xlsx("./input/IRQ_Dataset_Joint-Price-Monitoring-Initiative-JPMI_July-2021.xlsx", sheet = "Data")
log <- read.xlsx("./input/IRQ_Dataset_Joint-Price-Monitoring-Initiative-JPMI_July-2021.xlsx", sheet = "Cleaning Log")

df <- dplyr::rename(df, uuid = X_uuid)
df <- df %>% mutate(index = 1:nrow(.))

## inspector
issues <- inspect_all(df) %>% filter(!is.na(index))

print(df$sanitary_napkins_price)
min(df$sanitary_napkins_price, na.rm = TRUE)

source("./check_log.R")
log.c <- check_log(df, log, "Variable", "Value_raw", "Value_clean", "uuid", "X_uuid")

write.csv(log.c, paste0("./log check_",Sys.Date(),".csv"))

## sil analysis
tool <- read.xlsx("./input/IRQ_Dataset_Joint-Price-Monitoring-Initiative-JPMI_July-2021.xlsx", sheet = "Kobo Survey")
raw <- read.csv("./input/Raw Data Round 43_Anonymized.csv", stringsAsFactors = FALSE)

source("./data_falsification.R")
library(cluster)

false2 <- calculateDifferences(df, tool)



write.csv(false, "silhouette_analysis.csv")
write.csv(false2, "enumerator_differences.csv")
write.csv(check, "enumerator_check.csv")
