# FIAP - Faculdade de Informática e Administração Paulista

<br>

# Sistema de Registro de Carga de Soja

## Grupo

## 👨‍🎓 Integrantes: 
- **Antônio Ancelmo** | **E-mail:** antonio.anbarros@gmail.com | **GitHub:** @AntonioBarros19 | **RM:** 562099
- **Beatriz Pilecarte** | **E-mail:** beatrizpilecartedemelo@gmail.com | **GitHub:** @BPilecarte | **RM:** 564952
- **Claudio Santos** | **E-mail:** claudiossilva93@gmail.com | **GitHub:** @claudiossilva93s | **RM:** 562915
- **Francismar Alves** | **E-mail:** yggdrasil.git@gmail.com | **GitHub:** @yggdrasilGit | **RM:** 564952
- **Vitor Eiji** | **E-mail:** vitorfer2018@gmail.com | **GitHub:** @Vitor985-hub | **RM:** 562915


## 👩‍🏫 Professores:
### Tutor(a) 
- Leonardo Ruiz Orabona
### Coordenador(a)
- André Godoi Chiovato


## 📜 Descrição

Este sistema automatiza o processo de registro de carga de soja transportada por caminhões. Ele captura imagens de placas de caminhões, realiza a leitura da placa, converte essa leitura em texto e utiliza um simulador para calcular o peso da carga de soja. As informações geradas são então registradas em um banco de dados Oracle e também são salvas em um arquivo `.txt` para registro e controle.


### Funcionalidades Principais:

1. **Leitura de Placa de Caminhão**: O sistema usa a tecnologia OCR (Reconhecimento Óptico de Caracteres) para ler placas de veículos a partir de imagens. A biblioteca EasyOCR é utilizada para realizar a extração de texto da placa do caminhão.

2. **Simulação de Carga**: Após a leitura da placa, o sistema simula a quantidade de soja que o caminhão está carregando. A carga é simulada aleatoriamente, gerando valores entre 20 a 40 toneladas.

3. **Registro no Banco de Dados**: As informações do caminhão (placa, modelo, ano, motorista) e da carga (peso e tipo de cultura) são registradas em um banco de dados Oracle. A tabela de cargas está vinculada à tabela de caminhões por meio de uma chave estrangeira (placa).

4. **Geração de Arquivo TXT**: Após a leitura da placa e simulação do peso, o sistema cria um arquivo `.txt` contendo as informações detalhadas da carga (placa, tipo de cultura, peso da carga), facilitando o controle físico e eletrônico.

## Como Funciona o Processo:

1. **Leitura da Placa**:
   - O sistema captura a imagem da placa do caminhão.
   - A imagem é processada pela biblioteca `EasyOCR` para reconhecer a placa do veículo.
   - O texto da placa é extraído e convertido em um formato utilizável.

2. **Simulação do Peso da Carga**:
   - Com base na placa do caminhão, o sistema simula o peso da carga transportada (soja). O peso é gerado aleatoriamente entre 20 e 40 toneladas.
   
3. **Armazenamento no Banco de Dados**:
   - A informação sobre o caminhão (placa, modelo, motorista) e a carga (tipo de cultura, peso) é registrada no banco de dados.
   - A tabela `CAMINHAO` armazena dados sobre o caminhão, enquanto a tabela `GRAO_SOJA` registra as informações da carga. A chave estrangeira da tabela `GRAO_SOJA` faz referência à tabela `CAMINHAO` através da coluna `placa`.

4. **Geração do Arquivo TXT**:
   - Após o processo de leitura e simulação, o sistema gera um arquivo `.txt` contendo as informações registradas, como a placa do caminhão, tipo de carga (soja) e peso da carga.


## 📁 Estrutura de pastas

