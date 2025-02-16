<div align="center" style="font-family: Arial, sans-serif; font-size: 20px; line-height: 1.5;">

# 💻☁️ **Curso DPCN-EDN** 💻☁️
# 🌟 Solutions Architect Associate  🌟

###
<a href="https://escoladanuvem.org"><a href="https://aws.amazon.com/pt/?nc2=h_lg">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/Amazon_Web_Services_Logo.svg/2560px-Amazon_Web_Services_Logo.svg.png" width="180" alt="AWS Logo">
</a>
<img src="https://miro.medium.com/v2/resize:fit:512/0*81xCYukT_2jKzxgJ.png" width="80" alt="AWS Logo">- <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSBfRQV8LLwGpQciyGQ2drjckBDVvZCECVdzA&s" width="80" alt="AWS Logo">-<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ47Ji1yhUawSLNBXPp8UERlP7nKo3d1f2EKw&s" width="80" alt="AWS Logo">- 
    <img src="edn.png" width="210" alt="Second Image">
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

<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/VPC-Default.png?raw=true">-
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/VPC-Route-Tables.png?raw=true" width="400" alt="AWS Logo">- 
<img src="https://github.com/oalifiralph/Laboratorio-Auto-Scaling-ALB/blob/main/Note-pad.png" width="400" alt="AWS Logo">-

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
3. Salve as configurações.

📸 **Print do Security Group:** 

<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/create_security_group_01_basic%20details.jpg?raw=true">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/create_security_group_02_inboundRoules.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/create_security_group_03_outbound_padr%C3%A3o.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/create_security_group_04_sucess.jpg?raw=true" width="400" alt="AWS Logo">-

---
    
