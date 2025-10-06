# ESPECIFICAÇÃO DE REQUISITOS DE SOFTWARE (SRS)
## Sistema DistriSchool - Plataforma de Gestão Escolar Distribuída

---

## 1. Introdução

Este documento contempla os requisitos necessários para desenvolvimento do **DistriSchool**, plataforma de gestão escolar distribuída que visa modernizar e otimizar os processos administrativos e pedagógicos de instituições de ensino através de uma arquitetura escalável, tolerante a falhas e baseada em microsserviços.

### 1.1 Finalidade

A finalidade deste documento é apontar e organizar os requisitos funcionais e não funcionais envolvidos no planejamento do projeto DistriSchool. Os requisitos funcionais detalham as características e funções do sistema, enquanto os requisitos não funcionais especificam atributos de qualidade, desempenho, segurança e restrições técnicas que o sistema deve atender.

Este documento serve como base para:
- Desenvolvimento técnico da plataforma
- Validação com stakeholders
- Testes e homologação do sistema
- Manutenção e evolução futura

### 1.2 Escopo do Produto

O DistriSchool é uma plataforma completa de gestão escolar construída com arquitetura de microsserviços distribuídos, utilizando tecnologias modernas como Spring Boot, React, Kafka e Kubernetes. O sistema visa atender instituições educacionais de médio e grande porte, suportando mais de 10.000 alunos simultaneamente.

**Objetivos principais:**
- Automatizar processos administrativos escolares (matrículas, presenças, notas)
- Facilitar a comunicação entre escola, professores, alunos e pais
- Fornecer relatórios e análises em tempo real para tomada de decisão
- Garantir alta disponibilidade (99% uptime) e escalabilidade horizontal
- Assegurar conformidade com LGPD para proteção de dados pessoais

**Benefícios esperados:**
- Redução de 60% no tempo de processos administrativos
- Melhoria na comunicação institucional através de notificações em tempo real
- Visibilidade completa do desempenho acadêmico
- Acesso multiplataforma (web e mobile)
- Redução de custos operacionais com infraestrutura escalável em nuvem

### 1.3 Referências

- **IEEE 830-1998** - IEEE Recommended Practice for Software Requirements Specifications
- **Documentação Spring Boot** - https://spring.io/projects/spring-boot
- **Documentação React + Vite** - https://vitejs.dev/
- **Apache Kafka Documentation** - https://kafka.apache.org/documentation/
- **Kubernetes Documentation** - https://kubernetes.io/docs/
- **Lei Geral de Proteção de Dados (LGPD)** - Lei nº 13.709/2018
- **AWS Well-Architected Framework** - https://aws.amazon.com/architecture/well-architected/
- **Resilience4j Documentation** - https://resilience4j.readme.io/

---

## 2. Descrição Geral

### 2.1 Perspectiva do Produto

O DistriSchool é um sistema novo e autossuficiente que substitui processos manuais e planilhas desconectadas tradicionalmente utilizadas em gestão escolar. O sistema não substitui sistemas legados específicos, mas surge como uma solução moderna e integrada.

**Arquitetura do Sistema:**

O DistriSchool adota arquitetura de microsserviços com os seguintes componentes principais:

**Frontend:**
- Cliente web desenvolvido em React com Vite
- Interface responsiva para desktop e mobile
- Comunicação via REST APIs e WebSocket para notificações em tempo real

**Backend (Microsserviços):**
- **API Gateway** (Spring Cloud Gateway) - Roteamento e balanceamento de carga
- **School-Core-Service** - Gestão de alunos e turmas
- **Teacher-Service** - Gestão de professores e atribuições
- **Notification-Service** - Envio de mensagens e notificações
- **Grade-Service** - Lançamento de notas e avaliações
- **Attendance-Service** - Registro de presenças
- **User-Service** - Autenticação e autorização (JWT + OAuth2)
- **Report-Service** - Geração de relatórios via gRPC

**Infraestrutura:**
- Mensageria assíncrona via Apache Kafka
- Bancos de dados PostgreSQL (dados relacionais) e MongoDB (dados não estruturados)
- Cache distribuído com Redis
- Orquestração com Kubernetes (K8s)
- Monitoramento com Prometheus + Grafana
- Logs centralizados com ELK Stack
- Deploy em AWS/Azure com Terraform

### 2.2 Funções do Produto

O DistriSchool oferece as seguintes funções principais:

**Autenticação e Autorização:**
- Login seguro com email/senha ou OAuth2
- Gerenciamento de perfis (admin, professor, aluno, pai)
- Recuperação de senha com verificação por email
- Autenticação via JWT com renovação automática

**Gestão de Alunos:**
- Cadastro completo com dados pessoais e documentos
- Busca avançada por matrícula, nome ou turma
- Upload e armazenamento de documentos
- Histórico acadêmico integrado
- Exportação de listas em PDF/CSV

**Gestão de Professores:**
- Cadastro com qualificações e especializações
- Atribuição automática de disciplinas e turmas
- Visualização de horários e calendário acadêmico
- Relatórios de desempenho docente

**Gestão de Turmas e Horários:**
- Criação de turmas e disciplinas por período letivo
- Calendário escolar com feriados e eventos
- Detecção automática de conflitos de horário
- Suporte a múltiplos turnos
- Importação via planilhas Excel

**Registro de Presenças:**
- Chamada diária por turma/disciplina
- Suporte a biometria e QR Code
- Cálculo automático de percentual de presença
- Notificações automáticas para pais em caso de faltas
- Relatórios de frequência por período

**Gestão de Notas e Avaliações:**
- Lançamento de notas por avaliação
- Cálculo automático de médias
- Histórico completo de avaliações
- Notificações de resultados para alunos e pais
- Análise de desempenho por disciplina

**Comunicação e Notificações:**
- Avisos gerais da escola
- Notificações individualizadas
- Integração com email e push notifications
- Portal de comunicação para pais

**Relatórios e Análises:**
- Dashboard executivo com indicadores
- Relatórios de desempenho acadêmico
- Análises de frequência e evasão
- Exportação em múltiplos formatos

### 2.3 Classes de Usuários e Características

**Administrador do Sistema:**
- Frequência de uso: Diária
- Conhecimento técnico: Alto
- Privilégios: Acesso completo ao sistema
- Funções: Configuração geral, gestão de usuários, relatórios estratégicos
- Importância: Crítica

**Gestor Escolar (Diretor/Coordenador):**
- Frequência de uso: Diária
- Conhecimento técnico: Médio
- Privilégios: Visualização de todos os dados, aprovação de processos
- Funções: Acompanhamento pedagógico, aprovação de matrículas, análise de relatórios
- Importância: Alta

**Professor:**
- Frequência de uso: Diária
- Conhecimento técnico: Médio
- Privilégios: Acesso a suas turmas e disciplinas
- Funções: Registro de presenças, lançamento de notas, visualização de turmas
- Importância: Alta

**Secretaria/Administrativo:**
- Frequência de uso: Diária
- Conhecimento técnico: Médio
- Privilégios: Gestão de cadastros e documentos
- Funções: Matrícula de alunos, cadastro de professores, emissão de documentos
- Importância: Alta

**Aluno:**
- Frequência de uso: Semanal
- Conhecimento técnico: Baixo a Médio
- Privilégios: Visualização de seus dados acadêmicos
- Funções: Consulta de notas, frequência, horários e comunicados
- Importância: Média

