# -Criando-Transa-es-Executando-Backup-e-Recovery-de-Banco-de-Dados


Este repositório contém scripts SQL desenvolvidos para demonstrar o controlo avançado de transações, a criação de procedimentos armazenados (*Stored Procedures*) com tratamento automático de exceções, e rotinas de backup/recovery em bases de dados relacionais utilizando o MySQL (motor InnoDB).

---

## 📂 Estrutura do Repositório

* `parte1_transacoes_simples.sql` — Scripts para controlo manual de transações, desativação de `autocommit`, uso de variáveis dinâmicas e pontos de salvamento (`SAVEPOINT`).
* `parte2_procedures_transacao.sql` — Stored Procedures com manipulação de erros (`DECLARE EXIT HANDLER FOR SQLEXCEPTION`) que executam o `ROLLBACK` automático para preservar a integridade referencial.
* `backup_ecommerce.sql` — Ficheiro de exportação contendo a estrutura de tabelas, dados e rotinas gerado via `mysqldump`.

---

## 🚀 Como Executar os Scripts

1. **Pré-requisitos:** Ter o MySQL Server e o MySQL Workbench instalados (com o motor padrão **InnoDB**).
2. **Executando a Parte 1:** Abra o ficheiro `parte1_transacoes_simples.sql` no seu cliente MySQL e execute os blocos de transação.
3. **Executando a Parte 2:** Selecione todo o bloco da procedure (delimitadores `//`) no MySQL Workbench e execute de uma só vez, em seguida execute `CALL sp_transacao_segura();`.
4. **Restaurando o Backup (Parte 3):**
   * No terminal do sistema operativo, execute o comando de importação:
     ```bash
     mysql -u root -p nome_do_banco < backup_ecommerce.sql
     ```

---

## 💡 Conceitos Aplicados
* **ACID (Atomicidade, Consistência, Isolamento e Durabilidade):** Garantidos através da gestão rigorosa de transações, commits e rollbacks.
* **Integridade Referencial:** Validação estrita entre tabelas principais (`orders`) e filhas (`ordersDetails`).
