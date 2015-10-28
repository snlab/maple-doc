
## Optimizing MapleCore and Generating Efficient FT rules

Currently, MapleCore uses a straintforward yet naive approach to generating FT rules. Optimizations can be applied to

* utilize multi-tables.
    (Compressed TT) https://github.com/snlab/maple-doc/blob/master/design/maplecore/multitable-from-compressed-TT-v2.pdf
    (Annotation) https://en.m.wikipedia.org/wiki/Java_annotation
    (Magellan)

* reduce the number of rules generated.
    http://conferences.sigcomm.org/sigcomm/2013/papers/sigcomm/p87.pdf

* reduce the number of priorities.
    Reducing the number of priorities assigned to rules benefits TCAM-based switches. However, I'm not sure if this conclusion is true for latest SDN data planes (such as chipsets from Broadcom).

