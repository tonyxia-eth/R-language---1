# R-language---1


penguins %>%
  select(species, body_mass_g, sex) %>%
  group_by(species) %>%
  mutate(std_body_mass = (body_mass_g - mean(body_mass_g, na.rm = TRUE)) /
           sd(body_mass_g, na.rm = TRUE))


#------------------------------------



penguins %>%
  select(species, body_mass_g, sex) %>%
  group_by(species) %>%
  mutate(std_body_mass = (body_mass_g - mean(body_mass_g, na.rm = TRUE)) /
           sd(body_mass_g, na.rm = TRUE)) %>%
  ungroup() %>%
  ggplot(aes(x = std_body_mass)) +
  geom_histogram(aes(y = ..density..), bins = 30, fill = "skyblue", color = "black") +
  stat_function(fun = dnorm, args = list(mean = 0, sd = 1), color = "red", size = 1) +
  labs(title = "Bell Curve of Standardized Body Mass",
       x = "Standardized Body Mass (z-score)",
       y = "Density") +
  theme_minimal()
