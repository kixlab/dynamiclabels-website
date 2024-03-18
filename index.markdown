---
layout: default
---

## Abstract

{: .sys-img}
<!--
<video muted autoplay controls loop>
  <source src="/assets/video/interaction-overview.mp4" type="video/mp4">
</video>
-->

Label set construction—deciding on a group of distinct labels—is an essential stage in building a supervised machine learning (ML) application, as a badly designed label set negatively affects subsequent stages, such as training dataset construction, model training, and model deployment. Despite its significance, it is challenging for ML practitioners to come up with a well-defined label set, especially when no external references are available. Through our formative study (n=8), we observed that even with the help of external references or domain experts, ML practitioners still need to go through multiple iterations to gradually improve the label set. In this process, there exist challenges in collecting helpful feedback and utilizing it to make optimal refinement decisions. 
To support informed refinement, we present <span style="color:{{site.syscolor}};font-weight:500">DynamicLabels</span>, a system that aims to support a more informed label set-building process with crowd feedback. Crowd workers provide annotations and label suggestions to the ML practitioner’s label set, and the ML practitioner can review the feedback through multi-aspect analysis and refine the label set with crowd-made labels. Through a within-subjects study (n=16) using two datasets, we found that <span style="color:{{site.syscolor}};font-weight:500">DynamicLabels</span> enables better understanding and exploration of the collected feedback and supports a more structured and flexible refinement process. The crowd feedback helped ML practitioners explore diverse perspectives, spot current weaknesses, and shop from crowd-generated labels. Metrics and label suggestions in <span style="color:{{site.syscolor}};font-weight:500">DynamicLabels</span> helped in obtaining a high-level overview of the feedback, gaining assurance, and spotting surfacing conflicts and edge cases that could have been overlooked.



------

## System

{: .img-center; width=90vw}

![An image illustrating the overall workflow of DynamicLabels](/assets/img/overall-workflow-new.jpg)
Figure 1: Label set refinement workflow using DynamicLabels.

<span style="color:{{site.syscolor}};font-weight:500">DynamicLabels</span> is a system that aims to support ML practitioners’ label set construction. <span style="color:{{site.syscolor}};font-weight:500">DynamicLabels</span> supports iterative refinement of the label set through two separate interfaces: the <span style="font-weight:500">feedback collection interface</span> and the <span style="font-weight:500">label set refinement interface</span>. The former is provided to the crowd to collect annotations and label suggestions on the ML practitioner-built label set, and the latter is provided to the ML practitioners for refinement with multiple analyses of crowd feedback.

### Feedback Collection Interface




#### Phase 1: Providing label suggestions by making the crowd’s own label set

{: .img-center; width="80%"}

![Phase 1 interface of the feedback collection interface](/assets/img/feedback-collection-interface-1.jpg)
Figure 2: Phase 1 of the feedback collection interface. 

Crowd workers start from the Phase 1 task: creating their own label set (Fig. 2). They are first asked to take a look at 30 assigned images (Fig. 2-b) and come up with a set of labels (Fig. 2-a). Then, they are instructed to use the labels to make annotations (Fig. 2-c).

#### Phase 2: Annotating with the ML practitioner-built label set

{: .img-center; .width=80%}

![Phase 2 interface of the feedback collection interface](/assets/img/feedback-collection-interface-2.jpg)
Figure 3: Phase 2 of the feedback collection interface. 

<!--The crowd workers are instructed to take a look at the (a) ML practitioner’s
label set and use the labels to annotate the (b) assigned images. Annotations will show up in (c), under each label. For images annotated using the “others” label, the workers are asked to provide a (d) brief reason each as an additional step.-->

Crowd workers then proceed to the next phase and use the ML practitioner-built label set to annotate the same 30 images (Fig. 3, b->c). In addition to the ML practitioner-built label set (Fig. 3-a), the workers are provided with an additional <span style="background-color: #d3eafd; font-family:sans-serif;">others</span> label to annotate images that do not fit into the provided label set to spot edge cases. For each image labeled <span style="background-color: #d3eafd; font-family:sans-serif;">others</span>, the workers are asked to provide a brief reason (Fig. 3-d) to justify their choice.

### Label Set Refinement Interface

{: .img-center; .width=80%}

![Overview of the label set refinement interface](/assets/img/refinement-interface-overall.jpg)
Figure 4: Overview of the label set refinement interface.

<!--In the top example, the ML practitioner can select (a)twolabelsinthecurrentlabelset(city and countryside)toseeadetailedview.Fromtherefinementsuggestionsin
the detailed view, the ML practitioner can (b) select crowd-made labels ( Manmade ) and click on the action (replace) to trigger the action consequence modal and make refinement decisions. In the bottom example, the ML practitioner can (c) click the plus icon next to the crowd-made label ( Organisms ) to add the label, which will trigger the action consequence modal.-->

