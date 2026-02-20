# Análise da Arquitetura de Software - Adote Fácil

## 1. Padrão Arquitetural Adotado

### 1.1 Padrão MVC Modificado com Camadas de Serviço

O projeto implementa uma variação do padrão **MVC (Model-View-Controller)** com uma camada adicional de serviços, resultando em uma arquitetura em camadas.

### 1.2 Camadas da Arquitetura

#### **Camada de Apresentação (Frontend)**

#### **Camada de Roteamento (Routes)**
- **Arquivo**: `src/routes.ts`
- **Responsabilidade**: Definição de endpoints HTTP e aplicação de middlewares 
- **Padrão**: Rotas RESTful bem definidas
- **Autenticação**: Middleware `UserAuthMiddleware` aplicado em rotas protegidas

#### **Camada de Controladores (Controllers)**
- **Localização**: `src/controllers/`
- **Responsabilidade**: Receber requisições HTTP, validar entrada, chamar serviços e retornar respostas
- **Padrão**: Cada controller é uma classe com método `handle()`
- **Tratamento de Erros**: Try-catch com status HTTP apropriados

#### **Camada de Serviços (Services)**
- **Localização**: `src/services/`
- **Responsabilidade**: Implementar lógica de negócio, validações e orquestração de operações
- **Padrão**: Cada serviço é uma classe com método `execute()`
- **Resultado**: Utiliza padrão `Either<Failure, Success>` para tratamento funcional de erros

#### **Camada de Repositórios (Repositories)**
- **Localização**: `src/repositories/`
- **Responsabilidade**: Abstrair acesso ao banco de dados
- **Padrão**: Cada repositório encapsula operações CRUD para uma entidade
- **ORM**: Prisma Client para operações de banco de dados

#### **Camada de Provedores (Providers)**
- **Localização**: `src/providers/`
- **Responsabilidade**: Fornecer utilitários reutilizáveis
- **Componentes**:
  - `Authenticator`: Geração e validação de JWT
  - `Encrypter`: Criptografia de senhas com Bcrypt

#### **Camada de Banco de Dados**
- **Tecnologia**: PostgreSQL
- **ORM**: Prisma
- **Schema**: Definido em `prisma/schema.prisma`

### 1.3 Padrão de Injeção de Dependência

O projeto utiliza **injeção de dependência** através de instâncias singleton:

```typescript
export const createUserServiceInstance = new CreateUserService(
  encrypterInstance,
  userRepositoryInstance,
)

export const createUserControllerInstance = new CreateUserController(
  createUserServiceInstance,
)
```

## 2. Conclusão

O projeto **Adote Fácil** implementa uma arquitetura bem estruturada seguindo padrões consolidados de desenvolvimento web. A separação clara entre camadas, uso de injeção de dependência e padrões de projeto estabelecidos tornam o código manutenivel, testável e escalável. A aplicação demonstra boas práticas de engenharia de software e está pronta para evolução e manutenção.
