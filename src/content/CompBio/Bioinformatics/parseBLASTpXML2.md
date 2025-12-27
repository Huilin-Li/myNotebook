# parse Blastp XML2 file

```
NS = {"n": "http://www.ncbi.nlm.nih.gov"}  # default namespace in your XML

def parse_blastxml2(path: str):
    tree = ET.parse(path)
    root = tree.getroot()

    records = []

    # Find each Search block
    for search in root.findall(".//n:Results/n:search/n:Search", NS):
        rec = {
            # "query_id": search.findtext("n:query-id", default="", namespaces=NS),
            "query_title": search.findtext("n:query-title", default="", namespaces=NS),
            "query_len": int(search.findtext("n:query-len", default="0", namespaces=NS)),
            "hits": []
        }

        for hit in search.findall("n:hits/n:Hit", NS):
            descr = hit.find("n:description/n:HitDescr", NS)

            taxid_text = descr.findtext("n:taxid", default="", namespaces=NS) if descr is not None else ""
            taxid = int(taxid_text) if taxid_text.isdigit() else None

            hit_obj = {
                "num": int(hit.findtext("n:num", default="0", namespaces=NS)),
                "accession": descr.findtext("n:accession", default="", namespaces=NS) if descr is not None else "",
                "id": descr.findtext("n:id", default="", namespaces=NS) if descr is not None else "",
                "title": descr.findtext("n:title", default="", namespaces=NS) if descr is not None else "",
                "taxid": taxid,
                "sciname": descr.findtext("n:sciname", default="", namespaces=NS) if descr is not None else "",
                "len": int(hit.findtext("n:len", default="0", namespaces=NS)),
                "hsps": []
            }

            for hsp in hit.findall("n:hsps/n:Hsp", NS):
                hit_obj["hsps"].append({
                    "num": int(hsp.findtext("n:num", default="0", namespaces=NS)),
                    "evalue": float(hsp.findtext("n:evalue", default="0", namespaces=NS)),
                    "bit_score": float(hsp.findtext("n:bit-score", default="0", namespaces=NS)),
                    "score": int(hsp.findtext("n:score", default="0", namespaces=NS)),
                    "identity": int(hsp.findtext("n:identity", default="0", namespaces=NS)),
                    "align_len": int(hsp.findtext("n:align-len", default="0", namespaces=NS)),
                    "query_from": int(hsp.findtext("n:query-from", default="0", namespaces=NS)),
                    "query_to": int(hsp.findtext("n:query-to", default="0", namespaces=NS)),
                    "hit_from": int(hsp.findtext("n:hit-from", default="0", namespaces=NS)),
                    "hit_to": int(hsp.findtext("n:hit-to", default="0", namespaces=NS)),
                    # optional huge strings:
                    # "qseq": hsp.findtext("n:qseq", default="", namespaces=NS),
                    # "hseq": hsp.findtext("n:hseq", default="", namespaces=NS),
                })

            rec["hits"].append(hit_obj)

        records.append(rec)

    return records


# Example usage
data = parse_blastxml2("./MYYZBU9W016-Alignment.xml")

for rec in data:
    print("Query:", rec["query_id"], rec["query_title"], "len=", rec["query_len"])
    for hit in rec["hits"][:1]:
        print("taxid=", hit["taxid"], "sciname=", hit["sciname"])


```