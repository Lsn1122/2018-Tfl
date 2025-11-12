# 2018-Tfl
Math6183-Coursework3

# example for how to combine the data- using same way to deal with all the other sheets

```{r}
library(readxl)
library(dplyr)

station_alighters <- read_excel("D:/UOS-study&Career/UOS-Math6183/NBT18FRI_Outputs.xlsx", sheet = "Station_Alighters", skip = 2)
link_reduced <- station_alighters %>%
  select(1:which(names(station_alighters) == "Late"))
station_alighters <- read_excel("D:/UOS-study&Career/UOS-Math6183/NBT18MTT_Outputs.xlsx", sheet = "Station_Alighters", skip = 2)
link_reduced <- station_alighters %>%
  select(1:which(names(station_alighters) == "Late"))
station_alighters <- read_excel("D:/UOS-study&Career/UOS-Math6183/NBT18SAT_Outputs.xlsx", sheet = "Station_Alighters", skip = 2)
ink_reduced <- station_alighters %>%
  select(1:which(names(station_alighters) == "Late"))
station_alighters <- read_excel("D:/UOS-study&Career/UOS-Math6183/NBT18SUN_Outputs.xlsx", sheet = "Station_Alighters", skip = 2)
link_reduced <- station_alighters %>%
  select(1:which(names(station_alighters) == "Late"))

files <- c(
  "D:/UOS-study&Career/UOS-Math6183/NBT18FRI_Outputs.xlsx",
  "D:/UOS-study&Career/UOS-Math6183/NBT18MTT_Outputs.xlsx",
  "D:/UOS-study&Career/UOS-Math6183/NBT18SAT_Outputs.xlsx",
  "D:/UOS-study&Career/UOS-Math6183/NBT18SUN_Outputs.xlsx"
)

day_types <- c("Friday", "Weekday", "Saturday", "Sunday")
read_station_alighters <- function(file, daytype) {
  df <- read_excel(file, sheet = "Station_Alighters", skip = 2)
  df <- df %>% 
    select(1:which(names(df) == "Late")) %>%  
    mutate(DayType = daytype)               
  return(df)
}

link_all <- bind_rows(
  read_station_alighters(files[1], day_types[1]),
  read_station_alighters(files[2], day_types[2]),
  read_station_alighters(files[3], day_types[3]),
  read_station_alighters(files[4], day_types[4])
)

glimpse(link_all)

write.csv(link_all, "D:/UOS-study&Career/UOS-Math6183/Station_Alighters_All_Summary.csv", row.names = FALSE)
```
# 得到整合完成的8个表格