Dentre os arquivos e pastas presentes na raiz do projeto, definem-se:
```bash
SGAG-CARGO-REGISTRATION-SYSTEM/
│
├── 📂 api_read_plate/              # Módulo de leitura de placa via OCR
│   ├── 📂 images/                  # Imagens e arquivos de placas detectadas
│   │   ├── __init__.py
│   │   ├── placa_detectada.txt
│   │   └── tratamento_txt.py
│   ├── plate_read.py              # Lógica de leitura OCR da placa
│   └── __init__.py
│
├── 📂 display/                     # Interface do menu
│   ├── menu.py
│   └── __init__.py
│
├── 📂 manager/                     # Gerenciamento de entidades
│   ├── caminhao.py                 # Cadastro e controle de caminhões
│   ├── entrada_de_grao.py          # Registro de entrada de grãos
│   └── __pycache__/
│
├── 📂 oracle_db/                  # Acesso ao banco de dados Oracle
│   ├── conection.py               # Conexão com Oracle
│   ├── criar_tabela.py            # Criação de tabelas
│   ├── crud.py                    # Operações CRUD
│   └── __init__.py
│
├── 📂 simulador_carga/            # Simulação de peso da carga
│   ├── simulador_carga.py
│   └── __init__.py
│
├── 📂 sql_table/                  # Scripts SQL para criação de tabelas
│   └── tabela_cadastra_motorista.sql
│
├── .gitattributes                 # Configuração de atributos Git
├── carga_soja.json                # Dados simulados de carga
├── dados_caminhao.json            # Dados simulados de caminhões
├── main.py                        # Script principal do sistema
├── README.md                      # Documentação do projeto
└── requirmentsta.txt              # Dependências do projeto
 ```

## 🔧 Como executar o código

### Instalação das Dependências

Para instalar as dependências necessárias, siga os passos abaixo:

1. **Crie um ambiente virtual** (opcional, mas recomendado):
   
   ```bash
   python3 -m venv env
   ```

2. **Ative o ambiente virtual**:
   - No Windows:
     ```bash
     .\env\Scripts\activate
     ```
   - No Linux/macOS:
     ```bash
     source env/bin/activate
     ```

3. **Instale as dependências**:
   Execute o seguinte comando para instalar todas as bibliotecas necessárias:

   ```bash
   pip install -r requirements.txt
   ```

## Dependências

O sistema depende de várias bibliotecas para funcionar corretamente. Abaixo está a lista de dependências necessárias:

```txt
cffi==1.17.1
cryptography==44.0.2
cx_Oracle==8.3.0
easyocr==1.7.2
filelock==3.18.0
fsspec==2025.3.2
imageio==2.37.0
Jinja2==3.1.6
lazy_loader==0.4
MarkupSafe==3.0.2
mpmath==1.3.0
networkx==3.2.1
ninja==1.11.1.4
numpy==1.26.4
openalpr==1.1.0
opencv-python==4.11.0.86
opencv-python-headless==4.11.0.86
oracledb==3.1.0
packaging==24.2
pillow==11.2.1
pyclipper==1.3.0.post6
pycparser==2.22
pytesseract==0.3.13
python-bidi==0.6.6
PyYAML==6.0.2
scikit-image==0.24.0
scipy==1.13.1
shapely==2.0.7
sympy==1.13.3
tifffile==2024.8.30
torch==2.2.2
torchvision==0.17.2
typing_extensions==4.13.2
```

## Estrutura do Banco de Dados

O banco de dados utilizado é o Oracle, e a estrutura do banco é a seguinte:

### Tabelas:

- **Tabela CAMINHAO**:
  - `id`: Identificador único do caminhão (PK)
  - `placa`: Placa do caminhão
  - `modelo`: Modelo do caminhão
  - `ano`: Ano de fabricação
  - `motorista`: Nome do motorista

- **Tabela GRAO_SOJA**:
  - `id`: Identificador único da carga (PK)
  - `data_registro`: Data de registro da carga (com valor padrão de `SYSDATE`)
  - `tipo_cultura`: Tipo da cultura (no caso, "soja")
  - `peso_toneladas`: Peso da carga em toneladas
  - `placa`: Chave estrangeira que faz referência à tabela `CAMINHAO` (placa)


## Exemplos de Uso

### Registrar uma Carga

Após o processamento da imagem da placa e a simulação do peso da carga, o sistema registra as informações da carga no banco de dados.

```python
from datetime import datetime
from oracle_db.conection import conectar

# Exemplo de carga simulada
carga = {
    "tipo_cultura": "soja",
    "peso_toneladas": 27.6
}

placa = "ABC1234"  # Exemplo de placa de caminhão

registrar_carga_soja_no_banco(placa, carga)
```

### Gerar o Arquivo TXT

Após o registro da carga, o sistema cria um arquivo `.txt` com as informações da carga.

```python
salvar_em_json({'placa': placa, **carga}, 'carga_soja.txt')
```



## 📋 Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/agodoi/template">MODELO GIT FIAP</a> por <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://fiap.com.br">Fiap</a> está licenciado sobre <a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">Attribution 4.0 International</a>.</p>