**Pai/Responsável:**
- Frequência de uso: Semanal
- Conhecimento técnico: Baixo
- Privilégios: Visualização dos dados do aluno responsável
- Funções: Acompanhamento acadêmico, recebimento de notificações
- Importância: Média

### 2.4 Ambiente de Trabalho

**Plataforma de Hardware:**
- Servidores: AWS EC2 ou Azure VMs com mínimo de 4 vCPUs e 8GB RAM por microsserviço
- Clientes: Navegadores web modernos em desktops, tablets e smartphones

**Sistema Operacional:**
- Servidores: Linux Ubuntu 20.04 LTS ou superior (containerizado via Docker)
- Clientes: Multiplataforma (Windows 10+, macOS 11+, Android 8+, iOS 13+)

**Software e Dependências:**
- **Backend:** Java 17+, Spring Boot 3.x, Spring Cloud 2023.x
- **Frontend:** Node.js 18+, React 18+, Vite 5+
- **Banco de Dados:** PostgreSQL 14+, MongoDB 6+, Redis 7+
- **Mensageria:** Apache Kafka 3.5+
- **Container Runtime:** Docker 24+ e Kubernetes 1.28+
- **Monitoramento:** Prometheus 2.45+, Grafana 10+
- **Navegadores:** Chrome 100+, Firefox 100+, Safari 15+, Edge 100+

**Integrações Necessárias:**
- Serviços de email (SMTP)
- Serviços de SMS (opcional)
- Google Calendar API (sincronização de eventos)
- Serviços de storage em nuvem (AWS S3 ou Azure Blob)

### 2.5 Design e Implementação Restrições

**Restrições Tecnológicas:**
- Uso obrigatório de Java 17+ e Spring Boot para todos os microsserviços backend
- Frontend deve ser desenvolvido em React com Vite
- Toda comunicação assíncrona deve utilizar Apache Kafka
- Containerização obrigatória via Docker
- Orquestração via Kubernetes para ambientes de produção

**Restrições de Arquitetura:**
- Arquitetura de microsserviços com máximo de 500 linhas de código por endpoint
- Cada microsserviço deve ter seu próprio banco de dados (Database per Service pattern)
- Circuit Breaker obrigatório para todas as chamadas entre serviços
- API Gateway como único ponto de entrada externo

**Restrições Regulatórias:**
- Conformidade total com LGPD (Lei nº 13.709/2018)
- Criptografia de dados sensíveis em repouso e em trânsito
- Logs de auditoria para todas as operações críticas
- Política de retenção de dados conforme legislação educacional

**Restrições de Performance:**
- Tempo de resposta máximo de 2 segundos para operações de leitura
- Tempo de resposta máximo de 5 segundos para operações de escrita
- Suporte a pelo menos 1000 requisições simultâneas
- Disponibilidade mínima de 99% (SLA)

**Restrições de Segurança:**
- Autenticação via JWT com expiração de 1 hora
- Renovação automática de tokens
- Criptografia BCrypt para senhas (mínimo 12 rounds)
- HTTPS obrigatório para todas as comunicações
- Rate limiting no API Gateway (100 requisições/minuto por usuário)

**Padrões de Codificação:**
- Clean Code e SOLID principles
- Testes unitários com cobertura mínima de 80%
- Documentação de APIs via OpenAPI/Swagger
- Versionamento semântico (SemVer)
- Git Flow para controle de versão

### 2.6 Documentação do Usuário

**Documentação a ser entregue:**

**Manual do Administrador:**
- Formato: PDF e HTML online
- Conteúdo: Configuração inicial, gestão de usuários, troubleshooting
- Idioma: Português (PT-BR)

**Manual do Professor:**
- Formato: PDF e vídeos tutoriais
- Conteúdo: Registro de presenças, lançamento de notas, uso do calendário
- Idioma: Português (PT-BR)

**Manual do Secretário:**
- Formato: PDF e HTML online
- Conteúdo: Processo de matrícula, emissão de documentos, cadastros
- Idioma: Português (PT-BR)

**Guia Rápido para Alunos e Pais:**
- Formato: PDF simplificado e vídeos curtos (max 3 min)
- Conteúdo: Como acessar o sistema, consultar notas e frequência
- Idioma: Português (PT-BR)

**Documentação Técnica:**
- Formato: Markdown no repositório Git + Wiki
- Conteúdo: Arquitetura, APIs, guia de deploy, troubleshooting técnico
- Idioma: Português (PT-BR) e Inglês

**Sistema de Ajuda Online:**
- Integrado à aplicação web
- Contextual (ajuda específica por tela)
- Base de conhecimento com FAQ

### 2.7 Suposições e Dependências

**Suposições:**

1. **Infraestrutura:** Assume-se que a instituição possui ou contratará infraestrutura de nuvem (AWS/Azure) com recursos suficientes

2. **Conectividade:** Assume-se conectividade de internet estável com mínimo de 10 Mbps para uso adequado do sistema

3. **Dispositivos:** Assume-se que usuários possuem dispositivos compatíveis (computadores ou smartphones modernos)

4. **Capacitação:** Assume-se que haverá período de treinamento para usuários antes do go-live

5. **Dados Legados:** Assume-se que dados de sistemas anteriores estarão disponíveis em formato estruturado (CSV/Excel) para migração

6. **Equipe Técnica:** Assume-se disponibilidade de equipe técnica da instituição para suporte de primeiro nível

**Dependências:**

1. **Serviços de Terceiros:**
   - Provedores de nuvem (AWS/Azure) para hospedagem
   - Serviços de email (SMTP) para notificações
   - Google Calendar API para sincronização de eventos
   - Serviços de autenticação OAuth2 (Google, Microsoft)

2. **Bibliotecas e Frameworks:**
   - Spring Boot e ecossistema Spring
   - React e bibliotecas do ecossistema
   - Apache Kafka
   - PostgreSQL e MongoDB

3. **Ferramentas de Desenvolvimento:**
   - Docker e Kubernetes
   - Terraform para IaC
   - GitHub/GitLab para controle de versão
   - Jenkins/GitHub Actions para CI/CD

4. **Compliance:**
   - Certificados SSL/TLS válidos
   - Adequação às políticas de segurança da instituição
   - Aprovação de órgãos reguladores (se aplicável)

5. **Cronograma:**
   - Disponibilidade da equipe de desenvolvimento (3-5 desenvolvedores)
   - Prazo estimado de 8 semanas para MVP
   - Período de homologação e testes antes do lançamento

**Riscos Relacionados:**
- Mudanças em políticas de privacidade que afetem conformidade LGPD
- Alterações significativas em APIs de terceiros
- Indisponibilidade de serviços de nuvem
- Mudanças regulatórias no setor educacional
- Rotatividade na equipe de desenvolvimento

---

## 3. Requisitos do Sistema

### 3.1 Requisitos Funcionais

