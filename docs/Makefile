# Minimal makefile for Sphinx documentation

# You can set these variables from the command line.
SPHINXOPTS    =
SPHINXBUILD   = sphinx-build
SPHINXPROJ    = LightRAG
SOURCEDIR     = source
BUILDDIR      = build
APIDOCOUTDIR  = $(SOURCEDIR)/apis

# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

.PHONY: help Makefile

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

apidoc:
	@sphinx-apidoc -o $(APIDOCOUTDIR)/core ../lightrag/lightrag/core --separate --force
	@sphinx-apidoc -o $(APIDOCOUTDIR)/components ../lightrag/lightrag/components --separate --force --templatedir=$(SOURCEDIR)/_templates
	@sphinx-apidoc -o $(APIDOCOUTDIR)/eval ../lightrag/lightrag/eval --separate --force
	@sphinx-apidoc -o $(APIDOCOUTDIR)/optim ../lightrag/lightrag/optim --separate --force
	@sphinx-apidoc -o $(APIDOCOUTDIR)/utils ../lightrag/lightrag/utils --separate --force
	@sphinx-apidoc -o $(APIDOCOUTDIR)/tracing ../lightrag/lightrag/tracing --separate --force

# generate_autosummary:
# 	@echo "Generating autosummary files"
# 	@python $(SOURCEDIR)/generate_autosummary.py

update_files:
	@echo "Inserting reference labels into RST files."
	@python $(SOURCEDIR)/insert_labels.py
	@echo "Removing unnecessary strings for better formatting"
	@python $(SOURCEDIR)/remove_string.py
#@echo "Removing duplicated files"
# @python $(SOURCEDIR)/remove_files.py
	@echo "Renaming and updating file"
	@python $(SOURCEDIR)/change_api_file_name.py


html: apidoc  update_files
	@$(SPHINXBUILD) -b html "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)



# STEPS to make the components work
# 1. create autosummary but the update files would not work as it is run first and then the autosummary
# 2. distable the autosummary in conf.py
# 3. make file again to update the files
