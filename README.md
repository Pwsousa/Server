# Eureka Server - Sabores Conectados

## Visão Geral
Servidor de descoberta de serviços (Service Discovery) para o sistema de microserviços do restaurante Sabores Conectados.

## Funcionalidades
- ✅ Registro automático de microserviços
- ✅ Descoberta de serviços
- ✅ Health checks
- ✅ Dashboard web para monitoramento
- ✅ Load balancing
- ✅ Failover automático

## Tecnologias
- **Java 17**
- **Spring Boot 3.3.4**
- **Spring Cloud Netflix Eureka Server 2023.0.3**

## Estrutura do Projeto
```
server/
├── Server/                      # Projeto Spring Boot
│   ├── server/                  # Módulo Eureka Server
│   │   ├── src/main/java/
│   │   │   └── br/com/saboresconectados/server/
│   │   │       └── ServerApplication.java
│   │   ├── src/main/resources/
│   │   │   └── application.properties
│   │   └── src/test/            # Testes unitários
│   ├── Dockerfile               # Container Docker
│   └── README.md                # Este arquivo
└── README.md                    # Este arquivo
```

## Como Executar

### Pré-requisitos
- Java 17+
- Maven 3.6+

### Execução Local
```bash
cd server/Server/server
mvn spring-boot:run
```

### Execução com Docker
```bash
docker build -t eureka-server .
docker run -p 8761:8761 eureka-server
```

## Configuração

### Porta
- **Porta**: 8761

### Dashboard
- **URL**: http://localhost:8761
- **Usuário**: (sem autenticação)

### Configurações Avançadas
Para configurar o Eureka Server, edite o arquivo `application.properties`:

```properties
# Configurações básicas
spring.application.name=eureka-server
server.port=8761

# Configurações do Eureka
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
eureka.server.enable-self-preservation=false
```

## Microserviços Registrados
O Eureka Server registra automaticamente os seguintes microserviços:

| Microserviço | Porta | Status |
|-------------|-------|--------|
| cardapio | 8082 | ✅ Ativo |
| pedidos | 8083 | ✅ Ativo |
| pagamentos | 8081 | ✅ Ativo |
| gateway | 8084 | ✅ Ativo |

## Monitoramento

### Dashboard Web
Acesse http://localhost:8761 para visualizar:
- Lista de serviços registrados
- Status de cada serviço
- Instâncias ativas
- Health checks

### Health Checks
- **Endpoint**: http://localhost:8761/actuator/health
- **Status**: UP/DOWN

## Troubleshooting

### Problemas Comuns
1. **Serviços não aparecem**: Verifique se os microserviços estão rodando
2. **Erro de conexão**: Verifique se a porta 8761 está livre
3. **Timeout**: Verifique a conectividade de rede

### Logs
Para debug, verifique os logs do Eureka Server:
```bash
tail -f logs/eureka-server.log
```

## Configurações de Produção
Para ambiente de produção, considere:

1. **Alta Disponibilidade**: Configure múltiplas instâncias do Eureka
2. **Segurança**: Configure autenticação
3. **Persistência**: Configure banco de dados para persistir registros
4. **Monitoramento**: Configure alertas e métricas

### Exemplo de Configuração para Produção
```properties
# Configurações de produção
eureka.server.enable-self-preservation=true
eureka.server.eviction-interval-timer-in-ms=30000
eureka.client.service-url.defaultZone=http://eureka1:8761/eureka/,http://eureka2:8761/eureka/
```

## Desenvolvimento
Para contribuir com o desenvolvimento:
1. Clone o repositório
2. Configure o ambiente de desenvolvimento
3. Execute os testes: `mvn test`
4. Faça suas alterações
5. Execute os testes novamente
6. Faça commit das alterações

## Arquitetura
O Eureka Server é o componente central da arquitetura de microserviços, permitindo:

- **Descoberta de Serviços**: Microserviços se registram automaticamente
- **Load Balancing**: Distribuição de carga entre instâncias
- **Failover**: Detecção automática de falhas
- **Monitoramento**: Visibilidade completa do sistema
