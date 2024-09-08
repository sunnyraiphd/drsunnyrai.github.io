---
title: 'Detecting Human Needs from Social Media Posts'
layout: post
category:
- human behavior
---

Unmet needs scoping can help in designing public policies to cater to evolving needs of a society. Since COVID-19 was declared a pandemic, the world witnessed a variety of control measures which in turn led to the widespread feeling of unfulfillment either due to unfulfilled daily necessities or dwindling opportunities to accomplish one's goals. Early detection of human needs can enable public agencies and independent organizations to provide prompt support including food supplies, medical care and timely awareness about the crisis amongst masses. But how? Here's an approach with two key modules namely (a) Mapping Tweets with Needs and (b) Detecting Unmet needs, as shown below.

<figure>
  <img src="/images/pandemicNeeds/PandemicNeedsBlog.png" alt="news" style="width:100%">
</figure>


 The motive behind this study was to understand how the pattern of needs has evolved from pre-COVID-19 phase to different stages of COVID-19 namely *lockdown*, the *first wave* and the *second wave.* Indian tweets posted between Dec’19 to Jul’21, spanning a period of 19 months were collected using snscrape.

## Mapping Tweets with needs
Manual annotating tweets with their expressed need is expensive and time consuming. We use topic modeling to label tweets - topic modeling is statistical modeling for discovering the abstract “topics” that occur in a collection of documents [wiki]. Idea is to identify these abstract topics in large collection of tweets and then label topics which are much smaller in size! 
As a proof of concept, we used Maslow’s Hierarchy of Needs (MHoN) (Maslow and Lewis, 1987), which categorizes the
human needs into five distinct levels namely physiological[L1], Safety [L2], Love and Belonging [L3], Esteem [L4] and Self-Actualization [L5]. The first two levels namely physiological and safety in MTM are often considered as basic needs whereas the next three levels namely love and belonging, esteem and self-actualization are regarded as advanced needs. 

Here, we illustrate the week wise distribution of tweets tagged with needs. One such tweet annotated with physiological need is “*Nobody staying at hotels, So why not convert them into covid centers*”.

 <figure>
  <img src="/images/pandemicNeeds/maslowNeedsDistribution.png" alt="news" style="width:80%">
</figure>

## Detetecting unmet Needs
The next task was to identify the tweets that were discussing unfulfilled needs. In Frustration-Aggression theory, Dollard et al. (1939) defined frustration as an impediment
or blockage in achieving one’s needs or goals. We hypothesized that unmet needs can be detected by identifying if tweets already marked with needs contain frustration or not. We finetuned the pretrained RoBERTa language model for this task. 

Below are two example tweets:

`HOW fast does one have to be to book a slot on COWIN? I saw slots available at a hospital; I selected the time slot; entered the CAPTCHA in not more than 15 seconds... and still it didn't book the slot. And then when I refreshed, all the slots were gone.` - **Frustrated**

`I did it! ... I officially completed my undergraduate program and received my bachelors degree. may the glory be to God for blessing me with the gifts to achieve this great milestone` - **Not Frustrated**

### Results and Discussion:

 Of 1.1M tweets tagged with needs, our model predicted over 792K tweets expressing frustration. Below are few example tweets marked as frustrated.
 
  <figure>
  <img src="/images/pandemicNeeds/examples.png" alt="news" style="width:70%">
</figure>
 
Here's the week wise transition in the volume of frustrated tweets expressing basic and advanced needs. There is a huge jump in the volume of both categories of tweets. More tweets expressing frustration due to basic needs were posted during the lockdown in comparison to the second wave. The volume of basic tweets during the first wave remained slightly above the pre-COVID level.

 <figure>
  <img src="/images/pandemicNeeds/basicAdvRoberta.png" alt="news" style="width:80%">
</figure>


The proportion of frustrated tweets across *basic* and *advanced* level of needs is illustrated below. 

 <figure>
  <img src="/images/pandemicNeeds/ProportionBasicAdv.png" alt="news" style="width:80%">
</figure>

Almost 80% of tweets expressing basic needs are unmet irrespective of the time of the year. It seems that users discuss basic needs only when these needs are unfulfilled. The general rate of frustration for advanced needs is 60%. As soon as the frustration due to basic needs reduces, the frustration due to advanced needs increased by over 10%.

### Key Themes behind *frustration*

We used VOSviewer to learn the themes of frustrated tweets posted during lockdown and the second wave of COVID-19.

 <figure>
  <img src="/images/pandemicNeeds/LockdownVOS.png" alt="news" style="width:100%">
</figure>


The above figure illustrate the key concerns expressed during **Lockown**. Travel concerns due to the imposed nationwide lockdown are evident from the terms in cluster *blue* as shown above. Major Indian cities namely *bengaluru, bihar, pune* coupled with transportation choices such as *bus, train, vehicle* can be seen. There are terms such as *quarantine, doctor, patient, office* in the same cluster indicating the traveling problems faced during daily life activities. The nodes in *green* reveal the challenges faced by logistics and travel industry. Terms such as *refund, ticket, airline, flight, credit* reflect the chief complaints by customers along with *bill* and other *payments*.

The nodes in cluster *red* highlight the discussion on digital media and news channels. Growing concern due to increasing toll of infections in the USA and a sense of anger towards China were expressed through tweets. Fake news, channel, minority and economy were also a few topics of online discussion. The nodes in cluster yellow depict the concerns revolving around closed *educational institutions, payment of fees, online classes *and *exams.*

The below figure illustrate the key concerns expressed during the **Second Wave**.

 <figure>
  <img src="/images/pandemicNeeds/SecondWaveVOS.png" alt="news" style="width:100%">
</figure>

The usual customer care complaints are depicted in cluster *green*. The nodes in cluster *red* particularly reveal the frustration against political parties and elections. There are also terms such as *player, season, ball, game* due to upcoming IPL cricket matches. The anxiety due to shortage of *ventilator, patient, hospital, icu bed * and *oxygen cylinder* is captured through nodes in cluster blue. Words such as refer, friend, help reveal
anxious attempts to locate healthcare through contacts on Twitter. Availability of vaccine and booking of slots were also a cause of frustration amongst Indians. Education remained a concern during the second wave as evident from nodes marked in *purple*.

### Conclusion
A minimally supervised approach to annotate tweets with their need level as in Maslow's Hierarchy of Needs can greatly reduce the time and human effort without much impact on the quality of annotation. A recurring pattern in the needs, indicating predictability in the emerging needs was observed. Pretrained language models used for detecting unmet needs detection, generalises well and is capable of transfer learning from previously labelled data at the start of a crisis.

#### Credits:
[1] https://ai.facebook.com/blog/roberta-an-optimized-method-for-pretraining-self-supervised-nlp-systems/

Read more: Rai, S., Joseph R., Thakur P.S. & Khaliq A.M. (2022). **Identifying Human Needs through Social Media: A study on Indian cities during COVID-19**. <a href="https://sites.google.com/view/socialnlp2022/" target="_blank">Social NLP,  NAACL 2022</a> . Available at <a href="https://www.researchgate.net/publication/360726343_Identifying_Human_Needs_through_Social_Media_A_study_on_Indian_cities_during_COVID-19" target="_blank">Link</a>
