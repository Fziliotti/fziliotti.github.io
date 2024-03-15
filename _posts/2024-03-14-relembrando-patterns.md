---
title: "Relembrando Patterns: Singleton, Proxy, Prototype, Observer..."
author: fziliotti
date: 2024-03-14 04:33:00 +0800
categories: ["Desenvolvimento"]
tags: [frontend]
---

## Introdução

Me deu vontade de relembrar alguns patterns, já que "relembrar é viver". Nada melhor do que ler e rever as anotações do site https://www.patterns.dev/#patterns.

Deixarei aqui o resumo simplificado que anotei ao longo dos estudos, as implementações e exemplos podem ser facilmente pesquisadas ou perguntadas ao papai google ou ao primo ChatGPT.


## Patterns:

**Singleton Pattern**:

- Uma instância única, controla o acesso,
- Útil quando uma única instância é necessária,
- Como gerenciadores de logs ou conexões.

**Proxy Pattern**:
- Controla o acesso a um objeto,
- Útil para adicionar funcionalidades extras,
- Como cache, validação ou segurança.

**Prototype Pattern**:
- Cria novos objetos usando protótipos,
- Útil quando muitas instâncias são necessárias,
- Como na criação de objetos semelhantes.

**Observer Pattern**:
- Um objeto observa mudanças em outro,
- Útil para notificar dependências,
- Como atualizações em interfaces de usuário.

**Module Pattern**:
- Encapsula código em módulos independentes,
- Útil para organizar e proteger o código,
- Como em aplicações JavaScript modulares.

**Factory Pattern**:
- Cria objetos sem especificar a classe exata,
- Útil para criar famílias de objetos relacionados,
- Como em casos de fabricação de componentes.

**Mediator/Middleware Pattern**:
- Promove comunicação entre objetos,
- Útil para desacoplar componentes,
- Como em aplicações com múltiplos agentes interagindo.

## Performance

**Import on Visibility**:
- Importa recursos de forma condicional com base na visibilidade da página,
- Útil para carregar recursos apenas quando a página estiver visível,
- Como em imagens ou vídeos que estão abaixo da linha de visão inicial.

**Import on Interaction**:
- Importa recursos de forma assíncrona quando uma interação é detectada,
- Útil para carregar recursos apenas quando necessário,
- Como em componentes que são carregados após uma interação do usuário.

**Route Based Splitting**:
- Divide o código com base nas rotas da aplicação,
- Útil para carregar apenas o código necessário para cada rota,
- Como em aplicações de página única (SPA) com várias rotas.

**Bundle Splitting**:
- Divide o código em bundles menores,
- Útil para carregar apenas o código necessário em cada página,
- Como em aplicações com várias páginas ou componentes grandes.

**Tree Shaking**:
- Remove código não utilizado do bundle final,
- Útil para reduzir o tamanho do arquivo JavaScript,
- Como em bibliotecas e frameworks que possuem muitas funcionalidades.

**Preload**:
- Carrega recursos antes que sejam necessários,
- Útil para melhorar o tempo de carregamento da página,
- Como em recursos críticos para o carregamento inicial da página.

**Prefetch**:
- Carrega recursos em segundo plano para páginas futuras,
- Útil para acelerar a navegação entre páginas,
- Como em links de navegação ou botões que levam a páginas subsequentes.


## Outras técnicas e temas relacionados:

### Lazy Loading:

1. **Lazy Loading de Imagens**:
   - Carrega imagens apenas quando elas estão prestes a entrar na visão do usuário.
   - Reduz o tempo de carregamento inicial da página, especialmente em páginas com muitas imagens.
   - Melhora a experiência do usuário, evitando que o conteúdo seja bloqueado enquanto as imagens estão sendo baixadas.

2. **Lazy Loading de Vídeos**:
   - Adia o carregamento de vídeos até que sejam visíveis na tela do usuário.
   - Evita o consumo excessivo de largura de banda e recursos do dispositivo.
   - Permite que a página seja renderizada mais rapidamente, aumentando a percepção de velocidade pelo usuário.

3. **Componentes Lazy Loading**:
   - Carrega componentes de interface do usuário, como modais ou seções de conteúdo, sob demanda.
   - Reduz o tamanho inicial do pacote JavaScript, melhorando o tempo de carregamento da página.
   - Permite uma experiência de usuário mais fluida, carregando apenas o conteúdo necessário conforme necessário.

