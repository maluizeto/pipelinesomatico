# Pipeline Somático 

## Amostra WP048

### 1. Clonar o github Imabrasil-hg38
```bash
!git clone https://github.com/renatopuga/lmabrasil-hg38.git
```
### 2. Agora vá até o github Imabrasil-hg38 na seção Usando CGI via API Rest no google Colab 
```python
!cut -f1-4 /content/lmabrasil-hg38/vep_output/liftOver_WP048_hg19ToHg38.vep.filter.tsv | sed -e "s/CHROM/CHR/g"  > df_WP048-cgi.txt
head df_WP048-cgi.txt
```
Código para listar as 10 primeiras linhas do código
```bash
!head df_WP048-cgi.txt
```
### 3. Enviar Job para CGI API - Entrar no site do CGI, fazer o login e criar o seu token <br>
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
### 4. Status do JobID - A partir disso teremos nosso id job
```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers)
r.json()
```

### 5. Log ID

```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'logs'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
r.json()
```
### 6. Download dos resultados - Criar o diretorio com o ID da amostra dentro de results
#### Descrever cada arquivo de resultado:
***alterations.tsv:***  arquivo tabulado que contém as variantes genéticas identificadas após o processamento e filtragem do VCF; <br>
***biomarkers.tsv:***  tabela contendo os biomarcadores associados às variantes detectadas;<br>
***input01.tsv:***  arquivo de entrada do pipeline, contendo os dados iniciais que serão analisados;<br>
***summary.txt:***  arquivo de texto com um resumo final da análise.

```bash
!mkdir -p results/WP048
```
```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'download'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
with open('/content/results/WP048/W048-cgi.zip', 'wb') as fd:
    fd.write(r._content)
```

### 7. Descompactar o zip com os resultados
```bash
!unzip -o /content/results/WP048/W048-cgi.zip -d /content/results/WP048/
```
### 8. Instalar pip panda 
```bash
!pip install pandas
```
```python
import pandas as pd
pd.read_csv('/content/results/WP048/alterations.tsv',sep='\t',index_col=False, engine= 'python')
```



## Amostra WP017



### 1. Clonar o github Imabrasil-hg38
```bash
!git clone https://github.com/renatopuga/lmabrasil-hg38.git
```
### 2. Agora vá até o github Imabrasil-hg38 na seção Usando CGI via API Rest no google Colab 
```python
!cut -f1-4 /content/lmabrasil-hg38/vep_output/liftOver_WP048_hg19ToHg38.vep.filter.tsv | sed -e "s/CHROM/CHR/g"  > df_WP017-cgi.txt
head df_WP017-cgi.txt
```
Código para listar as 10 primeiras linhas do código
```bash
!head df_WP017-cgi.txt
```
### 3. Enviar Job para CGI API - Entrar no site do CGI, fazer o login e criar o seu token
Fonte: https://www.cancergenomeinterpreter.org/rest_api
```python
import requests
headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload = {'cancer_type': 'HEMATO', 'title': 'Somatic MF WP017', 'reference': 'hg38'}
r = requests.post('https://www.cancergenomeinterpreter.org/api/v1',
                headers=headers,
                files={
                        'mutations': open('df_WP017-cgi.txt', 'rb')
                        },
                data=payload)

r.json()
```
### 4. Status do JobID - A partir disso teremos nosso id job
```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers)
r.json()
```

### 5. Log ID

```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'logs'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
r.json()
```
### 6. Download dos resultados - Criar o diretorio com o ID da amostra dentro de results
```bash
!mkdir -p results/WP017
```
```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'download'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
with open('/content/results/WP017/W017-cgi.zip', 'wb') as fd:
    fd.write(r._content)
```

Descompactar o zip com os resultados
```bash
!unzip -o /content/results/WP017/W017-cgi.zip -d /content/results/WP017/
```
Instalar pip panda 
```bash
!pip install pandas
```
```python
import pandas as pd
pd.read_csv('/content/results/WP017/alterations.tsv',sep='\t',index_col=False, engine= 'python')
```


# Amostra WP019



Clonar o github Imabrasil-hg38
```bash
!git clone https://github.com/renatopuga/lmabrasil-hg38.git
```
Agora vá até o github Imabrasil-hg38 na seção Usando CGI via API Rest no google Colab 
```python
!cut -f1-4 /content/lmabrasil-hg38/vep_output/liftOver_WP019_hg19ToHg38.vep.filter.tsv | sed -e "s/CHROM/CHR/g"  > df_WP019-cgi.txt
```
Código para listar as 10 primeiras linhas do código
```bash
!head df_WP019-cgi.txt
```
Enviar Job para CGI API - Entrar no site do CGI, fazer o login e criar o seu token
Fonte: https://www.cancergenomeinterpreter.org/rest_api
```python
import requests
headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload = {'cancer_type': 'HEMATO', 'title': 'Somatic MF WP019', 'reference': 'hg38'}
r = requests.post('https://www.cancergenomeinterpreter.org/api/v1',
                headers=headers,
                files={
                        'mutations': open('df_WP019-cgi.txt', 'rb')
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

Log ID

```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'logs'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
r.json()
```
Download dos resultados - Criar o diretorio com o ID da amostra dentro de results
```bash
!mkdir -p results/WP019
```
```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'download'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
with open('/content/results/WP019/W019-cgi.zip', 'wb') as fd:
    fd.write(r._content)
