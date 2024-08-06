# Projeto de Cadastro de Produtos
## Visão Geral
Este projeto é um sistema de cadastro de produtos desenvolvido em PHP. Ele permite o gerenciamento de categorias, marcas e produtos, bem como a visualização de um carrinho de compras e o resumo de pedidos. Abaixo, estão listados os principais arquivos PHP utilizados no projeto, juntamente com exemplos auxiliares de uso.
# Arquivos e Métodos
1. ``carrinho.php``  
Este arquivo exibe a página do carrinho de compras.  <br>
*Exemplo de Uso:*<br>
```
require_once('controller/carrinho-busca.php');
```
2. ``categoria.php``<br>
Este arquivo exibe o formulário para cadastro de novas categorias.<br>
*Exemplo de Uso:*<br>

```
<form action="insere-categoria.php" method="post">
    <label for="">Descrição:</label>
    <input type="text" name="descricao">
    <input type="submit" value="Cadastrar">
</form>
```
3. ``index.php``<br>
Este arquivo exibe a página inicial, onde os produtos cadastrados são listados.<br>
*Exemplo de Uso:*<br>
```
require_once('controller/produtos-busca.php');
```
4. ``insere-categoria.php``<br>
Este arquivo processa o formulário de cadastro de novas categorias e insere os dados no banco de dados.<br>
**Métodos Utilizados:**
* include('controller/conexao.php');
* $_POST['descricao'];
* mysqli_query($mysqli, $cad_categoria);
* mysqli_error($mysqli);
* mysqli_close($mysqli);<br>
<br>
*Exemplo de Uso:*<br>

```g
$descricao = $_POST['descricao'];
$cad_categoria = "INSERT INTO categoria(DESCRICAO) VALUES ('$descricao')";
if (mysqli_query($mysqli, $cad_categoria)) {
    echo "<h1>Categoria cadastrada com sucesso!</h1>";
} else {
    echo "Erro: " . $cad_categoria . "<br>" . mysqli_error($mysqli);
}
mysqli_close($mysqli);
```

5. ``insere-marca.php``
Este arquivo processa o formulário de cadastro de novas marcas e insere os dados no banco de dados. <br> <br>
**Métodos Utilizados:**<br>

* include('controller/conexao.php');
* $_POST['descricao'];
* mysqli_query($mysqli, $cad_marca);
* mysqli_error($mysqli);
* mysqli_close($mysqli);<br>

*Exemplo de Uso:*<br>

```
$descricao = $_POST['descricao'];
$cad_marca = "INSERT INTO marca(DESCRICAO) VALUES ('$descricao')";
if (mysqli_query($mysqli, $cad_marca)) {
    echo "<h1>Marca cadastrada com sucesso!</h1>";
} else {
    echo "Erro: " . $cad_marca . "<br>" . mysqli_error($mysqli);
}
mysqli_close($mysqli);
```

6. ``insere-produto.php``<br>
Este arquivo processa o formulário de cadastro de novos produtos e insere os dados no banco de dados.<br>

**Métodos Utilizados:**<br>

* include('controller/conexao.php');
* $_POST['seleciona_categoria'];
* $_POST['seleciona_marca'];
* $_POST['nome'];
* $_POST['descricao'];
* $_POST['estoque'];
* $_POST['preco'];
* mysqli_query($mysqli, $grava_produto);
* mysqli_affected_rows($mysqli);<br>

*Exemplo de Uso:*
```
$categoria = $_POST['seleciona_categoria'];
$marca = $_POST['seleciona_marca'];
$nome_produto = $_POST['nome'];
$descricao = $_POST['descricao'];
$estoque = $_POST['estoque'];
$preco = $_POST['preco'];

$grava_produto = "INSERT INTO produtos(`IDCATEGORIA`, `IDMARCA`, `NOME`, `DESCRICAO`, `ESTOQUE`, `PRECO`) VALUES ('$categoria','$marca','$nome_produto','$descricao','$estoque','$preco')";

$result_gravacao = mysqli_query($mysqli, $grava_produto);

if (mysqli_affected_rows($mysqli) != 0) {
    echo "<script type=\"text/javascript\">alert('Produto cadastrado com sucesso');</script>";
} else {
    echo "<script type=\"text/javascript\">alert('Produto não cadastrado');</script>";
}
```

