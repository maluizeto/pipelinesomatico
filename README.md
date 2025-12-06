# pipeline somatico

AMOSTRA WP048

Clonar o github Imabrasil-hg38
```bash
!git clone https://github.com/renatopuga/lmabrasil-hg38.git
```
Agora vá até o github Imabrasil-hg38 na seção Usando CGI via API Rest no google Colab 
```bash
cut -f1-4 /content/lmabrasil-hg38/vep_output/liftOver_WP048_hg19ToHg38.vep.filter.tsv | sed -e "s/CHROM/CHR/g"  > df_WP048-cgi.txt
head df_WP048-cgi.txt
```
Código para listar as 10 primeiras linhas
```bash
head df_WP048-cgi.txt
```
