# README_Ajax001.md

## 📌 Visão Geral

Este documento explica **linha por linha** o funcionamento de uma requisição **AJAX** utilizando o objeto nativo `XMLHttpRequest` do JavaScript. AJAX *(Asynchronous JavaScript and XML)* permite que páginas web se comuniquem com servidores em **segundo plano**, sem precisar recarregar a página inteira.

---

## 🧾 Código Completo

```javascript
function loadDoc() {
  const xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML =
      this.responseText;
    }
  };
  xhttp.open("GET", "ajax_info.txt");
  xhttp.send();
}
```

---

## 🔍 Análise Linha por Linha

---

### 🔷 Linha 1 — Declaração da Função

```javascript
function loadDoc() {
```

| Elemento | Descrição |
|---|---|
| `function` | Palavra-chave do JavaScript para **declarar uma função** |
| `loadDoc` | **Nome da função** — pode ser chamada em qualquer lugar do código, por exemplo: em um botão com `onclick="loadDoc()"` |
| `()` | **Parâmetros** — neste caso, a função não recebe nenhum argumento |
| `{` | Abre o **bloco de código** da função |

> 💡 A função encapsula toda a lógica AJAX. Nada é executado até que ela seja **chamada explicitamente**.

---

### 🔷 Linha 2 — Criação do Objeto XMLHttpRequest

```javascript
const xhttp = new XMLHttpRequest();
```

| Elemento | Descrição |
|---|---|
| `const` | **Declaração de constante** — o valor de `xhttp` não será reatribuído |
| `xhttp` | **Nome da variável** que armazenará o objeto de requisição |
| `new` | Operador que **instancia** (cria) um novo objeto na memória |
| `XMLHttpRequest()` | **Construtor nativo do browser** — cria o objeto responsável por realizar requisições HTTP assíncronas |
| `;` | Encerra a instrução |

> 💡 `XMLHttpRequest` (XHR) é a base do AJAX clássico. Ele é capaz de enviar e receber dados do servidor sem recarregar a página.

---

### 🔷 Linha 3 — Definição do Evento `onreadystatechange`

```javascript
xhttp.onreadystatechange = function() {
```

| Elemento | Descrição |
|---|---|
| `xhttp` | Referência ao objeto XHR criado anteriormente |
| `.onreadystatechange` | **Propriedade-evento** que define uma função de *callback* — ela é **disparada automaticamente** toda vez que o estado da requisição muda |
| `= function() {` | Atribui uma **função anônima** (sem nome) como manipulador do evento |

> 💡 O evento `onreadystatechange` pode ser disparado **várias vezes** durante o ciclo de vida de uma requisição (estados 0, 1, 2, 3 e 4). Por isso, a verificação interna é essencial.

---

### 🔷 Linhas 4 e 5 — Verificação de Estado e Status

```javascript
if (this.readyState == 4 && this.status == 200) {
```

| Elemento | Descrição |
|---|---|
| `if (...)` | **Estrutura condicional** — só executa o bloco se a condição for verdadeira |
| `this` | Refere-se ao **próprio objeto `xhttp`** dentro do contexto da função de callback |
| `.readyState` | **Propriedade numérica** que indica o estágio atual da requisição (ver tabela abaixo) |
| `== 4` | Verifica se `readyState` é igual a `4`, que significa **"DONE" — operação concluída** |
| `&&` | Operador lógico **E** — ambas as condições precisam ser verdadeiras |
| `.status` | **Código de resposta HTTP** retornado pelo servidor |
| `== 200` | Verifica se o servidor retornou **HTTP 200 OK** — requisição bem-sucedida |

#### 📋 Tabela de Estados `readyState`

| Valor | Constante | Significado |
|---|---|---|
| `0` | `UNSENT` | Objeto criado, `open()` ainda não foi chamado |
| `1` | `OPENED` | `open()` foi chamado |
| `2` | `HEADERS_RECEIVED` | `send()` foi chamado, cabeçalhos recebidos |
| `3` | `LOADING` | Resposta em processo de download |
| `4` | `DONE` | Operação **completamente concluída** |

#### 📋 Códigos de Status HTTP Comuns

| Código | Significado |
|---|---|
| `200` | ✅ OK — sucesso |
| `404` | ❌ Not Found — recurso não encontrado |
| `500` | ❌ Internal Server Error — erro no servidor |

---

### 🔷 Linhas 5 e 6 — Exibição da Resposta no HTML

```javascript
document.getElementById("demo").innerHTML =
this.responseText;
```

| Elemento | Descrição |
|---|---|
| `document` | Objeto global que representa o **DOM** (Document Object Model) da página |
| `.getElementById("demo")` | **Método do DOM** que localiza e retorna o elemento HTML que possui `id="demo"` |
| `.innerHTML` | **Propriedade** que define ou retorna o conteúdo HTML interno do elemento selecionado |
| `=` | Operador de **atribuição** — substitui o conteúdo atual pelo novo |
| `this.responseText` | **Propriedade do XHR** que contém o corpo da resposta do servidor como **texto puro (string)** |
| `;` | Encerra a instrução |

