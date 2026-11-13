# Monitoramento Meteorológico - Jaraguá do Sul/SC



---

## Sobre o Projeto

Esse projeto foi desenvolvido como parte da avaliação prática para colocar em prática a comunicação entre sistemas via requisições HTTP e APIs REST. A ideia aqui foi criar uma aplicação em Python que busca dados climáticos de **Jaraguá do Sul – SC** (latitude `-26.4851` e longitude `-49.0713`) consumindo uma API local e mostra tudo organizado numa tela web feita com Streamlit.

Para manter o código limpo e fácil de dar manutenção, separei as responsabilidades em dois arquivos principais: um cuida só da conversa com a API e do tratamento do JSON (`consumidor_api.py`), e o outro monta a parte visual que aparece no navegador (`frontend.py`).

---

## Como os dados circulam na aplicação

O fluxo de funcionamento funciona assim:

1. **API Meteorológica Offline (`http://127.0.0.1:8000`):** É o servidor base (desenvolvido em FastAPI) que disponibiliza os dados simulados da estação de Jaraguá do Sul no endpoint `/v1/forecast`.
2. **Consumidor (`consumidor_api.py`):** Usa a biblioteca `requests` para fazer uma chamada `GET` passando a latitude e a longitude nos parâmetros. Ele verifica se a requisição deu certo (`raise_for_status()`), lê o JSON retornado, pega os valores dentro da chave `current` e devolve tudo organizado em um dicionário Python. Se a API estiver fora do ar ou der erro de conexão, ele trata a exceção para o programa não travar do nada.
3. **Interface (`frontend.py`):** Importa a função `obter_dados_meteorologicos()` direto do consumidor e exibe os 6 indicadores pedidos na atividade (temperatura, umidade relativa, sensação térmica, precipitação, velocidade do vento e o horário da medição) com suas respectivas unidades de medida.

---

## Estrutura dos Arquivos

```text
projeto_meteorologico/
├── .gitignore            # Evita subir a .venv e arquivos de cache pro GitHub
├── requirements.txt      # Lista das bibliotecas usadas no projeto
├── consumidor_api.py     # Módulo que faz a requisição HTTP e filtra o JSON
├── frontend.py           # Interface visual feita em Streamlit
└── README.md             # Documentação do projeto
