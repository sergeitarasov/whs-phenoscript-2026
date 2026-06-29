
# Annotation Guide

## Introduction

This guide explains the best practice to write phenotypic statements in Phenoscript. Phenoscript uses Entity-Quality (EQ) syntax as the foundation for all phenotypic statements, allowing precise description of morphological traits through ontologies. This approach builds upon previous standardized frameworks, such as those documented in the [Phenoscape Character Annotation Guide](https://wiki.phenoscape.org/wiki/Guide_to_Character_Annotation). It provides explanation of main character patterns and how to use positional and anatomical terminology in the most proper and consistent way.

-------------

Descriptions involve three major ontology objects:

- **entity**: something that exists and can be referred to as a distinct thing. In Phenoscript we can use both material (*e.g.*, the protibia, the anterior region) or immaterial (*e.g.*, an anatomical line, a body axis).

- **quality**: describes an intrinsic feature of an entity (*e.g.*, red, curved, length, diameter, presence). Qualities are of two types: 

  - ***value***: observable values like "red" or "diameter", typically associated with an entity via `has_characteristic` (=`bearer_of`);
  - ***relational quality***: qualities that express a relationship between two entities, such as "distal to" or "fused with";

- **relationship**: defines relationships between an entity and a quality or another entity (*e.g.*, `part_of`, `has_characteristic`, `encircles`). Different relationships are used to describe how qualities associate with entities.

--------------------------------------------------------------

The main strategy is to identify the specific anatomical structure on the insect body that you want to describe, and then assign the appropriate quality or characteristic to it. 

Phenotypic statements are built as **triplets** (or combinations of triplets) connecting an entity to another entity or a quality through a relationship. At minimum, Phenoscript requires composition involving at least two entities forming complete statements:

- **Simple composition**: `this > aism-protibia;` (stating that protibia is part of the organism)

```mermaid
graph LR
    A["this"] -- .bfo-has_part --> B["aism-protibia"]
    linkStyle default stroke:#0077be
```

- **Composition with quality**: `this > protibia >> pato-present;` (stating that the protibia is present as part of the organism)

```mermaid
graph LR
    A["this"] -- .bfo-has_part --> B["aism-protibia"]
    B -- .ro-has_characteristic --> C["pato-present"]
    linkStyle default stroke:#0077be
```

- **Complete EQ statement**: `this > protibia >> pato-red;` (stating that the protibia is red)

```mermaid
graph LR
    A["this"] -- .bfo-has_part --> B["aism-protibia"]
    B -- .ro-has_characteristic --> C["pato-red"]
    linkStyle default stroke:#0077be
```

--------------------------------------------------------------

## Syntax and notation

| Element | Description | Example |
|---------|-------------|----------|
| **Entity** | Objects written with an ontology prefix | `aism-protibia`, `bspo-anatomical_line` |
| **Quality** | Characteristics written with ontology prefix | `pato-red`, `pato-length` |
| **Relationship** | Written with a period prefix and ontology prefix | `.ro-adjacent_to`, `.phs-has_element_count` |
| **Statement closure** | Each statement must end with a semicolon | `aism-protibia .ro-has_characteristic pato-red;` |

The prefixes are provided automatically by the snippets in the dropdown menu, so you don't need to remember them!

--------------------------------------------------------------

Don't forget that the described organism, to which all statements refer, can be referred to as `this`. For example, to say that the insect is red, you can simply write:

`this .ro-has_characteristic pato-red;`


Moreover, if you want to mention the same individual structure (*e.g.*, exactly the same protibia) more than once within your description, you need to label it with a unique hexadecimal id-tag (generated automatically through the snippets dropdown menu by starting to type ":id" and pressing enter). You will need to use this tag every time you are referring to that same structure throughout the description. For example:

```py
# Head red and with antenna
this > aism-insect_head:id-1954fa .ro-has_characteristic pato-red;
aism-insect_head:id-1954fa .bfo-has_part aism-antenna;
```

After tagging a structure, you do not need to state again that the structure belongs to `this` in the following statements about it, as its existence was already declared once.

-------------------

Moreover, if multiple entities or qualities have an identical relationship with an entity, parentheses can be used to write a single statements instead of multiple ones:

```py
# Head red, microreticulate, flattened
this > aism-insect_head >> (pato-red, aism-microreticulate, pato-flattened);
```

instead of 

```py
# Head red, microreticulate, flattened
this > aism-insect_head:id-cd39ea >> pato-red;
  aism-insect_head:id-cd39ea >> aism-microreticulate;
  aism-insect_head:id-cd39ea >> pato-flattened;
```


## Making Entities

### Positional terminology

Positional terms must consistently refer to the main insect body axes and not the relative axis of each structure.

<img src="https://raw.githubusercontent.com/sergeitarasov/phenoscript-workshop-incol-2026/main/images/position_1.jpg" alt="Position 1" width="700" />

In some cases, the positional conventions adopted in the anatomy ontologies (and therefore in Phenoscript) may be counterintuitive for taxonomists used to traditional taxon-specific terms. For example, in some Coleoptera, legs are variously rotated around their proximo-distal axis, which led traditional family-specific terminology not to reflect the true correspondence between leg regions across all Coleoptera, *e.g.*, calling "lateral" the protibial teeth of some scarabeoid beetles which are in fact on the dorsal region of the protibia (see image below). However, in order to guarantee a consistent description of morphology across different insect families and orders the anatomically consistent positional conventions used in the ontologies must be utilized.

<img src="https://raw.githubusercontent.com/sergeitarasov/phenoscript-workshop-incol-2026/main/images/position_2.jpg" alt="Position 2" width="700" />


#### Spatial terms for main body parts:
- anterior region/margin
- posterior region/margin
- lateral
- medial
- dorsal 
- ventral

And their combinations: antero-lateral, antero-medial region/margin, etc.

#### Spatial terms for appendages:
- anterior region/margin
- posterior region/margin
- dorsal 
- ventral
- proximal 
- distal

And their combinations: antero-proximal region/margin, etc.

***Important:*** Do not use alternative terms such as basal or apical.

### Composition rules

Most anatomical entities are postcompositional, *i.e.*, frequently require combining spatial terms from the Biospatial Ontology (BSPO) to create precise descriptions of body structures.

Each anatomical entity should be composed with **at most one spatial term** to describe a region or margin:

***Correct:***
```py
# Anterior region of head is red
insect_head > anterior_region >> red;
aism-protibia > bspo-antero-lateral_region >> red;
```

***Incorrect*** **(avoid stacking spatial terms):**
```py
# Anterior region of head is red
insect_head > anterior_region > lateral_region >> red;
```

Descriptions should try to maximize the use of general insect anatomical terms and combine (post-compose) them in the descriptions to characterize specific structures. For example:

***Correct***
```py
# Protibia with spur
this > aism-protibia > aism-cuticular_spur;
```

***Incorrect***
```py
# Protibia with spur
this > aism-protibial_spur;
```

Similarly:

***Correct***
```py
# Abdomen with 7 sternites
this > aism-abdominal_sternite .has_element_count 7;
```

***Incorrect***
```py
# Abdomen with 7 sternites
this > aism-abdomen_with_7_sternites;
```


## Main types of phenotypic statement

### 1. `has_part` and `part_of`

The property `has_part` (alias: **\>**) is used to state that an **entity** is part of another **entity**:

```py
# Organism has head
this > aism-insect_head;
```

The reverse property is `part_of` (alias: **<**), which, however, should not be used unless strictly necessary to avoid a more difficultly intelligible rendering of the natural translation of the text.

```py
# Head is part of organism
aism-insect_head < this;
```


### 2. `has_characteristic` and `inheres_in`

The relationship `has_characteristic` (alias: **>>**) is used to state that an **entity** is characterised by some **quality**:

```py
# Head is red
this > aism-insect_head >> pato-red;
```

The reverse relationship `inheres_in` (alias: **<<**), which should also not be used unless strictly necessary to avoid a more difficultly intelligible rendering of the natural translation of the text.

```py
# Red inheres in head
pato-red << aism-insect_head < this;
```


### 3. `encircles` and `encircled_by`

The relationship `encircles` (alias: **->**) is used instead of has part when referring to ring sclerites that are connected to other ring sclerites via a conjunctiva. Common cases in species descriptions are **appendage sclerites** (tarsus, tibia, femur, antennomeres, etc.), as well as **setae**, which technically are separate sclerites articulated to other sclerites. For example:

```py
# Protibia with seta
this > aism-protibia -> aism-cuticular_seta;
```

The reverse relationship is `encircled_by` (alias: **<-**), which should also not be used unless strictly necessary to avoid a more difficultly intelligible rendering of the natural translation of the text.

```py
# Seta is encircled by protibia
aism-cuticular_seta <- aism-protibia < this;
```


### 4. Presence and absence

The `has_part` property implies that the object entity is present. However, the presence or absence of a structure can also be stated explicitly by using the qualities `present` or `absent`. For example:

```py
# Antenna present
this > aism-antenna >> pato-present;
```
Or

```py
# Antenna absent
this > aism-antenna >> pato-absent;
```

We may also state the absence of a structure by saying that an entity does **not have part** another entity, which can be done by negating `has_part`. The same is possible for `encircles`.

```py
# Antenna absent
this !> aism-antenna;
```

```py
# Seta absent
aism-protibia !-> aism-cuticular-seta;
```


### 5. Relative comparison

The relative comparison pattern is used to compare the extents of two qualities, *i.e.*, if one is **larger than** or **smaller than** another. For this, we use the relationships `increased_in_magnitude_relative_to` (alias: **|>|**) and `decreased_in_magnitude_relative_to` (alias: **|<|**), respectively. It is expressed in the form:

`'E1' >> 'Q1' |>| 'E2' >> 'Q2'` (larger than) 
And
`'E1' >> 'Q1' |>| 'E2' >> 'Q2'` (smaller than)

The pattern can be generated automatically from the snippets by typing the **tmp** command and selecting it from the dropdown menu, then filling the different elements with the relevant entities and qualities. For example:

```py
# Protibia longer than protarsus
this > aism-protibia >> pato-length |>| pato-length << aism-protarsus < this;
```

literally meaning "length of the protibia is larger than length of the protarsus".


### 6. Relative measurements

The relative measurement pattern allows you to measure the quality of an entity using the quality of another entity as the measurement unit. The pattern can be generated automatically as a YAML block from the snippets dropdown menu by typing **tmp**, and it is expressed in the form:

```py
    relative_measurement:
      .measured_trait:
        .entity: 'E1'
        .quality: 'Q1'
      .unit:
        .entity: 'E2'
        .quality: 'Q2'
      .value: 'Val'
```

 For example, to say that the length of the protibia is 3 times the length of the protarsus:

```py
    # Protibia 3 times as long as protarsus
    #>>>YAML relative_measurement
    relative_measurement:
      .measured_trait:
        .entity: aism-protibia:id-010498
        .quality: pato-length
      .unit:
        .entity: aism-protarsus:id-538e56
        .quality: pato-length
      .value: 3
    #<<<YAML
```


### 7. Absolute measurements

The absolute measurement pattern allows you to provide a measurement value of a quality using standard measurement units (length, volume, mass, etc.). It is also generated automatically from the snippets dropdown menu by typing **tmp** and it is expressed in the form:

```py
    absolute_measurement:
        .measured_entity: 'E'
        .measured_quality: 'Q'
        .value: 'Val'
        .unit: 'Unit'
```

For example, to say that the body length of an insect is 21.5 mm:

```py
    # Body length: 21.5 mm
    #>>>YAML absolute_measurement
    absolute_measurement:
        .measured_entity: this
        .measured_quality: pato-length
        .value: 21.5
        .unit: unit-millimeter
    #<<<\YAML
```

### 8. Element count

For structures occurring in series, you may want to state their exact number. This can be done with the `has_element_count` relationship. For example:

```py
# Protarsus with 5 protarsomeres
this > aism-protarsus > aism-protarsomere .phs-has_element_count 5;
```

### 9. Comparison between different organisms

You may want to compare traits of an organism with that of another organism. To do this, you must have the descriptions of the two organisms within the same file and use the `exclude` command. 

For example, to say that the protibia of *Scarabaeus viettei* is shorter than protibia of *Scarabaeus sakalava*:

```py
OTU = { # Scarabaeus viettei

  DATA = {
    #>>>YAML described_species
      described_species:
         .id: scarabaeus_viettei #OTU ID
         .rdfs-label: 'Scarabaeus viettei'
         .gbif_id: 'https://www.gbif.org/species/4997091'
         .dwc-Catalog_Number:
              - 'http://id.luomus.fi/GZ.15821'
          .is_a:
              - uberon-male_organism
              - uberon-adult_organism
              - dwc-Preserved_Specimen
      #<<<YAML
  }

  TRAITS = {
    
    # Protibia shorter than in Scarabaeus sakalava
    this > aism-protibia >> pato-length:id-111111 |<| pato-length:id-222222[exclude = TRUE];
  }
}

OTU = { # Scarabaeus sakalava

  DATA = { 
    #>>>YAML described_species
    described_species:
        .id: scarabaeus_sakalava #OTU ID
        .rdfs-label: 'Scarabaeus sakalava'
        .gbif_id: 'http://zoobank.org/7AD8F87F-E7C1-4094-BD63-7662F167E9CB'
        .dwc-Catalog_Number:
            - 'http://id.luomus.fi/GZ.15827'
        .is_a:
            - uberon-male_organism
            - uberon-adult_organism
            - dwc-Preserved_Specimen
    #<<<YAML
  }

  TRAITS = {
    
    # Protibia longer than in Scarabaeus viettei
    this > aism-protibia >> pato-length:id-222222 |>| pato-length:id-111111[exclude = TRUE];
  }
}
```

You can refer to the OTU (=`male_organism`) within another OTU's description by using the OTU `.id` found in the data block (*e.g.*, `scarabaeus_viettei`, `scarabaeus_sakalava`). 



### 10. Other useful statements

Other relationships and qualities useful in species descriptions:

***Example 1***. To say that the head has a cuticular groove along its posterior margin, you can use the relationship `coincident_with`:

```py
# Head grooved along posterior margin
this > aism-insect_head:id-56cc72 > aism-cuticular_groove .ro-coincident_with bspo-posterior_margin < aism-insect_head:id-56cc72;
```

-------------

***Example 2***. To say that a cuticular_tubercle is placed medially (=closer to the sagittal plane) with respect to the eye, you will use the `medial_to` (make sure to use the object relationship `aism-medial_to` and not the quality `pato-medial_to`!):

```py
# Head with tubercle placed medially to eye
this > aism-insect_head:id-2094bf > aism-cuticular_tubercle .aism-medial_to aism-eye_cuticle < aism-insect_head:id-2094bf;
```

-------------

***Example 3***. If you want to say that the protibial spur is fused with the protibia, you will need to use both the **relational quality** `fused_with` and the **relationship** `towards`:

```py
# Protibial spur fused with protibia
this > aism-protibia:id-296644 > aism-cuticular_spur pato-fused_with:id-748ca8 .ro-towards aism-protibia:id-296644;
```

You may then want to specify the degree of fusion of the spur to the tibia (for example, completely/strongly fused). In this case, the quality `fused_to` is further specified as `increased_magnitude` through the relationship `has_modifier`:

```py
# Protibia and spur completely fused
pato-fused_with:id-748ca8 .ro-has_modifier pato-increased_magnitude;
```
## Body regions and margins

To describe specific parts of an anatomical structure, the term "region" (`bspo-anatomical_region` and its derivatives) must be used. Do not use `anatomical_side`, `anatomical_surface`, or other variants. Similarly, the term "margin" (`bspo-anatomical_margin` and its derivatives) must be used to refer to the flat surface that delimit the boundary of a surface. Do not use `anatomical_boundary` or other variants.

All combinations of positional terms referred to anatomical region and margin are present in the ontologies (*e.g.*, `ventro-distal_region`, `dorso-medial_margin`, etc.). Once again, remember **not to postcompose regions nor margins**.

## Punctuation and setation

In taxonomic descriptions, it is often needed to describe traits referring to the presence of an unspecified number of structures of the same kind, like punctuation, setation, etc. While the simplest way could be using qualities such as `punctate` or `setose`, these terms do not allow to characterize punctures and setae in further detail. For this reason, it is recommended to use `anatomical_collection` and, for a linear assemblage of structures, its derivative `anatomical_row`. The property `has_member` must be used when assigning entities to an anatomical collection.

***Example 1***:

```py
# Head with simple setigerous punctures
this > aism-insect_head > uberon-anatomical_collection .has_member aism-simple_setigerous_cuticular_puncture;
```

***Example 2***:
```py
#Posterior margin of head with a row of setae
this > aism-insect_head > bspo-posterior_margin > uberon-anatomical_row .has_member aism-cuticular_seta;
```

## Numbering of serial structures

Some structures with the same developmental origin are often present in series, for example cuticular spines, cuticular teeth or setae on some body margin.

If you are not interested in describing specifically single elements within the series, `has_element_count` or `uberon-anatomical_collection` will suffice (see above). However, if you want to further specify some characteristics of single serial elements, you need to refer to their relative position within the series using the `aism-serial_position_id_X` **quality**. 

***Example 1***:

```py
# Dorsal margin of protibia with 4 cuticular teeth
this > aism-protibia > bspo-dorsal_margin > aism-cuticular_tooth >> aism-serial_position_id_1;
this > aism-protibia > bspo-dorsal_margin > aism-cuticular_tooth >> aism-serial_position_id_2;
this > aism-protibia > bspo-dorsal_margin > aism-cuticular_tooth >> aism-serial_position_id_3;
this > aism-protibia > bspo-dorsal_margin > aism-cuticular_tooth >> aism-serial_position_id_4;
```

<img src="https://github.com/sergeitarasov/phenoscript-workshop-incol-2026/blob/main/images/protibia.jpg?raw=true" alt="Protibia" width="500" />

--------------

If the series of structures is present in two specular copies on the left and right body sides, it is not necessary to state the presence of both left and right copies. The structure must simply be qualified as `pato-bilaterally_paired`:

***Example 2***. Anterior clypeal margin with two pairs of specular teeth:

```py
# Anterior clypeal margin with four teeth
this > aism-clypeus > bspo-anterior_margin > aism-cuticular_tooth >> (aism-serial_position_id_1, pato-bilaterally_paired);
this > aism-clypeus > bspo-anterior_margin > aism-cuticular_tooth >> (aism-serial_position_id_2, pato-bilaterally_paired);
```

<img src="https://github.com/sergeitarasov/phenoscript-workshop-incol-2026/blob/main/images/teeth.jpg?raw=true" alt="Head Scarabaeus1" width="500" />

The position of each tooth relative to the others, useful to describe the order in which the elements are set, can be further specified later. For example, if, on each side, tooth 1 is medial to tooth 2: 

```py
# Anterior clypeal margin with 4 teeth, teeth 1 medial to teeth 2
this > aism-clypeus > bspo-anterior_margin > aism-cuticular_tooth:id-9e09d9 >> (aism-serial_position_id_1, pato-bilaterally_paired);
this > aism-clypeus > bspo-anterior_margin > aism-cuticular_tooth:id-1f5b66 >> (aism-serial_position_id_2, pato-bilaterally_paired);
aism-cuticular_tooth:id-9e09d9 .aism-medial_to aism-cuticular_tooth:id-1f5b66;
```

In the case of a single medial tooth, the quality `unpaired` must be specified and you do not need to number it:

```py
# Anterior clypeal margin with a single tooth
this > aism-clypeus > bspo-anterior_margin > aism-cuticular_tooth >> pato-unpaired;
```

<img src="https://github.com/sergeitarasov/phenoscript-workshop-incol-2026/blob/main/images/head_Scarabaeus.jpg?raw=true" alt="Head Scarabaeus2" width="500" />

The chosen order of numbering (what element has `id_1` and so on) will depend on conventions used within each taxon, which should be adopted consistently among authors describing species within that group.

***Note.*** In Coleoptera, elytral striae are also repeated structures with the same developmental origin; however, specific numbered terms are present for them and shall be used instead of serial position ids (*e.g.*, `colao-elytral_stria_1`, `colao-elytral_interstria_2`).

## Antennomeres

Antennomeres comprise scapus, pedicellus and flagellomeres:

<img src="https://github.com/sergeitarasov/phenoscript-workshop-incol-2026/blob/main/images/antenna.jpg?raw=true" alt="Antenna" width="500" />

## Useful shape qualities

Useful qualities that may be recurrent in the description of shapes are:

- `angular`: used to describe a convexly angular margin. The type of angle can be further specified in its derivatives such as `acutely_angular`, `obtusely_angular` and `right-angled`;
- `notched`: used to describe a concavely angular margin. The type of notch can be further specified in its derivatives such as `acutely_notched`, `obtusely_notched`, `right-angled_notched` and `emarginate`.

<img src="https://github.com/sergeitarasov/phenoscript-workshop-incol-2026/blob/main/images/angular.jpg?raw=true" alt="Head Scarabaeus3" width="500" />

# Limitations

Phenoscript allows the description of a broad variety of phenotypic traits. However, the shape of some structures is notoriously difficult to capture even with natural language, for example some complex colour patterns or genital traits. In such cases, we suggest that the best solution is to avoid writing Phenoscript statement that may prove to be very difficult to craft and understand. Instead, complementing the taxonomic description with a self-explanatory picture of the structure is probably a much more effective solution. However, Phenoscript is constantly under development and the description of very complex structures may be easier in the future upon definition of additional ontology classes and tested descriptive patterns.

