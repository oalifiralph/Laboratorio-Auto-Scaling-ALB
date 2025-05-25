<div align="center" style="font-family: Arial, sans-serif; font-size: 20px; line-height: 1.5;">

# ☁️ **Curso DPCN-EDN** ☁️
# 👨🏻‍💻 Solutions Architect Associate  👨🏻‍💻

###
<img src="https://figmaresource.com/wp-content/uploads/2024/05/AWS-Marketplace-Logo-PNG-to-svg-1.svg" width="100" alt="AWS logo">
<img src="https://cloud-icons.onemodel.app/aws/Architecture-Service-Icons_01312023/Arch_Networking-Content-Delivery/64/Arch_Amazon-Virtual-Private-Cloud_64.svg" width="100" alt="AWS VPC"> 
<img src="https://cloud-icons.onemodel.app/aws/Architecture-Service-Icons_01312023/Arch_Compute/64/Arch_Amazon-EC2-Auto-Scaling_64.svg" width="100" alt="AWS EC2">
<img src="https://cloud-icons.onemodel.app/aws/Architecture-Service-Icons_01312023/Arch_Networking-Content-Delivery/64/Arch_Elastic-Load-Balancing_64.svg" width="100" alt="AWS ELB"> 
<img src="https://github.com/oalifiralph/oalifiralph/blob/main/img/EDN-Logo.svg" width="113" alt="Second Image">

</div>


# 👨🏻‍🔬  Laboratório:

## Aplicação de Auto Scaling e Load Balancing na instância EC2

**Turma:** DPCN 07  
**Aluno:** Álifi Ralph 

## 📌 Objetivos
Este laboratório ensina como configurar um ambiente web altamente disponível e escalável na **AWS**, utilizando:

✅ **Auto Scaling Groups** – Para gerenciar automaticamente o número de instâncias EC2 conforme a demanda.

✅ **Launch Templates** – Para definir as configurações das instâncias EC2.

✅ **Application Load Balancer** – Para distribuir o tráfego de entrada de maneira inteligente.

---

## 💡 Cenário:

Uma plataforma de streaming de vídeos está expandindo sua base de usuários e precisa garantir que os espectadores tenham uma experiência fluida, mesmo durante eventos ao vivo ou lançamentos populares.

- O time de operações quer garantir que os servidores escalem automaticamente para suportar picos de acesso sem quedas de desempenho.

- O time de engenharia precisa distribuir o tráfego entre os servidores para evitar sobrecarga e garantir streaming contínuo.
- A equipe financeira busca otimizar custos, garantindo que apenas os servidores necessários estejam ativos a cada momento.
 
#### **Para atender a estes requisitos, você configurará Auto Scaling Groups, Launch Templates e Application Load Balancer, garantindo uma infraestrutura altamente escalável, resiliente e otimizada na AWS.**
---
## 📋 Pré-requisitos
### 
- 🪪 **Conta**: AWS ativa.
- 🔑 **Permissões IAM**: `AmazonEC2FullAccess`, `AmazonEC2AutoScalingFullAccess`, `ElasticLoadBalancingFullAccess` 
- 🌐 **Navegador Web**: **Google Chrome**, **Mozilla Firefox**, **Microsoft Edge**, **Safari**... 
---
## 🛜🔒 Configurações da VPC

## ⬇️ Workflow
1️⃣. Acesse o **Console AWS** e selecione a região de sua escolha, exemplo: `us-east-1`.

2️⃣. No menu de pesquisa, digite **VPC** e selecione o serviço.

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/VPC/VPC-Default.png?raw=true" width="1000" alt="VPC">
3️⃣. Verifique a **VPC padrão** (`Default VPC = Yes`).

4️⃣. Anote o **ID da VPC** (`vpc-xxxxxxxxxxxxxxxxx`).

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/VPC/VPC-Route-Tables.png?raw=true" width="1000" alt="VPC">- 
5️⃣. Verifique as **subnets** disponíveis e anote os IDs (`subnet-xxxxxxxxxxxxxxxxx`).

6️⃣. Revise as anotações e siga o fluxo das etapas

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/Note-pad.png?raw=true" width="1000" alt="NotePad">-

