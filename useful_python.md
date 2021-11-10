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

## How to extract a sub_alignment of sites from a file sites.txt
`for a in `grep "BIN" partition_file | awk -F "=" '{print$2}' | sed ':a;N;$!ba;s/\n//g' | sed 's/,//g'`; do seq $(echo $a | awk -F "-" '{print$1}') $(echo $a | awk -F "-" '{print$2}') ; done > sites.txt`
for a in `awk -F "-" '{print$1}' file_esclusi`; do sed -i "s/^$a$//g" sites.txt ; sed -i '/^$/d' sites.txt ; done

```
import Bio
from Bio.Seq import Seq
from Bio.SeqRecord import SeqRecord
from Bio import AlignIO
from Bio.Align import MultipleSeqAlignment

align =  AlignIO.read("concat_mito.phy","phylip")

#Read the sites that show the indels in the total alignment, -1 since python starts from 0. 
with open("sites.txt","r") as r:
	sites=[int(a)-1 for a in r.readlines()]

align2=MultipleSeqAlignment([])
for a in range(0,len(align)):
	seq=""	
	for b in sites:
		seq+=align[a].seq[b]	
	
	align2.add_sequence(align[a].id,seq)
  
AlignIO.write(align2,"mito_gapped.phy","phylip")
```



          
