# Meu Laboratório Pessoal: AWS IAM Least Privilege 🛡️

Olá! Este projeto é o resultado prático dos meus estudos focados em Cloud Computing.

Estudando na **Escola da Nuvem**, aprendi os conceitos fundamentais de nuvem e arquitetura, decidi criar este laboratório pessoal para colocar a mão na massa e **demonstrar na prática que eu entendo de segurança em cloud**.

Escrevi toda a infraestrutura deste laboratório em **AWS CloudFormation (YAML)** para provar como aplicar regras rígidas de acesso e proteger um ambiente AWS de verdade.

---

## 🧭 O que este projeto demonstra que eu sei fazer:

Neste laboratório, apliquei o princípio de **Least Privilege (Menor Privilégio)**. Criando o código bloco por bloco, eu demonstro que domino:

1. **Separação Segura de Usuários**:
   - O `usr-lab-admin` (Administrador controlado).
   - O `usr-lab-auditor` (Com permissão estrita de leitura/auditoria).
   - O `usr-lab-s3-operator` (Operador focado apenas em dados).
2. **Criação de Políticas Customizadas**:
   - Coloquei regras para garantir que o operador do S3 consiga ler e listar **apenas** o bucket de teste deste laboratório (`LabS3Bucket`), sem permissão para bisbilhotar ou alterar o restante da conta.
3. **Bloqueio Global por falta de MFA (Explicit Deny)**:
   - Inclui regra de segurança que monitora o administrador. Se ele tentar realizar ações críticas sem ter logado com o Segundo Fator de Autenticação (MFA), a AWS bloqueia ele na hora.
4. **IAM Roles para Segurança de Servidores**:
   - Sei que aplicações e máquinas virtuais (EC2) nunca devem guardar senhas ou chaves fixas (`Access Keys`). Criei uma Role para que o servidor ganhe acessos temporários automáticos para enviar métricas ao CloudWatch.

---

## 🧠 Minha Visão sobre Segurança Cloud

- **Por que o "AdministratorAccess" é perigoso?**
  Durante meus estudos, entendi que usar privilégio máximo no dia a dia é uma grande falha de segurança. Se um analista comete um erro ou se uma chave de acesso desse nível vaza na internet, um invasor toma conta da infraestrutura inteira, gerando risco de roubo de dados ou cobranças financeiras gigantescas.
- **Exemplos Práticos de Menor Privilégio**:
  - Uma aplicação web que só precisa salvar fotos não deve ter acesso para mexer na rede ou deletar servidores; ela recebe uma Role limitada apenas ao bucket de fotos.
  - Um profissional que monitora o uso de CPU das máquinas não precisa de permissão para desligá-las. O acesso dele deve ser limitado a visualização de gráficos de monitoramento.

---

## 🛠️ Como eu executo este projeto

Para validar o código, usei os comandos do **AWS CLI** no terminal para conversar direto com a AWS:

1. **Para criar o laboratório e os usuários na minha conta:**
   ```bash
   aws cloudformation create-stack \
     --stack-name meu-lab-seguranca-iam \
     --template-body file://template.yaml \
     --capabilities CAPABILITY_NAMED_IAM
   ```
2. **Para deletar tudo de forma limpa e segura após os testes:**
   ```bash
   aws cloudformation delete-stack --stack-name meu-lab-seguranca-iam
   ```

---

_Fique à vontade para olhar o histórico de commits deste repositório e ver como eu construí a segurança desse ambiente passo a passo!_

---

## ✉️ Contato e Conexões

- **LinkedIn**: [Seu Nome Completo](https://linkedin.com)
- **E-mail**: seu.email@exemplo.com
