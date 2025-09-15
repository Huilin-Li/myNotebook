# Chapter 4 The Taxonomy Project
> https://www.ncbi.nlm.nih.gov/books/NBK21100/

Each entry in the database is a “taxon”, also referred to as a “node” in the database. The “root node” (taxid1) is at the top of the hierarchy. 

The path from the root node to any other particular taxon in the database is called its “lineage”; the collection of all of the nodes beneath any particular taxon is called its “subtree”. 


> https://ftp.ncbi.nih.gov/pub/taxonomy/

- taxdump.tar.gz
- taxdump.tar.gz.md5

which contain MD5 sums for the corresponding archive files. These files might be used to check correctness of the download of corresponding archive file.

```
gunzip -c taxdump.tar.gz | tar xf - 

# PARSE nodes.dmp
def parse_nodes_dmp(nodes_dmp_fp):
    ROWS = []
    tax_col_names = [
            "tax_id",                           # node id in GenBank taxonomy database
            "parent_tax_id",                    # parent node id in GenBank taxonomy database
            "rank",                             # rank of this node (domain, kingdom, ...)
            "embl_code",                        # locus-name prefix; not unique
            "division_id",                      # see division.dmp file
            "inherited_div_flag",               # 1 if node inherits division from parent
            "genetic_code_id",                  # see gencode.dmp file
            "inherited_GC_flag",                # 1 if node inherits genetic code from parent
            "mitochondrial_genetic_code_id",    # see gencode.dmp file
            "inherited_MGC_flag",               # 1 if node inherits mitochondrial gencode from parent
            "GenBank_hidden_flag",              # 1 if name is suppressed in GenBank entry lineage
            "hidden_subtree_root_flag",         # 1 if this subtree has no sequence data yet
            "comments"                          # free text comments
            ]
    with open(nodes_dmp_fp, "r") as f:
        for line in f:
            cleaned = []
            for x in line.split("\t|"):
                x = x.strip()
                if x.isdigit():
                    cleaned.append(int(x))
                else:
                    cleaned.append(x)
            ROWS.append(cleaned[:-1])
        
    return pd.DataFrame(ROWS, columns=tax_col_names)


```

The content of the archive
--------------------------

It may look like this:

- citations.dmp
- delnodes.dmp
- images.dmp
- division.dmp
- gencode.dmp
- merged.dmp
- names.dmp
- nodes.dmp
- readme.txt

Each record consists of one or more fields delimited by "\t|\t" (tab, vertical bar, and tab) characters.

nodes.dmp
---------

This file represents taxonomy nodes. The description for each node includes 
the following fields:

	tax_id					-- node id in GenBank taxonomy database
 	parent tax_id				-- parent node id in GenBank taxonomy database
 	rank					-- rank of this node (domain, kingdom, ...) 
 	embl code				-- locus-name prefix; not unique
 	division id				-- see division.dmp file
 	inherited div flag  (1 or 0)		-- 1 if node inherits division from parent
 	genetic code id				-- see gencode.dmp file
 	inherited GC  flag  (1 or 0)		-- 1 if node inherits genetic code from parent
 	mitochondrial genetic code id		-- see gencode.dmp file
 	inherited MGC flag  (1 or 0)		-- 1 if node inherits mitochondrial gencode from parent
 	GenBank hidden flag (1 or 0)            -- 1 if name is suppressed in GenBank entry lineage
 	hidden subtree root flag (1 or 0)       -- 1 if this subtree has no sequence data yet
 	comments				-- free-text comments and citations

names.dmp
---------
Taxonomy names file has these fields:

	tax_id					-- the id of node associated with this name
	name_txt				-- name itself
	unique name				-- the unique variant of this name if name not unique
	name class				-- (synonym, common name, ...)

division.dmp
------------
Divisions file has these fields:
	division id				-- taxonomy database division id
	division cde				-- GenBank division code (three characters, e.g. BCT, PLN, VRT, MAM, etc.)
	division name				-- e.g. Bacteria, Plants and Fungi, Vertebrates, Mammals, etc.
	comments

gencode.dmp
-----------
Genetic codes file:

	genetic code id				-- GenBank genetic code id
	abbreviation				-- genetic code name abbreviation
	name					-- genetic code name
	cde					-- translation table for this genetic code
	starts					-- start codons for this genetic code

delnodes.dmp
------------
Deleted nodes (nodes that existed but were deleted) file field:

	tax_id					-- deleted node id

merged.dmp
----------
Merged nodes file fields:

	old_tax_id                              -- id of nodes which has been merged
	new_tax_id                              -- id of nodes which is result of merging

citations.dmp
-------------
Citations file fields:

	cit_id					-- the unique id of citation
	cit_key					-- citation key
        medline_id                              -- unique id in MedLine database (0 if not in MedLine)
	pubmed_id				-- unique id in PubMed database (0 if not in PubMed)
	url					-- URL associated with citation
	text					-- any text (usually article name and authors)
						-- The following characters are escaped in this text by a backslash:
						-- newline (appear as "\n"),
						-- tab character ("\t"),
						-- double quotes ('\"'),
						-- backslash character ("\\").
	taxid_list				-- list of node ids separated by a single space

Organism images file (images.dmp):
---------------------------------
	image_id				-- the unique id of image
	image_key				-- image key
	url					-- image URL associated with citation
	license					-- image license
	attribution				-- image attribution
	source					-- source of the image
	properties				-- various image properties separated by semicolon
	taxid_list				-- list of node ids separated by a single space
