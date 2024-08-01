---
title: "Preneks normalne forme u Wolfram Mathematica"
date: 2023-01-15T22:30:15+01:00
draft: false
tags: ['tehnologija','matematika']
---

Prilično sam se namučio da bih saznao kako doći do preneks normalnih formi u Mathematici, da bih, naravno, provjerio
rezultate svog rada. Ispostavi se da u Mathematici ipak postoji (iz nekog razloga) nedokumentovana funkcija koja datu
predikatsku normalnu formu pretvara u preneks normalnu formu. Srećom postoji StackExchange na kojem sam, kao i mnogo puta
ranije, našao odgovor.

Da bi ovo funkcionisalo, moramo odraditi dvije stvari:
1. Koristiti Logical`Expand[predikat] da dobijemo predikat u normalnoj formi
2. Koristiti Reduce`ToPrenexForm[predikat] na normalnoj formi da bismo dobili preneks formu

Primjera radi, ovaj kod će dati preneks formu navedene formule:

(∀x)(F(x) ∧ (∃y)(G(y) ∧ H(x,y))) ⇒ (∃y)(T(y) ∧ P(a,b))
 
{{< highlight mathematica "linenos=table" >}}
predicate = 
 Implies[ForAll[x, F[x] && Exists[y, G[y] && H[x, y]]], 
  Exists[y, T[y] && P[a, b]]]

normalForm = LogicalExpand[predicate]

prenexNormalForm = Reduce`ToPrenexForm[normalForm]
{{< / highlight >}}

U Mathematica 13, to izgleda ovako:
{{< figure src="/images/prenex-mathematica.png" alt="Above source code in Mathematica" >}}

Nažalost, izgled jeste pomalo nezgrapan, posebno zbog neintuitivnih imena varijabli, no izgleda kao da se to ne može popraviti.
Ipak, i dalje odlično dobro radi kada treba provjeriti umjereno složene formule, nakon mnogo ručnog rada, naravno.
