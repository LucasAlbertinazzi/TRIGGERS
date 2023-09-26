## Trigger e Função de Trigger em PostgreSQL
A seguinte função de trigger e trigger foram criadas para monitorar eventos `INSERT` e `UPDATE` na tabela `tbl_analise_credito`, enviando notificações quando tais eventos ocorrem.

### 1. Função de Trigger: `att_auto_ocorrencia_app_func()`
A função `att_auto_ocorrencia_app_func()` é disparada quando um evento de trigger ocorre na tabela `tbl_analise_credito`. Ela é escrita na linguagem `plpgsql` do PostgreSQL. Segue uma descrição detalhada da função:

#### Operação `UPDATE`:
- **Quando:** Se a operação de trigger é um `UPDATE`.
- **Ação:** Envia uma notificação para o canal `att_auto_ocorrencia_app_channel` com a mensagem: `'Update na tabela tbl_analise_credito'`.

#### Operação `INSERT`:
- **Quando:** Se a operação de trigger é um `INSERT`.
- **Ação:** Envia uma notificação para o canal `att_auto_ocorrencia_app_channel` com a mensagem: `'Nova linha na tabela tbl_analise_credito'`.

#### Retorno:
- Retorna o novo registro inserido ou modificado, permitindo a conclusão bem-sucedida da operação `INSERT` ou `UPDATE`.

### 2. Trigger: `att_auto_ocorrencia_app`
A trigger `att_auto_ocorrencia_app` é disparada `AFTER INSERT OR UPDATE ON tbl_analise_credito`, significando que, para cada novo registro inserido ou registro existente atualizado nesta tabela, a trigger será acionada.

#### Ação:
- Para cada linha afetada, executa a função de trigger `att_auto_ocorrencia_app_func()`.

### Resumo
Quando um registro na tabela `tbl_analise_credito` é inserido ou atualizado, uma notificação é enviada para o canal `att_auto_ocorrencia_app_channel`, informando o tipo de operação realizada. Esta implementação é útil para monitorar mudanças na tabela e alertar outros sistemas ou usuários sobre modificações na tabela.
