The Lemon API
=============

The lemon (Lexicon Model for Ontologies) API provides a programmatic interface for the lemon model. The lemon model is a model for describing lexica and their relationships to ontologies given in the OWL format. Lemon was designed with the following goals

* RDF-native
* Concise
* Descriptive not Prescriptive
* Modular
* Semantics by Reference

For more details of the lemon model see http://lemon-model.net

JavaDoc
-------

JavaDoc is available at http://monnetproject.github.com/lemon.api/

Usage Example
-------------

    final LemonSerializer serializer = LemonSerializer.newInstance();
    final LemonModel model = serializer.create();
    final Lexicon lexicon = model.addLexicon(
            URI.create("http://www.example.com/mylexicon"),
            "en" /*English*/);
    final LexicalEntry entry = LemonModels.addEntryToLexicon(
            lexicon,
            URI.create("http://www.example.com/mylexicon/cat"),
            "cat",
            URI.create("http://dbpedia.org/resource/Cat"));
    
    final LemonFactory factory = model.getFactory();
    final LexicalForm pluralForm = factory.makeForm();
    pluralForm.setWrittenRep(new Text("cats", "en"));
    final LinguisticOntology lingOnto = new LexInfo();
    pluralForm.addProperty(
            lingOnto.getProperty("number"),
            lingOnto.getPropertyValue("plural"));
    entry.addOtherForm(pluralForm);
    
    serializer.writeEntry(model, entry, lingOnto, 
            new OutputStreamWriter(System.out));