> 💡 O conteúdo do arquivo `ajax_info.txt` é injetado diretamente dentro do elemento `<div id="demo">` da página, sem qualquer reload.

---

### 🔷 Linhas 6 e 7 — Fechamento dos Blocos

```javascript
    }
  };
```

| Elemento | Descrição |
|---|---|
| `}` | Fecha o bloco do `if` |
| `}` | Fecha o bloco da função anônima de `onreadystatechange` |
| `;` | Encerra a instrução de atribuição da função ao evento |

---

### 🔷 Linha 8 — Configuração da Requisição (`open`)

```javascript
xhttp.open("GET", "ajax_info.txt");
```

| Elemento | Descrição |
|---|---|
| `xhttp.open()` | **Método do XHR** que inicializa/configura a requisição (mas **não a envia**) |
| `"GET"` | **Método HTTP** utilizado — `GET` é usado para **buscar/ler** dados do servidor |
| `"ajax_info.txt"` | **URL do recurso** a ser requisitado — pode ser um arquivo, endpoint de API, etc. |
| `;` | Encerra a instrução |

> 💡 O método `open()` aceita até 5 parâmetros: `open(method, url, async, user, password)`. O terceiro parâmetro `async` é `true` por padrão (requisição assíncrona).

#### 📋 Métodos HTTP mais comuns

| Método | Uso |
|---|---|
| `GET` | Buscar/ler dados |
| `POST` | Enviar/criar dados |
| `PUT` | Atualizar dados completos |
| `PATCH` | Atualizar dados parciais |
| `DELETE` | Deletar dados |

---

### 🔷 Linha 9 — Envio da Requisição (`send`)

```javascript
xhttp.send();
```

| Elemento | Descrição |
|---|---|
| `xhttp.send()` | **Método do XHR** que **dispara efetivamente** a requisição para o servidor |
| `()` | Para requisições `GET`, nenhum argumento é necessário. Em `POST`, passaria o corpo: `xhttp.send(data)` |
| `;` | Encerra a instrução |

> 💡 A partir deste momento, o browser envia a requisição de forma **assíncrona**. O código JavaScript continua sua execução normalmente, e quando a resposta chegar, o callback `onreadystatechange` será disparado.

---

### 🔷 Linha 10 — Fechamento da Função

```javascript
}
```

Fecha o bloco principal da função `loadDoc()`.

---

## 🔄 Fluxo Completo da Execução

```
1. loadDoc() é chamada
        │
        ▼
2. Cria objeto XMLHttpRequest
        │
        ▼
3. Registra o callback onreadystatechange
        │
        ▼
4. Configura a requisição com open("GET", "ajax_info.txt")
        │
        ▼
5. Envia a requisição com send()
        │
        ▼
6. Browser aguarda resposta (assincronamente)
        │
        ▼
7. Servidor responde → readyState muda para 4
        │
        ▼
8. Callback é disparado → verifica readyState == 4 && status == 200
        │
        ▼
9. Injeta responseText no elemento #demo via innerHTML
```

---

## 📦 Exemplo de Uso no HTML

```html
<!DOCTYPE html>
<html>
<body>

  <div id="demo">
    <h2>Clique no botão para carregar o conteúdo via AJAX</h2>
  </div>

  <button type="button" onclick="loadDoc()">Carregar Arquivo</button>

  <script>
    function loadDoc() {
      const xhttp = new XMLHttpRequest();
      xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
          document.getElementById("demo").innerHTML = this.responseText;
        }
      };
      xhttp.open("GET", "ajax_info.txt");
      xhttp.send();
    }
  </script>

</body>
</html>
```

---

## ⚠️ Observações Importantes

- **Política CORS**: Requisições para domínios diferentes do atual são bloqueadas pelo browser por segurança. Para arquivos locais, é necessário um servidor HTTP (como Live Server, Apache, Nginx etc.)
- **`XMLHttpRequest` vs `fetch()`**: O XHR é a abordagem **clássica** do AJAX. Atualmente, a API `fetch()` é mais moderna, baseada em Promises e considerada mais legível. Porém, o XHR ainda é amplamente utilizado e suportado.
- **`innerHTML` e XSS**: Injetar conteúdo diretamente com `innerHTML` pode ser uma vulnerabilidade de segurança *(Cross-Site Scripting)* se o conteúdo vier de fontes não confiáveis.

---

## 📚 Referências

- [MDN Web Docs — XMLHttpRequest](https://developer.mozilla.org/pt-BR/docs/Web/API/XMLHttpRequest)
- [W3Schools — AJAX Introduction](https://www.w3schools.com/xml/ajax_intro.asp)
- [MDN — readyState](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/readyState)
- [MDN — HTTP Status Codes](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status)

---

*Documentação gerada para fins didáticos — Análise e Desenvolvimento de Sistemas.*
