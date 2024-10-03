---
layout: default
title: Python
parent: Códigos de programação
---
# {{page.title}}

## Encodes
```python
.encode('utf8')
.decode('latin1').encode('utf8')
.decode('ISO-8859-1').encode('UTF-8')
```

## Remover espaços em branco e converter caracteres em minúsculos
```python
.strip().lower()
```
## Transformar data texto em data objeto
```python
payment_date = datetime.datetime.strptime(data['payment_date'],'%H:%M:%S %b %d, %Y')
```
## Transformar retorno do objeto em array flat
```python
.values_list('assinante__pk', flat=True)
```
## Ler planilhas CSV
```python
lista = []
with open("/home/ec2-user/django/tools/logs/nome_planilha.csv") as f:
    for line in f:
        try:
            lista.append(line.replace('\n','').replace('\r',''))
        except:
            pass
```

## Limpar HTML de uma string 
```python
import re
TAG_RE = re.compile(r'<[^>]+>')
def remove_tags(text):
    return TAG_RE.sub('', text)
```