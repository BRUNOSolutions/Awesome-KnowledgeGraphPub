# Awesome Knowledge Graph Publications

The initial outline of this repository was primarily based the **comprehensive introduction to knowledge graphs** by [Hogan, A. et al, 02 July 2021, ACM Computing Surveys, 54(4): 1–37](https://dl.acm.org/doi/10.1145/3447772) as well as that introduction's [companion examples on GitHub](https://github.com/knowledge-graphs-tutorial/examples).

## Terminology

### Knowledge Graph 

Given the term's history, the exact [definition of a “***knowledge graph***"](https://arxiv.org/abs/2003.02320) was probably always bound to be a bit contentious, since the phrase “knowledge graph” was clearly used to evoke a hazily juxtaposed sketch of an idea linking "knowledge" and "graphs" in the technical literature since at least 1972 or mostly likely long before, because of how the term is built upon visionary notions of the ["information society"](https://en.wikipedia.org/wiki/Information_society) and ideas that have been floating around practically forever like *hyperlinks* from [Project Xanadu](https://en.wikipedia.org/wiki/Project_Xanadu) in 1965, which harked back to Vannevar Bush's popular essay, [As We May Think](https://en.wikipedia.org/wiki/As_We_May_Think) from 1945. Regardless of its original origins, the modern popularized incarnation of the phrase in common industry parlance seems to stem from the 2012 announcement of the Google Knowledge Graph echoed by the follow-on announcements of the development of *"yeah, we did that google stuff here, too"* [*knowledge graphs*](https://en.wikipedia.org/wiki/Knowledge_graph) by Airbnb, Amazon, eBay, Facebook, IBM, LinkedIn, Microsoft, Uber, and more besides. Even though its use might have been spurred by hypesters and evangelizers, the growing industrial uptake of the concept eventually proved difficult for even academia to ignore. More and more scientific literature is being published on [*knowledge graphs*](https://arxiv.org/search/advanced?advanced=&terms-0-term=%22knowledge+graphs%22&terms-0-operator=AND&terms-0-field=all&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=200&order=), which includes books as well as papers outlining definitions, novel techniques, surveys of specific aspects, at [REST API of ***academic graphs***](https://www.semanticscholar.org/product/api) based on [the Semantic Scholar Open Data Platform, the largest open scientific graph to-date ](https://www.semanticscholar.org/reader/cb92a7f9d9dbcf9145e32fdfa0e70e2a6b828eb1) ... and from that data platform, [a knowledge graph visual overview of ***ConnectedPapers*** on knowledge graphs](https://www.connectedpapers.com/main/091345fd98621d08424c93510149c13781da5f73/Knowledge-Graphs/graph).

The history of the Semantic Scholar Open Data Platform helps us to understand the defacto standard that make up a sophisticated data processing pipeline which continually ingests documents and metadata from numerous very large input sources, eg something Arxiv is one of more than fifty of those sources, extracting full text and metadata from PDFs, normalizing and disambiguating authors, institutions, and venues, classifying each paper’s field of study, generating a textual summary of its key results, and more. Sources may provide metadata in the [Journal Article Tag Suite (JATS) format](https://jats.nlm.nih.gov/), or a variety of proprietary formats ... one additional important source is human created data from manual corrections that are part of the curation process. 

The first task of the pipeline is to fetch the latest data from each source and parse it into a normalized format. Sources typically provide limited information about a paper in structured form: typically the title, author names, venue, and date, often linked to a
PDF file. A critical output of the Semnantic Scholar PDF content extraction is a structured bibliography from which the citation graph is constructed. To accomplish this, Semantic Scholar uses several open source toolkits, including:

* [PDFalto](https://github.com/kermitt2/pdfalto) is a command line executable for parsing PDF files and producing structured XML representations of the PDF content into [Analyzed Layout and Text (ALTO)](https://www.loc.gov/standards/alto/) format, which serves as an extension schema used within the [Metadata Encoding and Transmission Schema (METS)](https://www.loc.gov/standards/mets/) of the Library of Congress.

* [PDF-Plumber](https://github.com/jsvine/pdfplumber) is used to *Plumb a PDF* for detailed information about each text character, rectangle, and line, et cetera — and easily extract text and tables as well as debug visually. Works best on machine-generated, rather than scanned, PDFs and was built on [pdfminer.six](https://pdfminersix.readthedocs.io/en/latest/), which is the actively maintained version of the [original Python-based PDFMiner pdf-extractor, pdf2txt.py](https://pypi.org/project/pdfminer/).

* [PDFMiner.Six](https://github.com/pdfminer/pdfminer.six) is a community-maintained fork of the original PDFMiner. Since 2020, the original pdfminer went dormant and pdfminer.six became the recommended, actively maintained version of the original Python tool. PDFMiner.six, focuses on getting and analyzing text data, extracts the text from a page directly from the sourcecode of the PDF to parse all objects from a PDF document into Python objects in a human readable way.  PDFMiner.six can also be used to get the exact location, font or color of the text. It has support for [Chinese, Japanese and Korean (CJK) characters and derivatives](https://en.wikipedia.org/wiki/CJK_characters) as well as vertical writing and supports various font types (Type1, TrueType, Type3, and CID) as well as support for RC4 and AES encryption and support for [AcroForm interactive form extraction](https://pdfminersix.readthedocs.io/en/latest/howto/acro_forms.html) similar to that in [PyMuPDF](https://pymupdf.readthedocs.io/en/latest/about.html). PDFMiner.six is built in Python in a modular way, such that each component of can be replaced easily. Developers can implement their own interpreter or rendering device, such as [PDF-Plumber](https://github.com/jsvine/pdfplumber), that use/extend the power of PDFMiner for specific detailed purposes or to utilize Python objects for purposes that go beyond simpler text analysis.

* Older [PDFrw](https://github.com/pmaupin/pdfrw) or [fPDF in PHP](https://github.com/Setasign/FPDF) and hosts of other alternatives that preceded PDF-Plumber or PDFMiner.Six ... made necessary by the idiotic flocking to the proprietary PDF format by the publishing industry, which has been a source of frustration for developers for decades.

* [PyPDF](https://github.com/py-pdf/pypdf) a pure [python PDF library](https://pypdf.readthedocs.io/en/latest/) capable of splitting, merging, cropping, and transforming the pages of PDF files which is closely related to [PDFly](https://github.com/py-pdf/pdfly) a CLI tool to extract (meta)data from PDF and manipulate PDF files

* [Pike PDF](https://github.com/pikepdf/pikepdf) A Python library for reading and writing PDF, powered by [QPDF, content-preserving PDF document transformer](https://qpdf.readthedocs.io/en/stable/), which has been around and continuously developed since at least 2005.

* [PyMuPDF](https://pymupdf.readthedocs.io/en/latest/about.html) is perhaps the most mildly interesting new entrant into this realm of PDF parsing with a [comparatively active NEW dev community](https://github.com/pymupdf/PyMuPDF/issues), eg 367 forks and [three active discussion boards](https://github.com/pymupdf/PyMuPDF/discussions) on Github since [PyMuPDF's](https://github.com/pymupdf/PyMuPDF) [initial public release on GitHub [v 1.22.5] in June 2023.](https://github.com/pymupdf/PyMuPDF/releases/tag/1.22.5) 


https://github.com/kermitt2/grobid

https://github.com/allenai/science-parse

https://github.com/allenai/spv2

https://poppler.freedesktop.org/

https://github.com/Layout-Parser/layout-parser

https://github.com/allenai/VILA

https://github.com/allenai/papermage

### Related Tertiary Literature

A number of related surveys, books, and so on, have been published relating to knowledge graphs as tertiary literature—surveys, books, tutorials, andso on relating to knowledge graphs. Some of the related literature provides more detail on particular topics that are not particularly focused on knowledge graphs, familiarity with topics is useful as further background reading ... the primary focus of this curated list of publications is to provide a broad and accessible introduction to the specific topic of knowledge graphs.

#### Models

#### Querying

#### Shapes

#### Context

#### Ontologies

#### Entailment

#### Rules

#### DLs

#### Analytics

#### Embeddings

#### Graph Neural Networks

#### Symbolic Learning

#### Construction

#### Quality

#### Refinement

#### Publication

#### Enterprise KGs

#### Open KGs

#### Applications

#### History

#### Definitions