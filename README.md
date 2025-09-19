
# Rede Neural para Previsão de Vendas

> **Notebook para tratamento de dados, treinamento e previsão usando uma rede neural MLP (PyTorch) em séries temporais de vendas por produto e PDV.**

---

## Instalação de Dependências

Os arquivos .parquet gerados incluindo o arquivo original renomeado para 1.snappy.parquet estão em: https://drive.google.com/drive/u/0/folders/1wQW08fGFT5iFQV-UsEJLed0_vT8afdqQ

Execute a célula abaixo no início do notebook para instalar todas as bibliotecas necessárias:


```python
!pip install pandas pyarrow torch tqdm joblib
```

### Principais Bibliotecas Utilizadas
- **pandas**: Manipulação e análise de dados tabulares.
- **pyarrow**: Leitura e escrita eficiente de arquivos Parquet.
- **torch (PyTorch)**: Framework para construção e treinamento de redes neurais.
- **tqdm**: Barra de progresso para loops (opcional, mas útil para acompanhar execuções longas).
- **joblib**: Serialização de objetos Python (salvar modelos e metadados).

---

## Etapas do Notebook

1. **Tratamento dos Dados**
	- Leitura do arquivo de vendas original (`1.snappy.parquet`).
	- Conversão de datas, filtragem para o ano de 2022.
	- Remoção de outliers usando o método do IQR.
	- Cálculo da média móvel para suavização das quantidades.
	- Remoção de duplicidades e filtragem de séries temporais curtas.
	- Geração do arquivo `dados_tratados.parquet`.

2. **Remoção de NaNs**
	- Eliminação de linhas com valores ausentes nas colunas principais.
	- Geração do arquivo `dados_tratados_sem_nan.parquet`.

3. **Treinamento da Rede Neural (MLP)**
	- Definição da arquitetura MLP (Multi-Layer Perceptron) usando PyTorch.
	- Preparação do dataset global (janelas de séries temporais).
	- Treinamento do modelo para prever a quantidade futura.
	- Salvamento do modelo treinado (`mlp_global_2022.pth`) e metadados (`mlp_global_metadata.pkl`).

4. **Previsão para 2023**
	- Carregamento do modelo treinado.
	- Geração de previsões para cada produto/PDV para as próximas semanas.
	- Salvamento dos resultados em batches e arquivo final `previsoes_2023_mlp.parquet`.

---

## Arquivos Gerados

- **dados_tratados.parquet**: Dados limpos e suavizados, prontos para modelagem.
- **dados_tratados_sem_nan.parquet**: Dados sem valores ausentes, usados para o treinamento.
- **mlp_global_2022.pth**: Arquivo do modelo MLP treinado (PyTorch).
- **mlp_global_metadata.pkl**: Metadados do modelo (parâmetros, grupos, janela).
- **previsoes_2023_mlp.parquet**: Previsões geradas para o ano de 2023.

---

## Observações
- Recomenda-se rodar o notebook em ambiente com GPU para acelerar o treinamento.
- Certifique-se de que todos os arquivos estejam no mesmo diretório do notebook.
- O fluxo é modular: você pode adaptar as funções para outros contextos de séries temporais.

---

**Dúvidas ou sugestões? Fique à vontade para contribuir ou abrir uma issue!**

