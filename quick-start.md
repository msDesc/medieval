Full (draft) encoding guidelines can be found [here](https://msdesc.github.io/consolidated-tei-schema/msdesc.html). This page is intended as a high-level overview for cataloguers unfamiliar with TEI.

TEI has the same aim as a printed catalogue - to present information about the manuscript in a structured and consistent manner and to make that information discoverable. The different parts of a printed catalogue entry are typically indicated by labels and/or typographical clues (font size, italic, whitespace, etc.). The different parts of a TEI entry are indicated using **elements** and **attributes**. The entries of a printed catalogue are made discoverable via indices and tables; the entries in a TEI catalogue are made discoverable by processing the elements and attributes to create electronic indices.

Elements and attributes are part of the XML markup language: the TEI guidelines provide a [gentle introduction to XML](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/SG.html). An element usually comprises a start-tag and end-tag which enclose text, for example the element `incipit`: `<incipit>Lorem ipsum</incipit>`. An attribute typically characterizes an element in some way, for example the attribute `type`: `<incipit type="prologue">Lorem ipsum</incipit>`. Comments can be added like this: `<!-- this is a comment -->`.

Elements are usually part of a nested hierarchy or tree which expresses the relationships between them. In the following instance, for example, the incipit and explicit are 'child' elements of the same 'parent' manuscript item:
```
    <msItem>
        <incipit>Lorem ipsum</incipit>
        <explicit>id est laborum</explicit>
    </msItem>
```
To create valid XML you need to ensure: (1) that there is a single element enclosing the whole document (the root element); (2) that elements do not partially overlap one another; (3) that a tag marks the start and end of each element (unless the element is self-closing, like `<gap/>`); (4) that reserved characters are avoided - thus the ampersand needs to be written `&amp;` and the opening and closing angle-brackets need to be written `&lt;`, `&gt;`. Valid TEI needs in addition to follow the rules of TEI! 

The quickest way to start creating a TEI record is to use a template. Be very careful, though, that you remove everything from the template that is not relevant, and that you do not accidentally carry over element or attribute that are irrelevant or incorrect in the context of your description. TEI documents must also contain certain elements which describe the nature of the TEI record and those responsible for its creation - the title statement (`<titleStmt>`) and publication statement (`<publicationStmt>`) - these are most easily adapted from a template.

Printed descriptions usually contain identifying information about a manuscript (its shelfmark) followed by three basic sections - the textual content, the physical description, and the history (origin and provenance). These may be followed by bibliography or other administrative information. TEI uses the element `<msDesc>` to enclose a manuscript description. This element contains the elements `<msIdentifier>`, `<msContents>`, `<physDesc>`, `<history>`, and `<additional>` for these sections. They must appear in that order. Composite manuscripts use in addition the element `<msPart>` which is described more fully below.

## Manuscript identifier

The `<msIdentifier>` element contains the manuscript's current shelfmark and information relating to the holding institution. Former shelfmarks and other identifiers (e.g. reference numbers in works of reference) may also be included. A typical Bodleian library `<msIdentifier>` looks like this:
```
    <msIdentifier>
        <country>United Kingdom</country>
        <region type="county">Oxfordshire</region>
        <settlement>Oxford</settlement>
        <institution>University of Oxford</institution>
        <repository>Bodleian Library</repository>
        <idno type="shelfmark">MS. Laud Misc. 246</idno>
        <altIdentifier type="internal">
            <idno type="SCN">1303</idno>
         </altIdentifier>
     </msIdentifier>
```
## Manuscript contents

The `<msContents>` element describes the textual content of the manuscript. It may consist of one or more `<msItem>` elements; these can in turn contain further `<msItem>` elements. The `<msItem>` element will typically contain a selection from the following elements, whose names are mostly self-explanatory:
* `<locus>`: describes the folios or pages on which the item appears
* `<author>`: contains the name of an author
* `<title>`: contains a title
* `<rubric>`: contains a rubric
* `<incipit>`: contains an incipit
* `<explicit>`: an explicit
* `<finalRubric>`: contains a closing rubric
* `<colophon>`: contains a colophon
* `<note>`: contains a note of some kind
* `<bibl>`: contains a bibliographic reference.
The `@key` attribute should be used with the `<author>` and `<title>` elements to provide a link to relevant authority records. 

Here is an example of a simple `<msItem>`:
```
    <msItem xml:id="MS_Laud_Misc_246-item3" n="3">
        <locus from="5r" to="59v">(fols. 5r-59v)</locus>
        <author key="person_59875293">Bernard of Clairvaux</author>
        <title key="work_1050">Sermones XVII in Psalmum XC Qui habitat</title>
    </msItem>
```

Here is an example of a more complex item with nested content:
```
                <msItem xml:id="MS_Laud_Misc_246-item4" n="4">
                     <locus>(fols. 59v-107v)</locus>
                     <author key="person_59875293">Bernard of Clairvaux</author>
                     <title key="work_1054">Sermones per annum siue de tempore et de sanctis</title>
                     <note>(selection)</note>
                     <msItem>
                        <locus>(fol. 59v)</locus>
                        <note>In labore messis sermo 1 (Sermo de diversis 38)</note>
                     </msItem>
                     <msItem>
                        <locus>(fol. 62r)</locus>
                        <note>Sermo de altitudine et bassitudine cordis (Sermo de diversis 36)</note>
                     </msItem>
                     <msItem>
                        <locus>(fol. 64r)</locus>
                        <note>In labore messis sermo 3 (Sermo de diversis 37)</note>
                     </msItem>
                     <!-- etc -->                     
                  </msItem>
```
## Physical description

The `<physDesc>` element contains the physical description of the manuscript. It contains the following elements, which must appear in this order:
* `<objectDesc>`: describes the support and layout. The `<objectDesc>` has a `@form` attribute to describe the format of the object:
`<objectDesc form="codex">`.

`<objectDesc>` contains the `<supportDesc>` element, which has a `@material` attribute describing the material support.
`<supportDesc material="perg">`

`<supportDesc>` contains the following elements, in the following order:
`<support>`,
`<extent>` (which itself contains `<dimensions>`)
`<foliation>`,
`<collation>`,
`<condition>`.
```
                    <supportDesc material="perg">
                        <support>parchment</support>
                        <extent>
                           i (modern endleaf) + i (17th century endleaf) + 299 + i (modern endleaf) leaves
                           <dimensions unit="mm" type="leaf">
                              <height max="483" min="480">c. 480-3</height>
                              <width min="350" max="356">350-6</width>
                           </dimensions>
                        </extent>                       
                     </supportDesc>
```


`<objectDesc>` also contains the `<layoutDesc>` element, describes the layout or mise-en-page in a series of `<layout>` elements.

```
                    <layoutDesc>
                        <layout columns="2" ruledLines="26">Ruled in ink. 2 columns of 
                              26 lines, ruled space <dimensions unit="mm" type="ruled">
                           <height max="341" min="337">c. 337-41</height>
                           <width min="233" max="236">233-6</width>
                        </dimensions></layout>
                     </layoutDesc>
```

* `<handDesc>`: contains description of the script
This is presented in a series of `<handNote>` elements. The `@script` attribute is used to provide a broad classification of the script.
```
                  <handDesc hands="2">
                     <handNote script="textualisNorthern">Textura by at least two hands (the second from fol. 275r). The 
                      life of St Rupert added in contemporary textus quadratus by a third hand.</handNote>
                  </handDesc>
```

* `<musicNotation>`: contains description of any musical notation in the manuscript
This is presented in a series of `<p>` elements.

* `<decoDesc>`: contains description of any decoration
This is presented in a series of `<decoNote>` elements. The `@type` attribute is used to classify the decoration.
```
                 <decoDesc>
                     <decoNote type="flourInit">Blue and red initials, with fleuronnée decoration usually 
                         in the contrasting colour.</decoNote>
                     <decoNote type="colInit">Coloured initials in red and blue.</decoNote>
                     <decoNote type="rubrication">Tituli in red.</decoNote>
                  </decoDesc>
```

* `<additions>`: contains description of marginalia
This is presented in a series of `<p>` elements.

* `<bindingDesc>`: contains description of the binding
```
                 <bindingDesc>
                     <binding notAfter="1639" notBefore="1637">
                        <p>Brown tanned calf over laminated pulpboard for Abp. Laud, 1637–1639.</p>
                     </binding>
                  </bindingDesc>
```

* `<accMat>`: contains description of 'accompanying material'


## History

The `<history>` element describes the manuscripts origin, provenance, and acquisition, using elements with those names.
* `<origin>`
This element contains the `<origPlace>` and `<origDate>` elements which describe when and where the manuscript was written. Dating attributes are used on the `<origDate>` element to provide a machine-readable date, and the `@key` attribute is used in `<origPlace>` to link to authority files.
```
                  <origin>
                     <origPlace>
                        <country key="place_7000084">German</country>, <settlement 
                        key="place_7004335">Würzburg</settlement> (<orgName key="org_148998848">St. Kylian</orgName> (?))
                     </origPlace>
                     <origDate calendar="Gregorian" notAfter="1410" notBefore="1400">15th century, beginning</origDate>
                  </origin>
```
* `<provenance>` and `<acquisition>`
These elements describe the provenance and acquisition of the manuscript. Dating attributes can be used to provide a machine readable date. The names of persons are marked up using the `<persName>` element with `@role` and `@key` attributes.
```
                  <provenance notAfter="1500" notBefore="1400"><orgName role="fmo" key="org_148998848">Würzburg, Domstift 
                       St Kilian</orgName> (?): fifteenth-century foliation resembles that  of other manuscripts from St 
                       Kilian in the Laud collection (<bibl type="MS" subtype="internal">MS. Laud Misc. 153</bibl>, <bibl 
                       type="MS" subtype="internal">MS. Laud Misc. 155b</bibl>, <bibl type="MS" subtype="internal">MS. 
                       Laud Misc. 157</bibl>).</provenance>
                  <provenance when="1636"><persName role="fmo" key="person_54940373">William Laud, 1573-1645</persName>: 
                        his ex libris, 1636, fol. 1r.</provenance>
                  <acquisition when="1639">Given to the Bodleian as part of his third donation, dispatched on 28 June 
                        1639.</acquisition>
```
## Additional

The `<additional>` element is used to provide administrative information (including the source of the description, restrictions on access, exhibitions), information about surrogates, and bibliography.

## Composite manuscripts

Composite manuscripts are described using the `<msPart>` element. Any information relating to the manuscript as a whole - for example, its binding, foliation, or aspects of its history - should be placed in the `<msDesc>` element. Information relating to each separate codicological unit should be placed in a series of `<msPart>` elements which are placed at the end of `<msDesc>`, after the `<additional>` element. The structure of the `<msPart>` element is exactly the same as `<msDesc>`, that is, a sequence of the `<msIdentifier>`, `<msContents>`, `<physDesc>`, `<history>`, and `<additional>` sections. 