#### Showing varying levels of analysis for the collected feedback

When the ML practitioner enters the label set refinement interface, they can find their initial label set on the top left, under “Your label set”. Right next to it is an overview (Fig. 4-b) that shows a summary created with the crowd feedback. Right next to it is an <span style="font-weight:500">overview</span> (Fig. 4-b) that shows a summary created with the crowd feedback. For the ML practitioner to understand the collected annotation in detail, they can select label(s), top conflicts, or unlabeled images to see a <span style="font-weight:500">detailed view</span> (Fig. 4-c). On the bottom right, the ML practitioner can explore refinement options, through an analysis of the crowd-made labels through the <span style="font-weight:500">crowd label view</span> (Fig. 4-d).

#### Providing refinement support with crowd-made labels

{: .img-center; .width=80%}

![Illustrating two ways to apply crowd-made labels to the current label set](/assets/img/refinement-interface-action.jpg)
Figure 5: Two possible ways to apply crowd-made labels to the current label set in the label set refinement interface. 

In <span style="color:{{site.syscolor}};font-weight:500">DynamicLabels</span>, we allow ML practitioners to make additions or replacements to their label set using crowd-made labels. The refinement actions can take place from refinement suggestions (Fig. 5-#1) or labels by each worker (Fig. 5-#2). On each refinement action, we display the <span style="font-weight:500">action consequence modal</span> (right of Fig. 5), where the change in the overview (the number of labels, coverage, conflict) is shown before making the change. 

#### Creating and exploring multiple label set candidates
On the bottom left, there is a saved label sets component (Fig. 4-e), which enables exploration of potential candidates with version control.


------

## User Evaluation

{: .img-center; .width=80%}

![Illustrating two ways to apply crowd-made labels to the current label set](/assets/img/study-procedure.jpg)
Figure 6: Overview of the study procedure containing tasks and procedure for each session. 

<!--In session 1, each participant creates two initial label sets for each dataset. The label sets are given to the crowd workers to collect annotation or feedback depending on the condition. In session 2, the participant refines their label set with the collected crowd data presented.-->


We conducted a 2-day study with 16 ML practitioners to investigate how DynamicLabels assists the ML label set construction process, through a within-subjects study comparing DynamicLabels to the baseline system, having annotation for crowd feedback and a table-like analysis for feedback review. Below are our results for each of the research questions.

#### RQ1: Can crowd workers produce helpful feedback with the feed- back collection interface?

Feedback from the crowd—--both annotation and crowd-made labels---contained diverse viewpoints and helped participants understand the various viewpoints of the crowd, some they had never expected before, and found it meaningful and useful in making refinements.

#### RQ2: How do ML practitioners use crowd feedback to refine their label sets?

Both crowd annotations and crowd-made labels were utilized to help the participants understand and apply the feedback as refinements. The crowd annotations helped ML practitioners to (1) understand the crowd’s general opinions and perspectives and (2) spot the weakness of their label sets, and the crowd-made labels helped them (3) explore and apply relevant ones to their label sets.

#### RQ3: How do ML practitioners use the refinement interface in DynamicLabels to make informed refinement decisions?

Throughout the study, we were able to observe the distinctive benefits of DynamicLabels over the baseline system in making more informed refinement decisions. When asked to compare the two conditions on how they helped their refinement decisions, most participants (13/16) rated DynamicLabels better than baseline.

The results state that DynamicLabels supports (1) a high-level understanding of the feedback with metrics, (2) better assurance through examining multiple options, (3) a structured refinement process. In addition, DynamicLabels (4) encouraged a more flexible refinement and (5) surfaced issues that might have been missed in comparison to the baseline. Such benefits supported participants to make more confident, efficient refinements with crowd feedback.

## Useful Links for the IUI '24 Paper


[Link to the PDF][1]

[Link to the ACM Digital Library (to appear)][2]

## Bibtex
<pre>
TBA
</pre>

------

{: .logos}
[![Logo of KIXLAB](/assets/img/kixlab_logo.png)](https://kixlab.org)
[![Logo of KAIST](/assets/img/kaist_logo.png)](https://kaist.ac.kr)

{: .center .acknowledgement}
This work was supported by NAVER CLOVA and the Institute of Information & Communications Technology Planning & Evaluation (IITP) grant funded by the Korea government (MSIT) (No.2021-0- 01347, Video Interaction Technologies Using Object-Oriented Video Modeling).

[1]:/papers/IUI2024-DynamicLabels-camready.pdf
[2]:https://doi.org/10.1145/3640543.3645157
