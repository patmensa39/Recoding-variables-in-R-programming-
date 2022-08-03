# Recoding-variables-in-R-programming-
#RECODING VARIABLES ###
### Loading the libraries ###
pacman::p_load(pacman, rio, tidyverse)

### loading and preparing the dataset (Google search data) 
data<- import("StateData.xlsx") %>% as_tibble() %>% select(state_code, 
        psychRegions, instagram:modernDance) %>% 
        mutate(psychRegions = as.factor(psychRegions))

view(data) # viewing the data 

### Creating a new variable called Friendly from psychRegions and making the Friendly and 
### conventional states 'yes' and relaxed and creative 'maybe' Temperamental and Uninhibited 'no'
### and all others 'under investigation'

newdata<- data %>% mutate(Friendly = recode(psychRegions,
                          "Friendly and Conventional" = "yes",
                          "Relaxed and Creative" = "no", 
                          .default = "under investigation")) %>%
           select(state_code, psychRegions, Friendly)
view(newdata)

### Selecting multiple values and recoding them using case_when 
data2<- data %>% mutate(Philant = case_when(instagram < 1 | facebook > 0 | retweet < 1 ~ "yes", 
                                            TRUE ~ "no")) %>% 
                select(state_code, instagram, facebook, retweet, Philant)
view(data2)

### Arranging the new created variable 'Philant' in descending order 
data3<- data %>% mutate(Philant = case_when(instagram < 1 | facebook > 0 | retweet < 1 ~ "yes", 
                                            TRUE ~ "no")) %>% 
  select(state_code, instagram, facebook, retweet, Philant) %>% arrange(desc(Philant)) %>%
  print(n = Inf) # n = Inf helps in printing all the values 

view(data3)



