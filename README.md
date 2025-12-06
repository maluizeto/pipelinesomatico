# pipeline somatico

```bash
!pip install pandas
```
```python
import pandas as pd
pd.read_csv('results/WP048/alterations.tsv',sep='\t',index_col=False, engine= 'python')
```
