---
title: Dicas sobre segurança no frontend
author: fziliotti
date: 2024-02-29 04:33:00 +0800
categories: ["Desenvolvimento"]
tags: [frontend]
---

### **Atualize Dependências Regularmente:**
Manter as dependências atualizadas é crucial para incluir correções de segurança. Utilize o comando `npm audit` para identificar e corrigir vulnerabilidades conhecidas nas bibliotecas utilizadas.


## **Utilize HTTPS:**
Configurar sua aplicação React para usar HTTPS é essencial para proteger os dados em trânsito. Certifique-se de adquirir e instalar um certificado SSL válido. Isso previne ataques como interceptação de dados e man-in-the-middle.

**Prática:** Configure seu servidor para suportar HTTPS e atualize as URLs dos recursos na sua aplicação para usar `https://`.

**Referência:**
- [OWASP - Transport Layer Protection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html)

## **Autenticação Segura:**
Implemente métodos seguros de autenticação, como OAuth ou JWT. Evite o uso de autenticação básica e armazenamento de senhas no cliente. Priorize soluções modernas e seguras para autenticação de usuários.

**Exemplo em React:** Utilize bibliotecas como `react-oauth` ou `jsonwebtoken` para implementar autenticação segura. Para mais informações, leia o meu post [sobre os tipos de autenticação.](/)

**Referência:**
- [OWASP - Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)

## **Controle de Acesso:**
Implemente um sistema de controle de acesso robusto. Garanta que os usuários tenham acesso apenas às partes da aplicação para as quais têm permissão. Use tokens JWT para incluir informações sobre permissões.

**Exemplo em React:** Controle a exibição de componentes com base nas permissões do usuário.

Exemplo prático:

```jsx
import React, { createContext, useContext } from 'react';

// Criando o contexto de autenticação
const AuthContext = createContext();

// Provedor de autenticação que pode ser usado para envolver a aplicação
export const AuthProvider = ({ children }) => {
  // Simulação de informações do usuário e permissões
  const user = {
    id: 1,
    username: 'usuario_demo',
    permissions: ['VIEW_DASHBOARD', 'EDIT_PROFILE'],
  };

  return (
    <AuthContext.Provider value={user}>
      {children}
    </AuthContext.Provider>
  )
};

// Hook personalizado para acessar o contexto de autenticação
export const useAuth = () => {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth deve ser utilizado dentro de um AuthProvider');
  }
  return context;
};

// Componente protegido que requer permissões específicas
const ProtectedComponent = ({ requiredPermissions, children }) => {
  const user = useAuth();

  // Verifica se o usuário possui todas as permissões necessárias
  const hasRequiredPermissions = requiredPermissions.every(
    (permission) => user.permissions.includes(permission)
  );

  if (!hasRequiredPermissions) {
    // Se o usuário não tiver permissão, renderiza uma mensagem ou componente de acesso negado
    return <div>Acesso negado. Você não possui as permissões necessárias.</div>
  }

  // Se o usuário tiver permissão, renderiza o conteúdo do componente protegido
  return <>{children}</>
};

// Componente principal da aplicação
const App = () => {
  return (
    <AuthProvider>
      <div>
        <h1>Minha Aplicação React</h1>
        
        {/* Exemplo de componente protegido que requer permissões específicas */}
        <ProtectedComponent requiredPermissions={['VIEW_DASHBOARD']}>
          <p>Este é o painel de controle.</p>
        </ProtectedComponent>

        {/* Outros componentes... */}
      </div>
    </AuthProvider>
  );
};

export default App;
```

**Referência:**
- [OWASP - Access Control Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Access_Control_Cheat_Sheet.html)
  
## **Validação de Entradas:**
Realize validação e sanitize dos dados do usuário para evitar ataques como XSS e CSRF. Utilize bibliotecas apropriadas, como `DOMPurify`, para garantir que inputs não introduzam scripts maliciosos.

**Exemplo em React:** Utilize `dangerouslySetInnerHTML` com cuidado e sanitize dados antes de renderizar.

Exemplo prático:

```jsx
// Evite o uso desnecessário de dangerouslySetInnerHTML
const ComentarioInseguro = ({ texto }) => {
  return <div dangerouslySetInnerHTML={{ __html: texto }} />
};

const ComentarioSeguro = ({ texto }) => {
  // Utilize bibliotecas como DOMPurify para sanitização
  const textoSanitizado = DOMPurify.sanitize(texto);

  return <div dangerouslySetInnerHTML={{ __html: textoSanitizado }} />
};
```

