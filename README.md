# 🏐 Torneio Quartetos - Sistema de Controle

Sistema web para gerenciamento de torneios de vôlei de quartetos, com interface em tempo real usando Firebase Firestore.

## Sobre o Projeto

Sistema completo para controle de torneios esportivos que permite:

- Cadastro e gerenciamento de times
- Controle de partidas e placares
- Classificação automática
- Acompanhamento em tempo real
- Interface administrativa e pública

## Funcionalidades

### Gestão de Times

- Cadastro de times com até 4 jogadores
- Listagem alfabética de jogadores
- Exclusão individual ou em lote

### Controle de Partidas

- Rodada 1: Partidas iniciais (P1 a P4)
- Rodada 2: Chaveamento baseado nos resultados da Rodada 1
- Rodada 3: Finais e disputas de posição
- Partidas opcionais P9 e P10 (7º vs 8º e 5º vs 6º)

### Sistema de Classificação

- Cálculo automático de vitórias e derrotas
- Saldo de pontos (pontos pró - pontos contra)
- Critérios de desempate:
  - Maior número de vitórias
  - Confronto direto
  - Melhor saldo de pontos

### Área Administrativa

- Login seguro
- Controle de placares
- Geração de partidas
- Configurações do torneio

## Tecnologias Utilizadas

- **Frontend:** HTML5, CSS3, JavaScript (ES6+)
- **UI Framework:** jQuery
- **Backend:** Firebase Firestore
- **Estilo:** Modern Normalize CSS
- **QR Code:** API externa

## Estrutura do Projeto

A aplicação é composta por um único arquivo `index.html` que contém toda a lógica, estilos e scripts.

O Firestore é utilizado com duas coleções principais:

- `teams`: para cadastro dos times
- `matches`: para armazenar as partidas e resultados

A aplicação possui as seguintes abas:

- Público: Informações gerais e QR Code
- Times: Lista pública de times
- Partidas: Agenda de jogos
- Classificação: Tabela do torneio
- Administração: Login e ferramentas
- Gerenciar Times: CRUD de times (área admin)
- Gerenciar Partidas: Controle de placares (área admin)

## Configuração

### Firebase Setup

O projeto requer uma configuração do Firebase. No código, há um objeto `firebaseConfig` que deve ser preenchido com as credenciais do seu projeto Firebase.

### Credenciais de Acesso

- Usuário: `admin`
- Senha: `senha123`

### Pré-requisitos

- 8 times cadastrados para gerar partidas
- Conexão com internet para Firebase

## Como Usar

### Iniciando o Torneio

1. Fazer login na aba Administração
2. Cadastrar times na aba "Gerenciar Times"
3. Gerar partidas com "Montar Rodada 1"
4. Controlar placares na aba "Gerenciar Partidas"

### Fluxo das Partidas

**Rodada 1:** Partidas P1 a P4 (definem chaves principais)  
**Rodada 2:**  
- P5: Vencedor P1 vs Vencedor P2  
- P6: Vencedor P3 vs Vencedor P4  
- P7: Perdedor P1 vs Perdedor P2  
- P8: Perdedor P3 vs Perdedor P4  

**Rodada 3:**  
- P11: Semifinal (3º vs 4º)  
- P12: Final (1º vs 2º)  
- P9/P10: Partidas opcionais (7º vs 8º e 5º vs 6º)

### Controle de Placares

- Preencher scores nos campos numéricos
- Salvar para finalizar partida
- Resetar para reabrir partida

### Recursos de Segurança

- Confirmações antes de ações destrutivas
- Validação de dados de entrada
- Proteção contra sobrescrita acidental
- Área admin com autenticação

## Regras do Torneio

- Formato: Quartetos (4 jogadores por time)  
- Partidas: 1 set de 15 pontos  
- Total: 12 partidas (P9 e P10 opcionais)  
- Critério de vitória: Melhor de 1 set

## Recursos Públicos

- QR Code para acesso rápido
- Visualização responsiva para mobile
- Atualização em tempo real
- Tabela de classificação automática

## Desenvolvimento

### Estrutura de Dados

**Time (`team`):**

- `id`: identificador único
- `name`: nome do time
- `players`: lista de jogadores
- `wins`: número de vitórias
- `scored`: pontos feitos
- `conceded`: pontos sofridos

**Partida (`match`):**

- `id`: identificador único
- `matchCode`: código da partida (P1 a P12)
- `round`: número da rodada (1, 2 ou 3)
- `teamA`: id do time A
- `teamB`: id do time B
- `scoreA`: placar do time A
- `scoreB`: placar do time B
- `status`: pendente ou finalizado
- `winner`: id do time vencedor

### Funções Principais

- `generateStructure`: Cria todas as partidas
- `prepareR2`: Monta Rodada 2 baseada nos resultados
- `prepareR3`: Monta finais baseada no ranking
- `computeRankingFromData`: Calcula classificação

### Responsividade

- Mobile-first design
- Navegação por select em dispositivos móveis
- Layout adaptativo para tablets e desktop
- Interface touch-friendly

### Solução de Problemas

**Erros Comuns:**

- "Firestore não inicializado": Verifique configuração do Firebase  
- "É necessário exatamente 8 times": Cadastre 8 times antes de gerar partidas  
- Dados não atualizando: Verifique conexão com internet

**Logs e Debug:**

- O console do navegador mostra logs detalhados
- Erros do Firebase são exibidos em alertas

## Licença

Projeto para uso interno de torneios esportivos.  
Desenvolvido para Torneio Quartetos - Sistema de controle em tempo real com Firebase Firestore.