| ID | INTERESSADO | DESCRIÇÃO |
|----|-------------|-----------|
| RF001 | Administrador, Secretaria | O sistema deve permitir o cadastro de alunos com os campos: nome completo, data de nascimento, CPF, endereço completo, contatos (telefone, email), nome dos responsáveis, documentos (RG, certidão de nascimento) |
| RF002 | Administrador, Secretaria | O sistema deve permitir a edição e exclusão de dados de alunos, mantendo histórico de alterações para auditoria |
| RF003 | Administrador, Secretaria, Professor | O sistema deve permitir busca de alunos por matrícula, nome, CPF, turma ou responsável |
| RF004 | Secretaria | O sistema deve permitir o upload de documentos do aluno em formatos PDF, JPG, PNG com tamanho máximo de 5MB por arquivo |
| RF005 | Administrador, Gestor | O sistema deve permitir a exportação de listas de alunos nos formatos PDF e CSV |
| RF006 | Aluno, Pai, Professor, Gestor | O sistema deve exibir o histórico acadêmico completo do aluno incluindo notas, frequência e observações |
| RF007 | Administrador, Secretaria | O sistema deve permitir o cadastro de professores com os campos: nome completo, CPF, formação acadêmica, especializações, disciplinas habilitadas, contatos |
| RF008 | Administrador | O sistema deve permitir a atribuição de disciplinas e turmas aos professores |
| RF009 | Professor, Gestor | O sistema deve exibir os horários semanais do professor com suas turmas e disciplinas |
| RF010 | Administrador, Gestor | O sistema deve gerar relatórios de desempenho dos professores baseado em notas das turmas e feedbacks |
| RF011 | Administrador, Secretaria | O sistema deve permitir a criação de turmas especificando: código, nome, série/ano, turno, ano letivo, capacidade máxima |
| RF012 | Administrador | O sistema deve permitir a criação de disciplinas especificando: código, nome, carga horária, ementa |
| RF013 | Administrador, Secretaria | O sistema deve permitir a atribuição de alunos a turmas respeitando a capacidade máxima |
| RF014 | Administrador | O sistema deve criar o calendário escolar definindo início e fim dos períodos letivos, feriados e eventos |
| RF015 | Administrador, Secretaria | O sistema deve detectar e alertar sobre conflitos de horários de professores ou salas |
| RF016 | Secretaria | O sistema deve permitir a importação de dados de turmas via planilhas Excel (.xlsx, .xls) |
| RF017 | Professor | O sistema deve permitir o registro diário de presença por turma/disciplina marcando: presente, falta, atraso |
| RF018 | Professor | O sistema deve permitir registro de presença via QR Code gerado para cada aula |
| RF019 | Professor | O sistema deve calcular automaticamente o percentual de presença do aluno |
| RF020 | Sistema | O sistema deve enviar notificação automática para os pais quando o aluno tiver falta registrada |
| RF021 | Professor, Gestor, Pai | O sistema deve gerar relatórios de frequência por aluno, turma, disciplina e período |
| RF022 | Professor | O sistema deve permitir o lançamento de notas por avaliação especificando: tipo de avaliação, peso, data, valor |
| RF023 | Sistema | O sistema deve calcular automaticamente as médias parciais e finais conforme regras configuradas |
| RF024 | Professor, Aluno, Pai | O sistema deve exibir o histórico completo de avaliações e notas do aluno |
| RF025 | Sistema | O sistema deve notificar alunos e pais quando novas notas forem lançadas |
| RF026 | Gestor | O sistema deve gerar análises de desempenho por disciplina, turma e professor |
| RF027 | Todos | O sistema deve permitir login via email/senha com validação de credenciais |
| RF028 | Todos | O sistema deve suportar autenticação OAuth2 via Google e Microsoft |
| RF029 | Todos | O sistema deve implementar autenticação JWT com tokens de acesso (1 hora) e refresh tokens (7 dias) |
| RF030 | Todos | O sistema deve permitir recuperação de senha via email com link de redefinição válido por 24 horas |
| RF031 | Sistema | O sistema deve exigir verificação de email após cadastro enviando link de confirmação |
| RF032 | Administrador | O sistema deve permitir gestão de perfis e permissões: Admin, Gestor, Professor, Secretaria, Aluno, Pai |
| RF033 | Gestor, Administrador | O sistema deve enviar avisos gerais para grupos de usuários (turma, série, escola inteira) |
| RF034 | Professor | O sistema deve permitir envio de comunicados individuais para alunos e pais |
| RF035 | Sistema | O sistema deve enviar notificações push, email e SMS (opcional) |
| RF036 | Pai | O sistema deve exibir portal de comunicação com histórico de mensagens recebidas |
| RF037 | Gestor | O sistema deve gerar dashboard executivo com indicadores: total de alunos, taxa de frequência média, desempenho por disciplina |
| RF038 | Gestor, Professor | O sistema deve gerar relatórios de desempenho acadêmico com filtros por turma, disciplina, período |
| RF039 | Gestor | O sistema deve gerar análises de frequência e alertas de risco de evasão |
| RF040 | Gestor, Administrador | O sistema deve permitir exportação de relatórios em PDF, Excel e CSV |

### 3.2 Requisitos Não Funcionais

| ID | INTERESSADO | DESCRIÇÃO |
|----|-------------|-----------|
| RNF001 | Todos | O sistema deve ter tempo de resposta máximo de 2 segundos para operações de consulta (leitura) |
| RNF002 | Todos | O sistema deve ter tempo de resposta máximo de 5 segundos para operações de cadastro/atualização (escrita) |
| RNF003 | Administrador | O sistema deve suportar no mínimo 10.000 alunos cadastrados simultaneamente |
| RNF004 | Todos | O sistema deve suportar pelo menos 1.000 usuários simultâneos sem degradação de performance |
| RNF005 | Administrador | O sistema deve ter disponibilidade mínima de 99% (SLA), permitindo downtime máximo de 7,2 horas/mês |
| RNF006 | Todos | O sistema deve ser acessível via navegadores Chrome 100+, Firefox 100+, Safari 15+, Edge 100+ |
| RNF007 | Todos | A interface deve ser responsiva, adaptando-se a resoluções de 320px (mobile) até 2560px (desktop) |
| RNF008 | Todos | O sistema deve funcionar em dispositivos Android 8+ e iOS 13+ |
| RNF009 | Todos | Todas as senhas devem ser criptografadas usando BCrypt com mínimo de 12 rounds |
| RNF010 | Todos | Toda comunicação entre cliente e servidor deve usar HTTPS (TLS 1.3) |
| RNF011 | Todos | Dados pessoais sensíveis devem ser criptografados em repouso usando AES-256 |
| RNF012 | Administrador | O sistema deve implementar rate limiting de 100 requisições por minuto por usuário |
| RNF013 | Administrador | O sistema deve registrar logs de auditoria para todas as operações críticas (CRUD de dados, acessos, alterações) |
| RNF014 | Todos | O sistema deve estar em conformidade total com a LGPD (Lei nº 13.709/2018) |
| RNF015 | Todos | O sistema deve implementar Circuit Breaker com Resilience4J em todas as chamadas entre microsserviços |
| RNF016 | Todos | O sistema deve implementar retry automático (máximo 3 tentativas) em operações que falharem temporariamente |
| RNF017 | Administrador | O sistema deve permitir escalabilidade horizontal adicionando novos pods/containers sob demanda |
| RNF018 | Administrador | Cada microsserviço deve poder ser implantado independentemente sem afetar os demais |
| RNF019 | Administrador | O sistema deve realizar backup automático diário de todos os bancos de dados |
| RNF020 | Administrador | O sistema deve manter backups por no mínimo 90 dias |
| RNF021 | Todos | A interface deve suportar os idiomas Português (PT-BR) e Inglês (EN) |
| RNF022 | Todos | A interface deve seguir princípios de acessibilidade WCAG 2.1 nível AA |
| RNF023 | Administrador | O sistema deve expor métricas de monitoramento via Prometheus (latência, throughput, taxa de erro) |
| RNF024 | Administrador | O sistema deve centralizar logs via ELK Stack para análise e troubleshooting |
| RNF025 | Administrador | O sistema deve enviar alertas automáticos quando métricas críticas ultrapassarem thresholds definidos |
| RNF026 | Todos | Mensagens de erro devem ser claras e informativas, sem expor detalhes técnicos sensíveis |
| RNF027 | Desenvolvedor | O código deve ter cobertura de testes unitários mínima de 80% |
| RNF028 | Desenvolvedor | Todas as APIs devem ser documentadas via OpenAPI/Swagger |
| RNF029 | Administrador | O sistema deve suportar deploy em múltiplas regiões geográficas (multi-region) |
| RNF030 | Todos | O sistema deve ter RTO (Recovery Time Objective) de 4 horas e RPO (Recovery Point Objective) de 1 hora |

