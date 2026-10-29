# Análise de Não Conformidades, Reclamações, Sugestões de Melhoria e Elogios

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/docs/Web/JavaScript)
[![Sem dependências](https://img.shields.io/badge/depend%C3%AAncias-nenhuma-2E7D5B)](#requisitos)
[![Funciona offline](https://img.shields.io/badge/execu%C3%A7%C3%A3o-100%25%20local-0E4A54)](#proteção-de-dados)
[![ISO 9001:2015](https://img.shields.io/badge/ISO%209001%3A2015-cl%C3%A1usula%2010.2-0E4A54)](#correspondência-com-a-norma)

Aplicação autónoma, num único ficheiro HTML, para o registo e tratamento de não conformidades,
reclamações, sugestões de melhoria e elogios no âmbito de um sistema de gestão da qualidade
certificado pela NP EN ISO 9001:2015.

Foi desenvolvida para a Unidade de Ensino da Unidade Local de Saúde da Guarda, E.P.E., em substituição
de um formulário Microsoft Forms que, não mantendo registo acumulado, não permitia demonstrar o estado
de tratamento das ocorrências nem produzir a evidência exigida em auditoria.

---

## Índice

- [Motivação](#motivação)
- [Funcionalidades](#funcionalidades)
- [Instalação e utilização](#instalação-e-utilização)
- [Requisitos](#requisitos)
- [Importação a partir do Microsoft Forms](#importação-a-partir-do-microsoft-forms)
- [Armazenamento e salvaguarda dos dados](#armazenamento-e-salvaguarda-dos-dados)
- [Proteção de dados](#proteção-de-dados)
- [Correspondência com a norma](#correspondência-com-a-norma)
- [Adaptação a outra organização](#adaptação-a-outra-organização)
- [Estrutura do repositório](#estrutura-do-repositório)
- [Limitações conhecidas](#limitações-conhecidas)
- [Como citar](#como-citar)
- [Licença](#licença)
- [Autor](#autor)

---

## Motivação

Um formulário de recolha resolve a entrada de dados, mas não resolve a gestão do ciclo de tratamento.
A cláusula 10.2 da ISO 9001:2015 exige que a organização conserve informação documentada sobre a
natureza das não conformidades, as ações empreendidas e os **resultados de qualquer ação corretiva**,
o que pressupõe acompanhar cada ocorrência desde a deteção até à verificação da eficácia.

Esta aplicação acrescenta ao formulário aquilo de que ele carece: registo acumulado e pesquisável,
estados de tratamento, agregação das causas identificadas, relatórios para arquivo e para a revisão
pela gestão, e um conjunto de verificações automáticas que impedem os erros mais frequentes no
tratamento de não conformidades.

## Funcionalidades

**Registo e tratamento**

- Formulário com a estrutura integral do impresso em uso: descrição do evento, correção imediata,
  análise de causas, plano de ação corretiva, verificação da eficácia e atualização do SGQ.
- Numeração automática por tipo e por ano (`NC 1/2026`, `REC`, `SM`, `PF`, `ELO`).
- Estados de tratamento, classificação de não conformidades (maior, menor, observação) e prazos.
- Adaptação do formulário ao tipo de registo: um elogio não exige análise de causas nem plano de ação.

**Análise de causas**

- Método dos cinco porquês, com encadeamento das respostas.
- Diagrama de Ishikawa organizado pelas seis categorias (método, mão de obra, medida, material,
  máquina, meio ambiente), com causas normalizadas e campo livre por categoria.
- Plano de ação corretiva em 5W2H.
- Vista de **análise agregada**, que cruza as causas de todos os registos para identificar as que são
  recorrentes e, por isso, sistémicas.

**Verificações automáticas**

A aplicação sinaliza, no momento do preenchimento, situações que comprometem a validade do registo:

- Fecho de um registo com ação corretiva sem verificação da eficácia.
- Eficácia declarada menos de 30 dias após a implementação da ação.
- Declaração de alterações ao SGQ sem a correspondente atualização de riscos e oportunidades.
- Eficácia afirmada sem descrição do que foi verificado.
- Prazos de implementação ultrapassados com o registo ainda em aberto.

**Catálogo de processos e documentos**

Lista editável de processos e documentos do SGQ, que alimenta os campos do formulário. Permite
acrescentar entradas novas, registar versões, e impede a remoção de entradas associadas a registos
existentes, preservando a rastreabilidade histórica.

**Painel e relatórios**

- Painel com registos em aberto, prazos ultrapassados, eficácias por verificar e tempo médio de
  tratamento.
- Relatório PDF individual por registo, para arquivo documental.
- Relatório PDF consolidado, para as entradas da revisão pela gestão (cláusula 9.3).
- Exportação para JSON (cópia de segurança integral) e para XLS (folhas de registos, de causas e de
  histórico).

**Rastreabilidade**

Registo cronológico de todas as operações — criação, alteração, eliminação, importação, exportação e
reposição — que constitui evidência de controlo da informação documentada.

## Instalação e utilização

Não há instalação. A aplicação é um ficheiro HTML único, sem dependências externas, sem servidor e sem
ligação à Internet.

1. Descarregue `analise-nc.html` a partir da secção *Releases* ou do próprio repositório.
2. Abra o ficheiro no navegador, com duplo clique.
3. No primeiro arranque, o painel propõe carregar um registo de demonstração, que pode eliminar depois.

Para utilização por uma equipa, é preferível alojar o ficheiro num servidor interno ou publicá-lo em
GitHub Pages (basta renomear o ficheiro para `index.html`), mantendo um endereço estável. Note-se, em
qualquer caso, que **os dados não são partilhados entre utilizadores**: cada navegador mantém o seu
próprio registo. Para trabalho partilhado, use o ficheiro de cópia automática numa pasta de rede como
registo de referência.

## Requisitos

| Função | Requisito | Navegadores |
|---|---|---|
| Aplicação, registos, relatórios | Navegador com suporte de `localStorage` | Chrome, Edge, Firefox, Safari |
| Importação de ficheiros `.xlsx` | `DecompressionStream` | Chrome 80+, Edge 80+, Firefox 113+, Safari 16.4+ |
| Importação de ficheiros `.csv` | — | Todos |
| Cópia automática para ficheiro | *File System Access API* | Chrome, Edge |

Onde uma destas funções não esteja disponível, a aplicação degrada de forma controlada: indica a
limitação e propõe a alternativa (importar CSV, exportar JSON manualmente).

Não utiliza bibliotecas externas, CDN, telemetria ou quaisquer pedidos de rede. A leitura de ficheiros
`.xlsx` é feita por um descompactador ZIP e um analisador de XML implementados no próprio ficheiro.

## Importação a partir do Microsoft Forms

A aplicação lê diretamente a folha exportada do Microsoft Forms, em `.xlsx` ou `.csv`, sem conversão
prévia. A correspondência das colunas é automática e cobre as 37 perguntas do formulário de origem.

Durante a importação:

- Os tipos de registo do formulário são convertidos para a taxonomia da aplicação.
- Os códigos de processos e documentos são extraídos do texto das colunas «Processo» e «Onde?
  Processos?»; o que não for código é preservado num campo de texto livre.
- As causas normalizadas são recolocadas nas categorias de Ishikawa correspondentes.
- Os códigos são atribuídos pelo ano da ocorrência, respeitando a ordem cronológica.
- Os registos coincidentes com registos já existentes são detetados e desmarcados.

Antes de gravar, é apresentada uma pré-visualização com a distribuição por tipo, os avisos de
correspondência e a escolha entre **acrescentar aos registos existentes** ou **substituir tudo e
renumerar**.

## Armazenamento e salvaguarda dos dados

Os registos ficam no armazenamento local do navegador, e **não dentro do ficheiro HTML**. Esta
distinção é importante:

**Apagam os dados**

- Limpar «cookies e outros dados de sites» nas definições de privacidade do navegador. É a causa mais
  provável, por vir pré-selecionada na caixa de limpeza do Chrome e do Edge.
- A opção «eliminar dados dos sites ao fechar o navegador», se estiver ativa.
- Reinstalar o navegador, repor o perfil, ou uma reimagem do posto de trabalho.
- No Firefox, mudar o ficheiro de pasta ou de nome, porque o armazenamento de páginas abertas a partir
  do disco é isolado por ficheiro.

**Não apagam os dados**

- Limpar apenas o histórico de navegação.
- Fechar o separador ou o navegador, ou reiniciar o computador.
- Descarregar de novo o ficheiro HTML.

Para mitigar o risco, a aplicação dispõe de três mecanismos: pedido de armazenamento persistente ao
navegador, aviso visível quando a última cópia de segurança está em atraso, e **cópia automática para
um ficheiro** à escolha do utilizador — idealmente numa pasta de rede já salvaguardada pelos serviços
informáticos. Recomenda-se que, em uso institucional, essa cópia seja tratada como o registo oficial.

## Proteção de dados

A aplicação executa integralmente no computador do utilizador. Não existe servidor, base de dados
remota, autenticação, telemetria ou qualquer transmissão de dados. Nenhuma informação introduzida sai
do equipamento, salvo por ação deliberada do utilizador ao exportar um ficheiro.

Os registos de não conformidades podem conter dados pessoais — nomes de colaboradores, de estagiários
ou de reclamantes. A responsabilidade pelo tratamento desses dados, incluindo a determinação da base de
licitude, os prazos de conservação e as medidas de segurança do suporte onde as cópias são guardadas,
cabe à organização que utiliza a aplicação, nos termos do Regulamento (UE) 2016/679. Recomenda-se o
registo de ocorrências pelo cargo ou função sempre que a identificação nominal não seja necessária.

## Correspondência com a norma

| Cláusula | Requisito | Onde é respondido |
|---|---|---|
| 7.5 | Informação documentada | Catálogo de processos e documentos; histórico de atividade |
| 9.1.3 | Análise e avaliação | Vista de análise de causas e de tendências |
| 9.2 | Auditoria interna | Origem do registo; tratamento das constatações |
| 9.3 | Revisão pela gestão | Painel e relatório PDF consolidado |
| 10.2.1 a) | Controlo e correção | Campo de correção imediata, com responsáveis e prazos |
| 10.2.1 b) | Análise da causa | Cinco porquês e diagrama de Ishikawa |
| 10.2.1 d) | Implementação da ação | Plano de ação corretiva em 5W2H |
| 10.2.1 e) | Revisão da eficácia | Verificação da eficácia, com bloqueio de fecho sem verificação |
| 10.2.2 | Informação documentada | Relatórios PDF individual e consolidado; exportações |

## Adaptação a outra organização

O catálogo de processos e documentos é editável pela interface, pelo que a aplicação se adapta a outro
sistema de gestão sem alterar o código. Para uma adaptação mais profunda, as listas de domínio estão
agrupadas no início do bloco de *script*: tipos de registo, origens, classificações, unidades, pessoas,
estados, escala de eficácia e causas de Ishikawa. O catálogo predefinido pode ser substituído na
constante `CAT_BASE`.

## Estrutura do repositório

```
.
├── analise-nc.html     # a aplicação (ficheiro único, autónomo)
├── README.md
├── CITATION.cff        # metadados de citação
├── LICENSE             # licença MIT
└── .zenodo.json        # metadados para o depósito no Zenodo
```

## Limitações conhecidas

- **Monoposto.** Não há sincronização entre utilizadores nem controlo de concorrência. Para trabalho em
  equipa, o ficheiro de cópia automática numa pasta partilhada serve de registo de referência, mas a
  edição simultânea não é suportada.
- **Sem autenticação.** Quem tiver acesso ao navegador tem acesso aos registos. A proteção depende do
  controlo de acesso ao posto de trabalho.
- **Anexos não são armazenados.** As evidências são identificadas por referência textual, não
  carregadas para a aplicação, para não esgotar o armazenamento do navegador.
- **Relatórios PDF gerados por impressão.** São produzidos pela caixa de impressão do navegador, com a
  opção «Guardar como PDF», e não por um motor de composição tipográfica.

## Como citar

Se utilizar esta aplicação em contexto académico ou institucional, cite-a através do DOI atribuído pelo
Zenodo. O ficheiro [`CITATION.cff`](CITATION.cff) contém os metadados completos e é reconhecido pelo
GitHub, que apresenta a citação formatada no painel lateral do repositório.

> Marques Teixeira, P. M. (2026). *Análise de Não Conformidades, Reclamações, Sugestões de Melhoria e
> Elogios* (versão 1.0.0) [Software]. Zenodo. https://doi.org/10.5281/zenodo.XXXXXXX

Para obter o DOI: associe o repositório ao Zenodo em <https://zenodo.org/account/settings/github/>,
publique uma *release* no GitHub e o DOI é atribuído automaticamente. Substitua depois `XXXXXXX` pelo
identificador emitido, neste ficheiro, no `CITATION.cff` e no `.zenodo.json`.

## Licença

Distribuído sob a licença MIT. Ver [`LICENSE`](LICENSE).

O programa é disponibilizado tal como está, sem garantia de qualquer espécie. A sua utilização num
sistema de gestão certificado não dispensa a validação pela organização nem a conformidade com os
procedimentos internos aplicáveis.

## Autor

**Pedro Miguel Marques Teixeira**
Coordenador da Unidade de Ensino, Unidade Local de Saúde da Guarda, E.P.E.
ORCID: [0009-0005-7035-6736](https://orcid.org/0009-0005-7035-6736)

Desenvolvido no contexto da gestão do sistema da qualidade da Unidade de Ensino e disponibilizado em
acesso aberto, para reutilização por outras unidades e serviços com sistemas de gestão equivalentes.