### Data Compression:
1. **Compressão de Imagens**:
   - Utiliza técnicas de compressão de imagem, como JPEG e PNG, para reduzir o tamanho dos arquivos.
   - Diminui o tempo de carregamento da página, especialmente em sites com muitas imagens.
   - Mantém a qualidade visual aceitável, mesmo após a compressão.

2. **Minificação de CSS e JavaScript**:
   - Remove espaços em branco, comentários e caracteres desnecessários dos arquivos CSS e JavaScript.
   - Reduz o tamanho dos arquivos, melhorando o tempo de carregamento da página.
   - Acelera o processamento e a renderização do código pelo navegador.

3. **Compressão de Texto**:
   - Utiliza algoritmos de compressão, como gzip ou Brotli, para compactar o texto enviado pelo servidor.
   - Reduz a quantidade de dados transferidos entre o servidor e o navegador, economizando largura de banda.
   - Melhora significativamente o tempo de carregamento da página, especialmente em conexões de internet mais lentas.

### Caching:
1. **Cache do Navegador**:
   - Armazena em cache recursos estáticos, como CSS, JavaScript, imagens e fontes, no navegador do usuário.
   - Evita solicitações repetidas ao servidor, reduzindo o tempo de carregamento da página e a carga no servidor.
   - Configura cabeçalhos de cache para controlar a duração do armazenamento em cache e garantir a entrega de recursos atualizados quando necessário.

2. **Cache do Servidor**:
   - Armazena em cache recursos dinâmicos no servidor, como respostas de API ou conteúdo gerado dinamicamente.
   - Reduz o tempo de resposta do servidor e melhora a escalabilidade, especialmente em aplicativos com alto tráfego.
   - Implementa estratégias de invalidação de cache para garantir que os dados em cache sejam atualizados conforme necessário.

3. **Cache em Memória**:
   - Utiliza memória RAM para armazenar em cache dados frequentemente acessados, como consultas a banco de dados ou resultados de cálculos.
   - Reduz o tempo de acesso aos dados e melhora o desempenho geral do aplicativo.
   - Implementa políticas de expiração e limpeza para gerenciar o uso de memória e evitar vazamentos de memória.

### HTTP/2:
1. **Multiplexação de Streams**:
   - Permite que várias solicitações e respostas sejam transmitidas simultaneamente em uma única conexão TCP.
   - Reduz a latência e melhora o desempenho, especialmente em conexões de rede de alta latência.

2. **Compressão de Cabeçalhos**:
   - Comprime os cabeçalhos das solicitações e respostas HTTP usando o algoritmo HPACK.
   - Reduz o overhead de dados e a largura de banda necessária para transmitir os cabeçalhos.

3. **Server Push**:
   - Permite que o servidor envie recursos adicionais para o cliente antes que eles sejam solicitados explicitamente.
   - Melhora o tempo de carregamento da página, enviando recursos necessários sem esperar pela solicitação do cliente.

4. **Priorização de Streams**:
   - Permite que o cliente especifique a prioridade das solicitações, indicando ao servidor quais recursos são mais importantes.
   - Ajuda a garantir que recursos críticos sejam entregues primeiro, melhorando a experiência do usuário.

5. **Header Compression**:
   - Utiliza a compressão de cabeçalhos para reduzir o tamanho dos cabeçalhos HTTP enviados entre o cliente e o servidor.
   - Reduz a quantidade de dados transferidos pela rede, melhorando o desempenho e a eficiência.

6. **Upgrade Opcional**:
   - O HTTP/2 permite que a negociação da versão do protocolo seja opcional, facilitando a implementação em servidores e clientes.
   - Os clientes podem optar por negociar a versão do protocolo apenas quando o suporte ao HTTP/2 estiver disponível.

7. **Gerenciamento de Fluxo**:
   - Permite que o cliente e o servidor controlem o fluxo de dados para evitar congestionamentos e garantir um desempenho consistente.
   - Os mecanismos de controle de fluxo ajudam a prevenir sobrecargas e a manter uma comunicação eficiente.

8. **Segurança Integrada**:
   - O HTTP/2 é compatível com TLS (Transport Layer Security), oferecendo criptografia e autenticação para proteger a comunicação entre o cliente e o servidor.
   - Garante a confidencialidade e a integridade dos dados transmitidos, protegendo contra ataques de interceptação e manipulação.