### 3.3 Regras de Negócio

| ID | INTERESSADO | DESCRIÇÃO |
|----|-------------|-----------|
| RN001 | Administrador, Secretaria | Um aluno só pode estar matriculado em uma turma por período letivo para cada série |
| RN002 | Administrador | A capacidade máxima de alunos por turma deve ser respeitada (não permitir matrículas além do limite) |
| RN003 | Professor | A frequência mínima obrigatória é de 75% da carga horária total para aprovação |
| RN004 | Sistema | Alunos com frequência abaixo de 75% devem ser reprovados por falta, independente da média |
| RN005 | Professor | A média mínima para aprovação é 6.0 (configurável por instituição) |
| RN006 | Professor | Alunos com média entre 4.0 e 5.9 devem ir para recuperação final |
| RN007 | Professor | Alunos com média abaixo de 4.0 são reprovados diretamente |
| RN008 | Sistema | A média final é calculada como: (Nota1 x Peso1 + Nota2 x Peso2 + ... + NotaN x PesoN) / Soma dos Pesos |
| RN009 | Professor | Um professor não pode ter aulas simultâneas em turmas diferentes (validação de horário) |
| RN010 | Administrador | Uma sala não pode ser alocada para duas turmas no mesmo horário |
| RN011 | Sistema | O ano letivo deve ter no mínimo 200 dias letivos conforme legislação brasileira |
| RN012 | Professor | Presença só pode ser registrada na data da aula (não permitir registro retroativo além de 7 dias) |
| RN013 | Professor | Notas devem estar na escala de 0 a 10 com até uma casa decimal |
| RN014 | Sistema | Pai/Responsável só pode visualizar dados dos alunos vinculados a ele |
| RN015 | Sistema | Aluno só pode visualizar seus próprios dados acadêmicos |
| RN016 | Professor | Professor só pode lançar notas e presenças das turmas e disciplinas atribuídas a ele |
| RN017 | Sistema | Dados de alunos menores de 18 anos requerem consentimento dos responsáveis para tratamento (LGPD) |
| RN018 | Administrador | Exclusão de alunos deve ser lógica (soft delete), mantendo dados por no mínimo 5 anos para histórico |
| RN019 | Sistema | Notificações de faltas devem ser enviadas aos pais após 3 faltas consecutivas ou 5 faltas alternadas em 30 dias |
| RN020 | Sistema | Alterações em notas já publicadas devem gerar log de auditoria com justificativa obrigatória |
| RN021 | Professor | Prazo máximo para lançamento de notas é de 15 dias após a aplicação da avaliação |
| RN022 | Sistema | CPF deve ser único no sistema (não permitir cadastro duplicado) |
| RN023 | Administrador | Um professor deve ter no mínimo uma qualificação/formação compatível com as disciplinas que leciona |
| RN024 | Sistema | Senhas devem ter no mínimo 8 caracteres, incluindo letras maiúsculas, minúsculas, números e caracteres especiais |
| RN025 | Sistema | Tentativas de login com falha acima de 5 vezes em 15 minutos devem bloquear temporariamente a conta por 30 minutos |
| RN026 | Sistema | Tokens JWT expirados devem ser renovados automaticamente se o refresh token ainda for válido |
| RN027 | Administrador | Documentos enviados devem ser verificados quanto a vírus antes de serem armazenados |
| RN028 | Sistema | Relatórios com mais de 10.000 registros devem ser processados de forma assíncrona |
| RN029 | Gestor | Acesso a dados sensíveis (histórico completo, documentos) requer autenticação de dois fatores para gestores |
| RN030 | Sistema | Exportação de dados pessoais deve gerar log de auditoria incluindo: quem exportou, quando, quais dados |

---

## 4. Casos de Uso

### 4.1 Atores

| ID | ATOR | DESCRIÇÃO |
|----|------|-----------|
| AT001 | Administrador do Sistema | Usuário com permissões completas para configurar o sistema, gerenciar usuários, definir parâmetros globais e acessar todas as funcionalidades. Responsável pela manutenção técnica e operacional da plataforma. |
| AT002 | Gestor Escolar | Diretor ou coordenador pedagógico com acesso a relatórios estratégicos, aprovação de processos críticos e visualização completa de dados acadêmicos. Responsável pelas decisões pedagógicas e administrativas. |
| AT003 | Secretaria/Administrativo | Responsável por processos administrativos como matrícula de alunos, cadastro de professores, emissão de documentos e gestão de dados cadastrais. |
| AT004 | Professor | Docente responsável por registrar presenças, lançar notas, visualizar suas turmas e disciplinas, e acompanhar o desempenho dos alunos sob sua responsabilidade. |
| AT005 | Aluno | Estudante matriculado que acessa o sistema para consultar suas notas, frequência, horários, comunicados e histórico acadêmico. |
| AT006 | Pai/Responsável | Responsável legal pelo aluno que acessa o sistema para acompanhar o desempenho acadêmico, frequência e receber notificações sobre o estudante. |
| AT007 | Sistema | Componente automatizado que executa processos em background como: envio de notificações, cálculo de médias, geração de relatórios agendados e verificações de regras de negócio. |

### 4.2 Casos de Uso

