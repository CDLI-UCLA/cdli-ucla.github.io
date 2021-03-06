---
title: Annotation overview
sidebar:
  nav: "guides"
permalink: /guides/guide_overview.html
toc: true
---

## Gold standard annotation

### Workflow

1. Export raw ATF from the CDLI  
Manually export ATF of texts for annotation from the CDLI database. This can be done by performing a search at <http://cdli.ucla.edu/search> and clicking on "download" after the results appear.

2. Convert texts to pseudo-CoNLL for morphological annotation  
Use the Python script X to prepare a tokenized and CoNLL-style version of the textual information to facilitate morphological annotation.

3. Morphological annotation  
Manually annotate the morphology of the texts. In the case of the Ur III administrative texts, MTAAC follows the theory of Sumerian grammar described in Zólyomi 2017. According to this model, Sumerian adjectives are not a distinct word class — an adjectival expression is morphologically a non-finite verbal stem (see below for details). The nature of the writing of Ur III administrative texts, seemingly abbreviated and frequently omitting case markers, compels annotators to carefully adhere to theoretical models of grammar.

4. Conversion to full annotation set in CoNLL-U Format  
Using the X Python script, convert the new annotations to the fuller version that will be used by subsequent processes.

5. Conversion to Brat standoff  
Use the CoNLL-U to Brat standoff converter to prepare data for syntactic annotations using the Brat editor.

6. Syntax annotation  
Manual annotation of syntax using the Brat interface.


### CoNLL-like and CoNLL-U formats

CoNLL-U format information: <http://universaldependencies.org/format.html>  
CoNLL-U implementation based on: <http://universaldependencies.org/format.html>

Original CoNLL-U syntax calls for the following structure marking:

	# newdoc id = mf920901-001
	# newpar id = mf920901-001-p1
	# sent_id = mf920901-001-p1s1A
	# text = Slovenská ústava: pro i proti
	# text_en = Slovak constitution: pros and cons

We adapt this heading information as follows:
- In a comment line above the textual information, the text id must be mentioned, eg:
	# newdoc id = P653433

In CoNLL-U, blank lines are used to separate sentences. Since our documents are generally considered to be a sentence, a blank line will generally appear between texts and sometimes rarely inside a text to separate full sentences.

### CoNLL-U Fields  
#### Original CoNLL-U Fields  
ConLL-U field descriptions based on the Universal Dependencies website:

- ID: Word index, integer starting at 1 for each new sentence; may be a range for multi-word tokens; may be a decimal number for empty nodes.  
- FORM: Word form or punctuation symbol.  
- LEMMA: Lemma or stem of word form.  
- UPOSTAG: Universal Dependencies (UD) part-of-speech tag.  
- XPOSTAG: Language-specific part-of-speech tag; underscore if not available.  
- FEATS: List of morphological features from the universal feature inventory or from a defined language-specific extension; underscore if not available.  
- HEAD: Head of the current word, which is either a value of ID or zero (0).  
- DEPREL: Universal dependency relation to the HEAD (root if HEAD = 0) or a defined language-specific subtype of one.  
- DEPS: Enhanced dependency graph in the form of a list of HEAD-DEPREL pairs.  
- MISC: Any other annotation.  

#### MTAAC CoNLL-like fields for annotation
	# ID	FORM	SEGM	XPOSTAG	HEAD	DEPREL	MISC

- ID: all information about the surface, column, line and token (o.col1.1.1;  o.1.1 if there is no column). Only the column number is optional.  
- FROM: token from text, ATF transliteration  
- SEGM: normalized form of the token  
- XPOSTAG: ORACC ETCSRI morphological tags based on the segmentation and using POS tag or named entity tag instead of "STEM" for the stem (eg.: GN.ABL)  
- HEAD: id of token that is the verb for which this token is a subject or object  
- DEPREL: relationship with verb as subject, direct object or indirect object (nsbj/dobj/iobj)  
- MISC: semantic role of this word, eg. "seller"  

#### MTAAC CoNLL-U fields with processed data
	#ID	FORM	LEMMA	UPOSTAG	XPOSTAG	FEATS	HEAD	DEPREL	DEPS	MISC

- LEMMA: Lemma to which the token should be associated  
- UPOSTAG: Universal dependencies POS tag, based on a mapping between the ETCSRI POS and the UD POS  
- FEATS: Unimorph tags, in order of morpheme appearance  
- DEPS: will not be used at this time  


### Editors
- Morphological annotations are added to the CoNLL file manually using any plain text editor or a spreadsheet program.

- Syntax annotations can be added manually in the CoNLL file or using the Brat interface. We have a development Brat server up at <http://cdli-dev.org/brat/>.  

Brat website: <http://brat.nlplab.org/examples.html>  
Another dependency annotation tool: UD Annotatrix <https://github.com/jonorthwash/ud-annotatrix>    


### Morphological annotation example



| #ID           | FORM          | SEGM                |XPOSTAG        |
| ------------- |:-------------:| ----------------------:| -------------:|
| 0.1.1         | 3(u)          |3(u)[ten]               |NU             |
| 0.1.2         | sila3         |sila[unit]              |N              |
| 0.1.3         | sze           |sze[barley]             |N              |
| 0.2.1         | a-a-kal-la    |Ayakala[1]              |PN             |
| 0.2.2         | sagi          |sagi[cup_bearer][-ra]   |N.DAT-H        |
| 0.3.1         | 3(u)          |3(u)[ten]               |NU             |
| 0.3.2         | sila3         |sila[unit]              |N              |
| 0.3.3         |lu2-dinger-ra  |Ludingira[1]            |PN             |
| 0.3.4         |sagi           |sagi[cup_bearer][-ra]   |N.DAT-H        |
| 0.4.1         |sza3-gal       |szaggal[fodder]         |N              |
| 0.4.2         |udu            |udu[sheep]              |N              |
| 0.4.3         |niga           |niga[fattened][-ø][-sze]|N.V.ABS.TERM   |
| 0.5.1         |ki             |ki[place]               |N              |
| 0.5.2         |gu-du-du-ta    |Gududu[1][-ak]-ta       |PN.GEN.ABL     |
| r.1.1         |kiszib3        |kiszib[seal]            |N              |
| r.1.2         |a-lu5-lu5      |Alulu[1][-ak]           |PN.GEN         |
| r.2.1         |iti            |iti[month]              |N              |
| r.2.2         |diri           |dirig[excess][-'a]      |N.L1           |
| r.3.1         |mu             |mu[year]                |N              |
| r.3.2         |si-mu-ru-um{ki}|Simurrum[1][-ø]         |SN.ABS         |
| r.3.3         |ba-hul         |ba-hulu[destroy][-ø]    |MID.V.3-SG-S   |
| s1.1.1        |a-lu5-lu5      |Alulu[1]                |PN             |
| s1.2.1        |dumu           |dumu[child]             |N              |
| s1.2.2        |inim-{d}szara2 |Inimsara[1]             |PN             |
| s1.3.1        |kuruszda       |kuruszda[fattener]      |N              |
| s1.3.2        |{d}szara2-ka   |Szara[-ak][-ak]         |DN.GEN.GEN     |



## Automated annotation workflow




*Émilie Pagé-Perron*
