# BioDATEN-Minimalschema

**This is work in progress**


The *BioDATEN Metadata-schema* is work in progress. The design rational can be
found in the doc directory.

- **Construction:**

The schema is being constructed with the help of the CLARIN Component Registry (CCR),
see https://catalog.clarin.eu/ds/ComponentRegistry/#/browser.

At the time of writing, it is a private schema *BioDatenMinimal* being defined
by the user *nalida*. It consists of the main components *Study*, *Experiment*,
*Sample*, *Environment*, *Run*, and *Data*.

When the XSD is exported from the CCR, we manually remove occurrences of

- xml:base
- cmd:ref attributes.

Note that components have an attribute cmd:ComponentId which is a value that is
always fixed to a component's identifier. This is needed for the validation of
the schema. It should not be offered to users filling out the schema.
