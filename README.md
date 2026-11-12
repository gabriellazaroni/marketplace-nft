# NFT Marketplace

Marketplace de NFTs desenvolvido com React e TypeScript, como parte de um desafio técnico de desenvolvimento Front-end. O projeto contempla descoberta de colecionáveis digitais, autenticação de usuários, gerenciamento de favoritos, carrinho de compras, checkout e acompanhamento de pedidos.

A aplicação utiliza uma API REST simulada para representar operações de negócio, autenticação, carteiras digitais e pagamentos. As atualizações em tempo real são realizadas por meio de Socket.IO em ambiente controlado.

## Tecnologias

| Responsabilidade | Tecnologia |
|---|---|
| Interface | React |
| Linguagem | TypeScript |
| Build | Vite |
| Navegação | TanStack Router |
| Estado remoto | TanStack Query |
| Comunicação HTTP | Axios |
| Atualizações em tempo real | Socket.IO |
| Estilização | Tailwind CSS |
| Componentes | shadcn/ui |
| Validação | Zod + React Hook Form |
| Simulação de API | MSW |
| Testes automatizados | Playwright |
| Auditoria | Lighthouse |

## Executando o projeto

### Requisitos

- Node.js 22 ou superior.
- npm.
- Git.

### Instalação

Clone o repositório e acesse o diretório da aplicação:

```bash
git clone <URL_DO_REPOSITORIO>

cd nft-marketplace
```

Instale as dependências:

```bash
npm install
```

Prepare as variáveis de ambiente:

```bash
cp .env.example .env.local
```

Inicie o servidor de desenvolvimento:

```bash
npm run dev
```

A aplicação estará disponível no endereço indicado pelo Vite, normalmente `http://localhost:5173`.

## Configuração do ambiente

As variáveis de ambiente permitem controlar os recursos utilizados durante a execução.

| Variável | Descrição |
|---|---|
| `VITE_ENABLE_MOCKS` | Define se as APIs simuladas serão utilizadas. |
| `VITE_API_URL` | Endereço base da API REST. |
| `VITE_SOCKET_URL` | Endereço do serviço de comunicação em tempo real. |

O ambiente de demonstração utiliza dados simulados, dispensando a configuração de serviços externos ou credenciais reais.

## Funcionalidades

### Marketplace

- Exploração do catálogo de NFTs.
- Pesquisa por nome e características.
- Filtros combináveis e ordenação.
- Paginação integrada aos parâmetros da URL.
- Visualização detalhada dos colecionáveis.
- Gerenciamento de itens favoritos.

### Carrinho e compras

- Inclusão e remoção de NFTs.
- Controle de quantidades e disponibilidade.
- Aplicação e remoção de cupons.
- Cálculo de subtotal, descontos e taxas.
- Atualização de preços e estoque em tempo real.

### Checkout

- Identificação do colecionador.
- Seleção de carteira digital.
- Escolha da rede.
- Revisão dos valores antes da compra.
- Simulação de aprovação ou recusa do pagamento.
- Proteção contra pedidos duplicados.
- Recuperação de transações pendentes.

### Conta do colecionador

- Cadastro e autenticação.
- Gerenciamento de sessão.
- Atualização de informações pessoais.
- Alteração de senha.
- Gerenciamento de avatar.
- Cadastro e edição de carteiras.
- Histórico e consulta de pedidos.

## Simulação e cenários de teste

A camada de simulação utiliza MSW para interceptar as requisições HTTP e representar o comportamento de um backend.

Os dados são compartilhados entre os recursos da aplicação, mantendo a consistência entre catálogo, usuários, favoritos, carrinho e pedidos.

Os cenários de demonstração contemplam:

