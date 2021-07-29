.. Identifiers 

.. _biocode-fims-commons: https://github.com/biocodellc/biocode-fims-commons
.. _biocode-fims-fuseki: https://github.com/biocodellc/biocode-fims-fuseki
.. _biocode-fims-sequences: https://github.com/biocodellc/biocode-fims-sequences
.. _biscicol-fims: https://github.com/biocodellc/biscicol-fims
.. _fuseki: https://jena.apache.org/documentation/serving_data/
.. _`BiSciCol site`: http://www.biscicol.org/
.. _`GeOMe site`: http://www.geome-db.org/
.. _`GeOMe documentation`: https://www.geome-db.org/docs/helpDocumentation.pdf
.. _`NMNH FIMS documentation`: https://nmnh-fims.si.edu/fims/docs/FIMS-NMNH-Help_Master.pdf
.. _`BiSciCol FIMS installation`: http://biscicol.org/index.jsp
.. _`http://n2t.net/ark:/21547/R2MBIO56`: http://n2t.net/ark:/21547/R2MBIO56


User Guide to Creating Local Identifiers
========================================

A crucial part of the GEOME is converting local identifiers that you construct and use in your own research, and turning these into globally unique, resolvable identifiers.  Globally unique identifiers are created by appending your local identifier onto a unique root that is generated for every resource within every expedition.  Examples of locally unique identifiers are "Grinnell1213", "MooreaEvent2", or "MBIO56_1".  

Each identifier that is minted will be resolvable via HTTP using California Digital Library's Name-to-thing resolver.  Since the name-to-thing resolver is sensitive to certain characters, we have limited the characters that are suitable for use as local identifiers.  Allowable characters are validated on data load so if you choose an invalid character you will get an error message.   The following are the allowed local identifier characters:

  * A-Z
  * a-z
  * 0-9
  * + (plus)
  * = (equals)
  * : (colon)
  * . (period)
  * _ (underscore)
  * ( (open parantheses)
  * ) (close parantheses)
  * ~ (tilde)
  * \* (asterisk)

The following are valid identifiers:  "MVZ:Herp:1234", "Grinnell (1234)"

The following would be invalid identifiers:  "MVZ-Herp-1234", "Grinnell/Alexander 1234"

Once data is made loaded and made public, you can search for your newly minted globally unique and resolvable identifiers in the Query page, and they 
will be listed under the "BCID" column.  If the identifier is shown as ark:/21547/CSs2MBIO564 you can substitute http://n2t.net/ark: for the "ark:" to make a a resolvable identifier as https://n2t.net/ark:/21547/CXs2MBIO564, where MBIO564 is the locally uinque identifier.

