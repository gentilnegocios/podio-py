[![No Maintenance Intended](http://unmaintained.tech/badge.svg)](http://unmaintained.tech/)

PyPodio
=====

Python wrapper for the Podio API.

Install
-------

Dependencies

* httplib2

PyPodio is not yet available on PyPI, we're waiting to have it a bit more
stable. Install by cloning from the GitHub repo:

    $ git clone git://github.com/gentilnegocios/podio-py.git
    $ cp -r podio-py/pypodio2 path/to/destination

Alternatively, install via `pip`:

    $ pip install -e git+https://github.com/gentilnegocios/podio-py.git#egg=pypodio2


Example
-------

    from pypodio2 import api
    from client_settings import *

    c = api.OAuthClient(
        client_id,
        client_secret,
        username,
        password,
    )
    print c.Item.find(22342)

Notes
------

It is possible to override the default response handler by passing handler as
a keyword argument to a transport function call. For example:

    x = lambda x,y: (x,y)
    result = c.Item.find(11007, basic=True, handler=x)
    ($result, $data) #Returned info

Modified from original files:
* pypodio2/areas.py: lines 301 and 306, method 'get' to 'GET'


Tests
-----

To run tests for the API wrapper, you need two additional dependencies:

* mock
* nose

With those installed, run `nosetests` from the repository's root directory.


Meta
----

* Code: `git clone https://github.com/gentilnegocios/podio-py.git`
* Home: <https://github.com/gentilnegocios/podio-py>
* Bugs: <https://github.com/gentilnegocios/podio-py/issues>


# Guia Completo para Corrigir Erros de Importação na Biblioteca `pypodio2`

Se você está enfrentando erros relacionados à importação na biblioteca `pypodio2` ao usar Python 3.x (especialmente 3.12 ou superior), este guia fornece todas as instruções para corrigir os problemas.

---

## **1. Por que os Erros Acontecem?**

Os erros como `ImportError` ou `ModuleNotFoundError` ocorrem porque a biblioteca `pypodio2` utiliza funções ou módulos que foram modificados ou movidos em versões mais recentes do Python. Exemplos incluem:
- A função `urlencode`, que foi movida de `urllib` para `urllib.parse` no Python 3.
- Importações incorretas, como `from encode import ...`, que precisam ser ajustadas para importações relativas.

---

## **2. Passo a Passo para Corrigir os Erros**

### **2.1. Ajuste no Código Principal**

Antes de modificar a biblioteca diretamente, adicione o seguinte código no início do seu programa (onde você utiliza a biblioteca `pypodio2`). Isso cria uma referência temporária para `urlencode` dentro do módulo `urllib`, corrigindo problemas relacionados.

```python
import urllib.parse
import sys
sys.modules['urllib'].urlencode = urllib.parse.urlencode
```

### **2.2. Ajuste no Código dentro do diretório do pypodio2**

 Agora, dentro do diretório do pypodio2, localize o arquivo transport.py e altere o importação :
 
 'from urllib import urlencode'
 para 'from urllib.parse import urlencode'
 e 'from encode import multipart_encode' por 
 'from .encode import multipart_encode'



  
  
