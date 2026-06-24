CONFIG = phs-config.yaml

AISM_URL  = https://raw.githubusercontent.com/sergeitarasov/aism/devel/src/ontology/aism-edit.owl
# BSPO_URL  = https://raw.githubusercontent.com/sergeitarasov/biological-spatial-ontology/add-new-terms-clean/src/ontology/bspo-edit.owl

AISM_ORI  = owl-original/aism-edit.owl
BSPO_ORI  = owl-original/bspo-edit.owl

AISM_XML  = owl-xml/aism-edit.owl
BSPO_XML  = owl-xml/bspo-edit.owl

.PHONY: all download convert commit snips

all: download convert commit snips


# 1. Download ontologies into owl-original/ (always re-downloads)
download:
	curl -L $(AISM_URL) -o $(AISM_ORI)
#	curl -L $(BSPO_URL) -o $(BSPO_ORI)

# 2. Convert functional-syntax OWL → RDF/XML into owl-xml/
convert: $(AISM_XML) $(BSPO_XML)

$(AISM_XML): $(AISM_ORI)
	robot convert --input $< --format owl --output $@

$(BSPO_XML): $(BSPO_ORI)
	robot convert --input $< --format owl --output $@

# 3. Commit changes to GitHub
commit:
	git -C .. add make-snippets/owl-original/ make-snippets/owl-xml/
	git -C .. diff --cached --quiet || git -C .. commit -m "makefile: Update ontology files"
	git -C .. push

# 4. Generate snippets
snips:
	phenospy make-snips $(CONFIG)
