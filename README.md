Perfeito 🚀
Li o documento que você me enviou e preparei um **README.md** para o seu GitHub baseado nele. O conteúdo foca em apresentar os **padrões de desenvolvimento** do projeto no Dynamics 365 F\&O, de forma clara, organizada e com exemplos.

Aqui está uma primeira versão:

---

# 📘 GSWord 2.0 – Padrões de Desenvolvimento

Este repositório documenta os **padrões de desenvolvimento utilizados no Microsoft Dynamics 365 for Finance and Operations (D365FO)** no contexto do projeto **GSW**.
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

## 👨‍💻 Autor

**Thiago Miranda dos Santos**
📧 [thiago.santos@gsw.com.br](mailto:thiago.santos@gsw.com.br)

---

👉 Esse README pode ser usado diretamente no GitHub para documentar o repositório do projeto GSWord.

---

Você gostaria que eu já **estruturasse o README em Markdown pronto** (com cabeçalhos, tabelas e blocos de código), para você só colar no repositório, ou prefere que eu faça um modelo **mais resumido e executivo** (como um guia rápido de referência)?