| Cenário | Comportamento |
|---|---|
| Sucesso | Operações concluídas normalmente. |
| Resultado vazio | Catálogo sem resultados correspondentes. |
| Latência | Respostas com atrasos controlados. |
| Falha de conexão | Indisponibilidade temporária da API. |
| Erro HTTP | Respostas com códigos 4xx e 5xx. |
| Sessão expirada | Necessidade de autenticação novamente. |
| Conflito de cadastro | Tentativa de registrar um e-mail existente. |
| Cupom inválido | Rejeição de códigos promocionais. |
| Alteração de preço | Atualização de valores durante a navegação. |
| Edição esgotada | Indisponibilidade de unidades para compra. |
| Pagamento recusado | Pedido não confirmado e carrinho preservado. |
| Timeout | Recuperação de pedidos utilizando idempotência. |

Os eventos de atualização são transmitidos pelo cliente Socket.IO conectado ao transporte simulado, permitindo testar reconexões, duplicidades e eventos desatualizados.

## Rotas da aplicação

| Rota | Descrição | Acesso |
|---|---|---|
| `/` | Página inicial e catálogo | Público |
| `/nfts/:nftId` | Detalhes do NFT | Público |
| `/cart` | Carrinho de compras | Público |
| `/login` | Autenticação | Público |
| `/signup` | Cadastro | Público |
| `/checkout` | Finalização da compra | Privado |
| `/orders/:orderId` | Confirmação e recibo | Privado |
| `/profile` | Perfil do colecionador | Privado |
| `/wallets` | Gerenciamento de carteiras | Privado |

As rotas privadas exigem uma sessão válida. Os parâmetros de pesquisa e navegação são preservados na URL sempre que aplicável.

## Testes e qualidade

Os testes automatizados utilizam Playwright para verificar os principais fluxos de utilização, incluindo operações bem-sucedidas, falhas de rede, validações e recuperação de estado.

As verificações contemplam:

- Navegação e pesquisa no catálogo.
- Filtros, ordenação e paginação.
- Cadastro, login e encerramento de sessão.
- Gerenciamento de favoritos.
- Persistência e atualização do carrinho.
- Processo completo de compra.
- Recuperação de pedidos pendentes.
- Atualizações recebidas pelo Socket.IO.
- Validação de formulários e acessibilidade.
- Comportamento responsivo.

O Lighthouse será utilizado para avaliar performance, acessibilidade, boas práticas e otimização para mecanismos de busca.

## Build e distribuição

Para gerar a versão otimizada:

```bash
npm run build
```

Os arquivos de produção serão disponibilizados no diretório `dist/`.

Para executar uma prévia da versão compilada:

```bash
npm run preview
```

A aplicação deverá manter a configuração de mocks habilitada no ambiente de demonstração.

## Arquitetura e organização

O código é organizado por funcionalidades, mantendo componentes, hooks, serviços e tipos próximos de seus respectivos domínios.

| Diretório | Responsabilidade |
|---|---|
| `src/app` | Configuração global, providers e roteamento. |
| `src/features` | Funcionalidades e regras específicas do negócio. |
| `src/components` | Componentes compartilhados da interface. |
| `src/services` | Comunicação com serviços externos e APIs. |
| `src/mocks` | Dados, handlers e cenários de simulação. |
| `src/hooks` | Hooks compartilhados. |
| `src/types` | Definições e contratos TypeScript. |
| `src/utils` | Funções auxiliares e utilitários. |
| `src/styles` | Estilos globais e configurações visuais. |

## Documentação técnica

A documentação complementar será organizada nos seguintes arquivos:

- `ARCHITECTURE.md` — estrutura, decisões arquiteturais e gerenciamento de estado.
- `docs/CONTRACTS.md` — endpoints REST, estruturas de dados e eventos.
- `docs/TESTING.md` — cenários automatizados e execução dos testes.
- `docs/VALIDATION.md` — resultados das verificações e auditorias.
- `docs/REQUIREMENTS.md` — relação entre os requisitos do desafio e as funcionalidades implementadas.

---

**Status:** Em desenvolvimento.

O projeto será evoluído progressivamente, priorizando a consistência arquitetural, a confiabilidade das operações e a qualidade da experiência de utilização.