| ID | ATOR | CASO DE USO |
|----|------|-------------|
| UC001 | Administrador, Secretaria | Realizar login no sistema utilizando email e senha ou OAuth2 (Google/Microsoft) |
| UC002 | Todos | Recuperar senha esquecida através de email com link de redefinição |
| UC003 | Secretaria | Cadastrar novo aluno informando dados pessoais, documentos e responsáveis |
| UC004 | Secretaria | Editar dados cadastrais de aluno existente |
| UC005 | Secretaria | Realizar matrícula de aluno em turma específica |
| UC006 | Secretaria | Fazer upload de documentos do aluno (RG, histórico, certidões) |
| UC007 | Administrador, Secretaria, Professor | Buscar aluno por matrícula, nome, CPF ou turma |
| UC008 | Gestor | Exportar lista de alunos em formato PDF ou CSV |
| UC009 | Secretaria | Cadastrar novo professor informando qualificações e disciplinas habilitadas |
| UC010 | Administrador | Atribuir disciplinas e turmas a professor |
| UC011 | Professor | Visualizar horário semanal com turmas e disciplinas |
| UC012 | Administrador, Secretaria | Criar nova turma definindo série, turno e capacidade |
| UC013 | Administrador | Criar disciplina especificando nome, código e carga horária |
| UC014 | Administrador | Definir calendário escolar com períodos letivos e feriados |
| UC015 | Secretaria | Importar dados de turmas via planilha Excel |
| UC016 | Professor | Registrar presença diária de alunos da turma |
| UC017 | Professor | Gerar QR Code para registro de presença via smartphone |
| UC018 | Aluno | Registrar presença escaneando QR Code exibido pelo professor |
| UC019 | Professor, Gestor, Pai | Consultar relatório de frequência de aluno/turma |
| UC020 | Sistema | Enviar notificação automática de falta para responsáveis |
| UC021 | Professor | Lançar nota de avaliação para alunos da turma |
| UC022 | Sistema | Calcular automaticamente média do aluno conforme pesos configurados |
| UC023 | Aluno, Pai | Consultar notas e histórico de avaliações |
| UC024 | Sistema | Notificar aluno e pais sobre lançamento de novas notas |
| UC025 | Gestor | Gerar relatório de desempenho acadêmico por turma/disciplina |
| UC026 | Gestor | Visualizar dashboard executivo com indicadores da escola |
| UC027 | Gestor, Administrador | Enviar comunicado geral para grupos de usuários |
| UC028 | Professor | Enviar mensagem individual para aluno ou responsável |
| UC029 | Pai | Visualizar histórico de comunicados recebidos |
| UC030 | Aluno | Consultar horário de aulas da semana |
| UC031 | Administrador | Gerenciar perfis e permissões de usuários |
| UC032 | Administrador | Configurar parâmetros do sistema (média de aprovação, pesos, etc) |
| UC033 | Gestor | Gerar relatório de alunos em risco de evasão por baixa frequência |
| UC034 | Professor | Consultar histórico acadêmico completo de aluno |
| UC035 | Sistema | Realizar backup automático dos bancos de dados |
| UC036 | Administrador | Monitorar métricas de performance via Grafana |
| UC037 | Administrador | Consultar logs de auditoria de operações críticas |
| UC038 | Secretaria | Emitir declaração de matrícula para aluno |
| UC039 | Secretaria | Emitir histórico escolar completo |
| UC040 | Todos | Alterar senha de acesso ao sistema |

---

## 5. Diagrama de Classes

### Principais Classes do Domínio

```
┌─────────────────────┐
│      Usuario        │
├─────────────────────┤
│ - id: Long          │
│ - email: String     │
│ - senha: String     │
│ - perfil: Enum      │
│ - ativo: Boolean    │
│ - dataCriacao: Date │
├─────────────────────┤
│ + autenticar()      │
│ + redefinirSenha()  │
└─────────────────────┘
         △
         │
    ┌────┴────┬──────────┬────────────┐
    │         │          │            │
┌───┴───┐ ┌──┴──┐  ┌────┴─────┐ ┌───┴────┐
│ Admin │ │ Aluno│  │Professor │ │  Pai   │
└───────┘ └──┬──┘  └────┬─────┘ └───┬────┘
             │          │            │
             │          │            │
    ┌────────┴──────────┼────────────┘
    │                   │
┌───┴──────────┐   ┌───┴──────────┐
│    Pessoa    │   │  Responsavel  │
├──────────────┤   ├───────────────┤
│ - nome       │   │ - parentesco  │
│ - cpf        │   │ - telefone    │
│ - dataNasc   │   └───────────────┘
│ - endereco   │
└──────────────┘

┌─────────────────────┐      ┌─────────────────────┐
│       Turma         │      │     Disciplina      │
├─────────────────────┤      ├─────────────────────┤
│ - id: Long          │      │ - id: Long          │
│ - codigo: String    │      │ - codigo: String    │
│ - nome: String      │      │ - nome: String      │
│ - serie: String     │      │ - cargaHoraria: int │
│ - turno: Enum       │      │ - ementa: String    │
│ - anoLetivo: int    │      └─────────────────────┘
│ - capacidade: int   │               │
├─────────────────────┤               │
│ + matricular()      │      ┌────────┴────────┐
│ + verificarVaga()   │      │   Atribuicao    │
└─────────────────────┘      ├─────────────────┤
         │                   │ - professor     │
         │ 1..*              │ - disciplina    │
         │                   │ - turma         │
         │                   │ - dataInicio    │
    ┌────┴────┐             └─────────────────┘
    │Matricula│
    ├─────────┤
    │ - aluno │
    │ - turma │
    │ - data  │
    │ - status│
    └─────────┘

┌─────────────────────┐      ┌─────────────────────┐
│     Presenca        │      │       Nota          │
├─────────────────────┤      ├─────────────────────┤
│ - id: Long          │      │ - id: Long          │
│ - aluno: Aluno      │      │ - aluno: Aluno      │
│ - disciplina        │      │ - disciplina        │
│ - data: Date        │      │ - avaliacao         │
│ - status: Enum      │      │ - valor: Double     │
│ - professor         │      │ - dataLancamento    │
├─────────────────────┤      ├─────────────────────┤
│ + registrar()       │      │ + calcularMedia()   │
│ + calcularPerc()    │      │ + validarNota()     │
└─────────────────────┘      └─────────────────────┘

┌─────────────────────┐      ┌─────────────────────┐
│    Notificacao      │      │      Documento      │
├─────────────────────┤      ├─────────────────────┤
│ - id: Long          │      │ - id: Long          │
│ - destinatario      │      │ - aluno: Aluno      │
│ - titulo: String    │      │ - tipo: Enum        │
│ - mensagem: String  │      │ - arquivo: String   │
│ - tipo: Enum        │      │ - dataUpload: Date  │
│ - dataEnvio: Date   │      │ - tamanho: Long     │
│ - lida: Boolean     │      └─────────────────────┘
├─────────────────────┤
│ + enviar()          │
│ + marcarComoLida()  │
└─────────────────────┘
```

---

## 6. Arquitetura de Sistemas Distribuídos

### 6.1 Visão Geral da Arquitetura

O DistriSchool adota uma arquitetura de microsserviços distribuídos baseada nos seguintes princípios:

**Padrões Arquiteturais:**
- Microservices Architecture
- API Gateway Pattern
- Database per Service Pattern
- Event-Driven Architecture
- CQRS (Command Query Responsibility Segregation) para relatórios
- Circuit Breaker Pattern
- Service Discovery

### 6.2 Camadas da Arquitetura

