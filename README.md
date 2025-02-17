<div align="center" style="font-family: Arial, sans-serif; font-size: 20px; line-height: 1.5;">

# 💻☁️ **Curso DPCN-EDN** 💻☁️
# 🌟 Solutions Architect Associate  🌟

###
<a href="https://escoladanuvem.org"><a href="https://aws.amazon.com/pt/?nc2=h_lg">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/Amazon_Web_Services_Logo.svg/2560px-Amazon_Web_Services_Logo.svg.png" width="180" alt="AWS Logo">
</a>
<img src="https://miro.medium.com/v2/resize:fit:512/0*81xCYukT_2jKzxgJ.png" width="110" alt="AWS Logo">- <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSBfRQV8LLwGpQciyGQ2drjckBDVvZCECVdzA&s" width="110" alt="AWS Logo">-<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ47Ji1yhUawSLNBXPp8UERlP7nKo3d1f2EKw&s" width="110" alt="AWS Logo">- 
    <img src="edn.png" width="200" alt="Second Image">
</a>
</div>


# 🏗️ Laboratório: Auto Scaling e Load Balancing na AWS

**Turma:** DPCN 07  
**Aluno:** Álifi Ralph 

## 📌 Objetivos
Este laboratório ensina como configurar um ambiente web altamente disponível e escalável na **AWS**, utilizando:

✅ **Auto Scaling Groups** – Para gerenciar automaticamente o número de instâncias EC2 conforme a demanda.
✅ **Launch Templates** – Para definir as configurações das instâncias EC2.
✅ **Application Load Balancer** – Para distribuir o tráfego de entrada de maneira inteligente.

---

## 🔧 Pré-requisitos
- Conta AWS ativa
- Permissões IAM: `AmazonEC2FullAccess`, `AmazonEC2AutoScalingFullAccess`, `ElasticLoadBalancingFullAccess`
- Navegador Web

---

## 🚀 Passo a Passo

### 1️⃣ Configuração da VPC
1. Acesse o **Console AWS** e selecione a região `us-east-1`.
2. No menu de pesquisa, digite **VPC** e selecione o serviço.
3. Verifique a **VPC padrão** (`Default VPC = Yes`).
4. Anote o **ID da VPC** (`vpc-xxxxxxxxxxxxxxxxx`).
5. Verifique as **subnets** disponíveis e anote os IDs (`subnet-xxxxxxxxxxxxxxxxx`).

📸 **Print da VPC padrão:** 

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/VPC-Default.png?raw=true" width="800" alt="aws">
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/VPC-Route-Tables.png?raw=true" width="800">- 
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/Note-pad.png?raw=true" width="800" alt="AWS Logo">-

---

### 2️⃣ Criar um Security Group
1. Acesse **EC2 > Security Groups**.
2. Crie um novo Security Group:
   - **Nome:** `SG-Lab-SeuNome`
   - **Descrição:** HTTP, HTTPS, SSH
   - **VPC:** VPC padrão
   - **Inbound Rules:**
     - HTTP: `0.0.0.0/0`
     - HTTPS: `0.0.0.0/0`
     - SSH: `45.167.210.64/32`
3. Salve as configurações.

📸 **Print do Security Group:** 

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/Confi-Security-Group-Acess.png?raw=true">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/ASG-Create.png?raw=true">-

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

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/arquivos01/Launch-do-Ralph.png?raw=true" width="800" alt="aws"> 
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/arquivos01/Quick-Start.png?raw=true" width="800" alt="aws">
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/arquivos01/Launch-do-Ralph-02.png?raw=true" width="800" alt="aws">
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/arquivos01/Launch-Template.png?raw=true" width="800" alt="aws">
