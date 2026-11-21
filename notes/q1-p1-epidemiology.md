---
title: Q1 - Praktikumsaufgaben P1 - Epidemiologische Maßzahlen
author: Hüseyin Uysal
date: today
format: pdf
---

# Epidemiologische Maßzahlen

Anhand von Daten aus der Whitehall-II-Studie (über britische Beamte) wurde untersucht, ob das Auftreten einer kardiovaskulären Erkrankung (cardiovascular disease, CVD) im Zusammenhang mit dem Auftreten einer Demenzerkrankung steht. Die Studienpopulation umfasste 10.216 Personen, von denen 3.275 eine CVD hatten. Von diesen erkrankten 358 an Demenz. Unter denjenigen, die keine CVD hatten, erkrankten 292 an Demenz

```r
#| label: 3fdba35f
# load in the dataset
whitehall <- read.csv2("C:\\Users\\crypr\\vaults\\Hüseyins digitales Gehirn\\ressources\\!Datasets\\whitehall.csv", sep = ",", header = TRUE)
whitehall <- data.frame(whitehall)
head(whitehall)
```

<details class="callout callout-output" markdown="1" open>
<summary>{#output-3fdba35f}</summary>

Warning: unvollständige letzte Zeile von readTableHeader in 'C:\\Users\\crypr\\vaults\\Hüseyins digitales Gehirn\\ressources\\\!Datasets\\whitehall.csv' gefunden
  cvd\_status dementia\_status count
1          1               1   358
2          1               0  2917
3          0               1   292
4          0               0  6649


</details>

## Aufgabe 1: Vierfeldertafel

Bitte übertragen Sie die oben genannten Maßzahlen in die Vierfelder-Tafel und ergänzen Sie die fehlenden Werte.

```r
#| label: eb1e33e8
whitehall_xtab <- xtabs(count ~ cvd_status + dementia_status, data = whitehall)
print(whitehall_xtab)
```

<details class="callout callout-output" markdown="1" open>
<summary>{#output-eb1e33e8}</summary>

dementia\_status
cvd\_status    0    1
         0 6649  292
         1 2917  358


</details>

## 2. Häufigkeitsmaße

### 2.a) Risiko für Demenz, wenn CVD

Wie hoch ist das Risiko für jemanden, der eine kardiovaskuläre Erkrankung hat bzw. hatte, an Demenz zu erkranken?

```r
#| label: 031b4af5
# calculate & create variable for all ppl with cvd
count_cvd <- sum(whitehall$count[whitehall$cvd_status == 1])

# calculate & create variable for all ppl with cvd AND dementia
count_cvd_dementia <- sum(whitehall$count[whitehall$cvd_status == 1 & whitehall$dementia_status == 1])

# calculate & print the risk
risk_cvd_dementia <- count_cvd_dementia/count_cvd
print(risk_cvd_dementia)
```

<details class="callout callout-output" markdown="1" open>
<summary>{#output-031b4af5}</summary>

\[1\] 0.109313


</details>

### 2.b) Odds für Demenz bei nicht-CVD-Population

Wie hoch ist die Odds für jemanden, der keine kardiovaskuläre Erkrankung hat bzw. hatte, an Demenz zu erkranken?

```r
#| label: 87226162
# calculate & create variable for all ppl without cvd & without dementia
count_cvd0_dementia0 <- sum(whitehall$count[whitehall$cvd_status == 0 & whitehall$dementia_status == 0])

# calculate & create variable for all ppl without cvd but WITH dementia
count_cvd0_dementia1 <- sum(whitehall$count[whitehall$cvd_status == 0 & whitehall$dementia_status == 1])

# calculate & print the odds
odds_cvd0_dementia <- count_cvd0_dementia1/count_cvd0_dementia0
print(odds_cvd0_dementia)
```

<details class="callout callout-output" markdown="1" open>
<summary>{#output-87226162}</summary>

\[1\] 0.04391638


</details>

### 2.c) kumulative Inzidenz

Wie hoch ist die (kumulative) Inzidenz für Demenz?

```r
#| label: 6e400187
count_dementia1 <- sum(whitehall$count[whitehall$dementia_status == 1])
count_all <- sum(whitehall$count)
incidence_dementia <- count_dementia1/count_all
print(incidence_dementia)
```

<details class="callout callout-output" markdown="1" open>
<summary>{#output-6e400187}</summary>

\[1\] 0.06362569


</details>

### 2.d) Inzidenzrate?

<u>Frage</u>: Können Sie mit den o. g. Angaben eine Inzidenzrate berechnen? Bitte erläutern Sie Ihre Antwort.

<u>Antwort</u>: nope, weil überhaupt keine Angaben bzgl. der Zeit in der die Personen beobachtet wurden

## 3. Effektgröße

### 3.e) RR & OR berechnen

Berechnen Sie das Relative Risiko und das Odds Ratio, an Demenz zu erkranken (CVD versus keine CVD).

#### RR berechnen

```r
#| label: 28dae7c8
# risk ratio 

## risk_cvd_dementia already calculated, so now: risk for dementia for ppl without cvd 

### for this, count all the ppl without cvd 
count_nocvd <- sum(whitehall$count[whitehall$cvd_status == 0])

### now count all the ppl without cvd but WITH dementia 
count_nocvd_yesdementia <- sum(whitehall$count[whitehall$cvd_status == 0 & whitehall$dementia_status == 1])

## calculate risk
risk_nocvd_dementia <- count_nocvd_yesdementia/count_nocvd 

## calculate & print risk ratio 
rr_dementia_cvdyesvsno <- risk_cvd_dementia/risk_nocvd_dementia 
print(rr_dementia_cvdyesvsno)
```

<details class="callout callout-output" markdown="1" open>
<summary>{#output-28dae7c8}</summary>

\[1\] 2.598429


</details>

#### OR berechnen

```r
#| label: d6f0c71e
# odds ratio 

## odds for ppl without cvd already calculated (odds_cvd0_dementia), now same for with cvd 

### count every one with cvd & WITHOUT dementia
count_cvd1_dementia0 <- sum(whitehall$count[whitehall$cvd_status == 1 & whitehall$dementia_status == 0])

### count every one with cvd & WITH dementia 
count_cvd1_dementia1 <- sum(whitehall$count[whitehall$cvd_status == 1 & whitehall$dementia_status == 1])

## calculate odds 
odds_cvd1_dementia <- count_cvd1_dementia1/count_cvd1_dementia0 

## calculate & print OR  
or_cvd_dementia <- odds_cvd1_dementia/odds_cvd0_dementia 
print(or_cvd_dementia)
```

<details class="callout callout-output" markdown="1" open>
<summary>{#output-d6f0c71e}</summary>

\[1\] 2.794603


</details>

### 3.f) Interpretation RR & OR

Was sagen die berechneten Effektgrößen konkret aus?

*skipped*

### 3.g) Risikodifferenz

Berechnen Sie die Risikodifferenz (an Demenz zu erkranken) und erläutern Sie diese.

```r
#| label: 8cd25102
rd <- risk_cvd_dementia-risk_nocvd_dementia 
print(rd)
```

<details class="callout callout-output" markdown="1" open>
<summary>{#output-8cd25102}</summary>

\[1\] 0.06724411


</details>

<hr style="border: none; height: 1px; border-bottom: 1px solid; border-image-slice: 1; border-width: 3px; border-image-source: linear-gradient(to right, transparent, lightsalmon, transparent); margin-top: 20px; margin-bottom: 20px; ">

parent: [LogR](logr.html)
tags: 