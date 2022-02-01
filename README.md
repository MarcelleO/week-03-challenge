# week-03-challenge

library(skimr)
library(kableExtra)


f <- "https://raw.githubusercontent.com/difiore/ada-2022-datasets/main/KamilarAndCooperData.csv"
d <- read_csv(f, col_names=TRUE)

boxplot(log(d$Body_mass_female_mean)~d$Family)

p <- ggplot(data=d, aes(x=Family, y=log(Body_mass_female_mean)))
p <- p + geom_boxplot(na.rm=TRUE)
p <- p + theme(axis.text.x=element_text(angle=90))
p <- p + ylab("log(Female Body Mass)")
p


par(mfrow=c(1,2))
plot(x = d$Body_mass_female_mean, y = d$Brain_Size_Female_Mean)
plot(x = log(d$Body_mass_female_mean), y = log(d$Brain_Size_Female_Mean))

p <- ggplot(data=d, aes(x=log(Body_mass_female_mean),
  y=log(MaxLongevity_m)))
p <- p + geom_point(na.rm = TRUE)
p <- p + geom_smooth(method="lm", na.rm = TRUE)
p

s <-
  select(d,
    c(
      "Brain_Size_Female_Mean",
      "Body_mass_female_mean",
      "MeanGroupSize",
      "WeaningAge_d",
      "MaxLongevity_m",
      "HomeRange_km2",
      "DayLength_km"
    ))
pairs(s[,1:ncol(s)])