```
┌─────────────────────────────────────────────────────────┐
│                    CAMADA DE CLIENTE                     │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │  Web Browser │  │ Mobile App   │  │  Admin Panel │  │
│  │   (React)    │  │ (React Native│  │   (React)    │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
                           │ HTTPS/WSS
                           ▼
┌─────────────────────────────────────────────────────────┐
│                    CAMADA DE GATEWAY                     │
│               ┌──────────────────────────┐               │
│               │   Spring Cloud Gateway   │               │
│               │  - Roteamento            │               │
│               │  - Load Balancing        │               │
│               │  - Rate Limiting         │               │
│               │  - Authentication        │               │
│               └──────────────────────────┘               │
└─────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│                 CAMADA DE MICROSSERVIÇOS                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌─────────┐ │
│  │  User    │  │ Student  │  │ Teacher  │  │  Grade  │ │
│  │ Service  │  │ Service  │  │ Service  │  │ Service │ │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬────┘ │
│       │             │             │             │       │
│  ┌────┴─────┐  ┌───┴──────┐  ┌───┴──────┐  ┌───┴────┐ │
│  │Attendance│  │Notification│ │ Report   │  │Schedule│ │
│  │ Service  │  │  Service   │ │ Service  │  │Service │ │
│  └──────────┘  └────────────┘ └──────────┘  └────────┘ │
└─────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│                  CAMADA DE MENSAGERIA                    │
│               ┌──────────────────────────┐               │
│               │      Apache Kafka        │               │
│               │  Topics:                 │               │
│               │  - student.created       │               │
│               │  - notification.sent     │               │
│               │  - attendance.recorded   │               │
│               │  - grade.published       │               │
│               └──────────────────────────┘               │
└─────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│                  CAMADA DE PERSISTÊNCIA                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌─────────┐ │
│  │PostgreSQL│  │PostgreSQL│  │PostgreSQL│  │ MongoDB │ │
│  │  (User)  │  │(Student) │  │ (Grade)  │  │(Docs)   │ │
│  └──────────┘  └──────────┘  └──────────┘  └─────────┘ │
│  ┌──────────────────────────────────────────────────┐   │
│  │              Redis Cache Cluster                 │   │
│  └──────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│               CAMADA DE INFRAESTRUTURA                   │
│  ┌────────────┐  ┌───────────┐  ┌──────────────────┐   │
│  │ Kubernetes │  │Prometheus │  │   ELK Stack      │   │
│  │  Cluster   │  │ Grafana   │  │  (Logs)          │   │
│  └────────────┘  └───────────┘  └──────────────────┘   │
│  ┌──────────────────────────────────────────────────┐   │
│  │         AWS/Azure Cloud Infrastructure           │   │
│  │  - S3/Blob Storage  - EKS/AKS  - RDS/CosmosDB   │   │
│  └──────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

### 6.3 Detalhamento dos Microsserviços

**User Service (Serviço de Usuários)**
- Responsabilidade: Autenticação, autorização, gestão de perfis
- Tecnologias: Spring Boot, Spring Security, JWT, OAuth2
- Banco de Dados: PostgreSQL
- APIs: REST
- Comunicação: Publica eventos `user.created`, `user.logged`

**Student Service (Serviço de Alunos)**
- Responsabilidade: CRUD de alunos, matrículas, histórico acadêmico
- Tecnologias: Spring Boot, Spring Data JPA
- Banco de Dados: PostgreSQL
- APIs: REST
- Comunicação: Publica `student.created`, consome `grade.published`

**Teacher Service (Serviço de Professores)**
- Responsabilidade: Gestão de professores, atribuições, horários
- Tecnologias: Spring Boot, Spring Data JPA, Spring Scheduler
- Banco de Dados: PostgreSQL
- APIs: REST
- Comunicação: Publica `teacher.assigned`

**Grade Service (Serviço de Notas)**
- Responsabilidade: Lançamento de notas, cálculo de médias
- Tecnologias: Spring Boot, RabbitMQ
- Banco de Dados: PostgreSQL
- APIs: REST
- Comunicação: Publica `grade.published`, processamento assíncrono

**Attendance Service (Serviço de Presenças)**
- Responsabilidade: Registro de presenças, cálculo de frequência
- Tecnologias: Spring Boot, WebSocket
- Banco de Dados: PostgreSQL
- APIs: REST, WebSocket
- Comunicação: Publica `attendance.recorded`

**Notification Service (Serviço de Notificações)**
- Responsabilidade: Envio de notificações (email, SMS, push)
- Tecnologias: Spring Boot, Kafka Consumer, Spring Mail
- Banco de Dados: MongoDB (histórico de notificações)
- Comunicação: Consome todos os eventos relevantes

**Report Service (Serviço de Relatórios)**
- Responsabilidade: Geração de relatórios e análises
- Tecnologias: Python, gRPC, Pandas, ML libraries
- Banco de Dados: MongoDB (agregações)
- APIs: gRPC
- Comunicação: Consulta dados de outros serviços

**Schedule Service (Serviço de Horários)**
- Responsabilidade: Gestão de calendário, horários, conflitos
- Tecnologias: Spring Boot, Spring Data JPA
- Banco de Dados: PostgreSQL
- APIs: REST
- Comunicação: Publica `schedule.updated`

### 6.4 Padrões de Comunicação

**Síncrona (REST/gRPC):**
- Consultas imediatas (busca de aluno, login)
- Operações que requerem resposta imediata
- Comunicação entre API Gateway e serviços

**Assíncrona (Kafka):**
- Notificações (envio de emails, alertas)
- Processamento em background (cálculo de médias)
- Eventos de domínio (criação de aluno, publicação de nota)

### 6.5 Estratégias de Resiliência

**Circuit Breaker (Resilience4J):**
```
- Threshold: 50% de falhas em 10 requisições
- Wait Duration: 60 segundos
- Sliding Window: 100 requisições
```

**Retry Policy:**
```
- Max Attempts: 3
- Wait Duration: 2 segundos (exponential backoff)
- Retryable Exceptions: TimeoutException, ConnectionException
```

**Rate Limiting:**
```
- 100 requisições/minuto por usuário
- 1000 requisições/minuto por serviço
```

### 6.6 Estratégia de Deploy

**Containerização:**
- Cada microsserviço em container Docker independente
- Multi-stage builds para otimização de imagem
- Health checks configurados

**Orquestração Kubernetes:**
- Deployments com réplicas configuráveis (mínimo 2 por serviço)
- Horizontal Pod Autoscaler (HPA) baseado em CPU/Memória
- Services para descoberta de serviços
- Ingress Controller para roteamento externo

**CI/CD Pipeline:**
```
1. Commit → GitHub
2. GitHub Actions trigger
3. Build & Unit Tests
4. Docker Image Build
5. Push to Registry (ECR/ACR)
6. Deploy to K8s (staging)
7. Integration Tests
8. Deploy to K8s (production)
```

### 6.7 Monitoramento e Observabilidade

**Métricas (Prometheus):**
- Latência de requisições (p50, p95, p99)
- Throughput (req/s)
- Taxa de erro (%)
- Uso de recursos (CPU, memória)

**Logs (ELK Stack):**
- Logs estruturados em JSON
- Correlation ID para rastreamento distribuído
- Níveis: ERROR, WARN, INFO, DEBUG

**Tracing Distribuído:**
- Jaeger para trace de requisições cross-service
- Visualização de latência por serviço

**Alertas:**
- Taxa de erro > 5% por 5 minutos
- Latência p95 > 3 segundos
- CPU > 80% por 10 minutos
- Memória > 85%

---

## 7. Apêndice A: Glossário

**Termos e Definições:**

**AKS (Azure Kubernetes Service):** Serviço gerenciado de Kubernetes da Microsoft Azure para orquestração de containers.

**API Gateway:** Ponto único de entrada para todas as requisições externas, responsável por roteamento, autenticação e rate limiting.

**Apache Kafka:** Plataforma distribuída de streaming de eventos usada para comunicação assíncrona entre microsserviços.

**Artifact:** Pacote de software gerado como resultado do processo de build (JAR, WAR, Docker Image).

**Ator:** Entidade externa (pessoa ou sistema) que interage com o sistema.

**Availability (Disponibilidade):** Percentual de tempo que o sistema está operacional e acessível.

**Backup:** Cópia de segurança dos dados do sistema para recuperação em caso de falhas.

**BCrypt:** Algoritmo de hash para criptografia de senhas com salt automático.

**Circuit Breaker:** Padrão de design que previne cascata de falhas interrompendo chamadas a serviços com problemas.

**CRUD:** Create, Read, Update, Delete - operações básicas de manipulação de dados.

**Dashboard:** Painel visual com indicadores e métricas do sistema.

**Deploy:** Processo de implantação de uma nova versão do software em ambiente de produção.

**Docker:** Plataforma de containerização que empacota aplicações e suas dependências.

**ECR (Elastic Container Registry):** Serviço de registro de imagens Docker da AWS.

**EKS (Elastic Kubernetes Service):** Serviço gerenciado de Kubernetes da AWS.

**ELK Stack:** Conjunto de ferramentas (Elasticsearch, Logstash, Kibana) para análise de logs.

**Event-Driven Architecture:** Arquitetura baseada em eventos assíncronos entre componentes.

**Flyway:** Ferramenta de versionamento e migração de banco de dados.

**Grafana:** Plataforma de visualização e análise de métricas.

**gRPC:** Framework RPC de alto desempenho desenvolvido pelo Google.

**Health Check:** Endpoint que verifica se um serviço está operacional.

**Horizontal Scaling:** Adicionar mais instâncias do serviço para aumentar capacidade.

**IaaS (Infrastructure as a Service):** Modelo de nuvem que fornece infraestrutura virtualizada.

**Ingress Controller:** Componente K8s que gerencia acesso externo aos serviços.

**JWT (JSON Web Token):** Padrão de token para autenticação baseada em claims.

**Kubernetes (K8s):** Sistema de orquestração de containers open-source.

**Latência:** Tempo de resposta entre envio de requisição e recebimento da resposta.

**LGPD:** Lei Geral de Proteção de Dados (Lei nº 13.709/2018).

**Load Balancing:** Distribuição de carga entre múltiplas instâncias de um serviço.

**Microservice:** Serviço pequeno, independente e focado em uma responsabilidade específica.

**MongoDB:** Banco de dados NoSQL orientado a documentos.

**OAuth2:** Protocolo de autorização para acesso seguro a recursos.

**PaaS (Platform as a Service):** Modelo de nuvem que fornece plataforma de desenvolvimento.

**Pod:** Menor unidade de deploy no Kubernetes, contém um ou mais containers.

**PostgreSQL:** Sistema de gerenciamento de banco de dados relacional open-source.

**Prometheus:** Sistema de monitoramento e alerta baseado em métricas.

**QR Code:** Código de barras bidimensional usado para registro rápido.

**Rate Limiting:** Limitação de número de requisições por período de tempo.

**Redis:** Banco de dados em memória usado para cache distribuído.

**Replica:** Cópia de uma instância de serviço para alta disponibilidade.

**Resilience4J:** Biblioteca Java para implementação de padrões de resiliência.

**REST (Representational State Transfer):** Estilo arquitetural para APIs web.

**Retry Policy:** Política de tentativas automáticas após falha.

**RPO (Recovery Point Objective):** Perda máxima de dados aceitável medida em tempo.

**RTO (Recovery Time Objective):** Tempo máximo aceitável para recuperação do sistema.

**S3 (Simple Storage Service):** Serviço de armazenamento de objetos da AWS.

**Service Discovery:** Mecanismo para localizar serviços dinamicamente na rede.

**SLA (Service Level Agreement):** Acordo de nível de serviço com garantias de disponibilidade.

**SMTP (Simple Mail Transfer Protocol):** Protocolo padrão para envio de emails.

**Soft Delete:** Exclusão lógica de dados mantendo-os no banco com flag de inativo.

**Spring Boot:** Framework Java para criação de aplicações stand-alone.

**Spring Cloud:** Conjunto de ferramentas para construção de sistemas distribuídos.

**Spring Data JPA:** Abstração do Spring para persistência com JPA/Hibernate.

**Spring Security:** Framework para autenticação e autorização em aplicações Spring.

**SSL/TLS:** Protocolos criptográficos para comunicação segura na internet.

**Terraform:** Ferramenta de Infrastructure as Code para provisionamento de recursos.

**Throughput:** Quantidade de requisições processadas por unidade de tempo.

**Token:** Credencial usada para autenticação após login bem-sucedido.

**Uptime:** Tempo total que o sistema permanece operacional.

**Vite:** Ferramenta de build para aplicações frontend moderna e rápida.

**WCAG (Web Content Accessibility Guidelines):** Diretrizes de acessibilidade web.

**WebSocket:** Protocolo de comunicação bidirecional em tempo real sobre TCP.

---

## 8. Apêndice B: Modelos de Análise

### 8.1 Diagrama de Fluxo de Dados (DFD) - Nível 0

```
                    ┌──────────────┐
                    │   Aluno/Pai  │
                    └──────┬───────┘
                           │
                           │ Consultas
                           ▼
        ┌──────────────────────────────────┐
        │                                  │
