
%.pdf: %.tex $(wildcard fig/*) $(wildcard *.bib) $(wildcard *.sty) ../data_collection/results.csv
	xelatex -shell-escape -interaction=nonstopmode $*

all: poster.pdf
