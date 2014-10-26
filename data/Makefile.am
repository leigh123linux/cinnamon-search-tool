icondir = $(datadir)/pixmaps/csearchtool
icon_DATA = thumbnail_frame.png 

man_MANS = cinnamon-search-tool.1

@INTLTOOL_SCHEMAS_RULE@
@INTLTOOL_XML_NOMERGE_RULE@

gsettings_SCHEMAS = org.cinnamon.cinnamon-search-tool.gschema.xml
@GSETTINGS_RULES@

gsettingsconvertdir = $(datadir)/GConf/gsettings
gsettingsconvert_DATA = cinnamon-search-tool.convert

Utilitiesdir = $(datadir)/applications
Utilities_in_files = cinnamon-search-tool.desktop.in 
Utilities_DATA = $(Utilities_in_files:.desktop.in=.desktop)
@INTLTOOL_DESKTOP_RULE@

EXTRA_DIST = \
	$(icon_DATA) \
	$(man_MANS) \
	org.cinnamon.cinnamon-search-tool.gschema.xml.in \
	$(Utilities_in_files) \
	$(Utilities_DATA) \
	cinnamon-search-tool.convert

CLEANFILES = 				\
	cinnamon-search-tool.desktop	\
	$(gsettings_SCHEMAS)

disthook:
	cd $(distdir) ; rm -f $(CLEANFILES)
