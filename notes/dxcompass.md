---
title: "DxCompass"
banner: "![[../../ressources/!Media/default.webp]]"
banner_icon: 🧭
tags: database/dxcompass biosync/Lernpläne/Curriculum_anthropologicum/SKILLS/DDx  
---

# DxCompass ![55](../assets/pasted-image-20241009210408.png)

## Was ist das

Eine Datenbank an Leitsymptomen und klinischen Syndromen samt diagnostischer Algorithmen.

>[!opinion]- Why tho?
>- Im Rahmen meiner letzten Famulatur ist mir aufgefallen, dass wir im Uni-Alltag Krankheiten falschrum lernen.
>- Logistischerweise lernt man Stereotyp für jede Krankheit, Ideologie, Klinik, Pathologie, Diagnose und Therapie.
>- In der Realität stellen sich Patienten allerdings nicht vor mit einer bekannten Krankheit, sondern mit Symptomen. Und dann muss man diese Symptome interpretieren und wissen, welche diagnostischen und therapeutischen Schritte man einleiten muss.

>[!connection] fürs Lernen
>- Casus zur Überprüfung des hier Gelernten nutzen
>- Slide-Mode nutzen (sowohl Casus als auch Dx)

## MOC

```button
name Leitsymptom hinzufügen
type note(databases/DxCompass/leitsymptom_template, split) template
action leitsymptom_template
```
```dataview
TABLE from #database/dxcompass  
SORT file.name
```

## Tools

### Heuristiken

- "Häufiges ist häufig, Seltenes ist selten."

<hr style="border: none; height: 1px; border-bottom: 1px solid; border-image-slice: 1; border-width: 3px; border-image-source: linear-gradient(to right, transparent, lightsalmon, transparent); margin-top: 20px; margin-bottom: 20px; ">

tags: #database 