# 🎨 CycleGAN para Transferência de Estilo: Pokémon ao Estilo Van Gogh

### Tabela de Conteúdos
1. [Visão Geral](#1-visão-geral)
2. [Contexto Académico](#2-contexto-académico)
3. [Arquitetura do Modelo](#3-arquitetura-do-modelo)
4. [Funções de Perda](#4-funções-de-perda)
5. [Setup do Ambiente e Execução](#5-setup-do-ambiente-e-execução)
6. [Treino e Hiperparâmetros](#6-treino-e-hiperparâmetros)
7. [Resultados e Análise](#7-resultados-e-análise)
8. [Limitações e Trabalhos Futuros](#8-limitações-e-trabalhos-futuros)
9. [Autor](#9-autor)
10. [Licença](#10-licença)
11. [Contacto](#11-contacto)

---

## 1. Visão Geral

A tradução de imagem-para-imagem é uma tarefa central em Visão por Computador que visa aprender um mapeamento entre uma imagem de entrada e uma imagem de saída. Abordagens tradicionais requerem datasets *emparelhados*. Este projeto aborda a tradução **não emparelhada** usando o **CycleGAN**. O CycleGAN aprende mapeamentos entre dois domínios sem dados emparelhados, usando uma perda de consistência de ciclo para regular o treino.

## 2. Contexto Académico

Desenvolvido na Unidade Curricular de **Visão por Computador**, no Mestrado em Engenharia Informática (Perfil de Computação Gráfica) da **Universidade do Minho**.

- **Autor:** Fernando Daniel de Magalhães Pipa Alves (pg54470)
- **Ano Letivo:** 2023/2024

## 3. Arquitetura do Modelo

O CycleGAN consiste em duas redes Geradoras e Discriminadoras:
- **Geradores:** `G_AB` e `G_BA` para mapear entre os domínios.
- **Discriminadores:** `D_A` e `D_B` para distinguir imagens reais de geradas.

### Gerador

Tem um codificador-descodificador com blocos residuais:
- **Encoder:** Reduz a dimensão espacial.
- **ResNet Blocks:** Processam características extraídas.
- **Decoder:** Reconstrói a imagem no domínio de destino.

### Discriminador (PatchGAN)

Classifica *patches* individuais em vez de toda a imagem.

## 4. Funções de Perda

- **Perda Adversária:** Mede quão bem o gerador engana o discriminador (utilizando `MSELoss`).
- **Perda de Consistência de Ciclo:** Garante que a imagem regressa à forma original após tradução de ida e volta (`L1Loss`).
- **Perda de Identidade:** Ajuda a preservar a composição de cores original.

## 5. Setup do Ambiente e Execução

### Requisitos

Instala as bibliotecas necessárias usando pip:
```bash
pip install torch torchvision pillow matplotlib numpy torchsummary jupyterlab
```
### Instruções

1. **Clonar o Repositório:**
```bash
git clone https://github.com/Mastro66/VCPI-Individual.git
```
2. **Navegar para a pasta:**
```bash
cd VCPI-Individual
```
3. **Descarregar os Datasets:** Popula as pastas em `datasets/` com as respetivas imagens.

### Estrutura de Ficheiros
```
├── datasets/
│   ├── pokemon/
│   └── vangogh/
├── CycleGAN_pg54470.ipynb
└── README.md
```
## 6. Treino e Hiperparâmetros

| Hiperparâmetro          | Valor     | Descrição                                    |
|-------------------------|-----------|----------------------------------------------|
| Número de Épocas        | 100       | Total de passagens pelo dataset de treino.   |
| Tamanho do Lote         | 1         | Número de imagens por iteração.              |
| Taxa de Aprendizagem    | 0.0002    | Tamanho do passo do otimizador.              |
| Otimizador              | Adam      | Otimização para Geradores e Discriminadores. |
| `beta1`, `beta2` (Adam) | 0.5, 0.999| Parâmetros do otimizador Adam.               |
| `λ_cycle`               | 10.0      | Peso da Perda de Consistência de Ciclo.      |
| `λ_identity`            | 5.0       | Peso da Perda de Identidade.                 |

## 7. Resultados e Análise
[Ir para a Seção 7](./CycleGAN_pg54470.ipynb#7-visualização-e-guarda-dos-resultados-e-modelos)

## 8. Limitações e Trabalhos Futuros

- Aumentar o Dataset
- Ajuste Fino de Hiperparâmetros
- Exploração de Outras Arquiteturas
- Aplicação de Técnicas de Regularização
- Avaliação Quantitativa com métricas como FID ou IS

## 9. Autor

- **Fernando Daniel de Magalhães Pipa Alves**
- GitHub: [Mastro66](https://github.com/Mastro66)

## 10. Licença

Este projeto está licenciado sob a Licença MIT.