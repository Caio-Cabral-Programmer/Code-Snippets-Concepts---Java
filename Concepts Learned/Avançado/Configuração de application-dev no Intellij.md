Aqui está o passo a passo organizado e mais amigável:

---

### **Configurar e Executar o Perfil `application-dev` no IntelliJ**

1. **Abrir Configurações de Execução:**
   - No IntelliJ, vá para:  
     **`Run`** → **`Edit Configurations...`**

2. **Criar Nova Configuração:**
   - Clique no sinal de **`+`** (Adicionar).
   - Selecione **`Application`**.

3. **Preencher os Detalhes da Configuração:**
   - **Nome:** `Application DEV`  
   - **JDK:** Selecione **Java 17** (versão usada no projeto).  
   - **Módulo:** Escolha o módulo principal do projeto.  
   - **Classe principal (Main class):** Aponte para a classe que contém o método `main`.  

4. **Definir Diretório e Variáveis de Ambiente:**
   - **Working directory:** Defina como o diretório raiz do projeto.  
   - **Environment variables:**  
     - Clique no sinal de **`+`** e adicione:  
       - **Name:** `SPRING_PROFILES_ACTIVE`  
       - **Value:** `dev`  

5. **Finalizar e Executar:**
   - Clique em **`Apply`** e depois em **`OK`**.  
   - Agora é só executar (**`Run`**) e acompanhar os logs de criação do banco de dados!  

---

### **Acessar o Banco H2 no Navegador (Interface Amigável)**

1. **Abrir o Console H2:**
   - No navegador, digite:  
     **`http://localhost:8080/h2-console`**  
     *(Se estiver usando Docker, substitua `localhost` por `127.0.0.1`)*.

2. **Configurar a Conexão:**
   - **JDBC URL:** Altere para `jdbc:h2:mem:sdw2023` (igual ao configurado no `datasource`).  
   - **User:** `sdw2023`  
   - **Password:** *(deixe vazio)*  

3. **Conectar:**
   - Clique em **`Connect`** (ou **`OK`**).  
   - Pronto! Você está no **Console H2** e pode visualizar e gerenciar o banco de dados facilmente.  

---

Dúvidas? Basta seguir esses passos que tudo funcionará perfeitamente! 🚀