┌───────┴────────┐              ┌─────────┴────────┐
│   Professor    │              │    Secretaria    │
└───────┬────────┘              └─────────┬────────┘
        │                                  │
        │ Lançamentos                      │ Cadastros
        │                                  │
        ▼                                  ▼
┌────────────────────────────────────────────────────┐
│                                                    │
│            SISTEMA DISTRISCHOOL                    │
│                                                    │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐        │
│  │ Gestão   │  │ Gestão   │  │ Gestão   │        │
│  │ Alunos   │  │ Notas    │  │ Presença │        │
│  └──────────┘  └──────────┘  └──────────┘        │
│                                                    │
└────────────────────┬───────────────────────────────┘
                     │
                     │ Relatórios
                     ▼
              ┌──────────────┐
              │    Gestor    │
              └──────────────┘
```

### 8.2 Diagrama Entidade-Relacionamento (ER)

```
┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│   ALUNO     │         │  MATRICULA  │         │    TURMA    │
├─────────────┤         ├─────────────┤         ├─────────────┤
│ PK id       │         │ PK id       │         │ PK id       │
│    nome     │────1:N──│ FK aluno_id │──N:1────│    codigo   │
│    cpf      │         │ FK turma_id │         │    nome     │
│    data_nasc│         │    data     │         │    serie    │
│    endereco │         │    status   │         │    turno    │
└─────────────┘         └─────────────┘         │    ano_let  │
      │                                          │    capacid  │
      │                                          └─────────────┘
      │ 1:N                                            │ 1:N
      │                                                │
      ▼                                                ▼
┌─────────────┐                              ┌─────────────┐
│  PRESENCA   │                              │ ATRIBUICAO  │
├─────────────┤                              ├─────────────┤
│ PK id       │                              │ PK id       │
│ FK aluno_id │                              │ FK prof_id  │
│ FK disc_id  │                              │ FK turma_id │
│    data     │                              │ FK disc_id  │
│    status   │                              │    periodo  │
└─────────────┘                              └─────────────┘
                                                     △
                                                     │ N:1
                                                     │
                                              ┌─────────────┐
