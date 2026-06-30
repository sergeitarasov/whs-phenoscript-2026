DIAGRAMS = $(patsubst img/%.mmd, img/%.svg, $(wildcard img/*.mmd))

.PHONY: all diagrams

all: diagrams

diagrams: $(DIAGRAMS)

img/%.svg: img/%.mmd
	mmdc -i $< -o $@
