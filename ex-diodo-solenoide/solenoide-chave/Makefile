all: $(patsubst %.tex, %.svg, $(wildcard *.tex))

%.svg: %.pdf
	pdftocairo -svg $< $@

%.pdf: %.tex
	lualatex --synctex=1 $<
