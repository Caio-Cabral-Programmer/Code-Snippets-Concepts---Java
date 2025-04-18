### **Configurar e Executar o Perfil `application-prd` no IntelliJ**  

#### **Passo 1: Criar ou Duplicar a Configuração de Execução**  
1. No **IntelliJ**, vá para:  
   **`Run`** → **`Edit Configurations...`**  
2. Clique no **`+`** (Adicionar) → Selecione **`Application`** *(ou duplique uma configuração existente e renomeie)*.  
3. Preencha os seguintes campos:  
   - **Name:** `Application PRD`  
   - **JDK:** Selecione **Java 17** (versão usada no projeto).  
   - **Module:** Escolha o módulo principal do projeto.  
   - **Main class:** Aponte para a classe que contém o método `main`.  
   - **Working directory:** Defina como o diretório raiz do projeto.  

---

#### **Passo 2: Configurar as Variáveis de Ambiente**  
Adicione as seguintes variáveis (**`+`** em *Environment variables*):  

| **Variável**         | **Valor (Exemplo)**                | **Observação**                          |  
|-----------------------|------------------------------------|-----------------------------------------|  
| `SPRING_PROFILES_ACTIVE` | `prd`                             | Ativa o perfil de produção.             |  
| `PGHOST`              | `[endereço-do-servidor-postgres]`  | Host do PostgreSQL (Railway/outro).     |  
| `PGPORT`              | `[porta]`                         | Porta do banco (ex: `5432`).            |  
| `PGDATABASE`          | `[nome-do-banco]`                 | Nome do banco de dados.                 |  
| `PGUSER`              | `[usuário]`                       | Usuário com acesso ao banco.            |  
| `PGPASSWORD`          | `[senha]`                         | Senha do banco (Railway/outro).         |  

*(Substitua `[valor]` pelos dados fornecidos pelo **Railway** ou seu provedor de banco de dados.)*  

---

#### **Passo 3: Executar a Aplicação**  
- Clique em **`Apply`** → **`OK`**.  
- Execute (**`Run`**) e acompanhe os logs para verificar a conexão com o banco de dados.  

✅ **Pronto!** A aplicação está rodando no modo **produção (`prd`)** com as configurações do PostgreSQL.  

---

### **Dicas Importantes**  
🔹 **Railway/Outros Provedores:**  
   - As variáveis `PGHOST`, `PGPORT`, etc., são fornecidas no painel do serviço (ex: Railway, AWS RDS, etc.).  
   - Certifique-se de que a conexão externa está liberada (firewall, permissões, etc.).  

🔹 **Segurança:**  
   - Nunca commit **senhas** ou dados sensíveis no código! Use variáveis de ambiente ou um gerenciador de secrets.  

🔹 **Problemas comuns?**  
   - Verifique se o **PostgreSQL está acessível** (telnet/ferramentas como DBeaver).  
   - Confira se as **portas e credenciais** estão corretas.  

Se tudo estiver configurado corretamente, a aplicação se conectará ao banco de dados em produção! 🚀