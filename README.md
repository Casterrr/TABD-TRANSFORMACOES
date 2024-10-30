# README - Conexão e Execução do Pentaho e Banco de Dados Oracle

Este guia fornece instruções para conectar-se à máquina remota e acessar o Pentaho e o banco de dados Oracle. Ele cobre o uso do RealVNC Viewer para acessar o Pentaho e o SQL Developer para conectar-se ao banco de dados Oracle, incluindo configurações de SSH e detalhes de conexão.

## Índice
- [Requisitos](#requisitos)
- [Passos para Abrir o Pentaho na Máquina Remota](#passos-para-abrir-o-pentaho-na-máquina-remota)
- [Passos para Conectar no Banco Oracle via SQL Developer](#passos-para-conectar-no-banco-oracle-via-sqldeveloper)
- [Configurações do SQL Developer](#configurações-do-sqldeveloper)
- [Considerações de Segurança](#considerações-de-segurança)

---

### Requisitos

1. **RealVNC Viewer** para acesso remoto.
2. **SQL Developer** para conexão com o banco Oracle.
3. **Arquivo `ifal-oracle.pem`** para autenticação SSH.

### Passos para Abrir o Pentaho na Máquina Remota

1. **Abra o RealVNC Viewer** no seu computador.
2. **Conecte-se ao IP da máquina remota**:  
   - IP e porta: `18.224.107.67:5901`
   - Senha de acesso: `tabd2024`
3. Após acessar a máquina, **abra o terminal** e navegue até a pasta /home/ubuntu e lá encontrará a pasto do Pentaho (pdi-ce-9.4.0.0-343)
4. **Execute o Pentaho** com o comando:
   ```bash
   sh spoon.sh
   ```
   **Nota**: O Pentaho já está configurado para conexão com o banco Oracle.

---

### Passos para Conectar no Banco Oracle via SQL Developer

1. **Baixe o arquivo de chave SSH (`ifal-oracle.pem`)** para o seu computador.
2. **Acesse o diretório onde o arquivo está localizado** e rode o comando SSH para configurar o túnel:
   ```bash
   ssh -i "ifal-oracle.pem" ubuntu@ec2-18-224-107-67.us-east-2.compute.amazonaws.com -L 3521:localhost:1521
   ```
   Este comando cria uma conexão SSH com a máquina remota e redireciona a porta `1521` (Oracle) para a porta local `3521`.
3. **Mantenha o terminal aberto** para garantir que o túnel permaneça ativo.

---

### Configurações do SQL Developer

Após configurar o túnel SSH, abra o SQL Developer e configure a conexão da seguinte forma:

- **Nome da Conexão**: Escolha um nome de sua preferência (ex.: `Conexão Oracle Remota`).
- **Usuário**: `system`
- **Senha**: `tabd2024`
- **Host**: `localhost`
- **Porta**: `3521`
- **SID**: `ORCL`

Salve e teste a conexão. Com o túnel ativo e as configurações corretas, a conexão ao banco Oracle deverá ser bem-sucedida.

---

### Considerações de Segurança

- **Proteja o arquivo `ifal-oracle.pem`**. Ele é essencial para o acesso via SSH e deve ser mantido seguro.
- **Feche o RealVNC Viewer e o terminal SSH** após concluir seu trabalho para garantir a segurança dos dados e do acesso à máquina remota.
- **Não compartilhe credenciais e senhas publicamente** para evitar o acesso não autorizado.

