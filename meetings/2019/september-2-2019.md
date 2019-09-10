# Meeting September 2 - DCAP Hackathon

This document: https://hackmd.io/QBn-xdKjSvyytYt3yJIpzA

Monday, September 2
06:00-07:00 Berkeley / 15:00-16:00 Bonn / 22:00-23:00 Tsukuba
https://zoom.us/j/168793047

Expected: Tom, Karen, Phil, Stuart, Eric (Prud'hommeaux), Andra, Stefanie, Nishad
(see https://doodle.com/poll/3vu2kqanmf6enxfx )

## DCAP2

* Abstract model for application profiles
  * Motivating use case: helping the "spreadsheet-enabled" author application profiles
  * How simple can the model be? (What is _too_ simple?)
  * When is it "good enough" to get started?
  * Abstract model https://github.com/dcmi/dcap/blob/master/schemaList.csv
      * Inspired by [DC-DSP](https://www.dublincore.org/specifications/dublin-core/dc-dsp/) (2008)
  * Karen's [design questions](https://lists.dublincore.org/pipermail/application-profiles-ig/2019-August/000062.html)
      1. Can a profile exist without statements? (aka properties) I am imagining that a profile can exist ONLY of statements - can be a flat list of statements without separate descriptions. But I can't imagine that reversed.
      2. Along with identifiers, should display labels be mandatory for description set, description, statement?
  * [Trade-off](https://lists.dublincore.org/pipermail/application-profiles-ig/2019-August/000063.html) between simplicity and modularity?
  * Enable [descriptions within descriptions](https://lists.dublincore.org/pipermail/application-profiles-ig/2019-August/000065.html)?
  * How many of the [design patterns](https://github.com/kcoyle/RDF-AP/blob/master/Patterns.md) should be supported?

* Input formats for users creating profiles
  * Spreadsheet templates?
  * Editable markup (YAML, [YAMA](https://nishad.github.io/yama/spec/latest/))?
  * Forms interfaces ([Sinopia](https://profile-editor.sinopia.io/#/profile/sinopia))? ([Bibliotek-o](https://docs.google.com/presentation/d/1z6KkJ4SZLle_WECEbZ6sXdO5KfNhQ8MmhMvIXSZ-Ek4/edit#slide=id.g2a1735f29f_0_37))

* Export formats (or are they intermediate formats?)
    * [JSON](https://github.com/dcmi/dcap/blob/master/examples/schema2.json) (JSON-LD or JSON Schema)?
    * YAML? [YAMA](https://nishad.github.io/yama/spec/latest/)?
    * [ShEx Lite](https://dcmi.github.io/dcap/shex_lite/micro-spec.html)
    * How easily must the export format be editable by non-expert users?

* Conversion into schema languages?
    * [ShEx Lite](https://dcmi.github.io/dcap/shex_lite/micro-spec.html), [SHACL](https://data.perio.do/v.ttl.html), XSD... Any other obvious candidates?
        * Convert ShEx Lite converted to ShEx, SHACL, and JSON schema?

* Conversion of import _or_ export format into Web pages or visualizations
  * Jose Labra convert ShEx Lite into UML visualization?
  * Generate documentation from, say, YAML?

## What can we accomplish in Seoul?

* Preparation:
  * Draft Abstract Model ("vocabulary")?
  * Sample instances - eg, https://github.com/dcmi/dcap/blob/master/examples
  * Bring software or links for trials
  * Build out comparison at https://github.com/dcmi/dcap/blob/master/BIBFRAMEcompare.csv

* To do on site
  * Agree one or more vocabularies to test
    * How reduced of a vocabulary will be accurate for testing?
  * Debug vocabularies in tools (if possible)
  * Test transformations

* Next steps: 
  * Write up pitch for DC-2019 Hack Day https://hackmd.io/i7tC1gC6RXOFtzElnhlpZw

* Additional links
    * https://tools.ietf.org/html/rfc4180 
    * https://github.com/kcoyle/RDF-AP/blob/master/csv/statement.csv 

# Minutes

kcoyle: This meeting is to determine what we can accomplish in Seoul, and what we need to do beforehand so that the hack day goes well.

tom: The [schemalist.csv file](https://github.com/kcoyle/RDF-AP/blob/master/csv/statement.csv) is a schema for schemas. It is similar to the description set profile. To me this is "good enough" that we can accept it for now and move on to the next tasks, which are to define input and export formats (expressions) that use this model. Possibly spreadsheets or simple markup. Output could be JSON, shex, shacl, xml schema. We need examples that are expressed in that language and try out different models.  For the Hack Day, if we had examples that we could express in terms of that models, we could look at how to convert between representations.

kcoyle: my questions: (see agenda)
- how to have best reusability, how to link entities to each other (top down or bottom up? Description linking down to statements, or statements linking up to description?)
- nearly everything in list is optional, as a way to simplify the vocabulary
- the only thing that is required is the identifier on each entity, but even the different entities are not required, nor would Description Sets be mandatory

Stefanie: Also label is required.

kcoyle: we could rethink that

Stefanie questions whether description should be optional - to have statements one must have a description and a description set. Person filling in form doesn't need to say what they have; perhaps background software can fill in the structure.  Reality: If I have statements, I have a description - but the person filling in the form need not know that.

kcoyle: Possible to say: must be a description.  Many crude vocabularies are just lists of properties.

ericp: ...and no real guidance on where they MAY appear or MUST appear.  This lack of structure is partly what drove me to work on ShEx. In the interest of having the leanest viable product...: I you have min/max on descriptions - what is the use case?

kcoyle: Where you have a book entity and an author entity and you can have author required (min) and a maximum number allowed. (Note from KC: this brings up question of where min/max are located - in entity or in "calling" entity. We left this unclear.)

ericp: So is that in the scope of a document?  If I have a description of a book, I can limit the number of authors allowed.  That's a cardinality on the statement, not a description.

Tom: If you have entity creator and creator has max 3. Maybe remove these from description in the interest of simplification.

kcoyle: ok let's try with examples

Stefanie: description set is container of descriptions; descriptions are different things; description is package level (like a record)

ACTION: kcoyle - create a new UML; everything one-to-many except statement to value

tom: let's agree on set of examples.  And find different ways to express that syntax.

ACTION: kcoyle to change the display labels in the csv to camel-case so they can be used directly in the examples, and create a csv with just entity, camelCase and cardinality (DONE https://github.com/dcmi/dcap/blob/master/simpleSchema.csv)

ACTION: on Tom and Karen - Add a blurb to the hackathon page: https://hackmd.io/i7tC1gC6RXOFtzElnhlpZw

Tom: May I suggest that for the purposes of this exercise, we use the names in your second column and put them under the ex: namespace.

Karen: Will do a simplified list.  And display names will be optional.

Stefanie: If there are no Descriptions, I do not need a Description Set.  If I have a Description, need to say something about the Statements I use.

Karen: Dependencies are hard: if you have a value, there must be a statement.  We also have no way to say: If we have Statement A we must have Statement B.

Tom: Should be limits on this format.  Should be flat.  The more complex you get, the more you should be using ShEx, SHACL, or XML Schema directly.  Should come out of the Hack Day with something simple that works - that has an input format like a spreadsheet, and output formats like ShEx or documentation webpage.  But we should make this as simple as possible, even at the risk of being simplistic.

EricP: UML has been wrestling with disjunction for decades: it is really hard to say if you have one of these you must have one of those.

Stefanie: Problem is that I really need this in my work.

EricP: But do you need it the spreadsheet?

Stefanie: I need the spreadsheet to build the schema, and I need to schema to express such things.

EricP: When Tom and I did ShEx Lite, we pared it down to features we thought one would want to represent in spreadsheets.  Your model may be complex - cooccurrence constraints - but subset that is writable in spreadsheets.

Karen: Yes, and we'd like to have easy conversions from spreadsheets to other formats.

Tom: Jose Labra Gayo, at a biohackathon in Japan, heard about ShEx Lite - saw that his tool could visualize in UML.

Nishad: The "My Bookcase" example - would be nice to have entirely different.

ACTION: Stefanie to bring examples from German digital library and SUB university collection (all areas of science).

ACTION: Karen to bring examples from Data Catalogue (DCAT): census data, etc.

Stuart: Phil, something from education workforce development - something outside of library?

Karen: will provide test spreadsheet where labels directly usable in code.

Tom: Would that export to something beside CSV?  Nishad's YAML format?  ShEx Lite?  Those would be syntax representations of the content of the spreadsheets.  If we could at least get to that point - and have two or three targets from the spreadsheet, we could work on converting those into more expressive validation languages.  That is what I would like to see happen.  We would need a spreadsheet template and a target format, and some notion of what those would be converted into.

Karen: How do you represent multiple statements in spreadsheets without having multiple tabs?  What kind of a usable form?

Tom: Nishad, what is your thinking on use of YAML here.  Also: this discussion is confusing because of the meta levels.  The document we are discussing perhaps needs a name.  Nishad, it would be great if your YAML format could map directly to the spreadsheet model.  Would be great if it could round-trip - generate YAML from spreadsheet or vice versa.  And from there to ShEx Lite.

Nishad: I can work on a YAML expression and try to do a conversion.  One problem: if we put everything into one CSV, would break [RFC 4180](https://tools.ietf.org/html/rfc4180), which I would hate to do.  There was an initial proposal from Karen to split the model into separate CSVs.  This is easier than trying to put everything into a single CSV. 

Tom: What would the spreadsheets be?

Nishad: If you are using Excel, you could have multiple tabs, but if CSV, they would be multiple files. If every statement goes into a spreadsheet, can call by ID.

Karen: Iterate on IDs?

Nishad: Yes.

ACTION: Karen to send example to the list, with a crude example.

Stefanie: Would like to go from spreadsheet to ShEx we can use to validate the collection.  I have some data for that, so I would really love to test the data for the university collection - want to test compliance with my AP.

Karen: We talked about ability to go from individual elements directly to...  Wonder if an algorithm could go directly from CSV to ShEx/SHACL, etc.

Nishad: If every element has its own ID, straightforward.  Custom template.  Would be straightforward to convert to other formats.

EricP: Translation should be easy.  Depends how many things you want to translate to.  Are you mostly thinking of one input format - simplifies things.

Nishad: Eric, if we visualize a good structure for the AP - what about intermediate representation?

EricP: It's just that you end up writing tools for the intermediate representation.  Easier to steal existing tools and formats.

Tom: In the Japan workshop, today (looking at their hackathon notes) they concluded that ShEx Lite would be convertible into ShEx, SHACL, or JSON Schema.  It seems to be generic enough.  And presumably you could use YAML as an intermediate format.

Karen: Would that workflow work for non-RDF data?  Because we are not limiting ourselves to RDF.  Can ShEx convert to YAML?

EricP: People have been trying to solve this for a long time.  Have not seen anyone succeed without basically coercing to some format.   XML people coerce to XML. JSON people coerce to JSON. RDF people coerce to RDF. But have never seen any schema language that addresses multiple representations without having a canonical representation.

Stefanie: I think the question is: Can I use this spreadsheet and convert it to an XML schema?

EricP: This is where the canonical representation comes up.  You have a lot of arbitrary choices: when it comes down to elements vs attributes, you end up prescribing a particular mapping.

Karen: We would have something that is documentation - as needed, transformable into code. What we do will not be code, but something transformable into code.

EricP: That is the UML approach.  Sit around whiteboard and draw boxes - then they say "that's the spec, and it's up to implementers to decide how to represent in XML".  It's easy to get to the spec, but then you do not have interoperability on the tooling.  One person's XML parser does not consume someone else's XML serialization.  

Karen: So if our document supported simple UML functionality, would that work for everyone?

Tom: One argument for having a YAML representation is that it could share the same model (and labels) as the spreadsheet template.  If we could declare Karen's model to be "done" (for now) -- a given -- and work out a spreadsheet template and a simple YAML format that would capture the contents of that spreadsheet template, we would have basis for taking into different directions in Hackathon.

Nishad: I like  https://github.com/kcoyle/RDF-AP/tree/master/csv because it wouldn't break RFC 4180.

Tom: Are mandatory IDs a barrier?

EricP: Does the ID only need to be locally unique?  Web-scale uniqueness is great for architecture but hard to implement.

Karen: Look at https://github.com/kcoyle/RDF-AP/blob/master/csv/statement.csv - using the name as the identifier.  This is the data.  We would need to develop a profile.  Then create more instance data that adheres to that profile.  JSON objects if you use the same identifier in multiple places.

Tom: Maybe we need a diagram (boxes) to show how Model relates to Profile, Profile to Data.

Karen: We need to name these things.  Will try to do a document that talks through these things.  I may set up a project for Seoul - so that we manage our time at Hack Day.

Nishad: Will there be recommendation of how to publish application profile?

Stefanie: Only sensible thing is to link from the instance data to the AP, not the opposite.  When you create an AP, do not know how it will be used.  We discussed this in the KIM context; Jana, Kai, and Lars worked on this.

EricP: When you say: I want to link this data to this schema, implies this is the only way the data will be used.  In ShEx world we keep separate and let people connect data with schema in a manifest.

Stefanie: Would love to have a way to hold people accountable.

Karen: Alot of people are working with government datasets - their data is "contained" as opposed to the uncontained data of RDF.  Different philosophies.  We should see which can be handled.  Should be optional.

ACTION: Karen and Nishad to collaborate on spreadsheet template and matching YAML format.

ACTION: Stefanie to explain KIM approach to linking from instance data to APs.
