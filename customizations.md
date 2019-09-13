This page outlines in summary form changes made to the standard TEI usage of elements and attributes, and new elements and attributes created for this ODD.

# Modified elements
- `<collation>` has a new attribute `@mainStructures`, to record the most frequently occuring quire structure(s)
- `<foliation>` can have att.datable attributes
- `<signatures>` can have the `@type` attribute to distinguish leaf and quire signatures
- `<layout>` has two new attributes:
  - `@topLine`, specifies whether the mise-en-page is above top line, below top line, or mixed
  - `@rulingMedium` specifies the medium (ink, leadpoint, hardpoint, etc.) used to carry out the ruling


# New elements
- `<countermark>` element added for description of countermarks
