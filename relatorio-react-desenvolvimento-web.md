# SENAI

## Atividade 02

# React: fundamentos, arquitetura, vantagens e aplicações no mercado

**Relatório técnico sobre desenvolvimento Front-end**

*Relatório técnico apresentado como atividade acadêmica do componente curricular Desenvolvimento Web.*

| Informação | Dados |
|---|---|
| Componente curricular | Desenvolvimento Web |
| Tema | React e desenvolvimento Front-end |
| Aluno(a)/grupo | Pedro Henrqieu Campos<br>Felipe Nunes Ramalho<br>Juliana Karla Camargo da silva<br>Gustavo Leme de Castro<br>Jeniffer Camargo Oliveira |
| Turma | TADS2 |

---

## Sumário

1. [Resumo](#1-resumo)
2. [Introdução](#2-introdução)
3. [O que é React](#3-o-que-é-react)
4. [Fundamentos da programação em React](#4-fundamentos-da-programação-em-react)
5. [Renderização e arquitetura](#5-renderização-e-arquitetura)
6. [Estado, Hooks e fluxo de dados](#6-estado-hooks-e-fluxo-de-dados)
7. [Ecossistema e organização de projetos](#7-ecossistema-e-organização-de-projetos)
8. [Vantagens, limitações e aplicações no mercado](#8-vantagens-limitações-e-aplicações-no-mercado)
9. [Qualidade, acessibilidade, segurança e desempenho](#9-qualidade-acessibilidade-segurança-e-desempenho)
10. [Exemplo prático: painel de tarefas](#10-exemplo-prático-painel-de-tarefas)
11. [Conclusão](#11-conclusão)
12. [Referências](#12-referências)

---

## 1. Resumo

React é uma biblioteca JavaScript de código aberto para construção de interfaces de usuário. Sua principal ideia é decompor a interface em componentes reutilizáveis e descrever, de forma declarativa, como a tela deve aparecer para cada estado da aplicação. Quando os dados mudam, o React calcula uma nova descrição da interface e coordena a atualização do ambiente de renderização.

O React é muitas vezes chamado de framework no mercado por fazer parte de soluções completas de desenvolvimento Web. Tecnicamente, porém, ele se concentra na camada de interface e pode ser combinado com ferramentas de roteamento, estilização, testes, gerenciamento de dados e frameworks de aplicação. Essa característica oferece liberdade arquitetural, mas também exige que a equipe faça escolhas conscientes.

Este relatório apresenta os fundamentos do React, o modelo de componentes, JSX, props, estado, Hooks, reconciliação, estratégias de renderização, organização de projetos, ecossistema, aplicações profissionais e cuidados de qualidade. Ao final, é proposto um painel de tarefas que demonstra a passagem de dados, o gerenciamento de estado e a comunicação entre componentes.

**Palavras-chave:** React, JavaScript, Front-end, componentes, JSX, Hooks, interface Web.

---

## 2. Introdução

### 2.1 O problema que o React ajuda a resolver

Uma interface Web moderna não é apenas um conjunto de páginas estáticas. Ela precisa responder a cliques, entradas de formulário, filtros, carregamentos assíncronos, erros de rede, permissões, mudanças de rota e diferentes tamanhos de tela. Em uma aplicação grande, alterar manualmente cada elemento do DOM pode espalhar a lógica de apresentação por diversos arquivos e gerar inconsistências.

O React propõe um modelo no qual a interface é consequência dos dados. Em vez de escrever comandos como “encontre este elemento, altere seu texto e esconda aquele botão”, o componente declara quais elementos devem existir quando determinadas condições forem verdadeiras. Essa mudança de perspectiva é central para compreender a tecnologia: a equipe modela estados possíveis da tela e cria componentes que representam esses estados.

### 2.2 Objetivos

Este trabalho tem os seguintes objetivos:

- explicar o papel do React no desenvolvimento Front-end;
- apresentar seus principais conceitos e mecanismos;
- analisar vantagens, limitações e critérios de adoção;
- relacionar o React a aplicações e necessidades do mercado;
- demonstrar uma arquitetura de projeto com um exemplo funcional de código;
- registrar boas práticas de qualidade, acessibilidade, segurança e desempenho.

### 2.3 Metodologia

O conteúdo foi organizado como uma revisão técnica introdutória-intermediária, utilizando a documentação oficial do React como fonte principal. Foram priorizados conceitos estáveis da biblioteca, referências da documentação atual e exemplos pequenos o suficiente para explicar o fluxo de dados sem esconder a ideia principal atrás de uma grande quantidade de código.

---

## 3. O que é React

### 3.1 Biblioteca de interface, não solução completa

React fornece componentes, Hooks, APIs de renderização, regras de composição e ferramentas relacionadas. Ele não define sozinho como toda a aplicação deve tratar autenticação, roteamento, cache de dados, estilos, banco de dados ou observabilidade. Em um projeto profissional, essas decisões são feitas com bibliotecas adicionais ou com um framework que integre diversas camadas.

Essa distinção é importante porque afeta a arquitetura. Um projeto simples pode usar React com um build tool e poucas dependências. Uma aplicação que precisa de renderização no servidor, geração estática, carregamento progressivo, funções no servidor e componentes executados em ambientes diferentes pode adotar um framework de aplicação. A documentação oficial recomenda escolher a estratégia de criação de acordo com os requisitos do produto [6].

### 3.2 Versões e evolução recente

Na data de elaboração deste documento, a documentação oficial lista o React 19.3 como a versão mais recente [2]. O React 19.3 tornou estáveis recursos como `ViewTransition` e Fragment Refs, além de trazer melhorias para renderização e interação [3].

O React 19 também ampliou o suporte a Actions, formulários, atualizações assíncronas e recursos que ajudam a representar operações de dados dentro da árvore de componentes [4]. A escolha de APIs deve sempre considerar a versão usada no projeto, pois bibliotecas do ecossistema podem ter compatibilidade e recomendações diferentes.

### 3.3 Modelo mental

O modelo mental do React pode ser resumido em quatro ideias:

1. **A interface é composta por componentes.** Cada componente representa uma parte da experiência visual.
2. **Props configuram componentes.** O componente pai envia valores e funções para o componente filho.
3. **Estado representa memória mutável da interface.** Quando o estado muda, a interface pode ser renderizada novamente.
4. **A renderização deve ser previsível.** Componentes e Hooks devem ser puros, ou seja, produzir o mesmo resultado quando recebem os mesmos dados, sem efeitos colaterais durante o cálculo da interface [7].

---

## 4. Fundamentos da programação em React

### 4.1 Componentes e composição

Um componente React é normalmente uma função JavaScript que retorna JSX. Ele pode ser pequeno, como um botão, ou representar uma tela inteira. A composição ocorre quando componentes menores são combinados para formar componentes maiores.

```jsx
function Button({ children, variant = "primary" }) {
  return (
    <button className={`button button-${variant}`}>
      {children}
    </button>
  );
}

export default function WelcomeCard() {
  return (
    <section className="card">
      <h1>Bem-vindo ao painel</h1>
      <p>Consulte suas atividades e acompanhe o progresso.</p>
      <Button>Ver tarefas</Button>
    </section>
  );
}
```

Nesse exemplo, `Button` não precisa conhecer o texto que exibirá. Ele recebe `children`, uma prop especial que representa o conteúdo colocado dentro da abertura e do fechamento do componente. A mesma implementação pode ser usada com textos diferentes e variantes visuais distintas.

A composição é preferível à criação de componentes gigantes com muitas condições. Um componente grande pode funcionar, mas tende a concentrar responsabilidades, dificultar testes e aumentar o risco de mudanças em uma parte afetarem outra. A divisão deve ser guiada por responsabilidade e reutilização, não por uma regra mecânica de criar um arquivo para cada linha de JSX.

### 4.2 JSX

JSX permite escrever uma estrutura semelhante a HTML no código JavaScript. Ele não é interpretado diretamente pelo navegador: o processo de build transforma essa sintaxe em código que o React consegue utilizar. Entre suas regras estão o uso de `className` em vez de `class`, o fechamento de elementos e a necessidade de retornar um elemento raiz ou um Fragment.

```jsx
function UserStatus({ user }) {
  if (!user) {
    return <p>Usuário não autenticado.</p>;
  }

  return (
    <p>
      Olá, <strong>{user.name}</strong>!
    </p>
  );
}
```

Chaves `{}` permitem inserir expressões JavaScript no JSX. Assim, o componente consegue exibir dados, executar condições e renderizar listas. A lógica deve permanecer legível: quando um trecho de transformação de dados crescer demais, é melhor extraí-lo para uma função ou Hook.

### 4.3 Props e fluxo unidirecional

Props são semelhantes aos argumentos de uma função. Um componente pai passa dados para um componente filho, e o filho os utiliza para renderizar a própria interface. Esse fluxo é chamado de unidirecional porque os dados descem na árvore de componentes.

```jsx
function ProductCard({ product, onAddToCart }) {
  return (
    <article>
      <h2>{product.name}</h2>
      <p>R$ {product.price.toFixed(2)}</p>
      <button onClick={() => onAddToCart(product.id)}>
        Adicionar ao carrinho
      </button>
    </article>
  );
}
```

A função `onAddToCart` é uma callback enviada pelo pai. O componente filho não precisa saber como o carrinho é armazenado; ele apenas comunica a intenção do usuário. Essa separação reduz o acoplamento e permite reutilizar `ProductCard` em diferentes telas.

### 4.4 Listas e identidade com `key`

Para renderizar uma lista, o código normalmente utiliza `map`. Cada item deve receber uma `key` estável e única dentro daquela lista. O React usa essa identidade para entender quais itens foram mantidos, adicionados, removidos ou reordenados.

```jsx
function ProductList({ products }) {
  return (
    <ul>
      {products.map((product) => (
        <li key={product.id}>{product.name}</li>
      ))}
    </ul>
  );
}
```

Usar o índice do array como `key` pode gerar comportamentos inesperados quando a lista muda de ordem ou recebe itens no início. Um identificador do domínio, como `product.id`, é normalmente uma escolha melhor.

---

## 5. Renderização e arquitetura

### 5.1 O que acontece durante uma atualização

Quando uma interação altera o estado, o React pode chamar novamente o componente para obter uma nova descrição da interface. Em seguida, compara essa descrição com a anterior e aplica ao ambiente de renderização as alterações necessárias. No navegador, o ambiente normalmente é o DOM.

Esse processo costuma ser explicado com três etapas:

1. **Disparo:** uma ação, como um evento ou uma resposta de rede, solicita uma atualização.
2. **Renderização:** o React chama componentes e calcula o que a interface deveria exibir.
3. **Commit:** o React aplica as mudanças ao DOM ou a outro ambiente de renderização.

A renderização não deve produzir efeitos colaterais, como alterar uma variável externa, gravar no `localStorage` ou iniciar uma conexão. Esses trabalhos pertencem a eventos ou a efeitos controlados. Manter essa separação permite que o React analise e reprocesse a interface com segurança.

### 5.2 SPA, SSR, SSG e RSC

Existem estratégias diferentes para entregar uma aplicação React:

| Estratégia | Característica | Benefícios | Cuidados |
|---|---|---|---|
| SPA | Um documento inicial e atualizações no cliente | Simplicidade e boa interatividade após o carregamento | Pode exigir otimização do carregamento inicial e SEO adicional |
| SSR | O servidor gera HTML para cada requisição | HTML inicial rápido e possibilidade de conteúdo personalizado | Infraestrutura e hidratação são mais complexas |
| SSG | Páginas são geradas durante o build | Arquivos rápidos de distribuir e cachear | Conteúdo altamente dinâmico exige estratégia adicional |
| RSC | Componentes podem executar em ambiente separado do cliente | Reduz JavaScript enviado e aproxima renderização da camada de dados | Exige suporte do bundler/framework e separação clara entre servidor e cliente |

A documentação do React destaca que um build tool isolado normalmente começa com uma aplicação de página única. Quando o projeto precisa de SSR, SSG ou React Server Components, a equipe deve adotar uma solução que implemente esses padrões [6][9].

### 5.3 Server Components e Client Components

React Server Components são componentes executados em um ambiente separado do aplicativo do cliente. Eles podem ler dados no servidor ou durante o build e não são enviados ao navegador como componentes interativos. Por isso, não podem usar APIs como `useState` para controlar interação local.

Quando uma parte precisa de eventos, estado ou APIs do navegador, ela deve ser implementada como Client Component dentro da arquitetura escolhida. A divisão não é simplesmente “mais rápido no servidor”: ela muda onde o código roda, quais dados pode acessar e qual JavaScript chega ao usuário. A documentação alerta que a implementação de RSC depende de bundlers e frameworks, e que APIs de integração podem evoluir [8].

### 5.4 Suspense e carregamento progressivo

`Suspense` permite declarar um estado de espera enquanto uma parte da árvore não está pronta. A aplicação pode mostrar um skeleton ou uma mensagem de carregamento para uma região específica, evitando bloquear visualmente toda a tela.

```jsx
import { Suspense } from "react";

export default function Dashboard() {
  return (
    <main>
      <h1>Dashboard</h1>
      <Suspense fallback={<p>Carregando indicadores...</p>}>
        <Metrics />
      </Suspense>
    </main>
  );
}
```

O uso correto depende do framework e da forma como os dados são carregados. O fallback também precisa ser acessível e representar uma espera real; colocar `Suspense` indiscriminadamente não melhora automaticamente o desempenho.

---

## 6. Estado, Hooks e fluxo de dados

### 6.1 Estado mínimo e derivação

Estado deve representar apenas dados que variam e precisam ser lembrados. Informações que podem ser calculadas a partir de props e estado existente não precisam ser armazenadas novamente. Essa regra evita duplicidade e reduz a possibilidade de dois valores ficarem inconsistentes.

Por exemplo, uma lista filtrada não precisa necessariamente ser outro estado. Se a aplicação já possui `tasks` e `filter`, a lista visível pode ser calculada:

```jsx
const visibleTasks = tasks.filter((task) => {
  if (filter === "done") return task.done;
  if (filter === "pending") return !task.done;
  return true;
});
```

O guia oficial “Thinking in React” recomenda identificar o menor conjunto completo de estado e calcular os demais valores sob demanda [10].

### 6.2 `useState` e atualizações

`useState` declara uma variável de estado e uma função que solicita sua atualização. O valor de estado representa a memória do componente entre renderizações.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  function increment() {
    setCount((current) => current + 1);
  }

  return <button onClick={increment}>Cliques: {count}</button>;
}
```

A forma funcional `setCount((current) => current + 1)` é útil quando o novo valor depende do anterior. Para objetos e arrays, deve-se criar uma nova referência em vez de alterar diretamente o valor existente.

```jsx
setTasks((currentTasks) =>
  currentTasks.map((task) =>
    task.id === id ? { ...task, done: !task.done } : task
  )
);
```

### 6.3 `useReducer` para lógica complexa

Quando há muitos tipos de ação ou regras de atualização, `useReducer` pode centralizar as transições de estado. O componente envia uma ação; o reducer calcula o próximo estado.

```jsx
function tasksReducer(tasks, action) {
  switch (action.type) {
    case "added":
      return [...tasks, action.task];
    case "toggled":
      return tasks.map((task) =>
        task.id === action.id ? { ...task, done: !task.done } : task
      );
    case "removed":
      return tasks.filter((task) => task.id !== action.id);
    default:
      throw new Error(`Ação desconhecida: ${action.type}`);
  }
}
```

Esse padrão facilita testes porque o reducer pode ser testado como uma função pura, sem renderizar componentes ou depender do navegador.

### 6.4 `useEffect` e sistemas externos

Effects servem para sincronizar um componente com algo externo ao React, como uma conexão, uma API do navegador, um player de vídeo ou uma assinatura de eventos. Eles não devem ser usados apenas para transformar dados que poderiam ser calculados durante a renderização.

```jsx
import { useEffect, useState } from "react";

function useOnlineStatus() {
  const [isOnline, setIsOnline] = useState(navigator.onLine);

  useEffect(() => {
    function handleOnline() { setIsOnline(true); }
    function handleOffline() { setIsOnline(false); }

    window.addEventListener("online", handleOnline);
    window.addEventListener("offline", handleOffline);

    return () => {
      window.removeEventListener("online", handleOnline);
      window.removeEventListener("offline", handleOffline);
    };
  }, []);

  return isOnline;
}
```

O retorno do efeito realiza a limpeza. Isso é essencial para evitar listeners duplicados, conexões abertas e atualizações em componentes que já foram removidos. A documentação oficial chama atenção para a execução extra de setup e cleanup em desenvolvimento, justamente para revelar efeitos sem limpeza adequada [11].

### 6.5 `useContext`, refs e Hooks personalizados

`useContext` evita passar uma prop por muitos níveis quando vários componentes precisam de uma mesma informação, como tema, idioma ou usuário autenticado. Ele não deve virar um depósito indiscriminado de todo o estado da aplicação: quanto mais dados globais existem, mais difícil pode ser prever quais componentes serão atualizados.

`useRef` guarda um valor entre renderizações sem causar nova renderização quando seu campo `current` muda. É adequado para referências a elementos DOM, identificadores de temporizadores e integração com bibliotecas imperativas. Não é um substituto automático para estado.

Hooks personalizados extraem lógica, não necessariamente interface. Um Hook como `useOnlineStatus`, `useDebouncedValue` ou `useTasks` pode ser usado por vários componentes e esconder detalhes de eventos, requisições e limpeza.

### 6.6 Regras de Hooks

As principais regras são:

- chamar Hooks somente no nível superior do componente ou de outro Hook;
- não chamar Hooks dentro de `if`, `for`, `while`, callbacks ou funções comuns;
- chamar Hooks somente em componentes React ou Hooks personalizados;
- preservar a ordem de chamadas entre renderizações.

O plugin `eslint-plugin-react-hooks` ajuda a verificar essas regras e outras recomendações. O objetivo não é apenas padronizar estilo: o React depende da ordem consistente dos Hooks para associar cada chamada ao estado correto [12].

---

## 7. Ecossistema e organização de projetos

### 7.1 Ferramentas complementares

React cobre a camada de interface, enquanto projetos reais costumam acrescentar soluções para diferentes necessidades:

| Necessidade | Possíveis soluções | Pergunta arquitetural |
|---|---|---|
| Build e desenvolvimento | Vite, Rsbuild, Next.js e outros | Como o código será compilado e entregue? |
| Rotas | React Router ou roteador integrado ao framework | Quais URLs, layouts e permissões existem? |
| Dados remotos | `fetch`, TanStack Query e soluções do framework | Onde ficam cache, loading e erros? |
| Estado global | Context, reducer, Zustand, Redux e outros | O dado é realmente global ou pode ficar mais próximo do uso? |
| Formulários | APIs nativas, bibliotecas de formulário e validação | Como validar, enviar e exibir erros? |
| Estilos | CSS, CSS Modules, Tailwind, CSS-in-JS | Como manter consistência e responsividade? |
| Testes | Vitest/Jest, Testing Library, Playwright/Cypress | O comportamento crítico está protegido? |

Não existe uma combinação universalmente correta. A decisão deve considerar tamanho do time, experiência, requisitos de deploy, necessidade de SSR, vida útil do produto e custo de manutenção.

### 7.2 Estrutura sugerida

Uma organização por domínio pode ser mais sustentável do que separar todo o projeto apenas por tipo de arquivo:

```text
src/
  app/
    App.jsx
    routes.jsx
  components/
    Button/
    Modal/
  features/
    tasks/
      components/
      hooks/
      services/
      tasksReducer.js
      tasksApi.js
  lib/
    httpClient.js
  styles/
    globals.css
  main.jsx
```

Nesse modelo, regras relacionadas a tarefas permanecem próximas, enquanto componentes verdadeiramente genéricos ficam em uma área compartilhada. A estrutura pode mudar conforme o projeto; o princípio é tornar dependências e responsabilidades fáceis de localizar.

### 7.3 Fluxo de uma requisição

Em uma aplicação que salva dados em uma API, o fluxo pode ser representado assim:

```text
Usuário -> evento do componente -> função de aplicação
       -> serviço HTTP -> API/banco de dados
       -> resposta -> atualização de estado
       -> nova renderização -> interface atualizada
```

O componente visual não precisa conter todos os detalhes de HTTP. Um serviço ou Hook pode cuidar de estados de carregamento, cancelamento, erros e transformação da resposta. Essa separação facilita trocar a API, simular respostas em testes e reutilizar a mesma regra em mais de uma tela.

---

## 8. Vantagens, limitações e aplicações no mercado

### 8.1 Vantagens

**Reutilização.** Componentes e Hooks reduzem duplicação e permitem construir uma linguagem visual consistente.

**Composição.** Interfaces complexas podem ser formadas por partes menores, cada uma com responsabilidade bem definida.

**Fluxo de dados explícito.** Props e callbacks tornam a comunicação entre componentes visível no código.

**Adoção gradual.** A documentação destaca que o React pode ser adicionado a uma página existente ou usado como base de uma aplicação maior [5].

**Flexibilidade.** A equipe pode escolher ferramentas adequadas para rotas, dados, estilos e implantação, em vez de ficar presa a uma solução única.

**Ecossistema profissional.** Há ferramentas para depuração, linting, testes, análise de desempenho e integração com frameworks.

**Evolução para diferentes ambientes.** Além do navegador, o modelo de componentes pode ser aplicado a outras plataformas, desde que exista um renderer apropriado.

### 8.2 Limitações

**Decisões distribuídas.** O React não resolve sozinho toda a arquitetura do produto. Uma equipe inexperiente pode acumular bibliotecas sem critérios claros.

**Curva de aprendizagem.** Além de JavaScript, o estudante precisa compreender JSX, composição, estado, efeitos, imutabilidade, renderização e ferramentas de build.

**Complexidade acidental.** Componentes muito grandes, estado global excessivo, efeitos mal definidos e dependências circulares tornam a aplicação difícil de manter.

**Custo de desempenho.** Uma interface interativa pode enviar mais JavaScript ao cliente e executar mais trabalho no navegador. Code splitting, renderização adequada, imagens otimizadas e medição real são necessários.

**Mudanças no ecossistema.** Bibliotecas e recomendações evoluem. Atualizações devem ser planejadas, testadas e acompanhadas pela documentação e pelos changelogs oficiais.

### 8.3 Aplicações profissionais

React é adequado para:

- lojas virtuais e catálogos com busca e filtros;
- dashboards financeiros, industriais e administrativos;
- sistemas internos com permissões e fluxos de aprovação;
- plataformas educacionais e ambientes de aprendizagem;
- produtos SaaS com múltiplas áreas autenticadas;
- editores, calendários, quadros Kanban e ferramentas colaborativas;
- portais e sites que combinam conteúdo, personalização e interação;
- aplicações móveis quando combinado com React Native.

Em todos esses casos, a tecnologia é apenas uma parte da solução. A experiência final depende também do design, da API, do banco de dados, da observabilidade, da infraestrutura e da qualidade do processo de desenvolvimento.

---

## 9. Qualidade, acessibilidade, segurança e desempenho

### 9.1 Testes

Testes devem verificar comportamentos observáveis, não detalhes internos que podem mudar durante uma refatoração. Uma estratégia equilibrada inclui:

- **testes unitários:** reducers, funções de validação e transformações;
- **testes de componente:** interação com botões, formulários, estados de erro e carregamento;
- **testes de integração:** comunicação entre tela, serviço e estado;
- **testes End-to-End:** fluxos essenciais do ponto de vista do usuário.

Exemplo de teste de um reducer:

```js
test("alterna uma tarefa pelo id", () => {
  const initial = [{ id: 1, title: "Estudar React", done: false }];

  const result = tasksReducer(initial, {
    type: "toggled",
    id: 1,
  });

  expect(result[0].done).toBe(true);
  expect(initial[0].done).toBe(false);
});
```

O último `expect` verifica que o estado anterior não foi alterado, preservando a imutabilidade.

### 9.2 Acessibilidade

React não torna uma interface acessível automaticamente. A equipe precisa utilizar HTML semântico, labels associados a campos, foco visível, ordem de tabulação coerente, mensagens de erro compreensíveis, contraste suficiente e alternativas para conteúdo não textual.

```jsx
<label htmlFor="task-title">Título da tarefa</label>
<input
  id="task-title"
  name="title"
  aria-describedby="title-help"
  required
/>
<small id="title-help">Use até 80 caracteres.</small>
```

Componentes customizados não devem substituir elementos nativos sem necessidade. Um botão HTML, por exemplo, já possui comportamento de teclado e semântica que uma `div` com `onClick` não oferece automaticamente.

### 9.3 Segurança

JSX escapa valores de texto por padrão, o que reduz riscos comuns de injeção ao exibir conteúdo recebido. Isso não elimina a necessidade de validar dados no servidor, controlar autorização e tratar entradas não confiáveis.

Cuidados importantes incluem:

- não inserir HTML arbitrário sem sanitização rigorosa;
- não guardar segredos ou chaves privadas no bundle do cliente;
- validar autorização no servidor, mesmo que a interface esconda botões;
- proteger requisições contra abuso e tratar respostas inesperadas;
- manter dependências atualizadas e revisar pacotes de terceiros;
- não confiar em dados armazenados no navegador como fonte de segurança.

### 9.4 Desempenho

O desempenho deve ser medido, não presumido. Algumas estratégias são:

- dividir o código por rota ou funcionalidade;
- adiar componentes não essenciais;
- reduzir renderizações causadas por estado mal posicionado;
- manter listas grandes virtualizadas quando necessário;
- otimizar imagens e fontes;
- evitar cálculos caros a cada renderização;
- usar `memo`, `useMemo` e `useCallback` somente quando a medição justificar;
- analisar o bundle e o desempenho real em dispositivos móveis.

O React Compiler, documentado como ferramenta de otimização em tempo de build, pode reduzir a necessidade de memoização manual em cenários compatíveis [2]. Ainda assim, ele não corrige consultas lentas, componentes mal desenhados, imagens pesadas ou problemas no servidor.

---

## 10. Exemplo prático: painel de tarefas

### 10.1 Requisitos do projeto

Será desenvolvido conceitualmente um painel para uma equipe escolar. O usuário deve conseguir:

1. visualizar todas as tarefas;
2. filtrar tarefas por “todas”, “pendentes” ou “concluídas”;
3. cadastrar uma tarefa com título e prioridade;
4. marcar uma tarefa como concluída;
5. remover uma tarefa;
6. receber estados claros de carregamento e erro quando houver API.

### 10.2 Modelo de dados

```js
const task = {
  id: "task-001",
  title: "Entregar relatório de React",
  priority: "high",
  done: false,
  createdAt: "2026-09-16T18:00:00.000Z",
};
```

O `id` identifica o registro. `done` representa um estado booleano simples. A data pode ser usada para ordenação, histórico ou exibição formatada. Em uma aplicação real, validações deveriam ocorrer no formulário e também no servidor.

### 10.3 Arquitetura de componentes

```text
App
├── Header
├── TaskForm
├── FilterBar
└── TaskList
    └── TaskItem
```

| Componente | Responsabilidade |
|---|---|
| `App` | Mantém o estado principal e coordena ações. |
| `Header` | Exibe o título e um resumo da quantidade de tarefas. |
| `TaskForm` | Valida dados e solicita a criação de uma tarefa. |
| `FilterBar` | Permite selecionar o filtro atual. |
| `TaskList` | Recebe a lista visível e renderiza os itens. |
| `TaskItem` | Exibe uma tarefa e dispara conclusão ou remoção. |

### 10.4 Estado principal

```jsx
import { useMemo, useReducer, useState } from "react";

const initialTasks = [
  { id: "1", title: "Ler a documentação", priority: "medium", done: false },
  { id: "2", title: "Revisar o código", priority: "high", done: true },
];

function tasksReducer(tasks, action) {
  switch (action.type) {
    case "added":
      return [...tasks, action.task];
    case "toggled":
      return tasks.map((task) =>
        task.id === action.id ? { ...task, done: !task.done } : task
      );
    case "removed":
      return tasks.filter((task) => task.id !== action.id);
    default:
      return tasks;
  }
}

export default function App() {
  const [tasks, dispatch] = useReducer(tasksReducer, initialTasks);
  const [filter, setFilter] = useState("all");

  const visibleTasks = useMemo(() => {
    if (filter === "done") return tasks.filter((task) => task.done);
    if (filter === "pending") return tasks.filter((task) => !task.done);
    return tasks;
  }, [tasks, filter]);

  function addTask(title, priority) {
    dispatch({
      type: "added",
      task: {
        id: crypto.randomUUID(),
        title,
        priority,
        done: false,
      },
    });
  }

  return (
    <main>
      <h1>Painel de tarefas</h1>
      <TaskForm onAdd={addTask} />
      <FilterBar value={filter} onChange={setFilter} />
      <TaskList
        tasks={visibleTasks}
        onToggle={(id) => dispatch({ type: "toggled", id })}
        onRemove={(id) => dispatch({ type: "removed", id })}
      />
    </main>
  );
}
```

Esse componente demonstra alguns princípios importantes:

- o estado fica no ancestral comum dos componentes que precisam dele;
- o reducer centraliza as transições possíveis;
- a lista filtrada é derivada, não duplicada em outro estado;
- callbacks são passadas para componentes filhos;
- a tarefa recebe uma chave estável baseada em um identificador;
- a atualização cria novos arrays e objetos, sem modificar o estado anterior.

### 10.5 Lista e item

```jsx
function TaskList({ tasks, onToggle, onRemove }) {
  if (tasks.length === 0) {
    return <p role="status">Nenhuma tarefa encontrada.</p>;
  }

  return (
    <ul aria-label="Lista de tarefas">
      {tasks.map((task) => (
        <TaskItem
          key={task.id}
          task={task}
          onToggle={onToggle}
          onRemove={onRemove}
        />
      ))}
    </ul>
  );
}

function TaskItem({ task, onToggle, onRemove }) {
  return (
    <li>
      <label>
        <input
          type="checkbox"
          checked={task.done}
          onChange={() => onToggle(task.id)}
        />
        <span>{task.title}</span>
      </label>
      <span aria-label={`Prioridade ${task.priority}`}>
        {task.priority}
      </span>
      <button type="button" onClick={() => onRemove(task.id)}>
        Remover
      </button>
    </li>
  );
}
```

O estado vazio usa `role="status"` para indicar uma mudança informativa. O botão tem `type="button"` para não enviar um formulário acidentalmente. A informação de prioridade recebe uma descrição acessível, e a ação de remoção é explícita.

### 10.6 Formulário e validação

```jsx
import { useState } from "react";

function TaskForm({ onAdd }) {
  const [title, setTitle] = useState("");
  const [priority, setPriority] = useState("medium");
  const [error, setError] = useState("");

  function handleSubmit(event) {
    event.preventDefault();
    const normalizedTitle = title.trim();

    if (normalizedTitle.length < 3) {
      setError("Digite um título com pelo menos 3 caracteres.");
      return;
    }

    onAdd(normalizedTitle, priority);
    setTitle("");
    setError("");
  }

  return (
    <form onSubmit={handleSubmit} noValidate>
      <label htmlFor="task-title">Nova tarefa</label>
      <input
        id="task-title"
        value={title}
        onChange={(event) => setTitle(event.target.value)}
        aria-invalid={Boolean(error)}
        aria-describedby={error ? "task-error" : undefined}
      />

      <label htmlFor="task-priority">Prioridade</label>
      <select
        id="task-priority"
        value={priority}
        onChange={(event) => setPriority(event.target.value)}
      >
        <option value="low">Baixa</option>
        <option value="medium">Média</option>
        <option value="high">Alta</option>
      </select>

      {error && <p id="task-error" role="alert">{error}</p>}
      <button type="submit">Adicionar tarefa</button>
    </form>
  );
}
```

O formulário é controlado pelo estado do componente. A validação ocorre antes de chamar `onAdd`, e a mensagem é relacionada ao campo por `aria-describedby`. Em produção, a API deve repetir as validações e responder com erros estruturados, pois a validação no cliente não é uma barreira de segurança.

### 10.7 Evolução para uma aplicação real

Para transformar o exemplo em um produto, seria necessário acrescentar:

1. persistência em uma API com autenticação;
2. estados de `loading`, `success` e `error`;
3. cancelamento de requisições e tratamento de concorrência;
4. testes do reducer, do formulário e dos fluxos de usuário;
5. paginação ou virtualização para muitas tarefas;
6. feedback visual acessível após criar, editar ou remover;
7. controle de autorização no servidor;
8. métricas de desempenho e logs sem expor dados sensíveis.

O ponto principal é que React organiza a interface, mas a solução completa envolve também modelagem de dados, contratos de API, segurança, infraestrutura e processo de qualidade.

---

## 11. Conclusão

React é uma tecnologia relevante para o desenvolvimento Front-end porque oferece um modelo consistente para construir interfaces a partir de componentes e estados. JSX aproxima a estrutura visual da lógica que a produz, props tornam o fluxo de dados explícito e Hooks permitem encapsular estado, efeitos e lógica reutilizável.

Seu maior benefício não é apenas escrever menos código de DOM. A contribuição mais importante é fornecer um modelo de organização: a equipe descreve estados da interface, compõe componentes e estabelece responsabilidades claras. Esse modelo favorece manutenção, testes e evolução quando o produto cresce.

Ao mesmo tempo, React não elimina decisões difíceis. É preciso escolher como tratar rotas, dados remotos, autenticação, estilos, renderização e testes. Também é necessário controlar dependências, preservar acessibilidade, medir desempenho e validar segurança no servidor. A flexibilidade da biblioteca pode ser uma vantagem ou uma fonte de complexidade, dependendo da disciplina arquitetural da equipe.

O painel de tarefas mostrou como esses princípios se conectam em um projeto Web: o componente pai mantém o estado, o reducer organiza as ações, a lista deriva os dados visíveis, os filhos recebem props e callbacks, e o formulário controla sua própria entrada. Esse padrão pode ser ampliado para sistemas reais, desde que seja acompanhado por persistência, testes, observabilidade e requisitos de negócio bem definidos.

Portanto, React é uma escolha sólida para aplicações interativas, especialmente quando a organização por componentes e a reutilização de interface são importantes. A escolha final deve considerar a complexidade do produto, a experiência do time, a necessidade de renderização no servidor e o custo de manutenção ao longo do tempo.

---

## 12. Referências

1. REACT TEAM. *Quick Start*. Documentação oficial do React. Disponível em: <https://react.dev/learn>. Acesso em: 16 set. 2026.
2. REACT TEAM. *React Versions*. Documentação oficial do React. Disponível em: <https://react.dev/versions>. Acesso em: 16 set. 2026.
3. REACT TEAM. *React 19.3*. Blog oficial. 9 set. 2026. Disponível em: <https://react.dev/blog/2026/09/09/react-19-3>. Acesso em: 16 set. 2026.
4. REACT TEAM. *React v19*. Blog oficial. 5 dez. 2024. Disponível em: <https://react.dev/blog/2024/12/05/react-19>. Acesso em: 16 set. 2026.
5. REACT TEAM. *Installation*. Documentação oficial do React. Disponível em: <https://react.dev/learn/installation>. Acesso em: 16 set. 2026.
6. REACT TEAM. *Creating a React App*. Documentação oficial do React. Disponível em: <https://react.dev/learn/creating-a-react-app>. Acesso em: 16 set. 2026.
7. REACT TEAM. *Rules of React*. Documentação oficial do React. Disponível em: <https://react.dev/reference/rules>. Acesso em: 16 set. 2026.
8. REACT TEAM. *Server Components*. Documentação oficial do React. Disponível em: <https://react.dev/reference/rsc/server-components>. Acesso em: 16 set. 2026.
9. REACT TEAM. *Build a React app from Scratch*. Documentação oficial do React. Disponível em: <https://react.dev/learn/build-a-react-app-from-scratch>. Acesso em: 16 set. 2026.
10. REACT TEAM. *Thinking in React*. Documentação oficial do React. Disponível em: <https://react.dev/learn/thinking-in-react>. Acesso em: 16 set. 2026.
11. REACT TEAM. *Escape Hatches*. Documentação oficial do React. Disponível em: <https://react.dev/learn/escape-hatches>. Acesso em: 16 set. 2026.
12. REACT TEAM. *Rules of Hooks*. Documentação oficial do React. Disponível em: <https://react.dev/reference/rules/rules-of-hooks>. Acesso em: 16 set. 2026.
