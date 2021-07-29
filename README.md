# PLOVER

![plover_icon](https://github.com/openeventdata/PLOVER/blob/master/media/plover_icon175.png "PLOVER logo")

PLOVER–Political Language Ontology for Verifiable Event Records–is a
next generation political event coding specification under development by the
Open Event Data Alliance (http://openeventdata.org/) which is intended
to replace the earlier
[CAMEO] (http://eventdata.parusanalytics.com/data.dir/cameo.html)
system. 

The full PLOVER codebook is available in the repo
[above](https://github.com/openeventdata/PLOVER/blob/master/PLOVER_Manual.pdf),
and a short introduction to PLOVER and event data is below.

## Event Data and Ontologies

Event data in political science is a structured way of recording interactions
between political actors described in text. For instance, a researcher
encountering the sentence 

> A town in western Sudan's South Kordofan state has been recaptured by Sudanese
> government forces from the rebel Sudan People's Liberation Army (SPLA).
(AFP_ENG_19970408.0772)

might want to represent it as ACTOR = "Sudanese military", EVENT = "capture
territory", TARGET = "SPLA", a process that can be applied over hundreds of
thousands of reports to create datasets of thousands of such events for
answering research questions. 

The software to extract and categorize these events exists (see OEDA's
[Petrarch2](https://github.com/openeventdata/petrarch2), for instance), but all
event data systems require an ontology defining what actors events will be
recorded and how they will be defined.

Ontologies face difficult tradeoffs: broader groupings of event types and
actors are easier to define and implement, are easier to work with, and provide
data at a useful level of aggregation, especially analyzed globally. More
specialized and specific ontologies will sometimes be necessary for answering
certain research questions and allow more granular and subnational study, but
are more difficult to implement and may provide distinctions that are not
useful to most researchers. In the example above, should the event be
categorized as a general "seize" event? Or a more specific "capture territory"?
Should the target be the group the land was taken from, or should we think
about the territory itself as the target. If the group it was taken from,
should the target here be coded as a general "Sudanese rebel" or the very
specific "SPLA"? 

The best level of detail will depend on the question and resources of the
researcher.  PLOVER is a new event data ontology that choses to be more
general, easier to implement (including across languages), and at the level of
detail demanded by most existing users of event data. At the same time, PLOVER
defines and provides guidance on making "PLOVER-compliant extensions" that will
fit into the ecosystem of tools for creating and analyzing PLOVER event data.


PLOVER event categories 
====================

PLOVER defines 18 event types, many of which are aggregations of older CAMEO
codes:

CAMEO code | CAMEO text | PLOVER category |
--- | --- | --- |
01 | MAKE PUBLIC STATEMENT | dropped |
02 | APPEAL | dropped |
03 | EXPRESS INTENT TO COOPERATE | AGREE |
04 | CONSULT | CONSULT |
05 | ENGAGE IN DIPLOMATIC COOPERATION | SUPPORT |
06 | ENGAGE IN MATERIAL COOPERATION | COOPERATE |
07 | PROVIDE AID | AID |
08 | YIELD (081 to 083) | CONCEDE |
08 | YIELD (084 to 087) | RETREAT |
09 | INVESTIGATE | INVESTIGATE |
10 | DEMAND | DEMAND |
11 | DISAPPROVE | DISAPPROVE |
12 | REJECT | REJECT |
13 | THREATEN | THREATEN |
14 | PROTEST | PROTEST |
15| EXHIBIT FORCE POSTURE | MOBILIZE |
16 | REDUCE RELATIONS | SANCTION |
17 | COERCE | COERCE |
18 | ASSAULT | ASSAULT |
19 | FIGHT | ASSAULT |
20 | USE UNCONVENTIONAL MASS VIOLENCE | ASSAULT |
-- | no CAMEO equivalent | CRIME |

PLOVER quad categories
----------------------

Many users of event data aggregate events into four categories in a 2x2 of
cooperation--conflict and verbal--material. Those categories are defined in
terms of their constituent categories here:

Quad category | PLOVER categories |
--- | --- |
Verbal cooperation | AGREE, CONSULT, SUPPORT, CONCEDE |
Material cooperation | COOPERATE, AID, RETREAT, INVESTIGATE |
Verbal conflict | DEMAND, DISAPPROVE, REJECT, THREATEN, SANCTION |
Material conflict | PROTEST, CRIME, MOBILIZE, COERCE, ASSAULT |

Migrating From CAMEO 
---------------------

The existing standard ontology for event data is
[CAMEO](http://eventdata.parusanalytics.com/data.dir/cameo.html). Users who are
familiar with CAMEO may be interested in the differences between CAMEO and
PLOVER.

-  A set of standardized names ("fields") for JSON
   records are specified for both the core event
   data fields and for extended information such as geolocation and
   extracted texts. Most of these fields are optional but standardized
   field names will allow for the development of common utilities, which
   cannot be done with the current proliferation of incompatible CSV and
   tab-delimited formats.
-  Only the 2-digit event 'cue categories' have been retained from
   CAMEO: our hope is that these are sufficiently broad and distinct
   that it will be possible to achieve a reasonably high level of human
   inter-coder agreement— hence "verifiable"—on the coding categories,
   and that can be consistently implemented, across all categories, in
   automated systems. These are defined in much greater detail than they
   were in WEIS and CAMEO.
-  Much of the detail previously incorporated in the 3- and 4-digit CAMEO categories is
   now reflected in category-specific "mode" fields and a general "context"
   field: in effect, this "category-mode-context" scheme covers the "what-how-why" of
   the event. We anticipate these will be much easier to systematically code
   than the 250 or so hierarchically-arranged numerical codes of CAMEO. The "context" field also to handles
   issues such as refugees, disease, natural disaster, elections, parliamentary
   processes and cyber-security.
-  The CAMEO 01 and 02 categories dealing with comments have been
   eliminated.
-  A new category has been added for criminal behavior.
-  The WEIS/CAMEO YIELD category has been split into verbal (CONCEDE) and material (RETREAT) components.
-  The complexity of substate actor codes has been limited, and the
   allowable substate modifiers have been substantially simplified.
-  The "target" is optional in some categories.
-  Both the source and target fields can have compound actors, rather than 
   dealing with compounds by duplicating event.
-  'dead', 'injured' and 'size' fields are available for recording information
   on the magnitude of acts of violence and protests.
-  In the near future, we are hoping to make available a large corpus of
   "gold standard records" for validation purposes: these will include
   Spanish and Arabic cases as well as English. The current release
   has a file of English-language gold standard records derived from
   from the CAMEO manual.


Why "PLOVER"?
=============

[Plovers](http://www.rspb.org.uk/discoverandenjoynature/discoverandlearn/birdguide/name/r/ringedplover/)
(Charadriidae) are a globally-distributed family of short-billed
gregarious wading birds who spend their lives frantically poking through
endless stretches of sand and muck trying to find something of interest.
It is difficult to imagine a better analogy to the process of coding
event data.

Description of files in repository
==================================

* **PLOVER_Manual.pdf**

   The PLOVER manual is currently being developed on an *overleaf.com* site; this is intended to be reasonably current versions of that file
      
* **PLOVER_Manual_tex.zip**

   *overleaf.com* version of the source code for the PLOVER manual

* **plover_reference.html**

   Basic reference for the PLOVER event categories in HTML format
      
* **gold_standard_records/PLOVER_GSR_CAMEO.txt**

   This is a JSON file of the example sentences from the CAMEO 1.1b3 manual classified by PLOVER categories. The CAMEO LaTeX markup indicating source, target and event texts has been converted to a simple in-line markup; some locations have been added manually. The details of the coding are found in the files *PLOVER_GSR_CAMEO_readme.tex/pdf* and the version of PLOVER being coded is in the older file *plover-manual_draft.0.6b1.pdf*.
   
* **CAMEO-PLOV.txt**

   Translation table for CAMEO to PLOVER: this is still something of a draft but will get you started
   
* **CAMEO.RCS.pdf**

   CAMEO Religious Coding system (Mattias Heilke), pdf format
      
* **CAMEO.RCS.tex**

   CAMEO Religious Coding system, LaTeX source. This is formatted with sufficient consistency that it can easily be used as a sector dictionary.
   
   
* **CAMEO.ECS.pdf**

   CAMEO Ethnicity Coding system (Benjamin Bagozzi and Jay Yonamine), pdf format
      
* **CAMEO.ECS.tex**

   CAMEO Ethnicity Coding system, LaTeX source. This is formatted with sufficient consistency that it can easily be used as a sector dictionary.

Acknowledgments
===============
This program was developed as part of research funded by a U.S. National Science Foundation "Resource 
Implementations for Data Intensive Research in the Social Behavioral and Economic Sciences (RIDIR)" 
project: Modernizing Political Event Data for Big Data Social Science Research (Award 1539302)


Any opinions, findings, conclusions or recommendations in this document are [only *probably* still] those of [at least one of] the authors and do not necessarily reflect the views of the National Science Foundation, or any company or government agency employing or funding the authors or otherwise contributing to the document.

This work was sponsored by the Political Instability Task Force (PITF). The PITF is funded by the Central Intelligence Agency. The views expressed in this codebook are the authors' alone and do not represent the views of the US Government.

This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.