```

Descompactar o zip com os resultados
```bash
!unzip -o /content/results/WP019/W019-cgi.zip -d /content/results/WP019/
```
Instalar pip panda 
```bash
!pip install pandas
```
```python
import pandas as pd
pd.read_csv('/content/results/WP019/alterations.tsv',sep='\t',index_col=False, engine= 'python')
```


# Amostra WP058



Clonar o github Imabrasil-hg38
```bash
!git clone https://github.com/renatopuga/lmabrasil-hg38.git
```
Agora vá até o github Imabrasil-hg38 na seção Usando CGI via API Rest no google Colab 
```python
!cut -f1-4 /content/lmabrasil-hg38/vep_output/liftOver_WP058_hg19ToHg38.vep.filter.tsv | sed -e "s/CHROM/CHR/g"  > df_WP058-cgi.txt
```
Código para listar as 10 primeiras linhas do código
```bash
!head df_WP058-cgi.txt
```
Enviar Job para CGI API - Entrar no site do CGI, fazer o login e criar o seu token
Fonte: https://www.cancergenomeinterpreter.org/rest_api
```python
import requests
headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload = {'cancer_type': 'HEMATO', 'title': 'Somatic MF WP058', 'reference': 'hg38'}
r = requests.post('https://www.cancergenomeinterpreter.org/api/v1',
                headers=headers,
                files={
                        'mutations': open('df_WP058-cgi.txt', 'rb')
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

Log ID

```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'logs'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
r.json()
```
Download dos resultados - Criar o diretorio com o ID da amostra dentro de results
```bash
!mkdir -p results/WP058
```
```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'download'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
with open('/content/results/WP058/W058-cgi.zip', 'wb') as fd:
    fd.write(r._content)
```

Descompactar o zip com os resultados
```bash
!unzip -o /content/results/WP058/W058-cgi.zip -d /content/results/WP058/
```
Instalar pip panda 
```bash
!pip install pandas
```
```python
import pandas as pd
pd.read_csv('/content/results/WP058/alterations.tsv',sep='\t',index_col=False, engine= 'python')
```


# Amostra WP068



Clonar o github Imabrasil-hg38
```bash
!git clone https://github.com/renatopuga/lmabrasil-hg38.git
```
Agora vá até o github Imabrasil-hg38 na seção Usando CGI via API Rest no google Colab 
```python
!cut -f1-4 /content/lmabrasil-hg38/vep_output/liftOver_WP068_hg19ToHg38.vep.filter.tsv | sed -e "s/CHROM/CHR/g"  > df_WP068-cgi.txt
```
Código para listar as 10 primeiras linhas do código
```bash
!head df_WP068-cgi.txt
```
Enviar Job para CGI API - Entrar no site do CGI, fazer o login e criar o seu token
Fonte: https://www.cancergenomeinterpreter.org/rest_api
```python
import requests
headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload = {'cancer_type': 'HEMATO', 'title': 'Somatic MF WP068', 'reference': 'hg38'}
r = requests.post('https://www.cancergenomeinterpreter.org/api/v1',
                headers=headers,
                files={
                        'mutations': open('df_WP058-cgi.txt', 'rb')
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

Log ID

```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'logs'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
r.json()
```
Download dos resultados - Criar o diretorio com o ID da amostra dentro de results
```bash
!mkdir -p results/WP068
```
```python
import requests
job_id = "b0a7ea9ba22a3eade52f"

headers = {'Authorization': 'maluizeto@gmail.com cc8e478a27b52f75b94a'}
payload={'action':'download'}
r = requests.get('https://www.cancergenomeinterpreter.org/api/v1/%s' % job_id, headers=headers, params=payload)
with open('/content/results/WP068/W068-cgi.zip', 'wb') as fd:
    fd.write(r._content)
```

Descompactar o zip com os resultados
```bash
!unzip -o /content/results/WP068/W068-cgi.zip -d /content/results/WP058/
```
Instalar pip panda 
```bash
!pip install pandas
```
```python
import pandas as pd
pd.read_csv('/content/results/WP068/alterations.tsv',sep='\t',index_col=False, engine= 'python')
```

# Tabela 


Agora vamos juntas todas as tabelas em só uma tabela 

```python
import pandas as pd

wp048 = pd.read_csv('/content/results/WP048/alterations.tsv', sep='\t')
wp017 = pd.read_csv('/content/results/WP017/alterations.tsv', sep='\t')
wp019 = pd.read_csv('/content/results/WP019/alterations.tsv', sep='\t')
wp058 = pd.read_csv('/content/results/WP058/alterations.tsv', sep='\t')
wp068 = pd.read_csv('/content/results/WP068/alterations.tsv', sep='\t')


wp048["Sample"] = "WP048"
wp017["Sample"] = "WP017"
wp019["Sample"] = "WP019"
wp058["Sample"] = "WP058"
wp068["Sample"] = "WP068"

tabela_final = pd.concat([wp048, wp017, wp019, wp058, wp068], ignore_index=True)

tabela_final.head()

tabela_final.to_csv("tabela_final_CGI.tsv", sep="\t", index=False)

cols = ["Sample"] + [c for c in tabela_final.columns if c != "Sample"]
tabela_final = tabela_final[cols]
```