**Referência:**
- [OWASP - Input Validation Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html)


## **Proteção contra Clickjacking:**
Adicione cabeçalhos HTTP como `X-Frame-Options` para proteger contra ataques de clickjacking. Essa medida impede que sua aplicação seja incorporada em frames não autorizados.

**Exemplo em React:** Configure o cabeçalho no servidor para enviar `X-Frame-Options: SAMEORIGIN`.

**Referência:**
- [OWASP - Clickjacking Defense Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking_Defense_Cheat_Sheet.html)

## **Configurações de Segurança do Navegador:**
Ajuste cabeçalhos HTTP, como `Content-Security-Policy`, para controlar o comportamento do navegador e reduzir o risco de ataques como XSS. Esse cabeçalho define quais recursos são permitidos na página.

**Exemplo em React:** Adicione `<meta http-equiv="Content-Security-Policy" content="default-src 'self';">` ao HTML.

**Referência:**
- [MDN Web Docs - Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)

## **Logs de Segurança:**
   Implemente logs de segurança eficazes para monitorar atividades suspeitas. Registre informações relevantes sobre eventos como tentativas de login inválidas e acesse esses logs regularmente para detecção precoce de possíveis violações.

**Exemplo em React:** Integre uma biblioteca de logs como `log4javascript` ou envie logs para o servidor.

**Referência:**
- [OWASP - Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)


## **Tratamento de Erros Adequado:**
Forneça mensagens de erro genéricas para usuários, evitando expor detalhes técnicos que possam ser explorados por atacantes. Registre informações detalhadas do erro no backend para análise posterior.

**Exemplo em React:** Utilize `ErrorBoundary` para capturar erros e registre-os no servidor.

Exemplo prático:

```jsx
import React, { Component } from 'react';

// Função simulada para enviar informações de erro para o servidor
const enviarErroParaServidor = (error, errorInfo) => {
  // Simulação de lógica para enviar o erro para o servidor
  console.error('Erro enviado para o servidor:', error, errorInfo);
  // Aqui você pode fazer uma chamada real para um endpoint no servidor para enviar as informações do erro
};

// Componente que representa a mensagem de erro
const MensagemErro = () => (
  <div style={{ color: 'red', padding: '20px', textAlign: 'center' }}>
    <h2>Ocorreu um erro inesperado.</h2>
    <p>Nossas desculpas pelo inconveniente. Por favor, tente recarregar a página.</p>
  </div>
);

// Componente de ErrorBoundary para capturar erros e exibir uma mensagem de erro amigável
class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  // Captura erros na renderização de componentes filhos
  componentDidCatch(error, errorInfo) {
    // Atualiza o estado para indicar que ocorreu um erro
    this.setState({ hasError: true });

    // Envia informações do erro para o servidor (simulado)
    enviarErroParaServidor(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // Se ocorreu um erro, renderiza a mensagem de erro
      return <MensagemErro />
    }

    // Se não houve erro, renderiza os componentes filhos normalmente
    return this.props.children
  }
}

// Componente que pode gerar um erro para fins de demonstração
const ComponenteComErro = () => {
  throw new Error('Este é um erro simulado.');
};

// Componente principal que utiliza o ErrorBoundary
const App = () => {
  return (
    <ErrorBoundary>
      <div>
        <h1>Minha Aplicação React</h1>

        {/* Componente que gera um erro */}
        <ComponenteComErro />

        {/* Outros componentes... */}
      </div>
    </ErrorBoundary>
  );
};

export default App;
```

**Referência:**
- [OWASP - Error Handling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html)

## **Testes de Segurança:**

Realize testes de segurança regularmente, incluindo testes de penetração e auditorias de código. Ferramentas como OWASP ZAP e ESLint podem ajudar a identificar e corrigir potenciais vulnerabilidades.

**Exemplo em React:** Utilize `eslint-plugin-security` para verificar código em busca de vulnerabilidades.

**Referência:**
- [OWASP - Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)

## **Práticas de Desenvolvimento Seguro:**

É interessante que a equipe se informe e aplique práticas seguras, incluindo codificação segura, revisões de código focadas em segurança e integração contínua com ferramentas de segurança automatizadas.
