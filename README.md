# 🚪 API Gateway Service - Conecta Saúde

Este é o **API Gateway** do projeto Conecta Saúde. Ele atua como o único ponto de entrada (Single Point of Entry) para todas as requisições vindas do Front-end (Angular), roteando o tráfego de forma inteligente e segura para os microsserviços internos no back-end.

## 🎯 Responsabilidades Principais

*   **Roteamento Dinâmico:** Direciona as chamadas da API para o microsserviço correto (`identity-service`, `appointment-service` ou `clinical-service`) com base no caminho (path) da URL.
*   **Gerenciamento de CORS:** Centraliza a configuração de Cross-Origin Resource Sharing (CORS), permitindo que o front-end Angular consuma as APIs sem bloqueios do navegador.
*   **Isolamento da Arquitetura:** Impede que o cliente conheça os endereços (IPs/Portas) reais dos microsserviços, garantindo maior segurança e flexibilidade para mudar a infraestrutura interna sem quebrar o front-end.
*   **Segurança e Filtros (Futuamente):** Preparado para interceptar requisições e validar tokens JWT antes mesmo de baterem nos serviços de domínio.

## 🛠️ Tecnologias Utilizadas

*   **Java 17+**
*   **Spring Boot**
*   **Spring Cloud Gateway** (Roteamento reativo e assíncrono)
*   **Docker** (Containerização)

## 🗺️ Mapa de Rotas (Routing)

O Gateway escuta na porta `8080` e roteia as requisições da seguinte forma:

| Rota no Gateway (`localhost:8080`) | Microsserviço de Destino | Banco de Dados |
| :--- | :--- | :--- |
| `/api/auth/**` | `identity-service` (Porta 8082) | PostgreSQL |
| `/api/users/**` | `identity-service` (Porta 8082) | PostgreSQL |
| `/api/appointments/**` | `appointment-service` (Porta 8081)| PostgreSQL |
| `/api/records/**` | `clinical-service` (Porta 8083) | MongoDB |
| `/api/exams/**` | `clinical-service` (Porta 8083) | MongoDB |

## 🚀 Como Executar

### Pré-requisitos
Certifique-se de ter o **Docker** e o **Docker Compose** instalados ou o JDK configurado na sua máquina.

### Via Docker (Recomendado)
O Gateway está configurado para rodar na rede interna de microsserviços. A melhor forma de executá-lo é através do `docker-compose.yml` na raiz do projeto principal:

```bash
docker compose up api-gateway-service -d --build
Localmente (Dev Mode)
Para rodar direto no IntelliJ ou via terminal (necessário que os outros microsserviços estejam rodando nas portas originais):

Bash
./mvnw spring-boot:run
🤝 Autor
Desenvolvido por joaobrxyz como parte da arquitetura de microsserviços do projeto Conecta Saúde.