7. ``marca.php``<br>
Este arquivo exibe o formulário para cadastro de novas marcas.<br>
*Exemplo de Uso:*<br>

```
<form action="insere-marca.php" method="post">
    <label for="">Marca:</label>
    <input type="text" name="descricao">
    <input type="submit" value="Cadastrar">
</form>
```
8. ``pedido.php``

Este arquivo exibe a página de resumo do pedido.<br>
*Exemplo de Uso:*
```
require_once('controller/produtos-resumo.php');
```
9. ``produtos.php``<br>
Este arquivo exibe o formulário para cadastro de novos produtos.<br>
*Exemplo de Uso:*<br>
```
<form action="insere-produto.php" method="post">
    Nome: <input type="text" name="nome"><br>
    Descrição: <input type="text" name="descricao"><br>
    Estoque: <input type="number" name="estoque"><br>
    Preço: <input type="number" name="preco" min="0.00" max="10000.00" step="0.01"><br>
    Categoria:
    <select name="seleciona_categoria">
        <option value="">selecione</option>
        <?php
            $resultado_categoria = "SELECT * FROM categoria";
            $resultadocategoria = mysqli_query($mysqli, $resultado_categoria);
            while($row_categorias = mysqli_fetch_assoc ($resultadocategoria)) { ?>
                <option value="<?php echo $row_categorias['IDCATEGORIA'] ?>">
                <?php echo $row_categorias['DESCRICAO'] ?></option>
        <?php } ?>
    </select>
    <br>
    Marca:
    <select name="seleciona_marca">
        <option value="">selecione</option>
        <?php
            $resultado_marca = "SELECT * FROM marca";
            $resultadomarca = mysqli_query($mysqli, $resultado_marca);
            while
            ($row_marcas = mysqli_fetch_assoc($resultadomarca)) { ?>
      <option value="<?php echo $row_marcas['IDMARCA'] ?>">
      <?php echo $row_marcas['DESCRICAO'] ?></option>
      <?php } ?>
    </select>
<br>
    <input type="submit" value="Cadastrar">

</form>
```
# **Como Executar o Projeto**
1. Clone o repositório do GitHub:<br>
```
git clone https://github.com/seu-usuario/seu-repositorio.git
```
2. Configure o banco de dados conforme necessário (o script de criação do banco de dados não está incluído neste README).<br>
3. Certifique-se de que o servidor web e o banco de dados estejam configurados corretamente.<br>
4. Abra o navegador e navegue até a página inicial:
``index``<br>
# <span> **Tecnologias utilizadas** </span>
[<code><img height="32" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/html/html.png" alt="HTML5"/></code>](https://developer.mozilla.org/pt-BR/docs/Web/HTML)
[<code><img height="32" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/css/css.png" alt="CSS"/></code>](https://developer.mozilla.org/pt-BR/docs/Web/CSS)
[<code><img height="32" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/javascript/javascript.png" alt="Javascript"/></code>](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript)

[<code><img height="32" src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/></code>](https://github.com/)
[<code><img height="32" src="https://img.shields.io/badge/VSCode-0078D4?style=for-the-badge&logo=visual%20studio%20code&logoColor=white" alt="VisualStudio"/></code>](https://code.visualstudio.com/)

``HTML 5:`` O HTML foi usado neste projeto para criar a estrutura e o conteúdo da página da web.

``CSS 3:`` O CSS foi usado neste projeto para estilizar e melhorar a apresentação visual da página.

``JavaScript:`` O JavaScript foi usado neste projeto para adicionar funcionalidades interativas à página.


# ✍️(◔◡◔) **Autor**

<img style="border-radius: 50%" src="https://avatars.githubusercontent.com/u/127853755?s=400&u=0258f87ad131f48ebda0ce59c807b8ef147ae6a5&v=4" width="150px">

[Danilo Felype Lima](https://github.com/DaniloFelype)

<p align="left">
  <a href="mailto:danilo87651@gmail.com" alt="Gmail">
  <img src="https://img.shields.io/badge/-Gmail-FF0000?style=flat-square&labelColor=FF0000&logo=gmail&logoColor=white&link=LINK-DO-SEU-GMAIL" /></a>
  </p>
