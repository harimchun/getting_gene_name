# getting_gene_name
Collect the Genes' Name referring to the dbSNP
```python
from urllib.request import urlopen

ID = []
with open('C:/Users/bgr16/Desktop/Rosalind/snps.txt') as f:
    for line in f:
        snp = line[2:]
        ID.append(snp.strip())

print(ID)
Gene_table = []

for i in ID:
    URL = 'https://api.ncbi.nlm.nih.gov/variation/v0/beta/refsnp/' + i
    data = urlopen(URL)
    description = data.read().decode('utf-8', 'ignore')
    b = description.find('"locus"')
    gene_info = description[b+9:b+20]
    real_gene = ''
    for i in gene_info:
        if i == '"':
            break
        real_gene += i
    Gene_table.append(real_gene)

print(Gene_table)

with open('C:/Users/bgr16/Desktop/Rosalind/snps_genes.txt', 'w') as f:
    for i in Gene_table:
        f.write(i+'\n')
```
