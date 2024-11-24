---
title: 'ml-healthcare'
date: 2024-07-16
permalink: /posts/2024/01/ml-health/
# bibliography: test.bib
# layout: distill
tags:
  - Healthcare
  - ML
---

# Machine Learning for Healthcare: What Are We Doing, Really?


## Everything in ML is Relevant to Healthcare

## People >> Algorithms

Empathy and understanding is critical. Unlike some fields where being right or getting the best performance is all that matters, in healthcare, you need everyone to buy in, and to want to work with you. This extends beyond the doctors you work with to the IT staff, administrative support, and hospital executives. In fact, some of these other relationships can be even more important than the one you have with the doctors. For example, the IT staff for the hospital are essential for enabling and supporting your work. Their job first and foremost is to keep the hospital's network and systems running and safe. Any issues, any downtime, any vulnerability can cost millions of dollars, days of paperwork, and possibly patients' lives [reference optum outage]. It is very important to remember that their work does not revolve around what you are trying to do. Be respectful of this and appreciative for the time they spend helping you with your work. 

If you can, set up a brief, recurring meeting with the IT team where you can check in and raise any questions

## The Data is a Jungle
Complaining about messy data has become a common social practice for data scientists across disciplines. But throwing our hands up and calling the data "messy" sweeps too much nuance under the rug. It can mean many things in different contexts, and these differences matter. It is also a way to shift blame away from us, the practicioners, toward the data itself and the data collectors. Electronic medical records have been in use for decades with success, even if the system has not been optimal. While we can make progress toward improving the system over time, we, the new entrants into this well-established industry, must accept the realities of the data currently available, and work to prove the merits of our ideas within the existing framework. The reality is that in healthcare, the data isn't a mess, it's a __jungle__.

So what's in a jungle? Of course it's vibrant, lush, full of life. Hospital networks gather a staggering amount of data over time from millions of patients across different departments, sometimes with thousands of different measurements, tests, scans, and notes taken for each patient. There's data for newborns and their mothers, cancer patients coming in for regular treatments, emergency department patients with broken legs or bullet wounds (or both), and psychiatric patients, just to name a few. All these different pockets of life can be studied and explored, which is really exciting! Jungles also grow and change over time. In healthcare, the machines used change, the tests administered change, the patient population changes, and, critically, how data is recorded changes. Your data is in many ways a history of how this jungle has grown and changed over time, and it must be treated as such.

Like being dropped in a jungle, being handed access to a hospital network's data can feel daunting, overwhelming, and stressful. Even if you are only given access to a slice of the hospital's data, it can feel like information overload. What should you do? Where do you start? What does it all mean? This is where your relationship with clinicians becomes critical. Do not make assumptions about the meaning of different fields, or the properties of the data, or even the patients whose data you are analyzing. Ask, ask, ask. It will catch up to you eventually if you don't, and it can do real harm to real people if you deploy something that is based on false assumptions and misunderstandings. And remember, in this setting, you are the expert, and it may be the case that the clinicians you work with just assume your fancy algorithms have already figured it all out, so the onus is on you to ask.

Perhaps the most important and clarifying step in this process is __defining your cohort__. Do this early in collaboration with your clinical partners and revise as necessary. While this is standard practice for medical studies, it is not a concept typically discussed in the ML community. Clearly defining your cohort and agreeing on it with your clinical partners will help you focus your attention, cut through some of the weeds, and make sure you are on the right track. This is also the part where the dataset can significantly reduce in size. What was once a giant collection of data (inluding the aforementioned newborns and all) with millions of records will likely become a dataset a fraction of the size. 

Ask questions like how was this measurement taken? Will it change in the future? 


## Say Goodbye to the Cloud (For Now)

## Decisions or Predictions?

$x_7 + 8$

<!-- <d-cite key="arik_tabnet_2020"></d-cite> -->