---

2️⃣3️⃣4️⃣5️⃣6️⃣

### 🔐 Configurações do Security Group
1️⃣. Acesse **EC2 > Security Groups**.

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/Confi-Security-Group-Acess.png?raw=true">-
<img src="https://raw.githubusercontent.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/refs/heads/main/ASG-Config.md/ASG-Create.png">-

2️⃣. Crie um novo Security Group:
   - **Nome:** `SG-Lab-SeuNome`
   - **Descrição:** HTTP, HTTPS, SSH
   - **VPC:** VPC padrão
   - **Inbound Rules:**
     - HTTP: `0.0.0.0/0`
     - HTTPS: `0.0.0.0/0`
     - SSH: `45.167.210.64/32`

3️⃣. Salve as configurações.

📸 **Print do Security Group:** 


---

### 3️⃣ Criar um Launch Template
1. Acesse **EC2 > Launch Templates**.
2. Crie um novo **Launch Template** com as configurações:
   - **Nome:** `LT-SeuNome`
   - **AMI:** `Amazon Linux 2`
   - **Tipo de Instância:** `t2.micro`
   - **Security Group:** `SG-Lab-SeuNome`
   - **User Data:**
     ```bash
     #!/bin/bash
     yum update -y
     yum install -y httpd
     systemctl start httpd
     systemctl enable httpd
     echo "<h1>Servidor Web - Instância: $(hostname -f)</h1>" > /var/www/html/index.html
     ```
3. Salve e crie o template.

📸 **Print do Launch Template:** 

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/LaunchTemplate/Launch-do-Ralph.png?raw=true?raw=true" width="400" alt="aws">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/LaunchTemplate/Quick-Start.png?raw=true?raw=true" width="400" alt="aws">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/LaunchTemplate/Launch-do-Ralph-02.png?raw=true?raw=true" width="400" alt="aws">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/LaunchTemplate/Launch-Template.png?raw=true?raw=true" width="400" alt="aws">-

---

### 4️⃣ Criar um Auto Scaling Group
1. Acesse **EC2 > Auto Scaling Groups**.
2. Crie um novo **Auto Scaling Group**:
   - **Nome:** `ASG-SeuNome`
   - **Launch Template:** `LT-SeuNome`
   - **VPC:** Selecione a VPC padrão
   - **Subnets:** Escolha pelo menos duas públicas
   - **Capacidade Inicial:** `1`, **Mínima:** `2`, **Máxima:** `permite até 20.000 instâncias por região em um Auto Scaling Group.`
   - **Attach to a Load Balancer:** Selecione **Application Load Balancer**
   - **Health Check:** Ativar **Elastic Load Balancer health check**
3. Finalize a criação.

📸 **Print do Auto Scaling Group e Load Balancer:** 

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/ASG-Config.md/ASG-Config-1.png?raw=true?raw=true" width="400" alt="aws">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/ASG-Config.md/ASG-Config-2.jpeg?raw=true?raw=true" width="400" alt="aws">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/ASG-Config.md/ASG-Config-3.png?raw=true?raw=true" width="400" alt="aws">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/ASG-Config.md/Health-Check.png?raw=true?raw=true" width="400" alt="aws">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/ASG-Config.md/ASG-Create.png?raw=true?raw=true" width="400" alt="aws">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/ASG-Config.md/ASG-Created.png?raw=true?raw=true" width="400" alt="aws">-

---

### 5️⃣ Testando o Ambiente

1. Copie o **DNS do Load Balancer** e acesse pelo navegador.
2. Atualize a página e veja que a instância EC2 muda (balanceamento funcionando!).
3. Monitore o **Auto Scaling Group** e verifique a criação automática de novas instâncias.

📸 **Print do Teste:**

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/EC2/Instance--.png?raw=true" width="430" alt="aws">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/EC2/Instance-.png?raw=true" width="400" alt="aws">-

---

🔎 **Dúvidas ou melhorias? Compartilhe suas experiências!** 🚀

#AWS #CloudComputing #EC2 #AutoScaling #LoadBalancing 
