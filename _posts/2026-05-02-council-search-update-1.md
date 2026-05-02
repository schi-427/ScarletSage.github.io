---
layout: post
title: Conway Council Search Update
date: 2026-05-02
category: Programming
permalink: /blog/greenspace-map-2/
---
I've made a series of enhancements to my [city council search tool](https://schi-427.github.io/CouncilSearch/). 

This application came about because I wanted an easier way of analyzing and finding city council meeting minutes and agendas. 
For example, if I wanted to know when a certain ordinance was passed or discussed, I'd previously need to click on [each agenda document](https://www.conwaysc.gov/departments/administration_new/agendas___minutes.php) until I found what I wanted.
My app works by first scraping each link on the above page, producing a set of metadata for each. This metadata is then processed in order to extract the raw text of each pdf, which I then make searchable in my index.html page. 
After noticing some PDFs were only images rather than searchable documents, I added logic to run these through an OCR process in order to make them searchable. 

In this way, I make searching for particular topics covered by the various city commissions much faster, enhancing transparency and accountability.

The past couple days I've enhanced this tool to include filters for each of the city's commissions/boards, along with a sorting option selector. 
Also, after noticing some documents did not match the commissionTitleDate.pdf format that most of them had, I added logic in my pdf text extraction function to address this. 
Currently, documents without a commission in the title are given "unkonwn" as the commission title. Not ideal, but at least this way they show up in the search results.
Going forward I'll try to work out a way to possibly extract the commission from the document text in these cases. 

Also, in cases where the date is not in m.d.yyyy format, but rather simply "Month Name, Year Name", I handle this by assigning it to the first of the given month. 
Again, not ideal, but I determined this to be better than giving it no date. 

Overall Im quite happy with the application as it stands. Some enhancement I'll look into going foward include:

* Styling changes, make the app more visually appealing
* Data analytics tools, such as word cloud generation
* Analysis that determines major topics in each document, with associated filter options

