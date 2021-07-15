File with useful python command lines 


To download a fasta from NCBI
```
import Bio
from Bio import Entrez
from Bio import SeqIO
Entrez.email = "alessand.formaggioni@studio.unibo.it"
with Entrez.efetch(db="nucleotide", rettype="gb", retmode="text", id="NC_017612") as handle:
     for seq_record in SeqIO.parse(handle, "gb"):
             SeqIO.write(seq_record,"ciao.fasta","fasta")
```
          