┌─────────────┐                              │  PROFESSOR  │
│    NOTA     │                              ├─────────────┤
├─────────────┤                              │ PK id       │
│ PK id       │                              │    nome     │
│ FK aluno_id │──────────────────────────────│    cpf      │
│ FK aval_id  │                         1:N  │    formacao │
│    valor    │                              │    contato  │
│    data     │                              └─────────────┘
└─────────────┘
      △
      │ N:1
      │
┌─────────────┐         ┌─────────────┐
│  AVALIACAO  │         │ DISCIPLINA  │
├─────────────┤         ├─────────────┤
│ PK id       │──N:1────│ PK id       │
│ FK disc_id  │         │    codigo   │
│    nome     │         │    nome     │
│    peso     │         │    carga_h  │
│    data     │         │    ementa   │
└─────────────┘         └─────────────┘
```

### 8.3 Diagrama de Sequência - Registro de Presença

```
Professor    API Gateway    Attendance    Kafka    Notification    Pai
   │              │           Service       │        Service       │
   │──login────▶│             │             │          │           │
   │◀───token───│             │             │          │           │
   │              │             │             │          │           │
   │──POST /attendance─────────▶│            │          │           │
   │              │             │            │          │           │
   │              │             │─validar────│          │           │
   │              │             │            │          │           │
   │              │             │─save DB────│          │           │
   │              │             │            │          │           │
   │              │             │──publish───▶│         │           │
   │              │             │  (attendance.recorded)│           │
   │              │             │            │          │           │
   │◀─────200 OK────────────────│            │          │           │
   │              │             │            │          │           │
   │              │             │            │──consume─▶│          │
   │              │             │            │          │           │
   │              │             │            │      verificar       │
   │              │             │            │        falta         │
   │              │             │            │          │           │
   │              │             │            │    enviar email      │
   │              │             │            │          │──────────▶│
   │              │             │            │          │           │
```

### 8.4 Diagrama de Implantação

```
┌────────────────────────────────────────────────────────────────┐
│                      AWS/AZURE CLOUD                           │
│                                                                │
│  ┌──────────────────────────────────────────────────────────┐ │
│  │               KUBERNETES CLUSTER                         │ │
│  │                                                          │ │
│  │  ┌────────────────┐         ┌────────────────┐         │ │
│  │  │  API Gateway   │         │  User Service  │         │ │
│  │  │   (Pod x2)     │         │    (Pod x3)    │         │ │
│  │  └────────────────┘         └────────────────┘         │ │
│  │                                                          │ │
│  │  ┌────────────────┐         ┌────────────────┐         │ │
│  │  │Student Service │         │Teacher Service │         │ │
│  │  │    (Pod x3)    │         │    (Pod x2)    │         │ │
│  │  └────────────────┘         └────────────────┘         │ │
│  │                                                          │ │
│  │  ┌────────────────┐         ┌────────────────┐         │ │
│  │  │ Grade Service  │         │Attendance Svc  │         │ │
│  │  │    (Pod x2)    │         │    (Pod x2)    │         │ │
│  │  └────────────────┘         └────────────────┘         │ │
│  │                                                          │ │
│  └──────────────────────────────────────────────────────────┘ │
│                                                                │
│  ┌──────────────────────────────────────────────────────────┐ │
│  │                    KAFKA CLUSTER                         │ │
│  │             (3 brokers + Zookeeper)                      │ │
│  └──────────────────────────────────────────────────────────┘ │
│                                                                │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │ PostgreSQL   │  │  MongoDB     │  │ Redis Cluster│       │
│  │   (RDS)      │  │  (Atlas)     │  │  (3 nodes)   │       │
│  └──────────────┘  └──────────────┘  └──────────────┘       │
│                                                                │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │  Prometheus  │  │   Grafana    │  │  ELK Stack   │       │
│  └──────────────┘  └──────────────┘  └──────────────┘       │
│                                                                │
└────────────────────────────────────────────────────────────────┘
                           △
                           │ HTTPS
                           │
                    ┌──────┴──────┐
                    │   CLIENTS   │
                    │ Web/Mobile  │
                    └─────────────┘
```

### 8.5 Diagrama de Estados - Matrícula do Aluno

```
                    ┌──────────────┐
                    │  [INICIAL]   │
                    └──────┬───────┘
                           │
                   cadastro realizado
                           │
                           ▼
                    ┌──────────────┐
              ┌─────│  PENDENTE    │
              │     └──────┬───────┘
              │            │
              │    documentos enviados
              │            │
    rejeitar  │            ▼
    documento │     ┌──────────────┐
              │     │   ANÁLISE    │────┐
              └────▶└──────┬───────┘    │
                           │            │
                    aprovado            │ documentos
                           │            │ incompletos
                           ▼            │
                    ┌──────────────┐    │
                    │   APROVADO   │◀───┘
                    └──────┬───────┘
                           │
                  matrícula efetivada
                           │
                           ▼
                    ┌──────────────┐
         ┌──────────│  MATRICULADO │
         │          └──────┬───────┘
         │                 │
    cancelamento    conclusão/transferência
         │                 │
         │                 ▼
         │          ┌──────────────┐
         └─────────▶│   INATIVO    │
                    └──────────────┘
```

### 8.6 Diagrama de Componentes - Microsserviço Student

```
┌─────────────────────────────────────────────────────────┐
│              STUDENT MICROSERVICE                       │
│                                                         │
│  ┌──────────────────────────────────────────────────┐  │
│  │           API REST Layer                         │  │
│  │  ┌──────────────┐  ┌──────────────┐            │  │
│  │  │StudentController│ ErrorHandler  │            │  │
│  │  └──────────────┘  └──────────────┘            │  │
│  └────────────────┬───────────────────────────────────┘  │
│                   │                                      │
│  ┌────────────────┴───────────────────────────────────┐  │
│  │          Service Layer                            │  │
│  │  ┌──────────────┐  ┌──────────────┐              │  │
│  │  │StudentService│  │ValidationSvc │              │  │
│  │  └──────────────┘  └──────────────┘              │  │
│  └────────────────┬───────────────────────────────────┘  │
│                   │                                      │
│  ┌────────────────┴───────────────────────────────────┐  │
│  │        Repository Layer                           │  │
│  │  ┌──────────────┐  ┌──────────────┐              │  │
│  │  │StudentRepo   │  │DocumentRepo  │              │  │
│  │  │  (JPA)       │  │  (JPA)       │              │  │
│  │  └──────────────┘  └──────────────┘              │  │
│  └────────────────┬───────────────────────────────────┘  │
│                   │                                      │
│  ┌────────────────┴───────────────────────────────────┐  │
│  │         Integration Layer                         │  │
│  │  ┌──────────────┐  ┌──────────────┐              │  │
│  │  │KafkaProducer │  │CacheManager  │              │  │
│  │  └──────────────┘  └──────────────┘              │  │
│  └─────────────────────────────────────────────────────┘  │
│                                                         │
└─────────────────────────────────────────────────────────┘
                    │              │
                    ▼              ▼
            ┌──────────┐    ┌──────────┐
            │PostgreSQL│    │  Kafka   │
            └──────────┘    └──────────┘
```

---
