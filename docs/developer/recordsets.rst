.. _recordsets:

Record
======

Fims validation and upload is based around the concept of a `Record`. A `Record` is a single instance of an `Entity`.

A `Record` is typically a k:v map of properties. The key should be the columnUri. It is the responsibility of the `DataReader`
implementation to map any columnName -> columnUri when creating an instance of a `Record`.

Each type of `Record` will have a `RecordValidator` implementation that is responsible for handling the validation of 
that `Record` type. The default `Record` type is a `GenericRecord`. A `GenericRecord` is the most common in the fims 
system will be. The validation for a `GenericRecord` is strictly controlled by the project configuration w/o any additional
validation logic.

currently we have support for the following types:

* `GenericRecord`
* `FastaRecord`
* `FastqRecord`

Dataset
=======

A collection of `RecordSet` instances. If a `Dataset` has any `RecordSet`s for a child `Entity`, then the `Dataset` will contain the both the 
parent and child `RecordSet`s. The `DatasetBuilder` should be used to help construct a valid `Dataset` instance.

RecordSet
=========

A collection of `Record` instances.

Data Readers
------------

DataReader implementations contain the logic for reading and converting a specific file type into a RecordSet (TODO: more info about RecordSets).
When a file is uploaded for validation, it is passed to the `DataReaderFactory` which will return the appropriate
`DataReader` implementation for the provided file. A `DataReader` should return true when `handlesExtension` is called
if that reader can handle the provided ext.

A current limitation of DataReaders is that if multiple `DataReader` implementations handle the same file ext, only 1 can be enabled at a given time.
This restriction may be lifted in the future.

Entity
------

Custom entities can be created and must subclass the `Entity` class. All subclasses must exist in the `biocode.fims.digester` package to be properly
registered as a valid subtype for polymorphic serialization/deserialization via Jackson. An Entity subclass provides the ability to fix certain parts
of a given entity, as well as provide additional validation logic (to be executed on ProjectConfig updates) to ensure the entity is well formed 
and not missing any pertinant information.