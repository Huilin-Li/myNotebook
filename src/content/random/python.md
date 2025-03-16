## Assign files into different folders
Assuming I have 230 files in `db_folder`, and I want to copy these 230 files into different folders (`folder0`, `folder1` and so on) with at least 50 files in each folder.

`files_list` contains names of these 230 files, like `files_list=["file1", "file2", ..., "file230"]`
```python
import shutil
chunks = [files_list[x:x+50] for x in range(0, len(files_list), 50)]
# len(chunks) = 5

for i in range(53):
    chunk = chunks[i]
    newpath = "db_folder/folder" + str(i)
    if not os.path.exists(newpath):
        os.makedirs(newpath)

    for j in chunk:
        src = "db_folder/" + j
        dst = "db_folder/folder" + str(i) + "/" + j
        shutil.copyfile(src, dst)
```

## Copy files to a new folder
```python
import shutil
for i in files_list:
    src = "old_folder/" + i
    dst = "new_folder/" + i
    shutil.copyfile(src, dst)
```

## Remove legend in Plotly
```python
fig.update_layout(showlegend=False)
```


## unzip compressed files into a new directory
```python
gz_file = os.path.join(root, file)
out_file = "new_path/" + file
with gzip.open(gz_file,"rb") as f_in, open(out_file,"wb") as f_out:
    shutil.copyfileobj(f_in, f_out)
```

## copy and move 
```python
import shutil
shutil.copyfile("old_path/file.txt", "new_path/file.txt")
```