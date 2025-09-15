# parse JSON from foldseek search server
> https://search.foldseek.com/search

```python
import json, glob, os
from pprint import pprint
import pandas as pd


json_folder = "/storage/shenhuaizhongLab/lihuilin/A_piezo/2_StructureSearch/1_foldseekOnline/"
json_files = glob.glob(os.path.join(json_folder, "*.json")) 
# print(json_files)


queries_header_list = []
queries_seq_list = []
db_list = []
target_list = []
prob_list = []
e_val_list = []
score_list = []
qStartPos_list = []
qEndPos_list = []
qLen_list = []
dbLen_list = []
qAln_list = []
dbAln_list = []
tSeq_list = []
taxId_list = []
taxName_list = []
description_list = []
href_list = []


for json_fp in json_files:
    with open(json_fp) as f:
        json_d = json.load(f)
        #print(json_d[0].keys())
        queries_header = json_d[0]["queries"][0]["header"]
        queries_seq = json_d[0]["queries"][0]["sequence"]
        mode = json_d[0]["mode"]
        # print(json_fp,"###",queries_header, "###",mode)
        print("###",queries_header, "###",mode)
        res = json_d[0]["results"]
        for i in range(9):
            db = res[i]["db"]
            alignments_count = len(res[i]["alignments"])
            # print(db, len(res[i]["alignments"]))
            if alignments_count == 0:
                pass
            else:
                for j in range(alignments_count):
                    target = res[i]["alignments"][str(j)][0]["target"]
                    prob = res[i]["alignments"][str(j)][0]["prob"]
                    e_val = res[i]["alignments"][str(j)][0]["eval"]
                    score = res[i]["alignments"][str(j)][0]["score"]
                    qStartPos = res[i]["alignments"][str(j)][0]["qStartPos"]
                    qEndPos = res[i]["alignments"][str(j)][0]["qEndPos"]
                    qLen = res[i]["alignments"][str(j)][0]["qLen"]
                    dbLen = res[i]["alignments"][str(j)][0]["dbLen"]
                    qAln = res[i]["alignments"][str(j)][0]["qAln"]
                    dbAln = res[i]["alignments"][str(j)][0]["dbAln"]
                    tSeq = res[i]["alignments"][str(j)][0]["tSeq"]
                    taxId = res[i]["alignments"][str(j)][0].get("taxId", "None")
                    taxName = res[i]["alignments"][str(j)][0].get("taxName", "None")
                    description = res[i]["alignments"][str(j)][0].get("description", "None")
                    href = res[i]["alignments"][str(j)][0]["href"]

                    queries_header_list.append(queries_header)
                    queries_seq_list.append(queries_seq)
                    db_list.append(db)
                    target_list.append(target)
                    prob_list.append(prob)
                    e_val_list.append(e_val)
                    score_list.append(score)
                    qStartPos_list.append(qStartPos)
                    qEndPos_list.append(qEndPos)
                    qLen_list.append(qLen)
                    dbLen_list.append(dbLen)
                    qAln_list.append(qAln)
                    dbAln_list.append(dbAln)
                    tSeq_list.append(tSeq)
                    taxId_list.append(taxId)
                    taxName_list.append(taxName)
                    description_list.append(description)
                    href_list.append(href)



       

df = pd.DataFrame({
    "queries_header": queries_header_list,
    "queries_seq": queries_seq_list,
    "db": db_list,
    "target": target_list,
    "prob": prob_list,
    "e_val": e_val_list,
    "score": score_list,
    "qStartPos": qStartPos_list,
    "qEndPos": qEndPos_list,
    "qLen": qLen_list,
    "dbLen": dbLen_list,
    "qAln": qAln_list,
    "dbAln": dbAln_list,
    "tSeq": tSeq_list,
    "taxId": taxId_list,
    "taxName": taxName_list,
    "description": description_list,
    "href": href_list
})


#df.to_csv("/storage/shenhuaizhongLab/lihuilin/A_piezo/2_StructureSearch/1_foldseekOnline/foldseekOnlineStructure_result.csv", index=False)


```