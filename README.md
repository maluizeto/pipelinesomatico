# Pipeline Somético 

Amostra WP048



Clonar o github Imabrasil-hg38
```bash
!git clone https://github.com/renatopuga/lmabrasil-hg38.git
```
Agora vá até o github Imabrasil-hg38 na seção Usando CGI via API Rest no google Colab 
```python
cut -f1-4 /content/lmabrasil-hg38/vep_output/liftOver_WP048_hg19ToHg38.vep.filter.tsv | sed -e "s/CHROM/CHR/g"  > df_WP048-cgi.txt
head df_WP048-cgi.txt
```
Código para listar as 10 primeiras linhas do código
```bash
head df_WP048-cgi.txt
```
Enviar Job para CGI API - Entrar no site do CGI, fazer o login e criar o seu token
Fonte: https://www.cancergenomeinterpreter.org/rest_api
```python
import requests
headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload = {'cancer_type': 'HEMATO', 'title': 'Somatic MF WP048', 'reference': 'hg38'}
r = requests.post('https://www.cancergenomeinterpreter.org/api/v1',
                headers=headers,
                files={
                        'mutations': open('df_WP048-cgi.txt', 'rb')
                        },
                data=payload)

r.json()
```
Status do JobID - A partir disso teremos nosso id job
```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers)
r.json()
```

`
