# sequence similarity

## `import parasail`
```python
# 1
result = parasail.sw_trace_scan_16("asdf", "asdf", 11, 1, parasail.blosum62)

# 2
edlib.align(x, y, mode='HW', task='locations', k=max_dist + 1) # edit distance

```