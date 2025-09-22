# 📘 GSW_BP – Padrões de Desenvolvimento

Este repositório documenta os **padrões de desenvolvimento utilizados no Microsoft Dynamics 365 for Finance and Operations (D365FO)** no contexto do projeto **GSWord 2.0**.
O objetivo é garantir consistência, qualidade e facilidade de manutenção em todas as customizações.

---

## 📑 Sumário

1. [Regras Gerais](#-regras-gerais)
2. [Objects Naming](#-objects-naming)
3. [Tabelas](#-tabelas)
4. [Labels](#-labels)
5. [Forms](#-forms)
6. [Classes](#-classes)
7. [Comentários](#-comentários)
8. [Segurança: Privileges, Roles e Security Keys](#-segurança-privileges-roles-e-security-keys)

---

## ✅ Regras Gerais

* Todas as customizações devem ser realizadas **somente com o uso de extensions**.
* Todo código e nome de objetos deve ser escrito em **inglês**.
* Cada customização deve estar vinculada a uma **task no DevOps**.
* Estrutura do projeto deve seguir a **AOT e suas pastas**.
* **Aspas duplas** são utilizadas apenas para **labels**.
* **Não criar/atualizar tabelas em métodos `modified`**.
* **Sufixo do projeto:** `BR_GSW`.
* Nome do projeto segue o padrão: `GSWXXX` (obtido no PBI).

---

## 🏷️ Objects Naming

* Novos objetos AOT → utilizar o sufixo `BR_GSW`.

  * Exemplo: `VendInvoiceJour_BR_GSW`
* **Classes de Extension:**

  ```
  ObjetoPai + TipoAbreviado + _BR_GSW_Extension
  ```

  * Exemplo: `CustTableTbl_BR_GSW_Extension`

Abreviações:

* Tabelas → `tbl`
* Classes → `cls`
* Forms → `form`

### Nomenclaturas em Forms

* DataSource → `FormDS_<DataSourceName>`
* DataSource Field → `FormDsf_<DataSourceName>_<fieldName>`
* Control → `FormCtrl_<ControlName>`

---

## 🗄️ Tabelas

* Criar sempre **Primary e Clustered Index**.
* Adicionar **Relations** com `delete actions`.
* Criar **Field Groups** → obrigatoriamente `Overview`.
* Nome e campos com **Labels**.
* Utilizar **cache** em métodos `display`.
* Métodos padrões: ex. `find`.
* Extensions devem ter sufixo:

  * Campo: `CreditLimitPeriod_BR_GSW`
  * Index: `CreditLimitPeriodIdx_BR_GSW`

---

## 📝 Labels

* Único arquivo de labels: `Application_BR_GSW`.
* Labels em **PT-BR** e **EN-US**.
* Descrição da label deve conter o **código do desenvolvimento (ex: GSW001)**.
* Antes de criar, verificar se já existe label padrão.
* ID da label deve seguir lógica clara:

  * Exemplo: *Conta de Cliente* → `CustomerAccount`.

---

## 🖼️ Forms

* Sempre utilizar **Form Pattern**.
* Evitar lógica de negócio em Forms → usar **Tabelas/Classes**.
* Lookups customizados devem ser feitos na **tabela de referência**.
* Definir `Title Data Source` e `Caption` corretamente.
* Para telas com grande volume de dados → consultar o arquiteto.

---

## ⚙️ Classes

* **Construtores antigos (switch)** são obsoletos → usar `Attributes` e `Factories`.
* Método `main` não deve conter regra de negócio, apenas gatilho.
* Controlar transações com `ttsBegin/ttsCommit/ttsAbort`.
* Sempre que possível usar **try/catch**.
* Para processos em lote → usar `SysOperation`.

---

## 💬 Comentários

* Classes novas → bloco de comentários padrão:

  ```csharp
  /// <summary>
  /// Extension class for <c>MarkupTrans</c> table.
  /// </summary>
  /// <remarks>
  /// 2025.09.22 – GSW001 – devname – Class created
  /// </remarks>
  ```

* Métodos → sempre documentados:

  ```csharp
  /// <summary>
  /// This method will start the integration process
  /// </summary>
  /// <params>
  /// Vendor Id – Supplier/Vendor identification
  /// </params>
  /// <remarks>
  /// 2025.09.22 – GSW001 – Vendor Integration – devname – Created class
  /// </remarks>
  public void processIntegration(VendorId _vendorId)
  ```

* Comentários em bloco:

  ```csharp
  //<GSW - 2025.09.22 – GSW001 – devName >
  Código...
  //</GSW>
  ```

* Comentários de linha:

  ```csharp
  Código... //<2025.09.22 – GSW001 – devName >
  ```

---

## 🔐 Segurança: Privileges, Roles e Security Keys

A gestão de segurança segue os padrões do D365FO para garantir **segregação de funções** e **controle de acesso adequado**.

### 🔑 Security Keys

* Toda nova funcionalidade que envolva acesso deve ser vinculada a uma **Security Key**.
* Nome da Security Key deve seguir o padrão:

  ```
  <Funcionalidade>_BR_GSW_Sk
  ```

  Exemplo: `VendorIntegration_BR_GSW_Sk`.

### 📜 Privileges

* Cada operação (Ex.: Criar, Editar, Consultar, Excluir) deve estar associada a um **Privilege**.

* Nome do privilege deve seguir o padrão:

  ```
  <Funcionalidade>_<Ação>_BR_GSW_Priv
  ```

  Exemplo: `VendorIntegration_Create_BR_GSW_Priv`.

* Os **Privileges** devem conter referências a:

  * Menus
  * Botões de ação
  * Serviços ou classes relevantes

### 👤 Roles

* Criar **Roles** agrupando os privileges necessários para determinada função.

* Nome da Role deve seguir o padrão:

  ```
  <ÁreaNegócio>_<Funcionalidade>_BR_GSW_Role
  ```

  Exemplo: `AP_VendorIntegration_BR_GSW_Role`.

* Roles nunca devem conter permissões diretas → apenas **Privileges**.

### 📝 Boas práticas

* Manter consistência nos nomes.
* Documentar no **DevOps task** os privilégios criados.
* Sempre validar com o time de segurança/arquitetura antes de liberar em produção.

---

## 👨‍💻 Autor

**Thiago Miranda dos Santos**
📧 [thiago.santos@gsw.com.br](mailto:thiago.santos@gsw.com.br)

---

👉 Agora o README inclui também a parte de **segurança (privileges, roles e security keys)**.

Quer que eu monte também **exemplos em XML/metadata do AOT** (como ficariam os `Privileges` e `Roles` criados no código), ou prefere manter o README apenas como guia de boas práticas?
